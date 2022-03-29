#### Mnist hyperparameter tuning with Dkube pipelines.
1. This example shows how to do hyperparameter tuning with dkube pipelines.
## Create code repo
- Name: dkube-examples
- Project source: Git
- Git URL: https://github.com/pallavi-pannu-oc/hyperparameter-tuning-demo.git
- Branch: main

## Create dataset repo
- Name: mnist
- Dataset source: Other
- URL: https://s3.amazonaws.com/img-datasets/mnist.pkl.gz


## Create a model
- Name: mnist
- Keep default for others

## Katib based Hyperparameter Tuning (UI)
1. **Create a Run **
 - Runs->+Training Run.
 - Code: dkube-examples
 - Framework: Tensorflow
 - Version: 2.0.0
 - Start-up script: python mnist/train.py
 - Repos->Inputs->Datasets: select mnist and enter mountpath as /mnist
 - Repos->Outputs->Model: select mnist and enter mountpath as /model
 - For **hyperparameter tuning** upload the https://github.com/pallavi-pannu-oc/hyperparameter-tuning-demo/blob/main/mnist/tuning.json under upload tuning definition. 
 - Submit the run. 

## Tuning.yaml file Details:
1. **objective**: The metric that you want to optimize. 
2. **goal** parameter is mandatory in tuning.yaml file.
3. **objectiveMetricName:** Katib uses the objectiveMetricName and additionalMetricNames to monitor how the hyperparameters work with the model. Katib records the value of the best objectiveMetricName metric.
4. **parameters** : The range of the hyperparameters or other parameters that you want to tune for your machine learning (ML) model.
5. **parallelTrialCount**: The maximum number of hyperparameter sets that Katib should train in parallel. The default value is 3.
6. **maxTrialCount**: The maximum number of trials to run.
7. **maxFailedTrialCount**: The maximum number of failed trials before Katib should stop the experiment.
8. **algorithm**: Search algorithm to find the best hyper parameters. Value must be one of following:
  
   - random
   - bayesianoptimization
   - hyperband
   - cmaes
   - enas

## Launch Notebook (Pipeline Flow)
- Create Jupyterlab IDE with tensorflow framework.
- Select the Code dkube-examples.
- Run the mnist-pipeline-tuning.ipynb notebook, it will automatically create the hyperparameter training run.
- Go to Runs and click on the hyperparameter tuning action to see the graphs and the overall details of the katib run.



