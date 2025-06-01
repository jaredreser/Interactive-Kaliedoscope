# Interactive-Kaliedoscope
Interactive 3D Kaleidoscope with Three.js & lil-gui
This project is a web-based interactive 3D kaleidoscope simulation built using Three.js for the 3D rendering and lil-gui for real-time parameter control. Users can explore mesmerizing, ever-changing patterns created by mirrored segments of animated 3D objects.

Features
Dynamic Kaleidoscope Effect: Simulates a traditional kaleidoscope by cloning a set of "source" 3D objects and arranging them in mirrored segments around a central axis.

Interactive Camera Controls: Uses Three.js OrbitControls to allow users to:

Rotate the view around the kaleidoscope.

Zoom in and out.

Pan the camera (though typically the focus is on rotation and zoom).

Animated Objects: The individual 3D objects within the kaleidoscope have their own animations:

Ambient Tumbling & Drifting: Objects slowly rotate and change position, creating a constantly evolving base pattern.

Individual Spin: Each object can spin on its own unique axis.

Responsive Tumbling: The tumbling and spinning speed of the objects increases significantly when the user actively rotates the camera view, providing a more dynamic and interactive feel.

GUI Controls (lil-gui): A user-friendly interface allows real-time adjustment of various parameters:

Structure:

Number of kaleidoscope segments.

Number of objects in the source pattern.

Maximum size of the objects.

Spread/distribution of the objects.

Animation:

Speed of the kaleidoscope's overall auto-rotation.

Speed of individual objects' world-axis spin.

Speed of objects' ambient drift.

Speed of objects' personal tumbling/rotation.

Multiplier for animation speed when the user is dragging/rotating the view.

Customizable Visuals (Code-based):

Object geometries currently include Boxes, Spheres, and TorusKnots, chosen randomly.

Objects are assigned random colors from a predefined palette, with a subtle emissive quality.

Responsive Design: The canvas and rendering adapt to window resizing.

How It Works
Scene Setup: A basic Three.js scene is initialized with a camera, renderer, lighting (ambient and directional), and OrbitControls.

Source Objects: A configurable number of 3D objects (sourceObjects) are created with random geometries, materials (colors), initial positions, and rotations. Each object is also assigned userData properties to define its base animation behavior (drift velocity, rotation speed, spin axis).

Kaleidoscope Construction (buildKaleidoscopePattern):

The kaleidoscopeGroup (a THREE.Group) holds all the segments.

For the specified numSegments:

A new THREE.Group (a segmentGroup) is created.

All sourceObjects are cloned, and their userData (animation parameters) are copied to these clones.

The segmentGroup is rotated around the Z-axis by an angle corresponding to its segment index.

To achieve the classic mirrored effect, alternate segments are scaled by -1 along their Y-axis.

The segmentGroup is added to the main kaleidoscopeGroup.

Animation Loop (animate):

The main kaleidoscopeGroup can auto-rotate.

User Interaction Boost: A speedMultiplier is calculated. If the user is actively dragging the camera (detected via OrbitControls 'start' and 'end' events), this multiplier increases, making object animations more energetic.

Source Object Animation: The sourceObjects are animated by updating their positions (based on baseVelocity and objectDriftSpeed) and rotations (based on baseRotationSpeed and objectPersonalRotateSpeed), scaled by the speedMultiplier. A simple boundary check makes them "bounce" if they drift too far.

Clone Updates: The positions and rotations of the cloned objects within each segment are updated every frame to match their corresponding (now animated) sourceObject.

Individual Spin: Each clone also performs its own independent spin on its worldRotationAxis, scaled by objectWorldRotateSpeed, worldRotationSpeedFactor, and the speedMultiplier.

GUI Integration (setupGUI):

lil-gui is used to create controls bound to the params object.

Changes to structural parameters (like numSegments or objectCount) trigger a call to createSourceSegmentObjects (if necessary) and buildKaleidoscopePattern to regenerate the kaleidoscope.

Changes to animation speed parameters update the params object, which is then used directly in the animate loop.

To Run
Ensure you have a modern web browser with WebGL support.

Save the HTML file (containing the JavaScript module).

Open the HTML file in your browser.

You should see the interactive kaleidoscope and a GUI panel (usually top-right) to control its parameters.

Potential Future Enhancements
More diverse and complex object geometries.

User-selectable color palettes or individual color controls.

Post-processing effects (e.g., bloom for a neon glow, depth of field).

Sound reactivity.

Option to "shake" the kaleidoscope for a completely new random arrangement of source objects.

More sophisticated object interaction/collision simulation.
