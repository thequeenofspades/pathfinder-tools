<a href="http://interactjs.io"><img alt="interact.js" src="https://c4d6f7d727e094887e93-4ea74b676357550bd514a6a5b344c625.ssl.cf2.rackcdn.com/ijs-anim.svg" height="131px" width="100%"></a>

JavaScript drag and drop, resizing and multi-touch gestures with inertia and
snapping for modern browsers (and also IE8+).

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/taye/interact.js)

Features include:

 - **inertia** and **snapping**
 - **multiple interactions**
 - cross browser and device, supporting the **desktop and mobile** versions of
   Chrome, Firefox and Opera as well as **Internet Explorer 8+**
 - interaction with [**SVG**](http://interactjs.io/repo/demo/star.svg) elements
 - being **lightweight and standalone** (not _yet another_ jQuery plugin)
 - **not modifying the DOM** except to support IE8 and to change the cursor
   (but you can disable that)

Installation
------------

* [Bower](http://bower.io/): `bower install interact`
* [npm](https://www.npmjs.org/): `npm install interact.js`
* Direct download the latest version: http://interactjs.io/#download
* [jsDelivr CDN](http://www.jsdelivr.com/#!interact.js): `<script src="//cdn.jsdelivr.net/interact.js/1.2.6/interact.min.js"></script>`
* [cdnjs CDN](https://cdnjs.com/libraries/interact.js): `<script src="//cdnjs.cloudflare.com/ajax/libs/interact.js/1.2.6/interact.min.js"></script>`
  (replace `VERSION` with the SemVer you want to use)

Documentation
-------------

Visit http://interactjs.io/docs for the API documentation.

Example
-------

```javascript
var pixelSize = 16;

interact('.rainbow-pixel-canvas')
  .origin('self')
  .draggable({
    snap: {
        targets: [ interact.createSnapGrid({
          x: pixelSize, y: pixelSize
        }) ]
    },
    // allow multiple drags on the same element
    maxPerElement: Infinity
  })
  // draw colored squares on move
  .on('dragmove', function (event) {
    var context = event.target.getContext('2d'),
        // calculate the angle of the drag direction
        dragAngle = 180 * Math.atan2(event.dx, event.dy) / Math.PI;

    // set color based on drag angle and speed
    context.fillStyle = 'hsl(' + dragAngle + ', 86%, '
                        + (30 + Math.min(event.speed / 1000, 1) * 50) + '%)';

    // draw squares
    context.fillRect(event.pageX - pixelSize / 2, event.pageY - pixelSize / 2,
                     pixelSize, pixelSize);
  })
  // clear the canvas on doubletap
  .on('doubletap', function (event) {
    var context = event.target.getContext('2d');

    context.clearRect(0, 0, context.canvas.width, context.canvas.height);
  });

  function resizeCanvases () {
    [].forEach.call(document.querySelectorAll('.rainbow-pixel-canvas'), function (canvas) {
      canvas.width = document.body.clientWidth;
      canvas.height = window.innerHeight * 0.7;
    });
  }

  // interact.js can also add DOM event listeners
  interact(document).on('DOMContentLoaded', resizeCanvases);
  interact(window).on('resize', resizeCanvases);
```

See the above code in action at http://codepen.io/taye/pen/YPyLxE

License
-------

interact.js is released under the [MIT License](http://taye.mit-license.org).

[ijs-twitter]: https://twitter.com/interactjs
[upcoming-changes]: https://github.com/taye/interact.js/blob/master/CHANGELOG.md#upcoming-changes
