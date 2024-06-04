# Image-classification-of-KMNIST-with-CNN
The aim of this project is to perform image classification on the Kuzushiji (cursive Japanese) dataset using CNN. The dataset contains 70, 000 28*28 grey scale image with 10 classes picked by the author:おO, きKi, すSu, つTsu, なNa, はHa,まMa, やYa, れRe, をWo. These hand-written characters range from easy-to-recognize to nearly-impossible-to-recognize with bare eyes. This project will also explore the effects of changes in loss function, learning rate and batch size.

## Model Design
The model design of this project is inspired by George Seif and Dimitrios Androutsos ‘s [1] research on receptive field, where 1-D seperable convolutional kernel is used instead of square kernel to achieve large receptive field in training using very few parameters without increasing the depth of the network. Drawing idea from the research, 1-D seperable convolutional kernel is used in this project. Three kernel sizes(4,5,6) are evaluated and the training accuracy are 0.9895, 0.9801 and 0.9674 respectively. The model with kernel size of 4 is thus chosen as the base model for this project. 

## Loss function and optimizer
Loss function: Cross-entropy loss, Multi class margin loss
Optimizer: Adadelta

## Learning scheme
Initial learning rate: 0.1, 0.01
Batch size: 250, 500

## Training Termination
The training epochs has no predetermined limit. Termination condition is implemented using a validation set to avoid overfitting and save time. In every epoch, evaluation on validation set is ran after training. Training is allowed to run for at least 10 epochs. After 10 epochs, the program will compare the new accuracy with the current accuracy of the validation set. If the new accuracy is smaller than the current accuracy, the training will terminate. If the two accuracy are the same, the training continues. Else, the current model will be saved before training continues. The condition is defined as such, since through test run, for most of the time the gradient approaches a local minima after 10 epochs.

## Prediction
Since matplotlib does not support showing Japanese, a customized get_labels function for getting the Romanized equivalent of the Japanese character is defined. Saved base model is retrieved through the path generated while training to generate the prediction result.

## Result
### Results using the base learning scheme with initial learning rate = 0.1and batch size = 250:
![image](https://github.com/Heinz-Elio/Image-classification-of-KMNIST-with-CNN/assets/96605613/401b19c3-3793-4030-87a3-10790674e811)
![image](https://github.com/Heinz-Elio/Image-classification-of-KMNIST-with-CNN/assets/96605613/60f29abe-3cc7-4c25-80aa-243aac0e447e)

### Results of changing the initial learning rate from 0.1 to 0.01:
![image](https://github.com/Heinz-Elio/Image-classification-of-KMNIST-with-CNN/assets/96605613/7bf989ba-4086-477a-b051-1af06e0c2378)
![image](https://github.com/Heinz-Elio/Image-classification-of-KMNIST-with-CNN/assets/96605613/18aa58a8-65a1-4a94-8cd5-3e96f404c918)

### Results of changing the batch size from 250 to 500:
![image](https://github.com/Heinz-Elio/Image-classification-of-KMNIST-with-CNN/assets/96605613/7ed85ac4-e266-44c1-a957-fccf083d523e)
![image](https://github.com/Heinz-Elio/Image-classification-of-KMNIST-with-CNN/assets/96605613/eda101c9-b1f1-4133-adb7-75543969dca4)

## Conclusion
1. The results of training using CE loss always out-perform the results of training using multi margin loss.
2. Decrease in initial learning rate and increase in batch size have significantly lower the accuracy. 

Reference
1. Seif, G., & Androutsos, D. (2018). Large receptive field networks for high-scale image super-resolution. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition Workshops (pp. 763-772).
