# Setting up a React project with Vite

There are many ways to create a project with React.

The way I suggest is by using [Vite](https://vitejs.dev/).

Vite is a modern tool that provides a development server, is very fast, and many people in the JS community consider it optimal.

> 💁‍♂️ Note: Vite can be used as a replacement for `create-react-app`, another tool that’s popular but also slower. You can use that instead if you prefer, but I found Vite just great and it can also be used with other libraries, not just React.

To create a project using Vite you first go into the folder where you host all your projects, in my case a `dev` folder in my user’s home folder.

Then run

```
npm create vite@latest

# or

bun create vite
```

![](https://thevalleyofcode.com/\_astro/1-demo-setting-up-a-react-project-with-vite.CglZiGwf\_lrMzm.webp)

Choose a name for the project. That will also be the project’s folder name. In this case “test”:

![](https://thevalleyofcode.com/\_astro/1-demo-setting-up-a-react-project-with-vite-1.B3hLMWtm\_1X9x2m.webp)

Now you can choose a framework. Pick “React”.

![](https://thevalleyofcode.com/\_astro/1-demo-setting-up-a-react-project-with-vite-2.C65xXP5U\_57tCp.webp)

Pick JavaScript or TypeScript:

![](https://thevalleyofcode.com/\_astro/1-demo-setting-up-a-react-project-with-vite-3.DTNPY13m\_U2IMG.webp)

Done!

![](https://thevalleyofcode.com/\_astro/1-demo-setting-up-a-react-project-with-vite-4.BPx7ANgU\_Z1LIsg1.webp)

Now go to the newly created project folder:

```
cd test
```

and run

```
npm install
```

to install the dependencies, followed by

```
npm run dev
```

to start the application:

![](https://thevalleyofcode.com/\_astro/Screenshot-2023-11-13T08.55.30AM.Cx1PvqxX\_2dthwG.webp)

The application should be running at [http://localhost:5173](http://localhost:5173/) (the port might be different if it’s already used)

![](https://thevalleyofcode.com/\_astro/1-demo-setting-up-a-react-project-with-vite-6.DheN3laq\_1Fk4rl.webp)

Now you’re ready to work on this application!

Here’s the application folder opened in VS Code.

As you can see, Vite created a basic application and you can now open `src/App.tsx` (TypeScript) or `App.jsx` to start working on it.

![](https://thevalleyofcode.com/\_astro/Screenshot-2023-11-13T08.56.12AM.DwkSUPAg\_vq5ia.webp)

<div align="left" data-full-width="false">

<img src="https://thevalleyofcode.com/_astro/1-demo-setting-up-a-react-project-with-vite-7.iyFlLFAe_1CWTd.webp" alt="">

</div>

One convenience of a tool like Vite is that now you can add files and Vite will automatically recognize them, without the need of restarting `npm run dev` like we had to do with our Node.js projects.

And when you save a component, it’s automatically updated in your browser.

It makes development very fast and fun!
