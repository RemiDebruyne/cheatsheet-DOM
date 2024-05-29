# DOM Cheatsheet

## Move
For all nodes: 
- `parentNode()`
- `document.node.childNodes` : return a collection of all child nodes, including text node
- `document.node.firstChild`
- `document.node.lastChild`
- `document.node.previousSibling`
- `document.node.nextSibling`

For element nodes only: 
- `document.elem.parentElement`
- `document.elem.children` : return a collection of an element child's element
- `document.elem.firstElementChild`
- `document.elem.lastElementChild`
- `document.elem.previousElementSibling` 
- `document.elem.nextElementSibling`

## Search 
### getElements
- `document.getElementById`
- `document.getElementsByName`
- `document.getElementsByTagName`
- `document.getElementsByClassName`

### querySelector(css)
- `document.querySelector()` : return the first elemen that matches the css selector
- `document.querySelectorAll()` : return a **static** collection of elements matching the css selector

## Elements
- `elem.innerHTML` : modify the content **inside** an element with new one. Creates a reload.
- `elem.outerHTML` : replace the entire element **tags included**. The element itself isn't *modified* it is entirely replaced
- `elem.textContent` : returns or modify the text inside an element, tags are completly ignored
- `elem.data` : the `data` is similar to `innerHTML` but for `text node` 
- `elem.hidden` : When set to true, does the same as CSS display:none.

## Attributes
 - `elem.hasAttribute(name)` : checks for existence
 - `elem.getAttribute(name)` : gets the value
 - `elem.setAttribute(name, value)` : sets the value
 - `elem.removeAttribute(name)` : removes the attribute

## Document
- `document.createElement(tag)` : create an element node
- `document.createTextNode(tag)` : create a text node
- `node.append(...nodes)` : add `...nodes` at the end of the node
- `node.prepend(...nodes)` : same has `append` but at the beginning of the node
- `node.before(...nodes)` : add the `...nodes` before the node
- `node.after(...nodes)` : add the `...nodes` after the node
- `node.replaceWith(...nodes)` : replace the node with given `...nodes`
- `node.remove()` : remove the node

The methods above insert `html` as strings.

- `elem.insertAdjacentHTML('where', 'html')` : inserts HTML as is on the element at the `where` position.
    - `beforebegin`
    - `afterbegin`
    - `beforeend`
    - `afterend`