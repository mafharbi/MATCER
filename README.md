
# MATCER: MATLAB App for Quantitative Evaluation of Material Removal in Ceramic Machining

## Overview

**MATCER** is a MATLAB-based graphical application designed to quantify the material removal mechanisms in ceramic machining using digital image processing. The tool is intended for researchers, engineers, and students studying the brittle-to-ductile transition and surface integrity of ceramic components.

By analyzing microscopic images, MATCER distinguishes between brittle and ductile material removal zones and provides a precise percentage of ductile removal. This replaces subjective visual assessments with objective, repeatable analysis.

---

## Features

- GUI-based interface developed in MATLAB App Designer
- Automatic grayscale conversion and adaptive binarization
- User-defined region of interest (ROI) on the surface
- Real-time percentage calculation of ductile removal
- High-resolution support (minimum 1000x1000 pixels)

---

## System Requirements

- MATLAB R2021a or later
- Image Processing Toolbox
- Supported OS: Windows, Linux, or macOS

---

## Installation

1. Clone or download this repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/MATCER.git
   ```
2. Open `app1.m` in MATLAB.
3. Run the file. The App UI will launch automatically.

---

## Usage

1. Click **Upload** to load a high-resolution ceramic surface image (`.jpg`, `.png`, `.bmp`).
2. The app will:
   - Display the image and automatically overlay a 1000x1000 ROI.
   - Convert the ROI to grayscale and binarize it.
   - Compute and display the percentage of ductile removal based on pixel classification.
   - Show both original and processed images side-by-side.

---

## Example

Example Output:
```
Ductile Removal: 37.46%
```

---

## File Structure

- `app1.m`: The main App Designer file (MATLAB class)
- `LICENSE`: MIT License file
- `README.md`: Documentation and usage instructions

---

## Author

Dr. Mohammed Alharbi  
Department of Mechanical Engineering  
Umm Al-Qura University, Makkah, Saudi Arabia  
Email: mafharbi@uqu.edu.sa

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Citation

If you use this tool in your research, please cite:
```
Alharbi, M. (2025). MATCER: A MATLAB Tool for Quantitative Image-Based Analysis of Material Removal in Ceramic Machining. SoftwareX, [Manuscript in Review].
```
