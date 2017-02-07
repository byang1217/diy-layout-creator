### System requirements ###

  * [Java JRE/JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 1.6.0_45-b06 or newer
  * 1GB free RAM memory is recommended
  * 10MB free hard drive space
  * Zip utility to unpack the archive (7-zip, WinZip, Total Commander, etc)

### Running the app ###

For starters, make sure that you have downloaded the correct version. Mac OSX builds have names that end with "osx". The build without "osx" in their name are multi-platform and will work pretty much anywhere provided that Java JRE is available for that platform.

  * On **Windows** just run the diylc.exe
  * On **Linux/Unix** (will also work on **Mac OSX** if not using the OSX dedicated build), open the terminal, change the directory to diylc3 (**cd `<`path to diylc3`>`**) and type **./run.sh**
  
  * On **Mac OSX** you will need to allow 3rd party apps and then run the application package.

### User interface ###

User interface can be separated into 4 major components:

  1. **Canvas** is used as a [WYSIWYG](http://en.wikipedia.org/wiki/WYSIWYG) editor for the project.
  1. **Toolbox** lists all available components and allows you to pick the one you want to add.
  1. **Main menu** offers file operations, such as saving, loading and exporting, clipboard operations, etc.
  1. **Status bar**: shows context related information, zoom control, update information and memory consumption.

### Configuring the application ###

Application configuration may be changed from **Config** menu. It contains the following items:

  * **Anti-Aliasing**: when checked, objects and text will look smoother but it takes more time to render anti-aliased graphics. If you suffer from performance issues, try turning this option off.
  * **Auto-Create Pads**: when checked, application will automatically create solder pads whenever a component is added to the layout.
  * **Auto-Edit Mode**: when checked, the component edit dialog will appear after each component is created, the same way version 1.x works.
  * **Continuous Creation**: when checked, the last selected component type will remain active after you create a component, allowing you to create many components of the same type rapidly.
  * **Show Rulers**: controls whether the rulers should be displayed
  * **Show Grid**: controls whether the grid lines should be shown while working on the project.
  * **Export Grid**: controls whether the grid lines should be exported when saving the project to a file or printer.
  * **Hi-Quality Rendering**: when checked, image quality will improve slightly, but it may decrease performance.
  * **Mouse Wheel Zoom**: when checked, mouse wheel zooms in and out instead of scrolling the visible area of the project.
  * **Outline Mode**: when checked, components are drawn only as the the outline with no fill color or decorations.
  * **Snap to Grid**: when checked, drag & drop operations will snap control points to the grid instead of following the mouse cursor pixel by pixel.
  * **Sticky Points**: when checked, components are allowed to stick to each other when moved. Hold Ctrl key while dragging to temporarily toggle the Sticky Point mode. See [Control points](#Control_points.md) for more info on control points.
  * **Theme**: allows selecting a theme. Themes are read from **themes** directory under the DIYLC root and they include background color and grid line color. You can create your own themes by adding an XML file to themes directory. It's easiest to start with a copy of one of the existing files.

### Adding components to the drawing ###

This sections explains how to add an existing component to the project. To learn how to develop your own components follow [this tutorial](http://code.google.com/p/diy-layout-creator/wiki/Components). To instantiate a component, follow these steps:

  * Locate the component in the toolbox. Components are categorized into several tabs, so make sure you're looking into the right one.
  * Click on the button that shows the desired component. Note that text in the status bar changes to reflect this action.
  * Click on the desired location on the canvas to create the component. Some components (solder pads, trace cuts, etc) will be created on single click, others (like resistors, jumpers, etc) will require two clicks to set both ending points. Instructions in the status bar will guide you through the process. Component will be drawn translucent until the creation process is finalized.

### Moving components ###

The easiest way to move a component across the canvas is to drag it by clicking on it's body and moving the mouse to the desired location. When mouse cursor is over a component, it will change to "hand pointer" and status bar will read name of the component that will be dragged.

Note that:
  * if more than one component is selected, all of them will be moved
  * moving one (or more) components will move/stretch any components that are stuck to them. Status bar will inform you which components will be affected. Hold <b>Ctrl</b> to unstuck the selected components and move them only.

### Control points ###

A component may have one or more control points. Control points determine component's position on the layout and in some cases allows the component to get connected with other components. For some components, such as resistors, wires, etc, individual control points can be moved around when the component is selected.

Note that:
  * status bar lists all the components that will be affected by the drag&drop operation.
  * you can drag control points only when they turn green.

### Editing component properties ###

  * Double click on a component opens the Component Editor - dialog that lists all editable properties of the selected component(s).
  * Checking the "Default" checkbox on the right side will make the value for that property default. In other words, all the components created after that will inherit that value.
  * Boxes that edit measures (size, resistance, capacitance, etc) can take math expressions in addition to constants. For instance you can type 3/32 and it will be automatically converted to decimal. Even more complicated expressions with parenthesis and 4 basic numerical operators are possible.
  
### Using component variants ###

Each component is created using default values for size, color, etc. Users can make their own variants of components with different properties. After the component is edited to the desired state, it can be saved as a variant using the context menu action.

<p align='center'><img src='https://raw.githubusercontent.com/bancika/diy-layout-creator/wiki/images/save_variant.png' /></p>

After saving, the existing component variants can be employed in few different ways. One way would be to apply the variant to the existing component by using the context menu.

<p align='center'><img src='https://raw.githubusercontent.com/bancika/diy-layout-creator/wiki/images/apply_variant.png' /></p>

Applying a variant will copy all the properties associated with the variant to the selected component and transform it to conform the variant.

<p align='center'><img src='https://raw.githubusercontent.com/bancika/diy-layout-creator/wiki/images/apply_variant_after.png' /></p>

Another way to use variants is to add a component to the project using a saved variant as a blueprint. This can be done by right clicking on a component icon in the component tree and selecting a desired variant from the context menu.

<p align='center'><img src='https://raw.githubusercontent.com/bancika/diy-layout-creator/wiki/images/recall_variant.png' /></p>

Furthermore, a variant can be set as default and all components created after that will inherit their properties from the default variant. That can be done by using the pin button in the aforementioned context menu. Next to the pin button is the delete button we can use to delete a variant.

<p align='center'><img src='https://raw.githubusercontent.com/bancika/diy-layout-creator/wiki/images/use_variant.png' /></p>

### Grouping components together ###

Component groups behave similar to object groups Corel Draw. The idea is to keep two or more components together and move/edit/delete them at the same time. To group components, select them and press Ctrl+G (or select "Group Selection" from the menu). Double click on one of the grouped components will open the editor with all the mutual properties of selected components and allow editing them at the same time.
Note that while the components are grouped, you can't edit drag their individual control points.
To un-group the components, select them and press Ctrl+U (or select "Ungroup Selection" from the menu).

Note that:
  * nested groups are not currently supported. If you group two groups of components together you'll end up with one large group instead of a group that contains two groups.

### Using the status bar ###

Status bar contains three different features:

  * **Information bar** shows context related information and guidance through the app.
  * **Selection size** shows the dimensions of the minimal bounding rectangle that contains all the selected components. It takes default size units (in or cm) into account.
  * **Zoom control** allows you to zoom in or out.
  * **Auto-update** notification. When the bulb is on, there are updates available. Click on it for more information.
  * **Memory bar** is the blue-ish icon on the right side that shows the amount of memory occupied by the application. Move the mouse over it to see more details or click on it to try to cleanup as much memory as possible. Color will turn red when memory consumption is running high.