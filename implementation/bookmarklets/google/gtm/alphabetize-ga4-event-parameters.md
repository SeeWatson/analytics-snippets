# Alphabetize GA4 Event Parameters

This bookmarklet can be run within the GTM UI in order to reorder your event parameters alphabetically.

## Source
```js
(() => {
  // Get current parameters
  const paramRows = document.querySelectorAll('[diff-field^="tag.data.vendorTemplate.param.eventParameters.listItem"]');
  const nameAttributeBase = 'tag.data.vendorTemplate.param.eventParameters';
  const e = new Event("change");

  const values = Array.from(paramRows).map((paramRow, index) => {
    const key = paramRow.querySelector(`[name="${nameAttributeBase}.${index}.name"] input`).value;
    const value = paramRow.querySelector(`[name="${nameAttributeBase}.${index}.value"] input`).value;
    return {key, value};
  });

  // Do the actual sorting
  values.sort((a, b) => a.key.localeCompare(b.key));

  // To make the updates in GTM, we need to both set the values in the inputs and then fire a "change" event so that GTM will notice the changes and persist them
  values.forEach(({key, value}, index) => {
    const keyInput = document.querySelector(`[name="${nameAttributeBase}.${index}.name"] input`)
    keyInput.value = key;
    keyInput.dispatchEvent(e);
    
    const valueInput = document.querySelector(`[name="${nameAttributeBase}.${index}.value"] input`);
    valueInput.value = value;
    valueInput.dispatchEvent(e);
  })
})();
```

## Bookmarklet
```js
javascript:(()=>{const e=document.querySelectorAll('[diff-field^="tag.data.vendorTemplate.param.eventParameters.listItem"]'),a="tag.data.vendorTemplate.param.eventParameters",t=new Event("change"),n=Array.from(e).map(((e,t)=>({key:e.querySelector(`[name="${a}.${t}.name"] input`).value,value:e.querySelector(`[name="${a}.${t}.value"] input`).value})));n.sort((a, b) => a.key.localeCompare(b.key)),n.forEach((({key:e,value:n},r)=>{const u=document.querySelector(`[name="${a}.${r}.name"] input`);u.value=e,u.dispatchEvent(t);const l=document.querySelector(`[name="${a}.${r}.value"] input`);l.value=n,l.dispatchEvent(t)}))})();
```