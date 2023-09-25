
Driver drowsiness detection is a technology designed to monitor a driver's alertness and detect signs of drowsiness or fatigue while operating a vehicle. It aims to enhance road safety by alerting the driver or taking preventive actions to reduce the risk of accidents caused by drowsy driving

Drowsiness Detection System(webapp)
Click Here to see the demo
  GitHub last commit Libraries.io dependency status for GitHub repo  

Motivation:
According to the National Highway Traffic Safety Administration, every year about 100,000 police-reported crashes involve drowsy driving. These crashes result in more than 1,550 fatalities and 71,000 injuries. The real number may be much higher, however, as it is difficult to determine whether a driver was drowsy at the time of a crash. So, we tried to build a system, that detects whether a person is drowsy and alert him.

Installing and Configuring dlib:
We need to create an enivronment in order to install dlib, as it cannot be directly installed using pip. So, follow this commands in order to install dlib into your system if you haven't installed it previously. Make sure you have Anaconda installed, as we will be doing everyting in Anaconda Prompt.

Step 1: Update conda
conda update conda
Step 2: Update anaconda
conda update anaconda 
Step 3: Create a virtual environment
conda create -n env_dlib 
Step 4: Activate the virtual environment
conda activate env_dlib
Step 5: Install dlib
conda install -c conda-forge dlib 
If all these steps are completed successfully, then dlib will be installed in the virtual environment env_dlib. Make sure to use this environment to run the entire project.

Step to deactivate the virtual environment
conda deactivate 
Running the system:
Step 1:
Clone the repository into your system by:

git clone https://github.com/fear-the-lord/Drowsiness-Detection.git
Or directly download the zip.

Step 2:
Download the file shape_predictor_68_face_landmarks.dat here. Make sure you download it in the same folder.

Step 3:
Install all the system requirments by:

pip install -r requirements.txt
Step 4:
After the system has been setup. Run the command:

python app1.py
Step 5:
Open your browser and in the search bar type: localhost:8000 as this port is mostly used by flask. In case, this port is not available in your system, flask will try to use another port. The port number will be displayed in the command prompt. So, type in the same port number in that case as: localhost:<port_number>.

After all these steps have been completed successfully, you will see a web page opening up in the browser. Now you are free to explore the system.

Working Details:
The basic thing about drowsiness detection is pretty simple. We first detect a face using dlib's frontal face detector. Once the face is detected , we try to detect the facial landmarks in the face using the dlib's landmark predictor. The landmark predictor returns 68 (x, y) coordinates representing different regions of the face, namely - mouth, left eyebrow, right eyebrow, right eye, left eye, nose and jaw. Ofcourse, we don't need all the landmarks, here we need to extract only the eye and the mouth region.

Now, after extraxting the landmarks we calculate the Eye Aspect Ratio (EAR) as:

def eye_aspect_ratio(eye):
	# Vertical eye landmarks
	A = dist.euclidean(eye[1], eye[5])
	B = dist.euclidean(eye[2], eye[4])
	# Horizontal eye landmarks 
	C = dist.euclidean(eye[0], eye[3])

	# The EAR Equation 
	EAR = (A + B) / (2.0 * C)
	return EAR
The eye region is marked by 6 coordinates. These coordinates can be used to find whether the eye is open or closed if the value of EAR is checked with a certain threshold value.
