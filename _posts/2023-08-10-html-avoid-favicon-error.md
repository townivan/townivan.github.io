---
tags: html
---

# html: Avoid the missing favicon error

Does seeing this error in your console log annoy you?

> Failed to load resource: the server responded with a status of 404 (Not Found) 
> favicon.ico:1

Fix it my inserting this favicon placeholder in the HEAD of your html page:

```html
<link rel="icon" href="data:;base64,iVBORw0KGgo=">
```
