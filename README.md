UI Sass Utils
===

This library provides a simple, consistent interface for getting and setting configuration objects across a Sass project.

---



### How To

#### Install

This repo is designed to be consumed as a [Bower](https://bower.io/#getting-started) component. To use it, run this command:

```bash
bower install -D https://github.com/rafegoldberg/sass-map-deep-set.git#master
```

Wahoo! Now the `ui.sass.utils` repo lives in your project's `bower_comoponents` directory.

#### Import

Once you've got the repo installed, the next step is to include the main partial in your Sass project:

```scss
@import 'ui.sass.util/import';
```

Since you want to be able to access the config in your other partials, you'll probably want to `@import` the utils near the top of your Sass structure.

> **Note**: figuring out the relative path to your Bower components can be a bit trickier than the above example suggests. But since it really depends on the build tools and Sass workflow you've chosen, I'll leave it to you to figure out.



### Usage

Once you've imported the utils in to your project you're ready to get started! Beyond the helper functions in `lib/`, these utils also provide an interface (aka a couple of functions) to help manage a Sass project config object. At the moment the functionality is limited to get and set methods; more to come.

#### Adding to the Config

To add an object to your config, use the `Ds-add()` function as follows;

```sass
$ui-conf-variable-ref: Ui-add(name,(
  prop: #F00,
  deep: (
    nested: (
      key: "hi, I'm deeply nested!",
      alt: "hey, me too!"
      ))
  ));
```

> **Note**: in the above examples the return value of the `Ui-add()` call is assigned to variable. Since the method returns the passed object, the refrence variable will be identical to the new config object. Since Sass only permits function calls from the right-hand side of a assignment variable or property assignment statement

###### Real World Example

Here's one real-world example of using the `Ui()` and `Ui-add()` methods to set up a [modular-scale sass plugin](https://github.com/modularscale/modularscale-sass):

```sass
//-file-> ./sass/conf/_scale.scss
$ds-scale: Ui-add(scale,(
  base: 1em,
  ratio: (1.5,1.25)
  ));

//-file-> ./sass/libs/_modular_scale.scss
@import 'modular-scale/stylesheets/modular-scale';
$ms-base: Ui(scale,base);
$ms-ratio: Ui(scale,ratio);
```


#### Retrieving Config Values

To get a config object or a sub-value, use the `Ui()` function:

```sass
.example {
  conf-obj: Ui(name);                 //=get a config object
  deep-val: Ui(name,deep,nested,key); //=or pass keys to get deep conf vals
}
```



### Roadmap

- [x] rename this repository to `ui-sass-utils`