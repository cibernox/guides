Ember CLI by default uses [Babel.js](https://babeljs.io/) to allow you to use tomorrow's javascript, today.

It will ensure that you can use the newest features in the language and know that they will be transformed to javascript that can run in every browser you support.
That usually meant generating ES5 compatible code that can work on any modern browser, back until Internet Explorer 9.

But ES5 code is usually more verbose than the original javascript, and with time, as browsers gain the ability to execute the new features in javascript and older browers loose users, many users don't really need want this verbose code increasing their app's size and load times.

That is why Ember CLI exposes a way of configuring what browsers your app targets, and it can figure out automatically what features are natively supported by all the browsers you support and apply the minimum set of transformations possible to your code.

If you open the `config/targets.js` you will find this code:

```config/targets.js
module.exports = {
  browsers: [
    'ie 9',
    'last 1 Chrome versions',
    'last 1 Firefox versions',
    'last 1 Safari versions'
  ]
};
```

That default configuration matches the wider set of browsers that Ember.js itself supports, but if your app, per example, doesn't support IE anymore, you can change it to

```config/targets.js
module.exports = {
  browsers: [
    'last 1 edge versions',
    'last 1 Chrome versions',
    'last 1 Firefox versions',
    'last 1 Safari versions'
  ]
};
```

With this change, since all those browsers have full ES6 and ES2016 support, if you check the transpiled code, you will see that it no longer tanspiles features like arrow functions.

This feature is backed by [Browserlist](https://github.com/ai/browserslist) and [Can I Use](http://caniuse.com/), which track usage stats of browsers, so you can use complex queries based
on the userbased of every browser.


P.e, you want to target all browsers with more than a 4% market share in Canada.

```config/targets.js
module.exports = {
  browsers: [
    '> 4% in CA'
  ]
};
```

It is very important that you properly configure the targets of your app correctly so you get
the smallest and fastest code possible.

Build Targets can also be leveraged in other ways. Some addons might conditionally include polyfills only if needed, some linters may emit warnins when using features not yet fully supported in your targets, or automatically prefix unsupported CSS properties.



