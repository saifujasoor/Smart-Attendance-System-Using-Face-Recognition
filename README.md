# Smart Attendance System Using Face Recognition
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

## Tabular Representation of Attendance Data
The application provides the admin with the feature to view attendance reports, where in attendance
data is displayed as tables. This is achieved via Django’s ORM and Templating Language.
Data is fetched from the attendance database in the form of query sets, making use of Django’s ORM.
These query sets are then passed to the template (HTML) files using Django’s templating language.
These query sets can be displayed as a table by using the {% for tag %} of the templating language for
displaying rows and outputting each attribute of the object in a different table cell (column).
![image](https://user-images.githubusercontent.com/76810003/167387522-0773acd4-58f4-4bd3-bc37-b5904a1e3e0b.png)
- A Seaborn bar plot demonstrating the number of hours worked by each employee on a particular
date is displayed in the following figure.
![image](https://user-images.githubusercontent.com/76810003/167387617-e403ef1a-dd3d-4f12-8b0c-804f5bc27284.png)

- A Seaborn line plot demonstrating the number of hours worked by a particular employee for a range
of dates is displayed in the following figure. Note that it allows easy visualization of the weekly
minimum.
![image](https://user-images.githubusercontent.com/76810003/167387712-81b42f7c-03ca-4cf0-bf1c-9ef554842195.png)

## Future Enhancements
1. A feature which can give intruder alert can be included in the system. Furthermore, the images of
unknown people can be saved in an efficient manner and displayed in the system for better security.
2. The number of training images can be reduced so that less storage is required. This can be done by
removing duplicate images of the same person, or images with similar embeddings.
3. The training time can be reduced by retraining the classifier only for the newly added images.
4. A feature can be added where an employee is automatically sent a warning if his attendance or
working hours are below the threshold.
5. Wrongly classified images can be added to the training dataset with the correct label so as to
increase the accuracy of the recognition model.

# Project Demo

## Emplyee Home page

![home](https://user-images.githubusercontent.com/76810003/169558514-e393a6f6-fdf4-48ea-86c0-c15a2648dad0.png)


## Emplyee Dashboard

![user_dashboard](https://user-images.githubusercontent.com/76810003/169558550-7882aa04-44ef-4f02-b5d7-345b21e74411.png)


## Admin Dashboard

![admin_dashboard](https://user-images.githubusercontent.com/76810003/169558603-0e3889d7-b5c9-41b1-8e22-037e01d779c6.png)


## Attendance Report

![report](https://user-images.githubusercontent.com/76810003/169558678-d1525f8a-8b39-4f39-bab3-db64db187874.png)
![report bydate](https://user-images.githubusercontent.com/76810003/169558694-fd3294fd-103d-4d24-929c-a30e1cc52391.png)
![by-date](https://user-images.githubusercontent.com/76810003/169558764-83281901-abbb-495a-9000-1cccdb1e7eb5.png)


## Data Traning 

![training process](https://user-images.githubusercontent.com/76810003/169558818-47fe532f-daf1-44bf-b879-a0c6c3f03591.png)


## Django Administration Dashboard

![backend-dashboard](https://user-images.githubusercontent.com/76810003/169559016-ecfdf82b-92e8-42dd-9044-70e58ad2a9ff.png)

# Sources

```
blog.dlib.net/2017/02/high-quality-face-recognition-with-deep.html
krasserm.github.io/2018/02/07/deep-face-recognition/
medium.com/@krsatyam1996/face-recognition-using-openface-92f02045ca2a
www.learnopencv.com/histogram-of-oriented-gradients
towardsdatascience.com/https-medium-com-pupalerushikesh-svm-f4b42800e989
www.pyimagesearch.com/2017/05/22/face-alignment-with-opencv-and-python
us.norton.com/internetsecurity-iot-how-facial-recognition-software-works.html
ujjwalkarn.me/2016/08/11/intuitive-explanation-convnets
```


## Author

<table>
<tr>
<td>

     <img src="https://user-images.githubusercontent.com/76810003/169560636-a8c87af2-09a6-4a72-8dc3-73ce38449c9f.jpg" width="180"/>
     
     Saifullah Rahimi

<p align="center">
<a href = "https://github.com/saifujasoor"><img src = "http://www.iconninja.com/files/241/825/211/round-collaboration-social-github-code-circle-network-icon.svg" width="36" height = "36"/></a>
<a href = "https://www.linkedin.com/in/saifullahrahimi/"><img src = "http://www.iconninja.com/files/863/607/751/network-linkedin-social-connection-circular-circle-media-icon.svg" width="36" height="36"/></a>
</p>
</td>
</tr> 
  </table>




