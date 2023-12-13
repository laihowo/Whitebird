![Whitebird Banner](https://github.com/BuchholzTim/Whitebird/wiki/images/banner.png)

# Introduction

- Whitebird is an open-source, web-based, collaborative, digital Whiteboard. My modification focused on the frontend tech stack [VueJS](https://github.com/vuejs) and [FabricJS](https://github.com/fabricjs/fabric.js). This is based on the business requirement of [YoTeach](https://yoteachapp.com/), a virtual classroom interaction platform for teachers and students. The live demo of the application is available at [My Public Classroom](https://yoteachapp.com/laihowo).

- When the object is selected, it will show the buttons for layer position, rotation, scale, lock movement and deletion. The users can undo and redo their operation. The buttons are on the top right corner of the object and hidden when the object is not selected.

- By making use of FabricJS, the users can pan the canvas and object with hand gesture. They zoom in and zoom out the object by using the pinch gesture or mouse wheel. They move the object by using the arrow keys.

- The whiteboard is responsive to the screen size. The initial position of new object is calculated based on the view port. Thus, the users can use the whiteboard on their desktop and mobile devices. 

<p align="center">
  <img src="https://github.com/BuchholzTim/Whitebird/wiki/images/demo.gif">
</p>

# Features

Currently the application is in early development and contains the following features:

- Creation of whiteboard rooms
- Joining whiteboard rooms via Join-Codes or Links

- Concurrent working on the whiteboard together with colleagues
- Export of the whiteboard as .png/.pdf
- Changeable Background: Use backgrounds as templates for organizing your whiteboard

- Whiteboard Tools
  - Creation of Text-Fields
  - Pencil for freehand drawing
  - Basic geometric objects: circle, square
  - Sticky Notes
  - Basic Edit Actions: Deleting, Moving, Rotating and Scaling of objects
    - Deleting is currently only supported by selecting & pressing the 'delete'-key.

# Getting Started

## For Users

To run the application you can use docker to setup the application. Visit our [Getting Started](https://github.com/BuchholzTim/Whitebird/wiki/Getting-Started) for more information on how to deploy the application.

## For Developers

As a developer always feel free to create issues or maybe try to add your own functionality / feature to the project. We have created a [Getting Started for Developers](https://github.com/BuchholzTim/Whitebird/wiki/Getting-Started-Dev), where the installation steps are explained. For further information about the used [Technologies](https://github.com/BuchholzTim/Whitebird/wiki/Technologies) and the [Architecture](https://github.com/BuchholzTim/Whitebird/wiki/Architecture) visit the corresponding pages.
