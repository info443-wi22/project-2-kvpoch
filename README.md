# INFO 443 Project 2 (chart.js)

## Context and Background

**What is the software system, and what does it do?**

`Chart.js` is an open-source JavaScript library for creating data visualizations. It can visualize your data in eight different ways, each of them animated, customizable, and responsive. It is great at rendering performance across modern browsers.

**Who created the software, and who currently "maintains" it? Was it developed by a large company or an independent developer? Who seems to be in charge of approving changes to its code/architecture?)**

`Chart.js` was originally created by developer Nick Downie in 2013. It is now open for contribution by the entire developer community, but a dedicated `Chart.js` team of seven people is in charge of approving changes.

**Where can we find more information about the system?**

Official repo:
https://github.com/chartjs/Chart.js
Documentation: https://www.chartjs.org/docs/latest/

## Development View

## Applied Perspective

## Identify Styles & Patterns

## Architectural Assessment

To start, we can discuss the architecture of `chart.js` in relation to **Single-Responsibility Principle**. SRP is when an element has one and only one reason to change or is responsible for only one actor. Whether it is in accordance to a class or a variable, there should be only one thing that the element is responsible for. `chart.js` does adhere to this principle because for elements such as 'backgroundColor', 'borderWidth', etc, they only accept values that will change properties for each type for element. For example, the 'borderWidth' element's job is to change the border width and thats it; it doesn't have any affect on the border color or the background color.

Additionally, the **Interface Segregation Principle** is also applied to this architecture. The idea of ISP is to make sure classes and functions aren't being forced to use interfaces that aren't relavant to the code that someone is working with. This, essentially, makes the programming more precise, clean, and uses less data. `chart.js` does this by creating interfaces and functions that are small and cohesive. A component interface only has  properties that are relevant for it. For example, if we look at `helpers.color.js` as one of the components, it is pretty short with only two functions and the name being pretty descriptive. It has a 'color' function and a 'getHoverColor' function that helps determine the color or hover color for anything that calls them. Within them, they also call a constant variable that creates a gradient if a user wants a gradient or not.

Another OOP design principle that is important and one of the main ideas of object-oriented programming is **Open-Closed Principle**. It is the idea that elements should be open for extension but not for modification, in that developers should be able to add new functionalities to a program but it should modify the current functionalities and current code. In a very basic context, a function having parameters allows for a program to be modifiable without editing existing code as you can see  `chart.js` implements in the below example. The hasRadius function has different behaviors based on the different elements put into the parameter.

![hasRadius function within a bar chart in chart.js](./images/ocp.png)
###### Figure 1: `hasRadius` function example
This function  `hasRadius` is within `element.bar.js`. It take in a parameter of the radius and returns a boolean in order to allow for users to know if a radius exists. It lets users to be able to modify the behavior without modifying the code itself.

Another example of this is for the `DatasetController` class and all the classes that inherit it. The `DatasetController` controls the data while there are other classes such as `LineController`, `BarController`, etc that extend this class. In order to create these different type of charts and chart controllers, the `DatasetController` does not need to be touched or modified; instead, there are other classes that create extensions to it.

## System Improvement
