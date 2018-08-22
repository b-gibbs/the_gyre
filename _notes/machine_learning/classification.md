---
title: Supervised Classification Algorithms
permalink: /notes/machine_learning/supervised_classification
---
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Supervised-Linear-Algorithms">Supervised Linear Algorithms<a class="anchor-link" href="#Supervised-Linear-Algorithms">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="k-Nearest-Neighbors">k-Nearest Neighbors<a class="anchor-link" href="#k-Nearest-Neighbors">&#182;</a></h2><h3 id="Discussion"><strong>Discussion</strong><a class="anchor-link" href="#Discussion">&#182;</a></h3><p><strong>MODEL COMPLEXITY</strong></p>
<p>decision boundary</p>
<ul>
<li>larger k = smoother decision boundary = less complex model</li>
<li>smaller k = more complex model = can lead to overfitting</li>
</ul>
<h3 id="Code"><strong>Code</strong><a class="anchor-link" href="#Code">&#182;</a></h3>

<figure class="highlight"><pre><span></span><span class="c1"># imports</span>
<span class="kn">from</span> <span class="nn">sklearn.neighbors</span> <span class="kn">import</span> <span class="n">KNeighborsClassifier</span> 

<span class="c1"># break off Series y from matrix X</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">party</span><span class="o">.</span><span class="n">values</span>
<span class="n">X</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;party&#39;</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">values</span>

<span class="c1"># train test split</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span><span class="o">=</span><span class="mf">0.3</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">21</span><span class="p">,</span> <span class="n">stratify</span><span class="o">=</span><span class="n">y</span><span class="p">)</span>

<span class="c1"># Create a k-NN classifier with 6 neighbors:</span>
<span class="n">knn</span> <span class="o">=</span> <span class="n">KNeighborsClassifier</span><span class="p">(</span><span class="n">n_neighbors</span><span class="o">=</span><span class="mi">6</span><span class="p">)</span>

<span class="c1"># Fit the classifier to the data</span>
<span class="n">knn</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X</span><span class="p">,</span><span class="n">y</span><span class="p">)</span>

<span class="c1"># Predict the labels for the training data X</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">knn</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X</span><span class="p">)</span>


<span class="c1"># get a score</span>
<span class="n">knn</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">)</span>

<span class="c1"># Predict and print the label for the new data point X_new</span>
<span class="n">new_prediction</span> <span class="o">=</span> <span class="n">knn</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_new</span><span class="p">)</span>
<span class="k">print</span><span class="p">(</span><span class="s2">&quot;Prediction: {}&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">new_prediction</span><span class="p">))</span>
</pre>
</figure>
</div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Logistic-Regression">Logistic Regression<a class="anchor-link" href="#Logistic-Regression">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Linear-Discriminant-Analysis">Linear Discriminant Analysis<a class="anchor-link" href="#Linear-Discriminant-Analysis">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Support-Vector-Machines">Support Vector Machines<a class="anchor-link" href="#Support-Vector-Machines">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Decision-Trees">Decision Trees<a class="anchor-link" href="#Decision-Trees">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Random-Forests">Random Forests<a class="anchor-link" href="#Random-Forests">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Boosting">Boosting<a class="anchor-link" href="#Boosting">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="XGBoost">XGBoost<a class="anchor-link" href="#XGBoost">&#182;</a></h3>
</div>
</div>
</div>
 

