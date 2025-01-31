# Forest_Segmentation_Analysis-Using-Partial-CE-Loss
Impact of Partial CE Loss, Point Annotation Density and Learning Rate on Forest Segmentation

Technical Report
 Impact of Point Annotation Density and Learning Rate on Forest Segmentation with Partial Cross-Entropy Loss



# 1. Introduction:
Semantic segmentation of remote sensing imagery is vital for applications like environmental monitoring, urban planning, and resource management. However, obtaining pixel-perfect segmentation masks for training is costly and time-consuming. 
In many practical scenarios, such as in the case of satellite imagery annotation, we are limited to incomplete annotations like bounding boxes, polygons, or even sparse point annotations. This motivates research into methods that can learn effectively from limited or incomplete supervision.
In this study, we focus on training a deep learning model with a custom partial cross-entropy loss function using only point annotations instead of dense masks. We investigate the impact of two critical factors:
# •	The density of point annotations
# •	The learning rates.
# 2. Methods:
# 2.1 Partial Cross-Entropy Loss Implementation:
The core of our method lies in a custom Partial Cross-Entropy (CE) loss function, which includes a focal loss component to address the class imbalance between the forest and non-forest areas. The formula for our loss function is:
pfCE = ∑ (Focal loss (pre, GT) * MASKlabeled) / ∑ MASKlabeled

Where Focal loss (pre, GT) is the focal loss between predicted probabilities and ground truth classes and MASKlabeled is the binary mask that marks the annotated pixels.
Specifically, the implemented method performs the following:
•	Calculates the one-hot encoding of the ground truth labels.
•	Computes the focal loss component using the predicted class probabilities, one-hot encoded ground truth and the focal loss parameters.
•	Applies the mask using multiplication and calculates the sum of the loss values in the labeled areas.
•	Returns the normalized loss by dividing by the number of marked points.
2.2. Model Architecture:
We used a Transfer Learning, a modified ResNet50 model pre-trained on ImageNet as the basis for our segmentation network. To adapt it for the segmentation task, the final fully connected layer is replaced by a linear layer with 2 output units representing the two classes (forest and non-forest areas). The modified architecture allows us to leverage the knowledge obtained during ImageNet training and speeds up convergence. We have also replaced the original conv1 layer of the model to be adapted to our input images.

2.3 Data Preparation:
The "Forest Aerial Images for Segmentation" dataset, which includes images of forested areas and corresponding segmentation masks, is used in our experiments. The dataset consists of RGB aerial images and single-channel mask images. The mask images have values of 0 and 1 corresponding to the "non-forest" and "forest" classes, respectively. The dataset is split into training and validation sets using a standard 80/20 split.
Preprocessing steps:
Resizing: Images and masks are resized to a 256x256 pixel resolution using a bilinear interpolation.
Normalization: Images are normalized using the ImageNet mean and standard deviation, to be able to leverage the pre-trained weights from ImageNet.
Point Annotation Generation: Point annotations are simulated from the ground truth masks by randomly selecting a pre-defined number of pixels belonging to the forest class. The selected points are marked with the value 1 in the simulated point mask.
2.4. Training:
The model is trained with the partial cross-entropy loss function using the Adam optimizer. The optimizer's momentum is 0.9 and the weight decay is 1e-
3. Experiments: 
All experiments are performed using a batch size of 16 for 10 epochs. The rest of the hyperparameters are explored in the experiments to evaluate their impact on the model performance.

3.1. Point Sampling Study
•	Configurations : [10, 50, 100, 200] points per image
•	Fixed parameters: 
•	Learning rate : 1e-4
•	Batch size : 16
•	Epochs: 10
•	Optimizer: Adam



Results:
            
       Figure 01: Metrics with 10 points                                                       Figure 02: Metrics with 50 points                      
                     
             Figure 03: Metrics with 100 points                                       Figure 04: Metrics with 200 points                
   Key Findings :
•	Optimal performance at 50 points
•	Diminishing returns beyond 50 points
•	25 points provides good balance of accuracy vs annotation effort
3.2.	Learning Rate Study
•	Configurations : [1e-3, 1e-4, 1e-5]
•	Fixed parameters: 
•	Points per image : 50 points
•	Other parameters same as above
Results:
                
     Figure 05: Metrics with 0.001                                 Figure 06: Metrics with 0.0001                         Figure 07: Metrics with 0.00001            
Key Findings:
•	Learning rate 1e-4 provides best balance
•	Higher learning rates lead to instability
•	Lower learning rates require more epochs
3.	Recommandations :
•	Use 50 points per image for annotation
•	Set learning rate to 1e-4

4.	Conclusion:
In conclusion, our study underscores that both point annotation density and the choice of learning rate significantly affect segmentation performance in a limited annotation setup. Therefore, choosing the appropriate values is key for obtaining the best possible performance while minimizing the annotation costs and training time. Future work should explore alternative sampling methods or adaptive learning rate techniques to improve model accuracy and robustness.


