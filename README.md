# OCR-Based-Document-Data-Extraction-System

# OCR Preprocessing and Data Extraction Script

## Overview
This Python script preprocesses image data and extracts OCR (Optical Character Recognition) results from a JSON file. The script reads images and OCR data from Google Drive, processes the data to extract relevant information, and saves the results in a CSV file.

## Prerequisites
To run this script, you'll need to have the following installed:
- Google Colab (or another environment with Google Drive access)
- Python 3.x
- Required Python libraries:
  - `opencv-python-headless`
  - `pandas`
  - `openpyxl`
  - `tesseract-ocr`
  - `libtesseract-dev`

## Setup Instructions
1. **Mount Google Drive:**
   Ensure your Google Drive is mounted to access the images and JSON file.

   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```

2. **Install Required Libraries:**
   Install the necessary Python libraries and Tesseract OCR.

   ```bash
   !pip install opencv-python-headless pandas openpyxl
   !apt-get install -y tesseract-ocr
   !apt-get install -y libtesseract-dev
   ```

3. **Directory Structure:**
   - **Images Folder:** Store your images in a folder on Google Drive, e.g., `/content/drive/MyDrive/Images`.
   - **JSON File:** The OCR results should be in a JSON file on Google Drive, e.g., `/content/drive/MyDrive/filtered-data.json`.
   - **Output CSV:** The output CSV file will be saved in the specified path, e.g., `/content/Output_assessment.csv`.

## Script Explanation
1. **Loading JSON Data:**
   The script loads OCR data from a JSON file, which contains information about the image paths, document type, size, and OCR text with corresponding coordinates.

2. **Image Processing:**
   The script reads each image file using OpenCV, and if the image is not found or cannot be loaded, it skips that file.

3. **Text Labeling:**
   The script identifies whether the extracted OCR text matches any predefined template text (like 'Republic', 'Estonia', etc.). If a match is found, the text is labeled as `unknown`; otherwise, it's labeled as `user_data`.

4. **Coordinate and Ratio Calculation:**
   The script extracts and normalizes the bounding box coordinates for each OCR text entry, calculating the width and height of the bounding box, along with their respective ratios compared to the original image dimensions.

5. **Saving Results:**
   All processed data is saved into a CSV file, with columns detailing the document path, text label, extracted text, coordinates, dimensions, and ratios.

## Output
The script generates a CSV file (`Output_assessment.csv`) containing the following columns:
- **Document Path:** Full path of the processed image.
- **Label:** Indicates whether the text is `unknown` or `user_data`.
- **Text:** The OCR-extracted text.
- **X Coordinates:** List of x-coordinates for the bounding box.
- **Y Coordinates:** List of y-coordinates for the bounding box.
- **Width:** Width of the bounding box.
- **Height:** Height of the bounding box.
- **Width Ratio:** Ratio of the bounding box width to the image width.
- **Height Ratio:** Ratio of the bounding box height to the image height.

## Notes
- Ensure that the image filenames in the JSON match those in the specified images folder.
- The script is designed to work with JPEG images, but can be adapted for other formats if necessary.

## Acknowledgements
This script leverages several open-source libraries, including OpenCV for image processing and Tesseract for OCR.
