# Video Processing

## Introduction

A video is a sequence of images called frames.\
For each video we have a frame rate which can be identified using FPS
i.e. Frames per Second.

Ex : 30 fps means we can capture 30 images/frames per second.\
As the frame rate increases the quality of the video also increases.

Total Frames = FPS x Duration

------------------------------------------------------------------------

## Video Resolution

More the video resolution more the clarity of the image and size.

Resolution = width x height

Some of the resolutions:

-   640 x 480 (480 P) =\> SD quality video\
-   1280 x 720 (720 P) =\> HD quality video\
-   1920 x 1080 (1080 P) =\> FHD\
-   2560 x 1440 (1440 P) =\> 2K QUAD HD\
-   3840 x 2160 (2160 P) =\> 4K



------------------------------------------------------------------------

## Some the use cases that we can solve using the CC camera Data

### 1.

CCTV cameras can monitor public areas like roads or campuses to identify
sudden incidents such as accidents. When unusual activity is
observed---such as a collision, a person falling, or sudden crowd
disturbance---the system can immediately trigger an alert. It can
automatically share the location and relevant video clip with emergency
services such as police or hospitals, ensuring a faster response and
potentially saving lives.

### 2.

In educational institutions, CCTV footage can help ensure student safety
and protect property. The system can observe unusual physical
interactions, such as fighting, aggressive behavior, or vandalism. If
such behavior is detected, administrators can be alerted in real time.
This allows quick intervention to prevent harm, maintain discipline, and
protect college property from damage.

### 3.

If we are given a specific object image, such as a photo of a bag or
laptop, CCTV footage can be used to identify the last time that exact
object was seen in the recorded video. The system compares the given
image with the objects appearing in different time frames of the footage
and searches through the timeline. Once it finds matches, it determines
the most recent moment when the object was visible. This allows security
personnel to quickly know the exact last known time and location of the
object without manually reviewing hours of video.

------------------------------------------------------------------------

# Experiment - 1

-   Here we are extracting 20 Frames from each video.\
-   The shape of the video frame is (20,224,224,3) where 20 represents
    the frames and 224,224,3 represents the image / frame shape.\
-   Here we have used the MobileNetV2 model inorder to classify the
    video. But the MobileNetV2 is trained on ImageNet which are images.
    So it wont work well for classifying the video. For video
    classification we can go with CNN+RNN hybrid model or we can also go
    with 3D CNN.\
-   Here we are giving 20 frames as input to the model and for each
    frame it produces the output Probability distribution for 1000
    classes. So the output shape will be (20,1000).\
-   When we do np.mean() along the axis 0 we are find the average of
    probability of each class and we end up with the output shape of
    (1000,).\
-   We take the sum of all the 1000 values we will get the value
    0.99999994 (1 approx).\
-   We can plot the image / frames at a particular time frame t. Here we
    have 20 frames.

    ### Frame at Time Stamp t

    ![Frames](frames.png)

------------------------------------------------------------------------

# Experiment - 2

## OpenCV Attributes and Methods

### cv2.VideoCapture('video_file.mp4')

Returns: A VideoCapture object\
It creates a connection to the video file. This object allows us to
access and read frames from the video. It does not return frame data
directly, but prepares the system to retrieve video information.

### cap.get(cv2.CAP_PROP_FRAME_COUNT)

Returns: A number (float)\
It returns the total number of frames present in the video. This value
represents how many individual images make up the entire video.

### cap.get(cv2.CAP_PROP_FRAME_HEIGHT)

Returns: A number (float)\
It returns the height of each frame in pixels. The value tells how many
pixels exist vertically in every frame.

### cap.get(cv2.CAP_PROP_FRAME_WIDTH)

Returns: A number (float)\
It returns the width of each frame in pixels. The value tells how many
pixels exist horizontally in every frame.

### cap.get(cv2.CAP_PROP_FPS)

Returns: A number (float)\
It returns the number of frames displayed per second. This value
indicates how smooth the video appears during playback.

### cap.read()

Returns: Two values (ret, img)\
The first value (ret) is either True or False. It indicates whether a
frame was successfully read. The second value (img) is the actual image
frame stored as a numerical array containing pixel information.

### img.shape

Returns: A tuple of three numbers\
It returns the dimensions of the image in the format (height, width,
number of color channels). The first value is vertical pixels, the
second is horizontal pixels, and the third usually represents color
information (for example, 3 for color images).

### cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

Returns: A modified image array\
It returns a new image with rearranged color values. The pixel data
remains the same in size, but the color order is corrected for proper
display.

### cap.release()

Returns: No return value\
It closes the video file connection and frees system resources. It does
not produce any visible output.
