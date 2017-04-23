# ionic2-pinchzoom
Example of using pinch to zoom for div containers instead of just images, with multiple elements inside aligned vertically.

### How to run
run in terminal:

* `npm install`  
* `ionic platform add ios`
* `ionic run ios`

### Explanation

This is using one of ionics own imports called *Gesture*, which instantiates [Hammerjs](https://github.com/hammerjs/hammer.js)
to override **Pan, Pinch, and Tap** gestures in the element selected, this example uses the `<div #zoom>` element as the container
to 'zoom', with a fixed position, all of the elements inside have to have the same width, but can have different height.
Here each element has a red border to show where their boundaries are in order to see that it doesn't overflow, on zoom-in nor zoom-out

Hello everybody, I share this in hope that you don't waste as much time as I did on this, it still needs one more bug to fix but more on that below.

### What is this?
I have created a function that enables pinch to zoom using ionics **Gesture** import, for the **Pan and pinch** events to a div container with **Vertical** elements. Since I have googled this a lot a couldn't find an answer that would let me do this without the content being an image, I found that Ionic actually uses [HammerJS](https://github.com/hammerjs/hammer.js), to grab the touch gestures, and wraps them on the "Gesture" import as seen [Here](https://github.com/driftyco/ionic/blob/master/src/gestures/gesture.ts)

### The Magic

There are 3 files needed

* ~/src/pages/home/home.ts
* ~/src/pages/home/home.scss
* ~/src/pages/home/home.html

### home.html
The `<div #zoom class="zoom">` element is the **fixed container** that where we'll attach the events to, and its **children** are the items that will be zoomed.

### home.scss
`.zoom` to fill the container size, with a fixed position and the important `touch-action: none` which HammerJS needs. I have added the border color red, to show where the boundaries of each children are, so that we can see it doesn't overflow.

### home.ts

It takes the **Content** to figure out the actual size without the footer and headers getting in the way, the for loop just adds the absolute height of each children of #zoom. The original sizes equal to the viewport that the user sees minus the actual size of the content, since we override the scroll, the viewing of the content which will most likely overflow the bottom and right (because its fixed and can be any size), will be done via **panning** so we must know how much its overflowing.

the **max sizes** to pan are the original overflowed size, for now before zooming, and **scale** will equal to 1 at first.
**base** is to remember where we left off when pinched to zoom.

We initiate the event listening individually*, **panend & pancancel** as well as **pinchend & pinchcancel** are each called depending on the timing when you release the fingers so both must be added, to call their respective onEnd function.

#### setCoor function
sets the **x & y** coordinates making sure that it doesn't go past it's **max**
#### transform function
moves "translate", and scales the #zoom element, the **xx & yy** are for resetting the position
#### onPinchend function
sets the **base**, and sets the limits of the **scale**
#### onPinch function
sets the scale depending where it left off.
#### setBounds function
// hard to explain.

### TO-DO
The part that I am missing is that it zooms to the previous x & y coordinates, I need it to zoom to the center of the pinch.
Also to take account of negative margins the children might have.






