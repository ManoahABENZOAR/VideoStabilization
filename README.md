# VideoStabilization

  Motion Estimation

Firsty, I load the video and prepare the backup for our stabilized video : 
  it will allow us to use this video again to compare the 2 graph : 
    -the first for the initial video  
    -the second graph issued from the stabilized video

To do so I need to import « os » and « cv2 » : 
  Here I use VideoCapture to collect the video from my pc. 
  After I wrote a try loop, here I don’t enter in because I have the video, but in case where the program doesn’t find it Ienter in this loop and show off an error.

Then, I prepare the type of the output video in the variable « fourcc » and I load it in the function « VideoWriter » where I set the name

Now we have our video!!! 
But we can’t find out the key points directly from a video. 
We must use the video frame to find its : we use the video’s image ( and now we can use something we saw previously in this course). 
So we will transform our video into a serie of frame : 
![image](https://user-images.githubusercontent.com/79518374/201168369-10b7f59c-f04f-4c23-9d22-921bf3738151.png)

To do so I must collect some information as : number of frame for the video, the size of the video, (here the fps are only usefull to define the previous output video). 
Then we can start our work on the frame.
![image](https://user-images.githubusercontent.com/79518374/201168497-ba509115-2ecb-4bdd-b5e4-9566269468a2.png)

As usual, I convert frames into gray scale.


We are ready to start!!!
Let’s compute the translation to stabilized our video :
![image](https://user-images.githubusercontent.com/79518374/201168656-2d0692cd-4789-4950-a237-5b478b03febc.png)

We search key points with the function goodfeatureToTrack.
Then I use the idea of optical flow to track these good points in the next frame : work on the difference between to consecutive frame. 
And that for all the video’s frame, that’s the reason for our « for » loop. (We use the function presents in OpenCV library).
Error can occurs so it adviced to use a filter to fight against that. Here I use a found filter but I could have improve it.
Thanks to these points I will compute the transform, which will allow me to obtain the motion translation informations. 
We do this in several steps : first we compute the affine to obtain translation, after we find out the rotation. We could have use only translation but it will be less safe.
You could ask why I have to array mismatch and nbr : I use it to compute the difference between to point in consecutive picture, I store this difference in mismatch and I increament nbr with the final aim to show these information on a graph ; 
with it I will compare the translation between input and output video. ( I’m not sure for the method as I saw lot of other method, but they doesn’t show a graph, only scheme of the motion of some point on two consecutive image).
The following picture shows the graph of the input video

![image](https://user-images.githubusercontent.com/79518374/201169372-0093c2dc-9262-48a2-8099-d042303ce4b0.png)

After computing the motion between frames I will search a global trajectorie of motion to stabilize our video.
To do so I will use 3 function I fund on internet to do it by the good way 

![image](https://user-images.githubusercontent.com/79518374/201169455-5303de90-d1e8-4b27-a02e-26f614f57373.png)

Thanks to these function I think we also can compute the translation to show it on a graph but I don’t know if we how to do it and return a 2D graph : as we have x,y, but also the curve and the angle ; 
I think we can’t place all of these axes in one graph and still obtain a 2D graph !

![image](https://user-images.githubusercontent.com/79518374/201169596-d881312c-6be2-4399-82a4-2706587894ee.png)

According to the tuto of these  functions we could find graph like that I think it looks like what I found. So my method wasn’t wrong.


Use all these function have one aim : allow us to apply camera motion to frame to create the stabilization. 

![image](https://user-images.githubusercontent.com/79518374/201169702-9a6db62f-f8ad-477c-924f-42565fb3a064.png)

At the end, I obtain this after running the code : 
![image](https://user-images.githubusercontent.com/79518374/201170139-fdf77ee3-7da6-4cc9-9a88-4d4e6de0e059.png)
