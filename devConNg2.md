#  Why Angular? (10 min)

## What is Angular? (2 min)

Javascript framework built around creating components with a clear distinction between the DOM and the business logic then letting Angular handle the binding between them (MVC/MVVM).

Javascript framework for creating an MVC-type front-end. It consists of components (formerly directives) which are split into HTML and Typescript pieces, with Typescript services for communication, be it with another component or an external web service.



Angular simplifies much of the "Controller" part of the MVC paradigm with simple bindings that cut down on boilerplate.









## What's new with Angular2? (8 min)

Typescript (with es6) and simplified syntax are the most immediately apparent changes.



​	Typescript adds typing to javascript, allowing a lot of checks to be made ahead of time during compilation and writing, enabling the catching of many bugs before runtime, as well as allowing IDE's to better understand code being written, leading to support of many features typically missing from javascript development, such as autocomplete and assisted refactoring. This, combined with features added in es6 such as imports and Sets create an environment much more familiar to Java developers that still maintains the flexibility of javascript.



​	The syntax is also much simpler and more intuitive. AngularJS provides a plethora of directives to provide quick ways of doing common tasks. However, many of these directives merely set attributes under a specified condition and are no longer needed with Angular2's attribute bindings. Things like ng-show/hide or ng-click are replaced by simply adding your own bindings to HTML attributes like hidden or click (the HTML event), e.g. ng-click gets replaced with (click).



DISCLAIMER: while ng-hide is *essentially* the same as [hidden], it is slightly different in that it adds some extra css. Officially, it is not recommended to use [hidden] as it is not guaranteed to hide elements if there are other css rules setting the display property. Unofficially, set display for hidden elements yourself and you're just fine (i.e. .hidden{display:none !important;}).



​	The new binding syntax is much more transparent, and also has the benefit of putting the direction of the binding in the hands of the consumer of the component, rather than the creator. In Angular 1.x, directives declare their inputs with one of a handful of annotations that denote what type of input it is. These types were easy to confuse, and loosely correlated to a directionality of the binding, but with subtle differences that could lead to errors from using the wrong type. Since they were declared in the component,  users of the component didn't have much freedom for customization. With the new syntax, the "type" of the input is more in the hands of the consumers of the component, so they don't need different versions with different types. Plus, who can remember which type is @ and which is &?





















# Our Experience with Angular (15 min)

## What we've liked (8 min)

Using Angular. Really, it's quite pleasant. 



No more dealing with isolated scopes. In addition to not having to track what the different modifiers mean (@,=,& ?), we don't have to build up our own scope to make a call into another component.



## What we've hated (7 min)







### UPGRADING!!!

2.0.0-rc.1 --> 2.0.0-rc.4 --> 2.0.0-rc.5

Quick and painless, right?



Think again. Lots of breaking changes, even new modules getting split out from the core projects. Most of our upgrades took the better part of a week.





#### Ok, I'll just stay on the older version

Well, that doesn't really work, either. The Angular team doesn't maintain links to the older versions of their documentation, so if you need to look at the tutorials to see how to use a feature you're needing to add, you can expect it to only work if you upgrade to latest (since as mentioned, there's lots of breaking changes, so it's likely quite different from the version you're using).







# Should I switch? (5 min)

Most of the core functionality has been implemented in Angular2. The only real detractors are the lack of apps available using Angular2/typescript, such as material design (not all Angular 1 libraries can upgrade) and the upgrade pains.

Upgrade pains may be a thing of the past, we'll see

### Factors for

### Factors against





