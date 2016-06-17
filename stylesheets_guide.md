# Stylesheets Guide

## SASS / SCSS

### Filenames

Files to be imported by the `@import` statment should be prefixed with an
underscore. This is so that the SASS/SCSS compiler knows not to compile them in
insolation.

```
# Good
app/styles/
├── main.scss
├── modules
│   └── _colours.scss
└── partials
    ├── _header.scss
    └── _sidebar.scss

# Bad
app/styles/
├── main.scss
├── modules
│   └── colours.scss
└── partials
    ├── header.scss
    └── sidebar.scss
```
