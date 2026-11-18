#  Lane Detection

##  Aim

To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.

---

## Learning Objective

* Understand each stage of image processing
* Learn how to build a complete computer vision pipeline
* Practice writing code in guided sections

**Important Instruction:**
👉 Write code **ONLY in places marked as `# Your Code Here`**
👉 Do NOT modify any other part of the code

---

##  Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (cv2)
* NumPy
* Matplotlib

---

##  Algorithm & Explanation

---

###  Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

###  Step 2: Read the Image

```python
image_path = list(uploaded.keys())[0]

img = cv2.imread(image_path)

img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

print("Image loaded successfully")
```

---

###  Step 3: Convert to Grayscale

```python
gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)
```

---

###  Step 4: Display Images

```python
plt.figure(figsize=(10,5))
plt.imshow(gray, cmap='gray')
plt.title("Grayscale Image")
plt.axis('off')
plt.show()
```

---

###  Step 5: Thresholding

```python
threshold = 150

_, thresh = cv2.threshold(gray, threshold, 255, cv2.THRESH_BINARY)

plt.figure(figsize=(10,5))
plt.imshow(thresh, cmap='gray')
plt.title("Thresholded Image")
plt.axis('off')
plt.show()
```

---

###  Step 6: Region of Interest (ROI)

```python
height, width = gray.shape

mask = np.zeros_like(gray)

polygon = np.array([[
    (0, height),
    (width, height),
    (width, int(height * 0.6)),
    (int(width * 0.5), int(height * 0.4)),
    (0, int(height * 0.6))
]], np.int32)

cv2.fillPoly(mask, polygon, 255)

roi = cv2.bitwise_and(thresh, mask)

plt.figure(figsize=(10,5))
plt.imshow(roi, cmap='gray')
plt.title("ROI Masked Image")
plt.axis('off')
plt.show()
```

---

### Step 7: Edge Detection (Canny)

```python
edges = cv2.Canny(roi, 50, 150)

plt.figure(figsize=(10,5))
plt.imshow(edges, cmap='gray')
plt.title("Edge Detected Image")
plt.axis('off')
plt.show()
```

---

###  Step 8: Gaussian Blur

```python
blur = cv2.GaussianBlur(edges, (5,5), 0)

plt.figure(figsize=(10,5))
plt.imshow(blur, cmap='gray')
plt.title("Gaussian Blurred Image")
plt.axis('off')
plt.show()
```

---

###  Step 9: Hough Transform

```python
# Detect lines using Hough Transform
# Detect lines using Hough Transform

lines = cv2.HoughLinesP(
    blur,
    rho=1,
    theta=np.pi/180,
    threshold=50,
    minLineLength=40,
    maxLineGap=100
)

line_img = np.zeros_like(img)

if lines is not None:
    for line in lines:
        x1, y1, x2, y2 = np.array(line).flatten()[:4]

        cv2.line(line_img, (int(x1), int(y1)),
                 (int(x2), int(y2)), (255, 0, 0), 5)

plt.figure(figsize=(10,5))
plt.imshow(line_img)
plt.title("Detected Lines")
plt.axis('off')
plt.show()
```

---

### Step 10: Lane Detection Logic

```python
final = cv2.addWeighted(img, 0.8, line_img, 1, 0)

plt.figure(figsize=(12,6))
plt.imshow(final)
plt.title("Final Lane Detection Output")
plt.axis('off')
plt.show()
```

---

##  Expected Output

* Original image
* Grayscale image
* Thresholded image
* ROI masked image
* Edge detected image
* Smoothed image
* Detected lines
* Final lane detection output

<img width="890" height="1190" alt="image" src="https://github.com/user-attachments/assets/3204f438-c169-4575-91b8-840b8e9b7481" />


---

##  Instructions

* Fill ONLY in `# Your Code Here` sections
* Do NOT change existing code
* Run step-by-step
* Verify outputs

---

## Result

Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.

---

##  Developed By

* **Name:** ____________________________
* **Register No:** ______________________
