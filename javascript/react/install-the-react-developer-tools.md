# Install the React Developer Tools

Next.js is based upon React, so one very useful tool we absolutely need to install (if you haven’t already) is the React Developer Tools.

Available for both [Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) and [Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/), the React Developer Tools are an essential instrument you can use to inspect a React application.

They provide an inspector that reveals the React components tree that builds your page, and for each component, you can go and check the props, the state, hooks, and lots more.

Once you have installed the React Developer Tools, you can open the regular browser dev tools (in Chrome, right-click on the page, then click `Inspect`) and you’ll find 2 new panels: **Components** and **Profiler**.

Note that you might have to click this icon to see the new tabs:

![Untitled](https://thevalleyofcode.com/images/lessons/react/install-the-react-developer-tools/Untitled.png)

![Untitled](https://thevalleyofcode.com/images/lessons/react/install-the-react-developer-tools/Untitled%201.png)

Once you’re in the Components tab, you’ll see the application components list:

![Untitled](https://thevalleyofcode.com/images/lessons/react/install-the-react-developer-tools/Untitled%202.png)

In this case, we only have 1 component.

But as your app grows in size and components, you’ll find this panel very useful

![Untitled](https://thevalleyofcode.com/images/lessons/react/install-the-react-developer-tools/Untitled%203.png)

as you will be able to inspect the component’s data:

![Untitled](https://thevalleyofcode.com/images/lessons/react/install-the-react-developer-tools/Untitled%204.png)

If you move the mouse over the components, you’ll see that on the page, the browser will select the parts that are rendered by that component.

If you select any component in the tree, the right panel will show you a reference to **the parent component**, and the props passed to it.

You can easily navigate by clicking around the component names.

You can click the eye icon in the Developer Tools toolbar to inspect the DOM element, and also if you use the first icon, the one with the mouse icon (which conveniently sits under the similar regular DevTools icon), you can hover an element in the browser UI to directly select the React component that renders it.

You can use the bug-shaped 🐞 icon at the top right of the panel to log component data to the console.

![Untitled](https://thevalleyofcode.com/images/lessons/react/install-the-react-developer-tools/Untitled%205.png)

Those are the basics.

This is a super powerful tool that will help you debug your React applications going forward.
