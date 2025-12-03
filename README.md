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
- **Left-to-right swipe anywhere on screen**: Freezes current frame and replaces all existing layers with a new halftone layer
- **Left-to-right swipe in bottom zone** (bottom 25% of screen): Adds a new frozen layer on top of existing layers
- Automatic color cycling through: red → yellow → blue → green → red

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
4. Use your index finger to perform left-to-right swipe gestures:
   - Swipe from left to right in the **middle/top area** to create a single layer (clears previous layers)
   - Swipe from left to right in the **bottom 25% of screen** to add layers on top of existing ones

### Keyboard Shortcuts

- **R** or **C**: Clear all frozen layers and reset to initial state

### Gesture Tips

- Ensure your hand is well-lit and visible to the camera
- Use your index finger to perform gestures
- Swipe at a moderate speed (not too fast or slow)
- The swipe must cover at least 30% of the screen width
- Complete the swipe within 500 milliseconds

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

- **Gesture Recognition**: Custom swipe detection system
  - Tracks index finger position
  - Calculates swipe distance and direction
  - Detects bottom zone vs. full screen swipes

- **Real-time Processing**: Live halftone rendering at camera frame rate
- **Layer System**: Efficient stacking with automatic color cycling

### Configuration Options

The application includes configurable parameters in the `CONFIG` object:

- `dotSize`: Size of halftone dots (default: 8px)
- `dotSpacing`: Spacing between dots (default: 10px)
- `maxLayers`: Maximum number of frozen layers (default: 10)
- `layerOpacity`: Opacity of each layer (default: 0.5)
- `bottomZoneHeight`: Height of bottom zone for stacking (default: 0.25 or 25%)
- `swipeThreshold`: Minimum swipe distance as percentage of screen width (default: 0.3 or 30%)
- `swipeTimeWindow`: Maximum time for swipe gesture in milliseconds (default: 500ms)

### Browser Compatibility

- Chrome/Edge 90+: ✓ Full support
- Firefox 88+: ✓ Full support
- Safari: Limited (MediaPipe support may vary)

**Note**: HTTPS or localhost is required for webcam access in most browsers.

## Privacy

All video processing happens locally in your browser. No data is sent to any server. MediaPipe Hands runs entirely client-side.

## License

Open source - feel free to modify and use as you wish!
