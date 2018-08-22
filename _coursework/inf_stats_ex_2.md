--- 
title: Inferential Statistics - Racial Discrimination
permalink: /coursework/stats/racial_disc/
---


<div class="cell border-box-sizing text_cell rendered">
  <div class="prompt input_prompt">
  </div>
  <div class="inner_cell">
    <div class="text_cell_render border-box-sizing rendered_html">
      <h1 id="Examining-Racial-Discrimination-in-the-US-Job-Market">Examining Racial Discrimination in the US Job Market
        <a class="anchor-link" href="#Examining-Racial-Discrimination-in-the-US-Job-Market">&#182;</a>
      </h1>
      <h3 id="Background">Background
        <a class="anchor-link" href="#Background">&#182;</a>
      </h3>
      <p>Racial discrimination continues to be pervasive in cultures throughout the world. Researchers examined the level of
        racial discrimination in the United States labor market by randomly assigning identical résumés to black-sounding
        or white-sounding names and observing the impact on requests for interviews from employers.</p>
      <h3 id="Data">Data
        <a class="anchor-link" href="#Data">&#182;</a>
      </h3>
      <p>In the dataset provided, each row represents a resume. The 'race' column has two values, 'b' and 'w', indicating black-sounding
        and white-sounding. The column 'call' has two values, 1 and 0, indicating whether the resume received a call from
        employers or not.</p>
      <p>Note that the 'b' and 'w' values in race are assigned randomly to the resumes when presented to the employer.</p>

    </div>
  </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
  <div class="prompt input_prompt">
  </div>
  <div class="inner_cell">
    <div class="text_cell_render border-box-sizing rendered_html">
      <h3 id="Exercises">Exercises
        <a class="anchor-link" href="#Exercises">&#182;</a>
      </h3>
      <p>You will perform a statistical analysis to establish whether race has a significant impact on the rate of callbacks
        for resumes.</p>
      <p>Answer the following questions
        <strong>in this notebook below and submit to your Github account</strong>.</p>
      <ol>
        <li>What test is appropriate for this problem? Does CLT apply?</li>
        <li>What are the null and alternate hypotheses?</li>
        <li>Compute margin of error, confidence interval, and p-value. Try using both the bootstrapping and the frequentist statistical
          approaches.</li>
        <li>Write a story describing the statistical significance in the context or the original problem.</li>
        <li>Does your analysis mean that race/name is the most important factor in callback success? Why or why not? If not,
          how would you amend your analysis?</li>
      </ol>
      <p>You can include written notes in notebook cells using Markdown:</p>
      <ul>
        <li>In the control panel at the top, choose Cell &gt; Cell Type &gt; Markdown</li>
        <li>Markdown syntax:
          <a href="://nestacms.com/docs/creating-content/markdown-cheat-sheet" target="_blank">http://nestacms.com/docs/creating-content/markdown-cheat-sheet</a>
        </li>
      </ul>
      <h4 id="Resources">Resources
        <a class="anchor-link" href="#Resources">&#182;</a>
      </h4>
      <ul>
        <li>Experiment information and data source:
          <a href="http://www.povertyactionlab.org/evaluation/discrimination-job-market-united-states" target="_blank">http://www.povertyactionlab.org/evaluation/discrimination-job-market-united-states</a>
        </li>
        <li>Scipy statistical methods:
          <a href="http://docs.scipy.org/doc/scipy/reference/stats.html" target="_blank">http://docs.scipy.org/doc/scipy/reference/stats.html</a>
        </li>
        <li>Markdown syntax:
          <a href="http://nestacms.com/docs/creating-content/markdown-cheat-sheet" target="_blank">http://nestacms.com/docs/creating-content/markdown-cheat-sheet</a>
        </li>
        <li>Formulas for the Bernoulli distribution:
          <a href="https://en.wikipedia.org/wiki/Bernoulli_distribution" target="_blank">https://en.wikipedia.org/wiki/Bernoulli_distribution</a>
        </li>
      </ul>
      <hr>

    </div>
  </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
  <div class="prompt input_prompt">
  </div>
  <div class="inner_cell">
    <div class="text_cell_render border-box-sizing rendered_html">
      <h2 id="Summary-of-Findings">Summary of Findings
        <a class="anchor-link" href="#Summary-of-Findings">&#182;</a>
      </h2>
      <hr>

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
<span class="kn">import</span> <span class="nn">matplotlib.mlab</span> <span class="k">as</span> <span class="nn">mlab</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="kn">import</span> <span class="nn">scipy.stats</span> <span class="k">as</span> <span class="nn">stats</span>
<span class="kn">import</span> <span class="nn">pylab</span>

<span class="c1"># matplotlib setup</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
<span class="n">plt</span><span class="o">.</span><span class="n">style</span><span class="o">.</span><span class="n">use</span><span class="p">(</span><span class="s1">&#39;fivethirtyeight&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s2">&quot;figure.figsize&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">8</span><span class="p">)</span>

<span class="c1"># turn edges on in plt</span>
<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s2">&quot;patch.force_edgecolor&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="kc">True</span>

<span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="mi">42</span><span class="p">)</span>
</pre>
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
<div class="cell border-box-sizing code_cell rendered">
  <div class="input">
    <div class="prompt input_prompt">In&nbsp;[3]:</div>
    <div class="inner_cell">
      <div class="input_area">
        <div class=" highlight hl-ipython3">
          <pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">io</span><span class="o">.</span><span class="n">stata</span><span class="o">.</span><span class="n">read_stata</span><span class="p">(</span><span class="s1">&#39;data/us_job_market_discrimination.dta&#39;</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre>
        </div>

      </div>
    </div>
  </div>

  <div class="output_wrapper">
    <div class="output">


      <div class="output_area">

        <div class="prompt output_prompt">Out[3]:</div>



        <div class="output_html rendered_html output_subarea output_execute_result">
          <div>
            <style scoped>
              .dataframe tbody tr th:only-of-type {
                vertical-align: middle;
              }

              .dataframe tbody tr th {
                vertical-align: top;
              }

              .dataframe thead th {
                text-align: right;
              }
            </style>
            <table border="1" class="dataframe">
              <thead>
                <tr style="text-align: right;">
                  <th></th>
                  <th>id</th>
                  <th>ad</th>
                  <th>education</th>
                  <th>ofjobs</th>
                  <th>yearsexp</th>
                  <th>honors</th>
                  <th>volunteer</th>
                  <th>military</th>
                  <th>empholes</th>
                  <th>occupspecific</th>
                  <th>...</th>
                  <th>compreq</th>
                  <th>orgreq</th>
                  <th>manuf</th>
                  <th>transcom</th>
                  <th>bankreal</th>
                  <th>trade</th>
                  <th>busservice</th>
                  <th>othservice</th>
                  <th>missind</th>
                  <th>ownership</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <th>0</th>
                  <td>b</td>
                  <td>1</td>
                  <td>4</td>
                  <td>2</td>
                  <td>6</td>
                  <td>0</td>
                  <td>0</td>
                  <td>0</td>
                  <td>1</td>
                  <td>17</td>
                  <td>...</td>
                  <td>1.0</td>
                  <td>0.0</td>
                  <td>1.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td></td>
                </tr>
                <tr>
                  <th>1</th>
                  <td>b</td>
                  <td>1</td>
                  <td>3</td>
                  <td>3</td>
                  <td>6</td>
                  <td>0</td>
                  <td>1</td>
                  <td>1</td>
                  <td>0</td>
                  <td>316</td>
                  <td>...</td>
                  <td>1.0</td>
                  <td>0.0</td>
                  <td>1.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td></td>
                </tr>
                <tr>
                  <th>2</th>
                  <td>b</td>
                  <td>1</td>
                  <td>4</td>
                  <td>1</td>
                  <td>6</td>
                  <td>0</td>
                  <td>0</td>
                  <td>0</td>
                  <td>0</td>
                  <td>19</td>
                  <td>...</td>
                  <td>1.0</td>
                  <td>0.0</td>
                  <td>1.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td></td>
                </tr>
                <tr>
                  <th>3</th>
                  <td>b</td>
                  <td>1</td>
                  <td>3</td>
                  <td>4</td>
                  <td>6</td>
                  <td>0</td>
                  <td>1</td>
                  <td>0</td>
                  <td>1</td>
                  <td>313</td>
                  <td>...</td>
                  <td>1.0</td>
                  <td>0.0</td>
                  <td>1.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td></td>
                </tr>
                <tr>
                  <th>4</th>
                  <td>b</td>
                  <td>1</td>
                  <td>3</td>
                  <td>3</td>
                  <td>22</td>
                  <td>0</td>
                  <td>0</td>
                  <td>0</td>
                  <td>0</td>
                  <td>313</td>
                  <td>...</td>
                  <td>1.0</td>
                  <td>1.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>0.0</td>
                  <td>1.0</td>
                  <td>0.0</td>
                  <td>Nonprofit</td>
                </tr>
              </tbody>
            </table>
            <p>5 rows × 65 columns</p>
          </div>
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
          <pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre>
        </div>

      </div>
    </div>
  </div>

  <div class="output_wrapper">
    <div class="output">


      <div class="output_area">

        <div class="prompt output_prompt">Out[4]:</div>



        <div class="output_html rendered_html output_subarea output_execute_result">
          <div>
            <style scoped>
              .dataframe tbody tr th:only-of-type {
                vertical-align: middle;
              }

              .dataframe tbody tr th {
                vertical-align: top;
              }

              .dataframe thead th {
                text-align: right;
              }
            </style>
            <table border="1" class="dataframe">
              <thead>
                <tr style="text-align: right;">
                  <th></th>
                  <th>education</th>
                  <th>ofjobs</th>
                  <th>yearsexp</th>
                  <th>honors</th>
                  <th>volunteer</th>
                  <th>military</th>
                  <th>empholes</th>
                  <th>occupspecific</th>
                  <th>occupbroad</th>
                  <th>workinschool</th>
                  <th>...</th>
                  <th>educreq</th>
                  <th>compreq</th>
                  <th>orgreq</th>
                  <th>manuf</th>
                  <th>transcom</th>
                  <th>bankreal</th>
                  <th>trade</th>
                  <th>busservice</th>
                  <th>othservice</th>
                  <th>missind</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <th>count</th>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>...</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                  <td>4870.000000</td>
                </tr>
                <tr>
                  <th>mean</th>
                  <td>3.618480</td>
                  <td>3.661396</td>
                  <td>7.842916</td>
                  <td>0.052772</td>
                  <td>0.411499</td>
                  <td>0.097125</td>
                  <td>0.448049</td>
                  <td>215.637782</td>
                  <td>3.481520</td>
                  <td>0.559548</td>
                  <td>...</td>
                  <td>0.106776</td>
                  <td>0.437166</td>
                  <td>0.072690</td>
                  <td>0.082957</td>
                  <td>0.030390</td>
                  <td>0.085010</td>
                  <td>0.213963</td>
                  <td>0.267762</td>
                  <td>0.154825</td>
                  <td>0.165092</td>
                </tr>
                <tr>
                  <th>std</th>
                  <td>0.714997</td>
                  <td>1.219126</td>
                  <td>5.044612</td>
                  <td>0.223601</td>
                  <td>0.492156</td>
                  <td>0.296159</td>
                  <td>0.497345</td>
                  <td>148.127551</td>
                  <td>2.038036</td>
                  <td>0.496492</td>
                  <td>...</td>
                  <td>0.308866</td>
                  <td>0.496083</td>
                  <td>0.259649</td>
                  <td>0.275854</td>
                  <td>0.171677</td>
                  <td>0.278932</td>
                  <td>0.410141</td>
                  <td>0.442847</td>
                  <td>0.361773</td>
                  <td>0.371308</td>
                </tr>
                <tr>
                  <th>min</th>
                  <td>0.000000</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>7.000000</td>
                  <td>1.000000</td>
                  <td>0.000000</td>
                  <td>...</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                </tr>
                <tr>
                  <th>25%</th>
                  <td>3.000000</td>
                  <td>3.000000</td>
                  <td>5.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>27.000000</td>
                  <td>1.000000</td>
                  <td>0.000000</td>
                  <td>...</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                </tr>
                <tr>
                  <th>50%</th>
                  <td>4.000000</td>
                  <td>4.000000</td>
                  <td>6.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>267.000000</td>
                  <td>4.000000</td>
                  <td>1.000000</td>
                  <td>...</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                </tr>
                <tr>
                  <th>75%</th>
                  <td>4.000000</td>
                  <td>4.000000</td>
                  <td>9.000000</td>
                  <td>0.000000</td>
                  <td>1.000000</td>
                  <td>0.000000</td>
                  <td>1.000000</td>
                  <td>313.000000</td>
                  <td>6.000000</td>
                  <td>1.000000</td>
                  <td>...</td>
                  <td>0.000000</td>
                  <td>1.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                  <td>1.000000</td>
                  <td>0.000000</td>
                  <td>0.000000</td>
                </tr>
                <tr>
                  <th>max</th>
                  <td>4.000000</td>
                  <td>7.000000</td>
                  <td>44.000000</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                  <td>903.000000</td>
                  <td>6.000000</td>
                  <td>1.000000</td>
                  <td>...</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                  <td>1.000000</td>
                </tr>
              </tbody>
            </table>
            <p>8 rows × 55 columns</p>
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
      <h2 id="Generate-some-basic-statistics-about-the-data-set">Generate some basic statistics about the data set
        <a class="anchor-link" href="#Generate-some-basic-statistics-about-the-data-set">&#182;</a>
      </h2>
    </div>
  </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
  <div class="input">
    <div class="prompt input_prompt">In&nbsp;[5]:</div>
    <div class="inner_cell">
      <div class="input_area">
        <div class=" highlight hl-ipython3">
          <pre><span></span><span class="c1"># aggregate values</span>
<span class="n">r</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">call</span><span class="p">)</span>
<span class="n">n</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span>
<span class="n">p</span> <span class="o">=</span> <span class="n">r</span><span class="o">/</span><span class="n">n</span>

<span class="n">w</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">race</span> <span class="o">==</span> <span class="s1">&#39;w&#39;</span><span class="p">]</span>
<span class="n">b</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">race</span> <span class="o">==</span> <span class="s1">&#39;b&#39;</span><span class="p">]</span>

<span class="c1"># white-sounding names</span>
<span class="n">w_r</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">w</span><span class="o">.</span><span class="n">call</span><span class="p">)</span>
<span class="n">w_n</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">w</span><span class="p">)</span>
<span class="n">w_p</span> <span class="o">=</span> <span class="p">(</span><span class="n">w_r</span> <span class="o">/</span> <span class="n">w_n</span><span class="p">)</span>


<span class="c1"># black-sounding names</span>
<span class="n">b_r</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">b</span><span class="o">.</span><span class="n">call</span><span class="p">)</span>
<span class="n">b_n</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">b</span><span class="p">)</span>
<span class="n">b_p</span> <span class="o">=</span> <span class="p">(</span><span class="n">b_r</span> <span class="o">/</span> <span class="n">b_n</span><span class="p">)</span>


<span class="n">data</span> <span class="o">=</span> <span class="p">{</span><span class="s1">&#39;CB&#39;</span><span class="p">:</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="n">w_r</span><span class="p">,</span> <span class="n">b_r</span><span class="p">,</span> <span class="n">r</span><span class="p">])</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">),</span>
        <span class="s1">&#39;No CB&#39;</span><span class="p">:</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="n">w_n</span> <span class="o">-</span> <span class="n">w_r</span><span class="p">,</span> <span class="n">b_n</span> <span class="o">-</span> <span class="n">b_r</span><span class="p">,</span> <span class="n">n</span> <span class="o">-</span> <span class="n">r</span><span class="p">])</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">),</span>
        <span class="s1">&#39;Total&#39;</span><span class="p">:</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="n">w_n</span><span class="p">,</span> <span class="n">b_n</span><span class="p">,</span> <span class="n">n</span><span class="p">])</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">),</span>
        <span class="s1">&#39;% Success&#39;</span><span class="p">:</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="s1">&#39;</span><span class="si">{:.2%}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">w_r</span><span class="o">/</span><span class="n">w_n</span><span class="p">),</span> <span class="s1">&#39;</span><span class="si">{:.2%}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">b_r</span><span class="o">/</span><span class="n">b_n</span><span class="p">),</span> <span class="s1">&#39;</span><span class="si">{:.2%}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">r</span><span class="o">/</span><span class="n">n</span><span class="p">)])}</span>

<span class="n">tbl</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;CB&#39;</span><span class="p">,</span> <span class="s1">&#39;No CB&#39;</span><span class="p">,</span> <span class="s1">&#39;Total&#39;</span><span class="p">,</span> <span class="s1">&#39;% Success&#39;</span><span class="p">],</span> 
                   <span class="n">index</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;White-sounding names&#39;</span><span class="p">,</span> <span class="s1">&#39;Black-sounding names&#39;</span><span class="p">,</span> <span class="s1">&#39;Aggregate&#39;</span><span class="p">])</span>
<span class="n">tbl</span>
</pre>
        </div>

      </div>
    </div>
  </div>

  <div class="output_wrapper">
    <div class="output">


      <div class="output_area">

        <div class="prompt output_prompt">Out[5]:</div>



        <div class="output_html rendered_html output_subarea output_execute_result">
          <div>
            <style scoped>
              .dataframe tbody tr th:only-of-type {
                vertical-align: middle;
              }

              .dataframe tbody tr th {
                vertical-align: top;
              }

              .dataframe thead th {
                text-align: right;
              }
            </style>
            <table border="1" class="dataframe">
              <thead>
                <tr style="text-align: right;">
                  <th></th>
                  <th>CB</th>
                  <th>No CB</th>
                  <th>Total</th>
                  <th>% Success</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <th>White-sounding names</th>
                  <td>235</td>
                  <td>2200</td>
                  <td>2435</td>
                  <td>9.65%</td>
                </tr>
                <tr>
                  <th>Black-sounding names</th>
                  <td>157</td>
                  <td>2278</td>
                  <td>2435</td>
                  <td>6.45%</td>
                </tr>
                <tr>
                  <th>Aggregate</th>
                  <td>392</td>
                  <td>4478</td>
                  <td>4870</td>
                  <td>8.05%</td>
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
    <div class="prompt input_prompt">In&nbsp;[13]:</div>
    <div class="inner_cell">
      <div class="input_area">
        <div class=" highlight hl-ipython3">
          <pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">style</span><span class="o">.</span><span class="n">use</span><span class="p">(</span><span class="s1">&#39;fivethirtyeight&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s2">&quot;figure.figsize&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">8</span><span class="p">)</span>

<span class="c1"># Plot CDFs of callbacks for black- vs. white-sounding names</span>
<span class="n">w_samples</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">binomial</span><span class="p">(</span><span class="n">w_n</span><span class="p">,</span> <span class="n">w_p</span><span class="p">,</span> <span class="n">size</span><span class="o">=</span><span class="mi">10000</span><span class="p">)</span>
<span class="n">b_samples</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">binomial</span><span class="p">(</span><span class="n">b_n</span><span class="p">,</span> <span class="n">b_p</span><span class="p">,</span> <span class="n">size</span><span class="o">=</span><span class="mi">10000</span><span class="p">)</span>

<span class="n">bx</span><span class="p">,</span> <span class="n">by</span> <span class="o">=</span> <span class="n">ecdf</span><span class="p">(</span><span class="n">b_samples</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">bx</span><span class="p">,</span> <span class="n">by</span><span class="p">,</span> <span class="n">marker</span><span class="o">=</span><span class="s1">&#39;.&#39;</span><span class="p">,</span> <span class="n">linestyle</span><span class="o">=</span><span class="s1">&#39;none&#39;</span><span class="p">)</span>

<span class="n">wx</span><span class="p">,</span> <span class="n">wy</span> <span class="o">=</span> <span class="n">ecdf</span><span class="p">(</span><span class="n">w_samples</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">wx</span><span class="p">,</span> <span class="n">wy</span><span class="p">,</span> <span class="n">marker</span><span class="o">=</span><span class="s1">&#39;.&#39;</span><span class="p">,</span> <span class="n">linestyle</span><span class="o">=</span><span class="s1">&#39;none&#39;</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">margins</span> <span class="o">=</span> <span class="mf">0.02</span>

<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;number of callbacks&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;CDF&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Black- vs. White-sounding Names&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">((</span><span class="s1">&#39;Black-sounding Names&#39;</span><span class="p">,</span> <span class="s1">&#39;White-sounding Names&#39;</span><span class="p">),</span> <span class="n">loc</span><span class="o">=</span><span class="s1">&#39;lower right&#39;</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="s1">&#39;large&#39;</span><span class="p">,</span> <span class="n">markerscale</span><span class="o">=</span><span class="mi">2</span><span class="p">)</span>
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
          <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAArAAAAIdCAYAAADFxk6GAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4yLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvhp/UCwAAIABJREFUeJzs3Xl4U2X+/vE7SZcAAoVSyloYBBlAKsomm1QYBUV0RAERtTAiFWFEZdcRYRhHkXH8ucOIQBkVv6AssqjIIgUFFwRxlKWCIhRbZF9K6ZL8/mgTW5o26XpykvfrurhKzzlJPj1dcufJ5zyP5dSpU04BAAAAJmE1ugAAAACgJAiwAAAAMBUCLAAAAEyFAAsAAABTIcACAADAVAiwAAAAMBUCLFAB3n77bUVEROjtt9+u9Md85plnKu0xA01ERITatm3r8/EHDx5URESERo0aVYFVBTfXOe7Xr1+B7c8884wiIiK0efNmgyoDYCQCLOBFREREoX9RUVFq3bq1hg0bpu3btxtdYtDJyclRkyZNFBkZqVOnThXaf/bsWdWpU0cRERF6+eWXPd5HQkKCIiIi9NZbb5V7ff369VNERIQOHjxY7vcN/+b63teuXVvffvutx2OmTZtW6S9wgUBDgAV8NGnSJPe/kSNHqnnz5lqxYoX69OmjdevWGV1eULHZbOrevbtycnL02WefFdr/2WefKTs7WxaLRZs2bfJ4H1u2bJEk9ezZs9R1NGjQQF9++aWeeuqpUt8HSmfkyJH68ssv1b59e6NL8cjhcOhvf/ub0WUAASvE6AIAs5gyZUqhbS+99JKmTp2qF154QX/6058MqCp49ezZU6tXr9amTZsKvb28adMmWa1W9e/fX+vWrVNmZqbCwsLc+5OTk5WSkqJmzZqpcePGpa4hNDRUV1xxRalvj9KLjIxUZGSk0WUU6fLLL9fmzZu1Zs0a3XzzzUaXAwQcRmCBMujdu7ck6fjx4z4dn5SUpIcfflidOnVS48aNVa9ePV177bX65z//qQsXLni8TU5OjhYuXKibbrpJTZo0UXR0tGJjYzVixAjt2LHD62NmZmZq5MiRioiI0IMPPqisrCzfv8B8jhw5otq1a6tr165FHvOXv/xFERERBUY9V65cqVtvvVUtW7ZU3bp11bJlS/Xp00fPP/98qepwcY2cJiUlFdqXlJSkK6+8UrfeeqvOnz+vr7/+utB+SYqLi/N43+np6XryySd15ZVXqm7durr66qv1wgsvyOksuPK2px7YiIgI96jwVVdd5W47ubS39vTp03r66afVpUsX1a9fX40aNVLfvn21fPnykp0ISZs3b9bgwYPVpk0b1a1bV82bN1dcXJyeeOKJQjWfOXNGM2bMUMeOHRUdHa2YmBjdcsstWrlypcf7La6v2vV2uafbjBo1SgcPHtRf/vIXNWvWTNHR0erZs6fWrFnj8b7Onj2rxx9/XK1bt1Z0dLQ6duyol19+uVD9LkX1wLrOta/fQyl3tPS1115Tp06dFB0drVatWmnChAk6ffq02rZtW+hr9MXUqVNls9n01FNPKTs726fb7Ny5UxMnTlTXrl3dv+vXXHONHn/8cZ08ebLQ8fn73nfs2KE77rhDMTExiomJ0b333qvDhw9Lkg4cOKBhw4bp8ssvV7169dSvXz999913HmvIyMjQyy+/rJ49e6phw4Zq0KCB4uLiNG/ePI/nrqJ+vwFvGIEFymDDhg2SpGuuucan41988UXt27dPnTt3Vp8+fZSRkaFt27bpueee0+bNm7Vy5UqFhPz+a5mZmam7775b69atU7169XT77berVq1aOnz4sDZv3qzLL79cV199dZGPd/r0ad17771KSkrS+PHjy/SWZoMGDXT99ddr/fr12rlzp9q1a1fosdasWaNGjRqpR48ekqQ333xT48aNU926ddWnTx9FRUXp+PHj2rt3r+bPn69x48aVup6WLVuqfv362rNnj1JTU1WvXj1J0rFjx/TDDz9o9OjR7jo2bdpUIHi7Aran9oHs7GwNGDBAqamp+tOf/qSQkBCtXr1a06dP14ULF/T4448XW9ekSZP0zjvv6NChQ3rwwQdVs2ZNSXJ/lHJfDPTv31/79+9Xly5dNGzYMKWnp2vt2rUaNmyYJk2a5HHE35O1a9dq8ODBql69um666SY1bNhQp06d0v79+zVnzhxNnz7d/TN16tQp9e3bV3v27FFsbKwefPBBnT59WsuXL9e9996riRMnev36fHXo0CH17t1bf/jDHzR48GCdPHlSy5Yt09ChQ7V8+fIC5/7ixYu67bbb9M0336h169YaOHCgzpw5o+eff95ji4g3Jf0ePvbYY1qwYIHq1aun++67T+Hh4fr444+1fft2n8PnpVq1aqV77rlHiYmJmjdvnkaOHOn1NomJiVq1apW6deum66+/Xjk5Odq5c6dee+01ffLJJ9qwYYOqV69e6HY7duzQSy+9pOuuu0733Xeftm/frpUrV+qHH37Q22+/rb59+6pt27YaMmSI9u7dq08++US33367du7cqcsuu8x9P2fPntWf//xnbd++XbGxsbr77rslSevXr9djjz2mr776Sq+//rr7+Ir8/Qa8IcACPso/CnX+/Hl9//332rRpk7p06eJzD+Tzzz+vJk2ayGKxFNj+97//Xf/+97+1YsUK3XHHHe7tM2fO1Lp16xQXF6d33nlHVatWde/LycnRb7/9VuRjHT58WIMGDdK+ffv00ksv6b777vP1Sy3S0KFDtX79er399tuFAuyyZcuUkZGhu+66S1Zr7ps7iYmJCgsL0+bNmxUdHV3geF9HrYvTo0cPLV68WElJSRo0aJCk3NFVp9Op6667zj0ilJSU5A6ETqdTW7ZskdVq1XXXXVfoPn/99VfFxsZq+fLlstvtknJDafv27TV79mxNmDBBoaGhRdY0ZcoUbdmyRYcOHdKoUaPUpEmTQseMGjVKBw4c0Ny5c3XnnXe6t585c0a33HKLnnvuOfXr10+xsbFez8HChQvldDq1cuVKXXXVVQX2nThxosALomnTpmnPnj0aOnSoXnnlFffP4YQJE9SrVy/NmjVLffr0KZe+0i1btuiJJ57QhAkT3NsGDhyoO+64wz3C5/LKK6/om2++0c0336y33nrL/fPz6KOPFjlKXpySfA+3bNmiBQsWqFmzZtqwYYN7tHXq1KkaMGCAfv3119KeAj3xxBN6//33NXPmTA0aNMjrSO6jjz6qf/3rX7LZbAW2z58/X48++qjmzp2rRx99tNDt1q5dq8TERN12222Scn/G77zzTq1fv1433nijJk+erIceesh9/NixY5WYmKj//ve/Bd49ePzxx7V9+3ZNmzZNjzzyiHv7xYsXde+992rRokXq37+/uyWion+/geLQQgD4aObMme5/r7zyijZu3KiGDRvqrrvuKvTHuyhNmzYtFF4lacyYMZJ+H9GVcgPq3LlzFR4erhdffLFAeJVyL2RyjTpe6rvvvtONN96oX375RYsWLSqX8CrlvmVcs2ZNvf/++8rMzCyw75133pEk96iNJFmtVoWEhBToP3Upj/5FVwjK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11+XqX3AxWKxuFuMipoJxPX34eabby50keD27duLnGavvHTo0EFWq7XUP5cV9fsNFIUAC5TBqlWrdPDgQYWGhhYKTZdyjc5eOm/lzz//7HEWA5vNpgceeEAXL17UI488UugJLCcnR6mpqUU+3t///ndNmjRJ27Zt02233eZxHsnSGjx4sGw2m9555x33xVue2g8++eQTj/POukb78l9kc/r0ae3bt69EYV3KDbBWq1WbN29WUlKSOnXqpPDw8ALH9OjRQ06nU//85z8llW31LV+4LmDx9LW0a9dO3bp105o1a5SYmOjxhc+PP/7o83n49NNPlZ6eXmj7pec4NDRUgwcPVnp6uqZPn16o9/qFF16QxWLRPffc495+xRVXqEaNGlqzZo37/qTcfsgpU6aUW6gaOnSonE6npk6dWiD0//LLL+63pSvKXXfdJUl64YUXCox0Z2VlacaMGeX2ON26dVO/fv301VdfeZxz1/X34dLe9N9++03jx48vtzqKUqdOHQ0ePFjfffednnnmGY/BPSUlxd2bLZXs9xsob7QQAD7Kf2FDenq6ez5FKXfKHW+9en379lWzZs302muvaffu3YqNjdXhw4f18ccf68Ybb/Q4yjVx4kTt2LFD69ev1zXXXKO+ffuqVq1aOnLkiDZv3qx77rmn2FaAKVOmqFq1apo6dapuueUWLV++vMhew5KoV6+eevfurbVr12rfvn0F5n7N7/7771dYWJi6dOmimJgYWSwWbd++XVu3blXTpk315z//2X3sqlWrNHr0aHXr1k2rV6/2uZZatWqpbdu27ouPRowYUeiYbt26yWq16ocffpBU9AVc5eX666/XsmXLNHbsWN12222qVq2aatas6Z4LdO7cubrttts0duxYzZkzRx07dnR/X/fs2aNdu3bprbfe8mmVsL/97W/65Zdf1K1bN8XExMhut+v777/X+vXrVbt2bcXHx7uPfeqpp7R161YtXLhQu3btUlxcnHse2JMnT2rixInq0KGD+/jQ0FD99a9/1dNPP63rrrtO/fv3l5T7IszpdOrKK6/U//73vzKfrzFjxmj16tVas2aNevTooT/96U86c+aMli1bpi5duujDDz8s82MUpXv37ho2bJgWLFigLl26qH///goPD9dHH32k6tWrq379+sW+UCyJv//971q7dq3HketrrrlG1157rVauXKkbb7xR1157rY4ePap169apRYsWql+/frnUUJznnntOBw4c0MyZM/V///d/6tq1q6Kjo92j41999ZWefvpp9+pzJfn9BsobARbwUf4eVZvNpjp16qhv374aOXKkrr/+eq+3r1atmj744ANNnz5dW7Zscf+RnzBhgkaPHq2lS5cWuk1YWJgWL16sxMRELVq0SEuWLFF2draio6PVrVs33XTTTV4f9+GHH1aVKlU0ceJE9evXTytWrCiXJ8OhQ4dq7dq1ysrKKjD3a37Tpk3Thg0b9N1332n9+vUKCQlRo0aNNGnSJCUkJJRqhSNPevbs6Q6wnuZ2da3O9O2336pGjRo+LzxRWvfcc49SUlK0ePFivfrqq8rKylLjxo3dAbZ+/frauHGj3njjDa1YsULvv/++srKy3KtoPfvss+revbtPjzVu3DitXr1aO3bscI/uN2jQQKNGjdJDDz2kRo0auY+NiIjQxx9/rBdffFEffPCBXnvtNYWHhys2NlYJCQke21vGjx+vKlWqaP78+UpMTFTt2rXVr18/PfnkkwVGa8siPDxcy5cv17PPPqtly5Zp9uzZiomJ0bhx49S/f/8KDbCS9O9//1stWrTQggULtGDBAtWuXVu33HKLnnzySbVp06bIi8JK6vLLL9f999+v2bNnF9pns9m0aNEi/eMf/9DatWs1Z84c1a9fX/fdd5/Gjx/v9R2e8lC9enWtWrVK//3vf7VkyRKtWrVKGRkZioqKUkxMjKZOnVoglFbW7zfgieXUqVPFN+4BABCE9u/fr/bt26tTp05au3at0eUAyIceWABAUDt69GihC+7S09Pd7TmeRqYBGIsWAgBAUPvPf/6jd999V927d1e9evWUlpampKQkpaSk6JprrtEDDzxgdIkALkGABQAEtZ49e+p///ufNm/erOPHj8tisegPf/iD7r33Xv31r38tNKsFAOPRAwsAAABToQcWAAAApkKABQAAgKkQYAEAAGAqBFg/l5ycbHQJAYdzWv44pxWD81r+OKflj3Na/jin3hFgAQAAYCoEWAAAAJgKARYAAACmQoAFAACAqRBgAQAAYCoEWAAAAJgKARYAAACmQoAFAACAqRBgAQAAYCoEWAAAAJgKARYAAACmQoAFAACAqRBgAQAAYCoEWAAAAJiKoQH2s88+01133aVWrVopIiJCb7/9ttfbfP/9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
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
      <h3 id="Question-#1:-What-is-the-appropriate-test-for-this-problem?">Q1: Appropriate Test?
        <a class="anchor-link" href="#1: Appropriate Test?">&#182;</a>
      </h3>
      <p>What is the appropriate test for this problem?</p>
      <hr>
      <p>The null hypothesis for this problem is that the proportions in the two populations, from which the two samples are
        drawn, are equal. Therefore, a $Z$-test for proportions will be used. These samples are binomial distributions, and
        a callback will be labeled a success.</p>
      <p>Since there is no $t$-test for comparing proportions, in order to compare the proportions using a Frequentist approach,
        the $Z$-test for proportions will be used:</p>
      <p>$$Z = \frac{p_1 - p_2}{\sqrt{\hat p_1(1 - \hat p)\left(\frac{1}{n_1}+\frac{1}{n_2}\right)}}$$</p>
      <p>where $$\hat p = \frac{n_1p_1 + n_2p_2}{n_1 + n_2}$$</p>
      <p>When sample sizes $n_1$ and $n_2$ are large enough and/or the proportions in each sample ($p_1$ and $p_2$) are close
        enough to 0.5, the difference between the two proportions is Normally distributed. One guideline is that all of the
        following conditions must hold true for this Normal approximation to be valid:</p>
      <p>$n_1\ *\ p_1 \ge 5$
        <br> $n_2\ *\ p_2 \ge 5$
        <br> $n_1\ *\ (1-p_1) \ge 5$
        <br> $n_2\ *\ (1-p_2) \ge 5$</p>
      <p>Inserting the sample data yields the following:</p>

    </div>
  </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
  <div class="input">
    <div class="prompt input_prompt">In&nbsp;[7]:</div>
    <div class="inner_cell">
      <div class="input_area">
        <div class=" highlight hl-ipython3">
          <pre><span></span><span class="n">r1</span> <span class="o">=</span> <span class="n">w_n</span> <span class="o">*</span> <span class="n">w_p</span> <span class="o">&gt;=</span> <span class="mi">5</span>
<span class="n">r2</span> <span class="o">=</span> <span class="n">b_n</span> <span class="o">*</span> <span class="n">b_p</span> <span class="o">&gt;=</span> <span class="mi">5</span>
<span class="n">r3</span> <span class="o">=</span> <span class="n">w_n</span> <span class="o">*</span> <span class="p">(</span><span class="mi">1</span><span class="o">-</span><span class="n">w_p</span><span class="p">)</span> <span class="o">&gt;=</span> <span class="mi">5</span>
<span class="n">r4</span> <span class="o">=</span> <span class="n">b_n</span> <span class="o">*</span> <span class="p">(</span><span class="mi">1</span><span class="o">-</span><span class="n">b_p</span><span class="p">)</span> <span class="o">&gt;=</span> <span class="mi">5</span>

<span class="n">r1</span>
<span class="n">r2</span>
<span class="n">r3</span>
<span class="n">r4</span>
</pre>
        </div>

      </div>
    </div>
  </div>

  <div class="output_wrapper">
    <div class="output">


      <div class="output_area">

        <div class="prompt output_prompt">Out[7]:</div>




        <div class="output_text output_subarea output_execute_result">
          <pre>True</pre>
        </div>

      </div>

      <div class="output_area">

        <div class="prompt output_prompt">Out[7]:</div>




        <div class="output_text output_subarea output_execute_result">
          <pre>True</pre>
        </div>

      </div>

      <div class="output_area">

        <div class="prompt output_prompt">Out[7]:</div>




        <div class="output_text output_subarea output_execute_result">
          <pre>True</pre>
        </div>

      </div>

      <div class="output_area">

        <div class="prompt output_prompt">Out[7]:</div>




        <div class="output_text output_subarea output_execute_result">
          <pre>True</pre>
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
      <p>The tests all pass, the Normal approximation is valid and the $Z$-test for proportions can be used. An alternative
        would be resampling, which requires no approximations and can operate with small samples and extreme proportions.</p>

    </div>
  </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
  <div class="prompt input_prompt">
  </div>
  <div class="inner_cell">
    <div class="text_cell_render border-box-sizing rendered_html">
      <h3 class="ilink" id="Question-#2:-Null-&amp;-Alternate-Hypotheses">Q2: Null &amp; Alternate Hypotheses
        <a class="anchor-link" href="#2:-Null-&amp;-Alternate-Hypotheses">&#182;</a>
      </h3>
      <p>What are the null and alternate hypotheses?</p>
      <hr>
      <p>
        <strong>Null Hypothesis</strong>: the probability of success (getting a callback) is the same for both resumes with white-sounding
        names and black-sounding names.
        <br> $$H_0: \widehat p_w - \widehat p_b = 0$$</p>
      <p>
        <strong>Alternate Hypothesis</strong>: the probability of success IS NOT THE SAME for resumes with white-sounding names as
        it is for those with black-sounding names.
        <br> $$H_a: \widehat p_w - \widehat p_b \neq 0$$</p>

    </div>
  </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
  <div class="prompt input_prompt">
  </div>
  <div class="inner_cell">
    <div class="text_cell_render border-box-sizing rendered_html">
      <h3 class="ilink" id="Q3:-Margin-of-Error,-Confidence-Interval-and-p-value-testing">Q3: p-value testing
        <a class="anchor-link" href="#Q3:-Margin-of-Error,-Confidence-Interval-and-p-value-testing">&#182;</a>
      </h3>
      <p>Margin of error, confidence interval and p-value testing</p>
      <hr>

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
      <p>$$(\hat p_1 - \hat p_2) \pm z*{\sqrt{\frac{\hat p_1(1 - \hat p_1)}{n_1} + \frac{\hat p_2(1-\hat p_2)}{n_2}}}$$</p>

    </div>
  </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
  <div class="input">
    <div class="prompt input_prompt">In&nbsp;[8]:</div>
    <div class="inner_cell">
      <div class="input_area">
        <div class=" highlight hl-ipython3">
          <pre><span></span><span class="k">def</span> <span class="nf">ztest_proportions_two_samples</span><span class="p">(</span><span class="n">r1</span><span class="p">,</span> <span class="n">n1</span><span class="p">,</span> <span class="n">r2</span><span class="p">,</span> <span class="n">n2</span><span class="p">,</span> <span class="n">one_sided</span><span class="o">=</span><span class="kc">False</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;Returns the z-statistic and p-value for a 2-sample Z-test of proportions&quot;&quot;&quot;</span>
    <span class="n">p1</span> <span class="o">=</span> <span class="n">r1</span><span class="o">/</span><span class="n">n1</span>
    <span class="n">p2</span> <span class="o">=</span> <span class="n">r2</span><span class="o">/</span><span class="n">n2</span>
    
    <span class="n">p</span> <span class="o">=</span> <span class="p">(</span><span class="n">r1</span><span class="o">+</span><span class="n">r2</span><span class="p">)</span><span class="o">/</span><span class="p">(</span><span class="n">n1</span><span class="o">+</span><span class="n">n2</span><span class="p">)</span>
    <span class="n">se</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">p</span><span class="o">*</span><span class="p">(</span><span class="mi">1</span><span class="o">-</span><span class="n">p</span><span class="p">)</span><span class="o">*</span><span class="p">(</span><span class="mi">1</span><span class="o">/</span><span class="n">n1</span><span class="o">+</span><span class="mi">1</span><span class="o">/</span><span class="n">n2</span><span class="p">))</span>
    
    <span class="n">z</span> <span class="o">=</span> <span class="p">(</span><span class="n">p1</span><span class="o">-</span><span class="n">p2</span><span class="p">)</span><span class="o">/</span><span class="n">se</span>
    <span class="n">p</span> <span class="o">=</span> <span class="mi">1</span><span class="o">-</span><span class="n">stats</span><span class="o">.</span><span class="n">norm</span><span class="o">.</span><span class="n">cdf</span><span class="p">(</span><span class="nb">abs</span><span class="p">(</span><span class="n">z</span><span class="p">))</span>
    <span class="n">p</span> <span class="o">*=</span> <span class="mi">2</span><span class="o">-</span><span class="n">one_sided</span>
    <span class="k">return</span> <span class="n">z</span><span class="p">,</span> <span class="n">p</span>
    
</pre>
        </div>

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
          <pre><span></span><span class="c1"># 95% confidence interval</span>
<span class="n">prop_diff</span> <span class="o">=</span> <span class="n">w_p</span> <span class="o">-</span> <span class="n">b_p</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Observed difference in proportions: </span><span class="se">\t</span><span class="s1"> </span><span class="si">{}</span><span class="se">\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">prop_diff</span><span class="p">))</span>

<span class="n">z_crit</span> <span class="o">=</span> <span class="mf">1.96</span>
<span class="n">p_hat1</span> <span class="o">=</span> <span class="n">w_p</span><span class="o">*</span><span class="p">(</span><span class="mi">1</span><span class="o">-</span><span class="n">w_p</span><span class="p">)</span><span class="o">/</span><span class="n">w_n</span>
<span class="n">p_hat2</span> <span class="o">=</span>  <span class="n">b_p</span><span class="o">*</span><span class="p">(</span><span class="mi">1</span><span class="o">-</span><span class="n">b_p</span><span class="p">)</span><span class="o">/</span><span class="n">b_n</span>
<span class="n">ci_high</span> <span class="o">=</span> <span class="n">prop_diff</span> <span class="o">+</span> <span class="n">z_crit</span><span class="o">*</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">p_hat1</span> <span class="o">+</span> <span class="n">p_hat2</span><span class="p">))</span>
<span class="n">ci_low</span> <span class="o">=</span> <span class="n">prop_diff</span> <span class="o">-</span> <span class="n">z_crit</span><span class="o">*</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">p_hat1</span> <span class="o">+</span> <span class="n">p_hat2</span><span class="p">))</span>

<span class="n">z_stat</span><span class="p">,</span> <span class="n">p_val</span> <span class="o">=</span> <span class="n">ztest_proportions_two_samples</span><span class="p">(</span><span class="n">w_r</span><span class="p">,</span> <span class="n">w_n</span><span class="p">,</span> <span class="n">b_r</span><span class="p">,</span> <span class="n">b_n</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;z-stat: </span><span class="se">\t</span><span class="s1"> </span><span class="si">{}</span><span class="se">\n</span><span class="s1">p-value: </span><span class="se">\t</span><span class="s1"> </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">z_stat</span><span class="p">,</span> <span class="n">p_val</span><span class="p">))</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;95</span><span class="si">% c</span><span class="s1">onf int: </span><span class="se">\t</span><span class="s1"> </span><span class="si">{}</span><span class="s1"> - </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">ci_low</span><span class="p">,</span> <span class="n">ci_high</span><span class="p">))</span>
<span class="n">moe</span> <span class="o">=</span> <span class="p">(</span><span class="n">ci_high</span> <span class="o">-</span> <span class="n">ci_low</span><span class="p">)</span><span class="o">/</span><span class="mi">2</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Margin of err: </span><span class="se">\t</span><span class="s1"> +/-</span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">moe</span><span class="p">))</span>
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
          <pre>Observed difference in proportions: 	 0.032032854209445585

z-stat: 	 4.108412152434346
p-value: 	 3.983886837577444e-05
95% conf int: 	 0.016777447859559147 - 0.047288260559332024
Margin of err: 	 +/-0.015255406349886438
</pre>
        </div>
      </div>

    </div>
  </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
  <div class="input">
    <div class="prompt input_prompt">In&nbsp;[14]:</div>
    <div class="inner_cell">
      <div class="input_area">
        <div class=" highlight hl-ipython3">
          <pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">style</span><span class="o">.</span><span class="n">use</span><span class="p">(</span><span class="s1">&#39;fivethirtyeight&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s2">&quot;figure.figsize&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">8</span><span class="p">)</span>

<span class="c1"># Graph the Frequentist results</span>
<span class="n">x</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="o">-</span> <span class="mf">0.06</span><span class="p">,</span> <span class="mf">0.06</span><span class="p">,</span> <span class="mi">100</span><span class="p">,</span> <span class="n">endpoint</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">pdf</span> <span class="o">=</span> <span class="p">[</span><span class="n">stats</span><span class="o">.</span><span class="n">norm</span><span class="o">.</span><span class="n">pdf</span><span class="p">(</span><span class="n">_</span><span class="p">,</span> <span class="n">loc</span><span class="o">=</span><span class="mi">0</span><span class="p">,</span> <span class="n">scale</span><span class="o">=</span><span class="n">moe</span><span class="p">)</span> <span class="k">for</span> <span class="n">_</span> <span class="ow">in</span> <span class="n">x</span><span class="p">]</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">pdf</span><span class="p">,</span> <span class="s1">&#39;k-&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">8</span><span class="p">)</span>

<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">axvline</span><span class="p">(</span><span class="n">ci_high</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;red&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">axvline</span><span class="p">(</span><span class="n">ci_low</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;red&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">axvline</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;blue&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="o">-</span><span class="mf">0.023</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="s1">&#39;$H_0: p_w - p_b = 0$&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="mf">0.022</span><span class="p">,</span> <span class="mi">23</span><span class="p">,</span> <span class="s1">&#39;95% Confidence </span><span class="se">\n</span><span class="s1">     Interval&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Fig 3.1: Frequentist Approach&#39;</span><span class="p">);</span>
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
          <img src="data:image/png;base64,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
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
      <h4 id="Bootstrap">Bootstrap
        <a class="anchor-link" href="#Bootstrap">&#182;</a>
      </h4>
    </div>
  </div>
</div>
<div class="cell border-box-sizing code_cell rendered">
  <div class="input">
    <div class="prompt input_prompt">In&nbsp;[16]:</div>
    <div class="inner_cell">
      <div class="input_area">
        <div class=" highlight hl-ipython3">
          <pre><span></span><span class="c1"># Construct arrays of data: white-sounding names, black-sounding names</span>
<span class="n">all_callbacks</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="kc">True</span><span class="p">]</span> <span class="o">*</span> <span class="nb">int</span><span class="p">(</span><span class="n">r</span><span class="p">)</span> <span class="o">+</span> <span class="p">[</span><span class="kc">False</span><span class="p">]</span> <span class="o">*</span> <span class="nb">int</span><span class="p">(</span><span class="n">n</span><span class="o">-</span><span class="n">r</span><span class="p">))</span>

<span class="n">size</span> <span class="o">=</span> <span class="mi">10000</span>

<span class="n">bs_reps_diff</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">empty</span><span class="p">(</span><span class="n">size</span><span class="p">)</span>

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">size</span><span class="p">):</span>
    <span class="n">w_bs_replicates</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">choice</span><span class="p">(</span><span class="n">all_callbacks</span><span class="p">,</span> <span class="n">size</span><span class="o">=</span><span class="n">w_n</span><span class="p">))</span>
    <span class="n">b_bs_replicates</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">choice</span><span class="p">(</span><span class="n">all_callbacks</span><span class="p">,</span> <span class="n">size</span><span class="o">=</span><span class="n">b_n</span><span class="p">))</span>
    
    <span class="n">bs_reps_diff</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">w_bs_replicates</span> <span class="o">-</span> <span class="n">b_bs_replicates</span><span class="p">)</span><span class="o">/</span><span class="n">b_n</span>
    
<span class="n">bs_p_value</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">(</span><span class="n">bs_reps_diff</span> <span class="o">&gt;=</span> <span class="n">prop_diff</span><span class="p">)</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">bs_reps_diff</span><span class="p">)</span>

<span class="n">bs_ci</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">percentile</span><span class="p">(</span><span class="n">bs_reps_diff</span><span class="p">,</span> <span class="p">[</span><span class="mf">2.5</span><span class="p">,</span> <span class="mf">97.5</span><span class="p">])</span>
<span class="n">bs_mean_diff</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">bs_reps_diff</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;obs diff: </span><span class="si">{}</span><span class="se">\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">prop_diff</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;BOOTSTRAP RESULTS</span><span class="se">\n</span><span class="s1">p-value: </span><span class="si">{}</span><span class="se">\n</span><span class="s1">95</span><span class="si">% c</span><span class="s1">onf. int.: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">bs_p_value</span><span class="p">,</span> <span class="n">bs_ci</span><span class="p">))</span>
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
          <pre>obs diff: 0.032032854209445585

BOOTSTRAP RESULTS
p-value: 0.0
95% conf. int.: [-0.01519507  0.01519507]
</pre>
        </div>
      </div>

    </div>
  </div>

</div>
<div class="cell border-box-sizing code_cell rendered">
  <div class="input">
    <div class="prompt input_prompt">In&nbsp;[15]:</div>
    <div class="inner_cell">
      <div class="input_area">
        <div class=" highlight hl-ipython3">
          <pre><span></span><span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">bs_reps_diff</span><span class="p">,</span> <span class="n">bins</span><span class="o">=</span><span class="mi">20</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">axvline</span><span class="p">(</span><span class="n">prop_diff</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;red&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">axvline</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">bs_reps_diff</span><span class="p">),</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;blue&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;% Diff&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Frequency&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Fig 3.2: Empirical v Bootstrap Proportional Differences&#39;</span><span class="p">)</span>
<span class="n">_</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="o">-</span><span class="mf">0.0275</span><span class="p">,</span> <span class="mi">1300</span><span class="p">,</span> <span class="s1">&#39;Observed Diff: +</span><span class="si">{:0.5}</span><span class="s1">% WSNs</span><span class="se">\n\n</span><span class="s1">Highest BS Diff: +</span><span class="si">{:0.5}</span><span class="s1">% WSNs&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">prop_diff</span><span class="o">*</span><span class="mi">100</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">bs_reps_diff</span><span class="p">)</span><span class="o">*</span><span class="mi">100</span><span class="p">))</span>
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
          <img src="data:image/png;base64,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WV4XFBTowoULVn/QPP7445o1a1aR98bFxWnZsmX6/PPPVbVq1WLrCA0N1VtvvaXx48frueee0+23365x48Zp586dNs1KBgUFWX1dhISE6M8//9S7775rCb3btm3T9OnTNXPmTPn5+enSpUuKjo7W22+/rZdfflmS1Lt3b/Xu3dtynJ07d2r37t2aNGmS7rvvPsXFxalp06bq0KGD2rZtqxYtWlyzPZ06ddLYsWN1/vx5JSYmWtrQsWNHRUVFSbo82962bVtVrFhR0uV17vPnz9crr7yi77//Xj/++KPeffddzZw5U+vXry8SbDt27KiwsDC9+eab+vjjj632Va9eXU888YT69eunLl26qHPnznr00UdVt27dmz6nAADHYHmDgVSuXFkNGza0+nejtZhms/mmgtzVF75dec+VmeTCwkJFRUUpMTHR8m/79u36+eef5evrKzc3N3322WeKj49XixYt9OGHH+qee+7Rvn37bO6nyWSy9O/OO+/UyJEj1aFDhyIh0MvLSw899JBeffVVffTRR+rUqZMmT55sc32SdPDgQZlMJssstSPVqlXL6jzOnTu3yLar73AgXQ68kydP1po1a9SmTZsb1jNy5EgdPXpUv/zyi/773//qoYcekiTVq1evVO1v06aN5SI+SZo8ebL69eunwYMHq3Hjxurdu7deffVVzZ0795rLT/Lz8zVmzBjNnj1bR44cUX5+vrp27aqaNWuqY8eORS5K+6vOnTtbljVs27ZNHTt2lCS1bdtWR44cUWpqqrZv325Z2vBXtWvX1sCBAzVjxgzt2rVLFSpUsCxRudobb7yhb775Rjt27Ciyb/78+dq4caPat2+vr776Svfee682bdp0w/MGAHAsZnpvccHBwVq/fr3VtisXGNni7rvv1m+//aaGDRsWW8ZkMikkJEQhISGKiopSu3bt9Nlnn6lly5aqWLGiCgoKbK73Cjc3N507d+66dQcFBV33lmXFycnJ0fvvv68OHTqUaGbaVu7u7lbn8cSJE3Jzc7vuuZ03b55iYmK0Zs2am7r12xUmk8myLGTt2rWqW7eu7r777pI3XtK+ffuslnScO3euyOyxm5ubZfb8ajNmzFCnTp103333KTk52SoY5+fnX/frpF69egoMDNS3336rn376SbGxsZIuL59p1aqVlixZovT0dMtFbMXx9vaWv7+/cnNzr7m/efPmGjhwoF5//XXLjPFftWzZUi1bttSoUaPUv39/rVq1SmFhYdetEwDgWITeW1xERIRiY2P1yiuvaMiQITpw4IDef/99SbZ9lD9+/HgNGDBAAQEB6tu3r9zd3XXgwAH99NNPmjhxonbv3q2tW7cqLCxMfn5+Sk5O1okTJxQcHCxJCgwM1LFjx7R3714FBASoSpUquv32269Zl9lstqw7zcvL09atW7Vp0yaNHz9ekpScnKyYmBgNHDhQwcHBqlixor744gutXLlS/fr1u24//nrsM2fOWJZsnDlzRqtWrbrp81Gcn376Sc8++6zee++9m5qNvRlz587VW2+9pYULF6px48aW9leqVMmyrnjhwoVatGiR1dKKuXPnKiwsTBUqVFBCQoJmz56t999/3yqgHjx4UPn5+crMzFRubq6Sk5MlSXfddZeky7OagYGBatasmfLz87VmzRp9+eWXWr58ueUYPXr00Pz589W6dWv5+Pjo+PHjmjx5srp3717kE4SDBw/qk08+sVxUFhQUJHd3dy1dulRNmzbV999/bxnn4nTq1Envv/++fH19LetqJalDhw5asGCBvLy81KpVK8v2999/X/v27dPDDz+sBg0a6Pz58/r444+1f/9+vfDCC8XWM2HCBMtSoCvr048cOaJly5apZ8+eqlWrlo4cOaJff/31uuuQAQDOQei9xQUGBmr58uV6+eWXtWjRIt1zzz2KiorSyJEji1zdfz1hYWFas2aNpk+frnnz5snd3V2NGjXSE088IUmqWrWqdu3apYULFyo7O1t16tTRuHHjLA/UeOSRR5SQkKA+ffooOztbsbGxevLJJ69Z17lz5yxh+fbbb1dAQIAmTJigUaNGSZLq1Kmj+vXra+rUqTp27JgKCwtVo0YNjRw50uq2Y9c7tslkkpeXl+rXr68ePXpo+PDh8vPzu+nzcb3jp6SkXHdW2laLFi3SxYsXFRERYbV90KBBiouLk3T5XrgpKSlW+7/99lvNmDFD+fn5uvPOO/XRRx9Z7qhwxWOPPWa5/7EkywzplfsdX7x4Ua+++qpSU1NVqVIlNWvWTGvWrLG6r++4ceNkMpk0efJknThxQr6+vurRo4deffVVq7rMZrNGjRqlt99+W15eXpIu31FiwYIFGjt2rM6cOaMXX3xRrVu3vu756NSpk1auXFnkQr6OHTtq9uzZ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
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
      <h4 id="Analysis:">Analysis:
        <a class="anchor-link" href="#Analysis:">&#182;</a>
      </h4>
      <p>The p-value for the Frequentist and Boostrap approaches are both well below the p=0.05 threshold so the null hypothesis
        must be rejected in favor of the alternate hypothesis that perception of race based on the name on the resume does
        have an effect on whether an applicant will receive a callback.</p>
      <p>The null hypothesis states the $p_w - p_b = 0%$, but Figure 3.1 shows that the lower cut-off of the 95% confidence
        interval is 1.68%, well above 0%. Figure 3.2 shows that after 10,000 bootstrap samples, the greatest difference between
        success rates is 2.96%, well below the observed difference of 3.2%.</p>
      <p>It can be concluded that for samples taken in a similar fashion from the same population, at least 95% of the time,
        the difference in proportions will not be as great as the empirical results seen here.</p>

    </div>
  </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
  <div class="prompt input_prompt">
  </div>
  <div class="inner_cell">
    <div class="text_cell_render border-box-sizing rendered_html">
      <h3 id="Question-#4:-Write-a-story-describing-the-statistical-significance-in-the-context-of-the-original-problem.">Q4: Statistical Significance
        <a class="anchor-link" href="#Q4:-Statistical-Significance">&#182;</a>
      </h3>
      <p>Write a story describing the statistical significance in the context of the original problem.</p>
      <hr>
      <p>It has been proven conclusively that the proportion of callbacks received for resumes with white-sounding names is
        significantly and consistently higher than the proportion of callbacks for resumes with black-sounding names. The
        evidence for the samples provided show that resumes with white-sounding names are approximately 50% more likely to
        receive a callback.</p>

    </div>
  </div>
</div>
<div class="cell border-box-sizing text_cell rendered">
  <div class="prompt input_prompt">
  </div>
  <div class="inner_cell">
    <div class="text_cell_render border-box-sizing rendered_html">
      <h3 id="Q5:-Is-race/name-is-the-most-important-factor-in-callback-success?">Q5: Analysis
        <a class="anchor-link" href="#Q5:-Is-race/name-is-the-most-important-factor-in-callback-success?">&#182;</a>
      </h3>
      <p> Does your analysis mean that race/name is the most important factor in callback success? Why or why not?
        If not, how would you amend your analysis?</p>
      <hr>
      <p>According to the study's website:</p>
      <blockquote>
        <p>Researchers examined the level of racial discrimination in the United States labor market by randomly assigning identical
          résumés black-sounding or white-sounding names and observing the impact on requests for interviews from employers.</p>
        <p>According to this description, the researchers took great care to make sure that the resumes were identical aside
          from the names. So, examining the resumes more closely for differences in education, work experience, etc. should
          not be helpful if the study was executed properly. The methods of the study could be examined more closely for
          sample bias in the cities and the hiring managers selected, etc.</p>
      </blockquote>

    </div>
  </div>
</div>