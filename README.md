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

We need 4 offset values for the program to run (offset, velocityOffset, distanceThreshold, cameraCoef). These values are written in the first line of the labels file. They are present in the example videos, however you need to add them manually if you're running the program with your own videos. After running the detection algorithm on Google Colab, add them to the labels file that you downloaded. These values depend on several variables such as: resolution of the video, FPS of the video, distance of the road, height of the camera. First two offset values are used to check if a vehicle is close enough to the detection lines so they get counted correctly. A vehicle might move way too many pixels between two frames if the fps is low, making the program to miss the vehicle. These offset values are used to combat this. The third value is used to re-identify the same vehicles over two frames using the tracker so that they get assigned the same vehicle ID's. This is important not to count the same vehicles multiple times.


# Best Configuration

We used pre-trained language model BERT for our pipeline. We compared three different pipeline configurations: a light configuration, a configuration using ConveRT, and a heavy configuration that included BERT. In each case we’re training a DIETClassifier for combined intent classification and entity recognition for 200 epochs, but in the light configuration we have CountVectorsFeaturizer, which creates bag-of-word representations for each incoming message at word and character levels. In the end, we chose config-light as the configuration of the chatbot.

# Results of the Configurations

<p align="center"> 
      <img width="600" alt="Ekran Resmi 2021-06-20 15 21 16" src="https://user-images.githubusercontent.com/52889449/122673919-7c657900-d1db-11eb-933f-430a6520ec19.png">
</p>

<p align="center"> 
      <img width="600" alt="Ekran Resmi 2021-06-20 15 21 27" src="https://user-images.githubusercontent.com/52889449/122673920-7d96a600-d1db-11eb-9851-fcf36fc4f137.png">
</p>

In the images below, there are confusion matrices created by each configuration for intent classification and entity extraction in turn.

### config-light:

<p align="center">
      <img width="400" alt="Ekran Resmi 2021-06-20 15 26 15" src="https://user-images.githubusercontent.com/52889449/122674048-247b4200-d1dc-11eb-8cb3-dceebc77d571.png">
      <img width="400" alt="Ekran Resmi 2021-06-20 15 26 36" src="https://user-images.githubusercontent.com/52889449/122674049-25ac6f00-d1dc-11eb-8e26-9be55d352701.png">
      <img width="400" alt="Ekran Resmi 2021-06-20 15 27 25" src="https://user-images.githubusercontent.com/52889449/122674040-1d543400-d1dc-11eb-9f0d-d1936ddce096.png">
      <img width="400" alt="Ekran Resmi 2021-06-20 15 27 46" src="https://user-images.githubusercontent.com/52889449/122674055-29d88c80-d1dc-11eb-837a-37982315c32b.png">
</p>


### config-convert:

<p align="center">  
      <img width="400" alt="Ekran Resmi 2021-06-20 15 30 19" src="https://user-images.githubusercontent.com/52889449/122674162-8b98f680-d1dc-11eb-8639-140cfff0a7fc.png">
      <img width="400" alt="Ekran Resmi 2021-06-20 15 30 30" src="https://user-images.githubusercontent.com/52889449/122674166-8d62ba00-d1dc-11eb-9989-7b5067375f23.png">
      <img width="400" alt="Ekran Resmi 2021-06-20 15 30 42" src="https://user-images.githubusercontent.com/52889449/122674170-8e93e700-d1dc-11eb-8990-297eecbf0ab7.png">
      <img width="400" alt="Ekran Resmi 2021-06-20 15 30 54" src="https://user-images.githubusercontent.com/52889449/122674174-8f2c7d80-d1dc-11eb-94d1-d875971e7942.png">
</p>

### config-heavy:

<p align="center">    
      <img width="400" alt="Ekran Resmi 2021-06-20 15 32 01" src="https://user-images.githubusercontent.com/52889449/122674208-c0a54900-d1dc-11eb-8534-69aa843b5f2e.png">  
      <img width="400" alt="Ekran Resmi 2021-06-20 15 32 12" src="https://user-images.githubusercontent.com/52889449/122674209-c307a300-d1dc-11eb-9dce-836d022e241d.png">    
      <img width="400" alt="Ekran Resmi 2021-06-20 15 32 22" src="https://user-images.githubusercontent.com/52889449/122674210-c4d16680-d1dc-11eb-9503-ad7f33a51bef.png">   
      <img width="400" alt="Ekran Resmi 2021-06-20 15 32 32" src="https://user-images.githubusercontent.com/52889449/122674213-c69b2a00-d1dc-11eb-8821-75aa89e2ee33.png">
</p>
