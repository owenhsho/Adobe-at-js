**Angular UIRouter** extension for at.js library is using promises (delayed objects) within states to provide a "flicker-free" implementation on view changes.  This approach could be used in an application using Angular's `UIRouter` module.  Conveniently, this extension implementation can be added to the application using DTM.

##Prerequisites: 
  1. AT.js library
  1. Angular library 
  1. Angular UIRouter module 

##Integration Instructions:
  1. Use at.js without the auto-created mbox
  1. Add extension [adobe.target.ext.angular.lib+uirouter.js](https://github.com/Adobe-Marketing-Cloud/target-spa-extensions/blob/master/src/angular/adobe.target.ext.angular.lib%2Buirouter.js) to your server.
  1. Add the above file to the end of _at.js_ in the Target Tool configuration of DTM.  Or, include it in your HTML after _angular.js_ and _at.js_
  1. Initialize with `adobe.target.ext.angular.initStates` method by passing your Angular module as an argument. In DTM you might need to include this as a Sequential Javascript snippet in a Page Load Rule triggered at the Bottom of the Page. 

``` javascript
adobe.target.ext.angular.initStates(app);  // where app is a required argument, reference to an Angular module, can be object or string name
```

Example with all available options:
``` javascript
adobe.target.ext.angular.initStates(app,     // Angular module, object reference or string, required 
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
[State Change Example](http://adobe-marketing-cloud.github.io/target-sdk-libraries/demos/examples/angular/state_change_demo.html)