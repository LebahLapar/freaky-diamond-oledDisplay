

https://github.com/user-attachments/assets/247239c3-a1ca-4f97-84e1-03f18aa298c5







# 💎 Freaky Diamond OLED Display

An IoT project to display a **Satono Diamond** character animation on a 128x64 SSD1306 OLED display using I2C communication with an ESP32 DevKit V1.

![ESP32](https://img.shields.io/badge/Platform-ESP32-blue)
![OLED](https://img.shields.io/badge/Display-SSD1306%20128x64-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 🎬 Demo

https://github.com/user-attachments/assets/satono-diamond.mp4

https://github.com/LebahLapar/freaky-diamond-oledDisplay/raw/main/video/satono-diamond.mp4

## 📖 Description

This project converts a GIF animation into monochrome bitmap arrays stored in program memory (PROGMEM), then displays them frame-by-frame on an OLED screen to create a smooth animation effect (~33 FPS).

## 🛠️ Hardware Components

| Component | Specification |
|-----------|---------------|
| Microcontroller | ESP32 DevKit V1 |
| Display | OLED SSD1306 I2C 128x64 pixels |
| Cables | Jumper wires (SDA, SCL, VCC, GND) |

## 📌 Wiring

| OLED Pin | ESP32 DevKit V1 |
|----------|-----------------|
| VCC | 3.3V |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |

> **Note:** The default I2C address used is `0x3C`. If the display doesn't turn on, try changing it to `0x3D`.

## 📦 Required Libraries

Install the following libraries via Arduino IDE Library Manager:

- [Adafruit SSD1306](https://github.com/adafruit/Adafruit_SSD1306)
- [Adafruit GFX Library](https://github.com/adafruit/Adafruit-GFX-Library)
- Wire (built-in)

## 📂 Project Structure

```
freaky-diamond-oledDisplay/
├── README.md
├── sketch_nov16a/
│   └── sketch_nov16a.ino          # Main Arduino sketch
└── dataset/
    ├── satono.gif                  # Original animation GIF
    ├── images.steamusercontent.gif # Source GIF
    ├── ezgif-split.zip            # Archive of split frames
    └── ezgif-split/               # Individual frames (37 frames)
        ├── frame_00_delay-0.03s.gif
        ├── frame_01_delay-0.04s.gif
        ├── ...
        └── frame_36_delay-0.03s.gif
```

## ⚙️ How It Works

1. **Frame Preparation** — The GIF animation is split into 37 individual frames using [ezgif.com](https://ezgif.com/split)
2. **Bitmap Conversion** — Each frame is converted into a monochrome (1-bit) bitmap array at 128x64 pixels using a tool like [image2cpp](https://javl.github.io/image2cpp/)
3. **Storage** — Bitmap arrays are stored in PROGMEM to avoid consuming RAM
4. **Animation** — The main loop displays frames sequentially with a 30ms delay (~33 FPS)

## 🚀 Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/LebahLapar/freaky-diamond-oledDisplay.git
   ```

2. **Open the sketch in Arduino IDE:**
   - Open `sketch_nov16a/sketch_nov16a.ino`

3. **Install libraries:**
   - Go to *Sketch > Include Library > Manage Libraries*
   - Search and install `Adafruit SSD1306` and `Adafruit GFX Library`

4. **Configure the board:**
   - Go to *Tools > Board* and select `ESP32 Dev Module`
   - Select the correct port in *Tools > Port*

5. **Upload:**
   - Click the Upload button

## 🔧 Configuration

Some parameters you can adjust in the sketch:

```cpp
#define SCREEN_WIDTH 128    // OLED width (pixels)
#define SCREEN_HEIGHT 64    // OLED height (pixels)
#define OLED_RESET    -1    // Reset pin (-1 if sharing with Arduino reset)

const int FRAME_COUNT = 35; // Total number of animation frames

delay(30);                  // Animation speed (ms per frame)
```

## 🎨 Create Your Own Animation

Want to replace the animation with a different GIF? Follow these steps:

1. **Split the GIF** — Upload your GIF to [ezgif.com/split](https://ezgif.com/split) to get individual frames
2. **Resize** — Make sure each frame is 128x64 pixels
3. **Convert to bitmap** — Use [image2cpp](https://javl.github.io/image2cpp/) with the following settings:
   - Canvas size: 128x64
   - Background color: Black
   - Invert image colors: adjust as needed
   - Output format: Arduino code
4. **Replace arrays** — Paste the converted output into the sketch, replacing the existing arrays
5. **Update FRAME_COUNT** — Adjust the frame count accordingly

## ⚠️ Important Notes

- This project requires a significant amount of program memory (Flash) since it stores 37 bitmap frames. Make sure your board has enough Flash available.
- The ESP32 has 4MB of Flash, which is more than sufficient for this project.
- Animation speed can be adjusted by changing the `delay()` value in the `loop()` function.

## 📜 License

This project is made for educational and hobby purposes.

## 👤 Author

**LebahLapar** — [GitHub](https://github.com/LebahLapar)

---

⭐ If you find this project useful, don't forget to give it a star!
