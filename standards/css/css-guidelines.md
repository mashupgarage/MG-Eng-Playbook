# CSS Guidelines

It's easy to learn the basics of CSS but to be able to write effective CSS it needs proper practice and direction. These are the standards we follow when writing css.

# Do not use `!important`

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

# Prefer to select using class names

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

