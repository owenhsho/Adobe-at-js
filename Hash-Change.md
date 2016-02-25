Many single page applications update the URL on view changes. We can use these URL updates to trigger an mbox call.  Keep in mind that since the mbox call will be made asynchronously, in-parallel with your view change _visitors may experience flicker_ when the mbox response replaces default content.

##Example: Put this code after at.js to trigger mbox calls on pushState/hashchange:  

[Example Code](http://adobe-marketing-cloud.github.io/target-sdk-libraries/demos/examples/angular/js/offers.js)


**Data Layer:** Update your data layer before processing the URL change, if possible, to maximize potential usage with Target.

**DTM:** Event-based rules using the "pushState/hashChange" condition can be used to trigger mbox calls instead of the Example code below.  There is an additional roundtrip needed to retrieve code from DTM before making the mbox call.

##Demo:
[hashChange Example](http://adobe-marketing-cloud.github.io/target-sdk-libraries/demos/examples/angular/hash_change_event.html)