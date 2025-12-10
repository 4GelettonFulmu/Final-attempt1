# Gesture-Controlled Halftone Webcam Application

A fullscreen, text-free interactive application that transforms live webcam footage into a halftone visual experience, controlled entirely through hand gestures.

## Features

### Visual Style
- **Liquid Physics Grid**: Dots behave like floating particles with subtle micro-fluctuations
- Real-time halftone dot pattern with low-latency physics simulation
- Black background with vibrant color palette: bright red, blue, magenta, and green
- Large, circular dots create a bold graphic style
- Dramatic dot size variation: much larger dots for figures, minimal/no dots for background
- Enhanced contrast algorithm creates striking visual separation
- **Smooth gradient color transitions** between gesture actions (no flash overlays)
- **Subtle ambient motion**: Background dots gently breathe (1-2px movement, barely visible)
- **Micro-ripples**: Dots shift only 5-10px when motion detected, instant snap back
- Frozen layers display at 50% opacity for visual blending
- Completely fullscreen with no UI elements or text

### Gesture Interactions
- **Closed Fist**: Freezes current frame as a translucent halftone layer (replaces previous)
- **Open Hand**: Freezes current frame as a translucent halftone layer (replaces previous)
- **Smooth color transitions**: Each gesture triggers a gradient transition to the next color
- Automatic color cycling through: red → blue → magenta → green → red
- Visual hand position indicator (subtle circle) shows where your hand is detected
- 1-second cooldown between gestures to prevent accidental triggers
- **Motion-reactive dots**: Subtle micro-ripples respond to hand movements (5-10px displacement)

### Freeze Frame Behavior
- Each gesture creates a new translucent halftone snapshot (50% opacity)
- **Each freeze frame replaces the previous one** (no stacking)
- Colors blend naturally through 50% transparency overlay
- Live layer continues to move with physics while frozen layer remains static
- Smooth gradient transitions between colors with each new freeze

## Usage

### Running the Application

1. Open `index.html` in a modern web browser (Chrome, Edge, or Firefox recommended)
2. Grant camera permissions when prompted
3. The application will automatically enter fullscreen mode
4. Perform hand gestures in front of your camera:
   - **Make a fist** (close your hand) to freeze the current frame
   - **Show an open hand** to freeze the current frame
   - Each freeze replaces the previous frozen layer
5. Watch the **smooth gradient color transitions** as you create freeze frames
6. A subtle circle indicator shows where your hand is detected
7. Move your hand to see **subtle micro-ripples** - dots shift slightly (5-10px) and snap back instantly

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

**Physics Parameters (Tuned for Subtle Micro-Fluctuations):**
- `springStiffness`: High stiffness - dots tightly anchored (default: 0.09, was 0.015)
- `damping`: High damping - instant snap back, no wobble (default: 0.94, was 0.88)
- `repulsionRadius`: Smaller radius for localized effect (default: 60px, was 80px)
- `repulsionStrength`: Much weaker push - only 5-10px displacement (default: 3.5, was 12)
- `motionThreshold`: Minimum pixel difference to detect motion (default: 15)
- `ambientIntensity`: Barely visible breathing - 1-2px movement (default: 1.2, was 2.5)
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
