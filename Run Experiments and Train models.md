# Run Experiments and Train Model
- [Create a Pipeline using AzureML Designer](#create-a-pipeline-using-azureml-designer)
- [Submit the designer pipeline run](#submit-the-designer-pipeline-run)


## Create a Pipeline using AzureML Designer
- in the home page of resources click on start now tab in Designer
- on designer page click on + button
- now our designer interface opens
- we have the canvas in the middle where we can drag and drop our modules
- we have the list of modules on the left side
- in the search box we can search any module
- now change the name of the pipeline to `loan automation`
- then below this we have a button  `show assets library` to hide and show the libray
- Now First get out data from data set 
- just drag and drop loan application dataset from asset group of dataset
      
- when we click on the dataset in canvas , we will see the parameter on the right side <br>
          - in the output we will see an icon and by clicking on it. we see the visualizations
- Now drag and drop select columns in dataset and made node between loan application dataset and select column in dataset box
- in properties now we will select columns by clicking on `edit column` <br>
           - On that screen we will choose edit by name <br>
           - then select the columns that we need by clicking the + sign <br>
           - select the dependent or target feature also <br>
- To remove the missing values in our dataset , search for `clean Missing data` and drag and drop it to our canvas to clean the missing data <br>
           - in properties click on edit column <br>
           - click on select columns by name, on which we want to perform the cleaning operations <br>
           - leave minimum missing value ratio and maximum missing value ratio to their default values <br>
           - in cleaning mode choose remove entire row <br>
- The next step is to split the data into train and test
- search for split data
- and drag and drop it on the canvas
- connect 1st output node on clean missing data to split data <br>
           - in properties on split data <br>
           - keep splitting mode as split rows, because we are going to split this dataset into rows <br>
           - keep fraction of rows in the first output dataset to 0.7, which means 70% record will be used to train dataset and 30% for test dataset <br>
           - leave randomized split as tick <br>
           - keep random seed as 123 <br>
           - put stratified split as True <br>
           - in stratified key column, click on edit column to select the column name for stratification basicall select the target column, in our case it is `Loan_Status` <br>
           - Click on save
           - Now we are ready to train our algorithm <br>
- To train the model we use two class logistic regression
- Search for two class logistic regression and drag and drop it on the canvas
- search for train model and drag and drop it on canvas
- connect one node from `Spilt Data output` to `train model input`
- also connect one node from output of `two class logistic regression` to input of `train model`
- click on logistic regression module to see the properties and in random seed provide value 123 and keep the rest values as it is
- click train model module to go to properties and in edit column select the target variable `Loan_status`
- click save it
- search for score model and drag and drop it in canvas
- now connect the output node of train model to one input node of score model
- and connect the output node of split data to second input node of score model
- now search for evaluate model and drag and drop it in canvas below the score model
- connect the output of score model to the 1st node of evaluate model
- thats it , we only have 1 model so only 1 connection from the score
- this completes our 1st pipeline in the designer

[Go To Top](#run-experiments-and-train-model)


## Submit the designer pipeline run
- to run the pipeline we have to go to the settings
- there are two important setting: run settings and output settings
- in `default compute target`, we need to specify the compute target to run our pipeline <br>
              - click on `select compute target` link <br>
              - Click on create new to create compute target <br>
              - to make it easy azureML will recommend some machine usually 2 nodes <br>
              - u can simply give a new name and create one <br>
              - or u can click on `compute->training cluster` link, and it will open the same page to create cluster that we say earlier <br>
              - but we have already created cluster so we go to select existing and click on existing cluster which we have already created `AML-CC-D001` <br>
              - click save and this will become our default compute target on which all these modules will run <br>
- But as we discussed earlier we want some of these module to run on different clusters <br>
- For that suppose we want `train model` module to run on different cluster <br>
- click on train model module -> go to its properties ->under the run setting -> here we can  change compute cluster <b>
- here we can use other cluster with higher core and processing power <br>
- similarly change compute cluster [A001] for score model also <br>
- now click on settings again <br>
- under `Default output settings` -> Select default datastore -> here we can see that the default datastore is already selected, we can create new datastore also if we want <br>
- After everything is done, click on submit
- Thet it will ask to `select an experiment`
- click on `create new`
- give new name as `LoanExperiment`
- also it will show different compute target we have selected for different modules
- now cick on submit
- then it will submit the run pipeline
- Running the pipeline will take lot of time
- 1st it shows queued -> running -> competed
- Once it is  completed we can right click on any module -> click on visualize -> this will show us evaualtion result

  [Go To Top](#run-experiments-and-train-model)
