# Remedy-Ticket-Classification
## Problem statement
BMC Remedy is an ITSM application that provides incident, problem management and information technology service management capabilities. This technology is offered both as an on-premises edition and a PaaS edition. IFMY IT FSC MFW uses remedy for ticket management. These tickets will be created if an issue is raised to the service desk by the user. The service desk then passes the ticket to the IT ESH team. The IT ESH team will decide and pass the ticket to the service provider if they cannot resolve the issue by themselves. Service provider then will resolve the issue and the process ends there. 

When the ticket is created by the service desk, the IT ESH team needs to examine the ticket description and classify whether it is a system bug. If it is a system bug, they will pass it on to the service provider or else the IT ESH team themselves will solve it. According to current practice, an employee will be assigned to manually classify whether the ticket is a system bug or not. This practice takes up so much time and effort.

## Task specification
A solution for Smart Remedy Ticket Management was assigned to develop that:
* Uses AI to classify whether a ticket can be handled internally or externally
* Reduces human intervention in ticket classification, and
* Saves employee’s time and effort in ticket management

## Implementation and solution method
The project started with a brainstorming session with two other colleagues. Upon the brainstorming, a multi-phased project was planned which can minimize workforces and human intervention in ticket management. Figure below shows phase one (1) of the proposal which implements ticket classification model and chatbot into the existing framework. The chatbot will implement continual learning to learn from patterns however the ticket classification model will be implemented by IT ESH team to classify the ticket whether to be passed to service provider or not.

<p align="center" width="100%">
    <img width="80%" src="https://user-images.githubusercontent.com/55419300/230080394-84b40b95-ffe7-4965-84a1-ce99c9b8caa8.png">
</p>

The proposal was presented to the manager and he approved it but due to time restrictions, only ticket classification model was assigned to develop. Ticket classification model was developed using python programming language and JupyterLab was used as IDE for the project. 

### Data extraction
The data for this project was provided by one of the colleagues who is involved with remedy ticket management. He extracted the data from the remedy application. The data contains columns ‘Incident ID’ which is the unique ID ticket, ‘Notes’ which contains the description about the ticket and ‘Assigned Group’ which is the team it was assigned to. The data provided contains 921 rows. 

### Data preprocessing
The provided data was imported to python to further process it. This imported data has empty rows and the ‘Notes’ column contains a lot of new lines. Both of these issues were fixed. Although a specific format was provided for ‘Notes’, since it is not a strict field, oftentimes it contains irrelevant information. However, the project only focuses on tickets that follow the format. Any ticket that follows the format will begin with ‘Problem Description:’. Only tickets with proper format were filtered and problem description was stored.

The column ‘Notes’ sometimes contains German language which needs to be translated to English. A python package called ‘googletrans’ can be used to translate the German string to English. Next, labels for the prediction model need to be created. The model has to predict whether the ticket can be handled internally or externally which can be determined by the column ‘Assigned Group’. Whichever ticket that contains ‘INT’ in its ‘Assigned Group’ column was handled by the internal team and vice versa. The processed data then was splitted to a training and testing set with a test size of 0.2.

### Model development
A CNN model was used to develop the ticket prediction model. It contains 5 layers which was the state-of-the-art for CNN text classification models.

### Model training & evaluation
Model training and evaluation was done simultaneously using the testing and training data. The model was trained and evaluated using different configurations but this seems to be the best output which is training accuracy of 100% and testing accuracy of 81%.

## Results of task/project
At the end of the project, a ticket classification model with accuracy of 81% was developed. This model can be used to identify whether a ticket can be handled either internally or externally. However, the model is quite not accurate enough to be implemented in the system. That is mainly because of its low testing accuracy of 81%. Generally speaking, industry standards for good accuracy is above 70%. However, depending on the model objectives, this project demands 99% accuracy and up. The low amount of data used for training and testing is a main factor for this testing accuracy. The model can definitely be improved if more data is used to train and validate the model. Even at this current stage, this model can be used to assist employees to quickly make their ticket classification which will save a lot of their time and efforts.

## Advantage, disadvantage and suggestion for task improvement
In terms of advantage, the solution can reduce human intervention in ticket management. It also saves employees time and effort into classifying the ticket. If further improved, the solution can replace human workforce in remedy ticket management which will save a lot of money for the company.

In terms of disadvantage, this solution also has a steep learning curve as it dives deep into AI and CNN models. Current accuracy of the model is also not up to the industry standard. Other than that, ‘Notes’ column of the data needs to be standardized with a specific format.

In terms of suggestion, the model needs to be trained using a large dataset to increase its accuracy. Apart from that, standard format needs to be emphasized when creating tickets which will make the prediction model more accurate.
