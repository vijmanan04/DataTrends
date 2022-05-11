# DataTrends
Housing Price Prediction using Common Data Tools in Java.

# Objective
Try to predict housing prices based on non-temporal features about a given house (ex. square feet, age, etc...). Download historical data from https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data. 

# Background neccessary for a ML project
The following article has a comphrensive overview of all necessary steps for an ML project: https://www.altexsoft.com/blog/datascience/machine-learning-project-structure-stages-roles-and-tools/. For this project, data splitting (train and test) and modelling are must reads. The rest is helpful in understanding other aspects of the code provided below. 

# Brief overview of the steps
1. In Java, we can use the weka package, which contains classifiers and regressors that are used for machine learning and regression analysis. To get familiar with machine learning and types of AI, skim the following article: https://www.codingame.com/playgrounds/3771/machine-learning-with-java---part-1-linear-regression#:~:text=In%20Linear%20Regression%2C%20the%20outcome,variable%20is%20categorical%20in%20nature. Specfically, read about supervised vs unsupervised learning. Since we have a dataset in this problem, this is a supervised learning problem. 

2. Download and install the weka package into java. Import the following libraries. Code provided from https://www.codingame.com/playgrounds/3771/machine-learning-with-java---part-1-linear-regression. 

          import weka.classifiers.Classifier;
          import weka.classifiers.Evaluation;
          import weka.core.Instance;
          import weka.core.Instances;
          import weka.core.converters.ArffLoader;
The first import has the classifier that we will use. 

3. Process the dataset. Convert the dataset to a csv and save in a same local directory. 

Then the following code (which may need some modifications depending on how the dataset loads, can be used to read the data. 

	public static Instances getDataSet(String fileName) throws IOException {
		/**
		 * we can set the file i.e., loader.setFile("finename") to load the data
		 */
		int classIdx = 1;
		/** the arffloader to load the arff file */
		ArffLoader loader = new ArffLoader();
		/** load the traing data */
		loader.setSource(LinearRegressionDemo.class.getResourceAsStream("/" + fileName));
		/**
		 * we can also set the file like loader3.setFile(new
		 * File("test-confused.arff"));
		 */
		Instances dataSet = loader.getDataSet();
		/** set the index based on the data given in the arff files */
		dataSet.setClassIndex(classIdx);
		return dataSet;
	}
  
 If the following code does not work, read about ArffLoader in the weka package documentation to see how to use datasets with java for ML. 
 
 4. We are using multi-variate linear regression to predict housing prices. Although we do not have to program the math behind the linear regression due to the weka library, if you are intersested, you can see that here: https://www.analyticsvidhya.com/blog/2021/08/understanding-linear-regression-with-mathematical-insights/#:~:text=Linear%20Regression%20model%20study%20the,is%20called%20multiple%20linear%20regression. Only 4 lines of code are necessary to create a linear regressor: 

		Instances trainingDataSet = getDataSet(TRAINING_DATA_SET_FILENAME); // using getDataSet method from above to train the model
		Instances testingDataSet = getDataSet(TESTING_DATA_SET_FILENAME); // get a dataset to test our model on
		/** Classifier here is Linear Regression */
		Classifier classifier = new weka.classifiers.functions.LinearRegression(); // instantiate the classifier
		/** */
		classifier.buildClassifier(trainingDataSet); // train the classifier
    
5. We can then test the accuracy of the model using the following lines:

		Evaluation eval = new Evaluation(trainingDataSet); 
		eval.evaluateModel(classifier, testingDataSet);
		/** Print the algorithm summary */
		System.out.println("** Linear Regression Evaluation with Datasets **");
		System.out.println(eval.toSummaryString());
		System.out.print(" the expression for the input data as per alogorithm is ");
		System.out.println(classifier);
    
    
 ** All code was provided from https://www.codingame.com/playgrounds/3771/machine-learning-with-java---part-1-linear-regression
