# Image-handling-and-Pixel-transformation-using-openCV
## NAME:PORKODI B
## REG NO:212224240114
## AIM: 
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels.

### Ex. No. 01

#### 1. Read the image ('city.jpg') using OpenCV imread() as a grayscale image.
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread("PORKO.jpg", cv2.IMREAD_GRAYSCALE)
```

#### 2. Print the image width, height & Channel.
```python
height, width = img.shape

print("Width :", width)
print("Height:", height)
print("Channel: 1")
```

#### 3. Display the image using matplotlib imshow().
```python
plt.imshow(img, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
cv2.imwrite("PORKO.png", img)
print("Image saved successfully.")
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
img_gray = cv2.imread("city.png", cv2.IMREAD_GRAYSCALE)
img_color = cv2.cvtColor(img_gray, cv2.COLOR_GRAY2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
plt.imshow(img_color)
plt.title("Colour Image")
plt.axis("off")
plt.show()

height, width, channel = img_color.shape

print("Width :", width)
print("Height:", height)
print("Channel:", channel)
```

#### 7. Crop the image to extract any specific object from the image.
```python
cropped = img_color[150:450, 200:500]

plt.imshow(cropped)
plt.title("Cropped Image")
plt.axis("off")
plt.show()
```

#### 8. Resize the image up by a factor of 2x.
```python
resized = cv2.resize(
    img_color,
    None,
    fx=2,
    fy=2,
    interpolation=cv2.INTER_LINEAR
)

plt.imshow(resized)
plt.title("Resized Image (2x)")
plt.axis("off")
plt.show()
```

#### 9. Flip the cropped/resized image horizontally.
```python
flipped = cv2.flip(cropped, 1)

plt.imshow(flipped)
plt.title("Horizontally Flipped Image")
plt.axis("off")
plt.show()
```

#### 10. Read in the image ('city.jpg').
```python
img = cv2.imread("PORKO.jpg")
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image).
```python
text = "Smart City View"
font_face = cv2.FONT_HERSHEY_PLAIN

text_position = (180, img_rgb.shape[0] - 20)

cv2.putText(
    img_rgb,
    text,
    text_position,
    font_face,
    2,
    (255, 255, 255),
    2,
    cv2.LINE_AA
)
```

#### 12. Draw a magenta rectangle that encompasses any prominent object in the image.
```python
rect_color = (255, 0, 255)

cv2.rectangle(
    img_rgb,
    (250, 180),
    (500, 450),
    rect_color,
    3
)
```

#### 13. Display the final annotated image.
```python
plt.imshow(img_rgb)
plt.title("Annotated City Image")
plt.axis("off")
plt.show()
```

#### 14. Read the image ('city.jpg').
```python
img = cv2.imread("PORKO.jpg")
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

#### 15. Adjust the brightness of the image.
```python
# Create a matrix of ones (with data type float64)

matrix = np.ones(img.shape, dtype="uint8") * 50
```

#### 16. Create brighter and darker images.
```python
img_brighter = cv2.add(img, matrix)
img_darker = cv2.subtract(img, matrix)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
plt.figure(figsize=(15,5))

plt.subplot(1,3,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB))
plt.title("Darker Image")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB))
plt.title("Brighter Image")
plt.axis("off")

plt.show()
```

#### 18. Modify the image contrast.
```python
# Create two higher contrast images using the 'scale' option
# with factors of 1.1 and 1.2 (without overflow fix)

img_higher1 = cv2.convertScaleAbs(img, alpha=1.1, beta=0)
img_higher2 = cv2.convertScaleAbs(img, alpha=1.2, beta=0)
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
plt.figure(figsize=(15,5))

plt.subplot(1,3,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(cv2.cvtColor(img_higher1, cv2.COLOR_BGR2RGB))
plt.title("Contrast 1.1")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(cv2.cvtColor(img_higher2, cv2.COLOR_BGR2RGB))
plt.title("Contrast 1.2")
plt.axis("off")

plt.show()
```

#### 20. Split the image into the B, G, R components & Display the channels.
```python
B, G, R = cv2.split(img)

plt.figure(figsize=(12,4))

plt.subplot(1,3,1)
plt.imshow(B, cmap="gray")
plt.title("Blue")

plt.subplot(1,3,2)
plt.imshow(G, cmap="gray")
plt.title("Green")

plt.subplot(1,3,3)
plt.imshow(R, cmap="gray")
plt.title("Red")

plt.show()
```

#### 21. Merge the R, G, B displays along with the original image.
```python
merged_rgb = cv2.merge((R, G, B))

plt.figure(figsize=(10,5))

plt.subplot(1,2,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original")

plt.subplot(1,2,2)
plt.imshow(merged_rgb)
plt.title("Merged RGB")

plt.axis("off")
plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

H, S, V = cv2.split(hsv)

plt.figure(figsize=(12,4))

plt.subplot(1,3,1)
plt.imshow(H, cmap="gray")
plt.title("Hue")

plt.subplot(1,3,2)
plt.imshow(S, cmap="gray")
plt.title("Saturation")

plt.subplot(1,3,3)
plt.imshow(V, cmap="gray")
plt.title("Value")

plt.show()
```

#### 23. Merge the H, S, V displays along with the original image.
```python
merged_hsv = cv2.merge((H, S, V))
merged_bgr = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)

plt.figure(figsize=(10,5))

plt.subplot(1,2,1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original")

plt.subplot(1,2,2)
plt.imshow(cv2.cvtColor(merged_bgr, cv2.COLOR_BGR2RGB))
plt.title("Merged HSV")

plt.axis("off")
plt.show()
```

## Output:
<img width="440" height="522" alt="image" src="https://github.com/user-attachments/assets/ce5b55d9-6303-4054-be65-716ee821faf6" />

<img width="477" height="522" alt="image" src="https://github.com/user-attachments/assets/f8afaa9b-18fc-4b2e-82c3-125b4a637f23" />

<img width="493" height="523" alt="image" src="https://github.com/user-attachments/assets/ac646d5c-f04b-4992-af11-350e593c89e4" />

<img width="462" height="505" alt="image" src="https://github.com/user-attachments/assets/523d1a3e-b353-48a6-a0d6-a805eeab2cc4" />

<img width="406" height="517" alt="image" src="https://github.com/user-attachments/assets/890a3e36-1854-4269-aaf5-76ea8516932f" />

<img width="437" height="516" alt="image" src="https://github.com/user-attachments/assets/fe84d70c-d65d-42da-8a4c-730d5a18ce60" />

<img width="431" height="523" alt="image" src="https://github.com/user-attachments/assets/b4f5d194-3e03-47f5-9ffc-fe21d5808b53" />

<img width="463" height="512" alt="image" src="https://github.com/user-attachments/assets/21d8000b-96f0-4196-a547-393829c0e8d4" />

<img width="393" height="507" alt="image" src="https://github.com/user-attachments/assets/dde23b82-a78e-4929-86ca-1beac8484b05" />

<img width="377" height="510" alt="image" src="https://github.com/user-attachments/assets/79c748a1-bd9a-4cfb-bb76-0d9a729197cc" />

<img width="406" height="513" alt="image" src="https://github.com/user-attachments/assets/95178ccf-c119-4fbc-a245-525e4ae498cc" />

<img width="672" height="511" alt="image" src="https://github.com/user-attachments/assets/e4fc0e6e-0c6b-4f07-bcd2-bbe0954f8d1d" />

<img width="565" height="523" alt="image" src="https://github.com/user-attachments/assets/8233c54b-424e-4d91-aa2e-f9bd28f707db" />

<img width="437" height="508" alt="image" src="https://github.com/user-attachments/assets/05f3d404-175e-4abf-a9a4-5e05867b63f2" />

<img width="422" height="502" alt="image" src="https://github.com/user-attachments/assets/b9f77f42-b3d3-4f80-8dc3-b3c5045df5e2" />



