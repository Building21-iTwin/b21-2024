# Allow each group to have it's own selection color

What's the point in having groups if everyone is the same.

## Before Getting started

Make sure you have the project opened in the container.  If not use the command.

`>Dev Containers: Reopen in container`

![reopen in dev container](./media/reopen-dev-container.png)

## Making the changes

The color picker is now in `MyFirstWidget.tsx` because it sets the color for all groups.  It needs to be moved to `BuildingGroupComponent.tsx` so there is one per group.  Move the control and the state to `BuildingGroupComponent.tsx`.