# jsx-dom-builder

## Description

This is a library that allows to use jsx to create a wrapper to the dom elements, that you can use to change anything within that dom element

## Instalation

Create a vite vanilla app with the command:
```
npm create vite
```
open the project folder and run the following commands
```
npm install
npm install jsx-dom-builder
```

create the `vite.config.js` in the root directory of your project, with the following code:

```js
import { fileURLToPath, URL } from 'node:url'
import { defineConfig } from "vite"
import  jsxDomBuilderVitePlugin  from "jsx-dom-builder/vite-plugin"
// custom jsx pragma
export default defineConfig({
    plugins:[jsxDomBuilderVitePlugin()],
    // make the @ as a alias to the src folder (opitional but recomended)
    resolve: {
        alias: {
        '@': fileURLToPath(new URL('./src', import.meta.url)),
        }
    }
})
```
## Examples

Here is a example of a page with a red square and a button, when you click the button the red square turns blue

![image](https://user-images.githubusercontent.com/66787043/213872010-a6c7d213-26f3-46c7-9096-16eea23f32e4.png)


[here is a page with the goal of this example](https://thiago099.github.io/new-jsx-dom-builder-vite-examples/)

### the main way you whuld aproach this problem
```js
const ref = {}

var data = effect({color:"red"})

const app = 
<div class="container" effect={data}>
    <div 
        class="square" 
        ref={[ref,"colored_input"]} 
    />
    <button 
        ref={[ref,"make_it_blue"]}
        class="button"
    >
        make the square blue
    </button>
</div>

ref.colored_input.style.backgroundColor = () => data.color

ref.make_it_blue.event("click", () => {
    data.color = "blue"
})

app.parent(document.body)
```
### Without using effect
```js
import "./style.css"

const ref = {}

var color = "red"

const app = 
<div class="container">
    <div 
        class="square" 
        ref={[ref,"colored_input"]} 
    />
    <button 
        ref={[ref,"make_it_blue"]}
        class="button"
    >
        make the square blue
    </button>
</div>

ref.colored_input.style.backgroundColor = () => color

ref.make_it_blue.event("click", () => {
    color = "blue"
    app.update()
})

app.parent(document.body)
```

### Without reactivity

```js
import "./style.css"

const ref = {}

const app = 
<div class="container">
    <div 
        class="square" 
        ref={[ref,"colored_input"]} 
    />
    <button 
        ref={[ref,"make_it_blue"]}
        class="button"
    >
        make the square blue
    </button>
</div>

ref.colored_input.style.backgroundColor = "red"

ref.make_it_blue.event("click", () => {
    ref.colored_input.style.backgroundColor = "blue"
    app.update()
})

app.parent(document.body)
```

## Other examples

[gh pages](https://thiago099.github.io/jsx-dom-builder-vite-example/) 

[source](https://github.com/Thiago099/jsx-dom-builder-vite-example)

```js
import "./style.css"
import Counter from "./components/counter.jsx"
import Title from "./components/title.jsx"
import RefExample from "./components/ref-example.jsx"

const app = 
<div class="container">
    <Title text="vite + jsx-dom-builder"/>
    <Counter />
    <RefExample />
</div>

app.parent(document.body)
```

![image](https://user-images.githubusercontent.com/66787043/202039923-39d4c73f-73ba-4aac-b784-ea49e45aa7b8.png)

Just like to react you can create a component:

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

Every JSX elements are dom-builder elements and, here is what you can do with them: [here](https://www.npmjs.com/package/@thiago-kaique/dom-builder).

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
You can also pass an object in the ref property and the element will store a entry with its id as key and, its dom-builder element as the value;
```js
export default function RefExample()
{

    const ref = {}

    const container = 
    <div>
        <button class="button" ref={[ref,"main"]}>Main</button>
        <button class="button" ref={[ref,"secondary"]}>Secondary</button>
    </div>

    ref.main.event("click", () => alert("Main button clicked") )
    ref.secondary.event("click", () => alert("Secondary button clicked") )

    return container
}
```
