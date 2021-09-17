# CSS Guidelines

## Naming CSS files

- CSS files are located in the ```Styles``` folder.
- CSS files are named with lowercase letters.
- Multiple words are separated with a dash. For example: ```simple-confirm.css```.
- Every component, control and page is styled in its own CSS file.
- CSS files for controls and pages are prefixed with ```ascx``` or ```aspx```. For example: ```ascx-intership-settings.css```.

## Including CSS files

CSS files for controls and pages must be explicitly included. This is done like so:

1. Declare the CSS file in ```Code/Stylesheet/Includes.vb```.
2. Include the CSS file in the load handler in code behind of the control or page:
    ```vb
    Private Sub LoadHandler(...) Handles Me.Load
        Stylesheet.Includes.Add(Stylesheet.Includes.ASCX_GRADING, Me)
    End Sub
    ```

CSS files for components are included in the same way. Except for those that are very commonly used, like ```button``` or ```flash-message```. They should always be available and therefore included directly in the master page.

## Components and Elements

* The CSS selector for the component, control or page, should have the same name as the CSS file. For example, the control that is styled in ```ascx-internship-settings.css``` have the CSS selector ```.ascx-internship-settings```.
* Every element belong to a component, control or page. The CSS selector for an element have the component, control or page as a prefix, and then separated with double underscores. For example, the input element in the search component have the selector ```.search__input``` and can be found in the file ```search.css```.

## Use class selectors

```css
/* GOOD: Class selector. */
.button {

}

/* BAD: Type selector. */
button {

}

/* BAD: Id selector. */
#footer {

}
```

## Avoid combinators

```css
/* GOOD: Basic selector. */
.main-content__title {

}

/* BAD: Decendant combinator. */
.main-content .title {

}

/* BAD: Child combinator. */
.user-list > .item {

}
```

## Lowercase selectors


```css
/* GOOD: Lowercase name. */
.user {

}

/* BAD: Uppercase name. */
.User {

}
```

## Single dash between words

```css
/* GOOD: Single dash between words. */
.grading-history {

}

/* BAD: Camel case to separate words. */
.gradingHistory {

}
```

## Double underscores between component and element name

```css
/* GOOD: Double underscores between component and element name. */
.student-list__item-header {

}

/* BAD: Double dashes between component and element name. */
.student-list--item-header {

}
```

## Modifiers should be capitalized and used with compounders

Modifiers defines a type or a state of an element. Modifiers are always capitalized. For example, a button can be of type ```.LARGE``` and have the state ```.ACTIVE```.

Modifiers must always be selected with compounders. If the element depends on a modifier from a different component, it must be selected with both compunding and combinators. This is to avoid styling unintended elements.

```css
/* GOOD: Capitalized modifier used with compounder. */
.simple-confirm.OPEN {

}

/* GOOD: Capitalized modifier with compounder and combinator for element
   that is outside the scope of the modifier. In this example, the modifier
   EXPANDED belongs to the component expandable, and the target element
   belongs to the component grade-panel. */
.grade-panel.EXPANDED .grade-panel__title {

}

/* BAD: Selector is not specific enough. Risk of selecting unintended elements. */
.EXPANDED .grade-panel__title {

}
```

## Use view mode instead of media queries

Learnpoint have a built in view mode with two states: ```is-mobile``` and ```is-desktop```. The view mode is available at the root element. Use the view mode instead of media queries.

```css
/* GOOD: Using the view mode. */
.is-mobile .avatar {

}

/* GOOD: Using the view mode. */
.is-desktop .avatar {

}

/* BAD: Using media query. */
@media (min-width: 320px) {
    .avatar {
    
    }
}
```

## Each rule on a separate line

```css
/* GOOD: Each rule on a separate line. */
.button {
    color: #333;
    font-size: 16px;
}

/* BAD: Several rules on the same line. */
.button { color: #333; font-size: 16px; }
```


## Use 4 spaces for indentation
```css
/* GOOD: 4 spaces for indentation. */
.avatar {
    display: block;
}

/* BAD: 2 spaces for indentation. */
.avatar {
  display: block;
}
```

## Use comments to clearly separate elements

```css
/* GOOD: Elements are separated with comments. */

/* ==========================================================================
   Content
   ========================================================================== */

.avatar__content {
    position: absolute;
    top: 0;
    width: 264px;
    opacity: 0;
}

.is-mobile .avatar__content {
    position: fixed;
}

.avatar.OPEN .avatar__content {
    opacity: 1;
}



/* ==========================================================================
   Close Button
   ========================================================================== */

.avatar__close-button {
    font-size: 12px;
}



/* BAD: Elements are not separated with comments. */

.avatar__content {
    position: absolute;
    top: 0;
    width: 264px;
    opacity: 0;
}

.is-mobile .avatar__content {
    position: fixed;
}

.avatar.OPEN .avatar__content {
    opacity: 1;
}

.avatar__close-button {
    font-size: 12px;
}
```
