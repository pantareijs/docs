# Introduction

## What is Pantarei?

Pantarei is a JavaScript Web framework for building user interfaces.  
Unlike other opinionated frameworks, it's designed to be resilient.  
The core library is focused on the view layer only.  
When used in combination with modern tooling and supporting libraries,  
it's perfectly capable of powering sophisticated Progressive Web Apps.  

## WebComponents

Pantarei is based on WebComponents.  
WebComponents allows you building new custom elements.  

## Directives

Pantarei reactive rendering is driven by directives.  
Directives are special attributes that tells the DOM what to do.  

Pantarei core comes with a minimal set of built-in directives:
- attribute
- property
- text
- event
- repeat

Pantarei directives can be easily customized and extended.  
Create new directives, or modify the existing ones, is straightforward.  

### Example

```html
<template-element id="my-app">
  <template>
    <div text="message"></div>
  </template>
</template-element>

<script>
  class MyApp extends pantarei.Element {
    
    static get is () { return 'my-app' } 
    
    static get props () {
      return {
        message: { value: "Hello Pantarei!" }
      }
    }
    
  }

  customElements.define(MyApp.is, MyApp)
</script>
```

```html
<my-element id="element"></my-element>
```

### Another example

```html
<div id="my-app-2">
  <span attr-title="message">
    Hover your mouse over me for a few seconds
    to see my dynamically bound title!
  </span>
</div>

<script>
  class MyApp2 extends pantarei.Element {
    
    static get is () { return 'my-app-2'}
    
    static get props () {
      return {
        message: { value: `You loaded this page on ${new Date()}` }
      }
    }
    
  }
  
  customElements.define(MyApp2.is, MyApp2)
</script>
```