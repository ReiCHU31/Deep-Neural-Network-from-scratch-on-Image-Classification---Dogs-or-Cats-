# Deep Neural Network from scratch on Image Classification - Dogs or Cats?

## **Phuong T.M. Chu and Hai Nguyen**

**Deep Neural Network from scratch on Image Classification - Dogs or Cats?** is the project that we finished after the 5th week of studying **Machine Learning**.

<p align="center">
  <img width="460" height="300" src="https://storage.googleapis.com/kaggle-competitions/kaggle/3362/media/woof_meow.jpg">
</p>

## INTRODUCTION
**Dogs vs. Cats** [dataset](https://www.kaggle.com/c/dogs-vs-cats/data) provided by  Microsoft Research contains 25,000 images of dogs and cats with the labels 
* 1 = dog
* 0 = cat 

### Project goals:
1. Building a basic **deep neural network from scratch** to classify dogs and cats images

2. **Tunning the hyperparameters** of the model in order to achieve high accuracy. This project explores the applicability of deep neural network by tunning these hyperparameters:
    * Learning rate
    * Number of hidden layers
    * Number of nodes in each hiden layers
    * Number of iterations

## BUILDING DEEP NEURAL NETWORK FROM SCRATCH

In this notebook, we implemented all the functions required to build a deep neural network.
![](https://i.imgur.com/ivhZhmx.png)

**Notation**:
- Superscript <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$[l]$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$[l]$" title="\large $[l]$" /></a> denotes a quantity associated with the <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;l^{th}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;l^{th}$" title="\large $ l^{th}$" /></a> layer. 
    - Example: <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;a^{[L]}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;a^{[L]}$" title="\large $ a^{[L]}$" /></a> is the <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;L^{th}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;L^{th}$" title="\large $ L^{th}$" /></a> layer activation. <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;W^{[L]}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;W^{[L]}$" title="\large $ W^{[L]}$" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;b^{[L]}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;b^{[L]}$" title="\large $ b^{[L]}$" /></a> are the <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;L^{th}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;L^{th}$" title="\large $ L^{th}$" /></a> layer parameters.
- Superscript <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(i)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(i)$" title="\large $(i)$" /></a> denotes a quantity associated with the <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;i^{th}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;i^{th}$" title="\large $ i^{th}$" /></a> example. 
    - Example: <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;x^{(i)}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;x^{(i)}$" title="\large $ x^{(i)}$" /></a> is the <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;i^{th}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;i^{th}$" title="\large $ i^{th}$" /></a> training example.
- Lowerscript <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;i$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;i$" title="\large $ i$" /></a> denotes the <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;i^{th}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;i^{th}$" title="\large $ i^{th}$" /></a> entry of a vector.
    - Example: <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;a^{[l]}_i$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;a^{[l]}_i$" title="\large $ a^{[l]}_i$" /></a> denotes the <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;i^{th}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;i^{th}$" title="\large $ i^{th}$" /></a> entry of the <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;l^{th}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;l^{th}$" title="\large $ l^{th}$" /></a> layer's activations).
    
The initialization for a deeper L-layer neural network is more complicated because there are many more weight matrices and bias vectors. When completing the `initialize_params`, we made sure that our dimensions match between each layer. Given <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;n^{[l]}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;n^{[l]}$" title="\large $ n^{[l]}$" /></a> is the number of units in layer <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;l$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;l$" title="\large $ l$" /></a>. Thus for example if the size of our input <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;X$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;X$" title="\large $ X$" /></a> is <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(12288,&space;209)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(12288,&space;209)$" title="\large $(12288, 209)$" /></a> (with <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;m=209$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;m=209$" title="\large $ m=209$" /></a> examples) then:

| |**Shape of W**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |**Shape of b**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|**Activation**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|**Shape of Activation**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|:-|:-|:-|:-|:-|
|**Layer 1**|<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(n^{[1]},12288)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(n^{[1]},12288)$" title="\large $(n^{[1]},12288)$" /></a>|<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(n^{[1]},1)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(n^{[1]},1)$" title="\large $(n^{[1]},1)$" /></a>|<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;Z^{[1]}&space;=&space;W^{[1]}&space;X&space;&plus;&space;b^{[1]}&space;$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;Z^{[1]}&space;=&space;W^{[1]}&space;X&space;&plus;&space;b^{[1]}&space;$" title="\large $ Z^{[1]} = W^{[1]} X + b^{[1]} $" /></a>|<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(n^{[1]},209)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(n^{[1]},209)$" title="\large $(n^{[1]},209)$" /></a>|
| **Layer 2**|<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(n^{[2]},&space;n^{[1]})$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(n^{[2]},&space;n^{[1]})$" title="\large $(n^{[2]}, n^{[1]})$" /></a>|<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(n^{[2]},1)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(n^{[2]},1)$" title="\large $(n^{[2]},1)$" /></a>|<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;Z^{[2]}&space;=&space;W^{[2]}&space;A^{[1]}&space;&plus;&space;b^{[2]}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;Z^{[2]}&space;=&space;W^{[2]}&space;A^{[1]}&space;&plus;&space;b^{[2]}$" title="\large $ Z^{[2]} = W^{[2]} A^{[1]} + b^{[2]}$" /></a>|<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(n^{[2]},&space;209)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(n^{[2]},&space;209)$" title="\large $(n^{[2]}, 209)$" /></a>|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$\vdots$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$\vdots$" title="\large $\vdots$" /></a>| <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$\vdots$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$\vdots$" title="\large $\vdots$" /></a> | <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$\vdots$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$\vdots$" title="\large $\vdots$" /></a>|<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$\vdots$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$\vdots$" title="\large $\vdots$" /></a>|<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$\vdots$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$\vdots$" title="\large $\vdots$" /></a>|
|**Layer L-1** | <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(n^{[L-1]},&space;n^{[L-2]})$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(n^{[L-1]},&space;n^{[L-2]})$" title="\large $(n^{[L-1]}, n^{[L-2]})$" /></a> | <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(n^{[L-1]},&space;1)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(n^{[L-1]},&space;1)$" title="\large $(n^{[L-1]}, 1)$" /></a> | <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;Z^{[L-1]}&space;=&space;W^{[L-1]}&space;A^{[L-2]}&space;&plus;&space;b^{[L-1]}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;Z^{[L-1]}&space;=&space;W^{[L-1]}&space;A^{[L-2]}&space;&plus;&space;b^{[L-1]}$" title="\large $ Z^{[L-1]} = W^{[L-1]} A^{[L-2]} + b^{[L-1]}$" /></a> | <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(n^{[L-1]},&space;209)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(n^{[L-1]},&space;209)$" title="\large $(n^{[L-1]}, 209)$" /></a>|
|**Layer L** | <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(n^{[L]},&space;n^{[L-1]})$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(n^{[L]},&space;n^{[L-1]})$" title="\large $(n^{[L]}, n^{[L-1]})$" /></a> | <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(n^{[L]},&space;1)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(n^{[L]},&space;1)$" title="\large $(n^{[L]}, 1)$" /></a>|  <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;Z^{[L]}&space;=&space;W^{[L]}&space;A^{[L-1]}&space;&plus;&space;b^{[L]}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;Z^{[L]}&space;=&space;W^{[L]}&space;A^{[L-1]}&space;&plus;&space;b^{[L]}$" title="\large $ Z^{[L]} = W^{[L]} A^{[L-1]} + b^{[L]}$" /></a>|<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(n^{[L]},&space;209)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(n^{[L]},&space;209)$" title="\large $(n^{[L]}, 209)$" /></a> |

Remember that when we compute <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;WX&space;&plus;&space;b$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;WX&space;&plus;&space;b$" title="\large $ WX + b$" /></a> in python, it carries out broadcasting. For example, if: 

<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$$&space;W&space;=&space;\begin{bmatrix}&space;j&space;&&space;k&space;&&space;l\\&space;m&space;&&space;n&space;&&space;o&space;\\&space;p&space;&&space;q&space;&&space;r&space;\end{bmatrix}\;\;\;&space;X&space;=&space;\begin{bmatrix}&space;a&space;&&space;b&space;&&space;c\\&space;d&space;&&space;e&space;&&space;f&space;\\&space;g&space;&&space;h&space;&&space;i&space;\end{bmatrix}&space;\;\;\;&space;b&space;=\begin{bmatrix}&space;s&space;\\&space;t&space;\\&space;u&space;\end{bmatrix}$$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$$&space;W&space;=&space;\begin{bmatrix}&space;j&space;&&space;k&space;&&space;l\\&space;m&space;&&space;n&space;&&space;o&space;\\&space;p&space;&&space;q&space;&&space;r&space;\end{bmatrix}\;\;\;&space;X&space;=&space;\begin{bmatrix}&space;a&space;&&space;b&space;&&space;c\\&space;d&space;&&space;e&space;&&space;f&space;\\&space;g&space;&&space;h&space;&&space;i&space;\end{bmatrix}&space;\;\;\;&space;b&space;=\begin{bmatrix}&space;s&space;\\&space;t&space;\\&space;u&space;\end{bmatrix}$$" title="\large $$ W = \begin{bmatrix} j & k & l\\ m & n & o \\ p & q & r \end{bmatrix}\;\;\; X = \begin{bmatrix} a & b & c\\ d & e & f \\ g & h & i \end{bmatrix} \;\;\; b =\begin{bmatrix} s \\ t \\ u \end{bmatrix}$$" /></a>

Then <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;WX&space;&plus;&space;b$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;WX&space;&plus;&space;b$" title="\large $ WX + b$" /></a> will be:

<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$$&space;WX&space;&plus;&space;b&space;=&space;\begin{bmatrix}&space;(ja&space;&plus;&space;kd&space;&plus;&space;lg)&space;&plus;&space;s&space;&&space;(jb&space;&plus;&space;ke&space;&plus;&space;lh)&space;&plus;&space;s&space;&&space;(jc&space;&plus;&space;kf&space;&plus;&space;li)&plus;&space;s\\&space;(ma&space;&plus;&space;nd&space;&plus;&space;og)&space;&plus;&space;t&space;&&space;(mb&space;&plus;&space;ne&space;&plus;&space;oh)&space;&plus;&space;t&space;&&space;(mc&space;&plus;&space;nf&space;&plus;&space;oi)&space;&plus;&space;t\\&space;(pa&space;&plus;&space;qd&space;&plus;&space;rg)&space;&plus;&space;u&space;&&space;(pb&space;&plus;&space;qe&space;&plus;&space;rh)&space;&plus;&space;u&space;&&space;(pc&space;&plus;&space;qf&space;&plus;&space;ri)&plus;&space;u&space;\end{bmatrix}$$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$$&space;WX&space;&plus;&space;b&space;=&space;\begin{bmatrix}&space;(ja&space;&plus;&space;kd&space;&plus;&space;lg)&space;&plus;&space;s&space;&&space;(jb&space;&plus;&space;ke&space;&plus;&space;lh)&space;&plus;&space;s&space;&&space;(jc&space;&plus;&space;kf&space;&plus;&space;li)&plus;&space;s\\&space;(ma&space;&plus;&space;nd&space;&plus;&space;og)&space;&plus;&space;t&space;&&space;(mb&space;&plus;&space;ne&space;&plus;&space;oh)&space;&plus;&space;t&space;&&space;(mc&space;&plus;&space;nf&space;&plus;&space;oi)&space;&plus;&space;t\\&space;(pa&space;&plus;&space;qd&space;&plus;&space;rg)&space;&plus;&space;u&space;&&space;(pb&space;&plus;&space;qe&space;&plus;&space;rh)&space;&plus;&space;u&space;&&space;(pc&space;&plus;&space;qf&space;&plus;&space;ri)&plus;&space;u&space;\end{bmatrix}$$" title="\large $$ WX + b = \begin{bmatrix} (ja + kd + lg) + s & (jb + ke + lh) + s & (jc + kf + li)+ s\\ (ma + nd + og) + t & (mb + ne + oh) + t & (mc + nf + oi) + t\\ (pa + qd + rg) + u & (pb + qe + rh) + u & (pc + qf + ri)+ u \end{bmatrix}$$" /></a>

### **Mathematical expression of the algorithm**:

![](https://i.imgur.com/FPjpVDX.png)

### **Foward propagation:**

The linear forward module (vectorized over all the examples) computes the following equations:

<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$$Z^{[l]}&space;=&space;W^{[l]}A^{[l-1]}&space;&plus;b^{[l]}$$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$$Z^{[l]}&space;=&space;W^{[l]}A^{[l-1]}&space;&plus;b^{[l]}$$" title="\large $$Z^{[l]} = W^{[l]}A^{[l-1]} +b^{[l]}$$" /></a>

where <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;A^{[0]}&space;=&space;X^T$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;A^{[0]}&space;=&space;X^T$" title="\large $ A^{[0]} = X^T$" /></a>. And the activation functions:

<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$$A&space;=&space;RELU(Z)&space;=&space;max(0,&space;Z)$$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$$A&space;=&space;RELU(Z)&space;=&space;max(0,&space;Z)$$" title="\large $$A = RELU(Z) = max(0, Z)$$" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$$A^{[L]}&space;=&space;sigmoid(Z^{[L]})$$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$$A^{[L]}&space;=&space;sigmoid(Z^{[L]})$$" title="\large $$A^{[L]} = sigmoid(Z^{[L]})$$" /></a>

### **Cost function**

<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$$J&space;=&space;-\frac1m\sum&space;\bigg(&space;Y&space;\odot&space;log(A^{[L]})&space;&plus;&space;(1-Y)&space;\odot&space;log(1-A^{[L]})&space;\bigg)$$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$$J&space;=&space;-\frac1m\sum&space;\bigg(&space;Y&space;\odot&space;log(A^{[L]})&space;&plus;&space;(1-Y)&space;\odot&space;log(1-A^{[L]})&space;\bigg)$$" title="\large $$J = -\frac1m\sum \bigg( Y \odot log(A^{[L]}) + (1-Y) \odot log(1-A^{[L]}) \bigg)$$" /></a>

Note that <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$\odot$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$\odot$" title="\large $\odot$" /></a> denotes elementwise multiplication.

### **Backward propagation**

The three outputs <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$(dZ^{[l]},&space;dW^{[l]},&space;db^{[l]})$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$(dZ^{[l]},&space;dW^{[l]},&space;db^{[l]})$" title="\large $(dZ^{[l]}, dW^{[l]}, db^{[l]})$" /></a> are computed using the input <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$&space;dZ^{[l]}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$&space;dZ^{[l]}$" title="\large $ dZ^{[l]}$" /></a>.Here are the formulas we need:

<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$$dZ^{[l]}&space;=&space;W^{[l&plus;1]^T}dZ^{[l&plus;1]}&space;\odot&space;g^{[l]'}(Z^{[l]})$$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$$dZ^{[l]}&space;=&space;W^{[l&plus;1]^T}dZ^{[l&plus;1]}&space;\odot&space;g^{[l]'}(Z^{[l]})$$" title="\large $$dZ^{[l]} = W^{[l+1]^T}dZ^{[l+1]} \odot g^{[l]'}(Z^{[l]})$$" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$$&space;dW^{[l]}&space;=&space;\frac{\partial&space;\mathcal{L}&space;}{\partial&space;W^{[l]}}&space;=&space;\frac{1}{m}&space;dZ^{[l]}&space;A^{[l-1]&space;T}$$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$$&space;dW^{[l]}&space;=&space;\frac{\partial&space;\mathcal{L}&space;}{\partial&space;W^{[l]}}&space;=&space;\frac{1}{m}&space;dZ^{[l]}&space;A^{[l-1]&space;T}$$" title="\large $$ dW^{[l]} = \frac{\partial \mathcal{L} }{\partial W^{[l]}} = \frac{1}{m} dZ^{[l]} A^{[l-1] T}$$" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\large&space;$$&space;db^{[l]}&space;=&space;\frac{\partial&space;\mathcal{L}&space;}{\partial&space;b^{[l]}}&space;=&space;\frac{1}{m}&space;\sum_{i&space;=&space;1}^{m}&space;dZ^{[l](i)}$$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\large&space;$$&space;db^{[l]}&space;=&space;\frac{\partial&space;\mathcal{L}&space;}{\partial&space;b^{[l]}}&space;=&space;\frac{1}{m}&space;\sum_{i&space;=&space;1}^{m}&space;dZ^{[l](i)}$$" title="\large $$ db^{[l]} = \frac{\partial \mathcal{L} }{\partial b^{[l]}} = \frac{1}{m} \sum_{i = 1}^{m} dZ^{[l](i)}$$" /></a>


## CONCLUSION
We achieved the **Accuracy score of 66.8%** which is **better than** the Accuracy score of Logistic Regression Model in **sklearn (57.6%)**. Our hyperparameters are:

* Learning rate = `0.011`
* Number of hidden layers = `5`
* Number of nodes in each hidden layers = `[32,64,128,256,512]`
* Number of iterations = `1900`
