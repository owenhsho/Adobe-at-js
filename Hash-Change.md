Many single page applications update the URL on view changes. We can use these URL updates to trigger an mbox call.

##Example: Put this code after at.js to trigger mbox calls on pushState/hashchange:  

[Example Code](http://adobe-marketing-cloud.github.io/target-sdk-libraries/demos/examples/angular/js/offers.js)


**Data Layer:** Be sure to update your data layer before processing the URL change to maximize usage in Target.

**DTM:** Event-based rules using the "pushState/hashChange" condition can be used to trigger mbox calls instead of the Example code above.  There is an additional roundtrip needed to retrieve code from DTM before making the mbox call.

##Demo:
[hashChange Example](http://adobe-marketing-cloud.github.io/target-sdk-libraries/demos/examples/classic/hash_change_event.html)