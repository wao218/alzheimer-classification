# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) 

# Project 5: Predicting Dementia

## Problem Statement

You are a data science team that has been tasked by the UK government to develop a diagnostic solution that can improve the prediction rates of dementia and Alzheimer's within UK hospitals.  Using a Convolutional Neural Network on brain scan imaging, our group wishes to predict Alzheimer's disease with at least 50% accuracy and a recall of at least 64%. This metric is benchmarked to the average diagnostic performance of hospitals across the UK for patients, and an improvement in detection here can mean better outcomes and care for those within its early stages.


## Background

Alzheimer's disease is the most common influencer of dementia, as 62% of dementia cases are explained by the onset of Alzheimer's. The difference between the two diseases is shown below.

![](../support/vs.jpg)

The early diagnosis of both these conditions can greatly influence outcomes as treatment is available earlier, improving quality of life on behalf of patients, and reducing the overall impact of dementia on the economy, as care costs are lower and patients can continue working for longer.

In the United Kingdom, healthcare entities are instrumental in the recognition of dementia in the community. However, data suggests that current diagnostic effectiveness in the UK is less than ideal, and in a position to be improved. In 2018, Alzheimer's Research UK indicated that the diagnosis of dementia was only 67% effective ([*Source*](https://www.dementiastatistics.org/statistics/diagnoses-in-the-uk/)), suggesting that a third of patients did not receive a correct diagnosis. In individual healthcare systems in the UK, the range on this diagnosis varies anywhere from 54% to 80% ([*Source*](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6935598/)), as privacy policies and a lack of communication between systems can limit a practitioner's ability to fully evaluate a patient. 

Even for patients with a prior diagnosis of dementia, as one UCL study found, the identification rates of dementia by the hospitals they later attended was only 64% in 2016 ([*Source*](https://www.ucl.ac.uk/news/2018/apr/hospitals-often-missing-dementia-despite-prior-diagnosis)). 

The identification of dementia and Alzheimer's is critical to the current healthcare system in the UK, and improved outcomes can be attained by the improved effectiveness of diagnostic imaging via deep learning. In other [*regions*](https://mymodernmet.com/algorithm-identifies-alzheimers-brain-changes/), this is already the case, as algorithms are being developed as a means of filling diagnostic gaps worldwide.

#### Sources

- Diagnoses in the UK. Dementia Statistics Hub. (2021, July 7). Retrieved October 1, 2021, from https://www.dementiastatistics.org/statistics/diagnoses-in-the-uk/. 

- Rasmussen, J., &amp; Langerman, H. (2019, December 24). Alzheimer's disease - why we need early diagnosis. Degenerative neurological and neuromuscular disease. Retrieved October 1, 2021, from https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6935598/. 

- Ototo, Shovava, Day, T. is A., Comma, &amp; Colorsheets, V. (2021, September 30). New algorithm accurately spots early signs of brain changes before alzheimer's disease. My Modern Met. Retrieved October 1, 2021, from https://mymodernmet.com/algorithm-identifies-alzheimers-brain-changes/. 

- Ucl. (2019, June 28). Hospitals often missing dementia despite prior diagnosis. UCL News. Retrieved October 1, 2021, from https://www.ucl.ac.uk/news/2018/apr/hospitals-often-missing-dementia-despite-prior-diagnosis. 

Ford, E., Rooney, P., Oliver, S., Hoile, R., Hurley, P., Banerjee, S., van Marwijk, H., &amp; Cassell, J. (2019, December 2). Identifying undetected dementia in UK primary care patients: A retrospective case-control study comparing machine-learning and standard epidemiological approaches. BMC Medical Informatics and Decision Making. Retrieved October 1, 2021, from https://bmcmedinformdecismak.biomedcentral.com/articles/10.1186/s12911-019-0991-9. 

## The Data

The data we are using for this project can be found on [Kaggle](https://www.kaggle.com/tourist55/alzheimers-dataset-4-class-of-images)

#### Where it originated

The data is a random sampling of brain scans, initially collected from various websites where each classification was verified.

#### What it is

The data consists of 6,400 MRI images. The data has four classes of images that show severity, classified both in a training set as well as a testing set:

- Mild Demented
- Moderate Demented
- Non Demented
- Very Mild Demented


## Methods and Modeling

#### Diagnosis Model

We began our modeling with the goal of being able to accurately being able to predict Alzheimer’s in a patient.

For the diagnosis model, the goal was to deliver the simplest model that did better than the benchmark metrics outlined in the problem statement. The majority of hospital computers aren’t very powerful, so we wanted a model that would work in an environment with little resources. 

This would be very important when it came to model retraining. With just 1,000 nodes in the first hidden layer, we were able to achieve this goal. Because the model didn’t take a lot of time to train, we then focused on increasing complexity of the model so that it is more accurate while still making sure that there wasn’t a large trade off between model complexity and training time. At 8,000 nodes, the model started to significantly take longer to train so we stopped here.

We started with standardizing the data using the Min-Max method. From a layers standpoint, we flattened our data and then used dropout. Binary Cross Entropy was our loss function, as it was a binary classification problem.

Our model’s final scoring sat at:

Accuracy: 85%   
Precision: 87%
Recall: 85%


#### Model Predicting Severity Of Dementia

For the model that rated the progression of dementia in patients, we started by creating a base model to compare our other models. The design for this model was inspired by a model found in the book “Deep Learning with Python” by Francois Chollet. We then used 2 pertained models, InceptionV3 and MobileNetV3, to compare to our base model and they offered a worse performance.





## Conclusions and Recommendations

#### Conclusions

To conclude, our predictive models have improved diagnostics compared to baseline predictions, with accuracy and recall scores that are higher than baseline scores to varying degrees. 

Seen below is a summary of our baseline metrics and chosen models:

![](../support/Results.jpg)

Our most basic neural net (for binary classification) is 35 points above baseline accuracy (50%), and in terms of recall scores is 20 points above UK averages (64%). However, the recall scoring as it related to false negatives (128 false negatives in our model results) was significantly higher than what would be comfortable for a model that has been deployed within hospitals. This is primarily because the liability a hospital could incur and the delayed care a patient could receive in the event of a missed diagnosis.

In terms of classifying the severity of symptoms, we chose the basic tuned model over pre-trained models, and scored a uniform score of 72% on accuracy, precision, and recall. This metric is also below what we would be comfortable with for a model that is deployed in UK hospitals, but is also higher than baseline predictions.

Our models, with additional improvement and feature development before deployment, will improve the detection rate of dementia in UK hospitals and help determine the severity of a patient's dementia.

#### Recommendations

Below are our stated recommendations

- Fine-tune InceptionV3 and MobileNetV3 models to update weights to be specific to the MRI Images. Potential to improve scores more.

    - 

- Augment the data differently and see how that impacts the models (minimize shear and distortions, sharpening, changing contrast)

    -

- Integrate within existing image record data at select hospitals to begin testing over larger sets of image data.

    - Being able to integrate into existing image record data at hospitals will allow us to test out a greater sample of image scans, and test our model in an industry environment.

- We could use higher resolution images with more detail for our models to train with

- Develop the program to be hosted on a local machine

    - Given the extensive computational resources of our neural net, the model is currently unable to be hosted on local machines. An app that can run our model feasibly on one will enable hospital staff have greater access to these predictive models in their dealings with patients.
    
- Try to use other patient data to try and predict dementia
- General Wellness Survey
