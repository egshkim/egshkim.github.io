---
published: true
layout: single
title:  "[Trial][English] [Paper Review] Deep Residual Learning for Image Recognition (ResNet)"
---

<p data-ke-size="size16">This paper has been written by Kaming He in 2015 and citated about &ldquo;140,000&rdquo; times.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">Pasted 7 years but still has powerful impacts.</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@nc0rQ/btrRAEyYbyq/GWIZFiacEY2RouK8ZJIjuk/img.png|CDM|1.3|{"originWidth":1776,"originHeight":1012,"style":"alignCenter","caption":"Paper has been cited for about 140,000 times for now."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Why this paper has so powerful impact&nbsp;?</b></p>
<ol style="list-style-type: disc;" data-ke-list-type="disc">
<li>This paper introduced &ldquo;Skip Connection&rdquo; for the first time which is used in State-of-the-art Deep Learning Models like YOLO, Transformer, U-Net, etc.</li>
<li>This paper made &ldquo;Deep&rdquo; possible in Deep Learning. It has enabled neural networks to stack extremely deep layers in a very economic way.</li>
</ol>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">From this, it is possible to estimate how important ResNet is in the field of deep learning.</p>
<p data-ke-size="size16"><br />This review assumes that the reader understands basic FCNN and CNN.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">If you lack an understanding of FCN, refer to the following video.</p>
<p data-ke-size="size16"><a href="https://www.youtube.com/watch?v=aircAruvnKk&amp;ab_channel=3Blue1Brown">https://www.youtube.com/watch?v=aircAruvnKk&amp;ab_channel=3Blue1Brown</a>&nbsp;</p>
<figure data-ke-type="video" data-ke-style="alignCenter" data-video-host="youtube" data-video-url="https://www.youtube.com/watch?v=aircAruvnKk" data-video-thumbnail="https://scrap.kakaocdn.net/dn/LSQeR/hyQmHpoZdS/iwhsxNDl6ZeHWdhINAMJ10/img.jpg?width=1280&amp;height=720&amp;face=0_0_1280_720" data-video-width="860" data-video-height="484" data-video-origin-width="860" data-video-origin-height="484" data-ke-mobilestyle="widthContent"><iframe src="https://www.youtube.com/embed/aircAruvnKk" width="860" height="484" frameborder="0" allowfullscreen="true"></iframe>
<figcaption></figcaption>
</figure>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">If you lack an understanding of CNN, see the following blog.</p>
<p data-ke-size="size16">(Figures are perfect to understand CNN&hellip;!)</p>
<p data-ke-size="size16"><a href="https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53">https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53</a></p>
<figure id="og_1668941446333" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="article" data-og-title="A Comprehensive Guide to Convolutional Neural Networks &mdash; the ELI5 way" data-og-description="Artificial Intelligence has been witnessing a monumental growth in bridging the gap between the capabilities of humans and machines&hellip;" data-og-host="towardsdatascience.com" data-og-source-url="https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53" data-og-url="https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53" data-og-image="https://scrap.kakaocdn.net/dn/YTwJb/hyQnWrIB83/vkrKcLyuXx6qTzTMlcmZFK/img.jpg?width=1200&amp;height=405&amp;face=0_0_1200_405"><a href="https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53" data-source-url="https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/YTwJb/hyQnWrIB83/vkrKcLyuXx6qTzTMlcmZFK/img.jpg?width=1200&amp;height=405&amp;face=0_0_1200_405');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">A Comprehensive Guide to Convolutional Neural Networks &mdash; the ELI5 way</p>
<p class="og-desc" data-ke-size="size16">Artificial Intelligence has been witnessing a monumental growth in bridging the gap between the capabilities of humans and machines&hellip;</p>
<p class="og-host" data-ke-size="size16">towardsdatascience.com</p>
</div>
</a></figure>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">I review every paragraphs in Abstract and Introduction because all paragraphs contain very important content.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">After introduction, I review Figures and Tables.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">So, Let&rsquo;s get started&nbsp;!</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h3 data-ke-size="size23"><b>Abstract &amp; The heart of the paper</b></h3>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>Observed a problem : Degradation Problem.</b><br />
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="color: #ee2323;"><b>When layers be stacked extremely deep, Accuracy decreased.</b></span><br /><br /></li>
</ul>
</li>
<li><b>The solution this paper suggests&nbsp;: ResNet</b><br />
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>When <span style="color: #ee2323;"><b>ResNet</b></span> stacks extremely <span style="color: #ee2323;"><b>deep layers, it learns well.</b></span><span style="color: #ff0000;"><br /></span></li>
<li>Even <span style="color: #ee2323;"><b>extremely deep ResNet are easy to optimize.</b></span></li>
</ul>
</li>
</ul>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li style="list-style-type: none;">&nbsp;</li>
</ul>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<p>[##_Image|kage@vSDGw/btrRCYQ41qc/DA1PpVxn41rCGMpUlHSOvK/img.png|CDM|1.3|{"originWidth":686,"originHeight":458,"style":"floatRight","width":450,"height":300}_##]</p>
<h3 data-ke-size="size23"><span style="color: #000000;"><b>The 1st paragraph in Introduction</b></span></h3>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>Introduces existing perspectives in the field of Deep Learning<br /><br /></b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b><span style="color: #000000;">Existing perspectives :</span></b><span style="color: #ee2323;"><b> <br />"Deepening layers is (always) effective"</b></span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>The performance of Neural Networks <span style="color: #ee2323;">has improved a lot by deepening layers.</span></b></li>
<li><b>As the layer is deepened, <span style="color: #ee2323;">the level of extracted features can be further enriched.</span></b></li>
<li><b><span style="color: #ee2323;">Recent state-of-the-art models</span> on ImageNet have stacked <span style="color: #ee2323;">16~30 layers.</span></b><br />(Quite deep, isnt&rsquo; it?)</li>
</ul>
</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<p>[##_Image|kage@lstQq/btrRAiQAmtx/90Z829dDtmTRMOESuRBuk0/img.png|CDM|1.3|{"originWidth":844,"originHeight":422,"style":"floatRight","width":450,"height":225}_##]</p>
<h3 data-ke-size="size23"><span style="color: #000000;"><b>The 2nd paragraph in Introduction</b></span></h3>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="background-color: #fdfdfd; color: #000000;">Some people asked a question.<br /><b>"Really, the more layers the models stack, the better the models<span>&nbsp;</span><span style="color: #ee2323;">learn</span>?"<br /></b><br /></span><b><span style="background-color: #fdfdfd; color: #000000;">No. It didn't.<br /><br /></span></b></li>
<li>It's called "Gradient Vanishing problem".<br />But this problem has been solved recently.<br />
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="background-color: #fdfdfd; color: #000000;">The weight initial value has been initialized as a normal distribution with a mean of 0 and a standard deviation of 1.</span></li>
<li><span style="background-color: #fdfdfd; color: #000000;">It was observed that when initialized in this way, the output value of the activation function mainly exists at both ends of 0 and 1.</span></li>
<li><span style="background-color: #fdfdfd; color: #000000;">When the output value of the activation function is at the extremes of 0 and 1, the differential value of the activation function approaches 0.</span><br /><span style="background-color: #fdfdfd; color: #000000;">(Let's look at the differential values of the sigmoid function : output * (1-output) )</span></li>
<li><span style="background-color: #fdfdfd; color: #000000;">Then, as the layer is deeper, the back propagation value converges to zero. The gradients vanish.</span></li>
<li>In other words, learning is not achieved at all.<br /><br /></li>
</ul>
</li>
<li>Somehow, it is solved.
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Xavier Glorot and Yoshua Bengio suggested Normalized Initialization to solve this.
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Convolution layers in Tensorflow API used the uniform initiaization method in this paper as "default" initialization method.</li>
</ul>
</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="color: #ee2323;"><b>However.. We faced another problem.</b></span></p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h3 data-ke-size="size23"><b>The 3rd paragraph in Introduction</b></h3>
<p>[##_Image|kage@bICmZW/btrREWysahI/616SfZF9AX34fw1qhturn0/img.png|CDM|1.3|{"originWidth":772,"originHeight":308,"style":"floatRight","width":450,"height":180}_##]</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b><b>"Really, the more layers the models stack, the better the models<span>&nbsp;</span><span style="color: #ee2323;">perform</span>?"</b><br /><br /></b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>The problem of gradients vanishing&nbsp; was solved.<br />The models with extremely deep layers, started to learn anyway.</li>
<li>However, the Degradation problem was observed.<br /><br />
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>it was a phenomenon in which as the depth of the neural network deepened, the accuracy starts to "saturate".<br /><br /></li>
<li>Because the "Training error" increased when network be deepened, it was not due to overfitting.</li>
</ul>
</li>
</ul>
</li>
</ul>
<p>[##_Image|kage@VVKcp/btrRFfY2G2F/1Zh6uoDUozGkEf2sRTuhck/img.png|CDM|1.3|{"originWidth":1098,"originHeight":430,"style":"alignCenter","width":500,"height":196,"caption":"Let's take a look at the left of Figure 1. As the layer be deepened, the training error increased. As shown on the right, the test error also increased."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20"><b>So what on earth is the problem ?</b></h4>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h3 data-ke-size="size23"><b>The 4th paragraph in Introduction</b></h3>
<p>[##_Image|kage@vHKVP/btrREVl0OM7/eo7OLW1iWUpdVlYpWzxKD0/img.png|CDM|1.3|{"originWidth":670,"originHeight":394,"style":"floatRight","width":500,"height":294}_##]</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Explains which experiements they have conducted to explore problems.<br /><br /></li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@bDcdLw/btrRGwTMdae/cUr66vjT6t3ie59tIBU4vK/img.png|CDM|1.3|{"originWidth":816,"originHeight":126,"style":"alignCenter","caption":"Source : https://developer.nvidia.com/discover/artificial-neural-network"}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Suppose there are two FCNNs</b> that have learned that the figure shown in the above is <b>"Sara"</b>.</p>
<p data-ke-size="size16"><b>One of them has learned Sara</b> image with the following architecture.&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@bCzDKo/btrRCZPVSZX/gKiT9kY9HKv4Vg6eeRgSi0/img.png|CDM|1.3|{"originWidth":1804,"originHeight":464,"style":"alignCenter","caption":"Draw neural network on https://alexlenail.me/NN-SVG/index.html"}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">Then, <b>copy the <span style="color: #ee2323;">learned</span> neural network and add some layers</b> to the top (near output layer) .</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@bGxy2N/btrRDUHN7XF/3XZgt92bKHvtxbNbpdsnUK/img.png|CDM|1.3|{"originWidth":1852,"originHeight":467,"style":"alignCenter","caption":"Draw neural network on https://alexlenail.me/NN-SVG/index.html"}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">Ideally, it would be nice if each added layer works as identity mapping.<br />(Identity mapping : A layer that should approximate Identity Function.)</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">In other words, <b><span style="color: #ee2323;"><span style="color: #000000;">it would be very nice if</span> each added layer was optimized as a layer that approximates the identity function.</span></b></p>
<p data-ke-size="size16">(Identity function is a function that print out inputs as an output.)</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>If so, this "Deeper" neural network will still be able to correctly infer Sara.</b></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">If the added layers successfully approximated the identity function,</p>
<p data-ke-size="size16">The <b><span style="color: #ee2323;">"Deeper"</span> neural network should perform <span style="color: #ee2323;">better, or at least</span>&nbsp;simillar than the "Shallower"</b> neural network.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">However, <b>the results showed "Deeper" network performed worse.</b></p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@VVKcp/btrRFfY2G2F/1Zh6uoDUozGkEf2sRTuhck/img.png|CDM|1.3|{"originWidth":1098,"originHeight":430,"style":"alignCenter","width":500,"height":196,"caption":"Let's take a look at the left of Figure 1. As the layer be deepened, the training error increased. As shown on the right, the test error also increased."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">Therefore, this is a problem with the difficulty of optimization of deep neural networks.</span></p>
<p data-ke-size="size16"><b><span style="background-color: #fdfdfd; color: #000000;">It is a very fundamental problem.</span></b><br /><span style="background-color: #fdfdfd; color: #000000;">It's not just a matter of overfitting.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">(In fact, it is not easy for neural network layers to approximate the Identity Function.</span><br /><br /><span style="background-color: #fdfdfd; color: #000000;">Perhaps, the added layers might approximate Zero Function rather than the identity function.</span><br /><br /><span style="background-color: #fdfdfd; color: #000000;">This is because, I<span style="background-color: #fdfdfd; color: #000000;">n the first place,</span><span>&nbsp;</span>the weights flowing through the deep neural network have the property of approaching "0".)</span><br /><br /><br /><span style="background-color: #fdfdfd; color: #000000;">So, how can we reduce the difficulty of optimization?</span></p>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23"><b>The 5th paragraph in Introduction</b></h3>
<p>[##_Image|kage@bLvM2E/btrRDVT6HZ7/j0uK6LKoe4D2y9FUp6T8B0/img.png|CDM|1.3|{"originWidth":616,"originHeight":396,"style":"floatRight","width":450,"height":289}_##]</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="background-color: #fdfdfd; color: #000000;">Suggest ways to reduce the difficulty of optimization</span><br />
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Residual Mapping</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23"><b>The 6th paragraph In Introduction</b></h3>
<p>[##_Image|kage@4a8P3/btrRGkMEn6N/cM3f4YCkGprjbebX7gl6a0/img.png|CDM|1.3|{"originWidth":578,"originHeight":312,"style":"floatRight","width":450,"height":243}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Explains Shorcut Connections</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">Befor we get into the heart of this paper,<span>&nbsp;</span><b><span style="background-color: #fdfdfd; color: #000000;">There is something to point out.</span></b></p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">It's the definition of a <b>function</b>.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">Function is an expression, rule, or law that defines a relationship between one variable and another variable.</p>
<p data-ke-size="size16">For a certain input, function must print output in a consistent way.</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@s0ztW/btrRDYQMLl0/2shuVPMx3x2wodv3Pi2w6k/img.png|CDM|1.3|{"originWidth":340,"originHeight":306,"style":"alignCenter"}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">Let's look at the picture above.</span></p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">There is a function H that print Output H(x) for Input X.</span></p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">If the output of this function "H(x)" is equal to "x", then we can say the function H is the Identity Function.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>"Approximating<span style="color: #ee2323;"> Identity function</span>"</b> is equal to <b>"Approximating <span style="color: #ee2323;">the function H that makes H(x) = x.</span>"</b></p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">The problem is that, as mentioned above, it is not easy for neural network layers to approximate the Identity Function.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">But what if we could learn H(x) - x instead of H?</span></p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">(Let's H(x) - x = F(x) ).</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">Instead of learning "Ideal" H(x), The models learn "the gap between ideal and reality" H(x)-x, Residual.</span></p>
<div id="txtTarget"><span>Let's change Figure 2 a little by referring to the picture above.</span></div>
<p>[##_Image|kage@dTK9Z2/btrRGmwTwXV/r6PBTW3ynIsqlpdiKV5gtK/img.png|CDM|1.3|{"originWidth":1444,"originHeight":536,"style":"alignCenter","caption":"Ccovered the picture in Figure 2 with a blue box. That blue box represents the function H."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">The function H in that blue box will represent F(x) + x.</span><br /><br /><span style="background-color: #fdfdfd; color: #000000;">Let's remove the blue box.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@xxurB/btrRBfTuSpB/hAEr8BaBOtEA8Plkx15oK1/img.png|CDM|1.3|{"originWidth":1162,"originHeight":465,"style":"alignCenter","caption":"H(x) = 2 weight layers + Shortcut Connections"}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">The <b>function F</b> consists of <b>"Convolution operation - ReLu activation function operation - Convolution operation".</b></span><br /><br /><span style="background-color: #fdfdfd; color: #000000;">The <b>function H</b> consists of <b>"Convolution operation - ReLu activation function operation - Convolution operation - <span style="color: #ee2323;">An o<span style="background-color: #fdfdfd;">peration of adding Input x to F(x)</span></span>".</b></span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">In this case, <span style="color: #ee2323;"><b>"an operation of adding Input x to F(x)"</b></span> is just a <b><span style="color: #ee2323;">"command"</span></b> <b>in which a parameter to be learned does not exist.</b></span></p>
<p data-ke-size="size16"><br /><b><span style="background-color: #fdfdfd; color: #000000;">It's just a "command" to add Input x.</span></b></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="background-color: #fdfdfd; color: #000000;">This can achieve three.</span></b></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;"><b>1.</b><span>&nbsp;</span>When updating parameters, we learn function F, not function H.</span><br /><br /><span style="background-color: #fdfdfd; color: #000000;">This is because, at "H = F(x)<span>&nbsp;</span><span style="color: #ee2323;">+ x<span style="color: #000000;">"</span></span>,<span> "</span><span style="color: #ee2323;">+ x<span style="color: #000000;">"</span></span><span>&nbsp;</span>has no parameter to learn.</span><br /><br /><span style="background-color: #fdfdfd; color: #000000;">The function F = H - x.</span><br /><br /><span style="background-color: #fdfdfd; color: #000000;"><b>Without additional parameters to be learned, Residual,</b><span>&nbsp;</span>the gap between ideal and reality,<span>&nbsp;</span><b>is learned.</b></span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>2.<span>&nbsp;</span></b><span style="background-color: #fdfdfd; color: #000000;">It becomes easier for function H to approximate the Identity Function.</span><br /><span style="background-color: #fdfdfd; color: #000000;">Since the function H = F(x) + x, if F(x) becomes 0, then H = 0 + x = x and H(x) = x.</span></p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">That is, <b>if</b> function <b>F approximates Zero Function,</b> function <b>H become Identity Function.</b></span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">It is relatively easy to approximate the Zero Function because all the necessary parameters need to be zero.</span><br /><span style="background-color: #fdfdfd; color: #000000;">(Same whether it's FCNN or CNN. All operations only consists of multiplying and adding.)</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">In addition, Zero Function is easy to approximate because the weights flowing through the deep neural network have the property of approaching zero.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>3.</b><span>&nbsp;</span>Because t<span style="background-color: #fdfdfd; color: #000000;">here are no additional parameters to learn,</span><br /><span style="background-color: #fdfdfd; color: #000000;">A fair comparison between</span><br /><b><span style="background-color: #fdfdfd; color: #000000;">"Plain Networks" without Residual Connections</span></b><br /><b><span style="background-color: #fdfdfd; color: #000000;">"Residual Networks" with Residual Connections</span></b><br /><span style="background-color: #fdfdfd; color: #000000;">can be made.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h3 data-ke-size="size23"><b>The 7th ~ 9th paragraph in Introduction</b></h3>
<p>[##_Image|kage@P7Hqt/btrRGwTMdlH/IcQ9akbNiYF0GyismkkuG0/img.png|CDM|1.3|{"originWidth":606,"originHeight":816,"style":"floatRight","width":450,"height":606}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">The results of experiements with ResNet are summarized.</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="color: #ee2323;">With ResNet, even when the depth was extremely increased, it was easy to optimize.&nbsp;</span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Remember? Deeper plain net increased training error unexpectedly.<span style="font-family: -apple-system, BlinkMacSystemFont, 'Helvetica Neue', 'Apple SD Gothic Neo', Arial, sans-serif; letter-spacing: 0px; color: #000000;"><br /></span></li>
</ul>
</li>
<li>
<div><span style="color: #ff0000;">The deeper the depth, The higher the accuracy.</span></div>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>
<div><span style="color: #000000;">ResNet has recorded the best accuracy among the state-of-the-art networks.</span><span style="color: #000000;"><br /><br /></span></div>
</li>
</ul>
</li>
<li>
<div><span style="color: #000000;">The results of experiements be consistent whether it's on ImageNet dataset or CIFAR-10 dataset.</span></div>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>
<div><span style="color: #000000;">This result is not only for a certain dataset.<br /><br /></span></div>
</li>
</ul>
</li>
<li>
<div><span style="color: #000000;"><span style="background-color: #fdfdfd; color: #000000;">With 152 layers of incredible depth, ResNet is the highest ever, but fewer parameters to learn than<span>&nbsp;</span></span>VGG net.</span></div>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>
<div><span style="color: #000000;">Thans to Shortcut Connections</span><span style="color: #000000;"><br /><br /></span></div>
</li>
</ul>
</li>
<li>
<div><span style="color: #000000;">ResNet</span><span style="color: #000000;"><span>&nbsp;</span>has won the following competitions.</span></div>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>
<div><span style="color: #000000;">ImageNet detection in ILSVRC 2015</span></div>
</li>
<li>
<div><span style="color: #000000;">ImageNet localization in ILSVRC 2015</span></div>
</li>
<li>
<div><span style="color: #000000;">COCO detection in COCO 2015</span></div>
</li>
<li>
<div><span style="color: #000000;">COCO segmentation in COCO 2015</span></div>
</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">Let's look into details in Figures and Tables.</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h3 data-ke-size="size23"><b>Figure 3</b></h3>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;"><b>Figure 3</b> visualizes t<b>he network architectures</b> used in the experiment at a glance <b>with VGG-19.</b></span></p>
<p>[##_Image|kage@wiXUn/btrRBMDlTiB/zCUgu79W4p1lLLp1YkRHr0/img.png|CDM|1.3|{"originWidth":690,"originHeight":1042,"style":"floatRight","width":550,"height":831}_##]</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="color: #ff0000; font-family: -apple-system, BlinkMacSystemFont, 'Helvetica Neue', 'Apple SD Gothic Neo', Arial, sans-serif; letter-spacing: 0px;">Plain Network</span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="color: #000000;"><span style="background-color: #fdfdfd; color: #000000;">If the feature map size has been halved,<br /></span><span style="background-color: #fdfdfd; color: #000000;">The number of filters should be doubled to preserve the "time complexity" of each layer.</span>&nbsp;<br />(Inspired by VGG philosophy)<br /><br /></span><span style="color: #a6a6a6; font-family: -apple-system, BlinkMacSystemFont, 'Helvetica Neue', 'Apple SD Gothic Neo', Arial, sans-serif; letter-spacing: 0px;">The time complexity of an algorithm is the number of basic operations, such as multiplications and summations, that the algorithm performs.</span></li>
</ul>
</li>
</ul>
<div><span style="color: #a6a6a6;">&nbsp;</span></div>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="color: #ff0000;">Residual Network<span>&nbsp;</span></span><span style="color: #000000;">= Plain Network +<span>&nbsp;</span></span><span style="color: #0070c0;">Shortcuts</span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Dimension Staying Shortcuts : Identity Shortcuts</li>
<li>Dimension Increasing Shortcuts
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>When convolve with stride of 2, <span style="color: #000000;">Height<span> and</span></span><span style="color: #000000;"><span>&nbsp;</span></span><span style="color: #000000;">Width<span> decreased</span></span><span style="color: #000000;">,<br />Channel<span> numbers increased.</span></span><span style="color: #000000;"><br /><br /></span></li>
<li><span style="color: #000000;">For operations of </span><span style="color: #000000;">F(x) + x, <br />F(x) and x should have same dimensions.</span><span style="color: #000000;"><br /></span>&rarr;<span> Adjust the dimensions to be identical.</span><span style="color: #000000;"><br /><br /></span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Zero padding shortcuts</li>
<li>Projection shortcuts</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h3 data-ke-size="size23"><b>Table 1</b></h3>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;"><b>Table 1</b> summarizes the <b>architectures</b> of ResNet models used in experiments on ImageNet Dataset <b>according to layer depth.</b></span></p>
<p>[##_Image|kage@brUTVV/btrREWd9nYm/5vcbWpcOXGsKwWbU5kCGfK/img.png|CDM|1.3|{"originWidth":944,"originHeight":412,"style":"alignCenter","caption":"Table 1. Architectures for ImageNet. Building blocks are shown in brackets (see also Fig. 5), with the numbers of blocks stacked. Downsampling is performed by conv3 1, conv4 1, and conv5 1 with a stride of 2."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">When entering every convX_x layer, dimension be downsampled by stride 2 convolution.</p>
<p data-ke-size="size16">(Refer to the architecture of the 34-layer residual in Figure 3.)</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">However, if you look closely at Table 1, there is something strange.</span><br /><br /><span style="background-color: #fdfdfd; color: #000000;">Whether conv2_x or conv3_x, output size is maintained in the convolution operation.</span><br /><br /><span style="background-color: #fdfdfd; color: #000000;">Looking at the Pytorch source code, as expected, there was an appropriate number of padding per convolution layer.</span></p>
<p>[##_Image|kage@s4MIq/btrRA9yHl9S/L6e29FEVni4UmGMyVP0f90/img.png|CDM|1.3|{"originWidth":614,"originHeight":298,"style":"alignCenter","caption":"looking into the source code of ResNet in Pytorch, padding is performed once in 3x3 convolution within a block."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">Modified Table 1 with padding times information.</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@dsGCtZ/btrREV7zrbr/Nk0cu2Y4ih1q3bfLjECNr0/img.png|CDM|1.3|{"originWidth":688,"originHeight":315,"style":"alignCenter","caption":"Modified Table 1 with padding times information."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h3 data-ke-size="size23"><b>Table 2</b></h3>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Table 2</b><span> summarizes <b>validation error</b> after learning </span><b>ImageNet 2012 Classification Dataset.</b></p>
<p>[##_Image|kage@Fb81V/btrRCZbuMcr/Q5zr8fHXQShfS896SriFTk/img.png|CDM|1.3|{"originWidth":499,"originHeight":251,"style":"floatRight"}_##]</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>ImageNet 2012 Classification Dataset
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>1,000 classes</li>
<li>128 millions Training set</li>
<li>5 millions Validation set<br /><br /></li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>Results</b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>the deeper the Plain net,</b><span> the higher the error</span></li>
<li><b>the deeper the ResNet, the lower the error</b></li>
</ul>
</li>
</ul>
<h3 data-ke-size="size23">&nbsp;</h3>
<h3 data-ke-size="size23"><b>Figure 4</b></h3>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Figure 4</b><span> visualizes error transitional curve on </span><b>ImageNet 2012 Classification Dataset.</b></p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@b3jP52/btrRGlLvoEK/HEA8nnklkQW6kKKTVUlhq0/img.png|CDM|1.3|{"originWidth":1251,"originHeight":416,"style":"alignCenter","caption":"Figure 4. Training on ImageNet. Thin curves denote training error, and bold curves denote validation error of the center crops. Left: plain networks of 18 and 34 layers. Right: ResNets of 18 and 34 layers. In this plot, the residual networks have no extra parameter compared to their plain counterparts."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>The authors suggests that the error increase when deepening the Plain net is not due to gradients vanishing.<br /><br />
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Already applied methods which have solved gradients vanishing.</li>
<li>If it is due to gradients vanishing, learning should not have been achieved.<br />
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>But as you see, Plain-34 has competitive accuracy.</li>
<li>It means, learning is being achieved to some degree.</li>
</ul>
</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">Let's summarize Table 2 and Figure 4.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@bKRaR5/btrRACVEdGx/G2rhyKAWL0jzR4inyb0os0/img.png|CDM|1.3|{"originWidth":1368,"originHeight":367,"style":"alignCenter"}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>Degradation problem</b><span> can be solved with</span><span>&nbsp;</span><b>Residual Learning</b>.
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>When ResNet<span style="color: #000000;"><span> be deepened</span></span></b><span style="color: #000000;">,<span>&nbsp;</span><b>Training error<span> and </span></b></span><b><span style="color: #000000;">Validation error<span> decreased.</span></span></b><span style="color: #000000;"><br /><br /></span></li>
</ul>
</li>
<li><b>Verified effects of Residual Learning in Deep&nbsp;<span style="color: #000000;">Neural Networks.</span></b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b><span style="color: #000000;">ResNet-34 decreased</span><span style="color: #000000;"><span>&nbsp;</span></span><span style="color: #000000;">error</span><span style="color: #000000;"><span>&nbsp;</span></span><span style="color: #000000;">3.5% compared to Plain-34</span></b><span style="color: #000000;"><br /><br /></span></li>
</ul>
</li>
<li><b><span style="color: #000000;"><span style="color: #000000;">ResNet optimize much faster than Plain net.</span></span></b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="color: #000000;">If Neural Network is not very deep, Plain net performs quite good.</span><span style="color: #000000;"> (</span><span style="color: #000000;">27.94</span><span style="color: #000000;"><span>&nbsp;</span>vs 27.88)</span></li>
<li><span>But you should still use </span><b><span style="color: #000000;">ResNet</span><span style="color: #000000;">. It optimizes very fast.&nbsp;</span></b></li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h3 data-ke-size="size23"><b>Table 3 ~ 5</b></h3>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">With dimension increasing shortcut connections,</p>
<p data-ke-size="size16">Used 2 methods to make the dimensions be same.(Refer to Figure 3 explanation)</p>
<p>[##_Image|kage@nLcGl/btrRAhRDHVT/cZMVbcFKfjEUIpykMtBkeK/img.png|CDM|1.3|{"originWidth":794,"originHeight":1051,"style":"floatRight","width":450,"height":596}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Zero padding shortcuts : Add channels which have "0" values.
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>No parameters to be learned.<br /><br /></li>
</ul>
</li>
<li>Projection shortcuts : 1x1 convolution for doubling filter numbers&nbsp;
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>There are parameters to be learned.</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Table 3</b><span> summarized validation errors with the above two methods in various combinations on</span><span>&nbsp;</span><b>Dimension Increasing Shortcuts and Dimension Staying Shortcuts.</b></p>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style7" />
<p data-ke-size="size16">Let's look into the<b> middle part of Table 3.</b></p>
<p data-ke-size="size16">Compared Plain net and ResNet-34 with A/B/C options.</p>
<p>[##_Image|kage@dGBuyC/btrRAMqhWAT/KTeLnXrtd5xwCKcCKoSdek/img.png|CDM|1.3|{"originWidth":604,"originHeight":440,"style":"alignCenter"}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>Option<span>&nbsp;</span><span style="color: #ee2323;">A</span></b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Dimension<span>&nbsp;</span><span style="color: #000000;">Increasing</span><span style="color: #000000;"><span>&nbsp;</span>Shortcuts :<span> use </span></span><span style="color: #000000;">Zero padding</span><span style="color: #000000;"><span>&nbsp;</span>shortcuts</span></li>
<li>Dimension<span>&nbsp;</span><span style="color: #000000;">Staying</span><span style="color: #000000;"><span>&nbsp;</span>Shortcuts : use<span>&nbsp;</span></span><span style="color: #000000;">Identity shortcuts</span></li>
<li>&rarr; All <span style="color: #000000;">shortcuts<span> have no parameters to be learned.</span></span><span style="color: #000000;"><br /><br /></span></li>
</ul>
</li>
<li><b>Option<span>&nbsp;</span><span style="color: #ee2323;">B</span></b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Dimension<span>&nbsp;</span><span style="color: #000000;">Increasing</span><span style="color: #000000;"><span>&nbsp;</span>Shortcuts :<span> use </span></span><span style="color: #000000;">projection shortcuts</span></li>
<li>Dimension<span>&nbsp;</span><span style="color: #000000;">Staying</span><span style="color: #000000;"><span>&nbsp;</span>Shortcuts :<span> use </span></span><span style="color: #000000;">Identity shortcuts</span></li>
<li>&rarr;<span>&nbsp;</span><span style="color: #000000;">Dimension Increasing Shortcuts introduce parameters to be learned.</span><span style="color: #000000;"><br /><br /></span></li>
</ul>
</li>
<li><b>Option<span>&nbsp;</span><span style="color: #ee2323;">C</span></b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Dimension<span>&nbsp;</span><span style="color: #000000;">Increasing</span><span style="color: #000000;"><span>&nbsp;</span>Shortcuts :<span> use </span></span><span style="color: #000000;">projection shortcuts</span></li>
<li>Dimension<span>&nbsp;</span><span style="color: #000000;">Staying</span><span style="color: #000000;"><span>&nbsp;</span>Shortcuts :<span> use </span></span><span style="color: #000000;">projection shortcuts</span></li>
<li>&rarr; All<span>&nbsp;</span><span style="color: #000000;">Shortcuts<span> introduce parameters to be learned.</span></span></li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size18"><b><b>summarize </b>the middle part of Table 3 :</b></p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>With any options, Better performance than plain-34.</b></li>
<li>With B<span> option is better than with </span><span style="color: #000000;"><span>&nbsp;</span></span><span style="color: #000000;">A.</span><span style="color: #000000;"><br /></span><b>Because, with option A,<span style="color: #000000;"><span>&nbsp;</span></span><span style="color: #000000;">residual learning<span> isn't achieved in <b>zero padded channels.</b></span></span></b><span style="color: #000000;"><br /></span></li>
<li><span style="color: #000000;">Insignificant differences between A/B/C<span style="color: #000000;">&nbsp;</span></span><span style="color: #000000;">&rarr;<span> </span></span><span style="color: #ee2323;"><b>Projection shortcuts are not essential to solve degradation problem.</b></span><span style="color: #000000;"><br /></span></li>
<li><b>Used economic option B in the left experiments.</b></li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style7" />
<p data-ke-size="size16"><span style="color: #000000;">Let's look into <b>the bottom of Table 3.</b></span></p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@CXrlt/btrRAhqwSBv/JiSy0DkBUD3BuHHP2Rnsm0/img.png|CDM|1.3|{"originWidth":604,"originHeight":440,"style":"alignCenter"}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">ResNets with more layers than 34 were also tested.</p>
<p data-ke-size="size16">However, there were too many parameters to use the building block as it was.</p>
<p data-ke-size="size16">So, ResNet-50, ResNet-101, ResNet-152 use new building blocks.</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@mgwCy/btrRGxkPyWu/k64yMFeWd4sRUvtDA9Loik/img.png|CDM|1.3|{"originWidth":629,"originHeight":341,"style":"alignCenter"}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">Looking at the picture on the right side of Figure 5, "bottleneck" building block is shown.</span></p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">In the bottomleneck block, the number of channels is reduced by the first 1x1 convolution.</span></p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">It then goes through 3x3 convolution.</span></p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">As the 1x1 convolution is performed again, the number of channels is recovered.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<div id="txtTarget"><span>I compared the number of learning parameters because I was curious if the Bottleneck building block was really efficient.</span></div>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@qkhun/btrRAhxj5or/pPbbjUMr1O2QoIeKYnzpkK/img.png|CDM|1.3|{"originWidth":1283,"originHeight":591,"style":"alignCenter"}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<div id="txtTarget"><span>Certainly, <br />the number of parameters of the botleneck building block in the blue box is less than that of the building block in the red box, <br />so the operation will be efficient.</span></div>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style7" />
<p data-ke-size="size16">summarizes the bottom of Table 3&nbsp; + Table 4 + Table 5 :</p>
<p>[##_Image|kage@dYjkF4/btrRAipsoRu/a6ib9tfvBcxMriwqbjMKQK/img.png|CDM|1.3|{"originWidth":1192,"originHeight":302,"style":"alignCenter","caption":"Table 3, 4, 5"}_##]</p>
<div>&nbsp;</div>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>the bottom of Table 3
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="color: #ee2323;">Even extremely deep ResNet</span><span> learns well.</span></li>
<li><span style="color: #ee2323;">The deeper the ResNet, The lower the error.</span><br /><br /></li>
</ul>
</li>
<li>Table 4
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="color: #ee2323;">ResNet-34</span><span style="letter-spacing: 0px; color: #000000;"><span> has beaten all state-of-the-art deep learning models.</span></span></li>
<li><span style="color: #ff0000;">Single model ResNet-152</span><span style="color: #000000;"><span> has beaten all state-of-the-art deep learning ensemble models.</span></span><span style="color: #ff0000;"><br /><br /></span></li>
</ul>
</li>
<li><span style="letter-spacing: 0px; color: #000000;">Table 5</span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Made a<span style="color: #000000;"><span>&nbsp;</span></span><span style="color: #ff0000;">ResNet</span><span style="color: #ff0000;"><span>&nbsp;</span>Ensemble</span><span style="color: #000000;"><span>&nbsp;</span></span><span style="color: #000000;">with 6 different ResNets.</span></li>
<li>Won <span style="color: #ff0000;">2015 ILSVRC <span style="color: #000000;">with</span> </span>Top-5 error<span>&nbsp;</span><span style="color: #ff0000;">3.57%<span> </span></span><span style="color: #000000;">(Improved existing error 26%.</span><span style="color: #000000;">)</span></li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h3 data-ke-size="size23"><b>Table 6</b></h3>
<p data-ke-size="size16"><b>Experiments were conducted on CIFAR-10 Dataset to show that ResNet is not limited to a certain dataset.</b></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">The authors conducted experiments with CIFAR-10 Dataset with "simple architectures" on purpose.</p>
<p data-ke-size="size16">It was in order to focus on analyzing movement of extremely deep neural networks rather than produce good results.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">A figure summarizing the "simple architecture" used for learning CIFAR-10 Dataset is inserted in the paper.</span></p>
<p>[##_Image|kage@opjpW/btrRFfdFPay/jYIXLktE7AClYlrVEErmk0/img.png|CDM|1.3|{"originWidth":573,"originHeight":131,"style":"alignCenter","width":450,"height":103,"caption":"Conducted experiments on CIFAR-10 with simple ResNet like the above."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">With the above picture, couldn't have a good grasp, so I draw following table.</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@b0kPs1/btrRHCTOgoz/lFg8xZfHBXd583EzhTMUtK/img.png|CDM|1.3|{"originWidth":1470,"originHeight":310,"style":"alignCenter","caption":"Conducted experiments on CIFAR-10 with simple ResNet like the above."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">The result is following.</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@1evUW/btrRBe7VJ93/F37SAWKv5u25Bf3JahKwA1/img.png|CDM|1.3|{"originWidth":581,"originHeight":521,"style":"alignCenter"}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Table 6</b></p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>ResNet has beaten FitNet and Highway, the existing best Classification models</li>
<li><b>ResNet performs better with much fewer parameters.</b></li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">Q. By the way, Table 6 shows data augmentation be conducted.</p>
<p data-ke-size="size16">FitNet and Highway was learned with data augmentation, as well ?</p>
<p data-ke-size="size16"><span style="color: #000000;">&rarr; Reviewing those models' papers, It was. However, </span><span style="color: #000000;">augmentation<span> mothods differ.</span></span></p>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h3 data-ke-size="size23"><b>Figure 6</b></h3>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style7" />
<p data-ke-size="size16">Let's look into the left of Figure 6.</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@lkWrh/btrRGv8qSuw/fpvvk29rBfLcpmKkalimSk/img.png|CDM|1.3|{"originWidth":1820,"originHeight":488,"style":"alignCenter","caption":"Figure 6. Training on CIFAR-10. Dashed lines denote training error, and bold lines denote testing error. Left: plain networks. The error of plain-110 is higher than 60% and not displayed. Middle: ResNets. Right: ResNets with 110 and 1202 layers."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">The following conclusions can be drawn through the left picture of Figure 6, the left picture of Figure 4, and the existing paper.</span></p>
<h3 data-ke-size="size23"><i><b>"<span style="background-color: #fdfdfd; color: #000000;">"The optimization difficulity of deep neural networks is a FUNDAMENTAL problem."</span></b></i></h3>
<h3 data-ke-size="size23">(<span style="background-color: #fdfdfd; color: #000000;">It's not a matter of overfitting</span>.)</h3>
<p>[##_Image|kage@CFSxn/btrRBKMke1b/eJYWh4SVmsfBS2lb8uPEZ0/img.png|CDM|1.3|{"originWidth":366,"originHeight":302,"style":"floatRight"}_##]</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>the left of Figure 6
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="background-color: #fdfdfd; color: #000000;">The deep plain-net "suffers" from the increased depth, and the training error increases as the depth increases.</span><br /><br /></li>
</ul>
</li>
<li>the left of Figure 4
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>For ImageNet Dataset, <br />it was observed that the training error increases as the depth increases.<br /><br /></li>
</ul>
</li>
<li><span style="background-color: #fdfdfd; color: #000000;">Similar observations have been reported with MNIST dataset.</span><br />
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><i>R. K. Srivastava, K. Greff, and J. Schmidhuber. Highway networks. arXiv:1505.00387, 2015.</i></li>
</ul>
</li>
</ul>
<div id="txtTarget">&nbsp;</div>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style7" />
<p data-ke-size="size16"><span>The following conclusions can be drawn through the picture in the middle of Figure 6 and the picture on the right of Figure 4.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@bRYiBh/btrREVGi5xJ/r1rufvCeNM0mcPV946jsgk/img.png|CDM|1.3|{"originWidth":1819,"originHeight":488,"style":"alignCenter","caption":"Figure 6. Training on CIFAR-10. Dashed lines denote training error, and bold lines denote testing error. Left: plain networks. The error of plain-110 is higher than 60% and not displayed. Middle: ResNets. Right: ResNets with 110 and 1202 layers."}_##]</p>
<h3 data-ke-size="size23">&nbsp;</h3>
<h3 data-ke-size="size23"><i><b>"ResNet has overcome the optimization difficulity. Accuracy increased when depth increased."</b></i></h3>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@cDTcsF/btrRGmjl4Tr/LnmyOx5VDoBqAxN2fXkQ70/img.png|CDM|1.3|{"originWidth":365,"originHeight":300,"style":"floatRight"}_##]</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>the middel of Figure 6
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>As depth increased in ResNet, Training error and Testing error decreased.</li>
</ul>
</li>
<li>the right of Figure 4
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>Similar observations have been made with ImageNet dataset.</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style7" />
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span>Thereafter, the ResNet model with 1202 layers was evaluated by setting n = 200.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@O1umb/btrRHA9vvBp/4ya0AmdPKiPKXLFLhQzRM1/img.png|CDM|1.3|{"originWidth":1821,"originHeight":482,"style":"alignCenter","caption":"Figure 6. Training on CIFAR-10. Dashed lines denote training error, and bold lines denote testing error. Left: plain networks. The error of plain-110 is higher than 60% and not displayed. Middle: ResNets. Right: ResNets with 110 and 1202 layers."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;"><b>The test error of ResNet-1202</b> was 7.93%, <b>higher than that of ResNet-110.</b></span></p>
<p data-ke-size="size16"><span style="color: #ee2323;"><b><span style="background-color: #fdfdfd;">The authors argue that this may be due to overfitting.</span></b></span></p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">Because, although the test error is high, the training error of ResNet-1202 is similar to that of ResNet-110.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">The authors speculate that <b>ResNet-1202 would be a "unnecessarily" large model to train small datasets such as CIFAR-10.</b></span></p>
<p data-ke-size="size16">&nbsp;</p>
<div id="txtTarget"><span>It is also mentioned that follow-up research will be conducted by applying a Regularization technique such as Dropout.</span></div>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h3 data-ke-size="size23"><b>Figure 7</b></h3>
<p>[##_Image|kage@dzMy9x/btrRAiwe8x9/kw1QLOZCvQ9lGd97S102d1/img.png|CDM|1.3|{"originWidth":967,"originHeight":532,"style":"alignCenter","caption":"Figure 7. Standard deviations (std) of layer responses on CIFAR10. The responses are the outputs of each 3&amp;times;3 layer, after BN and before nonlinearity. Top: the layers are shown in their original order. Bottom: the responses are ranked in descending order."}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">Figure 7 is a graph of the standard deviation of outputs for each layer according to the layer index.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="background-color: #fdfdfd; color: #000000;">Since <b>ResNet learns residual</b>, or "the gap between ideal and reality",<br />the authors say i</span><span style="background-color: #fdfdfd; color: #000000;">t was expected that there would be <b>smaller layer responses than Plain-net.</b></span><br /><br /><span style="background-color: #fdfdfd; color: #000000;"><b>Figure 7 supports</b> such expectations.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<p style="position: absolute;" data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23"><b>Table 7, 8</b></h3>
<p data-ke-size="size16">&nbsp;</p>
<p>[##_Image|kage@wgfUX/btrRCYXZJWx/WVAFuxATMJugbiakvHw7sK/img.png|CDM|1.3|{"originWidth":952,"originHeight":572,"style":"alignCenter"}_##]</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<div id="txtTarget"><span>Tables 7 and 8 show the results of experiments with ResNet on the Object Detection task, not the Image Classification task.</span></div>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<p data-ke-size="size16"><span>Lastly, the authors wrap up this paper emphasizing on the excellence of ResNet, revealing that ResNet has won the following competitions.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>ImageNet detection in ILSVRC 2015</li>
<li>ImageNet localization in ILSVRC 2015</li>
<li>COCO detection in COCO 2015</li>
<li>COCO segmentation in COCO 2015</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
