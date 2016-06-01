# CSS methodology

Don't like BEM syntax?

With its awesome at-rules syntax, [PostCSS Bem](https://github.com/ileri/postcss-bem) seems quite interesting, but it adds another step into your build process.

Following examples use [LESS](http://lesscss.org/) syntax.

## SUIT inspired syntax...

### Component

Use component's name as CSS class name.

`MyComponent`



### Element

Just append component's CSS class name with hyphenated element:

```css
.MyComponent{
	&-header{}
	&-default-link{}
}
```
```xml
<MyComponent className='MyComponent'>
    <header className='MyComponent-header' />
    <a className='MyComponent-default-link'>Click here</a>
</MyComponent>
```



### Modifiers

Modifiers are element variations or component state


#### Variations

When applying a visual variation to a React Dumb Component (block) or one of its
elements, we should add another CSS class (prefixed with `mod-`) to the element:

```xml
<MyComponent className='MyComponent'>
    <!-- Variation : agressive-background -->
    <header className='MyComponent-header mod-agressive-background' />
</MyComponent>

<!-- Variation : bigger -->
<MyComponent className='MyComponent mod-bigger' />
```

To avoid collisions, the agressive-background or bigger classes will never be defined
as a global rules like those:

```css
/* bad */
.mod-agressive-background {
    border: 1px;
    padding: 10px;
	background-color: red;
}

.mod-bigger {
    transform: scale(2);
}
```

But rather like this:

```css
/* good */
.MyComponent-header {
    &.mod-agressive-background{
        border: 1px;
        padding: 10px;
    }

    &.mod-bigger {
        transform: scale(2);
    }
}
```

#### State

Component state defines a temporary variation reflecting user inputs or
application state.

Same rules as variations, but modifier name is prefixed with is[Upper case first
 next letter].

```css
.MyComponent-header {
    &.isFocused{
        border: 4px;
    }
}
```

```xml
<MyComponent className='MyComponent'>
    <input
        onFocus={setFocused}
        onBlur={unsetFocused}
        className='MyComponent-header' />
</MyComponent>
```

```javascript
setFocused(){
    this.parentNode.classList.add('isFocused');
}
unsetFocused(){
    this.parentNode.classList.remove('isFocused');
}

```
## Utils
Prefix global class names (utility/generic) class names with `u-`.

```css
.u-text-center {
	text-align: center;
}
```
