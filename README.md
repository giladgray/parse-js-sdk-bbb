parse-js-sdk-bbb
================

Parse.com JavaScript SDK modified (minimally) to work with [Backbone Boilerplate](https://github.com/backbone-boilerplate/backbone-boilerplate) and [LayoutManager](http://layoutmanager.org/).

## Why?
The Parse JS SDK v1.2.8 is not identical to Backbone v1.0.0, but it's close enough that most of the time it doesn't matter to the LayoutManager plugin. Except in one little situation: `Parse.Events` and `Backbone.Events` are implemented quite differently and do not have the same interfaces, so the LayoutManager errors consistently when removing views. In particular, `Parse.Events` is missing the `stopListening()` function.

The solution? Fork the SDK and monkey-patch it with `Backbone.Events`!

## Usage
```
# Install from Bower
$ bower install parse-js-sdk-bbb --save
```

```coffeescript
# If using RequireJS, put the following in the shim block:

# A dirty little trick where we pretend Parse is actually Backbone,
# so the LayoutManager doesn't get confused. You can use either the
# Parse or Backbone object in your app, although we'll continue to
# call it Backbone in this generator.
backbone:
    exports: 'Parse'
    init: ->
        @Backbone = Parse
        @Backbone.Model = Parse.Object
        @Backbone


