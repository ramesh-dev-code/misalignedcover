# Deep Learning-based Image Classification of Misaligned Cover
## Objectives    
1. To train the customized deep neural network on the device cover images
2. To develop the image classification application with the trained model to infer the real-time status of webcam images for automated optical insepction (AOI) applications

## Images   
### Aligned Device Cover (PASS)   
![](https://i.imgur.com/crEyxbY.png)
### Misaligned Device Cover (FAIL)   
![](https://i.imgur.com/PUSQOqZ.png)   

## Proposed Deep Neural Network   
![](https://i.imgur.com/kDrjwRs.png)   

## Training
1) Refer to this [link](https://github.com/ramesh-dev-code/misaligned-heat-sink/blob/main/README.md#training-platform-setup) for the training platform setup
2) Model Training: Execution Time: 2.45 m, Epochs: 57, Trained Model: best_model_14-01-2021_10:56:44.h5
3) Save the model after each epoch in the ModelCheckPoint and set patience = 30 in the EarlyStopping

## Training and Validation Performance
![](https://i.imgur.com/OJGL5s2.png)
![](https://i.imgur.com/2u9aRPf.png)


### Sample Output
**PASS**
![](https://i.imgur.com/7F8WlNI.png)

**FAIL**
![](https://i.imgur.com/NO5grtS.png)
