# Redux example
I created this repo after finding that my needs weren't addressed in the example repos out there. Unfortunately, I can't fully explain my needs due to NDA considerations, but I hope to explain enough with examples to help others who might be wondering the same types of things. I initially wrote all the code following the subjective "best practices," but I quickly found that it resulted in code that was extremely hard to follow and which required far too much type-checking, which suggested it was bad code. I decided to ignore best practices and use the redux concept without all of the ideals.

## My needs
I have a backend API that I need to communicate with and it's not RESTful, nor can it be. In short, there are many dozens of discrete endpoints; some require data, some don't. And for those that require data, it often is a subset of the data from a different call. I love what the redux team has created and decided to attempt to use it. In a bulleted list, here's what I need:
  * a means to query a particular endpoint
  * a means to identify whether or not a query is cacheable (some are stateful and can't be cached)
  * regarding caching: some calls can be cached indefinitely for the session while others would only be valid for a certain period of time
  * a means to query with data from a different call (possibly a subset of the previous call's results, so the entire response couldn't simply be passed as a parameter)

## Observations and choices (incomplete)
I noticed that the calls requiring data from a separate call are never cacheable, so I used that knowledge to create middleware that also "knew" it; meaning, the middleware doesn't perform validation and uses the action type or the presence of a particular property to indiscriminately decide what to do. I also opted to violate the standard action spec (see https://github.com/acdlite/flux-standard-action) in favor of conveniently adding properties that made my life easier.

## Other notes
I have studied much of the middleware out there but none of it completely meets my needs so I'm designing my own. That being said, I have undoubtedly written (or will write) some code that rips off someone else's idea. This is completely unintentional and I will make my best effort to credit those from whom I stole ideas. If you see anything in this repo as time goes on that is not original and deserves credit, please please please let me know.

I'll continue to update this as I progress and I hope someone finds value in it, even if that value is simply knowledge of what not to do. Considering my use-case and the fact that I can't use proprietary information, it may seem pretty bland, but I'll do my best to add tests and examples as I complete various pieces.
