
## Dataset
The datasets used for this project are [Helmet Detection Project](https://universe.roboflow.com/nckh-2023/helmet-detection-project), [Face Detection](https://universe.roboflow.com/mohamed-traore-2ekkp/face-detection-mik1i), and [Two Wheeler Lane Detection](https://universe.roboflow.com/prathamjaiswal/two-wheeler-lane-detection).

## Detected Objects
- Helmet Detection Project: Two-wheeler/motorcyclist, Helmet, License Plate
- Face Detection: Human Face
- Two Wheeler Lane Detection: Front-facing motorcycle, Rear-facing motorcycle

## Violations
- Wrong Lane: Driving away from the camera.
- No Helmet: Any rider not wearing a helmet.
- Triple riding: More than two riders.

## Process Flow
1. **Motorcycle Detection:**
   - Detects all two-wheelers/motorcycles in a frame.
2. **Bounding Box Extraction:**
   - For each detected motorcycle, extracts its bounding box.
3. **Orientation Check:**
   - Determines if the motorcycle is front-facing or rear-facing.
   - Flags a "Wrong Lane Violation" if the motorcycle is rear-facing.
4. **Face and Helmet Detection:**
   - Detects faces and helmets within the cropped image.
   - Counts the number of faces.
   - Reduces the face count if the detected face and helmet areas overlap by more than 60%.
5. **No Helmet Violation:**
   - Detects helmets again and counts them.
   - Flags a "No Helmet Violation" if no helmets are detected or if the number of faces is greater than 1.
6. **Triple Riding Violation:**
   - Sums up the final counts of helmets and faces.
   - Flags a "Triple Riding Violation" if the sum is greater than 2.
7. **License Plate Detection:**
   - If any violation is detected, captures the license plate using the [OCR.Space API](https://ocr.space/OCRAPI).
8. **Saving Violation Data:**
   - Saves the violated motorcycle image along with its license plate image and text.
   - Records the list of violations for each image.
