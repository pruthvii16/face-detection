import cv2

# Load the image
image_path = 'path_to_your_image.jpg'
image = cv2.imread(image_path)

# Define the coordinates of the eyes and mouth region for a typical face
eye_region = [(180, 200), (280, 200)]
mouth_region = [(180, 300), (280, 400)]

# Calculate the region for the forehead
forehead_region = [(eye_region[0][0], 100), (eye_region[1][0], eye_region[0][1])]

# Check if the defined regions have significant color difference
eye_diff = cv2.absdiff(image[eye_region[0][1]:eye_region[1][1], eye_region[0][0]:eye_region[1][0]], image[forehead_region[0][1]:forehead_region[1][1], forehead_region[0][0]:forehead_region[1][0]])
mouth_diff = cv2.absdiff(image[mouth_region[0][1]:mouth_region[1][1], mouth_region[0][0]:mouth_region[1][0]], image[forehead_region[0][1]:forehead_region[1][1], forehead_region[0][0]:forehead_region[1][0]])

# Set a threshold for color difference
threshold = 50

# If color difference is significant, consider it as a face
if cv2.mean(eye_diff)[0] > threshold and cv2.mean(mouth_diff)[0] > threshold:
    print("Face detected!")
else:
    print("No face detected.")

# Display the image
cv2.imshow('Image with Regions', image)
cv2.waitKey(0)
cv2.destroyAllWindows()
