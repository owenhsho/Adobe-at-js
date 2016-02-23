
## Angular ngRoute
Using promises in Angular's router can provide a "flicker-free" implementation on view changes.  This approach could be used in an application using Angular's ngRoute module.  Conveniently, it can be added to the application using DTM.

**Prerequisites:** 
  1. AT.js library
  1. Angular library 

**Instructions:** 
  1. Use at.js without the auto-created mbox
  1. Add extension [adobe.target.ext.angular.lib+ngroute.js](https://github.com/Adobe-Marketing-Cloud/target-spa-extensions/blob/master/src/angular/adobe.target.ext.angular.lib%2Bngroute.js) to your server.
  1. Add the above file to the end of _at.js_ in the Target Tool configuration of DTM.  Or, include it in your HTML after _angular.js_ and _at.js_
  1. Initialize with `adobe.target.ext.angular.initRoutes` method by passing your Angular module as an argument. In DTM you might need to include this as a Sequential Javascript snippet in a Page Load Rule triggered at the Bottom of the Page. 

``` javascript
adobe.target.ext.angular.initRoutes(app);  // where app is a required argument, reference to an Angular module, can be object or string name

   //or example with all available options:

adobe.target.ext.angular.initRoutes(app,     // Angular module, object reference or string, required 
    {
        params: {param1:'val1',param2:'val2'},     // Target mbox parameters, optional
        //mbox: 'custom-mbox-name',         // Target mbox name, optional
        //selector: 'body',                 // CSS selector to inject Target content to, optional
        //timeout: 5000,                    // Target call timeout
        allowedRoutesFilter: [],            // Blank for all routes or restrict to specific routes: ['/','/about','/item/:id']
        disallowedRoutesFilter: [],         // Exclude specific routes: ['/login','/privacy']
        debug: true                         // Print console statements
    });
```  

**Demo:** [Route Change Example](http://adobe-marketing-cloud.github.io/target-sdk-libraries/demos/examples/angular/route_change_demo.html)

## Hash Change
Many single page applications update the URL on view changes. We can use these URL updates to trigger an mbox call.

**Example:** Put this code after at.js to trigger mbox calls on pushState/hashchange:  

``` javascript
    put code here
```  


**Data Layer:** Be sure to update your data layer before processing the URL change to maximize usage in Target.

**DTM:** Event-based rules using the "pushState/hashChange" condition can be used to trigger mbox calls instead of the Example code above.  There is an additional roundtrip needed to retrieve code from DTM before making the mbox call.

**Demo:**
[hashChange Example](http://adobe-marketing-cloud.github.io/target-sdk-libraries/demos/examples/classic/hash_change_event.html)

## Custom Event
If your single page application does not update the URL on view change, consider triggering a custom event instead.  An event listener can then be used to trigger mbox calls when this happens. (Note: this technique can be used on small updates to the viewport, too)

**Data Layers:** Be sure to update your data layer before triggering the event to maximize usage in Target.

**DTM:** Event-based rules using the "custom" condition can be used to trigger mbox calls.  There is an additional roundtrip needed to retrieve code from DTM before making the mbox call.

**Demo:**

**Example:** Put this code after at.js to trigger mbox calls on custom events:  

``` javascript
// ie9+, needs ie8 support
// Listen for the event broadcast by the framework when it processes a view change
window.addEventListener('NAME_OF_YOUR_CUSTOM_EVENT_THAT_FIRES_AFTER_UPDATING_THE_DATA_LAYER',
    function(e) {
        adobe.target.getOffer({
            "mbox": "target-global-mbox",
            "params": {
                "trigger": "customEvent"
            },
            "success": function(offer) {
                adobe.target.applyOffer({
                    offer: offer
                });
            },
            "error": function(status, error) {}
        });
    }
);
```  

## Angular Directive
Wrapping mboxes can be added to elements using an Angular directive.

**Demo:**
[Angular Directive Example](http://adobe-marketing-cloud.github.io/target-sdk-libraries/demos/examples/angular/directive_example.html)