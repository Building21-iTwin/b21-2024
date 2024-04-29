# Add multiple selection groups

Now that the application can save a set of selected buildings we can update the code to allow the app to save multiple named sets of selected buildings.

## Before Getting started

Make sure you have the project opened in the container.  If not use the command.

`>Dev Containers: Reopen in container`

![reopen in dev container](./media/reopen-dev-container.png)

## Creating a new file

Up till now we have added all UI in the `MyFirstWidget.tsx` file.  This was convenient but if we continue to add more code to this file it will become hard to read.  So we will create a new file, add our new code there and even move some existing code over.

Create a new file in `src/providers` called `BuildingGroupComponent.tsx`.  This file will focus on code for creating, managing and selecting groups of buildings.

Breaking a UI into pieces is a common pattern.  In [React](https://react.dev) these individual pieces of the UI are called `Components`.  We want to create a component which encapsulates the UI and behavior for a group of buildings.

## Creating interfaces

An interface defines the structure of a value.  We want to store a list (array) of building ids and a name for the group of buildings.  It is important to understand this interface definition so read carefully and we will break it down line by line.

```typescript
export interface BuildingGroup {
  name: string;
  buildings: Id64Array;
}
```

The first line `export interface BuildingGroup {` has three important components.  First `export` means the interface can be imported into another file, we will use this interface in `MyFirstWidget.tsx`.  Second `interface` identifies what we are defining is an interface.  Finally `BuildingGroup` is the name of the interface.

The next two lines `name: string;` and `buildings: Id64Array;` define the structure of the data.  That is to say any value that has the properties name and buildings of the correct types (string, and Id64Array) can be considered a BuildingGroup.

To make a component that manages a single group of buildings we need an interface with a building group and a method that handles changes to the building group.

```typescript
export interface GroupListItemProps {
  item: BuildingGroup;
  handleItemChange: (oldItem: BuildingGroup, newItem: BuildingGroup) => void;
}
```

`item: BuildingGroup;` is the group of buildings, note it uses the previous interface.

`handleItemChange: (oldItem: BuildingGroup, newItem: BuildingGroup) => void;` is a method that takes the old building group before a change and the new building group after the change and it will update the application based on the change.

## Create the component

We will create a component called `BuildingGroupListItem`, this component will take the interface `GroupListItemProps` when constructed.

```typescript
export const BuildingGroupListItem: React.FC<GroupListItemProps> = ({
  item,
  handleItemChange,
}: GroupListItemProps) => {

  return (
    <div>
    </div>
  )
}
```

This is an empty component called `BuildingGroupListItem`, it has no behavior output but it does take `GroupListItemProps` when it is constructed.

**Example using new component.  We will use the component later**

```tsx
<BuildingGroupListItem item={a_building_group} handleItemChange={a_method_to_handle_changes} />
```

> NOTE: This is just an example of how the component could be used to help explain the components definition.

Look at the definition and use of this component.  Notice that:

- The name of the component defined here:

  `export const BuildingGroupListItem: React.FC<GroupListItemProps> = ({` 
  
  is the name used instantiating in tsx: 
  
  `<BuildingGroupListItem`
- The input parameters when instantiating the component:

  `item={a_building_group} handleItemChange={a_method_to_handle_changes}`

  match the parameters specified in the component definition:

  ```typescript
  item,
  handleItemChange,
  ```

## Moving existing code to the new component

We already wrote a lot of the functionality in `MyFirstWidget.tsx` that we need in this new component.  So we can move it from one file to another.

Copy the buttons to save selected building, to load saved selection and the clear saved selection if it exists.  You will also have to copy the methods that these buttons call.

Once you copy the components and methods you must modify them to work in the new context.

> Hint 1: You will have to change all calls to update state to calls to the handleItemChange method.

> Hint 2: You will need to get access to the viewport using this line of code: `const viewport = useActiveViewport();`

## Add new stuff to the component

The Component also needs to have a text box so we can set the name and we can show the count of selected buildings as a nice to have.

We can get the number of selected buildings using this snippet of code: `item.buildings.length`.  It can be added to the tsx by wrapping in curly braces: `{item.buildings.length}`.

To get text input we can use the pure html component 'input'

```tsx
<input type="text" value={item.name} onChange={onNameChange} />
```

The `onNameChange` method needs to update the name:

```typescript
  const onNameChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    const newItem = {...item, name: e.target.value};
    handleItemChange(item, newItem);
  }
```

## Update MyFirstWidget to use the new component

The first step is to clean up `MyFirstWidget` to remove things that are now unused.  For example the old state variables or any of the code you moved but did not delete.

Next we need to add a new state called `selectedBuildings`, with set method called `setSelectedBuildings` and of type `BuildingGroup[]`.

Next we need to add a button that adds a new building group:

```tsx
      <Button onClick={addNewGroup}>Add New Group</Button>
```

> Note: you will have to write the `addNewGroup` method.

Finally we need to add the building groups to the UI.  To do this we need to iterate over the `selectedBuildings` and create a `BuildingGroupListItem` for each one.

Here is the code to do that:

```typescript
  const handleItemChange = (oldItem: BuildingGroup, newItem: BuildingGroup) => {
    const newList = selectedBuildings.map((item) => item.name === oldItem.name ? newItem : item);
    setSelectedBuildings(newList);
  }

  const buildingGroups: JSX.Element[] = []
  selectedBuildings.forEach( (value: BuildingGroup) => {
    buildingGroups.push(<BuildingGroupListItem item={value} handleItemChange={handleItemChange} />);
  });
```

In the tsx add the elements we have created by adding a new line like this: `{buildingGroups}`

## Things to try

Save hilite color in each individual Building Group