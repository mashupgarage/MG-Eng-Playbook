# CSS Guidelines

It's easy to learn the basics of CSS but to be able to write effective CSS it needs proper practice and direction. These are the standards we follow when writing css.

## Do not use `!important`

The `!important` keyword overrides precedence and makes a rule priority over everything else. On surface level this doesn't seem like a problem but down the road when a stylesheet is updated in the future, especially by a dev unfamiliar with the style, this behavior can make things hard to debug. For example we have this a couple of labels with these classes:
```html
<div class='label'>Red</div>
<div class='label'>Green</div>
<div class='label'>Blue</div>
```

Let's say each label has a padding of 8px. Maybe at the time of development this was a requirement so we put an `!important`:
```css
.label {
  padding: 8px !important;
}
```

Let's say the requirements change in the future and we want a variant with no padding:
```css
.label.-no-padding {
  padding: 0px;
}
```

But no matter what the padding won't change. We could try a number of things but the end of the day we could only resort to another `!important`
```css
.label.-no-padding {
  padding: 0px !important;
}
```

If you're the only developer who touched the code maybe it can be fine but what if you forgot about it or another dev edits it in the future? It's usually tempting to just add another `!important` to force things to work like magic but as stylesheets grow that can cause additional complexity which may lead to bugs and other confusion. Save yourself the hassle, don't use it. We should flag any use of `!important` in our projects using linters.

## Prefer to select using class names

Classes are our preferred way to select elements. We generally avoid using tag selectors because they are too general and have high risk of hitting unintended items. On the other hand, we also rarely use id selectors because id's should ideally be unique and that discourages reuse.

- ✅ class
  ```css
  .label {
    color: red;
  }
  ```
- ⚠️  tag
  ```css
  div {
    color: red;
  }

  div.label {
    color: red;
  }
  ```
- ⚠️  id
  ```css
  #main {
    color: red;
  }
  ```

## Use descriptive class names

Classes should have a semantic meaning that directly relates to what the element does. This makes css rules easier to understand and trace.

- ✅ descriptive names
  ```html
    <div class='post'>
      <div class='title'>Sample Post</div>
      <div class='body'>This is a post</div>
    </div>
  ```

- ❌ names that don't mean anything
  ```html
    <div class='wat'>Test</div>
    <div class='x'>Test</div>
    <div class='asdf'>Test</div>
  ```
- ❌ names that contradict role
  ```html
    <input type='checkbox' class='radio' />
    <button class='textarea'>Submit</button>
  ```
## Avoid the descendant combinator

This combinator is too general and may unexpectedly target something unintended. To make things simpler to follow, prefer to use combinators which have more specific bounds such as child (>), next-sibling (+), or adjacent-sibling (~).
- ✅ child
  ```css
  .post > .title {
    font-weight: bold;
  }

  .post {
    > .body {
      padding: 8px;
    }
  }
  ```
- ✅ next-sibling
  ```css
  .post + .post {
    margin-top: 16px;
  }
  ```
- ✅ adjacent-sibling
  ```css
  .trigger:checked ~ .post {
    display: block;
    visibility: visible;
  }
  ```
- ⚠️  descendant
  ```css
  .post .title {
    font-weight: bold;
  }

  .post {
    .body {
      padding: 8px;
    }
  }
  ```

## Use RSCSS

At MG we follow the concepts of RSCSS to write maintainable CSS. The core concept of RSCSS is to group CSS rules into components, elements and variants. We can visualize RSCSS with the following:
```
Components
  > Elements
  & Variants
```

Components are groupings of CSS rules that represent objects or use cases. They can stand alone and should have specific behavior. They are also usually named with two words (e.g. .pricing-card, .comment-panel, .custom-table).

Elements are the parts that make up components. These usually have more vague or general behavior and only gain context when used under a component along with other elements. They are usually named with one word (e.g. .title, .form, .cell).

Variants are modifiers used on components or elements to change behavior for specific scenarios. They are usually prefixed with a dash (e.g. .-small, .-medium, .-large).

Here's an example of a component built in RSCSS:
```html
  <div class='post-panel -danger'>
    <div class='title -emphasized'>Sample Post</div>
    <div class='body'>This is a post</div>
  </div>
```

```css
.post-panel {
  padding: 8px;
  background-color: white;
  border: 1px solid black;

  &.-danger {
    background-color: $red-50;
    border: 1px solid $red-100;
  }

  > .title {
    font-weight: 400;
    color: black;
  }

  > .title.-emphasized {
    font-weight: bold;
  }

  &.-danger > .title {
    color: $red-100;
  }

  > .title + .body {
   margin-top: 16px;
  }
}
```
