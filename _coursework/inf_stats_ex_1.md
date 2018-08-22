--- 
title: Inferential Statistics - Body Temperature 
permalink: /coursework/stats/body_temp/ 
---


<div class="cell border-box-sizing text_cell rendered">
    <div class="input">
        <div class="prompt input_prompt"></div>
        <div class="inner_cell">
            <div class="text_cell_render border-box-sizing rendered_html">
                <h1 id="What-is-the-True-Normal-Human-Body-Temperature?">What is the True Normal Human Body Temperature?
                </h1>
            </div>
        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt"></div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h2 id="Background">Background</h2>
            <p>The mean normal body temperature was held to be 37$^{\circ}$C or 98.6$^{\circ}$F for more than 120 years since
                it was first conceptualized and reported by Carl Wunderlich in a famous 1868 book. But, is this value statistically
                correct?</p>

        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt"></div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h2>Exercises</h2>
            <p>In this exercise, you will analyze a dataset of human body temperatures and employ the concepts of hypothesis testing, confidence intervals, and statistical significance.</p>
            <p>Answer the following questions <b>in this notebook below and submit to your Github account</b>.</p>
            <ol>
                <li> Is the distribution of body temperatures normal?</li>
                    <ul>
                        <li> Although this is not a requirement for the Central Limit Theorem to hold (read the introduction on Wikipedia's page about the [CLT](https://en.wikipedia.org/wiki/Central_limit_theorem) carefully: it gives us some peace of mind that the population may also be normally distributed if we assume that this sample is representative of the population.</li>
                        <li> Think about the way you're going to check for the normality of the distribution. Graphical methods are usually used first, but there are also other ways: https://en.wikipedia.org/wiki/Normality_test </li>
                    </ul>
                    <li> Is the sample size large? Are the observations independent?</li>
                    <ul>
                        <li> Remember that this is a condition for the Central Limit Theorem, and hence the statistical tests we are using, to apply.</li>
                    </ul>
                    <li> Is the true population mean really 98.6 degrees F?</li>
                    <ul>
                        <li> First, try a bootstrap hypothesis test.</li>
                        <li> Now, let's try frequentist statistical testing. Would you use a one-sample or two-sample test? Why?</li>
                        <li> In this situation, is it appropriate to use the $t$ or $z$ statistic?</li>
                        <li> Now try using the other test. How is the result be different? Why?</li>
                    </ul>
                    <li> Draw a small sample of size 10 from the data and repeat both frequentist tests.</li>
                    <ul>
                        <li> Which one is the correct one to use?</li>
                        <li> What do you notice? What does this tell you about the difference in application ofmthe $t$ and $z$ statistic?</li>
                    </ul>
                    <li> At what temperature should we consider someone's temperature to be "abnormal"?</li>
                    <ul>
                        <li> As in the previous example, try calculating everything using the boostrap approach, as well as the frequentist approach.</li>
                        <li> Start by computing the margin of error and confidence interval. When calculating the confidence interval, keep in mind that you should use the appropriate formula for one draw, and not N draws.</li>
                    </ul>
                    <li> Is there a significant difference between males and females in normal temperature?</li>
                    <ul>
                        <li> What testing approach did you use and why?</li>
                        <li> Write a story with your conclusion in the context of the original problem.</li>
                    </ul>
                </ol>
            <p>You can include written notes in notebook cells using Markdown:</p>
            <ul>
                <li>In the control panel at the top, choose Cell &gt; Cell Type &gt; Markdown</li>
                <li>Markdown syntax:
                    <a href="http://nestacms.com/docs/creating-content/markdown-cheat-sheet" target="_blank">http://nestacms.com/docs/creating-content/markdown-cheat-sheet</a>
                </li>
            </ul>
            <h4 id="Resources">Resources
                <a class="anchor-link" href="#Resources">&#182;</a>
            </h4>
            <ul>
                <li>Information and data sources:
                    <a href="http://www.amstat.org/publications/jse/datasets/normtemp.txt" target="_blank">http://www.amstat.org/publications/jse/datasets/normtemp.txt</a>,
                    <a href="http://www.amstat.org/publications/jse/jse_data_archive.htm" target="_blank">http://www.amstat.org/publications/jse/jse_data_archive.htm</a>
                </li>
                <li>Markdown syntax:
                    <a href="http://nestacms.com/docs/creating-content/markdown-cheat-sheet" target="_blank">http://nestacms.com/docs/creating-content/markdown-cheat-sheet</a>
                </li>
            </ul>
            <hr>
        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt"></div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h2 id="Summary-of-Findings">Summary of Findings</h2>
            <hr>
            <p>The mean normal body temperature was held to be 98.6°F for more than 120 years since it was first conceptualized and reported by Carl Wunderlich in a famous 1868 book. After examining a data set of 130 samples (65 males and 65 females), we'll see that the mean normal body temperature is actually 98.25°F. We'll also see that the mean body temperature of females is significantly higher than males'.</p>
        </div>
    </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[1]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># IMPORTS</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="kn">import</span> <span class="nn">scipy.stats</span> <span class="k">as</span> <span class="nn">stats</span>
<span class="kn">import</span> <span class="nn">statsmodels.stats</span> <span class="k">as</span> <span class="nn">smd</span>
<span class="kn">import</span> <span class="nn">pylab</span>

<span class="c1"># matplotlib setup</span>
<span class="o">%</span><span class="k">matplotlib</span> inline

<span class="c1"># turn edges on in plt</span>
<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s2">&quot;patch.force_edgecolor&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="kc">True</span>

<span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="mi">42</span><span class="p">)</span>

<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;data/human_body_temperature.csv&#39;</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt output_prompt">Out[1]:</div>



                <div class="output_html rendered_html output_subarea output_execute_result">
                    <div>
                        <style>
                            .dataframe thead tr:only-child th {
                                text-align: right;
                            }

                            .dataframe thead th {
                                text-align: left;
                            }

                            .dataframe tbody tr th {
                                vertical-align: top;
                            }
                        </style>
                        <table border="1" class="dataframe">
                            <thead>
                                <tr style="text-align: right;">
                                    <th></th>
                                    <th>temperature</th>
                                    <th>gender</th>
                                    <th>heart_rate</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <th>0</th>
                                    <td>99.3</td>
                                    <td>F</td>
                                    <td>68.0</td>
                                </tr>
                                <tr>
                                    <th>1</th>
                                    <td>98.4</td>
                                    <td>F</td>
                                    <td>81.0</td>
                                </tr>
                                <tr>
                                    <th>2</th>
                                    <td>97.8</td>
                                    <td>M</td>
                                    <td>73.0</td>
                                </tr>
                                <tr>
                                    <th>3</th>
                                    <td>99.2</td>
                                    <td>F</td>
                                    <td>66.0</td>
                                </tr>
                                <tr>
                                    <th>4</th>
                                    <td>98.0</td>
                                    <td>F</td>
                                    <td>73.0</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[2]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># FUNCTIONS USED</span>

<span class="k">def</span> <span class="nf">ecdf</span><span class="p">(</span><span class="n">data</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Compute ECDF for a one-dimensional array of measurements.&quot;&quot;&quot;</span>

    <span class="c1"># Number of data points: n</span>
    <span class="n">n</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">data</span><span class="p">)</span>

    <span class="c1"># x: sort the data</span>
    <span class="n">x</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sort</span><span class="p">(</span><span class="n">data</span><span class="p">)</span>

    <span class="c1"># y: range for y-axis</span>
    <span class="n">y</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">n</span><span class="o">+</span><span class="mi">1</span><span class="p">)</span> <span class="o">/</span> <span class="n">n</span>

    <span class="k">return</span> <span class="n">x</span><span class="p">,</span> <span class="n">y</span>
</pre>
                </div>
            </div>
        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt"></div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h3 id="Question-#1">Question #1</h3>
            <hr>
            <p>Is the distribution of body temperatures normal?</p>
            <ul>
                <li>Although this is not a requirement for the Central Limit Theorem to hold (read the introduction on Wikipedia's page about the CLT carefully: https://en.wikipedia.org/wiki/Central_limit_theorem), it gives us some peace of mind that the population may also be normally distributed if we assume that this sample is representative of the population.</li><br>
                <li>Think about the way you're going to check for the normality of the distribution. Graphical methods are usually used first, but there are also other ways: https://en.wikipedia.org/wiki/Normality_test</li>
            </ul>
        </div>
    </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[3]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># Plot a histogram to see whether the distribution is normal</span>
<span class="n">temp</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">temperature</span>

<span class="n">sns</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">rc</span><span class="o">=</span><span class="p">{</span><span class="s2">&quot;figure.figsize&quot;</span><span class="p">:</span> <span class="p">(</span><span class="mi">12</span><span class="p">,</span> <span class="mi">8</span><span class="p">)})</span>
<span class="n">plt</span><span class="o">.</span><span class="n">style</span><span class="o">.</span><span class="n">use</span><span class="p">(</span><span class="s1">&#39;fivethirtyeight&#39;</span><span class="p">)</span>

<span class="c1"># Number of bins is the square root of number of data points: n_bins</span>
<span class="n">n_bins</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">temp</span><span class="p">))</span>

<span class="c1"># Convert number of bins to integer: n_bins</span>
<span class="n">n_bins</span> <span class="o">=</span> <span class="nb">int</span><span class="p">(</span><span class="n">n_bins</span><span class="p">)</span>

<span class="c1"># plot hist</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">temp</span><span class="p">,</span> <span class="n">density</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">bins</span><span class="o">=</span><span class="n">n_bins</span><span class="p">)</span>

<span class="c1"># overlay PDF of the Standard Normal Distribution</span>
<span class="n">x</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">min</span><span class="p">(</span><span class="n">temp</span><span class="p">)</span> <span class="o">-</span> <span class="mi">1</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">temp</span><span class="p">)</span> <span class="o">+</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">100</span><span class="p">,</span> <span class="n">endpoint</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">pdf</span> <span class="o">=</span> <span class="p">[</span><span class="n">stats</span><span class="o">.</span><span class="n">norm</span><span class="o">.</span><span class="n">pdf</span><span class="p">(</span><span class="n">_</span><span class="p">,</span> <span class="n">loc</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">temp</span><span class="p">),</span> <span class="n">scale</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">temp</span><span class="p">))</span> <span class="k">for</span> <span class="n">_</span> <span class="ow">in</span> <span class="n">x</span><span class="p">]</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">pdf</span><span class="p">,</span> <span class="s1">&#39;k-&#39;</span><span class="p">)</span>


<span class="c1"># labels</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="mf">95.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">,</span> <span class="sa">r</span><span class="s1">&#39;$\mu= </span><span class="si">{}</span><span class="s1">,\ \sigma=</span><span class="si">{}</span><span class="s1">$&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">round</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">temp</span><span class="p">),</span> <span class="mi">2</span><span class="p">),</span> <span class="nb">round</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">temp</span><span class="p">),</span> <span class="mi">2</span><span class="p">)))</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Temperature (F)&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Frequency&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Fig. 1.1: Human Body Temperatures&#39;</span><span class="p">)</span>

<span class="n">margins</span> <span class="o">=</span> <span class="mf">0.02</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">((</span><span class="s1">&#39;Std Normal Dist&#39;</span><span class="p">,</span> <span class="s1">&#39;Samples&#39;</span><span class="p">))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">(</span><span class="o">-</span><span class="mf">0.01</span><span class="p">,</span> <span class="mf">0.65</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">();</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>




                <div class="output_png output_subarea ">
                    <img src="data:image/png;base64,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wIEDXL16lblz53L8+HGGDh3KsmXLuHr1Kh9//DGdOnXi3LlzfPPNNzg4OPDVV1+xZ88eChcunKLzLFiwYJICbe3atfzwww8UKlQIf39/ChYsaDnntBQkoKJERERERCTFzp8/j5OTk6XL1Z9//sn7779P7dq1LduEhISQN29ey1OchwuOxJ5//nk6d+7MuHHjsLKyAuDs2bPUrFkTKysrbG1tqVq1KmfOnAGgVKlSlve6ublha2tLnjx5KFmyJHZ2duTNm5fIyEgAChQowGeffUbu3Lk5e/bsY/NI7J9//qFIkSKG2JgxY/juu++4ceMG9erVS/G+UkID3UVEREREUujUqVOMHz+eqKgoIL6oyJMnDzY2NlhbWxMXF0eBAgW4c+cOISEhAJaB8I/y+uuvExoayv79+wEoXbq0petWdHQ0R44cwdXVFYh/upIgoYhJTlhYGNOnT+fLL79k+PDh5MqVi7i4uBSdY2RkJPPnz8fT09MQ27hxI//+97/54YcfWLVqFdeuXbOcc1rpSYmIiIiIZFtPGgOS3po0acKZM2fo0aMHuXPnJjY2lkGDBuHs7EylSpWYOnUqpUuX5qOPPmLw4MHkzZsXW9vH33JbWVkxatQounbtCoCHhwcHDx6kV69eREdH06xZMypVqvRUeTo5OVG9enV8fHywsbEhb968XLt2jRIlSiS7/ZkzZ+jXrx9WVlZER0fTsmVL3N3duXTpEgD29vbkzZuXXr16kStXLl5++WUKFSpkOOeELmapYRUaGpr20iYLCA4Opnz58manIY+ha5T16RplfbpGWZ+uUdana5T16RplD+l5ndR9S0RERERETKWiRERERERETKWiRERERERETKWiRERERERETKWiRERERERETKWiRERERERETKV1SkREREQk2zpzO5oL4THptr+STjaUyfvkW+RZs2axb98+oqOjsba2ZvDgwbzwwgvplseBAwdYunQpX375ZbrtMytTUSIiIiIi2daF8Bjarrmebvv7rWWhJxYlf/31F9u2bcPX1xcrKyuCgoL47LPPmDdvXrrl8axRUSIiIiIi8hScnZ25cuUKK1eupF69elSoUIGZM2dy8OBBpk+fTlxcHHfv3uWLL77Azs6O4cOHU7RoUS5duoSnpyenT5/m5MmTNGjQgHfffZd+/fpRqlQp/v77b+Li4pI8HdmwYQPz5s3DxsaGGjVqMHDgQA4fPszkyZOxsbHBwcGB//73vzg5OZn0iaSdihIRERERkadQpEgRvv76axYtWoSvry8ODg7079+fmzdvMmbMGAoXLsyMGTPYuHEjLVu25OLFi0ydOpWIiAjat2+Pv78/Dg4OeHt78+677wJQvXp1hg4dyuLFi5k5cyZNmjQB4NatW0yfPp1Zs2bh4ODA6NGj2bt3L3v37qVZs2Z07dqVbdu2cefOHRUlIiIiIiLPivPnz+Pk5MTIkSMB+PPPP3n//fcZPHgwEyZMwNHRkWvXrlG9enUAnnvuOZydnbGzs6NgwYLky5cvyT7r1KkDxBcnW7dutcQvXLhASEgI77//PgB3797lwoUL9OzZkxkzZjBgwAAKFy5M1apVM/q0M5Rm3xIREREReQqnTp1i/PjxREVFAfD888+TJ08evvnmG0aOHMno0aMpVKiQZXsrK6sn7vPEiRMAHD58mLJly1riJUqUoGjRonz77bf8+OOPvP7661SrVo2AgADatGnDDz/8QNmyZVm2bFk6n2Xm0pMSEREREZGn0KRJE86cOUOPHj3InTs3sbGxDBo0iD/++IO+ffvi6OhIwYIFuXbtWor36e/vz7x583B0dOSzzz7j9OnTABQoUIBu3brxzjvvEBsbS/HixWnevDmRkZF8+eWXODg4YG1tzdChQzPqdDOFVWhoaJzZSaSH4OBgypcvb3Ya8hi6RlmfrlHWp2uU9ekaZX26Rlnf01wjs6YETk/9+vXj008/pXTp0pl63LRKz++SnpSIiIiISLZVJq9tphcRkv4y9QrGxsYyduxYgoODsbe3Z/jw4bi6ulpe37VrF76+vsTFxVGpUiU+/vjjFPXBExERERHJrn788UezUzBdpg5037p1K5GRkfj5+TFgwAAmT55seS08PJwpU6YwceJEZsyYQfHixQkNDc3M9ERERERExASZ+qTk0KFD1KtXD4Bq1apx/Phxy2tHjhyhXLlyTJo0iYsXL+Lt7U2BAgUyMz0RERERETFBphYl4eHhODs7W9rW1tZER0dja2vLrVu32L9/P3PmzCF37tz07duXatWqUapUqcxMUUREREREMlmmFiVOTk6Eh4db2nFxcdjaxqeQL18+KleubJnT+cUXXyQoKChFRUlwcLDhX8m6dI2yPl2jrE/XKOvTNcr6dI2yPl2j7OFprtPjZurK1KKkRo0abN++nRYtWhAYGIibm5vltYoVK3L69GlCQ0Nxdnbm6NGjtGvXLkX7LV++vKb3ywZ0jbI+XaOsT9co69M1yvp0jbI+XaPsIdtOCdy4cWP27t2Lj48PcXFxjBo1irlz5+Lq6krDhg0ZMGAAgwcPBqBZs2aGokVERERERHKmTC1Kkltt8uFFYjw9PfH09MzMlERERERExGSZOiWwiIiIiIhIYipKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERER12VCnAAAgAElEQVTEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVCpKRERERETEVLZmJyAiItnXmdvRXAiPMTuNFCnpZEOZvPq1JyKSFen/nUVEJNUuhMfQds11s9NIkd9aFlJRIiKSRan7loiIiIiImEpFiYiIiIiImEpFiYiIiIiImEpFiYiIiIiImEpFiYiIiIiImEpFiYiIiIiImEpFiYiIiIiImEpFiYiIiIiImEqrSImIiEVoaChHjhwhKCiIvHnz8sorr/Dcc8+ZnZaIiORwKkpERJ5RV65cYf/+/QQGBnLkyBECAwM5f/58ku3KlStHo0aNaNiwIQ0bNqRAgQImZCsiIjmZihIRkWdMSEgII0eOZN68ecTGxj5x+1OnTnHq1Cl+/vlnrKysqF69Om3btuXdd98FbDI+YRERyfFUlIiIZDFnbkdzITwm2dfu2RTmn8v3U7XfuLg4tq9ezvSvRhB643qq93H48GEOHz7MjLnzGfTf74CSqdqXiIhIAhUlIiJZzIXwGNqueVzREP70O715CRZ/Ace3PX47axso6gYlKsDNi/B3IMRGJ7vpxTOnGN69NfxrIDTtFf9eERGRVFBRIiKSk8XGwPa5sHoKRN5L+nrhUlDxFXiuEjz3AhRzA7tcD16PCIe/DkDwHgjaA5dOGt4eEx0NqybBiZ3Q/T9QoEQGn5CIiOREKkpERHKqa3/DnI/h3NGkr9nYgec70NQHbO0fvQ8HJ6jcMP4/gDs3YPVk2LPEuN3p32FcB3htJNRqnX7n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
">
                </div>

            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[4]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="n">sns</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">rc</span><span class="o">=</span><span class="p">{</span><span class="s2">&quot;figure.figsize&quot;</span><span class="p">:</span> <span class="p">(</span><span class="mi">12</span><span class="p">,</span> <span class="mi">8</span><span class="p">)})</span>
<span class="n">plt</span><span class="o">.</span><span class="n">style</span><span class="o">.</span><span class="n">use</span><span class="p">(</span><span class="s1">&#39;fivethirtyeight&#39;</span><span class="p">)</span>

<span class="n">stats</span><span class="o">.</span><span class="n">probplot</span><span class="p">(</span><span class="n">temp</span><span class="p">,</span> <span class="n">dist</span><span class="o">=</span><span class="s1">&#39;norm&#39;</span><span class="p">,</span> <span class="n">plot</span><span class="o">=</span><span class="n">pylab</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Fig. 1.2: Probability Plot of Human Body Temperatures&#39;</span><span class="p">);</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>




                <div class="output_png output_subarea ">
                    <img src="data:image/png;base64,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1WBAISIiIiIiq8GAQkREREREVoMBhYiIiIiIrAYDChERERERWQ0GFCIiIiIishoMKEREREREZDUYUIiIiIiIyGowoBARERERkdVgQCEiIiIiIqvBgEJERERERFaDAYWIiIiIiKwGAwoREREREVkNBhQiIiIiIrIaDChERERERGQ1GFCIiIiIiMhqMKAQEREREZHVYEAhIiIiIiKrwYBCRERERERWgwGFiIiIiIisBgMKERERERFZDQYUIiIiIiKyGgwoRERERERkNRhQiIiIiIjIajCgEBERERGR1WBAISIiIiIiq8GAQkREREREVoMBhYiIiIiIrAYDChERERERWQ0GFCIiIiIishoMKEREREREZDUYUIiIiIiIyGowoBARERERkdVgQCEiIiIiIqvBgEJERERERFaDAYWIiIiIiKwGAwoREREREVkNBhQiIiIiIrIaDChERERERGQ1GFCIiIiIiMhqMKAQEREREZHVYEAhIiIiIiKrwYBCRERERERWgwGFiIiIiIisBgMKERERERFZDQYUIiIiIiKyGgwoRERERERkNRhQiIiIiIjIajCgEBERERGR1WBAISIiIiIiq8GAQkREREREVoMBhYiIiIiIrAYDChERERERWQ0GFCIiIiIishoMKEREREREZDUYUIiIiIiICoOkpLyuwCwMKEREREREBZj42jUU6d8fDh4egEqV1+W8FwMKEREREVEBJLp9G0WGDYN9o0aQ/fknxPfuQbZxY16X9V4MKEREREREBYjo4UMo/Pzg0KABZNu2QaTVGvbJg4KAlJQ8rO79bPK6ACIiIiIiyj7R06eQz58P2dq1ECmVgm10jo4QP3oEbZUqFq7OfAwoRERERET5WWIi5EuWQL5iBUTJyYJNNC4uUE6ciPSOHQGxdd9ExYBCRERERJQfJSdDvnIl5IsWQfTihWATTaVKUE2YAHW3boBEYuECs4YBhYiIiIgoP1EqIVu3DvL58yF+8kSwidbJCarvvkPa118DUqmFC8weBhQiIiIiovxArYZsyxbI586F+OFDwSbaUqWg8vND2sCBgEJh4QJzBgMKEREREZE102gg3bED8p9/huT2bcEmumLFoBo9GqpvvgHs7S1bXw5jQCEiIiIiskZaLWx27YJi5kxIrl4VbKKzs4Nq2DCoRo4Eihe3cIG5w+IB5eLFi1iyZAlWrFiB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+ACqsWOR5usL2NoKtskp/v4qozEoen5+qlw9L1kXBhQiIiKiwkarhfSPPyCfNQuSGzcEm+iKFoVqxAiohg0Diha1SFmvx5mkIDhYjqtXxXBx0cLPT8XxJ4UMAwoRERFRYaHTwWbPHihmzoQkNla4SZEiUH3zDdJGj4bugw8sXODrkMJAUrgxoBAREREVdDodbA4fhnz6dNhERws3kcmQNmAAVH5+0Dk6WrhAov9wSgQiIiKiAkxy8iTsvL1h17mzYDjRSSRI69sXSVFRUM6ebTKcZHYBRS64SFnFKyhEREREBZDk3DnIp0+H9NAhwf06kQjqbt2gmjAB2ipV3nmszC6gyAUXKTt4BYWIiIioABHHxsL2669h7+VlMpyofXyQHBGB1FWr3htOgHcvoJgT7YnexCsoRERERAWA+OZNyGfNgvT33yHS6QTbqFu1gmrSJGg+/TRTx87sAopccJGyg72EiIiIKB8T3buHIqNHw75hQ8h27BAMJ+keHkj++2+k/P57psMJYHqhxJzaTvQmBhQiIiKifEj0779QjB8PB1dXyDZtgkijydAmvX59vPrjD7zaswcaD48sn8vfX3ihRFMLKGa2PdGbeIsXERERUT4iev4csoULIV+1CqKUFME2mtq1oZw0CekdOgAiUbbPmdkFFLngImUHAwoRERFRfvDyJeTLl0O+dClEL18KNtFUrQrV999D3bkzIM7ZG2Uyu4AiF1ykrGJAISIiIrJmKSmQrVkD+YIFECckCDbROjtDOX481D17Ajb8eEf5G3swERERkTVSqSDbtAnyoCCIHz0SbKJ1dITK3x9p/foBck7hSwUDB8kTERERWZP0dEg3b4ZDgwYo8t13guFEW6IEUqdORdK5c0gbMkQwnJizkjtXeydrxCsoRERERNZAq4V0507IZ82C5Pp1wSY6BweoRoyAavhwoGhRk4cyZyV3rvZO1opXUIiIiIjykk4Hmz17YN+kCWx9fQXDia5IEajGjEHS+fNQTZjwznACmLeSO1d7J2vFKyhEREREeUGng014OOTTp8MmKkq4iUyGtP79ofL3h87R0exDm7OSO1d7J2vFHkhERERkYZJTp2Dn4wO7L78UDCc6iQRpffogKTISyjlzMhVOAPNWcudq72StGFCIiIiILEQcEwPbrl1h364dbCIiMuzXiURI69YNyWfOIHXxYugq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bvUoIlKU+ZsUfzP/4itu41Na0oS84cRntZL19NMcW78e59ixCiciInJJAgooDRo04N///ndB9yIiIiF09tT2RqxjBffyL27lVv6Vp95nGGQ9+iiZ//kPJ6dMwXfllcFqVUREirCATvGqUaMGb7zxBitXrqR27dqUKFEi13rDMHjppZcKoj8REQmS+Hgv6elW6rGJEQzlYfzPuFoZ24YbP+mHt27dIHYoIiLFQUAB5YsvvuCyyy7D5/OxZcuWPOsNw8j3xkREJLheeiqdrEFjaMcbWMwGmQAruJchjKTHpLo0rqshiiIikv8CCigffPBBQfchIiIhYuzaReT48TyyaBEGHtOabyNuZYBnJH/WaU5ioksT3kVEpMAEfH/go0ePsm/fPgDKly9PqVKlCqwpEREpeMYff+CYMIGIBQswsrJMa9zXX48rOZmrW7TgA8MAMoPbpIiIFDvnDSjr1q1jzpw5fP/99/h8fx3yv+666+jYsSM33nhjgTYoIiL5yzh8mIjJk3HMmoVx4oRpjaduXZyDB+O+/37QabwiIhJE5wwob7/9NmlpaZQvX562bdty5ZVXYrVa+f333/nyyy/p1asXL7zwAu3atbvoBrKyshgxYgR79uwhOjqavn37sm/fPqZOnYrNZqNx48Z07979orcvIlLYnB6WuGWLhQoV/hqSeL6vd+82TIcrnl6fuecYydET6Zw5kUjfUdN974yoxc4Og2g4pjVYArrRo4iISL7yG1A2b97MxIkTeeSRR3jxxRex2+251j///PNMmTKFf/zjHzRs2JA6depcVANLly4lKiqKefPm8euvvzJ+/HgOHz7MiBEjqFatGl26dOGXX36hZs2aF7V9EZHC5OxhiaeGJAb+de7hiqcc2n2S55hGf8Zy2bGDpvv9lSoMZxgLs57GM8vG3BtP6DoTEREJCb8fj7355ps0aNCAPn365AknABaLhV69etGoUSPeeuuti25gx44dNG3aFICqVauyc+dO4uPjOXr0KG63G5fLhUWf4olIMeFvWOLFiMDFc0xlGzUYTz8uI2842UsFnucf1OZn5tMRz/8+t0pLy78+RERELoTfIygbN24M6NSqhx56iGnTpl10A7Vr12bVqlXcfvvtbNq0iQMHDlC9enUSExMpVaoUNWvW5Kqrrgp4e1u3br3oXiS49LMSM8X9fbFlS6NL3oYVN0+zkGEMpyq/mdYcpAxjGMA0nuMkUXnW//STEVY/i3DqRcKH3hdyNr0nCo9atWr5Xec3oBw8eJDy5cufd+PlypXj0KFDF9cZpwLOjh076NKlC9deey2VKlVi4cKFvPnmm5QrV44pU6awaNEi2rdvH9D2zvViJXxs3bpVPyvJQ++Lv4YlXgwDL4/yNsMZRjw/m9YcJZYJJDGR3hyjpN9t1anjC5ufhd4XYkbvCzmb3hNFh99zp0qVKsX+/fvPu4H9+/dTpkyZi24gPT2dxo0bM3v2bO68806qV69OiRIliIo69YneZZddxrFjxy56+yIihUlSkusinuWjFR+wkQa8STvTcHKCEoylH9XYwQiGnTOcACQmXkwfIiIil87vEZTrrruOZcuW0bJly3Nu4KOPPqJBgwYX3UCVKlUYPHgw8+fPJzY2luTkZDZt2kTPnj2JiIggNjaWoUOHXvT2RUQKk1MXpp8gLe2vu3gB7Ntn5P3a56Pe3n8y2jqEhtn/Nt2eiwgWxXRhauxAfjxwBRUq+IjCy549BnY7uN2n7vh1ervx8V4NYhQRkZDyG1DatWtH586dmT17Np07dzatmTJlCuvXr2fOnDkX3UBcXFyea1hatGhBixYtLnqbIiKFWUJC9nkDgnXNGiJHjsS2ezV48673Wa1kP/EErn79SLjyShIAML+1sIiISDjxG1CuueYaevbsyZQpU1i5ciU333wzFStWxGazsWfPHr744gt27dpFr169qFu3bjB7FhEptiwbNxKZkoJ95UrT9T7DIPuRR3ANGIC3Ro0gdyciInLpzjmo8cknn+Sqq65izpw5LFq0KNck+WuvvZa+ffvSuHHjAm9SRKS4s2zeTOSoUdg/+shvTfYDD+AcNAhvvXpB7ExERCR/nTOgADRv3pzmzZuTkZHB3r178fl8VKxYkbi4uGD0JyJSKF3sNPi9e09dB5KUdOo6EMv27TjGjMH+zjsYZ3xIdKbsO+/ENXgwnuuvD/KrFBERyX/nDSinxcXFKZSIiATgUqfBp6dbGdbpIM1fHUbtbxZieDym+3E3bYozORlP8+b52b6IiEhIBRxQREQkMJcyDb4cfzCIUXRjJo6vs0xr3A0b4kpOxn3HHWAYpjUiIiKFlQKKiEg+27LF74gpv0pziL6M5wWmEM0J0xpP3bo4Bw3C/cADCiYiIlJkKaCIiOSzC5kGH8MxejORJCZQys9tgD3Vq+MaOJDshx8G68VNmRcRESksLvxjPhEROadApsFHcpIkXmYH1RjBMNNwklmmMiemTCFz7Vqy27ZVOBERkWJBR1BERPLZuabBX1nexRPH59AjYxQV2Wv6/D9t5dn6aF/qTmyPx3Hx17OIiIgURgooIiIFIM80eLcb+5tvEjl2LJaMXabP8cbF4erVC3vnztSNjg5SpyIiIuFFAUVEpCB5vdiXLsUxejTWrVtNS3yxsbh69MDVoweUKhXkBkVERMKLAoqIFGuBDFSMj/dy881uVq2yBTx4Mb62h0l3vc8dnw/H+t//mu7bV6IEWZ074+rVC1+ZMkF+5SIiIuFJAUVEiq1AByqmp1tz3ZXr3MMWfdzJP0nZnMxNm9ea7tdnt5PVoQOupCR8FSrkx0sREREpMhRQRKTYupSBimaa8Q2pDOZ2vjJd77NayW7XDme/fviqVMnXfYuIiBQVCigiUmxdzEBFMw35jhSSuZ8Vput9hkF2QgKuAQPw1qyZL/sUEREpqjQHRUSKrfh47yU9vy7/5R0e4Tsa+Q0n/4xtReaqVZycM0fhREREJAAKKCJSbAUyUNFMdbaxkPb8yDU8whLTmk+4hyas5ddJb+CtV+9S2hQRESlWdIqXiBRb5xqoeObX8fFemjd3s+3LvTy2dRQdfPOx4zbd5r8jbqa/J4UDdW4mMdGVexaKiIiInJcCiogUa3kGKpow9u/HkZZGxK/zMXzmR13cDRrgSk4m/s47WWoYQGYBdCsiIlL0KaCIiPiTkYFjyhQcM2dinDhhWuK5+mqcgwbhfvBBMAzTGhEREQmcAoqIyNmOHcMxYwaOqVMxjh41LfFUq4Zr4ECyExLAajWtERERkQungCIiRY6/6fBnT4SPj/eSlHTGdSInTxIxZw6OSZOwHDxoum1v5co4+/Uju107sNuD+KpERESKBwUUESlSzjUd/uyJ8OnpVjp1isLizuCxY3NxvPwyln37TLfrvfxyXElJZHXoAJGRBda/iIhIcaeAIiJFyoVMh7fi5ile567nh1Mie6dpjTcujqwXX8TVpQtER+dTlyIiIuKPAoqIFCmBTIc38PII7zKCodRhC5jcxMsXE4OrRw9czz0HpUoVQKciIiJiRgFFRIqU+HhvrtO4cvPxIMsYyRAa8L15RWQkWZ074+rVC1/ZsgXXqIiIiJjSJHkRKVL8TYe/g3+ymmZ8RCvTcOKz23F17syxjRtxjhypcCIiIhIiOoIiIkXK2dPhHyj9DX2PDqW56wvTeq9hwf1EO5z9+uGrWjW4zYqIiEgeCigiUuQkJGTTtuY6IlNTsX/6qd+6rIQEXAMG4K1VK4jdiYiIyLkooIhIkWL56SciR4/G/sEHfmuy77sP5+DBeOvXD2JnIiIiEggFFBEJO2cOWjQbrmj2eOfnv/HUtpE84VuEFa/pdrNbtMA1eDCeG24I8isSERGRQCmgiEhYOXvQotlwxTMfH0nfS8P0FKYyFztu0226b7oJZ3IynptvLrjGRUREJF8ooIhIWAl00OLl7Gcgo+nODCIxv3OX57rrcCYn477rLjAM0xoREREJLwooIhJWzjdoMY7D9OFlXmQyMRw3rfkvdXnJMoI5X96pYCIiIlLIaA6KiISV+Hjz60diOMZgUthBNQYzyjScbKM6T/Ea1/IDm69uo3AiIiJSCCmgiEhYOXvQYiQn6U0a26lOCkOI40ie5+yiMp2ZRR1+YhFP4cVKYqL5aV8iIiIS3nSKl4iEldODFqe8bNB8ywKGWlIo795j+DfCXgAAIABJREFUWvsH5ZhfYQC77u/ImrUxsMVCvXgPiYmu/21HREREChsFFBEJLx4Pj7sW0+HEWCzeXzG7Y7CvVClcL75IZJcudI+J+d/SzKC2KSIiIgVDAUVEwoPXS+mVK4mZPx/rzz+blvhiYnB1747ruecgLi7IDYqIiEgwKKCISNDlGsRY20P3Kh9x51cjuNq50bTeFxlJ1rPP4urVC99llwW5WxEREQkmBRQRCaozBzG24HNSNifTbPMa01qf3U7WM8/gSkrCd8UVwWxTREREQkQBRUSCasIEBzexhhSSuZPPTWs8WPgwrj13fpWIr2rVIHcoIiIioaTbDItI0Fh++IFx6a1ZQzO/4eRNHqMe/+XRzPkKJyIiIsWQjqCISIGzbNmCY/RoIpYu5QE/NR/yEEMYyQ9cB0C9eE/wGhQREZGwoYAiIgXG2LmTyDFjsL/9NobXfEL8Z9zFEEaylptyLdegRRERkeJJAUVE8p2xZw+Ol18mYuFCDLfbtGZDiab0caXyx9W30ry5m8xvPPz0k0GdOj4NWhQRESnGFFBEJN8Yf/6JIy2NiLlzMVzmR0A8116LMzmZ6nffzXuGwZkDFrdu3UqtWrWC1K2IiIiEIwUUEbl0GRk4pk7FMWMGxvHjpiWe+HicgwbhfughsOj+HCIiImJOAUVELl5mJo6ZM3H84x8YR46YlniuugrXgAFkt20LVmuQGxQREZHCRh9jikgeS5bYadYshrJlS9KsWQxLlthzLbv9Jhs/dZ1JxNUNiExJMQ0nv1OJl66YwfN3/UjjKc9StlzpnG2JiIiI+KMjKCKSy5mT3gHS0605j+1k0Yk5DPlpJJV/2m36/P1czigGMZNuuPZGwhxMtnVCF8GLiIiIKR1BEZFcJkxw5FlmwUN7FvITdXiFblQmbzg5TByDSKU625lML1xE+t1HWlrefYiIiIiAjqCIyFm2bPnrcwsDLw/zHiMYSl02m9YfI4ZJ9GICSRwh7oL3ISIiInImBRQRySU+3kt6uoX7Wc5IhnA9G0zrnDiYxnOMYQB/cvkF70NERETEjAKKiOQy/oFPKZWeQnNWm67PxsZsOpPKYPZQ6aL2oSnxIiIi4o8CiogAYP3Pf4hMSeH+r74yXe81LHxY6in6HhuGo05VRia6gBOkpTnYssVCfLw3J3icuax5czfffGPLVaML5EVERMQfBRSRYs7yww9EpqZi/+QTvzVZf/sbrgEDaBEfzzrgzOnvZmFDAUREREQulgKKSDFl+flnHKNHE/H++35rslu2xDl4MN5rrw1iZyIiIlKcKaCIFDPGzp1Ejh2L/a23MLzmF6u7b7sN5+DBeJo0CXJ3IiIiUtwpoIgUE8bevThefpmIhQsxss1PwVpNUzL6DqH54GZB7k5ERETkFA0jECnijD//JHLwYGIbNsQxd65pONlAAx5gGc35hn7L7wlBlyIiIiKn6AiKSFGVkYFj6lQcM2diZGaalqRzNUMZwXs8jO9/n1doiKKIiIiEkgKKSFGTmYnjlVdwTJmCceSIaYm3alUGZ7/EuD3t8WLNtU5DFEVERCSUFFBEigqnk4h583BMnIjlwAHTEm/Firj69iXrySep9VE03k7WPDUaoigiIiKhpIAiUthlZ2NftIjI8eOx7N5tWuK97DJcvXuT1bEjlCgBnJ5VknfQomaYiIiISCgpoIgUVh4P9nfewTFmDNadO01LfCVL4nrhBVzdukFMTJ71CQnZCiQiIiISVhRQRAobrxfbRx8ROXo01p9+Mi3xRUfj6t4d1/PPQ1xckBsUERERuXgKKCKFhc+H7bPPiExJwfrDD+YlDgdZnTrh6t0b3+WXB7lBERERkUun+4mKFALWf/2L6PvuI/rRR03Diddqw9WxI2+lbuL6L6dQpk4NmjWLYckSOwBLlthp1iyGsmVL5louIiIiEm50BEUkjFnXrcORkoL9yy9N13uw8DpPMdwzjLttlZjVx5GzLj3dSqdOUaxd62LWrLzL4YSuPxEREZGwoyMoImHI8uOPRD3+ODF33eU3nLxNW+qziQ68yg6q8+qrEaZ1/panpTlMl4uIiIiEko6giIQRy9atOEaPJuK99/zWfMwDJDOSjTTMtdzlZ3yJv+WaGC8iIiLhSH+hiIQB49dfKdGjBzE33ug3nLhvuYXMTz6hX90P8oQTAIefAyL+lmtivIiIiIQjBRSREDL27iWyTx9ib7iBiMWLMbx5Q4O7cWMyP/iA4x99hOfGG0lKMj8k8swzWRe0XBPjRUREJBzpFC+REDAOHsQxcSIRc+ZgOJ2mNZ769XEmJ+Nu2RIMI2f5uSbA33ij54KWi4iIiIQbBRSRYDpyBMfUqThmzMDIzDQt8dSujXPQINytWoHF/CCnvwnwF7pcREREJNwooIgEw/HjOF55hYgpU7BkZJiWeKtUwTlgANmPPgo2/a8pIiIixZOuQREpIEuW2Ln9JhsvlZ5PdpWGRI4YYRpOdlORERWmsnDw92Q/8UROONFwRRERESmO9DGtSAF47y1Y03URHzKCK/kdPHlrDnAZoxnIDLrj3FcCuoLXdmp44pIl9v8NUzxFwxVFRESkuNARFJH85PFgf+st7ny+EbPpciqcnMVXsiRTLh9OdbYzkUSclMhZd3p44oQJ5vcG1nBFERERKep0BEUkP/h82D76iMjRo7Fu3kwVk5JMovmH8QI9fuhKYo0qeDDy1JwenuhviKKGK4qIiEhRp792RC6Fz4fts8+Iuf12op9+GuvmzXlKnDiYSC+qs51FdUdCXJzfIYmnl59vvYiIiEhRpYAicpGsq1YRff/9RLdti/X77/Osz8bGTLpSk19IZCIHKJczHNHfsMVA14uIiIgUVQooIhfIun49UX/7GzEPPohtzZo8632GQdZjj7F09Aam1pvGH7ZK1KvnYe7cvy5wT0jIZu7cE9Sr58Fm813wehEREZGiStegiATIsmkTkamp2Fes8FuT3bo1zoED8dapwz3APd3NhzHC+YcnariiiIiIFEcKKCLnYdm6FceYMdjfew/D5zOtyb7nHpyDBuFt0CDI3YmIiIgULSEPKFlZWYwYMYI9e/YQHR1N3759GTVqVM76nTt38uCDD/L888+HsEspjozffiNy7Fjsb7yB4TW/ON198804k5Px3HRTkLsTERERKZpCHlCWLl1KVFQU8+bN49dff2X8+PHMnDkTgN27dzNw4EA6duwY4i6lODH27cMxYQIRCxZgZJufYvV9iSb0daWy++DtJO3OIgGdiiUiIiKSH0IeUHbs2EHTpk0BqFq1Kjt37sxZl5aWxvPPP09UVJSfZ4vkH+PgQRyTJhExezaG02lac6hyfZ75fRTLTj4IGLAZOnWyoQnvIiIiIvkj5Hfxql27NqtWrcLn8/Hjjz9y4MABPB4PW7du5fjx4zRp0iTULUpRd+QIjlGjiG3QAMc//mEaTjy1anFi/nxujf2OZTwEZw1Z1IR3ERERkfxhZGRkmF/1GyRut5spU6awefNmrr32WtavX8+CBQuYMmUKtWvX5t57772g7W3durWAOpWixnLyJOXeeosKr72G7ehR0xpXxYrsefZZDt53H9hs3HRTIzyevBPgrVYv3377XUG3LCIiIlIk1KpVy++6kJ/ilZ6eTuPGjUlMTCQ9PZ19+/YBsG7dOp5++ukL3t65XqyEj61bt4buZ+VyETF/Po60NCz795uWeCtUwNWnD1lPP02ZiAjK/G95fLyX9HRrnvo6dXx67+WDkL4vJGzpfSFm9L6Qs+k9UXSEPKBUqVKFwYMHM3/+fGJjY0lOTgbg4MGDxMXFhbg7KVKys7G/8QaR48Zh+f130xJvmTK4evcm69lnoUSJPOuTklx06pT3mihNeBcRERHJHyEPKHFxcUybNi3P8o8//jgE3UiR5PFgX7IEx5gxWLdvNy3xlSyJ6/nncXXvDrGxfjd16kL4E6SlOdiyxUJ8vJfERJcukBcRERHJJyEPKCIFxufDtmwZkaNGYd282bwkKgpXt25k9eyJr3TpgDarCe8iIiIiBUcBRYoenw/bP/+JIyUF28aN5iUREWR17IgrMRFfuXJBblBERERE/An5bYZF8pP1m2+Ivv9+oh95xDSc+Gw2XB06cOy773COGZMrnCxZYqdZsxjKli1Js2YxLFliD2brIiIiIoKOoEgRYf3uOxwpKdg//9x0vc8wyG7bFtfAgXirVcuzfskSe66L39PTrf97rAGMIiIiIsGkIyhSqFn++1+inniCmDvu8BtOslu1InP1ak7OmmUaTgAmTDAftKgBjCIiIiLBpSMoUihZtm3DMXo09iVLMHzms0az774b5+DBeBs0OO/2tmwxz+r+louIiIhIwVBAkULF+O03IseNw/7GGxgej2mNu3lznMnJeJo2DXi7/gYwxsd7L7pXEREREblw+nhYCgVj3z4i+/Yl9oYbiHj9ddNw4m7UiMylSzm+bNkFhRM4NYDRjAYwioiIiASXjqBIWDMOHcIxaRIRs2djnDxpWuOpVw/n4MG477sPDOOi9qMBjCIiIiLhQQFFwtPRozimTcMxfTrGsWOmJZ6aNXENGkR2mzZgufSDgRrAKCIiIhJ6CigSXo4fJ2LOHByTJmE5fNi0xHvllTj79yf78cfBprewiIiISFGia1AkPLhcRLzyCrENG1Ji2DDTcOItX56T48dzbN06sp966rzhRIMXRURERAofffwsoeV2Y1+8mMhx47D8/rtpibdMGVy9e5PVqRNERZnWnE2DF0VEREQKJwUUCQ2vF/s77+AYPRrr9u2mJb6SJXE99xyu7t2hZMkL2vy5Bi8qoIiIiIiELwUUCS6fD9vHH1N32DCitm0zL4mKwtW1K1kvvICvdOmL2o0GL4qIiIgUTgooEhw+H7bPP8eRkoJtwwbzkogIsv7+d1yJifjKl7+k3WnwooiIiEjhpI+TpcBZV68m+v77iU5IMA0nPquVrGee4dj69TjHjr3kcAIavCgiIiJSWOkIihQY63ff4UhNxf7Pf5qu9xkG2W3b4howAG/16vm6bw1eFBERESmcFFAk31nS04lMTcX+8cd+aw63aIEtNRVv3boF1ocGL4qIiIgUPgookm8s27bhGDMG+7vvYvh8pjXZd92FMzmZbdHR1KpVK8gdioiIiEi4U0CRS2bs2kXkuHHYFy/G8HhMa9zNmuFMTsbTrNmpBVu3BrFDERERESksdJG8XDTjjz+I7NeP2EaNiHjtNdNw8mPkDdxr+YTrDn/F23tvu6j9aCK8iIiISPGhIyhywYxDh3BMnkzErFkYJ0+a1hyqXI+//57Kh85WgAGboVMnGxc6yV0T4UVERESKFx1BkcAdPYpjzBhiGzTAMXmyaTjx1KjBiblzuTV2Ax/SGjByrU9LM5/w7s+5JsKLiIiISNGjIyhyfidOEDFnDo5Jk7AcOmRa4q1cGWf//mS3awc2Gz91MX9rXegkd02EFxERESleFFDEP5eLiFdfxTFhApY//jAt8ZYvjyspiaxnngHHX0c18muSuybCi4iIiBQv+hha8nK7sb/2GrGNGlGiXz/TcOItXZqTI0ZwbMMGsrp0yRVOIP8muWsivIiIiEjxoiMo8hevF/t77+EYPRrrtm2mJb7YWFzPPYerRw8oWdLvpvJrkrsmwouIiIgULwooAj4ftuXLiUxNxZqebl5SogRZXbrgevFFfGXKBLTZ/JrkronwIiIiIsWHAkpx5vNh++ILHCkp2L77zrwkIoKsDh1wJSXhK18+yA2KiIiISHGjgFJMWdesIXLkSGyrV5uu91mtZD/5JM6+ffFdeWWQuxMRERGR4koBpZixbtiAIzUV+8qVput9hkH2I4/gGjAAb40aQe5ORERERIo7BZRiwrJ5M5GpqdiXLfNbk/3ggzgHDsRbr14QOxMRERER+YsCShFn2b4dx5gx2N95B8PnM63JvvNOXMnJeBo2DHJ3IiIiIiK5KaAUUcbvvxM5bhz2RYswPB7TGnfTpjiTk/E0bx7k7kREREREzCmgFDHG/v04JkwgYv58jKws0xp3w4a4kpNx33EHGEaQOxQRERER8U8BpYgwDh8mYvJkHLNmYZw4YVrjqVsX56BBuB94QMFERERERMKSAkphd/QojhkzcEybhnH0qGmJp0YNXAMHkv23v4HVGuQGRUREREQCp4BSWJ04QcTcuTgmTsRy6JBpibdyZZz9+pH9xBNg049aRERERMKf/motbLKyiHj1VRwTJmDZt8+0xFuuHK6kJLI6dACHI7j9iYiIiIhcAgWUwsLtxv7mm0SOHYtl1y7TEm/p0rh69SKrc2eIigpygyIiIiIil04BJdx5vdjffx/H6NFYf/nFtMQXG4urRw9cPXpAqVJBblBEREREJP8ooIQrnw/bihVEpqZi/e9/zUtKlCCrc2dcvXrhK1MmyA2KiIiIiOQ/BZRw4/Nh+/JLHCkp2NavNy+x28nq0AFXUhK+ChWC3KCIiIiISMFRQAkj1m+/JXLkSGzffGO63me1kv3EEzj79sVXpUqQuxMRERERKXgKKGHAsnEjkamp2D/7zHS9zzDITkjANWAA3po1g9ydiIiIiEjwKKCEkGXzZiJHjcL+0Ud+a7Lvvx/n4MF469ULYmciIiIiIqGhgBIClh07cIwejf2ddzB8PtOa7DvuwJWcjOf664PcnYiIiIhI6CigBJHx++9Ejh+P/fXXMTwe0xp306Y4k5PxNG8e5O5ERERERELPEuoGigNj/34iBwwgtlEjIl591TScuBs04Pi773J8+fKghJMlS+w0axZD2bIladYshiVL7AW+TxERERGR89ERlAJkHD5MxJQpOF55BePECdMaz9VX4xw0CPeDD4JhBKWvJUvsdOr016T59HTr/x6fICEhOyg9iIiIiIiYUUApCMeO4ZgxA8fUqRhHj5qWeKpVwzVwINkJCWC1BrW9CRMcpsvT0hwKKCIiIiISUgoo+enkSSLmzMExaRKWgwdNS7yVK+Ps14/sdu3AHprTqrZsMT+zz99yEREREZFgUUDJRyUGDCDi1VdN13nLlcOVmEhWhw4QGRncxs4SH+8lPT3vUZv4eG8IuhERERER+Ys+Ms9Hrh498Flyf0u9cXGcfOkljm3YQFa3biEPJwBJSS7T5YmJ5stFRERERIJFASUfeePjyX70UQB8MTE4+/Xj2Pffk9WrF0RHh7i7vyQkZDN37gnq1fNgs/moV8/D3Lm6QF5EREREQk+neOUz54AB+C6/HFevXvjKlg11O34lJGQrkIiIiIhI2FFAyWe+q67COXJkqNsQERERESmUdIqXiIiIiIiEDQWUfKLJ7CIiIiIil06neOUDTWYXEREREckfOoKSD841mV1ERERERAKngJIPNJldRERERCR/6C/ofOBvArsms4uIiIiIXBgFlHygyewiIiIiIvlDASUfaDK7iIiIiEj+0F288okms4uIiIiIXDodQRERERERkbChgCIiIiIiImFDAUVERERERMKGAoqIiIiIiIQNBRQREREREQkbCigiIiIiIhI2FFBERERERCRsKKCIiIiIiEjYUEAREREREZGwoYAiIiIiIiJhQwFFRERERETChgKKiIiIiIiEDQUUEREREREJGwooIiIiIiISNhRQREREREQkbBgZGRm+UDchIiIiIiICOoIiIiIiIiJhRAFFRERERETChgKKiIiIiIiEDQUUEREREREJGwooIiIiIiISNhRQREREREQkbCigiIiIiIhI2FBAkZDIzMwkMTGRrl270rFjR3744YdQtyRh5IsvviA5OTnU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V7n66qsBuP7662nfvj3r16+natWqnDx5ksTERFq2bJmz/vTr2L9/P+XLlz/v92vbtm188cUXJCYm8vjjjwNw00038cQTT3D06NEL+t7/8ssv1KpVi9GjRxMTEwOcOkL073//m++++y5XQImKimLixInYbKf+ST158iTDhw/np59+on79+jnfz/j4+JyvzyWQn+vOnTs5fPgwjz/+OA0aNADg6quvZv78+bhcrgt6rSIi4UZ38RIRCVOxsbE54QTI+VT82LFjAKxbt464uDiuueYa3G53zn+33HILv/32G3v37uW7774DyPnD/7S7774bq9XK+vXrc5bFxMTk+gN63bp1+Hw+br311lzbv/XWW/F4PPznP/8J6HVs3LiRChUq5IQTALvdzptvvsljjz2G3W5n8uTJtGzZkv3797Nu3Tree+89Vq1aBUB2dnZA+9mwYQNATuACsFqt3HPPPQE9/0w33XQTs2bNIjIyku3bt/P1118zb948Dh06RFZWVq7aunXr5oQTIOco0smTJy94vxDYz7VGjRqUKVOGpKQkUlNTWblyJTabjd69e1O9evWL2q+ISLjQERQRkTBVokSJXI9Pn+bk9XoByMjIICMjg2bNmpk+/8CBAzlHDsqWLZtrnc1mo1SpUmRmZuYsi4qKylWTkZEBwJNPPul3+4HIyMigdOnS56xZs2YNEydOZOfOnURHR1OzZs2cfgKdH3L6tZ69r0COvpyt4X0aAAAE6ElEQVTN6/Uyffp03n33XU6cOEG5cuWoV68eDocjT+3p61FOs1gsF9T32QL5uV5xxRXMnj2b+fPn8+WXX/LBBx9gt9tp0aIF/fv3JzY29qL2LSISDhRQREQKqZiYGCpVqkRqaqrp+qpVq/Lzzz8Dpy5SP/MOYm63myNHjlCqVCm/2z/9R+7UqVNzTnM60+lTuwLpc9euXXmWb9q0icjISCIjI+nXrx8333wzaWlpVKpUCcMwePfdd1mzZk1A+4BTd0UDOHToUK5rMI4cOZKrzjAMPP/f3t2Fsv/FcQB/2660PKWFsrXkZjNpHi/IBaU8ReJCaqNouZAbT+Wh1JJy4WJsM8ssTTQ3okQTJXZD4cZDcUORlFnKLFu/i3++/+b/j/1+9aup96t28T2d77fTOTfns3M+5wSDYWWfVzscDgecTicGBgZQVlYm9EVra2vE7flTkYwrAMhkMoyMjCAUCuH8/Bzb29twOp2Ij49HX1/fX28nEdHfwi1eREQ/VG5uLh4eHpCYmAiVSiX8Tk9PYbfbIRKJhFOyNjc3w97d2tpCMBgU8hf+z0f+w9PTU9j3/X4/zGYzHh8fAfyzjeorGo0Gd3d3uLi4EMre398xODgIl8uFs7MzvL29QavVIj09XVgpOjg4APDvitF38vPzERMTA7fbHVa+t7cX9iyRSODz+eD3+4Wyk5OTsDonJydQKBSoq6sTgpOHhwdcXV1F3J4P3/XPZ5GMq9vtRkVFBR4fHyESiaBSqdDV1QWFQhF2ISQR0U/EFRQioh+qtrYWLpcLXV1daGtrQ1paGo6OjmC321FVVYXY2FhkZGSguroaNpsNgUAAeXl5uLy8xOzsLDQaTdixtZ9lZmaisrIS4+PjuL+/R1ZWFm5vb2GxWJCQkCDkx3xM4Dc3N6FWq/9zglRNTQ2Wl5fR29sLvV6P5ORkrKys4Pn5Gc3NzRCLxRCLxTCbzWhpaUEgEMD6+jr29/cBICyQ+IpcLkdDQwOsVitCoRCUSiW2traE3JQPJSUlWF5ehsFgQH19Pa6urrC4uBh2UphKpYLH44HD4UB2djZubm4wPz+PQCDw27klH/2zs7OD4uJiKBSKL+tHMq45OTkIBoPo6emBTqdDXFwcPB4Prq+vodVqf6t9RETRhgEKEdEPFRsbC6vViunpaUxNTeHl5QUpKSno6OgIm6QODQ1BJpNhbW0NCwsLkEqlaGpqQnt7+7f/7g8PD8PhcGB1dRUzMzNISkpCaWkp9Hq9cOt9eXk5NjY2MDo6irq6OvT394d9QyKRYGZmBkajEZOTkwgGg1AqlTCZTMJk3WAwYHZ2Fj09PYiPj4darYbZbEZnZyeOj48jvgult7dXCIB8Ph+Ki4vR2NgIl8sl1CkqKkJ3dzeWlpawu7sLpVKJiYkJ6HQ6oU5rayuen5+xtLQEm82G1NRUVFZWQiQSYW5uDl6vV9hS9p3CwkIUFBTAZDLh8PAQk5OTX9aPZFylUimMRiMsFgvGxsbw+voKuVyOoaEhVFVVRdQuIqJoFeP1ev8si4+IiOgHsFqtsNlswkWNREQU3ZiDQkREREREUYMBChERERERRQ1u8SIiIiIioqjBFRQiIiIiIooaDFCIiIiIiChqMEAhIiIiIqKowQCFiIiIiIiiBgMUIiIiIiKKGgxQiIiIiIgoavwCpKn3QJ6W6YoAAAAASUVORK5CYII=
">
                </div>

            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[5]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="n">sns</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">rc</span><span class="o">=</span><span class="p">{</span><span class="s2">&quot;figure.figsize&quot;</span><span class="p">:</span> <span class="p">(</span><span class="mi">12</span><span class="p">,</span> <span class="mi">8</span><span class="p">)})</span>
<span class="n">plt</span><span class="o">.</span><span class="n">style</span><span class="o">.</span><span class="n">use</span><span class="p">(</span><span class="s1">&#39;fivethirtyeight&#39;</span><span class="p">)</span>

<span class="c1"># Plot the CDFs</span>
<span class="n">x</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">ecdf</span><span class="p">(</span><span class="n">temp</span><span class="p">)</span>

<span class="c1"># draw 100,000 random samples from a normal distribution</span>
<span class="n">nm_temp</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">normal</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">temp</span><span class="p">),</span> <span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">temp</span><span class="p">),</span> <span class="mi">100000</span><span class="p">)</span>
<span class="n">nm_x</span><span class="p">,</span> <span class="n">nm_y</span> <span class="o">=</span> <span class="n">ecdf</span><span class="p">(</span><span class="n">nm_temp</span><span class="p">)</span>

<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">marker</span><span class="o">=</span><span class="s1">&#39;.&#39;</span><span class="p">,</span> <span class="n">linestyle</span><span class="o">=</span><span class="s1">&#39;none&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">nm_x</span><span class="p">,</span> <span class="n">nm_y</span><span class="p">)</span>

<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Temperature (F)&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;CDF&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Fig. 1.3: Cumulative Distribution Function - Human Body Temperatures&#39;</span><span class="p">)</span>
<span class="n">margins</span> <span class="o">=</span> <span class="mf">0.02</span>

<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">();</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>




                <div class="output_png output_subarea ">
                    <img src="data:image/png;base64,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M2bM0LZt23TWWWfZXWbCy8nJ0WeffSZJWrZsmXr16qUePXro008/lWEY2rlzpwzDIEDaqLoxQuRxofspaN26te644w49/fTTSk9P1x/+8Adt2rRJv/vd75SUlKR27drxSa/Nqhuj/fv3669//atCoZBatGihKVOm2F1mQqtujCRp7969HJyjQHXj8+WXX2rKlCnyer1KT0/XtGnT7C4zoVU3Rp988ol+/etfKykpSaNGjVKHDh3sLjPh3Xzzzbr33nsVCATUrl07DRs2TC6XS7169dL48eNlGIZuv/12u8tMaNWNESLP4fP5TLuLAAAAAJC4mL4FAAAAwFaEEgAAAAC2IpQAAAAAsBWhBAAAAICtCCUAgJhjmtyjBQDiCbcEBoAo96c//Unz58+vcZ/mzZvrrbfeilBF9iosLNT06dP11FNP2V2KJOmvf/2rUlNTNWnSJG3dulUXX3zxcfc9PE579+7V1Vdfraeeekqnn356BKsFgOhEKAGAKDd+/HiNHTs23H7yySdVWFioBx54INzn9XrtKM0W7733nr766iu7y5AkrVy5Uh9++KFeffVVS/+1116rgQMHVtn/8Dg1adJEl156qe6++279/e9/l8PhiEi9ABCtCCUAEOWys7OVnZ0dbmdmZsrr9ap79+42VgXTNPXQQw/psssuU4MGDSzbsrOzTzg+l156qebMmaMPP/xQQ4cOrc9SASDqcU0JAMSZL774QhMnTtSgQYM0fPhwTZs2TXv27AlvX7lypfr166eVK1fqhhtu0KBBg3TRRRfp7bff1p49e3T77bdr8ODBGj16tF588cUqj1u+fLmuv/56DRo0SBdffHGVswSGYWjOnDkaO3asBg4cqLFjx+qFF16w7DNt2jRNmTJF9913n4YOHaqLL75YwWBQ+/fv1/3336+8vDydffbZGj58uH73u99px44dkqRZs2bp2WefVSgUUr9+/fTPf/5TwWBQ/fr10xNPPGF5jUcffVQDBgw44WvWpt7qLF26VN99951GjRpV+8E5SnJysoYMGaI5c+ac0uMBIJ5wpgQA4sjnn3+uyZMnq0+fPrr33nt18OBBPfHEE5o4caKeffZZpaSkhPf94x//qKuuukrXXHONnnnmGd13333Kzs7WiBEjdMkll+jll1/WQw89pB49euiMM84IP+4Pf/iD8vLydO211+rDDz8MTyMbN26cJGn69OmaN2+err76avXs2VNr1qzRI488Ip/Pp0mTJoWfZ/Xq1erfv78eeOABlZaWyuVy6eabb1ZZWZmmTJmiJk2aqKCgQI8//rjuv/9+zZw5U2PHjtXOnTu1cOFCPfHEE2rWrNlJ/fc59jXdbrfuu+++WtV7rHfeeUc9evRQ06ZNq2wzDEPBYLBKv9ttPewOHz5c8+bN05YtW9SmTZuT+lkAIJ4QSgAgjjz66KNq3bq1HnroofAfwL169dK4ceP02muv6Ve/+lV437y8PF1xxRWSpKSkJF1//fXq2rWrJkyYIElq3769PvroI61bt84SSs477zzdcsstkqQBAwZo9+7dmj17ti6++GJt2bJFb7zxhiZNmqRf//rXkqT+/fvL6/XqySef1CWXXKKsrCxJUigU0u9///twsNi1a5dSU1N16623qlevXpKkPn366Pvvv9e8efMkSc2aNQs//vD0qOr++D+eY19z8+bNta73WKtXr9bo0aOr3XbPPffonnvuqdK/cuVKS7tLly6SpFWrVhFKACQ0QgkAxImysjJ99dVXuvLKKyUd+WO9adOm6tSpk1asWGEJJT169Ah/37hxY0lSt27dwn0ZGRmSpIMHD1pe59jpSsOGDdMnn3yi77//XqtWrZIkDR482BIWBg8erMcee0yfffZZ+PEZGRmWMx3NmjXTrFmzZJqmtm/frq1bt2rLli1av369/H7/Kf5XsTr2NU+m3qOVlJTowIEDat68ebWvc9111+mcc845YT2ZmZlKSUkJT08DgERFKAGAOFFcXCzTNPXcc8/pueeeq7K9Xbt2lnZqamqVfY69YLs6x05XatSoUfj1fT6fJOkXv/hFtY/dvXt3+Pujp5IdNn/+fM2aNUu7d+9Ww4YN1blzZyUnJ5+wpto69jVPpt6jlZSUSKo8w1SdFi1aqGvXrrWqKTk5WaWlpbXaFwDiFaEEAOJEWlqaJOnyyy/XyJEjq2w/3h/QJ6u4uNhyN7B9+/ZJqjzbkp6eLkn6xz/+UW3oqO76i8M+++wz3X333brssst05ZVXhvd96KGHtG7duuM+7vDtdA3DsPQfOnTohD/LqdabmZkp6Ug4+W8cPHgwfFYKABIVd98CgDiRnp6uTp06acuWLeratWv4q1OnTpo9e7Y+/fTTOnmdjz76yNJevHixWrZsqezsbPXu3VtS5RmIo2soKyvTrFmzwgGmOuvWrZNpmpowYUI4DASDwfB1GIdDh9NpPXS5XC4lJydXOatRU5A57FTrTU5OVqNGjbRr164TvkZN9u/fr0AgcNxpYACQKDhTAgBxZNKkSfrtb3+rP/7xjxo1apQMw9BLL72kL774QpdffnmdvMbcuXPl9Xp1xhln6IMPPtDy5cv1l7/8RZLUuXNnjRw5Uvfee69++OEHdenSRVu3btWsWbPUpEmTKlPIjnb4YvoHH3xQo0ePVnFxsV555RV9++23kirPfKSmpqphw4YKhUJatGiRzjjjDLVo0ULnnHOOFi1apG7duik7O1tvv/12rQLDf1Nv//79tXbt2pP5T1fFmjVrws8FAImMMyUAEEcGDhyomTNnateuXZo6daruvPNOGYahmTNn6swzz6yT17jlllv08ccf67bbbtOGDRt0//33a/jw4eHtd911ly6//HK98cYbuummm/TUU09p6NCh+sc//iGPx3Pc5+3Xr59++9vfau3atbrllls0Y8YMZWdn6/7775d05A/4ESNGKDc3V3feeafmzp0rSbr11ls1cOBAzZgxQ//7v/+rjIyM8F3ETuRU6x0+fLgKCwtVVFRUq9epzrJly3TGGWdwpgRAwnP4fD7T7iIAANFv5cqVmjx5smbNmqU+ffrYXY7tTNPUFVdcoWHDhum666476ceXlpbqwgsv1N13363BgwfXQ4UAEDs4UwIAwCnTXgLUAAAAeklEQVRwOByaMmWKXnvttVO6e9Yrr7yinJwcAgkAiFACAMApGzBggM4991w988wzJ/W4PXv26LXXXtNdd91VL3UBQKxh+hYAAAAAW3GmBAAAAICtCCUAAAAAbEUoAQAAAGArQgkAAAAAWxFKAAAAANiKUAIAAADAVv8f9NdkckF5qHQAAAAASUVORK5CYII=
">
                </div>

            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <div class="alert alert-block alert-success">
                <h4>Analysis:</h4> The histogram (Fig. 1.1) shows that the sample's distribution is unimodal and essentially
                symmetrical about the mean. The QQ plot (Fig.1.2) and the CDF (Fig. 1.3), also show that the frequency distribution
                of the data is very close to normal, although the QQ plot and the CDF both show some variation and a couple
                of outliers on both tails.
            </div>
        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h3 id="Question-#2">Question #2</h3>
            <hr>
            <p>Is the sample size large? Are the observations independent?</p>
            <ul>
                <li>Remember that this is a condition for the Central Limit Theorem, and hence the statistical tests we are using,
                    to apply.</li>
            </ul>

        </div>
    </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[6]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>&lt;class &#39;pandas.core.frame.DataFrame&#39;&gt;
RangeIndex: 130 entries, 0 to 129
Data columns (total 3 columns):
temperature    130 non-null float64
gender         130 non-null object
heart_rate     130 non-null float64
dtypes: float64(2), object(1)
memory usage: 3.1+ KB
</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <div class="alert alert-block alert-success">
                <h4>Analysis:</h4>The sample size is not large as a fraction of all human beings, but it is large enough for
                the Central Limit Theorem to apply.

                <blockquote cite="Boslaugh, Sarah. Statistics in a Nutshell: A Desktop Quick Reference (p. 59). O'Reilly Media. Kindle Edition.">
                    <p>The central limit theorem states that the sampling distribution of the sample mean approximates the normal
                        distribution, regardless of the distribution of the population from which the samples are drawn if
                        the sample size is sufficiently large. This fact enables us to make statistical inferences based
                        on the properties of the normal distribution, even if the sample is drawn from a population that
                        is not normally distributed.</p>
                </blockquote>

                <p>The definition of the central limit theorem reads that the sample size must be 'sufficiently large', but
                    fails to define 'sufficiently large'. A commonly-accepted rule of thumb is that a sample size of 30 constitutes
                    'sufficiently large'. However, if the population from which the samples are drawn is unimodal and symmetric
                    about the mean, a sample size of less than 30 may be sufficient. Conversely, if the population is multi-modal
                    or skewed, a sample size of more than 30 would be required.</p>

                <p> The 130 observations is a tiny fraction of the population of all humans, but, as shown in the analysis of
                    Question #1, the data is unimodal and essentially symmetric about the mean, so, a sample size of 130
                    is more than sufficient to satisfy the 'sufficiently large' requirement of the central limit theorem.
                </p>

                <p>For the observations to be independent it would mean that knowing the outcome of one sample would provide
                    no information about another sample. In this case, knowing one person's body temperature gives no information
                    about any other measured body temperature. Gender or heart rate may have an affect on body temperature.
                    The effects of gender on mean body temperature are explored below.</p>
            </div>
        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h3 id="Question-#3">Question #3</h3>
            <hr>
            <p>Is the true population mean really 98.6 degrees F?</p>
            <ol>
                <li> First, try a bootstrap hypothesis test.</li>
                <li> Now, let's try frequentist statistical testing. Would you use a one-sample or two-sample test? Why?</li>
                <li> In this situation, is it appropriate to use the $t$ or $z$ statistic?</li>
                <li> Now try using the other test. How is the result be different? Why?</li>
            </ol>

        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <div class="alert alert-success">
            <p>
                <h4>Hypotheses:</h4>
                <br> $H_0:\ \bar x =$ 98.6°
                <br> $H_a:\ \bar x \neq$ 98.6°</p>
            </div>
        </div>
    </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[7]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt output_prompt">Out[7]:</div>



                <div class="output_html rendered_html output_subarea output_execute_result">
                    <div>
                        <style>
                            .dataframe thead tr:only-child th {
                                text-align: right;
                            }

                            .dataframe thead th {
                                text-align: left;
                            }

                            .dataframe tbody tr th {
                                vertical-align: top;
                            }
                        </style>
                        <table border="1" class="dataframe">
                            <thead>
                                <tr style="text-align: right;">
                                    <th></th>
                                    <th>temperature</th>
                                    <th>heart_rate</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <th>count</th>
                                    <td>130.000000</td>
                                    <td>130.000000</td>
                                </tr>
                                <tr>
                                    <th>mean</th>
                                    <td>98.249231</td>
                                    <td>73.761538</td>
                                </tr>
                                <tr>
                                    <th>std</th>
                                    <td>0.733183</td>
                                    <td>7.062077</td>
                                </tr>
                                <tr>
                                    <th>min</th>
                                    <td>96.300000</td>
                                    <td>57.000000</td>
                                </tr>
                                <tr>
                                    <th>25%</th>
                                    <td>97.800000</td>
                                    <td>69.000000</td>
                                </tr>
                                <tr>
                                    <th>50%</th>
                                    <td>98.300000</td>
                                    <td>74.000000</td>
                                </tr>
                                <tr>
                                    <th>75%</th>
                                    <td>98.700000</td>
                                    <td>79.000000</td>
                                </tr>
                                <tr>
                                    <th>max</th>
                                    <td>100.800000</td>
                                    <td>89.000000</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h4 id="3.1-bootstrap-hypothesis-test---100,000-samples">3.1 bootstrap hypothesis test - 100,000 samples
                <a class="anchor-link" href="#3.1-bootstrap-hypothesis-test---100,000-samples">&#182;</a>
            </h4>
        </div>
    </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[8]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># bootstrap hypothesis test with 100,000 samples</span>
<span class="n">bs_replicates</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">(</span><span class="mi">100000</span><span class="p">)</span>

<span class="n">size</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">bs_replicates</span><span class="p">)</span>

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">size</span><span class="p">):</span>
    <span class="n">bs_sample</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">choice</span><span class="p">(</span><span class="n">temp</span><span class="p">,</span> <span class="nb">len</span><span class="p">(</span><span class="n">temp</span><span class="p">))</span>
    <span class="n">bs_replicates</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">bs_sample</span><span class="p">)</span>
    
<span class="n">p</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">bs_replicates</span> <span class="o">&gt;=</span> <span class="mf">98.6</span><span class="p">)</span> <span class="o">/</span> <span class="n">size</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;p-value: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">p</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;mean: </span><span class="si">{:0.5}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">bs_replicates</span><span class="p">)))</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>p-value: 0.0
mean: 98.249
</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <div class="alert alert-block alert-success">
                <h4>Analysis:</h4> After 100,000 samples, the p-value is 0.0, indicating that the null hypothesis should be rejected.
                The mean body temperature of the sample set is 98.25°.
            </div>
        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h4 id="3.2-frequentist-statistical-testing">3.2 frequentist statistical testing
                <a class="anchor-link" href="#3.2-frequentist-statistical-testing">&#182;</a>
            </h4>
            <p>Now, let's try frequentist statistical testing. Would you use a one-sample or two-sample test? Why?</p>

        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <div class="alert alert-block alert-success">
                <h4>Analysis:</h4> When comparing the mean of a single sample to a population with an hypothesised mean, a one-sample
                $t$-test is appropriate.
            </div>
        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h4 id="3.3-/-3.4-$t$--or-$Z$--statistic?">3.3 / 3.4 $t$- or $Z$- statistic?
                <a class="anchor-link" href="#3.3-/-3.4-$t$--or-$Z$--statistic?">&#182;</a>
            </h4>
        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <p>In this situation, is it appropriate to use the $t$- or $Z$-statistic?</p>

        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <div class="alert alert-block alert-success">
                <h4>Analysis:</h4>
                <p>
                    $$Z-statistic = Z = \frac{\bar x - \mu}{\frac{\sigma}{\sqrt n}}$$
                </p>
                <p>
                    $$t-statistic = t = \frac{\bar x - \mu}{\frac{s}{\sqrt n}}$$
                </p>
                <p>The formula for the $Z$-statistic requires the population standard deviation, which is unknown. The $t$-statistic
                    requires only the sample standard deviation, which can be derived. Without knowing the population standard
                    deviation, the only choice is to use the $t$-statistic.</p>
                <p>A two-tailed test is required, since the alternative hypothesis is that there is a statistically-significant
                    difference between the sample mean and the hypothetical population mean of 98.6°, rather than testing
                    whether the actual mean temperature is greater than or less than the hypothesized 98.6°.</p>
            </div>
        </div>
    </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[9]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="n">t_stat</span> <span class="o">=</span> <span class="n">stats</span><span class="o">.</span><span class="n">ttest_1samp</span><span class="p">(</span><span class="n">temp</span><span class="p">,</span> <span class="mf">98.6</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;t-score: </span><span class="si">{}</span><span class="se">\n</span><span class="s1">p-value: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">round</span><span class="p">(</span><span class="n">t_stat</span><span class="o">.</span><span class="n">statistic</span><span class="p">,</span> <span class="mi">5</span><span class="p">),</span> <span class="nb">round</span><span class="p">(</span><span class="n">t_stat</span><span class="o">.</span><span class="n">pvalue</span><span class="p">,</span> <span class="mi">5</span><span class="p">)))</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>t-score: -5.45482
p-value: 0.0
</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt"></div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h3 id="Question-#4">Question #4</h3>
            <hr>
            <p>Draw a small sample of size 10 from the data and repeat both frequentist tests.</p>
            <ul>
                <li> Which one is the correct one to use?</li>
                <li> What do you notice? What does this tell you about the difference in application of the $t$ and $z$ statistic?</li>
            </ul>
        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h4 id="$t$-test">$t$-test
                <a class="anchor-link" href="#$t$-test">&#182;</a>
            </h4>
        </div>
    </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[10]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="n">sample_temp</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">choice</span><span class="p">(</span><span class="n">a</span> <span class="o">=</span> <span class="n">temp</span><span class="p">,</span> <span class="n">size</span><span class="o">=</span><span class="mi">10</span><span class="p">)</span>
</pre>
                </div>

            </div>
        </div>
    </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[11]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="n">r</span> <span class="o">=</span> <span class="n">stats</span><span class="o">.</span><span class="n">ttest_1samp</span><span class="p">(</span><span class="n">sample_temp</span><span class="p">,</span> <span class="mf">98.6</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;t-score: </span><span class="si">{:0.4}</span><span class="se">\n</span><span class="s1">p-value: </span><span class="si">{:0.4}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">r</span><span class="o">.</span><span class="n">statistic</span><span class="p">,</span> <span class="n">r</span><span class="o">.</span><span class="n">pvalue</span><span class="p">))</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>t-score: -1.546
p-value: 0.1565
</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt"></div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <div class="alert alert-block alert-success">
                <h4 id="Analyis">Analysis</h4>
                <p>Again, since the population standard deviation is unknown, the $t$-test is the only option available. The p-value is greater than 0.05, so the null hypothesis cannot be rejected on the basis of this test.</p>
            </div>
        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt"></div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h3 id="Question-#5">Question #5</h3>
            <hr>
            <p>At what temperature should we consider someone's temperature to be "abnormal"?</p>
            <ul>
                <li> As in the previous example, try calculating everything using the boostrap approach, as well as the frequentist approach.</li>
                <li> Start by computing the margin of error and confidence interval. When calculating the confidence interval,keep in mind that you should use the appropriate formula for one draw, and not N draws.</li>
            </ul>
        </div>
    </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[12]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># get the sample mean and standard deviation for use with bootstrap and frequentist approaches below</span>
<span class="n">x_bar</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">temp</span><span class="p">)</span>
<span class="n">s</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">temp</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;sample mean: </span><span class="si">{:0.4}</span><span class="se">\n</span><span class="s1">sample standard deviation: </span><span class="si">{:0.4}</span><span class="se">\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">x_bar</span><span class="p">,</span> <span class="n">s</span><span class="p">))</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>sample mean: 98.25
sample standard deviation: 0.7304

</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h4 id="Bootstrap">Bootstrap
                <a class="anchor-link" href="#Bootstrap">&#182;</a>
            </h4>
        </div>
    </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[13]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># Calculates p value using 100,000 boostrap replicates</span>
<span class="n">bootstrap_replicates</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">(</span><span class="mi">100000</span><span class="p">)</span>

<span class="n">size</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">bootstrap_replicates</span><span class="p">)</span>

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">size</span><span class="p">):</span>
    <span class="n">bootstrap_sample</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">choice</span><span class="p">(</span><span class="n">temp</span><span class="p">,</span> <span class="n">size</span><span class="o">=</span><span class="nb">len</span><span class="p">(</span><span class="n">temp</span><span class="p">))</span>
    <span class="n">bootstrap_replicates</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">bootstrap_sample</span><span class="p">)</span>

<span class="n">p</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">bootstrap_replicates</span> <span class="o">&gt;=</span> <span class="mf">98.6</span><span class="p">)</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">bootstrap_replicates</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;p-value: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">p</span><span class="p">))</span>

<span class="n">x_bar</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">bootstrap_replicates</span><span class="p">)</span>
<span class="n">ci</span> <span class="o">=</span> <span class="n">stats</span><span class="o">.</span><span class="n">norm</span><span class="o">.</span><span class="n">interval</span><span class="p">(</span><span class="mf">0.95</span><span class="p">,</span> <span class="n">loc</span><span class="o">=</span><span class="n">x_bar</span><span class="p">,</span> <span class="n">scale</span><span class="o">=</span><span class="n">s</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;95</span><span class="si">% c</span><span class="s1">onfidence interval: </span><span class="si">{:0.5}</span><span class="s1"> - </span><span class="si">{:0.5}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">ci</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="n">ci</span><span class="p">[</span><span class="mi">1</span><span class="p">]))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;margin of error: +/-</span><span class="si">{:0.5}</span><span class="se">\n\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">((</span><span class="n">ci</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span> <span class="o">-</span> <span class="n">x_bar</span><span class="p">)))</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>p-value: 0.0
95% confidence interval: 96.818 - 99.681
margin of error: +/-1.4315


</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h4 id="Frequentist-Approach">Frequentist Approach
                <a class="anchor-link" href="#Frequentist-Approach">&#182;</a>
            </h4>
            <p>Confidence Interval for One-Sample t-Test $$CI_{1-\alpha} = \bar x \pm \left(t_{\frac{\alpha}{2}df}\right)\left(\frac{s}{\sqrt
                n}\right)$$
            </p>

        </div>
    </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[14]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># frequentist approach - confidence interval for the one-sample t-test</span>

<span class="c1"># alpha = 0.05, confidence coefficient = 95%</span>

<span class="c1"># confidence interval for one draw</span>
<span class="n">ci_low_f</span><span class="p">,</span> <span class="n">ci_high_f</span> <span class="o">=</span> <span class="n">stats</span><span class="o">.</span><span class="n">norm</span><span class="o">.</span><span class="n">interval</span><span class="p">(</span><span class="mf">0.95</span><span class="p">,</span> <span class="n">loc</span><span class="o">=</span><span class="n">x_bar</span><span class="p">,</span> <span class="n">scale</span><span class="o">=</span><span class="n">s</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;95</span><span class="si">% c</span><span class="s1">onfidence interval: </span><span class="si">{:0.5}</span><span class="s1"> - </span><span class="si">{:0.5}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">ci_low_f</span><span class="p">,</span> <span class="n">ci_high_f</span><span class="p">))</span>

<span class="c1"># margin of error </span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;margin of error: +/-</span><span class="si">{:0.5}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">((</span><span class="n">ci_high_f</span> <span class="o">-</span> <span class="n">x_bar</span><span class="p">)))</span> 
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>95% confidence interval: 96.818 - 99.681
margin of error: +/-1.4315
</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <div class="alert alert-block alert-success">
                <h4>Analysis:</h4>According to both the Bootstrap and Frequentist approaches, using the mean we calculated (98.249°),
                and at a 95% confidence interval, a temperature below 96.818° or above 99.681° would be considered abnormal.
            </div>
        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h3 id="Question-#6">Question #6</h3>
            <hr>
            <p>Is there a significant difference between males and females in normal temperature?</p>
            <ul>
                <li> What testing approach did you use and why?</li>
                <li> Write a story with your conclusion in the context of the original problem.</li>
            </ul>
        </div>
    </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <h4 id="Hypotheses">Hypotheses</h4>
            <p>$H_0: \bar x_m\ =\ \bar x_f$</p>
            <p>$H_a: \bar x_m \neq\ \bar x_f$</p>

        </div>
    </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[15]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="n">males</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">gender</span> <span class="o">==</span> <span class="s1">&#39;M&#39;</span><span class="p">]</span>
<span class="n">females</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">gender</span> <span class="o">==</span> <span class="s1">&#39;F&#39;</span><span class="p">]</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Of the </span><span class="si">{}</span><span class="s1"> participants, </span><span class="si">{}</span><span class="s1"> are female and </span><span class="si">{}</span><span class="s1"> are male.&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">males</span> <span class="o">+</span> <span class="n">females</span><span class="p">),</span> <span class="nb">len</span><span class="p">(</span><span class="n">females</span><span class="p">),</span> <span class="nb">len</span><span class="p">(</span><span class="n">males</span><span class="p">)))</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>Of the 130 participants, 65 are female and 65 are male.
</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[16]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># plot a boxplot for an overview</span>
<span class="n">sns</span><span class="o">.</span><span class="n">boxplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">&#39;gender&#39;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">&#39;temperature&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">df</span><span class="p">)</span>

<span class="n">sns</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">rc</span><span class="o">=</span><span class="p">{</span><span class="s2">&quot;figure.figsize&quot;</span><span class="p">:</span> <span class="p">(</span><span class="mi">12</span><span class="p">,</span> <span class="mi">8</span><span class="p">)})</span>
<span class="n">plt</span><span class="o">.</span><span class="n">style</span><span class="o">.</span><span class="n">use</span><span class="p">(</span><span class="s1">&#39;fivethirtyeight&#39;</span><span class="p">)</span>

<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Gender&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Temp&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Fig. 6.1: Body Temp by Gender&#39;</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">();</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>




                <div class="output_png output_subarea ">
                    <img src="data:image/png;base64,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zwwYMCAPP/xwTjrppCoLrp9++unMnj17lZ/QYNGiRTnllFPy/PPPZ7vttssPf/jDzJ49O6NHj85TTz2V6667Lt/61reqfM9tt92WN998M7169cqOO+6YkSNH5qKLLsprr72WP/3pT9ljjz2y/fbbZ9SoUbnuuuuy4YYb5r/+67+qPMbAgQMzderU7Lvvvqlbt24effTRnHnmmTnjjDNy8MEH12j2AQMGZPHixdlnn30yf/78jB49OqeeemouvfTS9OzZM1tssUU6duyYF154IW+//Xa+8Y1vVH7v7Nmz88wzz2TXXXddbpwkyeOPP54k2W233b50ns+uYarw1ltvpV+/fnnvvfey6667pnXr1pk8eXJuv/32jBs3LoMGDaoWs+eee27efvvt7LHHHqlXr14efPDB/O53v0v9+vUrT+iwePHinHzyyXnppZey3XbbZY899sg//vGP/OxnP0ujRo2qzTF8+PAMGDAgG220UXr16pUGDRpkzJgxOeecczJ16tRqv3gYO3ZsFi5cmAMOOCDvvffeGlurBqw+AgUomeeffz433njjMm/bZ5990rp162XeNn/+/Fx++eVp1KhRBg8eXPmb88MPPzyHH374Ss8zb968zJ8/PwsXLkzfvn1Tv3799OrVK3PmzMmjjz6a4447Ln/4wx/SpUuXL32snXfeucbPu6J7embOnFnldVu8eHHefPPNPP744/n2t7+dE088sfK2JUuW5Ne//nUWLlyY//mf/6lyJqmK34JfddVVOe+885IkV1xxRebPn58rr7wyO+20U5LkuOOOy0knnZT33nuv8nsbNGiQPffcMyNHjswLL7xQ5exmDz74YOrUqZP99ttvhX6uLzNkyJA8//zz6du3b5XfvlfsMbvgggtyxx13VPmef/3rX7n11lsrw2WbbbbJhRdemDvuuKPKGo2DDjooP/rRj/LQQw9VC5TJkyfn5ptvzjbbbJMkOfLII9O3b98MHDgwe+21V5VDAZdn8eLFGTJkSDbddNMkyaGHHpp+/fplwIAB6dGjR+rVq5cDDjggEyZMyKhRo6q8j0eNGpUlS5Zk//33/8LneOONN5JkpU+QcOmll+a9996r9j7585//nN/+9re5/vrrc9ppp1X5nnnz5uWuu+6qDKcDDzwwRxxxRIYPH14ZKCNGjMhLL72U73//+/nlL39ZGbPXXnttbr311iqP99Zbb+WKK67Illtumeuvv74ynE844YScfPLJufnmm9OjR49svfXWld8ze/bsXHnllSv0vzmg2KxBAUrm+eefz0033bTMP6+//vpyv6/iN/Q//OEPqxzWs+mmm36lQzvmz5+fJPnnP/+Zli1bZujQoTnttNNy0UUX5corr8yiRYty8cUXZ+nSpSv9HKvCzJkzq7xWt956ax555JEsWrQoG264YWbPnl1535deeilvvPFG9tlnn2qnue3Xr1822WSTPPTQQ1m4cGFmzZqV//u//8tOO+1UGSdJssEGG6R///7V5qj4wPzQQw9Vbvvoo48yZsyYdOnSJZtssskq/bnvueeebLjhhtWCrkOHDunVq1emTJmSf/zjH1Vu23HHHavsVfn2t7+d5NP3ymcPF2rdunUaN26cmTNnVnve/fffvzJOkk/PKnbooYfm448/zpgxY2o0+2GHHVYZJ8mnJ3448MAD895771Ue/terV6/Ur1+/yuuZJA888EA22GCD7Lrrrl/4HO+//36SpEmTJtVuGz9+fG688cZqfyr2OM6cOTPPPvtsdt1112rvk4MPPjgtWrTIfffdV+2936dPnyp7dTp06JBmzZrlzTffrNw2atSo1K1bNyeccEKVPW39+vWrDJAK999/fxYvXpzjjjuuym1f+9rXctxxx6W8vDwjR46s8j2NGjWq8n4Faj97UICSWdl1Ii+//HKSVPnQWKHiA+jKqFh7kCSnnnpqlVOwduvWLT169MiYMWPyyiuvLPO515TPXxdk8eLFeffdd/PII4/kmmuuycSJEzNkyJBsvPHGefXVV5NkmddvqV+/frbeeus8/vjjef311/Puu+8mWfbr2qlTp2rbunTpkhYtWmT06NE57bTTUq9evTz22GNZsGDBl/62f0XNmTMnM2fOzMYbb5zBgwdXu71i9ldffbXKb9c/G7BJKv+btmzZstpj1K9fPwsXLqy2fVl7zCoO9avpGdqW9b6seIxXX3013bt3T5MmTdKjR4+MHj06U6dOTZs2bTJt2rT84x//yA9+8IOst956X/gcG2ywQZLkww8/rHbb3//+99xyyy3Vth9xxBHp1q1bZdjNmTNnmXs169Wrl48++igzZszIZpttVrn9869vkjRu3LjKabUnT56czTbbrFqM1KtXL9tuu22eeuqpym0Vczz77LOV790KCxYsSJJq21u0aFHlf7tA7SdQgFpnzpw5SZKvf/3r1W5r3rz5Sj9uxfH1FRdm/LxvfetbGTNmTN58882SBsrn1atXL5tuuml++tOfZvbs2bn99tvzpz/9KSeeeGLlB8XPrx2osPHGGyf59MPfBx98kCTLXBfQuHHj1K1bt8q2srKy7Lfffhk8eHDGjRuXHj165IEHHkiDBg1WaAF5TcybNy9J8s477+Smm25a7v0qfoYKy7vOx5d92P+sitfosyreexVzfZlmzZpV21bxOld88E4+XRsyevToPPjggzn++ONz//33J0mNDperuF5MxaFen3X88cfn+OOPr/y64iQCFSqi5qWXXspLL7203Of4/Ou7rIsrlpWVpby8PEmydOnSfPTRR8sMmeQ/UfX5Oe6+++4az7D++usv975A7SRQgFqn4oPdsj4cfpULIq6//vrZZJNN8s477yzzMK6K0wsX+QNRly5dcvvtt2fKlClJ/vNavfPOO8u8f8WHvQ033LDy9VzW67pw4cIsWbKk2vb9998/gwcPziOPPJLtttsuzz33XPbdd980bNhwlfw8FSpCo1u3bhk4cOAqfewv89mAqFDxQfqLFq0v6/6fVfHf5LMf0nfaaac0a9YsjzzySI4//vg88sgj2XzzzZe5B+vzdt9999x5553529/+lp/85Cc1mqtCxX+v/v3756ijjlqh7/0iderUSaNGjZYbchWHVX5+jpEjR67yQwSB2sM+UaDW6dChQ5Jk0qRJ1W5b1rYVsf3226e8vLzaWauS/xx+0rZt26/0HKtTxQfhijBp165dkuTFF1+sdt+lS5fmxRdfTMOGDdOiRYu0b98+ZWVleeGFF6rdd3mva8XZp5566qmMGTMmS5cuXeWL45NP91g0a9YsU6ZMWeZhWA8++GBuvPHGZe49+KoqDin8rIq9DDU9q9srr7xSbVvFf5OK93Py6d6wfffdN2+88Ub+9re/5Y033qjx67nDDjtkyy23zIsvvphHHnnkC+/7+QCveJ8s62dNkkGDBuXWW29dZqx9mQ4dOuStt96qPAyvQnl5ebU1Q180x1tvvZUrr7wyjz322ArPANQuAgWodXbfffdssMEGueuuu6osxn377bdrfJX35fn+97+f5NMzXH32t77jxo3L008/nS5dulQeSlM0CxYsyF133ZXkP6ea3X777bP55pvnsccey5NPPlnl/jfeeGPefvvt7LXXXqlfv36aN2+e7t2757nnnsvDDz9ceb/58+cv89ocFQ444IDMnTs3gwcPzsYbb1x5XZdVrXfv3pWnf644hChJXn/99QwYMCBDhgypdsjQqnD33Xdn2rRplV9Pnz49d9xxR5o1a5ZddtmlRo8xbNiwKhdFfPHFFzNq1Ki0atWq2vqUilMA/8///E/lYXQ1UVZWlt/85jf52te+lgsvvDAjRoxY5p7Axx9/PAMGDEjyn3VXrVu3znbbbZcxY8bkb3/7W5X7P/TQQxk0aFDGjBmzUnsPe/funaVLl+b3v/99lYucDh06NLNmzapy3/333z916tTJtddeW+WscUuWLMnvfve73HHHHVVOAgGsnRziBdQ6DRo0yBlnnJHzzjsvRx55ZOU1GD77m9XPrpeYMWNGRo4cmW9+85vp3bv3Fz52ly5d8uMf/zh33HFHDjvssPTs2bPyWhsbbLBBzjjjjCr3v/POO/Phhx/msMMOW+bZk2qiYlFyTU8Y8PnTDCfJ3Llz89hjj+Xdd9/Nd77zncozVNWpUye//vWvc8opp+QXv/hFdt1112y22WZ56aWXMnHixLRp0yannHJK5eOcfvrpOeaYY3Luuedm1KhR2XTTTfPUU09VCYLP69WrV37/+99n5syZ+elPf7raFiwfc8wxGT9+fO644448//zz2WGHHTJv3ryMHj068+fPz3nnnVdtIfaqsGTJkvTt2zd77bVXkk+vwTN//vxcdtllNT6UraysLD/5yU+y11575f3338+jjz6a+vXr59e//nW116t9+/Zp27ZtpkyZku23336ZC/qXp127drnuuutyzjnn5JJLLsnNN9+cbt26pVmzZnn//fczfvz4zJw5M3Xr1s0Pf/jDHHnkkZXfe+6556Z///4588wzs/POO6dNmzaZPn16xo4dm8aNG+eXv/xljef4rP333z+PPfZYHnnkkbz++uvZcccdKy9e2qJFiypnTttyyy1zwgknZODAgTn00EOz2267pUmTJhk3blymTp2a73znO/ne9763UnMAtYdAAWqlffbZJw0aNMgtt9ySUaNGZf31188+++yT7bffPuecc06V3/RWnJa3c+fOXxooyadX7W7fvn3+9Kc/5S9/+Uvlou/jjjsurVq1qnLfYcOGZebMmendu/dKB0rFou8VCZTPLhSvOM6/devWOfzww3PwwQdXOZ1rp06dcuutt+amm27K+PHj8/TTT2fTTTfNUUcdlSOOOKLKh+yWLVtm8ODBuf766/P000/n2WefTZcuXXLaaadVXtfi85o0aZJu3bpl7Nixq/zsXZ+1/vrr54YbbsiQIUPy8MMPZ/jw4WncuHE6duyYI444Il27dl0tz9uvX7/MmjUr999/fz755JNst912OfbYY2u0LqTCBRdckBEjRmTkyJFZvHhxunbtmhNOOKHykKbP23vvvTNlypSVej2322673HnnnXnkkUfy8MMPZ/z48XnvvffSsGHDbLHFFjnggANy0EEHVbkYZPJpHNx22225+eabM27cuDz77LNp3rx59t133xx99NHLXej+ZcrKynLZZZdl6NCh+etf/5r//d//zeabb55LL700jzzySLVTOx9xxBFp06ZN7rzzzjz66KNZunRpWrZsmZNPPjk/+tGPVugEB0DtVDZnzpzl/1oMoIDmzZuXjz/+OBtvvHGVD+JJcu+99+Y3v/lNlYvwsXqVl5enT58+2XDDDXPbbbeVepxVZvjw4bn88stz5pln5gc/+MEafe6zzjorY8eOzQMPPLDcM7ABrK2sQQFqnenTp6d37975zW9+U2X7ggUL8uc//zl169bN9ttvX6Lp1j333XdfZs6cudw9LKyYyZMnZ8yYMenVq5c4AdZJDvECap0OHTpk2223zciRIzNz5sxss802WbBgQcaOHZuZM2fm+OOPX+a1K1i1zjnnnEybNi2TJ09Oy5YtKxd3s3IGDx6cxx9/PK+99lrq1KmTvn37lnokgJIQKECtU6dOnVx99dW54447Mnr06Pz5z3/Oeuutl7Zt2+aUU06pXMzM6vX1r389TzzxRLbeeuucd955y7xoHzX3jW98I9OnT0/z5s3z85//fKXXfADUdtagAAAAhbHG16BMnDgx/fv3T5K88cYbOfbYY3Psscfmsssuq3K+9jfeeCOHHXbYmh4PAAAooTUaKLfddlsuvvjiyqsAX3nllenfv38GDRqU8vLyPP7440mS+++/P+ecc07ef//9NTkeAABQYms0UDbbbLNcfvnllV+/8sor6dy5c5Jk5513zvjx45N8ek79L7pqMQAAsHZao4vk99xzz8yYMaPy6/Ly8sprGDRs2DDz5s1LkvTo0WOln2Py5MlfbUgAAGC1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RSZMmJBJkyZl0qRJ9qIAAGslgQK1SMXek8//HQBgbSFQAACAwhAoUIsceuihy/w7AMDawiJ5qEU6duyYbbfdtvLvAABrG4ECtYw9JwDA2kygQC1jzwkAsDazBgUAACgMgQIAABSGQAEAAAqjbM6cOeWlHgIAWHv16dOn1COwFhoxYkSpR2A1sQcFAAAoDIECAAAUhkABAAAKwxoUAACgMOxBAQAACkOgAAAAhSFQAACAwhAoAABAYQgUAACgMAQKAABQGAIFAAAoDIECAAAUhkABAAAKQ6AAAACFIVAAAIDCECgAAEBhCBQAAKAwBAoAAFAYAgUAACgMgQIAABSGQAEAAApDoAAAAIUhUAAAgMIQKAAAQGEIFAAAoDAECgAAUBgCBQAAKAyBAgAAFIZAAQAACkOgAAAAhSFQoBaZMWNGevbsmf79+1f+uemmm0o9FgAr6bnnnku3bt0yatSoKtt//OMf54ILLijRVFBa9Uo9ALBi2rRpk+uvv77UYwCwirRu3TqjRo3KPvvskySZMmVK5s+fX+KpoHTsQQEAKKF27drl3//+d+bNm5ckeeCBB/Ld7363xFNB6QgUqGWmTp1a5RCvWbNmlXokAL6inj175rHHHkt5eXlefvnldOrUqdQjQck4xAtqGYd4Aax9vvvd7+ayyy5Ly5Yts/3225d6HCgpe1AAAEqsZcuWWbBgQe666y6Hd7HOEygAAAWw99575+23306rVq1KPQqUVNmcOXPKSz0EAABAYg8KAABQIAIFAAAoDIECAAAUhkABAAAKQ6AAAACF4UKNAHwl06dPz913351x48Zl1qxZKSsrS6tWrdKrV68cfPDBWX/99dfIHL/61a/y4osv5p577lkjzwfA6iFQAFhpjz76aC644IJsttlmOeSQQ9KmTZssWrQo48ePz6BBg/Loo4/m+uuvT/369Us9KgC1hEABYKVMnz49559/frp27ZrLL7889er95/+l7LTTTtl9993Tr1+/3HnnnTnyyCNLOCkAtYk1KACslCFDhqS8vDxnnXVWlTip0KlTpxxyyCFp0KBB5bZ77703hx12WHbZZZf07t0711xzTRYtWlR5+4033pj/+q//yrhx43L44Ydn1113zUEHHZShQ4dWeey5c+fm/PPPz9577529994711xzTZYuXVpthieeeCJ9+/ZNjx49su++++ayyy7LvHnzKm8fOXJkunfvnr/+9a/Zb7/9stdee+Uf//jHqnh5AFhJ9qAAsFIee+yxdO3aNc2bN1/ufX7+859X/n3IkCG5+uqrc/DBB+fUU0/Nv/71r9xwww158803c+mll1be7913380ll1yS//f//l8233zz3HPPPfnDH/6QNm3aZOedd87SpUtz6qmnZubMmTnllFPStGnTDBkyJJMmTcrGG29c+TgPP/xwzj333Oy9997p169fZs2aleuuuy6TJ0/ODTfcUBlVS5YsyW233Zazzz47c+fOzbe+9a3V8GoBUFMCBYAV9uGHH+aDDz5Iq1atqt22ePHiatsWLFiQQYMG5cADD8wZZ5yR5NPDwDbZZJOcc845eemll9KpU6fK+1522WXZeeedkyTf/va38/jjj2fMmDHZeeed89RTT+Xll1/OFVdckR49eiRJdtxxxxx00EGVz1deXp6rrroqXbp0ycUXX1y5vW3btjnqqKMyevTo7LvvvpXbK/ayAFB6DvECYIUtWbIkSVJWVlZl+5w5c7LzzjtX+zNhwoQsWLAgu+++exYvXlz5Z+edd06dOnXyzDPPVHmcilhJkvr166dp06aZP39+kuSFF15I3bp1KwMmSRo2bJju3btXfj19+vS8/fbb1Z6vQ4cOad68ebXna9++/ap5YQD4yuxBAWCFNW3aNA0bNsyMGTOqbG/cuHFuvfXWyq+HDx+ee++9N3Pnzk2SnHbaact8vHfeeafK158/NXGdOnVSXl6eJPnggw/SpEmT1K1bt8p9Pnuo2Zw5c5IkV1xxRa644oovfb7PrpMBoLQECgArZbfddssTTzyRjz76KI0aNUqS1KtXL9tss03lfR5//PEkn4ZLkpx//vlp3bp1tcdq2rRpjZ+3adOm+eCDD7J48eIqi/MrouSzz3fiiSema9eu1R6jYl4AischXgCslL59+2bJkiX5zW9+k4ULF1a7ffHixZk2bVqSZLvttst6662XWbNmZZtttqn807hx4wwcODCvv/56jZ93xx13zNKlS/PYY49Vbvvkk0/y7LPPVn7dunXrNGvWLDNmzKjyfJtttlmuu+66TJgwYeV/cABWK3tQAFgpW265ZS666KKcf/75+elPf5qDDjoo7dq1S3l5eSZNmpR77703b731Vvbbb780bdo0hx9+eAYNGpSPP/44O+64Y2bPnl359YqcOatbt275zne+k0svvTRz585NixYtMmzYsMydOzfNmjVLktStWzf9+/fPpZdemrp162a33XbL/Pnzc8stt2T69OlVzi4GQLEIFABW2m677ZY777wzw4cPz3333ZeZM2dm8eLF+eY3v5nu3bunT58+lQvQ+/fvn+bNm+fuu+/O0KFD06RJk3Tp0iX9+/fP17/+9RV63gEDBuSqq67KjTfemEWLFqVXr17ZYostMnbs2Mr79OnTJ40bN86QIUPy17/+Neuvv346duyYs88+O1tuueUqfR0AWHXK5syZU17qIQAAABJrUAAAgAIRKAAAQGEIFAAAoDAECgAAUBgCBQAAKAyBAgAAFIZAAQAACkOgAAAAhfH/AV1BHHoTeFm6AAAAAElFTkSuQmCC
">
                </div>

            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[17]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># are both samples normally distributed?</span>
<span class="n">sns</span><span class="o">.</span><span class="n">set</span><span class="p">(</span><span class="n">rc</span><span class="o">=</span><span class="p">{</span><span class="s2">&quot;figure.figsize&quot;</span><span class="p">:</span> <span class="p">(</span><span class="mi">12</span><span class="p">,</span> <span class="mi">8</span><span class="p">)})</span>
<span class="n">plt</span><span class="o">.</span><span class="n">style</span><span class="o">.</span><span class="n">use</span><span class="p">(</span><span class="s1">&#39;fivethirtyeight&#39;</span><span class="p">)</span>

<span class="c1"># Compute the ECDFs for males and females</span>
<span class="n">x_male</span><span class="p">,</span> <span class="n">y_male</span> <span class="o">=</span> <span class="n">ecdf</span><span class="p">(</span><span class="n">males</span><span class="o">.</span><span class="n">temperature</span><span class="p">)</span>
<span class="n">x_female</span><span class="p">,</span> <span class="n">y_female</span> <span class="o">=</span> <span class="n">ecdf</span><span class="p">(</span><span class="n">females</span><span class="o">.</span><span class="n">temperature</span><span class="p">)</span>

<span class="c1"># Generate plot</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x_male</span><span class="p">,</span> <span class="n">y_male</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s1">&#39;.&#39;</span><span class="p">,</span> <span class="n">linestyle</span> <span class="o">=</span> <span class="s1">&#39;none&#39;</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;b&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x_female</span><span class="p">,</span> <span class="n">y_female</span><span class="p">,</span> <span class="n">marker</span><span class="o">=</span><span class="s1">&#39;.&#39;</span><span class="p">,</span> <span class="n">linestyle</span><span class="o">=</span><span class="s1">&#39;none&#39;</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;r&#39;</span><span class="p">)</span>

<span class="c1"># draw 100,000 random samples from a normal distribution</span>
<span class="n">m_norm_dist</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">normal</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">males</span><span class="o">.</span><span class="n">temperature</span><span class="p">),</span> <span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">males</span><span class="o">.</span><span class="n">temperature</span><span class="p">),</span> <span class="mi">100000</span><span class="p">)</span>
<span class="n">mnd_x</span><span class="p">,</span> <span class="n">mnd_y</span> <span class="o">=</span> <span class="n">ecdf</span><span class="p">(</span><span class="n">m_norm_dist</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">mnd_x</span><span class="p">,</span> <span class="n">mnd_y</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;b&#39;</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">)</span>

<span class="c1"># draw 100,000 random samples from a normal distribution</span>
<span class="n">f_norm_dist</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">normal</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">females</span><span class="o">.</span><span class="n">temperature</span><span class="p">),</span> <span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">females</span><span class="o">.</span><span class="n">temperature</span><span class="p">),</span> <span class="mi">100000</span><span class="p">)</span>
<span class="n">fnd_x</span><span class="p">,</span> <span class="n">fnd_y</span> <span class="o">=</span> <span class="n">ecdf</span><span class="p">(</span><span class="n">f_norm_dist</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">fnd_x</span><span class="p">,</span> <span class="n">fnd_y</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;r&#39;</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">)</span>

<span class="c1"># Make the margins nice</span>
<span class="n">plt</span><span class="o">.</span><span class="n">margins</span> <span class="o">=</span> <span class="mf">0.02</span>

<span class="c1"># Label the axes</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Gender&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;ECDF&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Fig. 6.2: CDFs of males v. females&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">((</span><span class="s1">&#39;males&#39;</span><span class="p">,</span> <span class="s1">&#39;females&#39;</span><span class="p">),</span> <span class="n">loc</span><span class="o">=</span><span class="s1">&#39;lower right&#39;</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="s1">&#39;large&#39;</span><span class="p">,</span> <span class="n">markerscale</span><span class="o">=</span><span class="mi">2</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">();</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>




                <div class="output_png output_subarea ">
                    <img src="data:image/png;base64,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61RVFadOnUK3bt1gsVjw0Ucf4aeffkJRURH69u2Lp59+Gr179662DqPRiIceesjltpSUFBQVFWnqCA4Oxrx58zz6ZnrPnj0AgKFDh1a7X/v27fHwww/XWJ+r48LDw5GdnY38/Hyv5s1cvXoVTz/9NK5evYqEhAS0bdsWp0+fxrp165CSkoKvv/4aAQEBbo8vLS3FM888g8OHD6Nr16645557cOXKFezYsQN79uzB3//+d4wePdo5ZO2LL76AwWDAAw884NFreOLECWzatAnDhg3DPffcgx07dmDFihW4du0a9u/fj9tuuw3Tp09HWloafvzxRxQVFeGf//yn8/jXXnsNycnJiI2NxbRp02Cz2ZCamor169fj8OHDWLFiBXQ692+Lf/vb37B+/Xp06dIF06dPR2lpKbZu3YonnnjC+dwA4Ndff8XTTz8NQRAwduxYhISE4Pjx41i+fDnS0tKwZMkSCILg8hwTJ07EggULsGXLlipByrZt21BWVobJkyfX+FpVFhMTg3nz5mHVqlXIz8/HY4895vyAbrfb8dxzzyE1NRW9e/fGfffdh6tXr2Lr1q3Ys2cPPvzwwyrznJYuXYqzZ89i/PjxiIuLQ1JSEubPn48zZ87gm2++wejRo9GvXz9s3rwZn3zyCUJCQpzP5fr165gzZw4uXbqEUaNGYfTo0bh27Rq2b9+OTz/9FJcvX8Yrr7zi9rlYrVY8/vjj+OWXXxAXF4cxY8YgNzcXSUlJ2LNnDz799FPnHKsNGzbg9ddfR4cOHTBlyhSIoojdu3fjf//3f3Hp0iU8++yztXodiahhMUghIq8cOnQI//nPf1xumzBhAjp37uxyW3FxMd5++20EBQVh8eLF6NixIwBg1qxZmDVrltftsVqtKC4uRllZGebMmQODwYDx48cjPz8fycnJePLJJ/HBBx+4nNNRk5KSErz//vsAHEOrytVmrselS5cAwPl860N4eDguX76MvLw8TZBSUFDg9lp17twZEyZMAABs3rwZFy5cwGuvvYa77rrLuc+CBQvwxRdfYMeOHZg0aZLb83/11Vc4fPgwEhMT8corrzg/8JvNZjz++ON444038N1332HQoEEYNGgQVqxYUavX8NSpU3j22WedvycPPPAApk2bhh9//BFTp07FX/7yFwCOD973338/duzYgZKSEvj7+yM9PR3JyckYP3483nrrLWediqLgySefxOHDh3H8+HG3k8mTk5Oxfv16jBs3Dm+88Ybzuc2dOxePPvoo3nzzTQwePBiBgYFYu3YtrFYrPvzwQ02v3quvvorNmzfjyJEjLof7AUBYWBji4uJw4MABXL58WdMzsGnTJuh0OowbN86j16tcTEwMYmJikJycjOvXr2te76VLlyI1NRWzZs3SfGh/8MEH8dhjj+Gvf/0rVqxYoQmqfvnlFyxatMgZvPTp0wf//d//jWXLluGNN95w/o5Mnz4d9957LzZu3OgMUlauXInc3Fy88sormr+lJ598Evfccw82bNhQbZCyYMEC/PLLL3jppZdw7733Osv37t2L5557Du+8847zb/XLL79EUFAQvvzySwQGBjrPM2PGDKxatQpPPfVUtUEpEd1a/OskIq8cOnQIhw4dcrktOjrabZCyb98+WCwWPPbYY5oP7JGRkXjwwQfx73//26v2FBcXAwAyMjIwYMAAvP/++85v/ffv349nn30Wb731Fr799ttaDfOw2Wz485//jFOnTuGOO+7A+PHjvWpfQUEBACAoKMir4z1RPkymsLBQU261Wp3Dq242atQoZ5CiqioA4OjRo/jNb37j/AD36KOPYsaMGQgLC6v2/ElJSfD398eLL76o+fAXExOD++67D1999RW2b9+OxMREr5/f/fff73wcERGBdu3a4dy5c5reJ51Oh549e+LcuXPIzc1Fly5d0LZtW7z++utVggNRFDFgwAAcPnwY165dc3vu8qFoL7zwgua5RUREYMaMGfjwww+xc+dOTJo0yfk6HjlyBHFxcc4P+C+99BJefPFFmEymap/n5MmTkZKSgq1btzqzsl25cgWpqakYPnx4nbLL3WzdunUIDg7GU089pSmPjo7GxIkTsW7dOhw7dkwznK1///6a3pXy1zQ8PFwTxHbs2BGhoaHOIV0AMGLECLRu3brK70CbNm3QuXNnHD9+HKWlpfDz86vSVpvNhh9++AG33367JkABgGHDhmHw4MHYs2cP8vLyEBYWBlVVUVJS4vyfAAABAQFYuHAhjEYjAxSiRo5/oUTkFW/njRw/fhwAXKbKdfftsicqBx7PPfecZljSkCFDMHLkSOzcuRNms9nluV0pLi7GSy+9hJSUFMTExHi0Pow75R8sr1+/7nUdNSmfL3PzkCxP5swAwNixY7Fo0SKsXbsW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/wxa0guAsLAwli5d6pMaLwUt6UPPnj2ZMmUKAIZh4HK5sNl+fF+J/kXxM926dWPbtm2Ypklubi7Hjx+nX79+PP300yxbtozKykrefPNNX5d50Wvch5KSEr755hv69evH4sWLKSsrY/Pmzb4u85LQ3HvC5XKRn5/PyZMn6devn69LvCQ014eEhASeeuop7r33Xjp06ECXLl18XeYloXEvamtrqa6upqCgAJfLxUcffURlZaWvy7xoDRo0qMGHK9M0MQwDgJCQEMrLyykvL8fhcHiXqRuXC6slvQAYOHCg91t+ufBa0ofAwEDCw8NxOp0899xz3H333Wf9glEhxc/ccccdOBwOxowZwz//+U969OjBnXfeSXR0NIZhkJ6ezt69e31d5kWvcR+uvPJKHA4Hffv2xTAMrr/+er766itfl3lJaO49YbVaee+99856PKtcOI37EB0dzapVq3jttdf429/+RmxsLGvXrvV1mZeE5t4T06dPZ+7cuYwfP564uDgditqK6u9BrKioICwsjNDQUCoqKpqMy8+ruV5I6ztTH8rKynj88ceJj49n5MiRZ1/Pz1WgnJ+8vDxSUlLIyspi8ODBdOrUid/+9rccO3YMgJ07d3LllVf6uMqLX+M+xMTEEBsby65duwDYtWsXCQkJPq7y0tC4F3WHtPz73/9mwIABPq7u0tG4DwkJCQQHB3u/CYuMjOSHH37wcZWXhubeEzt27CAzM5OXXnqJb7/9lpSUFF+Xecno1q0b//nPfwD46KOP6NWrF8nJyezYsQO3283Ro0dxu90Kjq2guV5I62uuD1VVVYwdO5Y777yzxT/soRPn/Uznzp2ZPHkyK1asICwsjGeffZb9+/czceJEAgMDiY+P17fHraC5PhQXF/PCCy/gcrno1KkT48aN83WZl4TmegFw4sQJ/aPfiprrwxdffMG4ceOw2+2EhYUxdepUX5d5SWiuF9u3b2fkyJEEBgZy66230rVrV1+Xecl44oknmDVrFrW1tcTHxzNo0CCsViu9evVi1KhRuN1uJkyY4OsyLwnN9UJaX3N9eP311zl8+DAbN25k48aNAEyZMsX7xWNzjJKSErO1ihYRERERETkbHe4lIiIiIiJ+RSFFRERERET8ikKKiIiIiIj4FYUUERERERHxKwopIiIiIiLiV/QTxCIics4OHjzIG2+8wccff0xhYSGGYRAXF8fNN9/M8OHDCQoKapU6pk6dyu7du3nrrbdaZXsiItI6FFJEROScZGdn89xzzxETE8OIESOIj4+ntraWnTt3kpWVRXZ2NkuWLMFut/u6VBER+YVSSBERkRY7ePAg06dPJyUlhblz52Kznf5nZMCAAdxwww2MGTOGdevW8cADD/iwUhER+SXTOSkiItJiq1evxjRNJk2a1CCg1ElOTmbEiBEEBwd7xzZt2sR9993Hddddx9ChQ1m0aBG1tbXe+cuWLeOee+7h448/5v777+f6669n2LBhrF27tsG6S0tLmT59OkOGDGHIkCEsWrQIt9vdpIatW7cycuRIBg4cyC233MKcOXMoLy/3zn/nnXdITU3l7bff5rbbbmPw4MF89dVXF+LlERGRC0R7UkREpMU+/PBDUlJSiIyMPOMy48eP995fvXo1L7/8MsOHD+eJJ55g//79LF26lG+//ZbZs2d7l/v++++ZNWsWDz74ILGxsbz11lu89NJLxMfHk5aWhtvt5oknnuC7777j8ccfJyIigtWrV/Pll1/Srl0773o++OADnn32WYYMGcKYMWMoLCxk8eLF5Ofns3TpUm+wcrlcrFq1imeeeYbS0lK6d+/+M7xaIiJyvhRSRESkRX744QfKysqIi4trMs/pdDYZq6qqIisrizvuuIMJEyYAnkPC2rdvz+TJk/n8889JTk72LjtnzhzS0tIAuOaaa9iyZQv/+te/SEtL46OPPiIvL4/58+czcOBAAPr27cuwYcO82zNNk8zMTPr06cOf/vQn7/gVV1zBQw89xD/+8Q9uueUW73jd3hYREfE/OtxLRERaxOVyAWAYRoPxkpIS0tLSmky5ublUVVVxww034HQ6vVNaWhoWi4VPPvmkwXrqAguA3W4nIiKCyspKAHJycrBard4QAxASEkJqaqr38cGDBzl27FiT7fXo0YPIyMgm2+vWrduFeWFEROSC054UERFpkYiICEJCQjhy5EiD8dDQUF599VXv4w0bNrBp0yZKS0sBePrpp5td3/Hjxxs8bvyzxRaLBdM0ASgrKyMsLAyr1dpgmfqHnZWUlAAwf/585s+ff9bt1T9vRkRE/ItCioiItFh6ejpbt27l5MmTOBwOAGw2G0lJSd5ltmzZAnjCC8D06dPp0qVLk3VFRES0eLsRERGUlZXhdDobnLBfF0zqb2/s2LGkpKQ0WUddvSIi4v90uJeIiLTYyJEjcblczJw5k5qamibznU4nBw4cAODqq68mICCAwsJCkpKSvFNoaCgLFy6koKCgxdvt27cvbrebDz/80DtWXV3Np59+6n3cpUsX2rZty5EjRxpsLyYmhsWLF5Obm3v+f7iIiLQq7UkREZEWS0hI4Pnnn2f69On87ne/Y9iwYSQmJmKaJl9++SWbNm3i8OHD3HbbbURERHD//feTlZVFRUUFffv2paioyPv4XH5Rq1+/fvTv35/Zs2dTWlpKVFQUr732GqWlpbRt2xYAq9VKRkYGs2fPxmq1kp6eTmVlJStWrODgwYMNfnVMRET8m0KKiIick/T0dNatW8eGDRvYvHkz3333HU6nk06dOpGamspdd93lPSk9IyODyMhI3njjDdauXUtYWBh9+vQhIyODyy+//Jy2O2/ePDIzM1m2bBm1tbXcfPPNdO7cmW3btnmXueuuuwgNDWX16tW8/fbbBAUF0bNnT5555hkSEhIu6OsgIiI/H6OkpMT0dREiIiIiIiJ1dE6KiIiIiIj4FYUUERERERHxKwopIiIiIiLiVxRSRERERETEryikiIiIiIiIX1FIERERERERv6KQIiIiIiIifkUhRURERERE/Mr/A5Rv0ORpiYAqAAAAAElFTkSuQmCC
">
                </div>

            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[18]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># common variables</span>
<span class="n">temp_m</span> <span class="o">=</span> <span class="n">males</span><span class="o">.</span><span class="n">temperature</span>
<span class="n">temp_f</span> <span class="o">=</span> <span class="n">females</span><span class="o">.</span><span class="n">temperature</span>
</pre>
                </div>

            </div>
        </div>
    </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[19]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># Check for identical variances</span>
<span class="n">mv</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">var</span><span class="p">(</span><span class="n">temp_m</span><span class="p">)</span>
<span class="n">fv</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">var</span><span class="p">(</span><span class="n">temp_f</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Male variance: </span><span class="si">{}</span><span class="se">\n</span><span class="s1">Female variance: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">mv</span><span class="p">,</span> <span class="n">fv</span><span class="p">))</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>Male variance: 0.4807479289940825
Female variance: 0.5442698224852062
</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[20]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># confirm that variances are not equal with bootstrap - null hypothesis is that they are equal</span>

<span class="n">size</span> <span class="o">=</span> <span class="mi">10000</span>

<span class="n">bs_replicates_m</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">(</span><span class="n">size</span><span class="p">)</span>

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">size</span><span class="p">):</span>
    <span class="n">bs_sample_m</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">choice</span><span class="p">(</span><span class="n">temp_m</span><span class="p">,</span> <span class="nb">len</span><span class="p">(</span><span class="n">temp_m</span><span class="p">))</span>
    <span class="n">bs_replicates_m</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">var</span><span class="p">(</span><span class="n">bs_sample_m</span><span class="p">)</span>
    
<span class="n">bs_var_m</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">bs_replicates_m</span><span class="p">)</span><span class="o">/</span><span class="n">size</span>

<span class="n">bs_replicates_f</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">(</span><span class="n">size</span><span class="p">)</span>

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">size</span><span class="p">):</span>
    <span class="n">bs_sample_f</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">choice</span><span class="p">(</span><span class="n">temp_f</span><span class="p">,</span> <span class="nb">len</span><span class="p">(</span><span class="n">temp_f</span><span class="p">))</span>
    <span class="n">bs_replicates_f</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">var</span><span class="p">(</span><span class="n">bs_sample_f</span><span class="p">)</span>

<span class="n">bs_var_f</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">bs_replicates_f</span><span class="p">)</span><span class="o">/</span><span class="n">size</span>

<span class="n">bs_var_m</span>
<span class="n">bs_var_f</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Bootstrap verification:</span><span class="se">\n</span><span class="s1">Male variance: </span><span class="si">{}</span><span class="se">\n</span><span class="s1">Female variance: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">bs_var_m</span><span class="p">,</span> <span class="n">bs_var_f</span><span class="p">))</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>Bootstrap verification:
Male variance: 0.4734530054437869
Female variance: 0.5353755356213008
</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[21]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># Variances are not identical, so set `equal_var` to false to perform Welch&#39;s t-test</span>
<span class="n">r</span> <span class="o">=</span> <span class="n">stats</span><span class="o">.</span><span class="n">ttest_ind</span><span class="p">(</span><span class="n">temp_m</span><span class="p">,</span> <span class="n">temp_f</span><span class="p">,</span> <span class="n">equal_var</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;t-statistic: </span><span class="si">{:0.4}</span><span class="se">\n</span><span class="s1">p-value: </span><span class="si">{:0.4}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">r</span><span class="o">.</span><span class="n">statistic</span><span class="p">,</span> <span class="n">r</span><span class="o">.</span><span class="n">pvalue</span><span class="p">))</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>t-statistic: -2.285
p-value: 0.02394
</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[22]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># males</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;MALES&#39;</span><span class="p">)</span>
<span class="n">xbar_m</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">temp_m</span><span class="p">)</span>
<span class="n">s_m</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">temp_m</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;sample mean: </span><span class="si">{}</span><span class="se">\n</span><span class="s1">sample standard deviation: </span><span class="si">{}</span><span class="se">\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">round</span><span class="p">(</span><span class="n">xbar_m</span><span class="p">,</span> <span class="mi">3</span><span class="p">),</span> <span class="nb">round</span><span class="p">(</span><span class="n">s_m</span><span class="p">,</span> <span class="mi">3</span><span class="p">)))</span>

<span class="c1"># confidence interval for one draw</span>
<span class="n">ci_low_m</span><span class="p">,</span> <span class="n">ci_high_m</span> <span class="o">=</span> <span class="n">stats</span><span class="o">.</span><span class="n">norm</span><span class="o">.</span><span class="n">interval</span><span class="p">(</span><span class="mf">0.95</span><span class="p">,</span> <span class="n">loc</span><span class="o">=</span><span class="n">xbar_m</span><span class="p">,</span> <span class="n">scale</span><span class="o">=</span><span class="n">s_m</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;95</span><span class="si">% c</span><span class="s1">onfidence interval (one draw): </span><span class="si">{}</span><span class="s1"> - </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">round</span><span class="p">(</span><span class="n">ci_low_m</span><span class="p">,</span> <span class="mi">3</span><span class="p">),</span> <span class="nb">round</span><span class="p">(</span><span class="n">ci_high_m</span><span class="p">,</span> <span class="mi">3</span><span class="p">)))</span>

<span class="c1"># females</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\n\n</span><span class="s1">FEMALES&#39;</span><span class="p">)</span>
<span class="n">xbar_f</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">temp_f</span><span class="p">)</span>
<span class="n">s_f</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">temp_f</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;sample mean: </span><span class="si">{}</span><span class="se">\n</span><span class="s1">sample standard deviation: </span><span class="si">{}</span><span class="se">\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">round</span><span class="p">(</span><span class="n">xbar_f</span><span class="p">,</span> <span class="mi">3</span><span class="p">),</span> <span class="nb">round</span><span class="p">(</span><span class="n">s_f</span><span class="p">,</span> <span class="mi">3</span><span class="p">)))</span>

<span class="c1"># confidence interval for one draw</span>
<span class="n">ci_low_f</span><span class="p">,</span> <span class="n">ci_high_f</span> <span class="o">=</span> <span class="n">stats</span><span class="o">.</span><span class="n">norm</span><span class="o">.</span><span class="n">interval</span><span class="p">(</span><span class="mf">0.95</span><span class="p">,</span> <span class="n">loc</span><span class="o">=</span><span class="n">xbar_f</span><span class="p">,</span> <span class="n">scale</span><span class="o">=</span><span class="n">s_f</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;95</span><span class="si">% c</span><span class="s1">onfidence interval (one draw): </span><span class="si">{}</span><span class="s1"> - </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">round</span><span class="p">(</span><span class="n">ci_low_f</span><span class="p">,</span> <span class="mi">3</span><span class="p">),</span> <span class="nb">round</span><span class="p">(</span><span class="n">ci_high_f</span><span class="p">,</span> <span class="mi">3</span><span class="p">)))</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>MALES
sample mean: 98.105
sample standard deviation: 0.693

95% confidence interval (one draw): 96.746 - 99.464


FEMALES
sample mean: 98.394
sample standard deviation: 0.738

95% confidence interval (one draw): 96.948 - 99.84
</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
    <div class="input">
        <div class="prompt input_prompt">In&nbsp;[23]:</div>
        <div class="inner_cell">
            <div class="input_area">
                <div class=" highlight hl-ipython3">
                    <pre><span></span><span class="c1"># bootstrap - two-sided Welch&#39;s t-test  </span>
<span class="n">size</span> <span class="o">=</span> <span class="mi">10000</span>
<span class="n">bs_replicates_m</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">(</span><span class="n">size</span><span class="p">)</span>

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">size</span><span class="p">):</span>
    <span class="n">bs_sample_m</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">choice</span><span class="p">(</span><span class="n">temp_m</span><span class="p">,</span> <span class="nb">len</span><span class="p">(</span><span class="n">temp_m</span><span class="p">))</span>
    <span class="n">bs_replicates_m</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">bs_sample_m</span><span class="p">)</span>
    
<span class="n">bs_mean_m</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">bs_replicates_m</span><span class="p">)</span><span class="o">/</span><span class="n">size</span>

<span class="n">bs_replicates_f</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">(</span><span class="n">size</span><span class="p">)</span>

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">size</span><span class="p">):</span>
    <span class="n">bs_sample_f</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">choice</span><span class="p">(</span><span class="n">temp_f</span><span class="p">,</span> <span class="nb">len</span><span class="p">(</span><span class="n">temp_f</span><span class="p">))</span>
    <span class="n">bs_replicates_f</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">bs_sample_f</span><span class="p">)</span>

<span class="n">bs_mean_f</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">bs_replicates_f</span><span class="p">)</span><span class="o">/</span><span class="n">size</span>


<span class="n">result</span> <span class="o">=</span> <span class="n">stats</span><span class="o">.</span><span class="n">ttest_ind</span><span class="p">(</span><span class="n">bs_replicates_f</span><span class="p">,</span> <span class="n">bs_replicates_m</span><span class="p">,</span> <span class="n">equal_var</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Welch</span><span class="se">\&#39;</span><span class="s1">s t-test:</span><span class="se">\n</span><span class="s1">t-statistic: </span><span class="si">{:0.5}</span><span class="se">\n</span><span class="s1">p-value: </span><span class="si">{:0.5}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">result</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="n">result</span><span class="p">[</span><span class="mi">1</span><span class="p">]))</span>
</pre>
                </div>

            </div>
        </div>
    </div>

    <div class="output_wrapper">
        <div class="output">


            <div class="output_area">

                <div class="prompt"></div>


                <div class="output_subarea output_stream output_stdout output_text">
                    <pre>Welch&#39;s t-test:
t-statistic: 232.76
p-value: 0.0
</pre>
                </div>
            </div>

        </div>
    </div>

</div>
<div class="cell border-box-sizing text_cell rendered">
    <div class="prompt input_prompt">
    </div>
    <div class="inner_cell">
        <div class="text_cell_render border-box-sizing rendered_html">
            <div class="alert alert-block alert-success">
                <h4>Analysis:</h4>
                <p>The mean human body temperature has been proven to be 98.25°, rather than 98.6°. The sample consists of 130
                    samples; 65 male and 65 female.</p>

                <p>A boxplot (Fig. 6.1) shows that the females' mean body temperature is slightly higher than the males'.</p>

                <p>CDFs (Fig. 6.2) show that both sample sets roughly follow the standard normal distribution, with the females'
                    temperatures running a little warmer and with slightly more variation.</p>

                <p>The distributions for both samples approximate the standard normal distribution and both sample sizes are
                    sufficiently large, so the Central Limit Theorem applies and inferences can be made based on the properties
                    of the normal distribution.</p>

                $$H_0: \bar x_m = \bar x_f$$ $$H_A: \bar x_m \neq \bar x_f$$


                <p>The null hypothesis is that the mean male body temperature is equal to the mean female body temperature.
                    An unequal variance $t$-test will be used to test the means of two continuous distributions with unequal
                    variances. Because the null hypothesis is that the means are equal, a two-tailed test is required.
                </p>

                <p>The p-values and $t$-statistics for both the bootstrap and frequentist hypothesis tests require that the
                    null hypothesis be rejected and support the alternate hypothesis that mean male and female body temperatures
                    are different. A table summarizing the differences between male and female mean body temperatures is
                    provided below:</p>

                <table>
                    <thead>
                        <tr>
                            <th></th>
                            <th>Male</th>
                            <th>Female</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>$\bar x$</td>
                            <td>98.105</td>
                            <td>98.394</td>
                        </tr>
                        <tr>
                            <td>$s$</td>
                            <td>0.693</td>
                            <td>0.738</td>
                        </tr>
                        <tr>
                            <td>Margin of Error</td>
                            <td>1.359</td>
                            <td>1.446</td>
                        </tr>
                        <tr>
                            <td>95% Conf. Int.</td>
                            <td>(96.746, 99.464)</td>
                            <td>(96.948, 99.84)</td>
                        </tr>
                    </tbody>
                </table>

            </div>
        </div>
    </div>
</div>