# *Linear Regression* model deployment using *Flask*

## Steps
1. Install all the packages needed for the project
1. Import `Flask` module from the `flask` package
1. Write a boiler plate code for a minimal app to run in flask 
1. Run the python file using the command in the terminal  
`python api.py`
1. Import `render_template` from the `flask` package so we can render raw *HTML* files
1. Using the `render_template` method render a *HTML* file.
1. In the `index.html` file add the text field and button to predict by using `<input>` and `<button>` tags respectively
1. Add `<form>` tag to `index.html` file so we can fetch the values from `<input>` tag or the text field
1. Make a different route for the form
1. Have the methods to be `GET` and `POST` so whenever we go to form route, first the `GET` method gets executed and then `POST` will get executed. 
1. Import `pickle` package
1. Load the saved model using the `pickle.load()` method
1. Fetch the input from the form and save it in the variable
1. Transform the data as per the input of the model is required so that it can predict 
1. Then using `model.predict()` method prediction can be carried out. 
1. Pass the data as the parameter to the `model.predict()` and save the result in a variable 
1. Print that result to the webpage so the prediction can be seen.  
1. Run the python file after every change using the command  
`python api.py`

# References 
**Error** : `Template not found error`
https://stackoverflow.com/questions/33396064/flask-template-not-found  
**Error** : `Method not allowed error`
https://stackoverflow.com/questions/21689364/method-not-allowed-flask-error-405/21689599


