# Alphabetize GA4 Event Parameters

This bookmarklet can be run within the GTM UI in order to reorder your event parameters alphabetically.

## Source
```js
(() => {
  const paramRows = document.querySelectorAll('[diff-field^="tag.data.vendorTemplate.param.eventParameters.listItem"]');
  const nameAttributeBase = 'tag.data.vendorTemplate.param.eventParameters';
  const e = new Event("change");

  const values = Array.from(paramRows).map((paramRow, index) => {
    const key = paramRow.querySelector(`[name="${nameAttributeBase}.${index}.name"] input`).value;
    const value = paramRow.querySelector(`[name="${nameAttributeBase}.${index}.value"] input`).value;
    return {key, value};
  });

  values.sort(function(a, b) {
    if (a.key < b.key) return -1;
    if (a.key > b.key) return 1;
    return 0;
  });

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
javascript:(()=>{const e=document.querySelectorAll('[diff-field^="tag.data.vendorTemplate.param.eventParameters.listItem"]'),a="tag.data.vendorTemplate.param.eventParameters",t=new Event("change"),n=Array.from(e).map(((e,t)=>({key:e.querySelector(`[name="${a}.${t}.name"] input`).value,value:e.querySelector(`[name="${a}.${t}.value"] input`).value})));n.sort((function(e,a){return e.key<a.key?-1:e.key>a.key?1:0})),n.forEach((({key:e,value:n},r)=>{const u=document.querySelector(`[name="${a}.${r}.name"] input`);u.value=e,u.dispatchEvent(t);const l=document.querySelector(`[name="${a}.${r}.value"] input`);l.value=n,l.dispatchEvent(t)}))})();
```