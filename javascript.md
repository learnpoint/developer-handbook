# JavaScript Guidelines

## Naming JavaScript files

- JavaScript files are located in the ```Scripts``` folder.
- JavaScript files are named with lowercase letters.
- Multiple words are separated with a dash. For example: ```simple-confirm.js```.
- Every component, control and page is coded in its own JavaScript file.
- JavaScript files for controls and pages are prefixed with ```ascx``` or ```aspx```. For example: ```ascx-intership-settings.js```.

## Including JavaScript files

JavaScript files for controls and pages must be explicitly included. This is done like so:

1. Declare the JavaScript file in ```Code/Javascript/Includes.vb```.
2. Include the JavaScript file in the load handler in code behind of the control or page:
    ```vb
    Private Sub LoadHandler(...) Handles Me.Load
        Javascript.Includes.Add(Javascript.Includes.ASCX_GRADING, Me)
    End Sub
    ```

JavaScript files for components are included in the same way. Except for those that are very commonly used, like ```simple-confirm``` or ```flash-message```. They should always be available and therefore included directly in the master page.


## Don't pollute global namespace

Always wrap code in anonymous functions:


```js
 // GOOD:
 (function() {
     const size = 5;
 })();

 // BAD:
const size = 5;
```


## Avoid DOM state

Don't store DOM elements in variables outside event handlers. You never know when DOM content might change.

```js
// GOOD:
document.addEventListener('click', event => {
    if (event.target.matches('.save')) {
        console.log('Save');
    }
});


// BAD:
const btnSave = document.querySelector('.save');

btnSave.addEventListener('click', event => {
    console.log('Save');
});
```


## Store event handlers in document

Event handler should be stored in the document. For events that don't bubble, use capturing:

```js
// GOOD:
document.addEventListener('focus', event => { ... }, true);

// BAD:
saveButton.addEventListener('focus', event => { ... });
```


## Happy Path

Main flow should be left aligned. Indent the exceptions:

```js
// GOOD:
const res = getSomething();
if (!res.ok) {
    return res.err;
}
console.log(res.message);

// BAD:
const res = getSomething();
if (res.ok) {
    console.log(res.message);
} else {
    return res.err;
}
```


## Explain through code

Use expanatory variable names instead of comments:

```js
// GOOD:
const maxItemsOnPage = 100;
if (items.length > maxItemsOnPage) {
    paginate(items);
}

// BAD:
if (items.length > 100) { /* Paginate items when more than 100. */
    paginate(items);
}
```


## Use modern JavaScript

* Use let and const instead of var
* Use fetch insted of XMLHTTPRequest
* Use classList instead of className
* Use querySelector* instead of getElementBy*
* Use for...of when iterating NodeLists
* Use arrow syntax when passing functions
* Use map, reduce, forEach, etc on arrays


## Watch out for css transitions and transforms

When you need to use the size or position of an element, be aware of css transitions and transforms.

For instance, accessing ```el.width``` will (force layout and) return the current rendered width of the element. If you just added the element to the document, it might be in the middle of a transition that changes the width.
