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

Pantarei add a further reaction to the ones predefined by the custom element spec.
When the component is ready, that is, when its content is set and reactive,  
the `ready` callback is called.


## Element upgrades

We've already learned that custom elements are defined by calling `customElements.define()`.  
But this doesn't mean you have to define and register a custom element all in one go.  

Custom elements can be used before their definition is registered!
Progressive enhancement is a feature of custom elements.  

In other words, you can declare a bunch of `<my-component>` elements on the page  
and never invoke `window.customElements.define('my-component', ...)` until much later.  

This is because the browser treats potential custom elements differently, thanks to unknown tags.  
The process of defining a new custom element, calling `customElements.define`,  
and endowing an existing element with a class definition, is called "element upgrades".


## Attributes

TODO

## Properties

