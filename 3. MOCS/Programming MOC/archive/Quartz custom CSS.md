---
Main Moc: "[[Tech MOC]]"
related:
  - "[[Quartz]]"
  - "[[Quartz Setup Proces]]"
completed: true
created: 2024-12-04T12:32
updated: 2025-03-16T13:09
---
>[!abstract] Related
>- [[Quartz]]
>- [[Quartz Setup Proces]]

---
Quartz has a file dedicated to the customization of the site css, it's named `custom.scss` an the relative path is `quartz/styles/custom.scss`.

This are the things that i have added:
- center align for images
- custom text formatting

Here there is the code:

``` SCSS
@use "./base.scss";

// put your custom CSS here!

// center images
img {
    display: block;
    margin-left: auto;
    margin-right: auto;
}

// customize italic italic
em {
    background-color: var(--highlight);
    padding: 1px;
    border-radius: 4.5px;
    font-style: normal; /* Remove italic formatting */
}

// change bold color
strong, .page article p > strong {
    color: var(--tertiary);
}

// customize bold italic
em strong, strong em {
    color: var(--darkgray);
}
```

