# Introduction

## What is Pantarei?

Pantarei is a tiny foundation for building user interfaces for the Web.
Unlike other opinionated frameworks, it's designed to be resilient.  

Pantarei core is focused on the view layer only.  
When used in combination with modern tooling and supporting libraries,  
it's perfectly capable of powering sophisticated Progressive Web Apps.  


## Hello Web!

```html
<div id="app" text="message"></div>  
```

```js
var app = new Pantarei({
  el: app,
  data: {
    message: 'Hello Web!'
  }
})
```

```html
Hello Web!
```

## Key features

### Directives

Pantarei makes the existing (real!) DOM of your app reactive.  
The reactive rendering is driven by directives over the DOM.  
Directives are special attributes that tells the DOM what to do.  
[Read more](/directives.md)

### Custom Elements

Pantarei allows you to build reactive Web components as well.  
Web Components are based on the HTML5 WebCompoents starndards.  
WebComponents allows you to create new Custom Elements.  
Pantarei is add a thin layer of the spec to enable reactivity.  


## Show me the code!

Pantarei is [open source](https://github.com/pantareijs/pantarei) under the MIT License.