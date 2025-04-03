# 🖼️ IMAGE-BASED-SEARCH-ENGINE

Welcome to the **Image-Based Search Engine** — a cutting-edge visual search system that flips the traditional search paradigm. Instead of entering text queries, users simply upload an image, and the engine intelligently retrieves visually or contextually similar images from a preloaded dataset.

This project showcases how modern computer vision and feature extraction techniques can revolutionize the way we search, discover, and interact with visual data.

📄 **[Official Project Report](https://drive.google.com/file/d/1PthTos6DVZz7gy5lTqu-sWbmXABUSlkN/view?usp=sharing)**

## 🚩 Key Features

- 🔍 **Image as Input**: Search begins with an image, not a keyword.
- 🧠 **Deep Feature Extraction**: Utilizes deep learning to extract robust visual features.
- ⚡ **Efficient Similarity Matching**: Quickly finds the most contextually relevant results.
- 🖼️ **Dataset-Based Retrieval**: Results are fetched from a predefined image dataset.
- 🧩 **Modular Architecture**: Clean and extensible codebase for easy experimentation and upgrades.

## 🗂️ Project Structure

The repository consists of the following key files:

```
IMAGE-BASED-SEARCH-ENGINE/
│
├── IMG-20220906-WA0077.jpg        # Sample image for demo/testing
├── README.md                      # Project documentation
├── Steps                          # Instructions or stepwise breakdown of process
├── feature_extractor.py          # Deep feature extractor for input and dataset images
├── index.html                    # Web interface for uploading image and viewing results
├── offline.py                    # Preprocesses and indexes dataset image features
├── server.py                     # Flask server handling frontend-backend communication
```

---

## 🧩 File Breakdown

### `feature_extractor.py`
- Extracts high-level features from images using a pretrained CNN model.
- Converts images to fixed-length feature vectors for comparison.

### `offline.py`
- Preprocesses all dataset images.
- Extracts and stores features in a serialized format (e.g., `.pkl`, `.npy`) for fast retrieval.

### `server.py`
- Launches a Flask web server.
- Receives an image from the frontend, extracts its features, compares them to the dataset, and returns similar images.
- **Note:** Ensure the HTML interface is correctly linked by updating the path to `index.html`.

```python
# In server.py
from flask import Flask, render_template

app = Flask(__name__, template_folder='.')

@app.route('/')
def home():
    return render_template("index.html")
```

This setup serves the `index.html` file from the root directory, enabling users to interact with the visual search engine via the browser.

---

## ▶️ How to Run

Follow these steps to set up and launch the Image-Based Search Engine locally:

### 📦 1. Install Dependencies

Make sure you have Python installed (preferably 3.7 or above), then install required packages:

```bash
pip install tensorflow flask numpy pillow
```

### 🏗️ 2. Preprocess the Dataset

Use `offline.py` to extract and store features from the dataset images:

```bash
python offline.py
```

This will:
- Load all images from `./static/img/`
- Extract features using `FeatureExtractor`
- Save the `.npy` feature files into `./static/feature/`

### 🚀 3. Start the Flask Server

Run the backend server with:

```bash
python server.py
```

By default, the app will be hosted at:  
**http://0.0.0.0:5000/**

### 🌐 4. Access the Frontend

Open your browser and navigate to:

```
http://localhost:5000/
```

You can now upload an image and view the top visually similar images retrieved from the dataset!

---

Would you like a section for `📂 Dataset Structure`, `💡 Use Cases`, or `🤝 Contributing` next?





#Algorithm:
1. Feature_extractor.py:
  Step1:- Import modules from tensorflow.keras
  Step2:- import numpy as np
  Step3:- creat a class FeatureExtract 
  Step4:- define init function without taking any input
  Step5:- creat base_model = VGG16(weights=”imagenet”)
  Step6:- using model class divide input and output images
  Step7:- define extract under this class taking a input img
  Step8:- resize image and covert it into rbg
  Step9:- converting image into array using np
           X = image.img_to_array(img)
           X = np.expand_dims(X,axis=0)
           X = preprossing_input(X)
  Step10:- predicting the features
           feature = self.model.predict(X)[0]
  step11:- return feature / np.linalg.norm(feature)


2. Offline.py:
    Step1:- import modules from PIL, pathlib, numpy as np
    Step2:- import FeatureExtractor from feature_extractor class from feature_extract.py file
    Step3:- fe = FeatureExtractor()
    Step4:- extracting image path(“./static/img”) 
    Step5:- extracting features from the images in the above path
    Step6:- saving the features in a separate path(“./static/feature”) and converting into np array.
    Step7:- saving the features here using np.save(feature_path, feature)

3. Server.py:
    Step1:- import PIL, datetime, flask, pathlib, numpy as np
    Step2:- import FeatureExtractor from feature_extractor class from feature_extract.py file
    Step3:- creating an argument app = Flask(__name__)
    Step4:- fe = FeatureExtractor()
    Step5:- creating lists features and img_paths
    Step6:- using the for loop append all the feature .npy files to features list
    Step7:- append images from img folder like (feature_path.stem + “.jpg”) in img_path list
    Step8:- convert this features list into numpy array
    Step9:- using route decorator methods as ‘GET’, ‘POST’
    Step10:- defining index function
    Step11:- if request method is post then prosses the query
             file = request.files[‘query_img’]
    step12:- then save the query image in uploaded file in static 
    step13:- return render_template with query path , scores
    step14:- else return just render_template
    step15:- run app using app.run(“0.0.0.0”)
