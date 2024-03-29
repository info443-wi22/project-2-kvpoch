# INFO 443 Project 2 (Chart.js)

## Context and Background

**What is the software system, and what does it do?**

Chart.js is an open-source JavaScript library for creating data visualizations. It can visualize your data in eight different ways, each of them animated, customizable, and responsive. It is great at rendering performance across modern browsers.

**Who created the software, and who currently "maintains" it? Was it developed by a large company or an independent developer? Who seems to be iÂn charge of approving changes to its code/architecture?)**

Chart.js was originally created by developer Nick Downie in 2013. It is now open for contribution by the entire developer community, but a dedicated Chart.js team of seven people is in charge of approving changes.

**Where can we find more information about the system?**

Official repo:
https://github.com/chartjs/Chart.js <br>
Documentation: https://www.chartjs.org/docs/latest/

## Development View

_What modules (components) comprise the system, how are they organized, and how do they interact?_

**Component Diagram**

|![Component diagram](./images/dv_diagram1.png) |
|:--:|
| _Figure 1: UML Component Diagram Part 1_|

|![Component diagram](./images/dv_diagram2.png)|
|:--:|
| _Figure 2: UML Component Diagram Part 2_|
> These two figures represent the component diagram of this system's structure and organization.

This text refers to the UML Component Diagram Part 1 and UML Component Diagram Part 2 and explains each architectural component of the system.

The `types` directory contains tests and `helper` components that use TypeScript to create object types, which is given to the `helpers.core.js` of the `src` folder, a required interface.
The `helper` components of the `src` folder has helper functions that aid other modules to perform their work. The `core` components contain the foundation functions to create charts. Both `core` and `helper` components deal with handling the data and both are the provided interfaces for the rest of the components in the `src` folder. The `controller` components control or manage the data for each different type of chart.  The `element` components do the work of computing the mathematical attributes for charts with arc, line, point and bar attributes. The `platform` components sets up the platform for the chart. The `scale` components compute the chart scales for time series, logarithmic, linear, category and more. The `plugin` components deal with the chart attributes, like title, subtitle, Tooltip, legend, and more. All of these components are provided interfaces for the `index.js`, which brings everything all together and exports the chart made. The `test` folder and its components are a required interfaces for the `index.js` from the `src` folder. In the `test` folder, the `fixtures` set up the environment for testing and `specs` are the actual automated tests. There is the `docs` folder that contains all documentation Markdown files, which are then published with Vuepress.


**Source Code Structure**

This system mostly has a source code structure that mirrors the component structure. This means architectural elements (components) have a one-to-one relationship with code modules (files).

**Testing and Configuration**

This system has automated testing integrated into the code for developers and contributors to use.  They use it to test their code and check that is passes `eslint` code standards. After using `npm install` to install node and npm, running `npm test` will run both the linter and tests.

|![npm commands](./images/npm_test.png)|
|:--:|
| _Figure 3: `npm` commands to perform tests_|
> These are the following commands that are now available from the repository root. `npm run dev `and `npm test` can be appended with a string that is used to match the spec filenames.


This system also has image-based testing to make sure that a chart is matching the expected image pixel-by-pixel. The instructions to create a new image-based test can be found under the "Image-Based Tests" section here: https://www.chartjs.org/docs/latest/developers/contributing.html


For **bugs and issues**, there are reported on the issues tab at https://github.com/chartjs/Chart.js that are used to improve and create further tests to check the functionality of the library.

If a user wants to report a bug, they should:
- check if it's already an existing issue
- isolate the problem to a simple test case
- include a demonstration of the bug on a website such as https://jsbin.com/ or https://codepen.io/pen/


Users must request commit access to the project through the GitHub or the Chart.js Slack. All this information is from the Chart.js documentation and available to learn more at https://www.chartjs.org/docs/latest/.

## Applied Perspective

We’ve chosen to apply the **evolution** perspective. The evolution perspective aims for a system that is adaptable amongst the inevitable changes that all systems eventually face. It also strives for a system that balances the costs associated with supporting this adaptability. Although these qualities are desirable in practically any system, they’re especially important for Chart.js. Being the second most popular JavaScript charting library, it’s depended on by a wide variety of users, which all introduce a different technology level that must be accommodated by Chart.js. Since its first release in 2014, the library has undergone over 80 releases to keep up with this demand.

One concern that this perspective brings to Chart.js is that there are **changes driven by external factors**. ECMAScript (ES), the standardized version of JavaScript, is updated every year by an external organization, Ecma International. Thus, Chart.js has had to accommodate seven new versions of JavaScript during its deployment. Since the developers of Chart.js don’t directly contribute to the standardization process at Ecma International, this forces the library to adapt to changes that could potentially completely change their system.

Another concern of this perspective with Chart.js is the **reliability of change**. Since the software is open-sourced and open to contribution by anybody, this introduces a lot of variability in proposed changes. Compounded with the aforementioned everchanging ECMAScript, the wide variety of contributors will possess differing levels of knowledge about the most recent ES version, which could potentially create conflicting change proposals. Fortunately, Chart.js tries to alleviate this concern with official documentation on how to contribute to the library, as well as a folder of automated tests.

**Characterizing Evolution Needs**

| Change                                                                                                                              | Type of change required | Magnitude of change required                                                        | Likelihood of change                                            | Timescale of required changes                                                    |
|-------------------------------------------------------------------------------------------------------------------------------------|-------------------------|-------------------------------------------------------------------------------------|-----------------------------------------------------------------|----------------------------------------------------------------------------------|
| Ability to get data from different sources (such as APIs, relational/non-relational databases, etc.) that are converted into charts | Integration             | Not high risk, a somewhat small proportion of the initial system development effort | Very likely for common data sources, unlikely for uncommon ones | Vague, dependent on external factor: different data sources rising in popularity |
| Maintaining consistent functionality alongside the ES updates                                                                                                           | Platform                | Dependent on ES changes proposed. Most likely not high risk                         | Very likely, as ES is the most commonly used version of JS      | Vague, dependent on external factor: released changes of ES                      |

**Considering the Evolution Tradeoffs**

For the two evolution needs above, there is a range of possible approaches to support them.

| Change | Consequences of doing nothing                                                                                                                                                               | Consequences of designing but not implementing various options                                                                                                                                                                                                               | Consequences of developing a fully flexible system from the outset                                                                                                                                                                                                 |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | No labor cost. Most data is already stored in widely agreed upon formats, so accommodating additional ones isn't a huge priority. But you risk excluding users who do use those formats.    | Some labor cost to design many additional methods. Not much risk, as just designing the different data retrieval methods would allow contributors to actually implement them later on if they see fit. Easier to prioritize which methods would be necessary as time passes. | Very high labor cost, as each data format has its own complexities. It’s almost impossible to accommodate every single data format available. By prioritizing this, you risk putting labor towards other, more pressing issues.                                    |
| 2      | No labor cost. But if the ES updates were huge, it would have high risk. The functionality of the library could be completely altered by the ES update, thus rendering the library useless. | Some labor cost to ensure high modifiability in the system, which should already be a priority. There is a risk that ES updates are not big in the future, which could result in some wasted labor to ensure that modifiability.                                             | Very high labor cost to try to accommodate every potential ES update. Same issue as above: by prioritizing this, you risk putting labor towards other, more pressing issues. Most ES updates probably will not drastically alter the functionality of the library. |

## Identify Styles & Patterns

Chart.js is developed using the **Model-View-Controller** style. Charts are rendered in the View, the web browser. There are interactive elements (such as buttons) also rendered alongside the charts in the View that tell the Controller some sort of instruction when interacted with. For example, there could be a button labeled to select a different data set to render. There is a directory of different controllers in `Chart.js/src/controllers`, one for each kind of chart type. For instance, the bar chart controller (`controller.bar.js`) has methods to calculate the number of pixels an individual bar has, dependent on user-inputted parameters. The Controller gives these instructions to the Model, which handles any sort of manipulation of the state/charts (ex: changing from a bar to line graph). The Model is represented in both `Chart.js/src/core` and `Chart.js/src/elements`. The `core` directory holds the foundations of the different types of charts, such as the scaling. The `elements` directory contains representations of the user-inputted data, such as lines or points. The Controller then tells the View to re-render the state/charts using the new state created by the Model. The different controller components each have their own `update` functions that take in parameters to repopulate the existing charts.

Chart.js uses the **strategy** design pattern to create line segments. The line component is composed of two line segmentation strategies: [pathSegment](https://github.com/chartjs/Chart.js/blob/6a6693e26dc190acff9426174256bfe730f09629/src/elements/element.line.js#L68) and [fastPathSegment](https://github.com/chartjs/Chart.js/blob/6a6693e26dc190acff9426174256bfe730f09629/src/elements/element.line.js#L115). The interface [getSegmentMethod](https://github.com/chartjs/Chart.js/blob/6a6693e26dc190acff9426174256bfe730f09629/src/elements/element.line.js#L182) decides which method to use based on a few criteria, for example whether or not the line is decimated. The chosen method is then used as the segmentation method property when creating a line object. Regardless of the method chosen, the segmentation method will take in the parameters ctx, line, segment, and params to create the segment.

This system uses the **adapter** design pattern, especially when dealing with time variables and creating chart scales measured in time. Dates and times are often values that need to be reformatted in a way the system and client expects or understands. The `core.adapters.js` module exports the `DateAdapter` interface, which has functions that convert or format the given time values in a way that allows other interfaces to use them. The [`determineUnitForFormatting`](https://github.com/chartjs/Chart.js/blob/6a6693e26dc190acff9426174256bfe730f09629/src/scales/scale.time.js#L110) function is an example of how a different interface can use a function from the `DateAdapter` interface to fulfill its intended purpose, which otherwise could not have been done without an adapter. The `determineUnitForFormatting` function uses the `adapter.diff` function to return the number of units between the given timestamps.


This system uses the **decorator** pattern. An example of where this pattern is used is the [`parseObjectData`](https://github.com/chartjs/Chart.js/blob/6a6693e26dc190acff9426174256bfe730f09629/src/controllers/controller.polarArea.js#L25) function. This function processes its existing data object by calling another function (`parseObjectDataRadialScale`)  by binding to create a new data object. This function wrapped itself up to add an additional responsibility in creating its object, which provides more flexibility in the structural design.

This system uses a **proxy** design pattern within multiple components. For example, when a user is creating a bar chart and wants to put a border around the bars, the border function includes a proxy that has a placeholder/default options that creates a border around the bars with `BorderWidth` and `BorderColor`.


## Architectural Assessment

To start, we can discuss the architecture of Chart.js in relation to **Single-Responsibility Principle**. SRP is when an element has one and only one reason to change or is responsible for only one actor. Whether it is in accordance to a class or a variable, there should be only one thing that the element is responsible for. Chart.js does adhere to this principle because for elements such as 'backgroundColor', 'borderWidth', etc, they only accept values that will change properties for each type for element. For example, the 'borderWidth' element's job is to change the border width and thats it; it doesn't have any affect on the border color or the background color.

We can also look at this from a higher level: if we want to change the type of chart, how many places do I have to modify it? You would only need to change it in one area for the `type` of the chart but then, you would need to include additional requirements that are necessary for different types of chats. As a result, this would work cohesively with SRP.

Additionally, the **Interface Segregation Principle** is also applied to this architecture. The idea of ISP is to make sure classes and functions aren't being forced to use interfaces that aren't relevant to the code that someone is working with. This, essentially, makes the programming more precise, clean, and uses less data so that clients are not exposed to methods they don’t need. For example the `scale.linear.js` and `scale.time.js` are two interfaces that have their own separate purpose with a specific set of functions that only they need. Although they are both exporting scales, they are both different types of scales, therefore they are producing different outputs. The `scale.linear.js` is importing other components and functions like `LinearScaleBase` and `Ticks`, whereas `scale.time.js` is not importing those functions and only importing necessary functions specific to their needs like the adapter functions to format time and other helper functions to deal with the math and objects. Another example proving the ISP does adhere to this architecture is in [`index.js`](https://github.com/kvpoch/Chart.js/blob/master/src/index.js). This interface is importing essentially everything from the other interfaces to create a chart. However, it is not importing every `Element`, `Scale`, `Animation`, and more, but only the one needed. For example, if the client wants to create a bar chart, the structure is set up in a way that allows `index.js` to just import the bar chart functions and not the functions for a scatter plot, line chart, and more. Overall, this architecture adheres to ISP because it has separate and independent interfaces to deal with different purposes, which reduces the side effects and frequency of required changes.

Another important OOP design principle of object-oriented programming is the **Open-Closed Principle**. It is the idea that elements should be open for extension but not for modification, where developers should be able to add new functionalities to a program but it shouldn't modify the current functionalities and current code. Chart.js uses inheritance for many of its components, including but not limited to elements, scales, and controllers. By using inheritance, the library violates the Open-Closed Principle. This is because changing the parent components would also require changing the child components, thus making it NOT closed for modification. For instance, the `BarController` and `LineController` components both inherit from the `DatasetController` class. If you wanted to modify any of the functions in `DatasetController` (for example, wanting to modify the `scaleClip` function to accept a different kind of scale as a parameter), you'd also need to edit `BarController` and `LineController` to handle that different kind of scale. This same idea applies to the `Bar` and `Line` components, which inherits from the `Element` class.

One of the SOLID Principles of class design is the **Dependency Inversion Principle (DIP)**, which is when high level modules do not depend on low-level modules. One example of how the Chart.js system adheres to this principle is the [`index.js`](https://github.com/kvpoch/Chart.js/blob/master/src/index.js) module in the `src` folder. All the modules in the `src` folder export particular interfaces that other modules and the  `index.js` will import, without having to worry about the details inside those modules. The `index.js` module acts as a way to manage the abstractions and as a place for other modules to communicate so that it can bring everything together and export the charts made. An specific example of how this system _violates_ DIP is the [`element.arc.js`](https://github.com/kvpoch/Chart.js/blob/master/src/elements/element.arc.js#L1) module. `Element.arc.js` simply depends on importing different functions from different modules. There is no “middle man” that manages the abstractions or acts as a point of communication or modification between modules. It just simply imports the `Element` function to implement inheritance to create a more specific version, known as the `ArcElement`.

Finally, this system follows the **Liskov Substitution Principle** - the principle that "objects should be replaceable with their subtypes without altering the correctness of the program." One instance of this principle is in both the [`Scale`](https://github.com/chartjs/Chart.js/blob/master/src/core/core.scale.js) and [`CategoryScale`](https://github.com/chartjs/Chart.js/blob/master/src/scales/scale.category.js) components. The subtype (`CategoryScale`) would be able to replace its parent (`Scale`). For instance, a new scale object of `CategoryScale` type is still able to use the `generateTickLabels()` and `calculateLabelRotation()` methods, which it would've inherited from `Scale`. This same principle applies to the [`Element`](https://github.com/chartjs/Chart.js/blob/master/src/core/core.element.js) and [`LineElement`](https://github.com/chartjs/Chart.js/blob/master/src/elements/element.line.js) components. The subtype  `LineElement` would be able to replace its parent `Element`. For example, a new element object of `LineElement` type can still viably use the `getProps()` and `hasValue()` methods that it would've inherited from `Element`.
## System Improvement

|Changes Made| Why|
|--|--|
|Refactoring: Rename Variable|A vague variable was previously named “o” in `element.arc.js`. This variable name is too obscure for viewers, giving them a more difficult time to understand the intent of this variable and how it contributes to the system. After investigating for quite a bit, this variable looks like it returns an object of numbers given to compute limits for the outer radius of the pie chart’s arc. Therefore this variable was renamed to be `RadiusCornersObj`. |
| Refactoring: Remove setting method | `plugin.legend.js` contains the method [`setDimensions`](https://github.com/chartjs/Chart.js/blob/285d84515989a6ce4488a2702ba7ede58a7498e6/src/plugins/plugin.legend.js#L84). However, dimensions will most likely not need to be altered after the first instantiation of a `Legend` component. Removing the setting method will make the dimensions immutable, or in the other words, remove the possibility of them accidentally being changed later on. Instead, the dimensions can be inserted as a parameter when first creating a `Legend`. |
| Refactoring: Replace Inline Code with Function Call | In `core.animator.js`, [`draw`](https://github.com/chartjs/Chart.js/blob/285d84515989a6ce4488a2702ba7ede58a7498e6/src/core/core.animator.js#L66) is explicitly instantiated to be false. It is determined to be true or not through a for loop that checks each element in an array against a conditional. This could be condensed by declaring `draw` equal to that conditional. This makes it easier to follow along what `draw` represents, and makes it more easily modifiable. Because of this, you won't have to hunt down each instance of `draw` being modified in an external function.
| Refactoring: Remove Middle Man | In `helpers.color.js` there was a constant, `isPatternOrGradient`, that was defined as a callback function. However, this was serving as a middle man between `color`/`getHoverColor` and a bar chart, for example. We can remove this middle man constant but just replacing the contents of that into the two functions. This makes it easier to understand as anyone who wants to directly edit the color or hover color can do so with solely those individual functions. |
