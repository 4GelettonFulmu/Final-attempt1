# Gesture-Controlled Halftone Webcam Application

A fullscreen, text-free interactive application that transforms live webcam footage into a halftone visual experience, controlled entirely through hand gestures.

## Features

### Visual Style
- Real-time halftone dot pattern effect applied to live webcam feed
- Limited color palette: red, yellow, blue, and green
- Only one color displayed at a time
- All halftone layers maintain 50% opacity for visual blending
- Completely fullscreen with no UI elements or text

### Gesture Interactions
- **Closed Fist**: Adds a frozen layer on top of existing layers (green flash feedback)
- **Open Hand (top/middle area)**: Freezes current frame and replaces all layers with a new single layer (yellow flash feedback)
- **Open Hand (bottom 25% of screen)**: Adds a frozen layer on top of existing layers (yellow flash feedback)
- Automatic color cycling through: red → yellow → blue → green → red
- Visual hand position indicator (subtle circle) shows where your hand is detected
- 1-second cooldown between gestures to prevent accidental triggers

### Layering Behavior
- Each frozen frame transforms into a semi-transparent halftone layer
- Multiple swipes create overlapping compositions
- Colors blend naturally through 50% transparency stacking
- Maximum of 10 layers (oldest layer is removed when limit is reached)

## Usage

### Running the Application

1. Open `index.html` in a modern web browser (Chrome, Edge, or Firefox recommended)
2. Grant camera permissions when prompted
3. The application will automatically enter fullscreen mode
4. Perform hand gestures in front of your camera:
   - **Make a fist** (close your hand) to add a new layer on top of existing layers
   - **Show an open hand** in the top/middle area to create a single layer (clears previous layers)
   - **Show an open hand** in the bottom 25% of screen to add layers on top of existing ones
5. Watch for visual feedback: green flash for fist, yellow flash for open hand
6. A subtle circle indicator shows where your hand is detected

### Keyboard Shortcuts

- **R** or **C**: Clear all frozen layers and reset to initial state

### Gesture Tips

- Ensure your hand is well-lit and visible to the camera
- Hold gestures clearly for best detection (fully closed fist or fully open hand)
- Wait for the visual feedback flash before performing the next gesture
- The hand position indicator (circle) helps you see where the system detects your hand
- Position your hand in different zones to control layer behavior
- There's a 1-second cooldown between gestures to prevent accidental double-triggers

## Technical Details

### Technologies Used

- **HTML5 Canvas**: For rendering halftone dots and layers
- **MediaDevices API**: For real-time webcam access
- **MediaPipe Hands**: For accurate hand tracking and gesture recognition
- **JavaScript ES6+**: For layer management and gesture processing

### Key Components

- **HalftoneLayer Class**: Each frozen layer contains:
  - Captured frame image data
  - Color assignment (red, yellow, blue, or green)
  - Pre-calculated halftone dots with brightness mapping
  - 50% opacity for blending

- **Gesture Recognition**: Custom hand pose detection system
  - Detects closed fist (all fingers near palm)
  - Detects open hand (all fingers extended)
  - Tracks wrist position for zone detection
  - Cooldown system prevents accidental double-triggers
  - Visual feedback system (flash and hand indicator)

- **Real-time Processing**: Live halftone rendering at camera frame rate
- **Layer System**: Efficient stacking with automatic color cycling

### Configuration Options

The application includes configurable parameters in the `CONFIG` object:

- `dotSize`: Size of halftone dots (default: 8px)
- `dotSpacing`: Spacing between dots (default: 10px)
- `maxLayers`: Maximum number of frozen layers (default: 10)
- `layerOpacity`: Opacity of each layer (default: 0.5)
- `bottomZoneHeight`: Height of bottom zone for stacking (default: 0.25 or 25%)
- `gestureCooldown`: Milliseconds between gesture triggers (default: 1000ms)
- `handClosedThreshold`: Distance threshold for fist detection (default: 0.1)

### Browser Compatibility

- Chrome/Edge 90+: ✓ Full support
- Firefox 88+: ✓ Full support
- Safari: Limited (MediaPipe support may vary)

**Note**: HTTPS or localhost is required for webcam access in most browsers.

## Privacy

All video processing happens locally in your browser. No data is sent to any server. MediaPipe Hands runs entirely client-side.

## License

Open source - feel free to modify and use as you wish!
