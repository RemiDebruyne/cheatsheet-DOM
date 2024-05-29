# DOM CheatSheet

## Defintions
- `DOM` : Document object model
- `BOM` : Brower elemobject model
  - navigator
  - screen
  - location
  - frames
  - history
  - XMLHttpRequest

## How it works

Every HTML tag in is an `object`. Those `object`in the `DOM tree` are called `nodes`. Similarly to HTML, those nodes have `children`, `siblings` `parents` and  `ancestors`.

**warning**
`White spaces` and `line breaks` will create their own node of type `text`.

```html
<head>
    <title>this code</title>
</head>
```

Thus the previous code will display a `child`  of `<elem>`. Altough, visualizing the DOM inside the developer tools would hide such nodes to improve readability.

### Node types
There are a total of [12 node types](https://dom.spec.whatwg.org/#node). Altough a few are deprycated. The most used are :
- Document
- Elem
- Text
- Comment

## Move in the DOM
For all nodes: 
- `document.node.parentNode`
- `document.node.childNodes` : return a collection of all child nodes, including text node
- `document.node.firstChild`
- `document.node.lastChild`
- `document.node.previousSibling`
- `document.node.nextSibling`

For element nodes only: 
- `document.elem.parentElement`
- `document.elem.children`
- `document.elem.firstElementChild`
- `document.elem.lastElementChild`
- `document.elem.previousElementSibling` 
- `document.elem.nextElementSibling`

## Search in the DOM
**getElements***
- `document.getElementById`
- `document.getElementsByName`
- `document.getElementsByTagName`
- `document.getElementsByClassName`

**querySelector(css)**
- `document.querySelectorAll()`
- `document.querySelector()`

`getElements` return a **live** collection, meaning they reflect the current state of the DOM.
In the code below, `divs` is assigned a value using `getElementsByTagName`. Thus, when `divs.length`is alerted the second time, it nows alert two because a div was added between the first and second alert.

```html
<div>First div</div>

<script>
  let divs = document.getElementsByTagName('div');
  alert(divs.length); // 1
</script>

<div>Second div</div>

<script>
  alert(divs.length); // 2
</script>
``` 

In this example `divs` was assigned a value using `querySelectorAll`. Thus when `divs.length` is called a second time, it alerts one because it is `static`, the collection is never updated.

```html
<div>First div</div>

<script>
  let divs = document.querySelectorAll('div');
  alert(divs.length); // 1
</script>

<div>Second div</div>

<script>
  alert(divs.length); // 1
</script>
```


**closest(css)**
- Looks for closest ancestor mathching the `css selector`


## DOM Classes
![dom class inheritance diagram](/img/dom%20class%20inheritance%20diagram.png)

### Some useful methods :

- `elem.innerHTML` : Targets everything **inside** the html element as a **string**. It only works witl `elements`

Thus, you can append "new" html inside of your element with concatenation.
```html
chatDiv.innerHTML += "<div>Hello<img src='smile.gif'/> !</div>";
chatDiv.innerHTML += "How goes?";
``` 
However, it delete's the old html, then, loads the new one. **Warning**, this is to take into consideration when user it inside elements containing images, svg and such.

- `elem.outerHTML` : The full HTML of the element. A write operation into elem.outerHTML does not touch elem itself. Instead it gets replaced with the new HTML in the outer context.

- `elem.textContent` : The text inside the element: HTML minus all `tags`. Writing into it puts the text inside the element, with all special characters and tags treated exactly as text. Can safely insert user-generated text and protect from unwanted HTML insertions. For instance, calling `textContent` on the div would remove both `h1` and `p` tags. `alert(news.textContent)` would return : *"I'm an H1 I'm a paragraph"* in a single string.
```html
<div id="news">
  <h1>I'm an H1</h1>
  <p>I'm a paragraph</p>
</div>
```

- `elem.data` : the `data` is similar to `innerHTML` but for `text node` 

- `elem.hidden` : When set to true, does the same as CSS display:none.

## Attributes and properties

### DOM Properties

`DOM nodes` being regular JavaScript object, we can add any properties or method we want to them.

```javascript
//we can add properties to them with the object syntax
document.body.myData = {
  name: 'Caesar',
  title: 'Imperator'
};

//give them methods
document.body.sayTagName = function() {
  alert(this.tagName);
};

//and give methods to all element with the prototype
Element.prototype.sayHi = function() {
  alert(`Hello, I'm ${this.tagName}`);
};
```

### HTML Attributes
When the DOM parses the HTML and finds a **standard** attribute, it turns it into a DOM property.

```html
<div id="id">*
  <input type="text">
</div>
```

We could use `div.id` or `input.type`. However, it only works for **standard** tags. For example, `body` and `div` do not have a `type` attribute, and only `a` tag have an `href` attribute.

#### Methodes to manipulate attributes
 - `elem.hasAttribute(name)` : checks for existence
 - `elem.getAttribute(name)` : gets the value
 - `elem.setAttribute(name, value)` : sets the value
 - `elem.removeAttribute(name)` : removes the attribute


## Modifying the document

-  `document.createElement(tag)` : create an element node
-  `document.createTextNode(tag)` : create a text node

### Insertion methods

- `node.append(...nodes)` : append nodes or strings at the end of node
- `node.prepend(...nodes)` : same has `append` but at the beginning of the node
- `node.before/after(...nodes)` : add the `...nodes` before or after the node **but outside of it**
- `node.replaceWith(...nodes)` : replace the node with given `...nodes`

![modify the document](/img/modify%20the%20document.png)

However, these methods insert string safely like `textContent`. If we want to insert actual HTML we need to use **`elem.insertAdjacentHTML/Element/Text('where', 'html/element/Text')`**

where : 
- `beforebegin`
- `afterbegin`
- `beforeend`
- `afterend`

![insert adjacent html](/img/insert-adjacent-html.png)


