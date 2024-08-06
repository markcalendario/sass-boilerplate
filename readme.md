# Sass Architecture Structure

Unopinionated file structure of Syntactically Awesome Stylesheet (Sass).

## Definitions

### BASE FOLDER

The `base/` folder contains boilerplate code, including a reset file, typographic rules, and a stylesheet defining standard styles for commonly used HTML elements.

### COMPONENTS FOLDER

The `components/` folder contains smaller components, such as sliders, loaders, widgets, and other specific modules. Unlike the `layout/` folder, which defines the global wireframe, `components/` is focused on widgets and contains many files because the site/application is composed mostly of tiny modules.

### LAYOUT FOLDER

The `layout/` folder includes stylesheets for laying out the site or application, such as for the header, footer, navigation, sidebar, grid system, and forms.

### PAGES FOLDER

To organize page-specific styles, it's recommended to create a `pages/` folder and name the file after the page. For example, if there are very specific styles for the home page, create a `_home.scss` file in the `pages/` folder.

### ABSTRACTS FOLDER

The `abstracts/` folder contains Sass tools and helpers used throughout the project, including global variables, functions, mixins, and placeholders. It's important that this folder doesn't output any CSS when compiled on its own, as these files are only meant to be Sass helpers.

### VENDORS FOLDER

The `vendors/` folder is used to store third-party CSS files from external libraries or frameworks that are used in the project. These files are not part of the project's code and are typically included in the project through a CDN (Content Delivery Network) or by downloading the files and placing them in the `vendors/` folder.

### STYLE FILE

The style file should be the only Sass file from the whole code base not to begin with an underscore. This file should not contain anything but `@import` and comments.

Files should be imported according to the folder they live in, one after the other in the following order:

```
1. abstracts/
2. vendors/
3. base/
4. layout/
5. components/
6. pages/
```
