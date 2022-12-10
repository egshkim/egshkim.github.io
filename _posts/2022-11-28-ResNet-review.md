---
published: true
layout: single
title:  "[English] [Paper Review] Deep Residual Learning for Image Recognition (ResNet)"
---
<br/>

  This paper is written by Kaming He in 2015 and cited about “140,000” times.

  Pasted 7 years but still has powerful impacts.

<br/>

  ![Cited times](/assets/images/ResNet-review/다운로드.png)

<br/>

  **Why this paper has so powerful impact ?**

  1.  This paper introduced “Skip Connection” for the first time which is being used in the State-of-the-art Deep Learning Models like YOLO, Transformer, U-Net, etc.
  2.  This paper made “Deep” possible in Deep Learning. It has enabled neural networks to stack extremely deep layers in a very economic way.  

  From this, it is possible to __estimate   
  how important ResNet is__ in the field of deep learning.

<br/>

  This review assumes that the reader understands basic FCNN and CNN.

  If you lack an understanding of FCNN,  
  please refer to the following video.

  [https://www.youtube.com/watch?v=aircAruvnKk&ab\_channel=3Blue1Brown](https://www.youtube.com/watch?v=aircAruvnKk&ab_channel=3Blue1Brown) 

  <iframe src="https://www.youtube.com/embed/aircAruvnKk" width="860" height="484" frameborder="0" allowfullscreen="true"></iframe>

  If you lack an understanding of CNN, visit the following blog.
  (Figures are perfect to understand CNN…!)

  [https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53](https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53)

<br/>

  I review every paragraphs in Abstract and Introduction  
  because every paragraph is important.

  From then, I review Figures and Tables.

<br/>

  So, Let’s get started !

---
<br/>

  **### Abstract & The heart of the paper**

<br/>

  -   **Observed a problem : Degradation Problem.**  
      -   When layers be stacked extremely deep, Accuracy decreased.

<br/>          
      
  -   **The solution** this paper suggests : **ResNet**
      -   When **ResNet** stacks extremely **deep layers, it learns well.**  
          
      -   Even **extremely deep ResNet was easy to optimize.**

<br/>

---

<br/>

**The 1st paragraph in Introduction**

![The First paragraph of Introduction](/assets/images/ResNet-review/다운로드 (2).png)

<br/>

  -   **Introduces existing perspectives in the field of Deep Learning**
      
      -   **Existing perspectives :**  
          **"Deepening layers is (always) effective"**  

          <br/>

          why people had such perspectives?

          -   **The performance of Neural Networks has improved a lot by deepening layers.**
          -   **As the layer is deepened, the level of extracted features can be further enriched.**
          -   **Recent state-of-the-art models on ImageNet have stacked 16~30 layers.**  
              (Quite deep, isnt’ it?)

<br/>

---

  ### **The 2nd paragraph in Introduction**

![The Second paragraph of Introduction](/assets/images/ResNet-review/다운로드 (3).png)

  -   Some people asked a question.  
      **"Really, the more layers the models stack, the better the models learn?"  
      **  
      **No. It didn't.  
      
      **
  -   It's called "Gradient Vanishing problem".  
      But this problem has been solved recently.  
      -   The weight initial value has been initialized as a normal distribution with a mean of 0 and a standard deviation of 1.
      -   It was observed that when initialized in this way, the output value of the activation function mainly exists at both ends of 0 and 1.
      -   When the output value of the activation function is at the extremes of 0 and 1, the differential value of the activation function approaches 0.  
          (Let's look at the differential values of the sigmoid function : output \* (1-output) )
      -   Then, as the layer is deeper, the back propagation value converges to zero. The gradients vanish.
      -   In other words, learning is not achieved at all.  
          
      
  -   Somehow, it is solved.
      -   Xavier Glorot and Yoshua Bengio suggested Normalized Initialization to solve this.
          -   Convolution layers in Tensorflow API used the uniform initiaization method in this paper as "default" initialization method.

  **However.. We faced another problem.**

---

  ### **The 3rd paragraph in Introduction**

![The Third paragraph of Introduction](/assets/images/ResNet-review/다운로드 (4).png)

  -   ****"Really, the more layers the models stack, the better the models perform?"**  
      
      **
      -   The problem of gradients vanishing  was solved.  
          The models with extremely deep layers, started to learn anyway.
      -   However, the Degradation problem was observed.  
          
          -   it was a phenomenon in which as the depth of the neural network deepened, the accuracy starts to "saturate".  
              
          -   Because the "Training error" increased when network be deepened, it was not due to overfitting.

![Figure 1](/assets/images/ResNet-review/다운로드 (5).png) 

```
| ![Figure 1]({{"/assets/images/ResNet-review/다운로드 (5).png"| relative_url}}) | 
|:--:| 
| Let's take a look at the left of Figure 1. As the layer be deepened, the training error increased. As shown on the right, the test error also increased. |
```

{"originWidth":1098,"originHeight":430,"style":"alignCenter","width":500,"height":196,"caption":"Let's take a look at the left of Figure 1. As the layer be deepened, the training error increased. As shown on the right, the test error also increased."}_##]

  #### **So what on earth is the problem ?**

---

  ### **The 4th paragraph in Introduction**

  [##_Image|kage@vHKVP/btrREVl0OM7/eo7OLW1iWUpdVlYpWzxKD0/img.png|CDM|1.3|{"originWidth":670,"originHeight":394,"style":"floatRight","width":500,"height":294}_##]

  -   Explains which experiements they have conducted to explore problems.  
      
      

  [##_Image|kage@bDcdLw/btrRGwTMdae/cUr66vjT6t3ie59tIBU4vK/img.png|CDM|1.3|{"originWidth":816,"originHeight":126,"style":"alignCenter","caption":"Source : https://developer.nvidia.com/discover/artificial-neural-network"}_##]

  **Suppose there are two FCNNs** that have learned that the figure shown in the above is **"Sara"**.

  **One of them has learned Sara** image with the following architecture. 

  [##_Image|kage@bCzDKo/btrRCZPVSZX/gKiT9kY9HKv4Vg6eeRgSi0/img.png|CDM|1.3|{"originWidth":1804,"originHeight":464,"style":"alignCenter","caption":"Draw neural network on https://alexlenail.me/NN-SVG/index.html"}_##]

  Then, **copy the learned neural network and add some layers** to the top (near output layer) .

  [##_Image|kage@bGxy2N/btrRDUHN7XF/3XZgt92bKHvtxbNbpdsnUK/img.png|CDM|1.3|{"originWidth":1852,"originHeight":467,"style":"alignCenter","caption":"Draw neural network on https://alexlenail.me/NN-SVG/index.html"}_##]

  Ideally, it would be nice if each added layer works as identity mapping.  
  (Identity mapping : A layer that should approximate Identity Function.)

  In other words, **it would be very nice if each added layer was optimized as a layer that approximates the identity function.**

  (Identity function is a function that print out inputs as an output.)

  **If so, this "Deeper" neural network will still be able to correctly infer Sara.**

  If the added layers successfully approximated the identity function,

  The **"Deeper" neural network should perform better, or at least simillar than the "Shallower"** neural network.

  However, **the results showed "Deeper" network performed worse.**

  [##_Image|kage@VVKcp/btrRFfY2G2F/1Zh6uoDUozGkEf2sRTuhck/img.png|CDM|1.3|{"originWidth":1098,"originHeight":430,"style":"alignCenter","width":500,"height":196,"caption":"Let's take a look at the left of Figure 1. As the layer be deepened, the training error increased. As shown on the right, the test error also increased."}_##]

  Therefore, this is a problem with the difficulty of optimization of deep neural networks.

  **It is a very fundamental problem.**  
  It's not just a matter of overfitting.

  (In fact, it is not easy for neural network layers to approximate the Identity Function.  

  Perhaps, the added layers might approximate Zero Function rather than the identity function.  

  This is because, In the first place, the weights flowing through the deep neural network have the property of approaching "0".)  


  So, how can we reduce the difficulty of optimization?

---

  ### **The 5th paragraph in Introduction**

  [##_Image|kage@bLvM2E/btrRDVT6HZ7/j0uK6LKoe4D2y9FUp6T8B0/img.png|CDM|1.3|{"originWidth":616,"originHeight":396,"style":"floatRight","width":450,"height":289}_##]

  -   Suggest ways to reduce the difficulty of optimization  
      -   Residual Mapping

  ### **The 6th paragraph In Introduction**

  [##_Image|kage@4a8P3/btrRGkMEn6N/cM3f4YCkGprjbebX7gl6a0/img.png|CDM|1.3|{"originWidth":578,"originHeight":312,"style":"floatRight","width":450,"height":243}_##]

  -   Explains Shorcut Connections

  Befor we get into the heart of this paper, **There is something to point out.**

  It's the definition of a **function**.

  Function is an expression, rule, or law that defines a relationship between one variable and another variable.

  For a certain input, function must print output in a consistent way.

  [##_Image|kage@s0ztW/btrRDYQMLl0/2shuVPMx3x2wodv3Pi2w6k/img.png|CDM|1.3|{"originWidth":340,"originHeight":306,"style":"alignCenter"}_##]

  Let's look at the picture above.

  There is a function H that print Output H(x) for Input X.

  If the output of this function "H(x)" is equal to "x", then we can say the function H is the Identity Function.

  **"Approximating Identity function"** is equal to **"Approximating the function H that makes H(x) = x."**

  The problem is that, as mentioned above, it is not easy for neural network layers to approximate the Identity Function.

  But what if we could learn H(x) - x instead of H?

  (Let's H(x) - x = F(x) ).

  Instead of learning "Ideal" H(x), The models learn "the gap between ideal and reality" H(x)-x, Residual.

  Let's change Figure 2 a little by referring to the picture above.

  [##_Image|kage@dTK9Z2/btrRGmwTwXV/r6PBTW3ynIsqlpdiKV5gtK/img.png|CDM|1.3|{"originWidth":1444,"originHeight":536,"style":"alignCenter","caption":"Ccovered the picture in Figure 2 with a blue box. That blue box represents the function H."}_##]

  The function H in that blue box will represent F(x) + x.  

  Let's remove the blue box.

  [##_Image|kage@xxurB/btrRBfTuSpB/hAEr8BaBOtEA8Plkx15oK1/img.png|CDM|1.3|{"originWidth":1162,"originHeight":465,"style":"alignCenter","caption":"H(x) = 2 weight layers + Shortcut Connections"}_##]

  The **function F** consists of **"Convolution operation - ReLu activation function operation - Convolution operation".**  

  The **function H** consists of **"Convolution operation - ReLu activation function operation - Convolution operation - An operation of adding Input x to F(x)".**

  In this case, **"an operation of adding Input x to F(x)"** is just a **"command"** **in which a parameter to be learned does not exist.**


  **It's just a "command" to add Input x.**

  **This can achieve three.**

  **1.** When updating parameters, we learn function F, not function H.  

  This is because, at "H = F(x) \+ x", "\+ x" has no parameter to learn.  

  The function F = H - x.  

  **Without additional parameters to be learned, Residual,** the gap between ideal and reality, **is learned.**

  **2.** It becomes easier for function H to approximate the Identity Function.  
  Since the function H = F(x) + x, if F(x) becomes 0, then H = 0 + x = x and H(x) = x.

  That is, **if** function **F approximates Zero Function,** function **H become Identity Function.**

  It is relatively easy to approximate the Zero Function because all the necessary parameters need to be zero.  
  (Same whether it's FCNN or CNN. All operations only consists of multiplying and adding.)

  In addition, Zero Function is easy to approximate because the weights flowing through the deep neural network have the property of approaching zero.

  **3.** Because there are no additional parameters to learn,  
  A fair comparison between  
  **"Plain Networks" without Residual Connections**  
  **"Residual Networks" with Residual Connections**  
  can be made.

---

  ### **The 7th ~ 9th paragraph in Introduction**

  [##_Image|kage@P7Hqt/btrRGwTMdlH/IcQ9akbNiYF0GyismkkuG0/img.png|CDM|1.3|{"originWidth":606,"originHeight":816,"style":"floatRight","width":450,"height":606}_##]

  The results of experiements with ResNet are summarized.

  -   With ResNet, even when the depth was extremely increased, it was easy to optimize. 
      -   Remember? Deeper plain net increased training error unexpectedly.  
      
  -   The deeper the depth, The higher the accuracy.
      
      -   ResNet has recorded the best accuracy among the state-of-the-art networks.  
          
      
  -   The results of experiements be consistent whether it's on ImageNet dataset or CIFAR-10 dataset.
      
      -   This result is not only for a certain dataset.  
          
      
  -   With 152 layers of incredible depth, ResNet is the highest ever, but fewer parameters to learn than VGG net.
      
      -   Thans to Shortcut Connections  
          
      
  -   ResNet has won the following competitions.
      
      -   ImageNet detection in ILSVRC 2015
          
      -   ImageNet localization in ILSVRC 2015
          
      -   COCO detection in COCO 2015
          
      -   COCO segmentation in COCO 2015
          

  Let's look into details in Figures and Tables.

---

  ### **Figure 3**

  **Figure 3** visualizes t**he network architectures** used in the experiment at a glance **with VGG-19.**

  [##_Image|kage@wiXUn/btrRBMDlTiB/zCUgu79W4p1lLLp1YkRHr0/img.png|CDM|1.3|{"originWidth":690,"originHeight":1042,"style":"floatRight","width":550,"height":831}_##]

  -   Plain Network
      -   If the feature map size has been halved,  
          The number of filters should be doubled to preserve the "time complexity" of each layer.   
          (Inspired by VGG philosophy)  
          
          The time complexity of an algorithm is the number of basic operations, such as multiplications and summations, that the algorithm performs.

  -   Residual Network \= Plain Network + Shortcuts
      -   Dimension Staying Shortcuts : Identity Shortcuts
      -   Dimension Increasing Shortcuts
          -   When convolve with stride of 2, Height and Width decreased,  
              Channel numbers increased.  
              
          -   For operations of F(x) + x,  
              F(x) and x should have same dimensions.  
              → Adjust the dimensions to be identical.  
              
              -   Zero padding shortcuts
              -   Projection shortcuts

---

  ### **Table 1**

  **Table 1** summarizes the **architectures** of ResNet models used in experiments on ImageNet Dataset **according to layer depth.**

  [##_Image|kage@brUTVV/btrREWd9nYm/5vcbWpcOXGsKwWbU5kCGfK/img.png|CDM|1.3|{"originWidth":944,"originHeight":412,"style":"alignCenter","caption":"Table 1. Architectures for ImageNet. Building blocks are shown in brackets (see also Fig. 5), with the numbers of blocks stacked. Downsampling is performed by conv3 1, conv4 1, and conv5 1 with a stride of 2."}_##]

  When entering every convX\_x layer, dimension be downsampled by stride 2 convolution.

  (Refer to the architecture of the 34-layer residual in Figure 3.)

  However, if you look closely at Table 1, there is something strange.  

  Whether conv2\_x or conv3\_x, output size is maintained in the convolution operation.  

  Looking at the Pytorch source code, as expected, there was an appropriate number of padding per convolution layer.

  [##_Image|kage@s4MIq/btrRA9yHl9S/L6e29FEVni4UmGMyVP0f90/img.png|CDM|1.3|{"originWidth":614,"originHeight":298,"style":"alignCenter","caption":"looking into the source code of ResNet in Pytorch, padding is performed once in 3x3 convolution within a block."}_##]

  Modified Table 1 with padding times information.

  [##_Image|kage@dsGCtZ/btrREV7zrbr/Nk0cu2Y4ih1q3bfLjECNr0/img.png|CDM|1.3|{"originWidth":688,"originHeight":315,"style":"alignCenter","caption":"Modified Table 1 with padding times information."}_##]

---

  ### **Table 2**

  **Table 2** summarizes **validation error** after learning **ImageNet 2012 Classification Dataset.**

  [##_Image|kage@Fb81V/btrRCZbuMcr/Q5zr8fHXQShfS896SriFTk/img.png|CDM|1.3|{"originWidth":499,"originHeight":251,"style":"floatRight"}_##]

  -   ImageNet 2012 Classification Dataset
      -   1,000 classes
      -   128 millions Training set
      -   5 millions Validation set  
          
          

  -   **Results**
      -   **the deeper the Plain net,** the higher the error
      -   **the deeper the ResNet, the lower the error**

  ### **Figure 4**

  **Figure 4** visualizes error transitional curve on **ImageNet 2012 Classification Dataset.**

  [##_Image|kage@b3jP52/btrRGlLvoEK/HEA8nnklkQW6kKKTVUlhq0/img.png|CDM|1.3|{"originWidth":1251,"originHeight":416,"style":"alignCenter","caption":"Figure 4. Training on ImageNet. Thin curves denote training error, and bold curves denote validation error of the center crops. Left: plain networks of 18 and 34 layers. Right: ResNets of 18 and 34 layers. In this plot, the residual networks have no extra parameter compared to their plain counterparts."}_##]

  -   The authors suggests that the error increase when deepening the Plain net is not due to gradients vanishing.  
      
      -   Already applied methods which have solved gradients vanishing.
      -   If it is due to gradients vanishing, learning should not have been achieved.  
          -   But as you see, Plain-34 has competitive accuracy.
          -   It means, learning is being achieved to some degree.

  Let's summarize Table 2 and Figure 4.

  [##_Image|kage@bKRaR5/btrRACVEdGx/G2rhyKAWL0jzR4inyb0os0/img.png|CDM|1.3|{"originWidth":1368,"originHeight":367,"style":"alignCenter"}_##]

  -   **Degradation problem** can be solved with **Residual Learning**.
      -   **When ResNet be deepened**, **Training error and** **Validation error decreased.**  
          
      
  -   **Verified effects of Residual Learning in Deep Neural Networks.**
      -   **ResNet-34 decreased error 3.5% compared to Plain-34**  
          
      
  -   **ResNet optimize much faster than Plain net.**
      -   If Neural Network is not very deep, Plain net performs quite good. (27.94 vs 27.88)
      -   But you should still use **ResNet. It optimizes very fast.** 

---

  ### **Table 3 ~ 5**

  With dimension increasing shortcut connections,

  Used 2 methods to make the dimensions be same.(Refer to Figure 3 explanation)

  [##_Image|kage@nLcGl/btrRAhRDHVT/cZMVbcFKfjEUIpykMtBkeK/img.png|CDM|1.3|{"originWidth":794,"originHeight":1051,"style":"floatRight","width":450,"height":596}_##]

  -   Zero padding shortcuts : Add channels which have "0" values.
      -   No parameters to be learned.  
          
      
  -   Projection shortcuts : 1x1 convolution for doubling filter numbers 
      -   There are parameters to be learned.

  **Table 3** summarized validation errors with the above two methods in various combinations on **Dimension Increasing Shortcuts and Dimension Staying Shortcuts.**

---

  Let's look into the **middle part of Table 3.**

  Compared Plain net and ResNet-34 with A/B/C options.

  [##_Image|kage@dGBuyC/btrRAMqhWAT/KTeLnXrtd5xwCKcCKoSdek/img.png|CDM|1.3|{"originWidth":604,"originHeight":440,"style":"alignCenter"}_##]

  -   **Option A**
      -   Dimension Increasing Shortcuts : use Zero padding shortcuts
      -   Dimension Staying Shortcuts : use Identity shortcuts
      -   → All shortcuts have no parameters to be learned.  
          
      
  -   **Option B**
      -   Dimension Increasing Shortcuts : use projection shortcuts
      -   Dimension Staying Shortcuts : use Identity shortcuts
      -   → Dimension Increasing Shortcuts introduce parameters to be learned.  
          
      
  -   **Option C**
      -   Dimension Increasing Shortcuts : use projection shortcuts
      -   Dimension Staying Shortcuts : use projection shortcuts
      -   → All Shortcuts introduce parameters to be learned.

  ****summarize** the middle part of Table 3 :**

  -   **With any options, Better performance than plain-34.**
  -   With B option is better than with  A.  
      **Because, with option A, residual learning isn't achieved in **zero padded channels.****  
      
  -   Insignificant differences between A/B/C → **Projection shortcuts are not essential to solve degradation problem.**  
      
  -   **Used economic option B in the left experiments.**

---

  Let's look into **the bottom of Table 3.**

  [##_Image|kage@CXrlt/btrRAhqwSBv/JiSy0DkBUD3BuHHP2Rnsm0/img.png|CDM|1.3|{"originWidth":604,"originHeight":440,"style":"alignCenter"}_##]

  ResNets with more layers than 34 were also tested.

  However, there were too many parameters to use the building block as it was.

  So, ResNet-50, ResNet-101, ResNet-152 use new building blocks.

  [##_Image|kage@mgwCy/btrRGxkPyWu/k64yMFeWd4sRUvtDA9Loik/img.png|CDM|1.3|{"originWidth":629,"originHeight":341,"style":"alignCenter"}_##]

  Looking at the picture on the right side of Figure 5, "bottleneck" building block is shown.

  In the bottomleneck block, the number of channels is reduced by the first 1x1 convolution.

  It then goes through 3x3 convolution.

  As the 1x1 convolution is performed again, the number of channels is recovered.

  I compared the number of learning parameters because I was curious if the Bottleneck building block was really efficient.

  [##_Image|kage@qkhun/btrRAhxj5or/pPbbjUMr1O2QoIeKYnzpkK/img.png|CDM|1.3|{"originWidth":1283,"originHeight":591,"style":"alignCenter"}_##]

  Certainly,  
  the number of parameters of the botleneck building block in the blue box is less than that of the building block in the red box,  
  so the operation will be efficient.

---

  summarizes the bottom of Table 3  + Table 4 + Table 5 :

  [##_Image|kage@dYjkF4/btrRAipsoRu/a6ib9tfvBcxMriwqbjMKQK/img.png|CDM|1.3|{"originWidth":1192,"originHeight":302,"style":"alignCenter","caption":"Table 3, 4, 5"}_##]

  -   the bottom of Table 3
      -   Even extremely deep ResNet learns well.
      -   The deeper the ResNet, The lower the error.  
          
      
  -   Table 4
      -   ResNet-34 has beaten all state-of-the-art deep learning models.
      -   Single model ResNet-152 has beaten all state-of-the-art deep learning ensemble models.  
          
      
  -   Table 5
      -   Made a ResNet Ensemble with 6 different ResNets.
      -   Won 2015 ILSVRC with Top-5 error 3.57% (Improved existing error 26%.)

---

  ### **Table 6**

  **Experiments were conducted on CIFAR-10 Dataset to show that ResNet is not limited to a certain dataset.**

  The authors conducted experiments with CIFAR-10 Dataset with "simple architectures" on purpose.

  It was in order to focus on analyzing movement of extremely deep neural networks rather than produce good results.

  A figure summarizing the "simple architecture" used for learning CIFAR-10 Dataset is inserted in the paper.

  [##_Image|kage@opjpW/btrRFfdFPay/jYIXLktE7AClYlrVEErmk0/img.png|CDM|1.3|{"originWidth":573,"originHeight":131,"style":"alignCenter","width":450,"height":103,"caption":"Conducted experiments on CIFAR-10 with simple ResNet like the above."}_##]

  With the above picture, couldn't have a good grasp, so I draw following table.

  [##_Image|kage@b0kPs1/btrRHCTOgoz/lFg8xZfHBXd583EzhTMUtK/img.png|CDM|1.3|{"originWidth":1470,"originHeight":310,"style":"alignCenter","caption":"Conducted experiments on CIFAR-10 with simple ResNet like the above."}_##]

  The result is following.

  [##_Image|kage@1evUW/btrRBe7VJ93/F37SAWKv5u25Bf3JahKwA1/img.png|CDM|1.3|{"originWidth":581,"originHeight":521,"style":"alignCenter"}_##]

  **Table 6**

  -   ResNet has beaten FitNet and Highway, the existing best Classification models
  -   **ResNet performs better with much fewer parameters.**

  Q. By the way, Table 6 shows data augmentation be conducted.

  FitNet and Highway was learned with data augmentation, as well ?

  → Reviewing those models' papers, It was. However, augmentation mothods differ.

---

  ### **Figure 6**

---

  Let's look into the left of Figure 6.

  [##_Image|kage@lkWrh/btrRGv8qSuw/fpvvk29rBfLcpmKkalimSk/img.png|CDM|1.3|{"originWidth":1820,"originHeight":488,"style":"alignCenter","caption":"Figure 6. Training on CIFAR-10. Dashed lines denote training error, and bold lines denote testing error. Left: plain networks. The error of plain-110 is higher than 60% and not displayed. Middle: ResNets. Right: ResNets with 110 and 1202 layers."}_##]

  The following conclusions can be drawn through the left picture of Figure 6, the left picture of Figure 4, and the existing paper.

  ### _**""The optimization difficulity of deep neural networks is a FUNDAMENTAL problem."**_

  ### (It's not a matter of overfitting.)

  [##_Image|kage@CFSxn/btrRBKMke1b/eJYWh4SVmsfBS2lb8uPEZ0/img.png|CDM|1.3|{"originWidth":366,"originHeight":302,"style":"floatRight"}_##]

  -   the left of Figure 6
      -   The deep plain-net "suffers" from the increased depth, and the training error increases as the depth increases.  
          
      
  -   the left of Figure 4
      -   For ImageNet Dataset,  
          it was observed that the training error increases as the depth increases.  
          
      
  -   Similar observations have been reported with MNIST dataset.  
      -   _R. K. Srivastava, K. Greff, and J. Schmidhuber. Highway networks. arXiv:1505.00387, 2015._

---

  The following conclusions can be drawn through the picture in the middle of Figure 6 and the picture on the right of Figure 4.

  [##_Image|kage@bRYiBh/btrREVGi5xJ/r1rufvCeNM0mcPV946jsgk/img.png|CDM|1.3|{"originWidth":1819,"originHeight":488,"style":"alignCenter","caption":"Figure 6. Training on CIFAR-10. Dashed lines denote training error, and bold lines denote testing error. Left: plain networks. The error of plain-110 is higher than 60% and not displayed. Middle: ResNets. Right: ResNets with 110 and 1202 layers."}_##]

  ### _**"ResNet has overcome the optimization difficulity. Accuracy increased when depth increased."**_

  [##_Image|kage@cDTcsF/btrRGmjl4Tr/LnmyOx5VDoBqAxN2fXkQ70/img.png|CDM|1.3|{"originWidth":365,"originHeight":300,"style":"floatRight"}_##]

  -   the middel of Figure 6
      -   As depth increased in ResNet, Training error and Testing error decreased.
  -   the right of Figure 4
      -   Similar observations have been made with ImageNet dataset.

---

  Thereafter, the ResNet model with 1202 layers was evaluated by setting n = 200.

  [##_Image|kage@O1umb/btrRHA9vvBp/4ya0AmdPKiPKXLFLhQzRM1/img.png|CDM|1.3|{"originWidth":1821,"originHeight":482,"style":"alignCenter","caption":"Figure 6. Training on CIFAR-10. Dashed lines denote training error, and bold lines denote testing error. Left: plain networks. The error of plain-110 is higher than 60% and not displayed. Middle: ResNets. Right: ResNets with 110 and 1202 layers."}_##]

  **The test error of ResNet-1202** was 7.93%, **higher than that of ResNet-110.**

  **The authors argue that this may be due to overfitting.**

  Because, although the test error is high, the training error of ResNet-1202 is similar to that of ResNet-110.

  The authors speculate that **ResNet-1202 would be a "unnecessarily" large model to train small datasets such as CIFAR-10.**

  It is also mentioned that follow-up research will be conducted by applying a Regularization technique such as Dropout.

---

  ### **Figure 7**

  [##_Image|kage@dzMy9x/btrRAiwe8x9/kw1QLOZCvQ9lGd97S102d1/img.png|CDM|1.3|{"originWidth":967,"originHeight":532,"style":"alignCenter","caption":"Figure 7. Standard deviations (std) of layer responses on CIFAR10. The responses are the outputs of each 3&amp;times;3 layer, after BN and before nonlinearity. Top: the layers are shown in their original order. Bottom: the responses are ranked in descending order."}_##]

  Figure 7 is a graph of the standard deviation of outputs for each layer according to the layer index.

  Since **ResNet learns residual**, or "the gap between ideal and reality",  
  the authors say it was expected that there would be **smaller layer responses than Plain-net.**  

  **Figure 7 supports** such expectations.

---

  ### **Table 7, 8**

  [##_Image|kage@wgfUX/btrRCYXZJWx/WVAFuxATMJugbiakvHw7sK/img.png|CDM|1.3|{"originWidth":952,"originHeight":572,"style":"alignCenter"}_##]

  Tables 7 and 8 show the results of experiments with ResNet on the Object Detection task, not the Image Classification task.

---

  Lastly, the authors wrap up this paper emphasizing on the excellence of ResNet, revealing that ResNet has won the following competitions.

  -   ImageNet detection in ILSVRC 2015
  -   ImageNet localization in ILSVRC 2015
  -   COCO detection in COCO 2015
  -   COCO segmentation in COCO 2015
