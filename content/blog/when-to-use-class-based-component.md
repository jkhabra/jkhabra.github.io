
+++
title = "When to use a Class Component over a Function Component in React?"
description = "In React 16.8 with the addition of Hooks, you could use state , lifecycle methods and other features that were only available in class component right in your function component but functional component still can not handle react error boundary."
tags = [
    "programming",
    "frontend",
    "javaScript",
    "react",
    "functional programming",
    "development",
    "Js"
]
date = "2022-08-26"
categories = [
    "Development",
    "React"
]
featureImage = "images/math-think.png"
+++
In React 16.8 with the addition of Hooks, you could use state , lifecycle methods and other features that were only available in class component right in your function component but functional component still can not handle react error boundary.

### What is Functional components?
- Functional component is just a plain JavaScript pure function that accepts props as an argument and returns a React element(JSX).
- There is no render method used in functional components.
- React lifecycle methods (componentDidMount) cannot be used in functional components.
- Functional component run from top to bottom and once the function is returned it cant be kept alive.
- Hooks can be easily used in functional components to make them Stateful.

### What is Class component?
- Class component requires you to extend from React. Component and create a render function which returns a React element.
- It must have the render() method returning JSX.
- React lifecycle methods can be used inside class components (componentDidMount).
- Class component is instantiated and different life cycle method is kept alive and being run and invoked depending on phase of class component.
- It requires different syntax inside a class component to implement hooks.


So, when should we use a class component over a function component?

The answer is simple: when we need to handle react error boundary.

The new Hooks API allows you to do things like write your own state management, which makes it easier to hook into the lifecycle of your component and add custom methods.
You can hook into the lifecycle of your component to add custom methods. This API has been highly anticipated, and it's exciting to see what you come up with!

The Hooks API is really powerful, and it's been a long time coming. I'm excited to see how this will affect how we write React components going forward.
