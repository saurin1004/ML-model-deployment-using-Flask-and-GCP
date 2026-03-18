# ML-model-deployment-using-Flask-and-GCP
Title says it all. For step-by-step approach, please continue reading.
# ML Model Deployment Tutorial

# Overview

This is a simple project to elaborate how to deploy a Machine Learning model using Flask API

### **Prerequisites**

You must have Scikit Learn, Pandas (for Machine Leraning Model) and Flask (for API) installed.

### **Project Structure**

This project has four major parts :

1. model.py - This contains code for our Machine Learning model to predict employee salaries based on training data in 'hiring.csv' file.
2. app.py - This contains Flask APIs that receives employee details through GUI or API calls, computes the predicted value based on our model and returns it.
3. template - This folder contains the HTML template (index.html) to allow user to enter employee detail and displays the predicted employee salary.
4. static - This folder contains the css folder with style.css file which has the styling required for out index.html file.

### **Running the project**

1. Ensure that you are in the project home directory. Create the machine learning model by running below command from command prompt -
    
    `python model.py`
    
    This would create a serialized version of our model into a file model.pkl
    
2. Run app.py using below command to start Flask API
    
    `python app.py`
    
    By default, flask will run on port 5000.
    
3. Navigate to URL [http://127.0.0.1:5000/](http://127.0.0.1:5000/) (or) [http://localhost:5000](http://localhost:5000/)
    
    You should be able to view the homepage.
    
    Enter valid numerical values in all 3 input boxes and hit Predict.
    
    If everything goes well, you should be able to see the predcited salary vaule on the HTML page! check the output here: [http://127.0.0.1:5000/predict](http://127.0.0.1:5000/predict)
    
    ---
    
    ## Deployment on GCP
    
    1. Rename ‘app.py’ to ‘main.py’
    2. Create new ‘app.yaml’ file (copy yaml file from here “[https://github.com/saurin1004/ML-model-deployment-using-Flask-and-GCP/blob/main/app.yaml](https://github.com/saurin1004/ML-model-deployment-using-Flask-and-GCP/blob/main/app.yaml)”, this has default yaml file format for python)
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a5824ad7-d846-46e9-96c0-a50afd445658/Untitled.png)
        
    3. Open GCP
    4. Create new project
    5. Open terminal (icon with “Activate Cloud Shell” label, which is right next to search bar)
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6cd350db-6b97-48e8-a1ae-943df338ab81/Untitled.png)
        
    6. type “git clone [https://github.com/saurin1004/ML-model-deployment-using-Flask-and-GCP](https://github.com/saurin1004/ML-model-deployment-usinfg-Flask-and-GCP)” (I have already made a repository for you to clone, you can use this, or use your own repository. I hope you are aware of how to create a new github repo and upload your files from local storage to it, if no, then don’t worry I will explain it as many times needed)
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b6475642-bcbc-411c-b1d0-47d2438b7408/Untitled.png)
        
    7. Next, click on “Open Editor” button on your Terminal’s bar(with a pencil logo).
        
        Here you can see the repository you just cloned to your project.
        
    8. Go back to Terminal
    9. change your directory to the cloned directory, where your .yaml file is.
    10. Now just type “gcloud app deploy”… voila
    11. If you have properly configured your yaml and [main.py](http://main.py) file, thn there should be no problem, you maybe asked to enter server location just put it to asia-south-something and you are fine to go.
    12. This works basically for almost all ML models, for more complex problems you will have to dive deeper.
    13. Please note: I had to use github coz my mac was having issues on using gcloud SDK, if you have linux or windows, there is another way you can upload files (directly from local storage to gcp). Please explore that option as well.
