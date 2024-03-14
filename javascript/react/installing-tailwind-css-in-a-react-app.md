# Installing Tailwind CSS in a React app

{% embed url="https://www.youtube.com/watch?pp=ygUSdGFpbHdpbmRjc3MgIHNldHVw&v=SPr-1cwVn1k" %}

In this demo I’m going to assume you have created an app using Vite, like I showed you in [setting up a React project with Vite](https://thevalleyofcode.com/react/1-demo-setting-up-a-react-project-with-vite).

Now I want show you how to install Tailwind CSS.

In the terminal, run this command to install these dependencies:

```
npm i -D tailwindcss postcss autoprefixer
```

followed by

```
npx tailwindcss init -p
```

This command creates a file called `tailwind.config.js` which contains this:

```jsx
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Now open this file with VS Code and add to the `content` field the places where we might find the Tailwind classes we’re going to write:

```jsx
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

This setting will be used by Tailwind to determine where to look to generate the CSS file.

Now in the `src/index.css` file add those 3 lines:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

(you can remove all the other content, which most probably you will not use)

Restart the app with `npm run dev` and Tailwind should be enabled.

You should see something like this:

![](https://thevalleyofcode.com/\_astro/Screenshot-2023-11-13T08.59.12AM.DaOttpah\_1ws2Qz.webp)

Now for example try changing your `App.tsx` / `App.jsx` to this:

```jsx
import './App.css'

function App() {
  return (
    <>
      <p className='text-blue-600 font-bold text-6xl text-center'>TEST</p>
    </>
  )
}

export default App
```

It should work:

![](https://thevalleyofcode.com/\_astro/Screenshot-2023-11-13T09.00.06AM.BIpLofno\_Z2pzuBy.webp)

That’s it, we installed Tailwind CSS successfully.
