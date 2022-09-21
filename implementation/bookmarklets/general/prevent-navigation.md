# Prevent Navigation

This bookmarklet can be run on any page of any site to interrupt navigation when a link is clicked. This is a great way to QA data layer pushes or analytics calls that should go out before your browser navigates.

## Source
```js
window.onbeforeunload = () => "";
```

## Bookmarklet
```js
javascript:window.onbeforeunload = () => "";
```