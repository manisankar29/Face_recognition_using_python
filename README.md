# Face Recognition Using Python

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Code Explanation](#code-explanation)
- [Example Output](#example-output)
- [Note](#note)
- [License](#license)

## Introduction

This python script uses the `face_recognition` library to perform face recognition on an image. It can recognize faces of known individuals and label them in an unknown image. In this README, we'll provide instructions on how to use the code and set up the environment.

## Prerequisites

Before using this code, ensure that you have the necessary libraries installed. You can install them using `pip`:

```bash
!pip install face_recognition
```
Make sure you also have `numpy`, `Pillow`(PIL) and `IPython` installed in your Python environment.

## Getting Started

1. Clone this repository or create a new Python script.
2. Add the images you want to use for recognition. The known faces should be stored in seperate image files, and the unknown image should be specified as "unknown.jpg" in the code.
3. Replace the names and known face encodings in the code with the names and encodings of the individuals you want to recognize.
4. Run the Python script. The code will perform face recognition on the unknown image and display the results.

## Code Explanation

The code is divided into the following sections:

### Library Imports

Importing the required Python libraries, including `face_recognition`, `numpy`, `Pillow`, and `IPython.display`.

```python
import face_recognition
import numpy as np
from PIL import Image, ImageDraw
from IPython.display import display
```

### Loading Known Faces

Loading known faces and their encodings from image files. You can add more known faces by extending the `known_face_encodings` and `known_face_names` lists.

```python
face_1 = face_recognition.load_image_file("bill.jpg")
face_1_encoding = face_recognition.face_encodings(face_1)[0]

face_2 = face_recognition.load_image_file("elon.jpg")
face_2_encoding = face_recognition.face_encodings(face_2)[0]

face_3 = face_recognition.load_image_file("sundar.jpg")
face_3_encoding = face_recognition.face_encodings(face_3)[0]

known_face_encodings = [
    face_1_encoding,
    face_2_encoding,
    face_3_encodings
]
known_face_names = [
    "Bill Gates",
    "Elon Musk",
    "Sundar Pichai"
]
```

### Loading the Unknown Image

Loading the image in which you want to recognize faces. Ensure this image is named "unknown.jpg".

```python
unknown_image = face_recognition.load_image_file("unknown.jpg")
```

### Face Recognition

Detecting faces in the unknown image, comparing their encodings with the known faces, and assigning names to recognized faces.

```python
face_locations = face_recognition.face_locations(unknown_image)
face_encodings = face_recognition.face_encodings(unknown_image, face_locations)

pil_image = Image.fromarray(unknown_image)
draw = ImageDraw.Draw(pil_image)

for (top, right, bottom, left), face_encoding in zip(face_locations, face_encodings):
    matches = face_recognition.compare_faces(known_face_encodings, face_encoding)

    name = "Unknown"

    face_distances = face_recognition.face_distance(known_face_encodings, face_encoding)
    best_match_index = np.argmin(face_distances)
    if matches[best_match_index]:
        name = known_face_names[best_match_index]

    draw.rectangle(((left, top), (right, bottom)), outline=(0, 255, 255))
    print(name)

    text_width, text_height = draw.textsize(name)
    draw.text((left + 6, bottom - text_height + 25), name, fill=(255, 255, 255, 255))
```

### Displaying the Image

Drawing rectangles around recognized faces and displaying the image with labels.

```python
del draw

display(pil_image)
```

## Example Output

![Screenshot 2023-10-22 025259](https://github.com/manisankar29/Face_recognition/assets/138246745/46c2699a-9cb1-40ea-9749-fbf9116a27ee)

## Note

- The accuracy of face recognition depends on the quality and diversity of known face images. It may not be perfect in all cases.
- Ensure that the image file paths and names are correctly specified in the code.

Feel free to modify the code to suit your needs and add more individuals to the known faces list for recognition.

Enjoy using the face recognition script!

If you encounter any issues or have questions, feel free to reach out for assistance.

```vbnet

You can include this README.md file in your project's repository, and it will serve as a guide for users who want to use the provided face recognition code.
```

## License

[MIT License](LICENSE)
