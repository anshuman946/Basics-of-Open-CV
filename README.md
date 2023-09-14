# Basics-of-Open-CV
#Contains Video resizeing,rescalling, creating images using NumPy, RGB to Greyscale,Blurring the image, 
import cv2
import numpy as np
image = cv2.imread("D:\python\cat.jpeg")
#cv2.imshow('Cat', image)
cv2.waitKey(0)
cv2.destroyAllWindows()
path = "D:\python\dog.mp4"
cap = cv2.VideoCapture("D:\python\dog.mp4") #reading video
cv2.imshow('Dog',cap)

# Define the desired width and height for resizing
new_width = 640   # for img resizing & rescalling
new_height = 480

while True:
    # Read a frame from the video
    ret, frame = cap.read()

    # Check if the video has ended
    if not ret:
        break
    # Display the frame
    cv2.imshow('Video', frame)

    # Resize the frame to the desired dimensions
    resized_frame = cv2.resize(frame, (900, 610))

    # Display the resized frame
    cv2.imshow('Resized Frame', resized_frame)

    #Define the dimensions of the blank white image:
    width, height = 640, 480
    #Create a blank white image using NumPy:
    image = np.ones((height, width, 3), dtype=np.uint8) * 255
    cv2.rectangle(image, (100, 100), (400, 300), (0, 0, 255), thickness=2)  #BGR color (0, 0, 255) is red

    # Draw a filled circle
    cv2.circle(image, (300, 200), 50, (0, 255, 0), thickness=-1)  # BGR color (0, 255, 0) is green, thickness=-1 for filled circle
    # Draw a filled circle
    #cv2.circle(image, (300, 200), 50, (0, 255, 0), thickness=-1)  # BGR color (0, 255, 0) is green, thickness=-1 for filled circl
    
    # Add text
    text = "OpenCV Shapes & Text"
    font = cv2.FONT_HERSHEY_SIMPLEX
    font_scale = 1
    font_color = (255, 255, 255)  # BGR color (255, 255, 255) is white
    font_thickness = 2
    cv2.putText(image, text, (50, 50), font, font_scale, font_color, font_thickness)
    # Display the image
    cv2.imshow('Image with Shapes and Text', image)


    # converting rgb image to greyscale
    # Read the RGB image
    rgb_image = cv2.imread('D:\python\cat.jpeg')

    # Convert the RGB image to grayscale
    gray_image = cv2.cvtColor(rgb_image, cv2.COLOR_BGR2GRAY)

    # Save or display the grayscale image
    cv2.imwrite('output_gray_image.jpg', gray_image)

    # Define the kernel size for Gaussian Blur (must be an odd number)
    kernel_size = (5, 5)

    # Apply Gaussian Blur to the image
    blurred_image = cv2.GaussianBlur(image, kernel_size, 0)

    # Save or display the blurred image
    cv2.imwrite('output_blurred_image.jpg', blurred_image)


    #Changing real-time color grading for a webcam feed:

    # Create a VideoCapture object to access the webcam (0 indicates the default camera)
    cap = cv2.VideoCapture(0)

while True:
    # Read a frame from the webcam
    ret, frame = cap.read()
    if not ret:
        break

    # Apply color grading (you can adjust these parameters)
    frame = cv2.applyColorMap(frame, cv2.COLORMAP_COOL)

    # Display the graded frame
    cv2.imshow('Color Grading', frame)

    # Exit the loop if a key is pressed (e.g., 'q' for quit)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
cap.release()
cv2.destroyAllWindows()




