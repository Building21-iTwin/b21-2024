# Make a custom button

## Create a new file

For better organization components are often put in their own file that matches the name of the component.

We are going to call our component `PictureButton` so call the new file `PictureButton.js` in the `src` directory of the application.

## Create an empty component

The most basic definition of a component:

```jsx
function PictureButton () {

    return (
        <div>
            
        </div>
    )
}

export default PictureButton;
```

`function PictureButton () {}` defines an empty component and `export default PictureButton` makes the component visible to other files.  It can now be used in another file by importing it like this `import PictureButton from './PictureButton'`

## Add a picture to the component

Use the `img` tag.

`<img src="./cat.jpg" />`

Let's use this component and see how it looks.  You should see the picture but it's not a button.  We can wrap the `img` tag in a `button` tag to make it a button.

```jsx
<button>
    <img src="./cat.jpg" />
</button>
```

## Add onClick event to custom button

We want to expose the onClick event from the `button` as a function of the `PictureButton`.  We can do this by adding a parameters

```jsx
function PictureButton ( {onClick} ) {

    return (
        <div>
            <button onClick={onClick}>
                <img src="./cat.jpg" />
            </button>
        </div>
    )
}
```

You can now use the `onClick` function when you create a `PictureButton`:

```jsx
<PictureButton onClick={clickCounter}/>
```

## Add ability to set the picture when you construct the PictureButton

We want use of `PictureButton` to look like this

```jsx
<PictureButton onClick={clickCounter} imgSrc="./cat.jpg" />
```

## Resize the image so it fits in the button

We can limit the size of the button then size the image to fit in the button.  

```jsx
        <div>
            <button onClick={onClick} style={{width:"300px"}}>
                <img src={imgSrc} style={{width:"100%"}} />
            </button>
        </div>
```

Notice we are using `style`  to control the size of the button and the image.  On button we fix the width at a set number of pixels then se the width of the image to 100% so it fits within the size of the button.  Try adjusting the percent width of the image and the size of the button.


## Style the image to look like a button

Our picture button still looks like a button with a picture in it.  Let's try to make it look like the image itself is the button.

We could try to hide the button but we don't actually need the button, we can move the sizing to the `div` and `onClick` to the `img` element

```jsx
        <div style={{width:"300px"}}>
            <img src={imgSrc} style={{width:"100%"}} onClick={onClick} />
        </div>
```

This removes the outline of the button but should otherwise function the same.  To make it look more like a button we can add a radius around the image by adding `borderRadius:"10px"` to the img elements style

```jsx
            <img src={imgSrc} style={{width:"100%", borderRadisu:"10px"}} onClick={onClick} />
```

A normal reacts when you hover over them and reacts when you click on it.  We will use css to achieve this, css is a powerful tool to style webpages.  To start we must create a new file to hold the css, since this css is for the `PictureButton` component we can call it `PictureButton.css` and put it in the src directory next to the `PictureButton.js` file.

To use the css file update `PictureButton.js` to import the css file:

```jsx
import './PictureButton.css';
```

Css uses names to names to connect between the jsx and the css.  So we will give the `div` for the `PictureButton` a class name

```jsx
        <div className="picture-button" style={{width:"300px"}}>
```

The following css darkens the image when you hover over it

```css
.picture-button img:hover {
    filter: brightness(90%);
    transition: 50ms ease
}
```

Notice that the line starts with `.picture-button`, that means it refers to the `div`.   Next it says `img` that is for the `img` element inside the `div`.  `:hover` indicates what should happen when the user hovers over the image.

This is half of the behavior we're looking for the second half is brightening again when clicked

```css
.picture-button img:active {
    filter: brightness(100%);
    transition: 50ms ease;
}
```