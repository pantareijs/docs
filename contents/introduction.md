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

### Example

```html
<template-element id="my-element">
  <template>
    <div>Hello Pantarei!</div>
  </template>
</template-element>

<script>
  class MyElement extends pantarei.Element {
    
    static get is () { return 'my-element' } 
    
  }

  customElements.define(MyElement.is, MyElement)
</script>
```

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
<template-element id="my-element">
  <template>
    <template repeat="countdown" item="number">
      <div text="number"></div>
    </template>
    <div>Welcome <span text="name">WebComponents</span>!</div>
  </template>
</template-element>

<script>
  class MyElement extends pantarei.Element {
    
    static get is () { return 'my-element' } 
    
    static get props () {
      return {
        name: { value: "Pantarei" },
        countdown: { value: [3, 2, 1] }
      }
    }
    
  }

  customElements.define(MyElement.is, MyElement)
</script>
```

```html
<my-element id="element"></my-element>
```
