# TECHIN515 Magic Wand Project

This project implements a gesture recognition magic wand using an ESP32, MPU6050 sensor, and Edge Impulse machine learning. The system supports gesture data collection, model training, and real-time gesture inference with visual feedback.

## Project Structure

```
TECHIN515-magic-wand/
├── src/
│   ├── sketches/               # Arduino sketches and Edge Impulse exports
│   ├── python-scripts/         # Python scripts for data collection
│   └── dataset/                # Collected dataset (CSV files)
│
├── docs/
│   └── lab4_wand_report.pdf    # Final report
│
├── media/
│   ├── demo_link.txt           # Link to demo video
│   └── images                  # Project images (optional)
│
├── enclosure/
│   ├── final-enclosure-images/ # Enclosure/CAD images
│   └── notes.md                # Materials, design, and battery notes
│
├── README.md                   # This file
└── .gitignore                  # Ignore unnecessary files
```

## Hardware Setup
- **ESP32 development board**
- **MPU6050 sensor** (I2C: SDA=GPIO21, SCL=GPIO22)
- **Button** (D3)
- **RGB LED** (R: D7, G: D8, B: D9)
- **3.7V LiPo battery** (see enclosure/notes.md for details)

## Data Collection
1. Go to `src/python-scripts/` and install requirements:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
   ```
2. Upload `gesture_capture.ino` from `src/sketches/` to your ESP32.
3. Run the Python script to collect data:
   ```bash
   python process_gesture_data.py --gesture Z --person your_name --port /dev/cu.usbmodemXXXX
   ```
   - Data will be saved in `src/dataset/data/O`, `V`, `Z` folders as CSV files.

## Model Training (Edge Impulse)
1. Upload your dataset from `src/dataset/data/` to Edge Impulse.
2. Design, train, and test your model in Edge Impulse.
3. Export the model as an **Arduino library** and place all exported files (e.g., `Jazmyn-lab4_inferencing.h`, `.cpp`, etc.) in `src/sketches/`.

## Gesture Inference
1. Upload `wand_button_led.ino` (or `wand.ino`) from `src/sketches/` to your ESP32.
2. Ensure Edge Impulse export files are in the same folder.
3. Open Serial Monitor at 115200 baud.
4. Press the button to trigger gesture capture and see LED feedback for recognized gestures.

## Demo Video
- The demo video is available at the link in `media/demo_link.txt`.

## Enclosure
- See `enclosure/notes.md` for materials, design, and battery info.
- Enclosure images are in `enclosure/final-enclosure-images/`.

## Report
- The final report is in `docs/lab4_wand_report.pdf`.

## Troubleshooting
- **Missing libraries:** Install Adafruit MPU6050, Adafruit Sensor, and Edge Impulse SDK via Arduino Library Manager.
- **Edge Impulse include errors:** Ensure all exported files are in `src/sketches/`.
- **Serial port issues:** Specify the correct port with `--port` in the Python script.

## Credits
- Project for UW TECHIN515 Spring 2025
- See report for full references and acknowledgments.
