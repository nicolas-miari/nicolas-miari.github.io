---
layout: post
title:  "Serializing Asunchronous Operations Using Closures and Private Fucntions"
date:   2015-12-01 14:47:37 +0900
categories: personal 
---

Sometimes you need to perform an asynchronous task, like downloading a file. In 
swift, closures come in very handy to perform some operation once the asynchronous
task completes. For example:

    func downloadFile(fromURL url:NSURL, completion:((error:NSError?)->()))
    {
        MyHTTPAPI.sendRequest({ response in
        
            if response.statusCode == 200 {
                // SUCCESS
                completion(error:nil)
            }
            else{
				// FAILURE:
                completion(error: response.error!)
            }
        })
    }

And some _other_ times, you need to perform _a lot_ of asynchronous tasks (like 
- for example- downloading a lot of files). We could expand the previous code
with a `for` loop, like this:


    func downloadFiles(fromURLs urls:[NSURL], completion:((error:NSError?)->()))
    {
        for url in urls {
            self.downloadFile(fromURL:url, completion:{ error in 
				if error != nil {
					completion(error:error)
					break
				}

				if url == urls.lastObject(){
					completion(error:nil)
				}
            })
        }
    }

This will loop through all the URLs and send an asynchronous request for each. The problem is, all the requests are
sent almost at the same time: Most likely, you will finish sending the last request _before_ you get the first response.
Moreover, we have setup our success trigger (`completion(error:nil)`) at the end of the completion handler of the last request. This assumes that the last request will complete last: a race condition.

A better design requires that we serialize (or enqueue) all our requests, so that they are performed one at a time.
This way, no matter how long each request takes, we can be sure that request number N+1 is sent only _after_ we received
a response to request number N. Also, we don't need to worry about our HTTP library having to deal with too many 
concurrent connections.

In a delegate-based scenario, we would have a mutable array of connection tasks serving as a queue, and dequeue them
one by one on the delegate method that is called on completion, to start the new task.

But with colsures, we have all our code on-site (no separate methods), so at first it is not clear how to "serialize"
all our downloads. However, with a clever trick we can accomplish this:

	func downloadFiles(fromURLs urls:[NSURL], completion:((error:NSError?)->()))
    {
		// [1] Define recursion:

		var mutableURLs = urls

		func downloadNext() 
		{
			if mutableURLs.count == 0 {
				// Terminating condition
				return completion(error:nil)
			}

			let url = urls.removeFirst()

			self.downloadFile(fromURL:url, completion:{error in 
				guard error == nil else {
					// Failure; abort:
					completion(error:error)
					return
				}

				// Success; recurse:
				donwloadNext()
			})
		}


		// [2] Kickstart recursion :

		donwloadNext()
    }
  

The code runs as follows:

1. We make a mutable copy of the URL array.
2. Call `downloadNext()` for the first time: the array is not empty. We remove first URL and send an asynchronous request to it.
3. Return from `downloadNext()` right away.
4. Return from `downloadFiles()` right away.
5. ...
6. On request completion, `downloadNext()` calls itself -this time, with the diminished URL array- and the
cycle goes on, until the array is empty and `downloadNext()` bails out to success.

All in all, `downloadNext()` is called N+1 times to perform N requests (the last time finds the URL array emoty and bails out).
