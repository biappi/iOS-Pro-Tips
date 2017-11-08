iOS Pro Tips
============

This repo contains an unordered collection of advice for iOS
programming.

Every tip stems from real production code seen in the wild.

It is intended as a living document.

Instead of -- or in addition to -- shouting on twitter,
consider clicking the
[pull request button](https://github.com/biappi/iOS-Pro-Tips/pull/new/master).

> Stop trying to hit me, and hit me.

General
-------

Try hard to not replicate your deployment's target base functionality. Some times it's appropriates, often times is not.

Do not introduce new abstractions until absolutely necessary, bad abstractions prevent extending software without bending themselves.

Modeling a state machine, the concept of an Event is as important and maybe more importan than the concept of a State. Pay attention to it.

Don’t let indices surface in your APIs. Get the thing, pass the thing along. Don’t tell anybody where the thing is.

Naming
------

Do not include "etcetera" in your symbol name. (Yes, Actually seen in production code)

When dealing with structured identifiers from other systems (URLs for example) do not replicate the construction logic, use plain strings. (e.g.: `get_url("https://example.com/v1/data.json")` instead of `get_url(SERVER + VERSION + endpoint_name + SERIALIZATION)`)

If you find having a symbol named `numberOfSomething` consider calling it `somethingCount`

Name your instance variables for what they do, not for what they are. (e.g.: `enableThingButton` instead of `toggleButton`)

Lifecycle
---------

Your initial view controller should be decided in didFinishLaunchingWithOptions. The data to base the decision on is already in the AppDelegate, moving the responsability away from it would mean also moving the data with it.

Initializers and deinitializers (aka: constructors and destructors) should be side-effects free. e.g.: not reading files, not subscribing to observers...

UI
--

UIView subclasses should not communicate to other collaborators their size change.

If an UIView subclass has both a "setState" method, and does respond to UI events, it should not change state from it's ui events callback, it should always do a roundtrip to the viewcontroller it's presented in.

Datasource updates and user interactions are different things, and must follow different code paths.

When working with designers, do not try to replicate in code any design guideline. Leave designers the option to break their own rules.
