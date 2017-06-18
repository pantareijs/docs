# Introduction

## What is Pantarei?

Pantarei is a tiny foundation for building user interfaces for the Web.  
Unlike other opinionated frameworks, Pantarei is designed to be resilient.

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


## Under the hood

### Directives

Pantarei makes the existing (real!) DOM of your app reactive.  
Pantarei reactive rendering is driven by directives.  
Directives are special attributes that tells the DOM what to do.  
[Read more](directives.md)

### Components

Pantarei allows you to build components and componentize your app.  
Pantarei components are based on the HTML5 WebComponents standard.  
Pantarei adds a thin layer over WebComponents to enable reactivity.  
[Read more](components.md)


## Show me the code!

Pantarei is [open source](https://github.com/pantareijs/pantarei) under the MIT License.