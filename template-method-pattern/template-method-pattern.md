# Template Method Pattern

Design patterns are a non-fundamental piece of software engineering. They are named and used not by their concrete examples, but by the patterns that have been developed over time. They are used to help write cleaner, and more extensible code. 

The **Template Method Pattern** is used often in frameworks, such as React and Ruby On Rails, however it can be used to great effect in re-useable software written specifically for your own applications.

## What is it?

The **Template Method Pattern** is a behavioral pattern used to define an algorithm that has very specific steps, but each step may vary in it's implementation. This pattern relies on having an abstract base class that has abstract methods to be overwritten by the child classes, and a method that runs each of those overwritten methods in a specific order.

Below is some code that outlines a few of the concepts on this pattern.

~~~javascript
class FunkySong {
  play() {
    this.intro();
    this.verseOne();
    this.chorus();
    this.verseTwo(); 
    this.chorus();
    this.instrumentSolo(); 
    this.chorus();
    this.verseThree();
    this.chorus();
  }

  intro() {
    throw new Error("'intro' Not implemented")
  }

  chorus() {
    throw new Error("'chorus' Not implemented")
  }

  verseOne() {
    throw new Error("'verseOne' Not implemented")
  }

  verseTwo() {
    throw new Error("'verseTwo' Not implemented")
  }

  instrumentSolo() {
   // Do nothing if not implemented in child class
   // This is an optional method, or "hook"
  }

  verseThree() {
    throw new Error("'verseThree' Not implemented")
  }
}

class MyFunkySong extends FunkySong {
  constructor() {
    super();
  }

  intro() {
    console.log("🎶 Smooth Jazz plays while you read this 🎶");
  }

  verseOne() {
    console.log("🎶 I'd write a song, but I'm a programmer 🎶");
  }

  chorus() {
    console.log("🎶 Nobody would listen to my music anyway 🎶");
  }

  verseTwo() {
    console.log("🎶 I'd write a song, but I have no musical talent 🎶");
  }

  verseThree() {
    console.log("🎶 I'd ask you to forgive my cheesy joke here, and terrible prose, but... 🎶");
  }
}

const myJam = new MyFunkySong();
myJam.play(); // This runs all the other methods we defined in the MyFunkySong class
~~~

Notice how we do not overwrite the `play` method while defining a sub-class? This is to help us re-use our algorithm to do some sort of process. Overwriting `play` defeats the purpose of using this pattern.

Just as a song has defined portions that need to happen in a certain order, our template method makes sure this happens. It would be pretty strange if our song played out of order. 

You may notice I didn't add the `instrumentalSolo` method to the child class, this is optional for songs, so it's optional for our template method. Classes that take advantage of the **Template Method Pattern** often have methods that do not need to be implemented, these are called "hooks" as they hook into the currently running process, "lifecycle hooks" is another way to define these. Hooks can be both synchronous and interrupt the flow of the currently running process and modify data (or any other number of operations), or be asynchronous and be used for reporting the status of the currently running operation.


## Where is it used?

As I mentioned before, this pattern is used often in class-based frameworks. If you're familiar with React's class based syntax for creating components, you will be familiar with the life-cycle hooks. These hooks are called by React itself via a template method during the lifecycle of the component. `render` itself is something we overwrite from the base class. 

This pattern can also be used in every-day code whenever you need to run a "process", but change the implementation of parts of that process. This may remind you of the **Adapter Pattern** but it is distinctly different as the **Adapter Pattern** is defined in a way to make related, but different, APIs into a singular API. 

## Example Case Study

Below is a link to an example that can be played with and run.

https://repl.it/@I3uckwheat/Template-method-pattern#index.js

This example is one way you could create a file-uploader that can handle different types of files. Pay close attention to the base class `FileUpload` and take note at how there are "hooks" and mandatory methods. Hooks are used to run operations during the process of the defined algorithm (such as starting a loading indicator, then later stopping it), `uploadingFile` and `finishedUploading` are examples of hooks. 

The most important part of this pattern is throwing errors on things that *need* to be implemented. Failing to do so, can make it difficult for future developers to know what is wrong with the application. 

In the example, you can clearly see the complexity of each implementation differs, and can differ as much as it needs to. 

## Conclusions

You may recognize this pattern in your own code, even if you're not explicitly using it. This pattern is one that lends itself naturally in OOP, but being aware of it's advantages and definition, can help you use it more deliberately and effectively. It's a fairly simple pattern, but a very powerful one.

## More Resources

* https://sourcemaking.com/design_patterns/template_method
* A very cool example in Ruby: https://repl.it/@rlmoser/TemplatePattern-Coffee#main.rb
* A long video, but is mostly useful to understanding this pattern up to the 20 min mark: https://www.youtube.com/watch?v=7ocpwK9uesw
