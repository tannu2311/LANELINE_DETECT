# **Lane Lines Detection Using Python and OpenCV** 
### In this project, I used Python and OpenCV to detect lane lines on the road. I developed a processing pipeline that works on a series of individual images, and applied the result to a video stream.

<p align="center">
  <img src="OutputExample.gif">
</p>

# Image Processing Outline:

## Color Selection (HSL):

- Apply HSL color selection to isolate lane lines.
- Variations in lighting, such as shadows, glare, or changes in ambient light, can cause lane markings to appear differently in terms of brightness while maintaining their color.
- HSL's ability to separate color from brightness allows the algorithm to remain robust against these lighting variations.
- It ensures that lane lines can be detected reliably across different lighting conditions, enhancing the overall robustness and performance of the lane detection system.
- Using HSL produces the clearest lane lines of all color spaces.
- **Function:** `HSL_color_selection(image)`

## Grayscale Conversion:

- The Canny edge detection algorithm measures the intensity gradients of each pixel. So, we need to convert the images into gray scale in order to detect edges.
- Converting the color-selected image to grayscale simplifies further processing by reducing computational complexity.
- **Function:** `gray_scale(color_select)`

## Gaussian Smoothing:

- Apply Gaussian smoothing to reduce noise and blur the image.
- Gaussian smoothing emphasizes central pixels while suppressing noise.
- **Function:** `gaussian_smoothing(gray)`

## Edge Detection (Canny):

- Detect edges in the smoothed grayscale image using the Canny edge detector.
- **Function:** `canny_detector(smooth)`

## Region of Interest Selection:

- Define a region of interest to focus on relevant parts of the image (e.g., the road).
- Focusing on relevant parts of the image reduces computational load and increases the accuracy of lane line detection.
- The region of interest is typically a trapezoidal shape representing the area where lane lines are expected to appear in the image.
- **Function:** `region_selection(edges)`

## Hough Transform:

- Apply Hough transform to detect lines in the region of interest.
- `hough_lines` contains the list of lines detected in the selected region.
- **Function:** `hough_transform(region)`

## Averaging and extrapolating the lane lines:

- Detect lane lines using the `hough_lines` produced from Hough Transform.
- We have multiple lines detected for each lane line.
- We need to average all these lines and draw a single line for each lane line.
- We also need to extrapolate the lane lines to cover the full lane line length.
- **Function:** `lane_lines(image, hough_lines)`

## Drawing Lane Lines:

- Draw detected lane lines on a blank image.
- The detected lane lines drawn on the blank image are combined with the original input image using `cv2.addWeighted()`.
- This function blends the two images together, producing an output image where the lane lines are overlaid on top of the original image.
- The function returns the resulting image with the detected lane lines overlaid.
- **Function:** `draw_lane_lines(image, lane_lines)`

## Result:

- Final image with detected lane lines overlaid.
- Lane line detection is a fundamental component of many advanced driver assistance systems (ADAS) and autonomous vehicles, contributing to enhanced road safety and automation.
- **Variable:** `result`

## Apply on video streams:

- `frame_processor` function is designed to process a single frame of a video to detect lane lines.
- This function applies a series of image processing steps, including color selection, grayscale conversion, edge detection, Hough transform for line detection, and drawing lane lines.
- The processed video stream, containing frames with detected lane lines overlaid, is obtained using `fl_image` with `frame_processor` applied to each frame of the input video.


## **Conclusion:**

The project succeeded in detecting the lane lines clearly in the video streams.
