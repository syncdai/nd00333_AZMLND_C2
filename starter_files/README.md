*NOTE:* This file is a template that you can use to create the README for your project. The *TODO* comments below will highlight the information you should be sure to include.


# Operationalizing Azure ML

Create and try out two enpoints using Azure ML.  One provides REST API for submitting data queries to be classified by a trained Voting Ensemble model.  The second provides a REST endpoint to trigger rerunning an AutoML pipeline step on stored bank-marketing data.

## Architectural Diagram
![architecture_diagram](https://user-images.githubusercontent.com/80217508/111923271-b6a46a80-8a74-11eb-9d39-98cc0545591c.png)

Track A was done using AzureML Studio and command line.  Track B was done using Jupyter notebook.  Though the two tracks are independent, B reused several resources due to running after A.

## Key Steps
A1. Register bank-marketing tabular dataset from URL; Configure compute instance for notebooks and compute cluster for AutoML training.
![registered_datasets](https://user-images.githubusercontent.com/80217508/111924533-84e2d200-8a7b-11eb-9276-5a09bdba6a74.jpg)

A2. Run AutoML experiment on the data to find the most accurate classifier, which turned out to be a Voting Ensemble.
![experiment_completed](https://user-images.githubusercontent.com/80217508/111924551-99bf6580-8a7b-11eb-8027-ca79089939c7.jpg)
![best_model](https://user-images.githubusercontent.com/80217508/111924575-b8256100-8a7b-11eb-9560-2a73e04b368a.jpg)

A3. Register Voting Ensemble model from the experiment and deploy it using Azure Container Instance with authentication enabled.  Also, enable Application Insights to pull logs, and host Swagger documentation locally.
![logs](https://user-images.githubusercontent.com/80217508/111924606-d3906c00-8a7b-11eb-8179-9eeee9ac3d00.jpg)
![swagger](https://user-images.githubusercontent.com/80217508/111924608-d5f2c600-8a7b-11eb-8ab6-cbea2c8e569b.jpg)

A4. Consume deployed model via REST API and authentication key to classify a couple conformant data entries; Benchmark performance using Apache command.
![endpoint](https://user-images.githubusercontent.com/80217508/111924603-d0957b80-8a7b-11eb-988a-b5e6f73207cd.jpg)
![benchmark](https://user-images.githubusercontent.com/80217508/111924666-0aff1880-8a7c-11eb-9644-0e25e6b4c4b7.jpg)

B1. Reuse bank-marketing data, experiment, and compute cluster to create and run a pipeline comprised of a single AutoML step to train on the data.
![pipeline_created](https://user-images.githubusercontent.com/80217508/111924684-19e5cb00-8a7c-11eb-9d7a-a0225f1a6dce.jpg)
![bankmarketing_with_automl_module](https://user-images.githubusercontent.com/80217508/111924685-1c482500-8a7c-11eb-82ea-021bb025c4bf.jpg)
![run_widget](https://user-images.githubusercontent.com/80217508/111924688-1e11e880-8a7c-11eb-8677-590dcfb15b8b.jpg)

B2. Publish a REST endpoint for the completed pipeline.
![pipeline_endpoint](https://user-images.githubusercontent.com/80217508/111924732-55809500-8a7c-11eb-9b37-1553119f9198.jpg)
![published_pipeline_overview](https://user-images.githubusercontent.com/80217508/111924735-57e2ef00-8a7c-11eb-8a06-b91a67dde25a.jpg)

B3. Consume the endpoint using authentication header and a new experiment name, to rerun the pipeline.
![run_widget_2](https://user-images.githubusercontent.com/80217508/111924826-b14b1e00-8a7c-11eb-8f59-330ebb413a66.jpg)
![post_rest_pipeline](https://user-images.githubusercontent.com/80217508/111924833-b4460e80-8a7c-11eb-938a-4c130750c78e.jpg)

## Improvement Suggestions

For track A, it would be interesting to introduce errors when querying the model, to experience debugging with error logs and consulting the Swagger documentation in order to resolve.

For track B, the pipeline is quite simple, and the entire run seemed cacheable as a result.  Introducing PipelineParameters for a Python script step to allow different behavior, or some way to submit a new data URL, would add a new dimension of engagement when building the query message.

## Screen Recording
https://drive.google.com/file/d/1bOOTcDikuZ5jZwQXg0F7W8CFt8YOkN_O/view?usp=sharing

## Standout Suggestions
Benchmarked with Apache
