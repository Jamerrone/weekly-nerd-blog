[Back <](../README.md) | [Part 1 <](./article-3.md)

# Article 4/5: Service Worker the Basic part 2

This is the fourth article of a short blog series where I will be sharing my experience, interesting findings and much more about frontend development. This series is part of an assignment for my “Everything Web” Minor course. I really hope you guys enjoy reading it as much as I enjoyed writing it.

Previous week you guys learned about service workers, what they are, what you can accomplish with them and how to set one up yourself. Today we will be focussing pretty much on code only. You will learn how you can cache files and web pages for offline support and I will be sharing some resources where you can find more information about this new API. Take your time reading through this article, it will get quite technical and sometimes quite complicated. If something is not working as expected or if you do not understand a concept, please make sure you read it over or search for help online. Just copying everything will not teach you anything, it is very important that you actually understand what you are doing.

## Caching Files

The first thing we need to do is to declare with files we always want to cache. This can be anything we rely on, for example, CSS files, HTML files, and even web-fonts. These files are generally local files hosted by your own server. You can, however, also cache files from external servers, for example, Google fonts or API responses.

In order to do this, we will need to update our `./service-worker.js` file.

**service-worker.js**

```javascript
const cacheVersion = 'v1.0.0';
const filesToCache = ['./', './index.html', './css/main.css', './img/some-image.png'];

self.addEventListener('install', e => {
  console.log('[SW]: Installed');
  e.waitUntil(caches.open(cacheVersion).then(cache => {
    console.log('[SW]: Caching files...');
    return e.cache.addAll(filesToCache);
  }));
});

...
```

The `cacheVersion` constant is just a name, you can name it whatever you feel like. I myself prefer to give them version numbers so I know if the current cache is up to date or not. The `filesToCache` array is a list containing all the files we want to cache. For now, we will be caching the root, our HTML file, and our CSS file. `e.waitUntil` forces the install event to wait until our cache promise is resolved.

All we need to do inside this code block is to open the current cache and save the files we want inside of it. In our case, the cache is named `v1.0.0` and the files we want to cache can be found inside our previously defined array. You can now check your browser’s console for the `'[SW]: Caching files...'` message indicating everything is working as expected.

## Nice! This is working now, but how can I clear my old cache in case of an update?

Good question! Before I actually explain you how to clear your old cache, let me first explain why you should want to do this. Let’s say you updated some files and changed the current cache version/name to `v1.5.0`. Everything will be working fine as you expect, however, the previous cache version `v1.0.0` will still be saved inside your user's device. In order to keep our service worker as clean and small as possible, we should delete/clear our previous unused `v1.0.0` cache.

**service-worker.js**

```javascript
...

self.addEventListener('activate', e => {
  console.log('[SW]: Activated');
  e.waitUntil(caches.keys().then(cacheVersions => {
    return Promise.all(cacheVersions.map((cache) => {
      if (cache !== cacheVersion) {
        console.log('[SW]: Removing old cache files...');
        return caches.delete(cache);
      }
    }))
  }));
});

...
```

Essentially this code is just looping through the entire cache from our service worker and deleting any cached files from a previous version. You can now rename your `cacheVersion` to something else then `v1.0.0` and see a message in the browser’s console saying that it is deleting old cached files.

You can now cache anything you want, update your cached files and clean/remove your old unused files! There is one more thing I want to go through with you guys, handling fetch requests.

## Caching fetch requests

If you ever want to cache a file from an API or external source you will need to use the fetch event handler. For this example, I suggest you guys to fetch an image from any API using the XHTML method. If this sounds too complicated you can test this technique by importing an external font, for example, a Google font.

**service-worker.js**

```javascript
...

self.addEventListener('fetch', e => {
  console.log('[SW]: Fetching ', e.request.url);
  e.respondWith(caches.match(e.request).then((response) => {
    if (response) {
      console.log('[SW]: Found in cache: ', e.request.url);
      return response;
    }
    const requestClone = e.request.clone();
    fetch(requestClone).then((response) => {
      if (!response) { return response; }
      const responseClone = response.clone()
      caches.open(cacheVersion).then(cache => {
        cache.put(e.request, requestClone);
        return response
      });
    });
  }))
});
```

This code checks if the request is already saved in our current cache or not. If the file is already cached it will simply respond with the cached file. If the file is not cached, it will make the request as normal. You may have noticed that we also clone the original request and response. We need to do this because we cannot use the same one twice.

## Resources and conclusion

Bellow, you can find a list of resources used in this article where you can find more in-depth information and techniques about service workers. Keep in mind that what you learned in the past two weeks is a very small portion of what you can accomplish with this API. There is a lot more to learn but these two articles are a good starting point for most beginners.

- [Service Workers: an Introduction  |  Web Fundamentals  |  Google Developers](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [Service Worker API - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
- [Making A Service Worker: A Case Study — Smashing Magazine](https://www.smashingmagazine.com/2016/02/making-a-service-worker/)
- [Introduction to Service Workers - YouTube](https://www.youtube.com/watch?v=jVfXiv03y5c)

I really hope you guys found this article somewhat useful or at least entertaining. This was it for today's article, and I really hope to see you guys next week. Take care!

[Back <](../README.md) | [Part 1 <](./article-3.md)
