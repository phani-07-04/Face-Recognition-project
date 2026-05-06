# face-detection-project
🎭 Face Recognition System — FaceNet + KNN
A real-time face recognition system that classifies individuals as Accused or Normal Citizen using FaceNet embeddings and a K-Nearest Neighbors (KNN) classifier. The system uses live webcam input and processes faces on-the-fly.

📸 Demo

Live webcam feed detects faces and labels them with a classification and confidence score in real time.


🧠 How It Works

Face Detection — MTCNN detects and crops faces from images/webcam frames.
Embedding Extraction — InceptionResnetV1 (pretrained on VGGFace2) converts each cropped face into a 512-dimensional feature vector.
Classification — A KNN classifier (k=1) compares embeddings against a trained dataset and predicts the class.
Live Inference — OpenCV captures webcam frames, runs the pipeline in real time, and overlays the prediction on screen.


🗂️ Project Structure
├── face_KNN.py                  # Main script
├── knn_facenet_model.joblib     # Saved KNN model (auto-generated after training)
├── C:/Program Files/
│   ├── accused/                 # Training images of accused individuals
│   └── normal citizen/          # Training images of normal citizens
└── README.md

⚙️ Requirements
Python Version

Python 3.8 or higher

Dependencies
Install all required packages via pip:
**bashpip install torch torchvision
pip install facenet-pytorch
pip install opencv-python
pip install scikit-learn
pip install joblib
pip install Pillow
pip install numpy**

Note: If you have a CUDA-compatible GPU, install the appropriate PyTorch CUDA build from pytorch.org for faster inference.

**
📁 Dataset Setup**
Before running the script, organize your training images into two directories:
C:\Program Files\accused\
    ├── person1.jpg
    ├── person2.png
    └── ...

C:\Program Files\normal citizen\
    ├── person1.jpg
    ├── person2.png
    └── ...
Supported image formats: .jpg, .jpeg, .png
Recommendations:

Use clear, front-facing photos with good lighting.
Include multiple photos per person for better accuracy.
Ensure each image contains exactly one clearly visible face.


⚠️ You can change the directory paths by editing the accused_dir and normal_citizen_dir variables at the top of face_KNN.py.


**🚀 Usage**
Step 1 — Train and Run
Simply run the main script:
bashpython face_KNN.py
First run: The script will automatically:

Extract FaceNet embeddings from all training images.
Train the KNN classifier.
Save the model as knn_facenet_model.joblib.
Launch the live webcam feed.

Subsequent runs: The saved model is loaded directly, skipping the training step.
Step 2 — Live Recognition

A webcam window will open titled "Face Recognition - FaceNet + KNN".
Detected faces are labeled with their predicted class and confidence score.
Red label → Accused
Green label → Normal Citizen
Press Q to quit the application.


**🔧 Configuration**
You can customize the following variables at the top of face_KNN.py:
VariableDefaultDescriptionaccused_dirC:\Program Files\accusedPath to accused training imagesnormal_citizen_dirC:\Program Files\normal citizenPath to normal citizen training imagesmodel_pathknn_facenet_model.joblibPath to save/load the trained model
To retrain the model (e.g., after adding new images), simply delete knn_facenet_model.joblib and rerun the script.

🏗️ Model Details
ComponentDetailsFace DetectorMTCNN (facenet-pytorch)Embedding ModelInceptionResnetV1 pretrained on VGGFace2Embedding Size512 dimensionsClassifierKNeighborsClassifier (k=1)Input Image Size160×160 px (MTCNN output)FrameworkPyTorch

**⚠️ Limitations & Considerations**

k=1 KNN — The classifier uses only the single nearest neighbor, which can be sensitive to outliers. Consider increasing n_neighbors for larger datasets.
Single face per frame — The current implementation processes one detected face per frame. Multiple faces in the same frame may not all be classified.
Fixed categories — The system only supports two classes (Accused / Normal Citizen). Extending to more classes requires modifying the labels and label_names dictionaries.
Lighting sensitivity — Recognition accuracy can drop in poor lighting conditions or with heavily obstructed faces.
Dataset quality — Model accuracy is directly dependent on the quality and diversity of training images.


**🔒 Ethical Notice**
This project is intended for educational and research purposes only. Deploying face recognition systems for real-world surveillance, law enforcement, or identification without proper legal authorization, consent, and oversight may violate privacy laws and ethical standards. Use responsibly.

**🛠️ Troubleshooting**
No face detected during training:

Ensure images are clear and front-facing.
Try increasing the margin parameter in MTCNN initialization.

Low confidence scores:

Add more diverse training images per class.
Improve lighting conditions during webcam capture.

CUDA out of memory:

Switch to CPU by changing device = torch.device('cpu').

Webcam not opening:

Ensure your webcam is connected and not in use by another application.
Try changing cv2.VideoCapture(0) to cv2.VideoCapture(1) if you have multiple cameras.


**📄 License**
This project is open-source and available under the MIT License.

**🙌 Acknowledgements**

facenet-pytorch — FaceNet implementation in PyTorch
VGGFace2 — Pretrained face recognition dataset
scikit-learn — KNN classifier
OpenCV — Real-time webcam capture and display
