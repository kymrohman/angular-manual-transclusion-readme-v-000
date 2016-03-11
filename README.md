# Manual and isolate transclusion

## Overview

Now that we know what transclusion does, we can look into more advanced methods of implementing it. Let's take a look how to transclude our content manually.

## Objectives

- Use the transclude function inside the link function

## transclude()

If we change over the value of our `transclude` property to `'element'` in our directives, we can use the fifth function provided in our `link` function.

This function returns our transcluded content as an actual DOM element. This allows us to manually append our elements into our directives instead.

```js
function ourDirective() {
  return {
    transclude: 'element',
    template: [
      '<div class="ourDirective">',
        'The content of our directive is: <span></span>',
      '</div>'
    ].join(''),
    link: function (scope, element, attrs, ctrl, transclude) {
        // transclude() = DOM elements
    }
  };
}

angular
  .module('app', [])
  .directive('ourDirective', ourDirective);
```

Now that we've got the transcluded elements as actual DOM elements and also our whole directive element (the `element` variable), we can insert our transcluded content wherever we want. If we want to put it into the span, we can do this:

```js
function ourDirective() {
  return {
    transclude: 'element',
    template: [
      '<div class="ourDirective">',
        'The content of our directive is: <span></span>',
      '</div>'
    ].join(''),
    link: function (scope, element, attrs, ctrl, transclude) {
        el.find('span').after(transclude());
    }
  };
}

angular
  .module('app', [])
  .directive('ourDirective', ourDirective);
```

Awesome! This puts our transcluded content inside the `<span />`.