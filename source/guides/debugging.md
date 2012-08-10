# Debugging Ember

To improve as a developer, a developer has to become better with the tools the
he is using. Effective debugging is one of the most important skills to have and
nuture. Improving your debugging con-fu with Ember is what this guide is about.

## General Tips

The most effective debugging skill is to avoid bugs in the fist place:

 * following a good styleguide for your code and have good naming conventions. 
 * Use `var` declararions for your variables because you might leak variable
   names in the global namespace leading to very hard to debug bugs.
 * Use [jslint][2] or [jshint][3] while coding. They provide you helpfull guidance and help you avoid
   common pitfalls.

If you have an hour to spare watch [debugging emberjs][1].

### Read The source

Knowing the "how" of the objects you work with will take away a lot of the
guessing and make you a very confident hacker. So Read the source during
developent if things don't work as expected. Reading the source is easy if you
avoid using the minified version of Emberjs during development. The non minified
version of Ember also contains a lot of assert statements helping you avoid
errors and gives you hints and the ability to follow the stacktrace in case of
an error more easily.  Reading the source can be somewhat intimidating in the
beginning, but there are a ton of
those "AH-HA" moments hidden in the source which will make it worth the effort.

### Javascript console

Most of you will know this, but for the people who are new to js development,
find out how to acces the console in your browser of choise.

### logging

`console.log` is the most usefull command to find out whats going on.  With
`console.log(variable)` one can inspect any variable.  variables often used are `this`,
`context`

## Ember related.

### Debugging handlebars templates.

Use `{{ log }}` and `{{ debugger }}` in your templates to find out why stuff is
not printed.

### Getting access to a View instance. 

Views are instances of the views you created in your code. They are not
singletons you can easily access and thinker with. To get access to a specif
View you have to look at the DOM tree in your browser.  find the id of the view
you want to debug and lookup it's id field in `Em.view.views`.  

```
 <div id="ember667" class=​"ember-view" > 
``` 

Now in the console you can get access to the view instance by `Em.view.views["ember667"]`.

### break on error

learn to put the js debugger in break on error. You can do that by making the break 
button in the javascript console purple.

### ObeserveBefore.

If you need to find out when a binding is set use `ObeserveBefore` in
combinations with a `debugger` statement. This way you have a usable stacktrace
pointing you to the 'cause'.

## Advanced

### Window.billy

If you need to debug a higly used part of your code but only need to debug it
under some conditions. Use a conditional debugger statement:

```
someView = Em.View.extend({
  buggyMethod : function(arguments){
       //only if window.billy is set the debugger is activated.
       //usefull when method is used a lot and only fails sometimes.
       if ( window.billy ) { debugger; }
       ..more code..
  })
})
```

## If All Else Fails 

The most anoying kinds of bugs are the ones without a usable callstack or
complete lack of even an error.  

### Devide and conquer

Devide and conquer is the last resort to finding the cause of an bug.  
The only option left to
do is to disable more and more of your code until you have singled out the
malfunctioning piece of code.

If you still can't solve it yourself, ask at stackoverflow, irc and finally make
an issue on github accompanied with a jsFidle so the true js gods will bother to
look at it and fix it.
 

 [1]: http://vimeo.com/37539737
 [2]: http://www.jslint.com/lint.html
 [3]: https://github.com/jshint/jshint/
