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
An attribute directive attribute starts with the `attr.` prefix.  

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
A property directive attribute starts with the `prop.` prefix.  

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

The text directive allows you to bind an element's property with a data property.  
A text directive attribute has the `text` name.  

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

## Repeat

The repeat directive allows you to repeat the content of an element.  
A repeat directive attribute has the `repeat` name.

```html
<ul id="list">
  <template repeat="items">
    <li>{{ item.message }}</li>
  </template>
</ul>
```

```js
var app = new Pantarei({
  el: list,
  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```

## Event

The event directive allows you to delegate events.  
An event directive attribute starts with the prefix 'ev.'


```html
<ul id="list">
  <template repeat="items">
    <li ev.click="on_click">{{ item.message }}</li>
  </template>
</ul>
```

```js
var app = new Pantarei({
  el: list,

  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  },

  on_click (event) {
    console.log(`Touchè my ${event.target}`)
  }

})
```