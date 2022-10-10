# Custom Click Data Layer Event

## What is it and why would I need it?
Sometimes the GTM `All Elements` and `Just Links` tags are too restrictive in what they can do. This approach enables you to send your own click event to GTM in data layer format it expects them to be in. This is what Google's tags are doing under the hood anyway, so doing it yourself can help your developers better understand what's going on.

### Notes
This approach can sometimes have issues getting data out the door before the page navigates. In that case, you can add an `event.preventDefault` and a timeout if you need to...but you are probably using this because of propogation or default prevention in the first place so be careful with them.

`var` is used instead of `const` due to GTM not allowing ES6, but by all means use `const` if you're adding this code to your site directly


## Code
```js
document.body.addEventListener('click', (event) => {
  var e = event.target;
  
  // Exit early if not a link (or write your own condition for send)
  if(!e.href) return;
  
  // If using GTM variable for internal domain array
  // var internalDomainsArray = {{Custom | Internal Domains Array}}

  // If building internal domains array in code
  var internalDomainsArray = [
    window.location.hostname,
    "otherdomain.whatever"
  ];

  // RegEx-ify the domains
  var internalDomains = internalDomainsArray.join('|').replace('.','\.');
  
  // Regex to compare link domain against specified internal domains
  var outboundRegex = new RegExp("^https?:\/\/((?!" + internalDomains + ").)*([\?\/].*)?$", 'i');

  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    "event": "click",
    "eventModel": {
      "link_domain": e.hostname,
      "link_classes": e.className,
      "link_id": e.id,
      "link_text": e.innerText,
      "link_url": e.href,
      "outbound": outboundRegex.test(e.href),
    }
  })
}, true); // True is important here to enable useCapture
```