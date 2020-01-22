# Ionic Print-test

I would like to be able to print a report from Ionic. It should be able to span multiple printed pages. 

The `body`, `ion-app`, `ion-router-outlet`, `app-home`, and `ion-content` elements need some styles overridden for printing (using `@media print`). 

```CSS
@media print {

    body {
        position: relative !important;
        max-width: unset !important;
        height: unset !important;
        max-height: unset !important;
    }

    app-home,
    ion-app,
    ion-router-outlet,
    ion-content {
        position: relative !important;
        contain: unset !important;
    }
}
```

## Problem

Once that is done, everything works fine **except for the `ion-content main.inner-scroll` element**. It needs to be set to `position:relative` to be visible while printing.

In this example app, if you print the home page from Chrome, you'll notice a blamk page. If you then use the developer tools (`F12` or `CTRL-SHIFT-I`) to manually add `position:relative` to the `main.inner-scroll` element, you'll notice the scrollbar disappears in the screen display, but then printing works across multiple pages.

## Solution?

If Ionic adds a CSS variable to the `ion-content .inner-scroll`, this wouldn't be a breaking change, and I would then be able to override this setting when printing:

```CSS
@media print {
    ion-content {
        --inner-scroll-position: relative;
    }
}
```

There may also be a way to inject that style into the page with Javascript, but I haven't figured that out yet.
