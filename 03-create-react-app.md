# Learn React

[React](https://react.dev/) is a way to make web applications created by Facebook.  It is used by iTwin.js.


## Create a new app

Start in the terminal and `cd` to the `src` directory.

Use `create-react-app` to create a new application.

```bash
npx create-react-app learn-react
```

This will create a new folder `learn-react` containing an empty react app.

Open the app in VS Code

```bash
code learn-react
```

Install and run the new app

```bash
npm install
npm run start
```

For a quick overview of react visit the [React learning page](https://react.dev/learn)

## Modify the app

It's easy to change the app by changing the `src\App.js` file then saving it.  

For your first change add the word `BANANA!!` after the text `Edit src/App.js and save to reload. `.  Save the file and go back to the app to see the new text!!!

Next change the link to some site you want and change the link text.


## Create your first component

A component is a piece of the UI (user interface) that has its own logic and appearance. A component can be as small as a button, or as large as an entire page.

To make a react component create a function that returns html

```jsx
function MyButton() {
  return (
    <button>I'm a button</button>
  );
}
```

Add this button to App.js before `function App() {` and save.

Look at the app, notice that the button did not appear.  That is because you must use the `MyButton` component.

To use the component add `<MyButton/>` after `</a>` and before `</header>` then save.

Try clicking the button, what does it do?

## Add behavior to your new component

For a button to do something when you click on it you need to tell the computer what to do when someone clicks.

To do this you must write a new function that runs `onClick`.

```jsx
function buttonClicked() {
    alert("BANANA!!!");
}

function MyButton() {
  return (
    <button onClick={buttonClicked}>I'm a button</button>
  );
}
```

## Cleanup starter code

Remove everything but the `<div>` and your button

```jsx
function App() {
  return (
    <div className="App">
      <MyButton/>
    </div>
  );
}
```

## Add something of your own

Spend some time adding stuff to your app.  If you want to add something but do not know how, ask!