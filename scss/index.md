# scss/css

## Formatting

- Use soft tabs (2 spaces) for indentation
- Prefer dashes over camelCasing in class names.
- Do not use ID selectors
- When using multiple selectors in a rule declaration, give each selector its own line.
- Put a space before the opening brace { in rule declarations
- In properties, put a space after, but not before, the : character.
- Put closing braces } of rule declarations on a new line
- Put blank lines between rule declarations

Please refer to airbnb [formatting](https://github.com/airbnb/css#formatting)

## Naming
The CSS responsible for component-specific styling.

Syntax: `[<namespace>-]<ComponentName>[-descendentName][--modifierName]`

Please refer to suit [naming conventions](https://github.com/suitcss/suit/blob/master/doc/naming-conventions.md)

```css
/* Utility */
.u-utilityName {}

/* Component */
.ComponentName {}

/* Component modifier */
.ComponentName--modifierName {}

/* Component descendant */
.ComponentName-descendant {}

/* Component descendant modifier */
.ComponentName-descendant--modifierName {}

/* Component state (scoped to component) */
.ComponentName.is-stateOfComponent {}
```

### Components

We use a variant of BEM with PascalCased "blocks"

*Example*

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard-title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard-content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```

```css
/* ListingCard.css */
.ListingCard { }
.ListingCard--featured { }
.ListingCard-title { }
.ListingCard-content { }
```

- `.ListingCard` is the “block” and represents the higher-level component
- `.ListingCard-title` is an “element” and represents a descendant of `.ListingCard` that helps compose the block as a whole.
- `.ListingCard--featured` is a “modifier” and represents a different state or variation on the `.ListingCard` block.

## ID selectors

While it is possible to select elements by ID in CSS, it should generally be considered an anti-pattern. ID selectors introduce an unnecessarily high level of [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) to your rule declarations, and they are not reusable.

[source](https://github.com/airbnb/css)

## JavaScript hooks

Avoid binding to the same class in both your CSS and JavaScript. Conflating the two often leads to, at a minimum, time wasted during refactoring when a developer must cross-reference each class they are changing, and at its worst, developers being afraid to make changes for fear of breaking functionality.

We recommend creating JavaScript-specific classes to bind to, prefixed with `.js-`:

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

[source](https://github.com/airbnb/css)

# scss

## Syntax
- Use the .scss syntax, never the original .sass syntax
- Order your regular CSS and @include declarations logically (see [here](https://github.com/airbnb/css#ordering-of-property-declarations))


# css
