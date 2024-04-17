# Classifiers and Hilite colors

Classifiers let you select things in the Reality Model.  A classifier is registered that lets you select individual buildings based on their footprint.  When you select a building it is hilited in blue, today we are going to add the ability to change that color.

The hilite color is changed on the viewport:

```typescript
    if (viewport) {
      viewport.hilite = {...viewport.hilite, color: newColor};
    }
```

This code creates a new copy of the existing hilite settings replacing the previous color with the `newColor`.

> We will use this code later


## Step 0 - Start Dev environment

Make sure you have the project opened in the container.  If not use the command.

`>Dev Containers: Reopen in container`

![reopen in dev container](./media/reopen-dev-container.png)

Once open in container start the application by running `npm start`

## Step 1 - Add color to state

When the user picks the color, we need to store it somewhere, that place is state.

For the state we will store a variable of type `ColorDef`:

```typescript
  const [hiliteColor, setHiliteColor] = React.useState<ColorDef>(ColorDef.green);
```

## Step 2 - Initialize state to the current hilite color

When the widget is initialized add code to save default hilite color in state:

```typescript
        setHiliteColor(viewport.hilite.color);
```

## Step 3 - Add a ColorPicker so the user can select a color

Add a `ColorPickerButton` after the `ToggleSwitch` to select the new color:

```typescript
      <ColorPickerButton initialColor={hiliteColor} onColorPick={onColorChange} />
```

## Step 4 - Add function alled when the color is changed

Create a function called `onColorChange` that sets the hilite color state and updates the hilite settings on the viewport.  Both bits of code can be found above.  

Here is an empty version of the onColorChange method to start with:

```typescript
  const onColorChange = async (newColor: ColorDef) => {
    // Code goes here
  }
```

## Try on your Own

Try some of the following things on your own

- Improve the layout of the widget by putting the color picker on it's own line
- Add text next to the color picker to describe what it is for
- Change the starting color from light blue to some other color