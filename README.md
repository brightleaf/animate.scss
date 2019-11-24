# Animate.scss

_Just-add-water (s)CSS animation. A sass port of [Animate.css](https://daneden.github.io/animate.css/)_

`animate.scss` is a bunch of cool, fun, and cross-browser animations for you to use in your projects. Great for emphasis, home pages, sliders, and general just-add-water-awesomeness.

## Installation

Install via npm:

```bash
$ npm i @brightleaf/animate.scss
```

or yarn:

```bash
$ yarn add @brightleaf/animate.scss
```

## Usage

To use animate.scss in your website, you can either 1) simply drop the compiled stylesheet into your document's `<head>`, or you can import the sass files into your project directly. From there you can add the class `animated` to an element, along with any of the animation names. That's it! You've got a CSS animated element. Super!

```html
<head>
  <link rel="stylesheet" href="animate.min.css" />
</head>
```

If you are importing sass directly, you have two options. You can pull in the package as a whole -- including all animations -- by importing `animate.scss` from the package root:

```scss
@import "~@brightleaf/animate.scss/animate";
```

...or you can pull in animations (or animation groups) as you need them. Using this option, you'll also need to import the `settings` and `classes` files independently:

```scss
@import "~@brightleaf/animate.scss/source/settings"; // settings first!
@import "~@brightleaf/animate.scss/source/flippers"; // animation group!
@import "~@brightleaf/animate.scss/source/lightspeed/lightSpeedIn"; // individual animation!
@import "~@brightleaf/animate.scss/source/classes"; // classes!
```

### Animations

To animate an element, add the class `animated` to an element. You can include the class `infinite` for an infinite loop. Finally you need to add one of the following classes to the element:

| Class Name        |                    |                     |                      |
| ----------------- | ------------------ | ------------------- | -------------------- |
| `bounce`          | `flash`            | `pulse`             | `rubberBand`         |
| `shake`           | `headShake`        | `swing`             | `tada`               |
| `wobble`          | `jello`            | `bounceIn`          | `bounceInDown`       |
| `bounceInLeft`    | `bounceInRight`    | `bounceInUp`        | `bounceOut`          |
| `bounceOutDown`   | `bounceOutLeft`    | `bounceOutRight`    | `bounceOutUp`        |
| `fadeIn`          | `fadeInDown`       | `fadeInDownBig`     | `fadeInLeft`         |
| `fadeInLeftBig`   | `fadeInRight`      | `fadeInRightBig`    | `fadeInUp`           |
| `fadeInUpBig`     | `fadeOut`          | `fadeOutDown`       | `fadeOutDownBig`     |
| `fadeOutLeft`     | `fadeOutLeftBig`   | `fadeOutRight`      | `fadeOutRightBig`    |
| `fadeOutUp`       | `fadeOutUpBig`     | `flipInX`           | `flipInY`            |
| `flipOutX`        | `flipOutY`         | `lightSpeedIn`      | `lightSpeedOut`      |
| `rotateIn`        | `rotateInDownLeft` | `rotateInDownRight` | `rotateInUpLeft`     |
| `rotateInUpRight` | `rotateOut`        | `rotateOutDownLeft` | `rotateOutDownRight` |
| `rotateOutUpLeft` | `rotateOutUpRight` | `hinge`             | `jackInTheBox`       |
| `rollIn`          | `rollOut`          | `zoomIn`            | `zoomInDown`         |
| `zoomInLeft`      | `zoomInRight`      | `zoomInUp`          | `zoomOut`            |
| `zoomOutDown`     | `zoomOutLeft`      | `zoomOutRight`      | `zoomOutUp`          |
| `slideInDown`     | `slideInLeft`      | `slideInRight`      | `slideInUp`          |
| `slideOutDown`    | `slideOutLeft`     | `slideOutRight`     | `slideOutUp`         |
| `heartBeat`       |

Full example:

```html
<h1 class="animated infinite bounce delay-2s">Example</h1>
```

<!--
[Check out all the animations here!](https://daneden.github.io/animate.scss/)
 -->

It's possible to change the duration of your animations, add a delay or change the number of times that it plays:

```css
.yourElement {
  animation-duration: 3s;
  animation-delay: 2s;
  animation-iteration-count: infinite;
}
```

## Usage with jQuery

You can do a whole bunch of other stuff with animate.scss when you combine it with jQuery. A simple example:

```javascript
$("#yourElement").addClass("animated bounceOutLeft");
```

You can also detect when an animation ends:

<!--
Before you make changes to this file, you should know that $('#yourElement').one() is *NOT A TYPO*

http://api.jquery.com/one/
-->

```javascript
// See https://github.com/daneden/animate.scss/issues/644
var animationEnd = (function(el) {
  var animations = {
    animation: "animationend",
    OAnimation: "oAnimationEnd",
    MozAnimation: "mozAnimationEnd",
    WebkitAnimation: "webkitAnimationEnd"
  };

  for (var t in animations) {
    if (el.style[t] !== undefined) {
      return animations[t];
    }
  }
})(document.createElement("div"));

$("#yourElement").one(animationEnd, doSomething);
```

[View a video tutorial](https://www.youtube.com/watch?v=CBQGl6zokMs) on how to use Animate.scss with jQuery here.

**Note:** `jQuery.one()` is used when you want to execute the event handler at most _once_. More information [here](http://api.jquery.com/one/).

It's possible to extend jQuery and add a function that does it all for you:

```javascript
$.fn.extend({
  animateCss: function(animationName, callback) {
    var animationEnd = (function(el) {
      var animations = {
        animation: "animationend",
        OAnimation: "oAnimationEnd",
        MozAnimation: "mozAnimationEnd",
        WebkitAnimation: "webkitAnimationEnd"
      };

      for (var t in animations) {
        if (el.style[t] !== undefined) {
          return animations[t];
        }
      }
    })(document.createElement("div"));

    this.addClass("animated " + animationName).one(animationEnd, function() {
      $(this).removeClass("animated " + animationName);

      if (typeof callback === "function") callback();
    });

    return this;
  }
});
```

And use it like this:

```javascript
$("#yourElement").animateCss("bounce");
or;
$("#yourElement").animateCss("bounce", function() {
  // Do something after animation
});
```

## Setting _Delay_ and _Speed_

### Delay Class

It's possible to add delays directly on the element's class attribute, just like this:

```html
<div class="animated bounce delay-2s">Example</div>
```

These class names are generated by the `$animate-scss-second-delays` list variable. You can override this variable to create classes for your own needs as such:

```scss
$animate-scss-second-delays: 1, 2, 3, 4, 5, 6, 7; // go on to your heart's content!
```

| List Item | Class Name | Delay Time |
| --------- | ---------- | ---------- |
| 2         | `delay-2s` | `2s`       |
| 3         | `delay-3s` | `3s`       |
| 4         | `delay-4s` | `4s`       |
| 5         | `delay-5s` | `5s`       |

### Speed Classes

These class names are generated by the `$animate-scss-durations` map variable. It's possible to control the speed of the animation by adding these classes, as a sample below:

```html
<div class="animated bounce faster">Example</div>
```

You can override these values by creating your own map -- and even add custom speeds -- as demonstrated below:

```scss
$animate-scss-durations: (
  fast: 800ms,
  faster: 500ms,
  fassssssssssst: 200ms,
  // custom speed!
    slow: 2s,
  slower: 3s
);
```

| Class Name/Map Key | Default Speed |
| ------------------ | ------------- |
| `slow`             | `2s`          |
| `slower`           | `3s`          |
| `fast`             | `800ms`       |
| `faster`           | `500ms`       |

> **Note**: The `animated` class has a default speed of `1s`. If you need custom duration, set a new value for the `$animate-scss-default-duration` variable.

## Accessibility

Animate.scss supports the [`prefers-reduced-motion` media query](https://webkit.org/blog/7551/responsive-design-for-motion/) so that users with motion sensitivity can opt out of animations. On supported platforms (currently only OSX Safari and iOS Safari), users can select "reduce motion" on their operating system preferences and it will turn off CSS transitions for them without any further work required.

## License

Animate.scss is licensed under the MIT license. (http://opensource.org/licenses/MIT)

## Contributing

Pull requests are the way to go here. We only have two rules for submitting a pull request: match the naming convention (camelCase, categorised [fades, bounces, etc]) and let us see a demo of submitted animations in a [pen](http://codepen.io). That **last one is important**.
