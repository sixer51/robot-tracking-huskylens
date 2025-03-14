# HuskyLens Robot Tracking

This project sets up and runs a **HuskyLens-based tracking system** to detect and track a tagged moving object, here robot. The camera hangs above the object and outputs its **X and Y position in cm**.

## Prerequisites

Ensure you have the following before proceeding:

- **HuskyLens** camera module
- **pip** (Python package manager)

---

## **1. Set Up a Virtual Environment**

To isolate dependencies, create and activate a **virtual environment**:

### **On macOS/Linux**
```bash
python3 -m venv venv
source venv/bin/activate
```

### **On Windows**
```powershell
python -m venv venv
venv\Scripts\activate
```

---

## **2. Install Dependencies**



Install dependencies:

```bash
pip install pyserial pypng numpy
```

---

## **3. List Available Serial Ports (For Debugging)**

Check if the HuskyLens is connected and find the correct serial port:

### **On macOS/Linux**
```bash
ls /dev/tty.*
ls /dev/cu.*
```

### **On Windows (PowerShell)**
```powershell
Get-WMIObject Win32_SerialPort
```

---

## **4. Camera Spatial Resolution Calibration**

Setup four large April tags as four corner of a square, and measure the width and height of the square. The dimension should reflect the distance between the central position of the tags. Ideally, the width align with the x-axis of the image, and height align with the y-axis of the image.

Change `width_physical` and `height_physical` to the measured width and height.

Set the camera to **Tag Recognition** mode.

Execute the camera calibration script:

```bash
python camera_calibration.py
```

Get the output of `cm_per_pixel_x` and `cm_per_pixel_y` from terminal. They should be very similar values.

## **5. Run the HuskyLens Tracking Script**

Change the value of `cm_per_pixel_x` and `cm_per_pixel_y` to the result from last step

Execute the main tracking script:

```bash
python robot-tracking.py
```

If the script fails due to a **serial connection error**, double-check the correct port and modify the script:

```python
hl = HuskyLensLibrary("SERIAL", "/dev/cu.usbserial-10", 3000000)
```
Change `/dev/cu.usbserial-10` to match your system’s detected port.

---


## **6. Exit the Virtual Environment**
When done, deactivate the virtual environment:

```bash
deactivate
```
