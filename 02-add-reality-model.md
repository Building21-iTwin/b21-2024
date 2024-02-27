# Add Philadelphia 3D Reality Data

Follow these instructions to add reality data to the application created in [viewer-start](./01-viewer-start.md).

## Copy the starting code

Copy the `providers` folder into your application under the `src` directory.  This directory includes all the code necessary to fetch reality data and add or remove it from the view.

> Notes

- Use the `cp` command or the VS Code UI to copy the `providers` directory
- `MyFirstWidget.tsx` defines a widget that fetches the reality data and a toggle button to turn it on and off.
- `PhillyWidgetProvider.tsx` holds the widget and is what will be added to the application
- `RealityDataApi.ts` includes code to fetch reality data and to add it to the view

## Update the application to use the new code

To use the new widget modify the `App.tsx` file to include the new widget provider.  `App.tsx` defines the `Viewer` component, this component is the application.  Modify the `Viewer` to include the widget provider:

```ts
      <Viewer
        iTwinId={iTwinId ?? ""}
        iModelId={iModelId ?? ""}
        changeSetId={changesetId}
        authClient={authClient}
        viewCreatorOptions={viewCreatorOptions}
        enablePerformanceMonitors={true} // see description in the README (https://www.npmjs.com/package/@itwin/web-viewer-react)
        onIModelAppInit={onIModelAppInit}
        uiProviders={[
          new ViewerNavigationToolsProvider(),
          new ViewerContentToolsProvider({
            vertical: {
              measureGroup: false,
            },
          }),
          new ViewerStatusbarItemsProvider(),
          new TreeWidgetUiItemsProvider(),
          new PropertyGridUiItemsProvider({
            propertyGridProps: {
              autoExpandChildCategories: true,
              ancestorsNavigationControls: (props) => (
                <AncestorsNavigationControls {...props} />
              ),
              contextMenuItems: [
                (props) => <CopyPropertyTextContextMenuItem {...props} />,
              ],
              settingsMenuItems: [
                (props) => (
                  <ShowHideNullValuesSettingsMenuItem
                    {...props}
                    persist={true}
                  />
                ),
              ],
            },
          }),
          new MeasureToolsUiItemsProvider(),
          // Add PhillyWidgetProvider here
        ]}
      />
```

> Notes

- Adding the widget provider should add a line at the top of `App.tsx` that imports the `PhillyWidgetProvider`.  If it is not added automatically add `import { PhillyWidgetProvider } from "./providers/PhillyWidgetProvider";` under the other imports at the top of the file.

## Try it!

Make sure all files are saved then use the `npm start` command to start the application with the changes.

The widget will be hidden by default, hover over the tab on the left hand side to expand it

![widget tab](./media/widget-tab.png)

Toggle the switch to turn the reality data on and off and move around the 3d view.

## Make some changes

Now that the application is running it is easy to make changes and see the results quickly.  Just change a file and save it, the application will reload with the changes if they are successful.

Modify the application changing the widget tab titled `Change Me!!` and text in it saying `This is my first widget`.  

![widget title](./media/widget-title.png)

> Hints

- You can find the text to change by searching the source code using the magnifying glass icon on the left hand side
- If you make a mistake the page will show an error message which may help you to fix the problem.
