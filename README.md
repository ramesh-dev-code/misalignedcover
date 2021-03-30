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

## Dataset
1. Convert the color space of the image from BGR to RGB
2. Resize the image to 224 x 224
3. Subtract the per-channel mean of the imagenet dataset (RGB:[123.68, 116.779, 103.939]) from the resized image   
4. Dataset: 600 images (PASS), 600 images (FAIL)   

## Experiment-I: Transfer-learning the pre-trained VGG model on images captured at limited distances from the camera        
1) Refer to this [link](https://github.com/ramesh-dev-code/misaligned-heat-sink/blob/main/README.md#training-platform-setup) for the training platform setup
2) Model Training: Execution Time: 2.45 m, Epochs: 57, Trained Model: best_model_14-01-2021_10:56:44.h5
3) Save the model after each epoch in the ModelCheckPoint and set patience = 30 in the EarlyStopping

### Training and Validation Performance
![](https://i.imgur.com/OJGL5s2.png)
![](https://i.imgur.com/2u9aRPf.png)


### Sample Outputs
**PASS**
![](https://i.imgur.com/7F8WlNI.png)

**FAIL**
![](https://i.imgur.com/NO5grtS.png)

### Inference   
Failed to achieve higher accuracy on testing images which are captured at different angles and varying distances from the camera   

## New Dataset   
Created the training and validation datasets with the images covering the entire device cover   
**Sample Images**   
**PASS**    
![](https://i.imgur.com/iWdp9NE.png)   
![](https://i.imgur.com/erkFnRS.png)   

**FAIL**   
![](https://i.imgur.com/ey4s6UC.png)   
![](https://i.imgur.com/bU8lKkj.png)   

## Experiment-II: Transfer-learning the pre-trained VGG model on images captured at different angles and varying distances from the camera    
1) Dataset: PASS: 1000 images per class    
2) Resize the image to 224 x 224    
3) Subtract the RGB values of each pixel from the mean RGB of the imagenet dataset. Set batch size to 32   
4) Freeze all the layers in the VGG network. FC network: 2 x 512-node hidden layer+2-node output layer with softmax classifier. Train the network on the target dataset.    
5) Epochs: 42, Time:  2.8 m, Trained Model: best_model_30-03-2021_13:29:22.h5   

### Inference     
Better than Experiment-I, but still failed on testing images captured at different angles which are not included in the training dataset   

## Experiment-III: Training the pre-trained VGG-16 model by fine-tuning the convolution layers   
1) Dataset: PASS: 1000 images per class   
2) Resize the image to 224 x 224    
3) Subtract the RGB values of each pixel from the mean RGB of the imagenet dataset. Set batch size to 32   
4) Unfreeze the last two blocks of conv layers in the VGG network. FC network: 2 x 512-node hidden layer+2-node output layer with softmax classifier. Train the network on the target dataset    
5) Epochs: 30, Time:  3.4 m, Trained Model: best_model_30-03-2021_11:58:56.h5   

### Sample Outputs   
**PASS**   
![](https://i.imgur.com/zxVdC2C.png)       
**FAIL**   
![](https://i.imgur.com/zChUV7S.png)    

### Inference   
Achieves the best performance on testing images captured at different angles   

### Performance Evaluation   
Evaluate the performance of models trained in Experiment-I and Experiment-II
![](https://i.imgur.com/jqZCo4F.png)    

