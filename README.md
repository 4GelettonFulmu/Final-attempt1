# Gesture-Controlled Halftone Webcam Application

A fullscreen, text-free interactive application that transforms live webcam footage into a halftone visual experience, controlled entirely through hand gestures.

## Features

### Visual Style
- **Liquid Physics Grid**: Dots behave like floating particles that react to movement
- Real-time halftone dot pattern with interactive physics simulation
- Black background with vibrant color palette: bright red, blue, magenta, and green
- Large, circular dots create a bold graphic style
- Dramatic dot size variation: much larger dots for figures, minimal/no dots for background
- Enhanced contrast algorithm creates striking visual separation
- **Smooth gradient color transitions** between gesture actions (no flash overlays)
- **Ambient motion**: Background dots gently float and breathe with sine wave animation
- **Interactive ripples**: Dots scatter away from hand movements and bounce back
- All halftone layers maintain 50% opacity for visual blending
- Completely fullscreen with no UI elements or text

### Gesture Interactions
- **Closed Fist**: Adds a frozen layer on top of existing layers
- **Open Hand (top/middle area)**: Freezes current frame and replaces all layers with a new single layer
- **Open Hand (bottom 25% of screen)**: Adds a frozen layer on top of existing layers
- **Smooth color transitions**: Each gesture triggers a gradient transition to the next color
- Automatic color cycling through: red → blue → magenta → green → red
- Visual hand position indicator (subtle circle) shows where your hand is detected
- 1-second cooldown between gestures to prevent accidental triggers
- **Motion-reactive dots**: Dots scatter away from hand movements and spring back

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
5. Watch the **smooth gradient color transitions** as you create layers
6. A subtle circle indicator shows where your hand is detected
7. Move your hand quickly to see the **interactive ripple effect** - dots scatter and bounce back

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

- **LiveDot Class**: Physics-enabled particles for live layer:
  - State tracking: position (currentX/Y), velocity (velocityX/Y), origin (originX/Y)
  - Spring-Damper physics system pulls dots back to origin
  - Friction/damping for smooth settling without oscillation
  - Repulsion forces scatter dots away from detected motion
  - Ambient sine wave motion for background dots (breathing/floating effect)
  - Brightness-based radius calculation (figures = large, background = small)

- **HalftoneLayer Class**: Static frozen snapshots:
  - Captured frame image data
  - Color assignment from vibrant palette optimized for black background
  - Pre-calculated halftone dots with brightness mapping
  - Dramatic dot size variation: figures = much larger dots, background = minimal/no dots
  - Enhanced contrast boost algorithm (2.0x) greatly exaggerates differences
  - 50% opacity for blending

- **Motion Detection System**:
  - Frame differencing algorithm compares consecutive video frames
  - Detects pixel changes above threshold
  - Applies repulsion forces to nearby dots
  - Creates interactive ripple effects

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

**Visual Parameters:**
- `dotSize`: Maximum size of halftone dots (default: 14px)
- `dotSpacing`: Spacing between dot centers (default: 12px)
- `maxLayers`: Maximum number of frozen layers (default: 10)
- `layerOpacity`: Opacity of each layer (default: 0.5)
- `colors`: Vibrant color array for black background (default: bright red, blue, magenta, green)
- `contrastBoost`: Greatly exaggerates brightness differences (default: 2.0)

**Physics Parameters:**
- `springStiffness`: How strongly dots return to origin (default: 0.015)
- `damping`: Friction/energy loss, 0-1 (default: 0.88)
- `repulsionRadius`: Distance at which motion affects dots (default: 80px)
- `repulsionStrength`: How strongly dots are pushed away (default: 12)
- `motionThreshold`: Minimum pixel difference to detect motion (default: 15)
- `ambientIntensity`: Background floating intensity (default: 2.5)
- `ambientSpeed`: Speed of ambient animation (default: 0.0015)
- `colorTransitionSpeed`: Speed of gradient transitions (default: 0.05)

**Gesture Parameters:**
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
