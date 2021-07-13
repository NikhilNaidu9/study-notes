# Model Deployment Using AWS Sagemaker
## Steps
1. Create a AWS account to use it's services 
1. Create a notebook instance first so we can create a model using it 
1. Specify a `Iam` role while creating the notebook for mentioning access priveledges  
1. Create a notebook in the `us-east-1` region or else there are more configuration to be done to make it work
1. All the request goes to the `us-east-1` region and then gets redirected to the desired location - 307 redirection ( fact check remaining )
1. Import all the necessary libraries
1. `boto3` - library used to interact with the s3 buckets  
1. Bucket name shouldn't have extra characters 
1. Create an instance of the s3 bucket 
1. Create a bucket using `create_bucket` function present in the s3 instance
1. Create an output path in the bucket where all the models will get saved 
1. Upload the dataset using the Jupyter home interface
1. Perform pre-processing on the dataset like imputation, encoding, scaling and more as per required
1. Split the data into train and test sets
1. Using `sagemaker` module create a `TrainingInput` instance which will be used for storing and retreiving the training and testing data from S3 bucket
1. We used a built-in model by specifying the container 
1. We fetch container using `get_uris` method from `sagemaker` module
1. Container which is used is called `Linear Learner`
1. After specifying container we create and instance of the `Estimator` which we can find in `sagemaker` module
1. This instance will contain the arguments like container, role, train instance count, train instance type, session details and many more  
1. This instance is responsible for training the model using the specified container on desired hardware specification  
1. We can set hyperparameters on the instances like feature dimension, prediction type and many more based on the model type using `.set_hyperparameter()  `
1. At last we fit the model with training data using `.fit()`
1. After training we deploy the model using `.deploy` with arguments like instance count and instance type which make a predictor instance of the model
1. Using some serilizers from `sagemaker.serialiizers` we transform data into desired format 
1. Then using the predictor instance we can predict using test data by implementing `.predict()`
1. There we two ways that the `LinearLearner` takes the data
1. First is data in the format of the csv
1. Requirements were that the target column should be the first column of the dataframe 
1. We were facing some issue while parsing the csv file 
1. We decided to use another way 
1. Second is data in the format of the buffer or bytes
1. We load the data into memory and then ingest the data to the model 
1. This way it worked without errors and we successfully trained and deployed a model by using built-in algorithms 
1. At last by deleting all the data from the S3 bucket, endpoints that got created and notebook instances we ensured not is working and getting stored without being used which save the billing cost
1. Next we have to do model deployment when we already have a model created from some other source

---
# References

https://sagemaker.readthedocs.io/en/stable/api/training/estimators.html  

https://sagemaker-examples.readthedocs.io/en/latest/introduction_to_amazon_algorithms/linear_learner_mnist/linear_learner_mnist.html#Training-the-linear-model  

https://docs.aws.amazon.com/sagemaker/latest/dg/linear-learner.html#ll-sample-notebooks  

https://github.com/awslabs/fraud-detection-using-machine-learning/blob/master/source/notebooks/sagemaker_fraud_detection.ipynb 

https://kingsubham27.medium.com/build-train-deploy-machine-learning-models-using-aws-sagemaker-4ad682acf1cd  

https://github.com/krishnaik06/AWS-SageMaker/blob/master/Untitled2.ipynb  

https://michael-timbs.medium.com/linear-regression-with-aws-sagemaker-15feefb19342  

---
# Errors 
1. IllegalLocationConstraintException  
https://stackoverflow.com/questions/49174673/aws-s3api-create-bucket-bucket-make-exception  
1. UnexpectedStatusException  
https://stackoverflow.com/questions/61979691/changing-input-type-for-linear-learner-to-csv/64980410
1. Customer Error: Rows 1-1000 in file /opt/ml/input/data/train/train.csv have different fields than the expected size 15.  
https://github.com/aws/amazon-sagemaker-examples/issues/1017