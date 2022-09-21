# Prevent Navigation

This bookmarklet can be run within the GTM UI in order to reorder your event parameters alphabetically.

## Source
```js
(() => {
  const paramRows = document.querySelectorAll('[diff-field^="tag.data.vendorTemplate.param.eventParameters.listItem"]');
  const nameAttributeBase = 'tag.data.vendorTemplate.param.eventParameters';

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
    document.querySelector(`[name="${nameAttributeBase}.${index}.name"] input`).value = key;
    document.querySelector(`[name="${nameAttributeBase}.${index}.value"] input`).value = value;
  })
})();
```

## Bookmarklet
```js
javascript:(()=>{const paramRows=document.querySelectorAll('[diff-field^="tag.data.vendorTemplate.param.eventParameters.listItem"]'),nameAttributeBase="tag.data.vendorTemplate.param.eventParameters",values=Array.from(paramRows).map(((e,a)=>({key:e.querySelector(`[name="${nameAttributeBase}.${a}.name"] input`).value,value:e.querySelector(`[name="${nameAttributeBase}.${a}.value"] input`).value})));values.sort((function(e,a){return e.key<a.key?-1:e.key>a.key?1:0})),values.forEach((({key:e,value:a},t)=>{document.querySelector(`[name="${nameAttributeBase}.${t}.name"] input`).value=e,document.querySelector(`[name="${nameAttributeBase}.${t}.value"] input`).value=a}))})();
```