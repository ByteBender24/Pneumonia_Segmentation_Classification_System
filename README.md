# Pneumonia Detection from Chest X-rays

This project aims to detect pneumonia from chest X-ray images using a combination of image segmentation and radiomic feature-based classification. The system consists of a Flask backend for processing images and a React frontend for user interaction.

## Overview

The application allows users to upload a chest X-ray image. The backend then performs the following steps:

1.  **Lung Segmentation:** Identifies and isolates the lung regions in the X-ray image.
2.  **Infection Segmentation:** Attempts to segment the areas of potential infection within the lungs.
3.  **Radiomic Feature Extraction:** Extracts quantitative features from the segmented lung regions, focusing on the infection areas. These features describe the texture, shape, and intensity characteristics of the image.
4.  **Classification:** Uses pre-trained machine learning models (RandomForest, Logistic Regression, SVM, KNN) to classify the X-ray as either "Normal" or indicating "Pneumonia" based on the extracted radiomic features.
5.  **Visualization:** Provides visual feedback by displaying the original image alongside the lung and infection segmentations.

## Technologies Used

**Backend (Flask):**

* Python 3
* Flask: Web framework for building the API.
* Flask-CORS: For handling Cross-Origin Resource Sharing to allow communication with the React frontend.
* OpenCV (cv2): For image loading, saving, and basic image processing.
* NumPy: For numerical operations and array manipulation.
* Pandas: For data manipulation and creating DataFrames for features.
* scikit-learn (joblib): For loading pre-trained machine learning models.
* SimpleITK: For image registration and used by PyRadiomics.
* PyRadiomics: For extracting radiomic features from medical images.
* Pillow (PIL): For image format handling.

**Frontend (React):**

* React: JavaScript library for building the user interface.
* Axios: For making HTTP requests to the Flask backend.
* react-dropzone: For easy drag-and-drop file uploading.
* Bootstrap: For basic styling and layout.
* react-bootstrap: React components for Bootstrap.

## Setup and Installation

### Backend (Flask)

1.  **Clone the repository (if applicable):**
    ```bash
    git clone <repository_url>
    cd <backend_directory>
    ```

2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv nyumon
    source nyumon/bin/activate  # On Linux/macOS
    nyumon\Scripts\activate  # On Windows
    ```

3.  **Install the required Python packages:**
    ```bash
    pip install -r requirements.txt
    ```
    *(You'll need to create a `requirements.txt` file listing all the backend dependencies. A basic one would include: `Flask`, `Flask-CORS`, `opencv-python`, `numpy`, `pandas`, `scikit-learn`, `SimpleITK`, `pyradiomics`, `Pillow`)*

4.  **Download Pre-trained Models:** Place the pre-trained models (`xray_segmentation.h5`, `xray_infec_last.h5`, `randomforest_model.pkl`, `logisticregression_model.pkl`, `svm_model.pkl`, `knn_model.pkl`) in the `./models` directory. You might need to train these models separately or obtain them from a relevant source.

5.  **Run the Flask backend:**
    ```bash
    python app.py
    ```
    The backend should start running on `http://localhost:5000`.

### Frontend (React)

1.  **Navigate to the frontend directory:**
    ```bash
    cd <frontend_directory>
    ```

2.  **Install the required Node.js packages:**
    ```bash
    npm install
    # or
    yarn install
    ```

3.  **Run the React frontend:**
    ```bash
    npm start
    # or
    yarn start
    ```
    The frontend should open in your browser, usually on `http://localhost:3000`.

## Project Structure

pneumonia-detection/
├── backend/
│   ├── requirements.txt         # Backend dependencies
│   ├── app.py                   # Flask application entry point
│   ├── utils/                   # Utility functions
│   │   ├── lung_segmentation.py   # Lung segmentation logic
│   │   ├── infec_segmentation.py  # Infection segmentation logic
│   │   ├── radiomic_feature.py  # Radiomic feature extraction and classification
│   │   └── visualize.py         # Visualization utilities
│   ├── models/                  # Directory for pre-trained models (.h5, .pkl)
│   └── static/                  # For uploaded images
│       └── uploaded_images/
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── App.js               # Main React component
│   │   ├── App.css              # Styles for the main component
│   │   └── ...                  # Other React components and files
│   ├── package.json
│   └── ...
└── README.md

## Usage

1.  Open the web application in your browser (usually `http://localhost:3000`).
2.  Drag and drop a chest X-ray image into the designated area, or click to select a file.
3.  Click the "Predict" button.
4.  The backend will process the image, and the frontend will display:
    * The original uploaded image.
    * A visualization of the lung segmentation.
    * A visualization of the infection segmentation.
    * The classification result ("Normal" or "Pneumonia") from the different models.
    * The extracted radiomic features.

## Important Notes

* **Model Training:** The accuracy of this application heavily relies on the quality and training data of the pre-trained machine learning models. You might need to train your own models using a large and diverse dataset of chest X-ray images.
* **Segmentation Accuracy:** The accuracy of the segmentation steps (lung and infection) will impact the quality of the extracted radiomic features and the final classification result.
* **Hardware Requirements:** Running deep learning models (for segmentation) might require significant computational resources, including a GPU for faster processing.
* **Ethical Considerations:** This project is for research and educational purposes only and should not be used for clinical diagnosis without proper validation and regulatory approval. Medical image analysis requires careful consideration of ethical implications and patient privacy.

## Further Development

* Implement more advanced segmentation techniques.
* Incorporate explainable AI (XAI) methods to understand the model's predictions.
* Evaluate the performance of different classification models and fine-tune their hyperparameters.
* Add error handling and user feedback mechanisms.
* Improve the user interface and user experience.
* Consider deploying the application on a cloud platform.

## License

[Your License Here (e.g., MIT License)]