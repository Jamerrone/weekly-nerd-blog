[Back <](../README.md) | [Part 2 >](/article-4.md)

# Article 3/5: Service Worker the Basic part 1

This is the third article of a short blog series where I will be sharing my experience, interesting findings and much more about frontend development. This series is part of an assignment for my “Everything Web” Minor course. I really hope you guys enjoy reading it as much as I enjoyed writing it.

Today’s article is actually split into two different parts, you guys can expect part 2 next week. During this two parts article, we will be taking a look at the “Service Worker” API, our most complicated and advanced topic so far. While this technology is new and not well supported, it can be very powerful in the right hands. However, we developers need to use this technology wisely as it is very easy to abuse users with it.

## Service Worker? What are you even talking about?

“Service workers essentially act as proxy servers that sit between web applications, the browser, and the network (when available). They are intended, among other things, to enable the creation of effective offline experiences, intercept network requests and take appropriate action based on whether the network is available, and update assets residing on the server. They will also allow access to push notifications and background sync APIs.” — MDN Web Docs

Service workers are basically scripts that run independently from the webpage itself. With normal JavaScript, you can as you know interact with the DOM tree. Services workers, on the other hand, cannot interact with the DOM what so ever. Instead of DOM manipulation service workers focus on things like background sync, push notifications, fetch requests and resource caching.

Because service workers run on different threads than your normal client-side JavaScript they are not blocking and are fully async. This, however, means that API's like localStorage does not work inside service workers at all.

## Sounds nice, but what can we accomplish using this technology?

There are actually a lot of things you can accomplish using this technology, there is almost no limit to it. Bellow, you can find a small list with examples that you can accomplish using this new API.

- Full offline support
- Push notifications
- Differential update of text files
- Capability and feature detection
- Support for new image types
- Client-side load balancing
- Generally faster requests handling
- Background synchronization

And this is just the start, your creativity is your only limitation. Like I said before, this new technology can be extremely useful and powerful, however, it is also easily abused. It can for example cache gigabytes of data on your device, slowing it down. As this technology gets more mature, I really hope they limit it’s “usefulness”.

Service workers are, however, not perfect. The cached data can actually be deleted at any time by any user or sometimes even randomly by the browser. This is rarely an issue, but it is something to keep in mind when developing your next offline web app.

## Let’s get started!

Let’s start by creating the necessary files and folder structure. If you are planning on following my guidance step by step I highly recommend that you rebuild the exact same folder structure used in this tutorial.

- ./js/app.js
- ./img/some-image.png
- index.html
- service-worker.js

The image can be anything of your own choice and of any type.

**index.html**

```html
<body>
    <h1>Service Worker - Demo</h1>
    <p>Asymmetrical tbh leggings ethical, flexitarian mumblecore church-key pickled gluten-free.</p>
  <img src="./img/some-image.png"></img>
  <script src="./js/app.js"></script>
</body>
```

Next, we need to register our service worker. In the `./js/app.js` file write the following code:

**app.js**

```javascript
if ('serviceWorker' in navigator) {
  navigator.serviceWorker
    .register('./service-worker.js', { scope: './' })
    .then(registration =>
      console.log('Service Worker was successfully registered.')
    )
    .catch(error =>
      console.log('There was an error registering the Service Worker: ', error)
    );
}
```

As you can see we are using feature detection just like in the last article. The scope option is not required as the standard value is `./`. If everything is working you should see the following message in your browser’s console: `Service Worker was successfully registered.`. If this is not what you see, please make sure that you followed each step with attention and try to fix any differences.

Next, we will create the needed event listeners inside our `./service-worker.js` file. Just like before make sure every character is the same as the code below:

**service-worker.js**

```javascript
self.addEventListener('install', e => console.log('[SW]: Installed'));

self.addEventListener('activate', e => console.log('[SW]: Activated'));

self.addEventListener('fetch', e =>
  console.log('[SW]: Fetching ', e.request.url)
);
```

The `[SW]` inside the console log messages is so we can see the difference between log messages from the app vs log messages from the service worker itself. Just to make our debug live a bit easier.

## Can we finally start doing something useful? Please…

Well yes, but not today! Next week we will finish this tutorial and you will learn how to actually use your newly created service worker. Today you learned what service workers are, what you can do with them and how to set one up yourself.

Next week we will be focusing much more on code and practical examples. You will learn how to cache your files and where to find more information about this topic.

I really hope you guys found this article somewhat useful or at least entertaining. This was it for today's article, and I really hope to see you guys next week. Take care!

## Resources
* [Service Workers: an Introduction  |  Web Fundamentals       |  Google Developers](https://developers.google.com/web/fundamentals/primers/service-workers/)
* [Service Worker API - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
* [Making A Service Worker: A Case Study — Smashing Magazine](https://www.smashingmagazine.com/2016/02/making-a-service-worker/)
* [Introduction to Service Workers - YouTube](https://www.youtube.com/watch?v=jVfXiv03y5c)

[Back <](../README.md) | [Part 2 >](/article-4.md)
