# Satisfy that selector!

***Satisfy*** is a stand-alone (no dependencies) JavaScript function for generating HTML from CSS selectors. It's incredibly simple.

This:

```js
satisfy('div a');
```

Returns the following DOM structure:

```js
<div>
    <a></a>
</div>
```

You can use attribute selectors and a numerical psuedo-class to manipulate the produced structure further:

```js
satisfy('ul li:5 span[innerHTML="item"]');
```

And that would produce this:

```html
<ul>
    <li><span>item</span></li>
    <li><span>item</span></li>
    <li><span>item</span></li>
    <li><span>item</span></li>
    <li><span>item</span></li>
</ul>
```

And sibling combinators (note: `~` and `+` do the same thing in this context):

```js
staisfy('div span + a');
```

Output:

```html
<div>
    <span></span>
    <a></a>
</div>
```

**Note: `satisfy()` returns a NodeList containing the elements you want. It's not a *real* array.**

### Other minor features

You can set a boolean property with a no-value attribute expression (Thanks to [Kangax](http://twitter.com/kangax/status/13569875690)):

```js
satisfy('input[type=checkbox][checked]');
satisfy('audio[autoplay]');
```

You can also set an element's `innerHTML` like so:

```js
satisfy('div a[innerHTML=blah]');
// or:
satisfy('div a[html=blah]);
```
    
It's also possible to set multiple classes:

```js
satisfy('a.b.c.d'); // => <a class="b c d"></a>
```

### jQuery

If you're using jQuery then you can use ***Satisfy*** like so:

```js
jQuery.satisfy('div a:5').prependTo('body');
```
    
`jQuery.satisfy` returns a jQuery instance containing all of the elements produced from whatever selector you pass to it. This makes it possible to use any of jQuery's methods... So, instead of:

```js
jQuery('<div><a/></div>').appendTo(foo);
```
    
... you can do:

```js
jQuery.satisfy('div a').appendTo(foo);
```

### Improvements in 0.3

I re-wrote most of the code in 0.3. The mechanism now used for creating elements is mostly fragment-based and the selector is processed in reverse.
