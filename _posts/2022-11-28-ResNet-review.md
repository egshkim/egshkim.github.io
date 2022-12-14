---
published: true
layout: single
title:  "[Paper Review] Deep Residual Learning for Image Recognition (ResNet)"
tags:
  - Residual
  - ResNet
  - Residual Connection
  - Skip Connection
  - ResNet explained
  - ResNet review
  - resnet
  - resnet paper review
  - resnet paper explained
  - resnet paper
---
  This paper is written by Kaming He in 2015 and cited about “140,000” times.

  Pasted 7 years but still has powerful impacts.

  ![Cited times](/assets/images/ResNet-review/다운로드.png)

  **Why this paper has so powerful impact ?**

  1.  This paper introduced “Skip Connection” for the first time which is being used  
  in the State-of-the-art Deep Learning Models like YOLO, Transformer, U-Net, etc.
  1.  This paper made “Deep” possible in Deep Learning.  
  It has enabled neural networks to stack extremely deep layers in a very economic way.  

  From this, it is possible to __estimate   
  how important ResNet is__ in the field of deep learning.

  This review assumes that the reader understands basic FCNN and CNN.

  If you lack an understanding of FCNN,  
  please refer to the following video.

  [https://www.youtube.com/watch?v=aircAruvnKk&ab\_channel=3Blue1Brown](https://www.youtube.com/watch?v=aircAruvnKk&ab_channel=3Blue1Brown) 

  <iframe src="https://www.youtube.com/embed/aircAruvnKk" width="860" height="484" frameborder="0" allowfullscreen="true"></iframe>
  
  <br/>

  If you lack an understanding of CNN, visit the following blog.
  (Figures are perfect to understand CNN…!)

  [https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53](https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53)

  I review every paragraphs in **Abstract and Introduction.**
  From then, I review Figures and Tables.

<br/>

  So, Let’s get started !

---
<hr color="black" size="10">

  <span style='background-color:orange; font-size:20pt;'>**Abstract & The heart of the paper**

  -   **Observed a problem : Degradation Problem.**  
      -   When layers be stacked extremely deep, Accuracy decreased.

  -   **The solution** this paper suggests : **ResNet**
      -   When **ResNet** stacks extremely **deep layers, it learns well.**  
          
      -   Even **extremely deep ResNet was easy to optimize.**

<br/>

---

<span style='background-color:orange; font-size:20pt;'>**The 1st paragraph in Introduction**

![The First paragraph of Introduction](/assets/images/ResNet-review/다운로드 (2).png){: width="50%" height="50%"}

<span style='background-color:orange; font-size:16pt;'>**Summary:**
  -   **Introduces existing perspectives in the field of Deep Learning**
      
      -   **Existing perspectives :**  
          **"Deepening layers is (always) effective"**  

          <br/>

          <u>why people had such a perspective?</u>

          -   **The performance of Neural Networks has improved a lot by deepening layers.**
          -   **As the layer is deepened, the level of extracted features can be further enriched.**
          -   **Recent state-of-the-art models on ImageNet have stacked 16~30 layers.**  
              (Quite deep, isnt’ it?)

<br/>

---

  <span style='background-color:orange; font-size:20pt;'>**The 2nd paragraph in Introduction**

![The Second paragraph of Introduction](/assets/images/ResNet-review/다운로드 (3).png){: width="50%" height="50%"}

<span style='background-color:orange; font-size:16pt;'>**Summary:**
  -   Some people asked a question.  
      **"Really, the more layers the models stack, the better the models** <span style='color: red'>**learn?"**  

      **No. It didn't.**

  -   It's called **"Gradient Vanishing problem".**  
      But this problem has been solved recently.  
      -   The weight initial value has been initialized as a normal distribution  
      with a mean of 0 and a standard deviation of 1.
      -   It was observed that when initialized in this way, the output value of the activation function mainly exists at both ends of 0 and 1.
      -   When the output value of the activation function is at the extremes of 0 and 1, the differential value of the activation function approaches 0.  
          (Let's look at the differential values of the sigmoid function : output \* (1-output) )
      -   Then, as the layer is deeper, the back propagation value converges to zero. The gradients vanish.
      -   In other words, learning is not achieved at all.  
          
  -   **Somehow, it is solved.**
      -   Xavier Glorot and Yoshua Bengio suggested **Normalized Initialization** to solve this.
          -   Convolution layers in Tensorflow API used the uniform initiaization method in this paper as "default" initialization method.

  <span style='color: red'>**However.. People faced another problem.**

---

<span style='background-color:orange; font-size:20pt;'>**The 3rd paragraph in Introduction**

![The Third paragraph of Introduction](/assets/images/ResNet-review/다운로드 (4).png){: width="70%" height="70%"}

<span style='background-color:orange; font-size:16pt;'>**Summary:**
  -   **"Really, the more layers the models stack, the better the models** <span style='color: red'>**perform?"**  

      -   **The problem of gradients vanishing  was solved.**
          The models with extremely deep layers, started to learn anyway.
      -   However, <span style='color: red'>**the Degradation problem was observed.**
          
          -   it was a phenomenon in which **as the depth of the neural network deepened,**  
          <span style='color: red'>**the accuracy starts to "saturate".**
              
          -   Because **the "Training error" increased when network be deepened,  
          it was not due to overfitting.**

<br/>

![Figure 1](/assets/images/ResNet-review/다운로드 (5).png){: width="50%" height="50%"}

<br/>

Let's take a look at the left of Figure 1.  
**As the layer be deepened, the training error increased** as well as the test error.


  <span style='color: red'>**So what on earth is the problem ?**

---

  <span style='background-color:orange; font-size:20pt;'>**The 4th paragraph in Introduction**


![4th paragraph of Introduction](/assets/images/ResNet-review/다운로드 (6).png){: width="50%" height="50%"}

<span style='background-color:orange; font-size:16pt;'>**Summary:**
  -   Explains which experiements they have conducted to explore problems.  


they conducted experients in this way.

![Sara](/assets/images/ResNet-review/다운로드 (7).png)

<br/>

The picture in the above is, "Sara".

  **Suppose there are two Fully Connected Neural Networks**,  
  and the **"shallower" model has learned the image of Sara**  
  with the following architecture. 

<br/>

![Architecture of the Shallower model](/assets/images/ResNet-review/다운로드 (8).png)

<br/>

  And suppose we have **copied the learned shallower model and add some layers** to the top (near output layer).

![Architecture of the deeper model](/assets/images/ResNet-review/다운로드 (9).png)

  Ideally, **it would be very nice**  
  <span style='color:red'>**if each added layer was optimized as a Identity mapping**</span>  
  **so that the "Deeper" network still be able to correctly infer Sara.**

  Then, the <span style='color:red'>**"Deeper" neural network should perform better, or at least simillar**</span>  
  **than the "Shallower"** neural network.

  However, **the results show** <span style='color:red'>**the "Deeper" network performed worse.**

![Figure 1](/assets/images/ResNet-review/다운로드 (5).png){: width="50%" height="50%"}

  Therefore, The authors say it is "a fundamental problem" about  
  the optimization difficulty of deep neural networks.

  Not just a matter of overfitting.

  *(In fact, it is not easy for neural network layers to approximate the Identity Function.  
  Perhaps, <span style='color:red'>**the added layers might approximate Zero Function**</span> rather than the identity function.  
  This is because, In the first place,   
  **the weights flowing through the deep neural network have the property of approaching "0".**)*


  <span style = "color:red">**How can we reduce the difficulty of optimization?**</span>

---

  <span style='background-color:orange; font-size:20pt;'>**The 5th paragraph in Introduction**


![5th paragraph of Introduction](/assets/images/ResNet-review/다운로드 (10).png){: width="50%" height="50%"}

<span style='background-color:orange; font-size:16pt;'>**Summary:**

  -   Suggest ways to reduce the difficulty of optimization  
      -   Residual Mapping

<br/>

  <span style='background-color:orange; font-size:20pt;'>**The 6th paragraph in Introduction**


![6th paragraph of Introduction](/assets/images/ResNet-review/다운로드 (11).png){: width="50%" height="50%"}

<span style='background-color:orange; font-size:16pt;'>**Summary:**
  -   Explains Shorcut Connections

---
---

<br/>

<span style='background-color:orange; font-size:20pt;'>**Pre-requistie Before Getting into the Heart**

  Befor we get into the heart of this paper, **There is a thing to point out.**

  *__Function is an expression, rule, or a thing  
  that print output for an input in a consistent way__*

![Function](/assets/images/ResNet-review/다운로드 (12).png){: width="30%" height="30%"}

  Let's look at the picture above.

  **H is a functuion that print-out output H(x) for input x.**
  **"Approximating identity function"** is equal to **"Approximating the function H that makes H(x) = x."**

  The problem is that, as mentioned above,  
  it is **not easy** for neural network layers to **approximate the identity function.**

  But <span style='color:red'>**what if layers could approximate H(x) - x instead of H?**</span>  
  **The gap between ideal and reality, the Residual.**

  Suppose "H(x) - x = F(x)".  
  Then "H(x) = F(x) + x".

  Let's change Figure 2 a bit by referring to the picture above.

<br/>

![Blux box](/assets/images/ResNet-review/다운로드 (13).png){: width="80%" height="80%"}

<br/>

  **The blue box is a function H that print-out H(x), which is equal to F(x) + x.**

  Let's remove the blue box.

<br/>

![Figure 2](/assets/images/ResNet-review/다운로드 (14).png)

<br/>

  The **function F** consists of  
  **"Convolution operation - ReLu activation function operation - Convolution operation".**  

  The **function H** consists of  
  **"Convolution operation - ReLu activation function operation - Convolution operation**  
  <span style='color:red'>**- An operation of adding Input x to F(x)".**</span>

  <span style='color:red'>**"An operation of adding Input x to F(x)"**</span> is just a  
  <span style='color:red'>**"command" to add input x**</span> **in which** <span style='color:red'>**parameters**</span> **to be learned** <span style='color:red'>**do not exist.**</span>

  **This achieves three.**

  1. When updating parameters, layer learns function F, not function H.  
  Because, in the equation "H(x) = F(x) \+ x", **"\+ x" doesn't introduce parameters to learn.**  
  **Without additional parameters,  
  learning the residual,** the gap between ideal and reality, **is achieved.**

  1. It becomes <span style = 'color:red'>**easier for function H to approximate the identity function.**</span>  
  As H(x) = F(x) + x, <span style = 'color:red'>**when F(x) becomes 0**</span>, then H(x) = 0 + x = x <span style = 'color:red'>**then H(x) = x.**</span>  
  That is, **when** function **F approximates zero function,**  
  function **H approximates identity function.**  
  And it is relatively **easy to approximate the Zero Function.** Just **make all the parameters "0".** That's all.  
  * Because All operations of FCNN and CNN only consists of multiplying and adding.  
  * Additionally, the weights flowing through the deep neural network have the property of approaching zero.  

  3. Because there are no additional parameters to learn,  
  **A fair comparison** between  
  **"Plain Networks"** without Residual Connections  
  **"Residual Networks"** with Residual Connections  
  can be made.

---
  <span style='background-color:orange; font-size:20pt;'>**The 7th ~ 9th paragraph in Introduction**

  ![7th~9th paragraphs](/assets/images/ResNet-review/다운로드 (15).png){: width="50%" height="50%"}

  **The results of experiements with ResNet are summarized.**

  -   **With ResNet**, even when the depth was extremely increased, **it was easy to optimize.** 
      -   Remember? Deeper plain net increased training error unexpectedly.  
      
  -   **The deeper the depth, The higher the accuracy** with ResNet.
      -   **ResNet has recorded the best accuracy** among the state-of-the-art networks.  
          
  -   The results of experiements be consistent whether it's on ImageNet dataset or CIFAR-10 dataset.
      -   So, these **results are not only for a certain dataset.**  
            
  -   With 152 layers of incredible depth, **ResNet is the deepest ever**, but **fewer parameters to learn** than VGG net.
      -   Thanks to Shortcut Connections  
          
  -   ResNet has won the following competitions.
      
      -   ImageNet detection in ILSVRC 2015
      -   ImageNet localization in ILSVRC 2015
      -   COCO detection in COCO 2015
      -   COCO segmentation in COCO 2015
          
  Let's look into details in Figures and Tables.

---

  <span style='background-color:orange; font-size:20pt;'>**Figure 3**

  ![Figure3](/assets/images/ResNet-review/다운로드 (16).png){: width="70%" height="70%"}

  **Figure 3** visualizes **the network architectures** used in the experiment at a glance.

  -   <span style='color:red'>**Plain Network**
      -   If the feature map size has been halved,  
          The number of filters should be doubled to preserve the "time complexity" of each layer.   
          (Inspired by VGG philosophy)  
          
          *The time complexity of an algorithm is the number of basic operations, such as multiplications and summations, that the algorithm performs.*

  -   <span style='color:red'>**Residual Network**</span> **\= Plain Network +** <span style='color:blue'>**Shortcuts**</span>
      -   Dimension Staying Shortcuts : Identity Shortcuts
      -   Dimension Increasing Shortcuts

          -   When convolve with stride of 2, Height and Width decreased, Channel numbers increased.  
              
          -   For **operations of F(x) + x, F(x) and x should have same dimensions.**  
              → Adjust the dimensions to be identical. There are 2 ways.
              
              -   Zero padding shortcuts
              -   Projection shortcuts

---

  <span style='background-color:orange; font-size:20pt;'>**Table 1**

  ![Table1](/assets/images/ResNet-review/다운로드 (17).png){: width="100%" height="7\100%"}

  **Table 1** summarizes the **architectures** of ResNet models used in experiments on ImageNet Dataset **according to layer depth.**
  
  Building blocks are shown in brackets (see also Fig. 5), with the numbers of blocks stacked.  
  Downsampling is performed by conv3 1, conv4 1, and conv5 1 with a stride of 2.

  When entering every convX\_x layer, dimension be downsampled by stride 2 convolution.  
  (Refer to the architecture of the 34-layer residual in Figure 3.)

  However, if you look closely at Table 1, there is something strange.  

  All "output size" are maintained during the convolution operations.

  Looking at the Pytorch source code, as expected, there was an appropriate number of padding per convolution layer.

  ![PytorchFigure](/assets/images/ResNet-review/다운로드 (18).png){: width="100%" height="100%"}

  So I have modified Table 1 with padding times information.

  ![ModifiedTable](/assets/images/ResNet-review/다운로드 (19).png){: width="100%" height="100%"}

---

  <span style='background-color:orange; font-size:20pt;'>**Table 2**

![Table2](/assets/images/ResNet-review/다운로드 (20).png){: width="50%" height="50%"}

  **Table 2** summarizes **validation error** after learning **ImageNet 2012 Classification Dataset.**

  -   ImageNet 2012 Classification Dataset
      -   1,000 classes
      -   128 millions Training set
      -   5 millions Validation set  

<span style='background-color:orange; font-size:16pt;'>**Summary:**
  -   **the deeper the Plain net,** the higher the error
  -   **the deeper the ResNet, the lower the error**

<br/>

---

  <span style='background-color:orange; font-size:20pt;'>**Figure 4**

  **Figure 4** visualizes error transitional curve on **ImageNet 2012 Classification Dataset.**

![Figure4](/assets/images/ResNet-review/다운로드 (21).png){: width="100%" height="100%"}


Thin curves denote training error, and bold curves denote validation error of the center crops.   
In this plot, the residual networks have no extra parameter compared to their plain counterparts.

<span style='background-color:orange; font-size:16pt;'>**Summary:**

  -   The authors suggests that the error increase when deepening the Plain net is not due to gradients vanishing.  
      
      -   Already applied methods which have solved gradients vanishing.
      -   If it is due to gradients vanishing, learning should not have been achieved.  
          -   But as you see, Plain-34 has competitive accuracy.
          -   It means, learning is being achieved to some degree.

<br/>

---

  <span style='background-color:orange; font-size:20pt;'>**Let's summarize Table 2 and Figure 4.**

![Table2&Figure4](/assets/images/ResNet-review/다운로드 (22).png){: width="100%" height="100%"}

<span style='background-color:orange; font-size:16pt;'>**Summary:**

  -   **Degradation problem** can be solved with **Residual Learning**.
      -   **When ResNet be deepened**, **Training error and** **Validation error decreased.**  
          
      
  -   **Verified effects of Residual Learning in Deep Neural Networks.**
      -   **ResNet-34 decreased error 3.5% compared to Plain-34**  
          
      
  -   **ResNet optimize much faster than Plain net.**
      -   If Neural Network is not very deep, Plain net performs quite good. (27.94 vs 27.88)
      -   But you should still use **ResNet. It optimizes very fast.** 

<br/>

---

  <span style='background-color:orange; font-size:20pt;'>**Table 3 ~ 5**

  When dimension increases by shortcut connections,  
  **Used 2 methods to make the dimensions be identical.**  
  (Refer to Figure 3 explanation)

![Table3~5](/assets/images/ResNet-review/다운로드 (23).png){: width="70%" height="70%"}

  -   **Zero padding shortcuts** : Add channels which have "0" values.
      -   No parameters to be learned.  
  -   **Projection shortcuts** : 1x1 convolution for doubling filter numbers 
      -   There are parameters to be learned.

  **Table 3** summarizes validation errors with the above two methods in various combinations  
  of **Dimension Increasing Shortcuts and Dimension Staying Shortcuts.**

<br/>

---

  <span style='background-color:orange; font-size:20pt;'> **Table 3.**

  Let's look into the middle part of Table 3.  
  Compared Plain net and ResNet-34 with A/B/C options.

![Table3](/assets/images/ResNet-review/다운로드 (24).png){: width="70%" height="70%"}

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

<span style='background-color:orange; font-size:16pt;'>**Summary:**</span>

  -   **With any options, Better performance than plain-34.**

  -   With B option is better than with  A.  
      **Because, with option A, residual learning isn't achieved in **zero padded channels.****  
      
  -   Insignificant differences between A/B/C → **Projection shortcuts are not essential to solve degradation problem.**  
      
  -   **Used economic option B in the left experiments.**

<br/>

---

  <span style='background-color:orange; font-size:20pt;'>Let's look into **the bottom of Table 3.**

![Table3](/assets/images/ResNet-review/다운로드 (25).png){: width="70%" height="70%"}

  ResNets with more layers than 34 were also tested.

  However, there were too many parameters to use the building block as it was.

  So, **ResNet-50, ResNet-101, ResNet-152 use new building blocks.**

![Table3](/assets/images/ResNet-review/다운로드 (26).png){: width="50%" height="50%"}

  Looking at the picture on the right side of Figure 5, "bottleneck" building block is shown.

  In the bottomleneck block, the number of channels is reduced by the first 1x1 convolution.

  It then goes through 3x3 convolution.

  As the 1x1 convolution is performed again, the number of channels is recovered.
  
  Would the Bottleneck building block be really efficient ?  
  I compared the number of learning parameters

![Table3](/assets/images/ResNet-review/다운로드 (27).png){: width="100%" height="100%"}

  Certainly,  
  the number of parameters of the botleneck building block in the blue box  
  is less than that of the building block in the red box,  
  so **the operation will be efficient.**

---

  <span style = 'background-color:orange; font-size:20pt;'>**Summary of the bottom of Table 3  + Table 4 + Table 5 :**

![Table3](/assets/images/ResNet-review/다운로드 (28).png){: width="100%" height="100%"}

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

  <span style = 'background-color:orange; font-size:20pt;'>**Table 6**

  **Experiments were conducted on CIFAR-10 Dataset to show 
  that ResNet is not limited to a certain dataset.**

  The authors conducted experiments with CIFAR-10 Dataset with "simple architectures" on purpose.

  It was in order to focus on analyzing movement of extremely deep neural networks rather than produce good results.

  A figure summarizing the "simple architecture" used for learning CIFAR-10 Dataset is inserted in the paper.

![Table3](/assets/images/ResNet-review/다운로드 (29).png){: width="50%" height="50%"}

  With the above picture, couldn't have a good grasp, so I draw following table.

![Table3](/assets/images/ResNet-review/다운로드 (30).png){: width="100%" height="100%"}

  The result is following.

![Table3](/assets/images/ResNet-review/다운로드 (31).png){: width="60%" height="60%"}

  <span style = 'background-color:orange; font-size:20pt;'>**Summary of Table 6:**
  -   ResNet has beaten FitNet and Highway, the existing best Classification models
  -   **ResNet performs better with much fewer parameters.**

  *Q. By the way, Table 6 shows data augmentation be conducted.
  FitNet and Highway was learned with data augmentation, as well ?
  → Reviewing those models' papers, It was. However, augmentation mothods differ.*

---

  <span style = 'background-color:orange; font-size:20pt;'>**The left of Figure 6**

  Let's look at the left of Figure 6.

![Figure6](/assets/images/ResNet-review/다운로드 (32).png){: width="100%" height="100%"}

  Dashed lines denote training error, and bold lines denote testing error.

<br/>

<span style = 'background-color:orange; font-size:16pt;'>**Summary:**</span>
  -   the left of Figure 6
      -   The deep plain-net "suffers" from the increased depth, and the training error increases as the depth increases.  
      
  -   **seen the similar observation in the left of Figure 4**
      -   For ImageNet Dataset,  
          it was observed that the training error increases as the depth increases.  
          Refer to the below figure.
          
  -   Similar observations have been reported with MNIST dataset.  
      -   _R. K. Srivastava, K. Greff, and J. Schmidhuber. Highway networks. arXiv:1505.00387, 2015._

![the left of Figure4](/assets/images/ResNet-review/다운로드 (33).png){: width="50%" height="50%"}  
*-the left of Figure 4*

  **The following comprehensive conclusion can be drawn.**

  <span style='color:red; font-size:14pt;'>_**""The optimization difficulity of deep neural networks is a FUNDAMENTAL problem."**_</span>  
  *(It's not a matter of overfitting.)*

---

  <span style = 'background-color:orange; font-size:20pt;'>**The middle of Figure 6**

  Let's look at the middle of Figure 6.

![the middle of Figure6](/assets/images/ResNet-review/다운로드 (34).png){: width="100%" height="100%"}  

  <span style = 'background-color:orange; font-size:16pt;'>**Summary:**</span>
  -   the middel of Figure 6
      -   As depth increased in ResNet, Training error and Testing error decreased.
  -   the right of Figure 4
      -   Similar observations have been made with ImageNet dataset.

![the right of Figure4](/assets/images/ResNet-review/다운로드 (35).png){: width="50%" height="50%"}  
*-the right of Figure 4*

**The following comprehensive conclusions can be drawn.**

  <span style='color:red; font-size:13pt;'>_**"ResNet has overcome the optimization difficulity. Accuracy increased when depth increased."**_

![the right of Figure6](/assets/images/ResNet-review/다운로드 (36).png){: width="100%" height="100%"}  

  Thereafter, the ResNet model with 1202 layers was evaluated by setting n = 200.

  **The test error of ResNet-1202** was 7.93%, **higher than that of ResNet-110.**

  **The authors argue that this may be due to overfitting.**

  Because, although the test error is high, the training error of ResNet-1202 is similar to that of ResNet-110.

  The authors speculate that **ResNet-1202 would be a "unnecessarily" large model to train small datasets such as CIFAR-10.**

  It is also mentioned that follow-up research will be conducted by applying a Regularization technique such as Dropout.

---

  <span style='background-color:orange; font-size:20pt;'>**Figure 7**

  ![Figure7](/assets/images/ResNet-review/다운로드 (37).png){: width="70%" height="70%"}  

  **Figure 7 is a graph of the standard deviation of outputs for each layer** according to the layer index.

  Since **ResNet learns residual**, or "the gap between ideal and reality",  
  the authors say it was **expected** that there would be **smaller layer responses than Plain-net.**  

  **Figure 7 supports** such expectations.

---

  <span style='background-color:orange; font-size:20pt;'>**Table 7, 8**

  ![Table7&8](/assets/images/ResNet-review/다운로드 (38).png){: width="70%" height="70%"}  


  Tables 7 and 8 show the results of experiments with **ResNet on the Object Detection task as well as the Image Classification task.**

---

  Lastly, the authors **wrap up this paper emphasizing on the excellence of ResNet, mentioning the following competitions ResNet has won.**

  -   ImageNet detection in ILSVRC 2015
  -   ImageNet localization in ILSVRC 2015
  -   COCO detection in COCO 2015
  -   COCO segmentation in COCO 2015
