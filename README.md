# jsx-dom-builder

## Description

this is a library that allows to use jsx to create dom elements, and manipulaing them with a builder method

## Example

![image](https://user-images.githubusercontent.com/66787043/202048536-5d087204-2299-47d0-8940-457074aec9e9.png)

[gh pages](https://thiago099.github.io/jsx-dom-builder-vite-example/) [source](https://github.com/Thiago099/jsx-dom-builder-vite-example)

## Instalation

create a vite vanilla app with the command:
``
npm create vite
``

create the `vite.config.js` with the following code:

```js
import { defineConfig } from "vite"
import  jsxDomBuilderVitePlugin  from "jsx-dom-builder/vite-plugin"
// custom jsx pragma
export default defineConfig({
  plugins:[jsxDomBuilderVitePlugin()],
})

```

or colne the following repository

https://github.com/Thiago099/jsx-dom-builder-vite-example

## Example

```js
import "./style.css"
import Counter from "./components/counter.jsx"
import Title from "./components/title.jsx"
import RefExample from "./components/ref-example.jsx"

<div parent={document.body} class="container">
    <Title text="vite + jsx-dom-builder"/>
    <Counter />
    <RefExample />
</div>
```

![image](https://user-images.githubusercontent.com/66787043/202039923-39d4c73f-73ba-4aac-b784-ea49e45aa7b8.png)

just like on react you can create a function component with props

```js
export default function Title( { text } )
{
    const title = 
        <h1 
            class="title" 
        >
            {text}
        </h1>
    return title
}

```

every jsx code are dom-builder elements and this is what you can do with them: [here](https://www.npmjs.com/package/@thiago-kaique/dom-builder).

```js
export default function Counter()
{
    const data = effect( { count: 0 } )

    const button = 
        <button 
            class="button" 
            effect={data}
        >
            Count is: { () => data.count }
        </button>

    button.event("click", () => data.count++ )

    return button
}
```
you can also pass a object in the ref propery and the element will store a key with its id, the dom-builder element as value
```js
export default function RefExample()
{

    const ref = {}

    const container = <div>
        <button class="button" id="main" ref={ref}>Main</button>
        <button class="button" id="secondary" ref={ref}>Secondary</button>
    </div>

    ref.main.event("click", () => alert("Main button clicked") )
    ref.secondary.event("click", () => alert("Secondary button clicked") )

    return container
}
```
