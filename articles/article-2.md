[Back <](../README.md)

# Article 2/5: Feature detection

This is the second article of a short blog series where I will be sharing my experience, interesting findings and much more about frontend development. This series is part of an assignment for my “Everything Web” Minor course. I really hope you guys enjoy reading it as much as I enjoyed writing it.

Today we will be focussing on two major topics. First I will talk a bit about browser support and _"feature detection"_. Secondly, I will be explaining how to import or _"fetch"_ the content from an HTML file into another one. While these topics may sound nonrelated, they are actually depended on each other. You will understand it soon enough. Fetching content from another file can be very helpful for us developers, while also providing a better and faster experience for our users.

## What is feature detection anyway?

"Feature detection involves working out whether a browser supports a certain block of code, and running different code dependent on whether it does (or doesn't), so that the browser can always provide a working experience rather crashing/erroring in some browsers." — [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Feature_detection)

In other words, Feature Detection is the art of detecting whether a given browser supports a feature we want to use or not. In case it doesn't, we may choose to provide an alternated option, also called the fallback. We can also choose to skip the nonsupported feature altogether.

### Example:

```javascript
if (!('open' in document.creatElement('details'))) {
  // Do something here...
}
```

The example above will only execute the code inside the if-statement if the browser supports the "details" HTML element. The technic used here can be applied in most cases, all you need to know is a unique property from the element you want to check.

**Explaining the code:**

- First, we create a new "details" element.
- Next, we check if the newly created element has the "open" property.
- If the browser does not support the "details" element this will return false.
- We only want to execute the code above if the browser supports the element, so we wrap the if-statement inside the not (!) operator.

## Why should we want to use Feature Detection?

Let’s say you read about this new cool feature on the internet. The problem is, it only works on Google Chrome, at least for now. Most likely you won’t use this feature because you need to support every major browser. You could also say, fuck it I will use it anyway. Doing so can lead to two problems. First of all, it can break your program on browsers that do not support the feature. Secondly, it means that you will need to rewrite your code whenever another browser adds support for the given feature.

Using feature detection means that you can choose to run a code block only on browsers that support the given feature. If you choose to create a fallback, you can do it quite easily inside the else-statement, however, this is not necessary. Let’s say Firefox adds support for this new feature, you won't need to update your code at all. It will simply work!

## Sounds great, but how can we do it? I really need a better example.

Fair enough. Let’s code! We are going to build a simple model using the newest and bad supported "dialog" element. Right now Google Chrome is the only browser that really supports this new feature. In case a user is using another browser, he won’t even notice anything. In the place of a "dialog", we will simply redirect the user to a new and standalone HTML page.

Given the fact that we developers don’t repeat ourselves, we will be fetching the content from the second HTML page and display it inside the modal for Chrome users.

You can find a working demo [here](https://jamerrone.github.io/browser-technologies/opdracht2/modal/).

And the GitHub repository [here](https://github.com/Jamerrone/browser-technologies/tree/master/opdracht2/modal).

Let’s start by creating the two required HTML pages. All we need is an index.html file with a single link and a lorem.html file with some paragraphs.

**index.html**

```html
<body>
  <a id="lorem" href="./lorem.html">Lorem Ipsum</a>
</body>
```

**lorem.html**

```html
<body>
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse facilisis, eros ut fringilla accumsan, sem enim posuere metus, a ullamcorper justo dolor vel arcu. Nam eu vestibulum urna, eu porta lacus. Aliquam erat volutpat. Maecenas blandit tincidunt nisi sed tristique. Donec dui turpis, euismod quis accumsan et, ultrices eget magna. Vivamus semper, dolor sit amet ultricies vulputate, quam mauris ornare dolor, vel ultricies magna massa tristique nibh. Suspendisse vestibulum, libero vel bibendum cursus, diam justo facilisis eros, et interdum enim tellus non nunc. Nullam vehicula nunc eu ante convallis auctor. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.</p>
</body>
```

Next, we will need to write some simple JavaScript.

**main.js**

```javascript
if ('open' in document.createElement('dialog')) {
  const dialog = document.createElement('dialog');
  document.getElementById('lorem').addEventListener('click', e => {
    dialog.open ? (dialog.open = false) : (dialog.open = true);
    fetch('./lorem.html')
      .then(resp => resp.text())
      .then(text => (dialog.innerHTML = text));
    document.body.appendChild(dialog);
    e.preventDefault();
  });
}
```

This is all we need! Now let me explain what is going on. Just like the details element, the dialog element also has an open property.

- Using the example I explained earlier we can check if a browser supports the dialog tag if it does we can execute our code. `const dialog = document.createElement('dialog')` will create a new dialog element and store it in memory.
- Using the following ternary operator we can toggle the open property on or off: `dialog.open ? dialog.open = false : dialog.open = true`.
- Next we can simply fetch the content from lorem.html and use its content as the innerHTML of our newly created dialog element.
- We can prevent the default behavior of links using: `e.preventDefault()`.

If the browser does not support the dialog element the code above will never execute meaning that the link will just work normally and link to the lorem.html page. This technic is simple but extremely useful when used right.

## Conclusion

I really hope you guys found this article somewhat useful or at least entertaining. This was it for today's article, and I really hope to see you guys next week. Take care!
