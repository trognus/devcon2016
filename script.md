# Title slide

Hello, and welcome to Angular 2 w/ Typescript and Rx Javascipt. My name's Troy Briggs, I'm on the Internal Tools team, where we use Angular 2 for our account configuration tool.



# Overview

I'll start out with a quick overview of what Angular is, followed by what's new in Angular 2. From there I'll be moving on to our experiences with Angular2, what we've liked and disliked with it, after coming from using Angular 1.x for our most recent projects. And, lastly, I'll go over the state of the project, and whether or not we think it's a good time to switch to Angular 2



# What is Angular?

So what is Angular? Angular JS is a javascript framework built around the use of components. These components consist of an HTML template, a javascript controller, and, optionally, a stylesheet. It's important to note that these stylesheets are utilized in such a way as to keep the styling for components compartmentalized, so any rules defined in one component aren't applied to other components (this can be done by emulating the Shadow DOM, which is the default behavior, or actually utilizing it natively).



The communication between the HTML template and the javascript controller is handled via simple bindings in the template. In Angular 1.x these were mostly done via custom directives or custom attributes on components, but Angular 2 uses a new syntax that really simplifies the written code, which I'll be showing in a moment.



And finally the communication between components is largely handled by Observables in services, which are also what is returned when making web service requests via Angular's http module. These observables replace the Promises that Angular 1.x and many other javscript services use.



# Angular Diagram

Here we can see the general layout of Angular apps. The HTML template and styesheet(s) make up the view, which can update the client-side model directly, or through the javascript controller, with the communication between the view and the model being handled by Angular through the bindings. The communication with web services is also shown here, and is handled by Angular's http module. Web calls are expected to return JSON, which will then get served back to the controller in the form of Observable events.



# What's new with Angular 2?

One of most immediately apparent changes is that Angular 2 uses typescript, which uses es6. It also incorporates Reactive programming with the javascript implementation of Reactive extensions, RxJS (not to be confused with Facebook's UI library, React, which is something entirely different.) In addition to these technology changes, Angular 2 strives to be more modular, and has an increased focus on performance, in order to make Angular more viable for mobile development. And, as I touched on briefly, there's some syntactical differences that simplify Angular2 code. These also have the benefit of making many of Angular 1.x's custom directives obsolete.

So, let's take a look at what we're getting with these.

# Typescript

Typescript, as you likely guessed from the name, is meant to be javascript with typing. By adding types to our variables, method return signatures, and arguments, we can get a lot more compile-time error checking, as well as improved IDE support. Typescript also incorporates a few other common programming elements, such as classes and lambdas, expanding the OO and functional capabilities of javascript, respectively. Typescript also uses es6, the latest (ok not latest, as of June, this is the ever-changing world of javascript after all, but one of the latest) versions of ECMA Script, which javascript implements. Among the new features of es6 are a new import syntax, replacing requires, and the For/Of statement. Anyone familiar with javascript should know of For/In statements, which are similar to the advance For loops seen in, for instance, Java, but have some important distinctions that make them prone to bugs due to incorrect usage. The For/Of statement, however, more closely resembles this advanced For loop, and is intended to be used to iterate through collections.

# Mini Demo

Here we can see some of the Typescript syntax. The myThings object has type of MyThing array (this can also be declared using the tag syntax commonly seen in Java). In fact, Java developers should feel very at home with Angular 2. Between the new imports, the types, and the classes, typescript feels a lot like Java, albeit with a bit less boilerplate. It still, however maintains the flexibility of javascript thanks to the "any" type which acts like a traditional javascript object, making Typescript more of an opt-in system.

The method here is typical of web service calls in Angular 2. Here, getThings is returning an Observable, which we then subscribe to, passing a function to get called on the returned json data. For that function, we're using a lambda using the arrow syntax which does not bind it's own this but rather maintains the scope of the caller, so there's no more need to bind to a "self" object.

 # RxJS

RxJS is built around objects known as Observables, which are similar to Promises, but with a lot of additional functionality. They are what Angular http calls return, and they are often used for communication between components. They also can be used to replace watches and event buses. 

These Observables are highly configurable through the use of chaining different operations on them.  For this first example we can see an "event bus" type Observable. We can simply add a debounce to cut down on excessive, duplicate events, filter out events of types we don't want, and specify a method to be called when events do come through and pass the filter (here, since we are using the event as a trigger and don't actually need it, anymore, we're ignoring it and using this empty argument syntax). In the second example we can see how Observables can be used to manipulate collections, much like streams. It's important to note that the objects getting passed along in these events are shared amongst subscribers, but the chains of methods are kept separate, so, for instance, if someone else subscribed to this eventQueue Observable prior to the filter, they would also see the same events coming through, though without the filtering to only create events. Since these events are shared, there is potential for unwanted side effects if you make changes to the objects being passed along as events.

# Demo Code

So here we can see a more fleshed out component. You've got your imports and component class in the javascript file on the left, and the HTML template on the right. This template is tied to the component via an annotation property, here (templateUrl, though you can also define the template here inline, as is often needed in library components where it is common to compress all the javascript into a single libary file. The same can be done for the css). Here we can see the constructor, with the dependant objects, which Angular will be injecting for us. Note that these don't need to be declared outside of the constructor to be used outside of it, but rather keep the scope more typical to javascript. 

Here you can see the router at work; simply call router.navigate and pass in the route you want to direct to (as defined in our bootstrapping file) and Angular will handle the rest.

Over here we have the template. ngFor is used as a replacement for ng-repeat, and here we have the basic usage, though there are expanded forms, such as for when you need to maintain the index of the elements you're iterating through. The double curly braces here allow us to call javascript code directly from the DOM, from the context of the component. Here we see the new binding syntax that Angular 2 uses, with ngModel being two-way bound to myThing's name. By leaving off the square brackets for these buttons, we now have eventlistener's on the click event. Note that while ngModel is one of the few custom directives that is kept in Angular 2, we no longer need ng-click, as we can now just bind to the base HTML click event.

# Demo bootstrap

A lot of the initial configuration is handled in a bootstrapping file like this one. Here, we setup our routes for the router, declare dependencies that will be injected, and define providers for our various services. One thing to note is that Angular 2 recently added the idea of modules for dependencies, so instead of declaring your dependencies on a per-component basis, you declare what module your component is in, and declare dependencies at the module level.

# Our Experiences with Angular: Pros and "Khan"s

So, now that you have a basic understanding of what Angular 2 brings to the table, let's talk about what we've liked and disliked about developing with Angular 2. I like to end on a high note, so we'll start with the "Khan"s.

# Khans

The biggest "Khan" so far has definitely been upgrading our Angular dependency. The Angular project has been shifting a ton throughout the alpha, beta, and even RC stages, with lots of breaking changes throughout. This, combined with the fact that we only have our explicitly declared version of Angular, not a separate version for each library we use that also depends on Angular means that any version Angular-version discrepencies will almost surely result in build or runtime failures.

# Bad News

The breaking changes have been brutal thus far, making beta development really rough. Even seemingly safe versions, such as the rc builds, have had several breaking changes, even going so far as pulling entire modules out to stand on their own, namely the router and forms modules.

Normally, this problem would be mitigated by simply sticking with an older version until you need something in a newer one. However, there is a problem with this, in that the tutorial docs are always kept updated to the latest version, with no apparent links to older versions. This means that if you've needed to refer to the documentation to see how to use something, you'd either need to be using the latest version or look to others' experiences. For this, Stack Overflow has been our saving grace, as we could almost always find where someone else had been running into the same problem and was helped by either an Angular developer, or someone who had done that thing before and after the breaking change.

This has created somewhat of a love-hate relationship with Google for us, as Google was now our friend, but we were only in this situation because of what Google had done to us.

# Good News

The good news is that Angular 2 has been officially released, so hopefully these issues are a thing of the past.

# Angular claims SemVer

With the release of 2.0, the developers of Angular apologized for the turbulent state of the Angular codebase, particularly with regards to their breaking changes in RC builds, and has pledged to adhere to semantic versioning going forward. This means there should be no breaking changes outside of major releases, which are scheduled to be 6 months apart. Hopefully, this will mean a less turbulent code base and better historical documentation, but as this is such a recent development, only time will tell. They have released 2.1.0 and it is considered a drop-in replacement for 2.0.x, so thus far it looks like they're sticking to their claim.

# Pros

So, now that I've gone over what we've disliked about developing with Angular 2, let me talk about what we have liked: pretty much everything else.

Typescript has been particularly nice for development. It's great having autocomplete in a javascript IDE, especially when I'm used to writing code in either Netbeans for Java or SQL Studio for SQL. With other javascript environments, including Angular 1.x, if I was unsure of what method it was I was wanting to call, or had a question about the arguments, I usually either relied on the Chrome debugger or looking up documentation. Having good syntax coloring and error highlighting has also been quite a boon.

# Binding syntax

The new binding syntax has also been quite pleasant, and significantly reduces the learning curve for new Angular developers. You simply use parentheses for sending data from the template to the controller and square brackets for going from controller to template. You can combine these to create basic two-way bindings, or leave them all off to set to a static value. That's it. No more having to keep track of the isolated scope types and remember what @, =, or & meant, as these loosely correlated to these directional bindings, but had some nuanced differences.

# Directives b gone

With the simplified syntax, many of the old custom directives are no longer needed, further reducing the learning curve for Angular, as you no longer need to memorize all these custom directives, but rather can just bind to plain HTML properties. As mentioned earlier, ng-click is replaced by a parenthetical binding on the click event, just as ng-href is replaced by a square bracket binding on the href property. Ng-show and ng-hide are also no longer needed. They can be replaced by either binding to the hidden property, or using an ngIf to conditionally display the element. Note that in Angular 1.x, ng-hide didn't just set to display:none like hidden does, but also set it to !important. For this reason, some consider it erroneous to bind to hidden as it can potentially be overridden by another CSS rule and instead recommend using ngIf determine if the element is displayed. Personally, I prefer to bind to hidden and simply set a global css rule for hidden to display:none !important to make it more like how Angular 1.x was. This is because a) I think it looks better and prefer using bound HTML properties over custom directives and b) using ngIf will remove the element from the DOM, and destroy any of its components, so you lose state held by that element.

# RxJS Methods

One last thing we've really liked is all the functionality that RxJS provides. Here I've listed some of the main methods we've found useful.  I will note, however, that while the new Angular2 syntax helps give Angular2 a more shallow learning curve, RxJS, or rather Reactive Extensions in general, has a rather steep learning curve. Hopefully Reactive programming will become more and more common outside of Angular development, making this less of an issue, but I will say that if you're considering using Angular2, I highly recommend going to Michael's presentation on Reactive programming. That being said, these are some of the methods we've commonly used. Map is typically your go-to transformation, and should generally be used in lieu of do, as do does not use the return value of the passed in function, which encourages modifying the event passed in, leading to unintended side effects. Merge is useful for combining Observables such that an event is triggered when any of the originating observables produces an event. ForkJoin is another way of combing Observables, but waits for all the passed in Observables to return an event, then combines their results into an array of event objects. Flatmap, on the other hand, is used for splitting collections of items into separate events.

# Should I switch?

So, now that I've gone over the pros and cons of Angular 2, the only question left is whether or not it's worth switching to.  If you're using Angular 1.x, you should know that pretty much all the core functionality is there, and the project is mostly stable. Also, Angular 1.x has been officially deprecated, with support going to Stack Overflow, so the answer is definitely yes.

If you're coming from something other than Angular 1.x, I'd ask do you like the idea of developing under a unified framework with a fairly large, and rapidly growing userbase,  produced by a leading tech company with plenty of resources that also happens to develop one of the most popular browsers, uniquely positioning itself to really drive javascript development (by which I mean development of the language, not developing in that language). If so, then Angular 2 is for you. If you don't like frameworks you can stick with your choice of libraries glued together in a hopefully-not-frankenstein kind of way. Or if you just don't like Angular 2, maybe try your hand at something like Elm.

I, for one, am glad to be developing in Angular 2. While I may feel a little battered and bruised after dealing with Angular 2 in beta, The clouds appear to have parted, and everything else about Angular 2 has been a vast improvement over every other javascript ecosystem I've used.