# Smart-Attendance-System-Using-Face-Recognition

Smart Attendance System using Face Recognition(SASUFR) web application demonstrating the use of facial recognition for marking attendance built as a part of my  master's degree thesis. It is a web application that can be used by the company to manage attendance of its employees. Face Recognition is a biometric method of identifying an individual by comparing live capture or digital image data with the stored record for that person.
Smart Attendance System is marking of attendance based on this technology, which provides an automated attendance system that is practical, reliable and eliminate disturbance and time loss of traditional attendance systems.

### Provided Functionalities 
- Admin and Employee Login
- Admin : Register new employees.
- Admin : Add employee photos to the training dataset.
- Admin: Train the model.
- Admin: View attendance reports of all employees. Attendance can be filtered by date or employee. 
- Employee - View attendance reports of self.
- Employee - Mark Attendance

### Methodology
The face recognition system analyses video feed frame by frame for detection of faces. Then a
predictor is used to identify the facial landmarks in the faces detected using a predefined template.
Using this template, the faces are aligned to increase the accuracy of the model. Now the unique
embeddings of these aligned faces are generated. These embeddings are biometrics of the face and
hence unique. These embeddings are classified using the classifier. This classifier is trained on the
images collected from the users beforehand to ensure the smooth workflow of the program.

# Built Using
## OpenCV
### Image Processing with OpenCV:
OpenCV can be installed by building from source which can be downloaded from OpenCV’s website.
Once it is downloaded, it can be imported using the command: import cv2
In order to load an image in OpenCV, the imread() method is used, in which the path of the image file
is provided as a parameter. An image, once loaded, can be displayed using the imshow() method.
Images are loaded as numpy arrays, and hence their dimensions can be retrieved using the shape
attribute of numpy arrays. This provides another advantage - cropping images and extracting regions
of interest is reduced to array slicing. Images can be resized using the resize() method. Rectangles,
circles and text can be drawn onto an image using the rectangle(), putText() and circle() methods.
OpenCV loads images in BGR format which is not always desirable. Colorspace conversions to
Grayscale and RGB formats is achieved easily using the cvtColor() method. All of these methods are
used throughout the project for image manipulation.
### Working with Video Streams
OpenCV provides VideoCapture and VideoWriter classes to capture videos and save them on disk,
respectively. In this project, VideoCapture objects have been used to work with webcam streams. The
VideoCapture() constructor takes one argument, which can either be a number, specifying the index of
the camera device, or the path to a video file. Once a VideoCapture object is created, it can be
processed frame by frame, allowing us to apply the same image processing techniques that we use for
static images. The video capture can be released with the release() method.


## Dlib
Dlib is a general-purpose cross-platform software library written in C++. Its libraries are available for
use in different programming languages. The Object detection task can be achieved using Dlib’s
detectors such as Histogram of Oriented Gradients (HOG), or Convolutional Neural Network (CNN)
based face detector.

## Face Recognition
A facial recognition system typically works by extracting face encodings from faces and
comparing them with an existing database of known faces to find a match. Given an unknown image,
the process of facial recognition comprises of detecting faces in that image, aligning them, extracting
feature vectors from aligned faces and classifying each feature vector as belonging to one class from a
set of classes.

## Django
Django Template Language is used to send data from the view to the templates. It provides the
developer with tags that function similarly to some programming constructs - such as the ‘if’ tag for
boolean tests and the ‘for’ tag for looping. The templating language has been used throughout the
project for interaction between the view and the templates.

## Face Detection
- Dlib's HOG facial detector.
### Histogram of Oriented Gradients (HOG) detector
HOG is a feature descriptor used in computer vision and image processing for the purpose of object
detection. It works on the concept of finding gradients along the x and y-axis. These gradients are
added vectorially and information such as magnitude and direction of the gradients are extracted
forming edges in the image. Now the whole gradient image is divided into 8*8- dimension matrix i.e.
carrying 64 gradient vectors. Each matrix contains 9 bins and each bin has a range of 40 degrees to
allocate the gradient vector lying in that range. After each gradient vector has been allocated a bin, a
histogram of this matrix is formed which determines the overall direction and magnitude of the
gradient. Luminosity plays a great role in the proper detection of gradients. To overcome this failure
the value of the histogram is obtained in the red, green and blue frame and then normalized making it
lighting invariant. Finally, the normalized histogram is compared with its default histogram for faces to
identify a face in an image.
The following code is used to initialize the HOG based face detector:
```
hog_face_detector = dlib.get_frontal_face_detector()
```
### Facial Landmark Detection
- Dlib's 68 point shape predictor
### acial Alignment using Landmark Predictors
Dlib has a 5 point and 68 points facial landmark predictor. It extracts important landmarks on the face
like left eye start point, the center of the nose, etc. The facial landmark points help us to perform
operations using the point coordinates. The operations performed for facial alignment are: -
1) Rotation, such that the eyes lie on a horizontal line
2) Scaling, such that the size of faces is approximately identical
3) Translation, such that the image is centred
In this project, 68 points facial landmark predictor is used. The results can be seen in the following
figure :- 

![align](https://user-images.githubusercontent.com/76810003/167385801-047c1288-880f-40cf-8159-b58546cd4b61.png)

# Training and Testing
Once the CNN is built, it is trained on a number of classes, each having several training images. Once
trained with images and associated labels, the CNN is expected to predict the associated label for an
unknown image input.The training time of the CNN depends on the number of training images, the
size of the batch, the number of times epochs, etc. In order to obtain high accuracy, it is necessary to
train the CNN on a large dataset, which is computationally expensive and takes a lot of time. When
trained and tested on a small dataset, the team was unable to get accurate results. Hence, for this
project, the team decided to use pre- trained CNNs to extract encodings from images.

