# Text Detection
Text Detection from Image

## Steps:
1. Applying image processing for the image:
The colorspace of the image is first changed and stored in a variable. For color conversion we use the function cv2.cvtColor(input_image, flag). The second parameter flag determines the type of conversion. We can chose among cv2.COLOR_BGR2GRAY and cv2.COLOR_BGR2HSV. cv2.COLOR_BGR2GRAY helps us to convert an RGB image to gray scale image and cv2.COLOR_BGR2HSV is used to convert an RGB image to HSV (Hue, Saturation, Value) color-space image. Here, we use cv2.COLOR_BGR2GRAY. A threshold is applied to the converted image using cv2.threshold function. 
cv2.threshold() has 4 parameters, first parameter being the color-space changed image, followed by the minimum threshold value, the maximum threshold value and the type of thresholding that needs to be applied.

2. To get a rectangular structure:
cv2.getStructuringElement() is used to define a structural element like elliptical, circular, rectangular etc. Here, we use the rectangular structural element (cv2.MORPH_RECT). cv2.getStructuringElement takes an extra size of the kernel parameter. A bigger kernel would make group larger blocks of texts together. After choosing the correct kernel, dilation is applied to the image with cv2.dilate function. Dilation makes the groups of text to be detected more accurately since it dilates (expands) a text block.

3. Finding Contours:
cv2.findContours() is used to find contours in the dilated image. There are three arguments in cv.findContours(): the source image, the contour retrieval mode and the contour approximation method. 
This function returns contours and hierarchy. Contours is a python list of all the contours in the image. Each contour is a Numpy array of (x, y) coordinates of boundary points in the object. Contours are typically used to find a white object from a black background. All the above image processing techniques are applied so that the Contours can detect the boundary edges of the blocks of text of the image. A text file is opened in write mode and flushed. This text file is opened to save the text from the output of the OCR.

4. Applying OCR:
Loop through each contour and take the x and y coordinates and the width and height using the function cv2.boundingRect(). Then draw a rectangle in the image using the function cv2.rectangle() with the help of obtained x and y coordinates and the width and height. There are 5 parameters in the cv2.rectangle(), the first parameter specifies the input image, followed by the x and y coordinates (starting coordinates of the rectangle), the ending coordinates of the rectangle which is (x+w, y+h), the boundary color for the rectangle in RGB value and the size of the boundary. Now crop the rectangular region and then pass it to the tesseract to extract the text from the image. Then we open the created text file in append mode to append the obtained text and close the file.

## Sample Image
![image](https://user-images.githubusercontent.com/72964595/202905072-ec4a0ff5-acf3-4631-91c2-f9701aaf0050.png)
(contains heavy text and blurry) 

## Contoured Image
![image](https://user-images.githubusercontent.com/72964595/202905173-bdbf727f-23aa-4794-8701-aefceec6bb9a.png)


## Dilated Image
![image](https://user-images.githubusercontent.com/72964595/202905194-99dad177-741d-4e52-8221-c90182077540.png)


## Threshold Image
![image](https://user-images.githubusercontent.com/72964595/202905124-e27b5b98-413c-4bde-a105-db0e4894aa02.png)


## Output Image
![image](https://user-images.githubusercontent.com/72964595/202905018-3a1dcc31-41e9-4ba7-9ac7-8b08cb23dec7.png)
