# Scaling all the texts

As apart of the process of making our apps more accessible, we want to scale the text so the visually impaired.

On Android the texts on labels and buttons is scaled automatically, we don't need to do anything to support it. We might want to fix the layout when this happens.

On iOS on the other hand doesn't scale the text automatically, on iOS 10+  *adjustsFontForContentSizeCategory* can be used on a UILabel to have it scaled.
Unfortunately this only works for prefered fonts. which is difficult to set from NativeScript.

Luckily **@nota/nativescript-accessiblity-ext** now supports font scaling via CSS.

## Getting started

Start by creating a new NativeScript project. I'm using Angular, but it will work just as well with NativeScript Core.

```bash
tns create projectname --ng

cd projectname
npm i
npm i --save-dev nativescript-dev-sass
npm i --save @nota/nativescript-accessibility-ext@^3.0.0-alpha.7 nativescript-globalevents
```

Create the SCSS files for the [nativescript-theme-core](https://docs.nativescript.org/ui/theme#sass-usage)

### app/_app.common.scss
```sass
// Import the theme’s variables. If you’re using a color scheme
// other than “light”, switch the path to the alternative scheme,
// for example '~nativescript-theme-core/scss/dark'.
@import '~nativescript-theme-core/scss/light';

// Customize any of the theme’s variables here, for instance $btn-color: red;

// Import the theme’s main ruleset.
@import '~nativescript-theme-core/scss/index';

// Place any CSS rules you want to apply on both iOS and Android here.
// This is where the vast majority of your CSS code goes.
```

### app/app.android.scss
```sass
@import 'app-common';
@import '~nativescript-theme-core/scss/platforms/index.android';
```

### app/app.ios.scss
```sass
@import 'app-common';
@import '~nativescript-theme-core/scss/platforms/index.ios';
```

Now import the a11y-scss from **@nota/nativescript-accessiblity-ext**:

Add this to `app/app.ios.scss`:
```sass
@import '~@nota/nativescript-accessibility-ext/scss/a11y.ios.scss';
```

Now we need to load import the plugin in our `app/app.module.ts`

Add this:
```typescript
import { NgModule, NO_ERRORS_SCHEMA } from "@angular/core";
import { NativeScriptModule } from "nativescript-angular/nativescript.module";
import '@nota/nativescript-accessibility-ext'; // <-- this line
```

## Screenshots

**Witout scaling/default scale level**
![Without scaling](images/1-without-scaling.png)

**Scaled to 150%**

![Scaled to 150pct](images/2-with-scaling.png)

