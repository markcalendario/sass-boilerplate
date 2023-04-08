# Sass Architecture Structure

Unopinionated file structure of Syntactically Awesome Stylesheet (Sass).

## Using SASS Compilers

A Sass-compiled stylesheet uses one primary file that handles all the imports. Once that file is compiled, the compiler will generate a plain `.css` file that can be used to style an HTML.

A sub-files must include an underscore `_[filename].scss`. The sub-files can be imported inside the primary file.

Here's an example.

```
sass/
|
|– base/
|   |– _default.scss        # Reset/normalize
|   |– _typography.scss  	# Typography rules
|   ...                  	# Etc…
|
|– components/
|   |– _buttons.scss    	# Buttons
|   |– _dropdown.scss   	# Dropdown
|   ...                  	# Etc…
|
|– layout/
|   |– _navigation.scss  	# Navigation
|   |– _grid.scss        	# Grid system
|   ...                  	# Etc…
|
|– pages/
|   |– _home.scss        	# Home styles
|   |– _login.scss	     	# Login styles
|   ...                  	# Etc…
|
|– abstracts/
|   |– _variables.scss   	# Sass Variables
|   |– _functions.scss   	# Sass Functions
|   |– _mixins.scss      	# Sass Mixins
|   ...                  	# Etc…
|
|– vendors/
|   |– _bootstrap.scss   	# Bootstrap
|   ...                  	# Etc…
|
|– style.scss               # Primary Sass file that '@imports' required files.
```

The `style.scss` includes all the imported sub-files. Once it was compiled, it will generate a css file followed by its name `style.css`. The generated css file can be used as a normal stylesheet throughout an app.

## Using CSS Modules

CSS modules are popularly used in React JS and Next JS for preventing styling collision and overriding other class styles. CSS module will then generate a unique class names such as `myClass` to `myClass__djTxl3`. Notice the unqiue suffix.

### Implementing CSS Modules

Here, you may not use a Sass compiler that generates plain css file. However, in React, it requires you to install `sass` module. Reference: `https://www.npmjs.com/package/sass`

```
sass/
|
|– base/
|   |– _default.scss        # Reset/normalize
|   |– _typography.scss  	# Typography rules
|   ...                  	# Etc…
|
|– components/
|   |– buttons.module.scss  # Buttons Module
|   |– dropdown.module.scss # Dropdown Module
|   ...                  	# Etc…
|
|– layout/
|   |– _navigation.scss  	# Navigation
|   |– _grid.scss        	# Grid system
|   ...                  	# Etc…
|
|– pages/
|   |– home.module.scss     # Home styles
|   |– login.module.scss	# Login styles
|   ...                  	# Etc…
|
|– abstracts/
|   |– _variables.scss   	# Sass Variables
|   |– _functions.scss   	# Sass Functions
|   |– _mixins.scss      	# Sass Mixins
|   ...                  	# Etc…
|
|– vendors/
|   |– _bootstrap.scss   	# Bootstrap
|   ...                  	# Etc…
|
|– style.scss               # Primary Sass file that '@imports' required files.
```

Notice the changes on the file names on the files inside the `components` and `pages` directories. Here, the underscore (`_`) is removed and `module` is inserted to the name (`[filename.module.scss]`). By adding `.module` allows CSS modules to know that a scss file is a module.

Global files such as the `style.scss` cannot be inserted on a JSX component, only the `module` files.

#### Importing module file to a JSX component.

On the top of the `.js` file, import the module file.

```js
import styles from "../path/to/file.module.scss";
```

Then, you can use the classes inside the module file as a property of an object.

```js
...
<h1 className={styles.myTitle}> Hello, my class name is obfuscated. </h1>
...

// class name will be displayed as myTitle__[rand suffix]
```

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
