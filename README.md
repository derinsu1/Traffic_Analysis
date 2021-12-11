# Traffic_Analysis

<p align="center"> 
      <img width="1000" alt="Traffic_Analysis" src="https://user-images.githubusercontent.com/54302889/145484767-a82e3e69-6bc9-4852-909d-d57eabe581ac.png">
</p>

This project is used to analyse traffic congestion. It counts the number of vehicles on preferred lanes in a camera recording. Additionally, it estimates the velocities of the vehicles. This data can be used for many purposes. If used on a live recording, it can be used to optimize traffic lights in real-time.

# How to Run the Project?

1. Clone the project using git lfs, run this command: git lfs clone derinsu1/Traffic_Analysis
2. To use your own video recordings, run the VehicleDetection.ipynb file on Google Colab. (Skip this step if you wish to use the pre-uploaded videos)
3. Run the Traffic_Analysis.py file
4. Draw detection lines on preferred lanes
5. Hit the enter or space key to start analysis

# Interface

The Interface has a few operations. Once the program is run, the first frame of the uploaded video is shown on screen. To draw a detection line, left-click on one end of a lane and left-click again on the other end. You can right click on any line to delete it. If you wish, you can draw a line that covers multiple lanes. After you're done with drawing detection lines, hit the enter, space or escape key to start the analysis.

# Choosing the Video

The default video for the program is a recording from a highway in Netherlands. You can change this to recordings from Switzerland or Thailand which are present in the data folder (swissVideo.mp4, thaiVideo.mp4). The screenshot at the top of the readme file is taken from the Swiss video. Simply change the path of the input video and labels at lines 97 and 98.

In order to use a different camera recording, you need to run VehicleDetection.ipynb file on Google Colab to detect vehicles, save the output video with boxes around the vehicles and save the coordinates of the labels in each frame. All instructions to run the detection algorithm are present in the Colab file. After downloading the output video and the labels file, you need to add offset values to the first line of the labels file. This is explained further in the next part.


# Offset Coefficients

We need 4 offset values for the program to run (offset, velocityOffset, distanceThreshold, cameraCoef). These values are written in the first line of the labels file, seperated by spaces. They are present in the example videos, however you need to add them manually if you're running the program with your own videos. After running the detection algorithm on Google Colab, add them to the labels file that you downloaded. These values depend on several variables such as: resolution of the video, FPS of the video, distance of the road, height of the camera. 

First two offset values are used to check if a vehicle is close enough to the detection lines so they get counted correctly. A vehicle might move way too many pixels between two frames if the fps is low, making the program miss the vehicle. These offset values are used to combat this. The third value is used to re-identify the same vehicles over two frames using the tracker so that they get assigned the same vehicle ID's. This is important not to count the same vehicles multiple times. The fourth and final value is used to estimate velocities. You might need to try different configurations for the program to run accurately.

A recommended example for the coefficients are: 20 100 50 0.06

# Vehicle Tracker 

Each vehicle is given a unique ID, and in the next frame, the program checks if the same vehicles are still in the frame. The distance between the vehicles are calculated over two consecutive frames, and we can conclude that it’s the same vehicle from the previous frame if the distance is lower than a certain threshold. This improved the detection accuracy as well, because it became easier to check if a vehicle had already passed the detection line or not. By default the program is set not to show the unique ID's for the vehicles. However you can un-comment the lines 173 and 174 to show the ID's.

# Speed Estimation

The first step in detecting velocity is to measure how many pixels a vehicle moved between two frames. This gives us pixels per frame, and if we multiply this with frames per second, we end up with pixels per second. Multiplying this number with the actual distance, the distance that represents a few pixels, we get the velocity of the vehicle in terms of meters per second. And, of course, we multiply this with 3.6 to get kilometers per hour.

In order to correctly measure the velocity of a vehicle, using a stationary camera recording, we need to know the actual distance between the camera and the road. And this distance changes for every other part of the road. We do not have this distance information for our test videos because they were downloaded from the internet. The simplest way to solve this problem was to guess the distance. Therefore, the speed estimation is far from perfect. However, at least the relative speeds between the vehicles are correct. Another solution would be to ask the user, just like we did with the detection lines. We can ask the user to draw a line on the road, perpendicular to the detection lines, and the user can enter the actual length of the drawn line. However, this would mean that the user would guess the distance so it wouldn’t improve the program much. The best solution would be of course to have our own cameras on highways and record our own videos. This way, we could actually measure the distance and consequently, the velocity.

# Sample Results

Here you can see the trimmed versions of the sample videos in the data folder.

<br>

Dutch Highway

https://user-images.githubusercontent.com/54302889/145693761-2ebcf731-a7f3-420b-ac09-556ed04afda1.mp4

<br>

Swiss Highway

https://user-images.githubusercontent.com/54302889/145693967-f59d4746-029b-49ad-893f-f03941202459.mov

<br>

Thai Highway

https://user-images.githubusercontent.com/54302889/145694060-d86d0c48-3a46-4c9f-8822-c69d970e6307.mov
