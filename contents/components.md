# Components

Components are one of the most powerful features of Pantarei.  
They help you extend basic HTML elements to encapsulate reusable code.  

Pantarei Components are based on the HTML5 WebComponents standards: 

- Custom elements
- Templates
- Shadow DOM  
- HTML Import

## Component definition

To define a component, you create an ES6 class and associate it with the component name.

```js
class MyComponent extends HTMLElement { 
  // ...
}

window.customElements.define('my-component', MyComponent)
```

The element's class defines its behavior and public API.  
The class must extend HTMLElement or one of its subclasses (for example, another custom element).  

To take advantage of the powers of Pantarei, like the directive-driven reactivity,  
your component class must extend the `Panterei.Element` class. 

```js
class MyComponent extends Pantarei.Element { 
  // ...
}

window.customElements.define('my-component', MyComponent)
```


### Components name

By specification, the custom element's name must start with a lower-case ASCII letter and must contain a dash (-).  
There's also a short list of prohibited element names that match existing names.  
For details, see the [Custom elements core concepts](https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements-core-concepts) section in the HTML specification.

It's convenient for the component class to have a static getter `is` to specify the name of the component.

```js
class MyComponent extends Pantarei.Element { 

  static get is () { return 'my-component' }

}

window.customElements.define(MyComponent.is, MyComponent)
```


## Component usage

To use a component is just like using a standard element.  
The following are equivalent:

```html
<my-component></my-component>
```

```js
const component = document.createElement('my-component')
```

```js
const component = new MyComponent();
```


## Component lifecycle

The custom element spec provides a set of callbacks called "custom element reactions"  
that allow you to run user code in response to certain lifecycle changes.

### Create
When the element is "upgraded", that is, when it's created or when a previously-created element becomes defined,  
the `constructor` is called.

The element constructor has a few special limitations:

- The first statement in the constructor body must be a parameter-less call to the `super` method.
- The constructor can't include a return statement, unless it is a simple early return (return or return this).
- The constructor can't examine the element's attributes or children, and the constructor can't add attributes or children.

### Connect
When the element is added to a document  
the `connectedCallback` is called.

### Disconnect
When the element is removed from a document  
the `disconnectedCallback` is called.
    
For each reaction, the first line of your implementation must be a call to the superclass constructor or reaction.  
For the constructor, this is simply the `super()` call.

```js
class MyComponent extends Pantarei.Element { 

  static get is () { return 'my-component' }

  constructor () {
    super()
    console.log(`${this.constructor.is} created!`)
  }
  
  connectedCallback () {
    super.connectedCallback()
    console.log(`${this.constructor.is} added to ${this.parentNode}!`)    
  }

  disconnectedCallback () {
    super.disconnectedCallback()
    console.log(`${this.constructor.is} removed from ${this.parentNode}!`)    
  }

}

window.customElements.define(MyComponent.is, MyComponent)
```

### Ready 

The custom elements specification doesn't provide a one-time initialization callback.  
Pantarei provides a `ready` callback, invoked the first time the element is added to the DOM,  
and so it's ready to be uses.

The `Pantarei.Element` class initializes your element's template and data system during the ready callback,  
so if you override ready, you must call `super.ready()` at some point.

When the superclass `ready` method returns, the element's template has been instantiated  
and initial property values have been set. 


```js
class MyComponent extends Pantarei.Element { 

  static get is () { return 'my-component' }

  //...
  
  ready () {
    super.ready()
    console.log(`${this.constructor.is} is ready!`)
  }
  
}

window.customElements.define(MyComponent.is, MyComponent)
```


### Element upgrades

We've already learned that custom elements are defined by calling `customElements.define()`.  
But this doesn't mean you have to define and register a custom element all in one go.  

Custom elements can be used before their definition is registered!
Progressive enhancement is a feature of custom elements.  

In other words, you can declare a bunch of `<my-component>` elements on the page  
and never invoke `window.customElements.define('my-component', ...)` until much later.  

This is because the browser treats potential custom elements differently, thanks to unknown tags.  
The process of defining a new custom element, calling `customElements.define`,  
and endowing an existing element with a class definition, is called "element upgrades".


## Templates

For those unfamiliar, the `<template>` element allows you to declare fragments of DOM  
which are parsed, inert at page load, and can be activated later at runtime.  
It's another API primitive in the WebComponents family.  
Templates are an ideal placeholder for declaring the structure of a component.

```
<template id="my-template">
  <style>
    p { color: coral; }
  </style>

  <p>I'm in Shadow DOM. My markup was stamped from a template</p>
</template>
```

```js
class MyComponent extends Pantarei.Element { 

  static get is () { return 'my-component' }

  static get template () { return document.getElementById('my-template') }
  
  ready () {
    super.ready()
    console.log(`${this.constructor.is} is ready!`)
  }
  
}

window.customElements.define(MyComponent.is, MyComponent)
```

## Custom attributes

TODO


## Custom properties

Every component instance has its own isolated scope.  
This means you cannot (and should not) directly reference parent data in a child component's template.  
Data can be passed down to child components using props.  
A prop is a custom property for passing information from parent components.


## Component composition

As indicated by their name, components are expected to be composed.
