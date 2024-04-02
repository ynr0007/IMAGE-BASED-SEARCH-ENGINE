# IMAGE-BASED-SEARCH-ENGINE
Instead of text we will be giving image as input in the search engine and output will be showing as similar context which were loaded form the dataset given.
The dataset used in this Project can be downloaded from: "https://drive.google.com/drive/folders/18qAlnvfo1WDzdJ6JjD4D3xXiSoiSg0bp?usp=sharing"
They were Total of 3 files, The order of Execution is:
  1. Feature_extractor.py
  2. Offline.py
  3. Server.py
  4. On Server.py file copy and paste the path of index.html file.

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
