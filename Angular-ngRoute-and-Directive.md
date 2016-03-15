**Angular ngRoute and Directive** extension for at.js library uses a mix of two approaches - [ngRoute](Angular-ngRoute) and [Directive](Angular-Directive) to deliver more testing capabilities to the site. While ngRoute implementation can handle the global mbox calls for each page on route change, the Directive may work well for adding additional mboxes on a page to test smaller sections of the site.

Conveniently, this extension can be added to the application using DTM.

##Prerequisites: 
  1. AT.js library
  1. Angular library 
  1. Angular ngRoute module 

##Integration Instructions:
  1. Use at.js without the auto-created mbox
  1. Add the extension [adobe.target.ext.angular.lib+ngroute+directive.js](https://github.com/Adobe-Marketing-Cloud/target-atjs-extensions/blob/master/src/angular/adobe.target.ext.angular.lib%2Bngroute%2Bdirective.js) to your page after _angular.js_ and _at.js_ OR add the extension to the end of _at.js_ in the Target Tool configuration of DTM.
  1. Initialize ngRoute part with `adobe.target.ext.angular.initRoutes` method by passing your Angular module as an argument. In DTM you might need to include this as a Sequential Javascript snippet in a Page Load Rule triggered at the bottom of the relevant page. 
  1. Initialize Directive part with `adobe.target.ext.angular.initDirective` method by passing your Angular module as an argument. In DTM this may also need to be included as a Sequential Javascript snippet in a Page Load Rule triggered at the bottom. 

Simple example:
``` javascript
adobe.target.ext.angular.initRoutes(app);  // where app is a required argument, reference to an Angular module, can be object or string name

adobe.target.ext.angular.initDirective( app, {
    mbox:'directive-mbox',
    selector:'body > div:nth-child(2) > div:nth-child(2) > div > div > div:nth-child(2)',
    debug: true } );

```

Example with all available options:
``` javascript
adobe.target.ext.angular.initRoutes(app,     // Angular module, object reference or string, required 
    {
        params: {param1:'val1',param2:'val2'},     // Target mbox parameters, optional
        mbox: 'custom-mbox-name',            // Target mbox name, optional
        selector: 'body',                    // CSS selector to inject Target content to, optional
        timeout: 5000,                       // Target call timeout
        allowedRoutesFilter: [],             // Blank for all routes or restrict to specific routes: ['/','/about','/item/:id']
        disallowedRoutesFilter: [],          // Exclude specific routes: ['/login','/privacy']
        debug: true                          // Print console statements
    });
```  

##Demo 
[Route Change & Directive Example](http://adobe-marketing-cloud.github.io/target-sdk-libraries/demos/examples/angular-dtm-ngroute-directive/index.html)