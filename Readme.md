
# Slitscan

![](https://github.com/janiswalser/Slitscan/blob/master/assets/slitscan_gif.gif)

The weird and beautiful effect of Slitcan. 
(Unfortunately, the performance isn't good enough — but try it by yourselve)

# Usage
Run the Python script and enjoy your weird motions. 
The second window will display your Slit Scan effect after a few seconds.

# Content

**1.)** Import

```
import cv2
import numpy as np
```

**2.)** Setup

```
#capture
cap = cv2.VideoCapture(0)

h = 480
w = 640
cap.set(3,w)
cap.set(4,h)


cv2.namedWindow('background')
cv2.namedWindow('frame')
background = np.zeros((h, w, 3), np.uint8)

allFrames = []
counter = 0

```

**3.)** Add Magic

```
while(1):
    # read the frames
    success,frame = cap.read()
    if success:
        frame = cv2.flip(frame, flipCode=1)

        current_Frame =  frame[:]
        
        #add current_Frame
        allFrames.append(current_Frame)



        #first capture image
        if len(allFrames) > (h):
            for i in range(10,h):
                background[i] = allFrames[(counter-i)][i]

        counter+=1

        #show images
        cv2.imshow('background',background)
        cv2.imshow('frame',frame)

    #exit
    if cv2.waitKey(33)== 27:
        break



# Clean up everything before leaving
cv2.destroyAllWindows()
cap.release()

