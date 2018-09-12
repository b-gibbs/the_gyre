---
title: Relax Take Home Challenge - Analysis
permalink: /coursework/takehomes/relax/
---



<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Relax-Take-Home-Challenge---Analysis">Relax Take Home Challenge - Analysis<a class="anchor-link" href="#Relax-Take-Home-Challenge---Analysis">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Some quick EDA showed that the data in the form given to us didn't provide many distinguishing features, so I decided to create some new features.  Common sense suggests that those who login shortly after generating their accounts and those who login more frequently are most likely to become adopted users.</p>

</div>
</div>
</div>

<a class="anchor" name="Project Desc"></a>
<a href="/coursework/takehomes/relax_instructions"><button type="button" class="btn btn-primary">Project Desc</button></a>

<a class="anchor" name="Relax_work.ipynb"></a>
<a href="/coursework/takehomes/relax_work"><button type="button" class="btn btn-primary">Relax_work.ipynb</button></a>

<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Cleaning-and-Feature-Engineering-Steps">Cleaning and Feature Engineering Steps<a class="anchor-link" href="#Cleaning-and-Feature-Engineering-Steps">&#182;</a></h2><h3 id="1.-identify-adopted-users">1. identify adopted users<a class="anchor-link" href="#1.-identify-adopted-users">&#182;</a></h3><p>To identify the adopted users (users who logged in at least three times over a seven day period), I added a column to count the number of visits over a rolling seven day period:</p>
<div class="highlight"><pre><span></span><span class="k">def</span> <span class="nf">get_rolling_count</span><span class="p">(</span><span class="n">grp</span><span class="p">,</span> <span class="n">freq</span><span class="p">):</span>
    <span class="k">return</span> <span class="n">grp</span><span class="o">.</span><span class="n">rolling</span><span class="p">(</span><span class="n">freq</span><span class="p">,</span> <span class="n">on</span><span class="o">=</span><span class="s1">&#39;time_stamp&#39;</span><span class="p">)[</span><span class="s1">&#39;user_id&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">count</span><span class="p">()</span>

<span class="n">engage</span><span class="p">[</span><span class="s1">&#39;visits_7_days&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">engage</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;user_id&#39;</span><span class="p">,</span> <span class="n">as_index</span><span class="o">=</span><span class="bp">False</span><span class="p">,</span> <span class="n">group_keys</span><span class="o">=</span><span class="bp">False</span><span class="p">)</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">get_rolling_count</span><span class="p">,</span> <span class="s1">&#39;7D&#39;</span><span class="p">)</span>
</pre></div>
<p>Then, I collected each row &gt;= 3, dropped duplicates after the first occurrence and converted the results to a list. I used <code>.isin</code> to check whether the <code>object_id</code> in the users DataFrame was in the list of adopted users and marked matches as <code>True</code> in the users DataFrame.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="2.-add-col-for-time-between-account-creation-and-initial-login">2. add col for time between account creation and initial login<a class="anchor-link" href="#2.-add-col-for-time-between-account-creation-and-initial-login">&#182;</a></h3><p>I grouped by <code>user_id</code> and used <code>np.min</code> with a <code>.agg</code> function to find the first login for each user, added that time stamp to the users DataFrame and created a new column to record the time in days between creation of each account and first login.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="3.-add-col-for-mean-time-between-logins">3. add col for mean time between logins<a class="anchor-link" href="#3.-add-col-for-mean-time-between-logins">&#182;</a></h3><p>I created a new DataFrame to calculate and store the time between logins:</p>
<div class="highlight"><pre><span></span><span class="n">gap</span> <span class="o">=</span> <span class="n">engage</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;user_id&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">time_stamp</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">x</span> <span class="o">-</span> <span class="n">x</span><span class="o">.</span><span class="n">shift</span><span class="p">())</span><span class="o">.</span><span class="n">dt</span><span class="o">.</span><span class="n">days</span>
</pre></div>
<p>I then grouped these by user, calculated a mean time between all logins for each user and merged the resulting Series into the users DataFrame.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="4.-add-col---org-size-categorical">4. add col - org size categorical<a class="anchor-link" href="#4.-add-col---org-size-categorical">&#182;</a></h3><p>I used <code>.value_counts()</code> to generate a dictionary counting the number of users who belonged to each org, then binned these into XS, S, M, L and XL and each these to users in the users DataFrame:</p>
<div class="highlight"><pre><span></span><span class="k">def</span> <span class="nf">org_size</span><span class="p">(</span><span class="n">ct</span><span class="p">):</span>
    <span class="n">rtn</span> <span class="o">=</span> <span class="s1">&#39;XS&#39;</span>
    <span class="k">if</span> <span class="n">ct</span> <span class="o">&gt;</span> <span class="mi">200</span><span class="p">:</span>
        <span class="n">rtn</span> <span class="o">=</span> <span class="s1">&#39;XL&#39;</span>
    <span class="k">elif</span> <span class="n">ct</span> <span class="o">&gt;</span> <span class="mi">149</span><span class="p">:</span>
        <span class="n">rtn</span> <span class="o">=</span> <span class="s1">&#39;L&#39;</span>
    <span class="k">elif</span> <span class="n">ct</span> <span class="o">&gt;</span> <span class="mi">99</span><span class="p">:</span>
        <span class="n">rtn</span> <span class="o">=</span> <span class="s1">&#39;M&#39;</span>
    <span class="k">elif</span> <span class="n">ct</span> <span class="o">&gt;</span> <span class="mi">49</span><span class="p">:</span>
        <span class="n">rtn</span> <span class="o">=</span> <span class="s1">&#39;S&#39;</span>

    <span class="k">return</span> <span class="n">rtn</span>

<span class="n">o</span><span class="p">[</span><span class="s1">&#39;org_size&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">o</span><span class="o">.</span><span class="n">user_count</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">org_size</span><span class="p">)</span>

<span class="n">org_size_dict</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">o</span><span class="o">.</span><span class="n">org_id</span><span class="p">,</span> <span class="n">o</span><span class="o">.</span><span class="n">org_size</span><span class="p">))</span>
<span class="n">org_size_dict</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">nan</span>

<span class="n">users</span><span class="p">[</span><span class="s1">&#39;org_size&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">org_id</span><span class="o">.</span><span class="n">map</span><span class="p">(</span><span class="n">org_size_dict</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="5.-add-col---invited-by-user-group-size">5. add col - invited by user group size<a class="anchor-link" href="#5.-add-col---invited-by-user-group-size">&#182;</a></h3><p>I used a strategy similar to the org size categorizing and binning described above to make each user's social network within the app into a feature binned by size.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="6.-drop-unneeded-cols">6. drop unneeded cols<a class="anchor-link" href="#6.-drop-unneeded-cols">&#182;</a></h3><p>I dropped unneeded columns, such as <code>object_id</code>, <code>name</code>, <code>email</code>, etc.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="7.-transform-categoricals">7. transform categoricals<a class="anchor-link" href="#7.-transform-categoricals">&#182;</a></h3><p>I used <code>pd.get_dummies</code> to one-hot encode <code>creation_size</code>, <code>org_size</code> and <code>group_size</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Modeling">Modeling<a class="anchor-link" href="#Modeling">&#182;</a></h2><p>The target set was imbalanced, with approximately 13% of all users labeled positively, as adopted users. While not massively imbalanced, I decided to use the SMOTE technique from <code>imblearn</code> to amplify the signal in the noise.  Because the goal of the project is "to identify which factors predict future user adoption", I chose to focus on precision scores and the models that produced the highest number of true positives.  I used sklearn's dummy classifier as a baseline, which produced the following classification report:</p>
<p><img src="images/dummy_classifier.png" alt=""></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>I ran the dataset through Logistic Regression, LinearSVC, SVC and Random Forest.  The results from Random Forest were the best, so I tuned the hyperparameters and re-ran the model with tuned parameters.  The tuned model results in a slightly higher F1 score, but the precision score was a mixed bag -- the number of true positives increased from 411 to 472, but the number of false positives also increased from 59 to 129.  Below are the results of the tuned Random Forest:</p>
<p><img src="images/tuned_rf.png" alt=""></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The feature importances aren't surprising.  <code>mean_gap_length</code> indicates the mean gap between logins in days.  Since this is so closely related to the definition of an adopted user, it's not surprising that the two are highly correlated. This is still a useful bit of information.  The company could send tickler emails or find other ways to encourage users login, particularly within the days immediately following account creation.  The second most important feature, by a wide margin, is the gap in days between account creation and initial login.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Conclusion">Conclusion<a class="anchor-link" href="#Conclusion">&#182;</a></h2><p>Encouraging users to login as they sign up and again soon after account creation will, according to this data, increase the number of adopted users.  Perhaps another department should create a short series of tips on how to get the most out of the app and send some number of emails offering these tips at different times of day over the course of the first several days after a new user creates an account.  We could track and model response data from these emails and decide how to proceed from there.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="TO-DO:">TO DO:<a class="anchor-link" href="#TO-DO:">&#182;</a></h2><p>With more time, I'd like to put this in a Docker instance on AWS and tune the hyperparameters of an XGBoost model.</p>

</div>
</div>
</div>
 

