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

// TO-DO
