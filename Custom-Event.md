## Custom Event
If your single page application does not update the URL on view change, consider triggering a custom event instead.  An event listener can then be used to trigger mbox calls when this happens. (Note: this technique can be used on small updates to the viewport, too)

**Data Layers:** Be sure to update your data layer before triggering the event to maximize usage in Target.

**DTM:** Event-based rules using the "custom" condition can be used to trigger mbox calls.  There is an additional roundtrip needed to retrieve code from DTM before making the mbox call.

##Demo:

##Example: Put this code after at.js to trigger mbox calls on custom events:  

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
