
# Introduction to Deep Learning Project Repo

## How to Run the Code

Running the code is simplified by use of a python notebook. All that is required is to run each cell in the [Final Model](Models/Final/psmreimp_ir(1).ipynb). The training should take about 4 hours for 100 epochs for the final model and 11 and a half hours for the baseline model. The accuracies and model will be saved automatically every 10 epochs.

## Model Code

1. [Final Model](Models/Final/psmreimp_ir(1).ipynb)
2. [Baseline Model](Models/Baseline/11785_ProjMidterm_Baseline.ipynb)
3. [Other Modified Model Architectures](Models/Modified/11785_ProjMidterm_Parameter_Reduction.ipynb)
4. [Utils](Utils/plot_util.py)
5. [Data](Utils/data)

## PSMNet Literature Replication 

A PSMNet model was developed based on the literature [[1]](#1).  This was used to generate disparity maps and they were tested based on the training L1 loss and validation 3-pixel accuracy.  The PSMNet architecture from [[1]](#1) is shown in Figure 1.  

![](./Images/Architecture_PSMNet.png)*Figure 1: PSMNet Literature Architecture*

### Comparison of Results
We use the 3 pixel disparity error to evaluate our models and compare them against the original PSMNet [[1]](#1)performance.  A comparison of each model’s total number ofparameters used, error on the RGB dataset, and error on the IR dataset can be seen in Table

*Table 1: Performance Comparison*
| Name              |  Params. |RGB Error | IR Error |
| ----------------- | ------   | -------- | -------- |
| PSMNet            | 3.6 mil  | 6.4 %    | 25.9 %   |
| Our Model         | 3.1 mil  | 6.9 %    | 31.2 %   |
| v1 reduced param  | 2.77 mil | 6.7 %    | 33.3 %   |
| v2 reduced param  | 2.58 mil | 9.7 %    | 36.8 %   |
| Final model       | 1.77 mil | -        | 23.7 %   |
#### Disparity error visualization, Top row is the generated disparity map, middle row is the GT,and the last row is the error visualized on the GT

<table>
  <tr>
    <td>Figure 2: Better Disprity map </td>
     <td>Figure 3: Worse Disparity Map</td>
  </tr>
  <tr>
    <td><img src="./Images/Ref_err.png" width=600 height=400></td>
    <td><img src="./Images/Model_err.png" width=600 height=400></td> 
  </tr>
 </table>

## Modifications to the PSMNet model in literature

Three main modification to the architecture of the model were also tested. 

1. Less Convolutional layers
2. More Convolutional layers
3. 2D and 3D asymmetric convolutions
4. New feature extraction Module 


These modifications to the literature PSMNet model all reached the same minima (at differing amounts of Epochs).  Figures for the changes in loss and accuracy are shown below in Figure 4 and Figure 5.  
             Training                                              |                                        Validation
:-------------------------:|:-------------------------:
![L1 Loss](./Images/L1_loss.png)*Figure 4: L1 Loss Experiments*  |  ![Accuracy](./Images/Accuracy.png)*Figure 5: 3-pixel Accuracy Experiments*





The asymmetric convolutions idea was based on the paper "Rethinking the Inception Architecture for Computer Vision" [[2]](#2).  The inception paper has shown that for example using a 3x1 convolution followed by a 1x3 convolution is equivalent to sliding a two layer network with the same receptive field as in a 3x3 convolution.  This is shown in Figure 6.  It has been shown in the literature that the asymmetric convolutions are equivilant to sliding a two layer network with the same receptive field as in a 3x3 convolution.  This is illustrated in Figure 6.  The change to the basic block in the PSMNet architecture is shown in figure 7.  


Asymmetric Convolutions                                                                                                     |  Change in Basic Block Model Architectures 
:-------------------------:|:-------------------------:
![Spatial Factorization Figure](./Images/Spatial_Factorization.png)*Figure 6: Mini-network replacing the 3x3 convolutions [[2]](#2)*  |  ![Parameter_Reduction Figure](./Images/Parameter_Reduction.png)*Figure 7: Comparison between the original and the modified architecture with asymmetric convolutions*

## References
<a id="1">[1]</a> 
Jia.-Ren Chang and Yong.-Sheng Chen (2018). 
Pyramid Stereo Matching Network
CoRR, abs/1803.08669, http://arxiv.org/abs/1803.08669

<a id="2">[2]</a> 
Christian Szegedy and
               Vincent Vanhoucke and
               Sergey Ioffe and
               Jonathon Shlens and
               Zbigniew Wojna (2015). 
Rethinking the Inception Architecture for Computer Vision 
CoRR, abs/1512.00567, http://arxiv.org/abs/1512.00567

