# Svelte Todo

First Svelte application. Learning the framework and its tools. Built a little todo application, as it is 
customary to do when learning a new framework.

# Takeaways

Things I used:

- Components
- Props
- Svelte logic. `if` and `each` blocks
- Animations
- Dispatching custom events
- Styling with Tailwind CSS
- Local storage
- TypeScript

---

Svelte has been the most loved framework by the wider community, and I can see why now.

- It is very easy to get started with Svelte. The documentation is very good.
- Svelte is a compiler, not a framework. It compiles your code into vanilla JavaScript.
- Working with reactive values is intuitive and easy to understand.
- Updating the state of a parent from the child component is easy. 
  - You can dispatch custom events from the child component and listen to them in the parent component.
- Great developer experience with the Svelte VSCode extension.

# Installation

## Checkout code from GitHub

```sh
$ git clone https://github.com/mir-mirsodikov/svelte-todo
```

## Install Dependencies
```sh
$ npm i
```

# Build and Run

## NPM Commands

| Command           | Description                              |
| ----------------- | ---------------------------------------- |
| `npm run dev`     | Run the application in development mode. |
| `npm run build`   | Build the application for production.    |
| `npm run preview` | Run the production bundle.               |

# Technologies

- Svelte
- Tailwind CSS
- TypeScript