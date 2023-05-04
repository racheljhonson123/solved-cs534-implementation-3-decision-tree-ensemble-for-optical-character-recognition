Download Link: https://assignmentchef.com/product/solved-cs534-implementation-3-decision-tree-ensemble-for-optical-character-recognition
<br>
In this assignment we continue working on the Optical Character Recognition task to classify between two numbers 3 and 5. The goal in this assignment is to develop variations of the <strong>decision tree</strong>.

<strong>Data. </strong>The data for this assignment is generated from the data of implementation assignment 2. We apply the Principal Component Analysis (PCA) to reduce the dimension from 784 to 100. Here is a short description of each train and validation split:

<ul>

 <li><strong>Train Set (pa3 train reduced.csv): </strong>Includes 4888 rows (samples). Each sample is in fact a list of 101 values. The first number is the digit’s label which is 3 or 5. The other 100 floating values are the the flattened feature values given by the PCA.</li>

 <li><strong>Validation Set (pa3 valid reduced.csv): </strong>Includes 1629 rows. Each row obeys the same format given for the train set. This set will be used to tune the hyper parameters and select the best model.</li>

</ul>

<strong>Important Guidelines.           </strong>For all parts of this assignment:

<ul>

 <li>Please assign labels +1 to number 3 and -1 to label 5.</li>

 <li>Please <u>do not </u>add bias to the features.</li>

</ul>

<strong>Part 1 (20 pts) : Decision Tree (DT). </strong>For this part we are interested in using a decision tree with below configuration:

<ul>

 <li>The DT uses gini-index to measure the uncertainty. Specifically if we have a node split from list A to</li>

</ul>

two left and right lists AL and AR as depicted in figure 1 then

Figure 1: Split list A to two lists AL and AL with feature <em>f<sub>i </sub></em>at threshold T

the benefit of split for feature <em>f<sub>i </sub></em>at threshold <em>T </em>is computed as:

<table width="591">

 <tbody>

  <tr>

   <td width="574"><em>B </em>= <em>U</em>(<em>A</em>) − <em>p<sub>l</sub>U</em>(<em>AL</em>) − <em>p<sub>r</sub>U</em>(<em>AR</em>)Where <em>U </em>is the gini-index function which is computed for a list such as AL as follows:</td>

   <td width="17">(1)</td>

  </tr>

 </tbody>

</table>

(2)

and <em>p<sub>l </sub></em>and <em>p<sub>r </sub></em>are the probabilities for each split which is given by

(3)

<ul>

 <li>The feature values are continuous. Therefore you need to follow the descriptions and hints given in the slide to search for the best threshold <em>T </em>for a feature <em>f<sub>i</sub></em>.</li>

</ul>

Please implement below steps:

<ul>

 <li>Create a decision tree with maximum depth of 20 (root is at depth=0) on the train data. (Note that</li>

</ul>

a normal implementation of the tree should take about 220 seconds on Babylon for this maximum of depth.)

<ul>

 <li>Using the created decision tree, compute and plot the train and validation accuracy versus depth.</li>

 <li>Explain the behavior of train/validation performance against the depth. At which depth the train accuracy reaches to 100% accuracy? If your tree could not get to 100% before the depth of 20, keep on extending the tree in depth until it reaches 100% for the train accuracy.</li>

 <li>Report the depth that gives the best validation accuracy?</li>

</ul>

<strong>Part 2 (30 pts) : Random Forest (Bagging). </strong>In this part we are interested in random forest which is a variation of bagging without some of its limitations. Please implement below steps:

<ul>

 <li>Implement a random forest with below parameters:</li>

</ul>

<em>n </em>: The number of trees in the forest. <em>m </em>: The number of features for a tree. <em>d </em>: Maximum depth of the trees in the forest.

Here is how the forest is created: The random forest is a collection of <em>n </em>trees. All the trees in the forest

has maximum depth of <em>d</em>. Each tree is built on a data set of size 4888 sampled (with replacement) from the train set. In the process of building a tree of the forest, each time we try to find the best feature <em>f<sub>i </sub></em>to split, we need to first sub-sample (without replacement) <em>m </em>number of features from 100 feature set and then pick <em>f<sub>i </sub></em>with highest benefit from <em>m </em>sampled features.

<ul>

 <li>For <em>d </em>= 9, <em>m </em>= 10 and <em>n </em>∈ [1<em>,</em>2<em>,</em>5<em>,</em>10<em>,</em>25], plot the train and validation accuracy of the forest versus the number of trees in the forest <em>n</em>.</li>

 <li>What effect adding more tree into a forest has on the train/validation performance? Why?</li>

 <li>Repeat above experiments for <em>d </em>= 9 and <em>m </em>∈ [20<em>,</em>50]. How greater <em>m </em>changes the train/validation accuracy? Why?</li>

</ul>

<strong>Part 3 (30 pts) : AdaBoost (Boosting). </strong>For this part we are interested in applying AdaBoost to create yet another ensemble model with decision tree. Considering the AdaBoost algorithm described in the slide, please do below steps:

<ul>

 <li>Let the weak learner be a decision tree with depth of 9. The decision tree should get a weight parameter <em>D </em>which is a vector of size 4888 (train size). Implement the decision tree with parameter <em>D </em>such that it considers <em>D </em>in its functionality.</li>

</ul>

(Hint: It changes the gini-index and also the predictions at leaves).

<ul>

 <li>Using the decision tree with parameter <em>D </em>implemented above, develop the AdaBoost algorithm as described in the slide with parameter L.</li>

 <li>Report the train and validation accuracy for <em>L </em>∈ [1<em>,</em>5<em>,</em>10<em>,</em>20].</li>

 <li>Explain the behavior of AdaBoost against the parameter <em>L</em>.</li>

</ul>