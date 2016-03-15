**Angular Directive** extension for at.js library provides a "flicker-free" implementation on view changes. This approach could be used for any Angular application. Conveniently, this extension implementation can be added to the application using DTM.

##Prerequisites: 
  1. AT.js library
  1. Angular library 

##Integration Instructions:
  1. Use at.js
  1. Initialize Directive part with [adobe.target.ext.angular.initDirective](https://github.com/Adobe-Marketing-Cloud/target-atjs-extensions/blob/master/src/angular/adobe.target.ext.angular.lib%2Bdirective.js) method by passing your Angular module as an argument. In DTM this may also need to be included as a Sequential Javascript snippet in a Page Load Rule triggered at the bottom. 

Simple example:
``` javascript
adobe.target.ext.angular.initDirective( app, {
    mbox:'directive-mbox',
    selector:'body > div:nth-child(2) > div:nth-child(2) > div > div > div:nth-child(2)',
    debug: true } );

```

Example with all available options:
``` javascript
adobe.target.ext.angular.initDirective(app, // Angular module, object reference or string, required 
    {
        params:  {param1:'val1',param2:'val2'}, // Target mbox parameters, optional
        mbox: 'directive-mbox',           // Target mbox name, optional
        selector: '.selector',            // CSS selector for mbox element, optional
        //timeout: 5000,                  // Target call timeout
        allowedRoutesFilter: [],          // Blank for all routes or restrict to specific routes: ['/','/about','/item/:id']
        disallowedRoutesFilter: [],       // Exclude specific routes: ['/login','/privacy']
        debug: true                       // Print console statements
    });
```  

##Demo 
[Angular Directive Example](http://adobe-marketing-cloud.github.io/target-sdk-libraries/demos/examples/angular/directive_example.html#/view1)