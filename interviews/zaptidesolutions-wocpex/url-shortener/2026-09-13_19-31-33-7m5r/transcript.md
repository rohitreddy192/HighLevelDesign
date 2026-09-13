# Design a URL Shortener — Interview Transcript

**Round:** HLD · **Difficulty:** Easy · **Date:** 2026-09-13 · **Duration:** 5m 33s

## Problem

Design a URL shortening service like TinyURL or Bit.ly. Users submit a long URL and receive a short URL; visiting the short URL redirects to the original. Walk me through the requirements, the API, the data model, how you generate short codes, and how you would scale reads.

---

**Interviewer:** Let's dive into the requirements for designing a URL shortening service. Describe what you believe the system should be able to do and what constraints it might have.

**You:** Okay. In my idea I'm thinking of understanding the estimate or the scale of users first.

I'm thinking that the shortner is like we have the url and we shorten it and when user sees user will see the shortened url and when clicked he will be re-directed to the original url right??

**Interviewer:** Exactly! That's the core functionality. The system accepts a long URL and returns a short URL. When the user visits the short URL, it should redirect to the original URL. To clarify, what do you think the system should be able to do with multiple inputs, such as different users submitting the same long URL? How would the system keep track of all these URLs?

**You:** So can different users submit the same url?? If they do so then its nothing different and they ppl will access the same thing so it wont be an issue. We can assume they all be the same.  If the user tries to do so we will check for the url in url_links that are there not the shortened ones but the long urls and then we will just return the short url for it than just doing the short url for it. 

We will have a key value store for shortend_url => long_url so get(short_url) takes very short time.

**Interviewer:** Got it. It appears that you're suggesting checking the original long URLs in a separate database to handle duplicates. Is there a reason to keep a separate database for storing the original URLs, or would a single database suffice for everything? How would you handle scaling the long URL database?

**You:** No we wont keep seperate database we will have the same kv store to do this for us

**Interviewer:** Understood. So you're proposing using a single key-value store that maps the short URL to the long URL and vice versa. How would you ensure that the storage is resilient and can handle high read-to-write ratios? What kind of caching layer might be necessary to improve read performance? And what about the generation of a unique short code for each long URL?

**You:** Sure we can delve into it as well.

**Interviewer:** 
