# Directives

Pantarei reactive rendering is driven by directives.  
Directives are special attributes that tells an element what to do,  
usually when the data associated with the element change.


## Built-in directives

Pantarei comes with a minimal set of built-in directives:
- attribute
- property
- text
- repeat
- event

Pantarei directives can be easily customized and extended.  
Create new directives, or modify the existing ones, is straightforward.  


## Attribute

The attribute directive allows you to bind an element's attribute with a data property.  
Attribute directives have the `attr.` prefix.  

### Example

```html
<div id="element" attr.title="message">
  Hover your mouse over me for a few seconds
  to see my dynamically bound `title`!
</div>
```

```js
var app = new Pantarei({
  el: element,
  data: {
    message: `You loaded this page on ${new Date()}!`
  }
})
```


## Property

The property directive allows you to bind an element's property with a data property.  
Attribute directives have the `prop.` prefix.  

### Example

```html
<button id="button" prop.disabled="disabled">Don't touch me!</button>  
```

```js
var app = new Pantarei({
  el: button,
  data: {
    disabled: true
  }
})
```


## Text

The property directive allows you to bind an element's property with a data property.  
Attribute directives have the `text` prefix.  

### Example

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
