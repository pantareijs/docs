# Components

Components are one of the most powerful features of Pantarei.  
They help you extend basic HTML elements to encapsulate reusable code.  

Pantarei Components are based on the HTML5 WebComponents standards: 

- Custom elements
- Templates
- Shadow DOM  
- HTML Import

## Define a new component

To define a component, you create an ES6 class and associate it with the component name.

```js
class MyComponent extends HTMLElement { }

window.customElements.define('my-component', MyComponent)
```

You can use a component just like you'd use a standard element.  
The following are equivalent:

```html
<my-component></my-component>
```

```js
const component = document.createElement('my-component')
```

```js
const myEl = new MyElement();
```

The element's class defines its behavior and public API.  
The class must extend HTMLElement or one of its subclasses (for example, another custom element).  

To take advantage of the powers of Pantarei, like the directive-driven reactivity,  
your component class must extend the `Panterei.Element` class. 

```js
class MyComponent extends Pantarei.Element { 

  static get is () { return 'my-component' }

}

window.customElements.define(MyComponent.is, MyComponent)
```

### Components name

By specification, the custom element's name must start with a lower-case ASCII letter and must contain a dash (-).  
There's also a short list of prohibited element names that match existing names.  
For details, see the [Custom elements core concepts](https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements-core-concepts) section in the HTML specification.

It's convenient for the component class to have a static getter `is` to get the name of the component.

