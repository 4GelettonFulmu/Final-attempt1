# Interactive Webcam Halftone Dots

An interactive web application that captures live webcam video and displays it as a dynamic halftone pattern using individual dots. The dots respond to your voice volume by changing color and vibrating.

## Features

- **Live Webcam Capture**: Real-time video processing from your webcam
- **Halftone Effect**: Video is rendered as individual black and white dots
- **Independent Dot Elements**: Each dot is a separate object that can move and change color independently
- **Audio Reactivity**: Dots change color based on voice/sound volume
- **Vibration Effect**: Loud sounds cause dots to vibrate
- **Adjustable Parameters**:
  - Dot size (4-20 pixels)
  - Audio sensitivity (0.5-5x)
- **Visual Volume Meter**: Real-time display of audio input level

## How It Works

1. **Halftone Processing**: The webcam video is analyzed pixel by pixel, and brightness values are calculated for each dot region
2. **Audio Analysis**: Microphone input is processed using the Web Audio API to calculate volume levels
3. **Color Mapping**: When volume exceeds threshold:
   - Low volume (quiet): Green dots
   - Medium volume: Yellow dots
   - High volume (loud): Red dots
   - No sound: Black and white halftone
4. **Vibration**: Each dot independently vibrates with a phase-shifted sinusoidal motion proportional to volume

## Usage

### Running the Application

1. Open `index.html` in a modern web browser (Chrome, Firefox, Edge, or Safari)
2. Click the "Start Webcam & Audio" button
3. Grant permissions for webcam and microphone access when prompted
4. Speak, sing, or make sounds to see the dots react!

### Controls

- **Start Webcam & Audio**: Initializes the webcam and microphone
- **Stop**: Stops the application and releases camera/microphone
- **Dot Size Slider**: Adjusts the size of halftone dots (larger = fewer dots, more abstract)
- **Audio Sensitivity Slider**: Controls how responsive dots are to sound (higher = more reactive)

### Tips

- For best results, use good lighting
- Start with default sensitivity and adjust as needed
- Try different dot sizes for various artistic effects
- Experiment with different sounds (whisper, shout, music, clapping)

## Technical Details

### Technologies Used

- **HTML5 Canvas**: For rendering the halftone dots
- **Web Audio API**: For real-time audio analysis
- **MediaDevices API**: For webcam and microphone access
- **JavaScript ES6+**: For dot management and animations

### Key Components

- **Dot Class**: Each dot is an independent object with:
  - Position (base and offset for vibration)
  - Brightness (from video)
  - Color (RGB values with smooth transitions)
  - Vibration phase (for unique movement patterns)

- **Animation Loop**: 60 FPS rendering using `requestAnimationFrame`
- **Audio Analysis**: FFT-based frequency analysis with 256 samples
- **Color System**: HSL to RGB conversion for smooth color gradients

### Browser Compatibility

- Chrome/Edge: ✓ Full support
- Firefox: ✓ Full support
- Safari: ✓ Full support (iOS may require user interaction)
- Opera: ✓ Full support

**Note**: HTTPS or localhost is required for webcam/microphone access in most browsers.

## Customization

You can modify the code to:

- Change color schemes (modify the `hslToRgb` hue range)
- Adjust vibration patterns (modify `vibrationPhase` calculations)
- Add different effects (trails, glow, etc.)
- Change dot shapes (squares, triangles, etc.)

## Privacy

All video and audio processing happens locally in your browser. No data is sent to any server.

## License

Open source - feel free to modify and use as you wish!
