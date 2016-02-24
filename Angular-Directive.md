**Angular Directive** extension for at.js library can provide a "flicker-free" implementation on view changes.  This approach could be used for any Angular application. Conveniently, this extension implementation can be added to the application using DTM.

##Prerequisites: 
  1. AT.js library
  1. Angular library 

##Integration Instructions:
  1. Use at.js
  1. Add extension [directive-mbox.js](http://adobe-marketing-cloud.github.io/target-sdk-libraries/demos/examples/angular/js/directive-mbox.js) to your server.
  1. Add the above file to the end of _at.js_ in the Target Tool configuration of DTM.  Or, include it in your HTML after _angular.js_ and _at.js_

``` javascript
angular.module('adobe.target.directives', []).directive('mbox', function() {
  return {
    restrict: 'AE',
    link: {
      pre: function preLink(scope, element, attributes, controller) {
        element.css('visibility', 'hidden');
      },
      post: function postLink(scope, element, attributes, controller) {
        adobe.target.getOffer({
          mbox: attributes.mboxname,
          success: function(response) {
            adobe.target.applyOffer({
              element: element[0],
              offer: response
            });
            element.css('visibility', 'visible');
          },
          error: function(status, response) {
            element.css('visibility', 'visible');
          }
        });
      }
    }
  };
});
```

##Demo 
[Angular Directive Example](http://adobe-marketing-cloud.github.io/target-sdk-libraries/demos/examples/angular/directive_example.html#/view1)