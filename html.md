# HTML Guidelines


## Buttons should be button elements

Use `button` if the element have click behaviour:

```html
<!-- GOOD -->
<button type="button">Delete</button>

<!-- BAD -->
<div>Delete</div>
```


## Use inlined svg

Avoid background svg. Use inlined svg for better styling control:

```html
<!-- GOOD -->
<button type="button">
    <!-- #include file="/Images/svg-icons/trash.svg" -->
    <span>Delete</span>
</button>

<!-- BAD -->
<button type="button" style="background-image: '/Images/svg-icons/trash.svg';">
    <span>Delete</span>
</button>
```