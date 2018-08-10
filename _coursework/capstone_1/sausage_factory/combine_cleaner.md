---
title: Combine Cleaner Notebook
layout: code
permalink: /coursework/projects/nfl_defensive_back/combine_cleaner_notebook
excerpt: ""
section: "/coursework/projects/nfl_defensive_back/#combine_cleaner.ipynb"
---
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">os</span>

<span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s1">&#39;display.max_columns&#39;</span><span class="p">,</span> <span class="mi">500</span><span class="p">)</span>
<span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s1">&#39;display.max_rows&#39;</span><span class="p">,</span> <span class="mi">250</span><span class="p">)</span>

<span class="n">pd</span><span class="o">.</span><span class="n">options</span><span class="o">.</span><span class="n">display</span><span class="o">.</span><span class="n">float_format</span> <span class="o">=</span> <span class="s1">&#39;</span><span class="si">{:.0f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stderr output_text">
<pre>/anaconda3/lib/python3.6/importlib/_bootstrap.py:219: RuntimeWarning: numpy.dtype size changed, may indicate binary incompatibility. Expected 96, got 88
  return f(*args, **kwds)
/anaconda3/lib/python3.6/importlib/_bootstrap.py:219: RuntimeWarning: numpy.dtype size changed, may indicate binary incompatibility. Expected 96, got 88
  return f(*args, **kwds)
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">ncaa</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;~/Documents/Data Science/Data Projects/Capstone 1/data/CLEAN/ncaa_bios+stats_FINAL.csv&#39;</span><span class="p">,</span> <span class="n">index_col</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
<span class="n">ncaa</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
<span class="n">ncaa</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>&lt;class &#39;pandas.core.frame.DataFrame&#39;&gt;
Int64Index: 7532 entries, 0 to 7531
Data columns (total 14 columns):
player_id       7532 non-null int64
player          7532 non-null object
team            7532 non-null object
class           7528 non-null object
position        7532 non-null object
height          7532 non-null float64
weight          7532 non-null float64
home_town       7488 non-null object
home_state      7483 non-null object
home_country    7489 non-null object
last_school     7236 non-null object
first           7532 non-null object
last            7532 non-null object
stats_name      7532 non-null object
dtypes: float64(2), int64(1), object(11)
memory usage: 882.7+ KB
</pre>
</div>
</div>

<div class="output_area">

<div class="prompt output_prompt">Out[2]:</div>



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
      <th>player_id</th>
      <th>player</th>
      <th>team</th>
      <th>class</th>
      <th>position</th>
      <th>height</th>
      <th>weight</th>
      <th>home_town</th>
      <th>home_state</th>
      <th>home_country</th>
      <th>last_school</th>
      <th>first</th>
      <th>last</th>
      <th>stats_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1007910</td>
      <td>Junaid Abdullah</td>
      <td>Akron</td>
      <td>SR</td>
      <td>DB</td>
      <td>70</td>
      <td>210</td>
      <td>Akron</td>
      <td>OH</td>
      <td>US</td>
      <td>Kiski (Pa.) Prep</td>
      <td>Junaid</td>
      <td>Abdullah</td>
      <td>Junaid Abdullah</td>
    </tr>
    <tr>
      <th>1</th>
      <td>56609</td>
      <td>Reggie Corner</td>
      <td>Akron</td>
      <td>SR</td>
      <td>DB</td>
      <td>69</td>
      <td>175</td>
      <td>Canton</td>
      <td>OH</td>
      <td>US</td>
      <td>McKinley HS</td>
      <td>Reggie</td>
      <td>Corner</td>
      <td>Reggie Corner</td>
    </tr>
    <tr>
      <th>2</th>
      <td>56032</td>
      <td>Yamari Dixon</td>
      <td>Akron</td>
      <td>SR</td>
      <td>DB</td>
      <td>69</td>
      <td>200</td>
      <td>Miami</td>
      <td>FL</td>
      <td>US</td>
      <td>Booker T. Washington HS</td>
      <td>Yamari</td>
      <td>Dixon</td>
      <td>Yamari Dixon</td>
    </tr>
    <tr>
      <th>3</th>
      <td>85465</td>
      <td>Rodney Etienne</td>
      <td>Akron</td>
      <td>SO</td>
      <td>DB</td>
      <td>74</td>
      <td>195</td>
      <td>Pompano Beach</td>
      <td>FL</td>
      <td>US</td>
      <td>Blanche Ely HS</td>
      <td>Rodney</td>
      <td>Etienne</td>
      <td>Rodney Etienne</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1007908</td>
      <td>Mateo Jimenez</td>
      <td>Akron</td>
      <td>FR</td>
      <td>DB</td>
      <td>69</td>
      <td>165</td>
      <td>Pembroke Pines</td>
      <td>FL</td>
      <td>US</td>
      <td>Flanagan HS</td>
      <td>Mateo</td>
      <td>Jimenez</td>
      <td>Mateo Jimenez</td>
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
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">combine</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;~/Documents/Data Science/Data Projects/Capstone 1/data/combine/Combine.csv&#39;</span><span class="p">)</span>
<span class="n">combine</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
<span class="n">combine</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>&lt;class &#39;pandas.core.frame.DataFrame&#39;&gt;
RangeIndex: 632 entries, 0 to 631
Data columns (total 16 columns):
Rk                     632 non-null int64
Year                   632 non-null int64
Player                 632 non-null object
Pos                    632 non-null object
AV                     490 non-null float64
School                 632 non-null object
College                560 non-null object
Height                 632 non-null object
Wt                     632 non-null int64
40YD                   630 non-null float64
Vertical               527 non-null float64
BenchReps              518 non-null float64
Broad Jump             519 non-null float64
3Cone                  408 non-null float64
Shuttle                421 non-null float64
Drafted (tm/rnd/yr)    436 non-null object
dtypes: float64(7), int64(3), object(6)
memory usage: 79.1+ KB
</pre>
</div>
</div>

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
      <th>Rk</th>
      <th>Year</th>
      <th>Player</th>
      <th>Pos</th>
      <th>AV</th>
      <th>School</th>
      <th>College</th>
      <th>Height</th>
      <th>Wt</th>
      <th>40YD</th>
      <th>Vertical</th>
      <th>BenchReps</th>
      <th>Broad Jump</th>
      <th>3Cone</th>
      <th>Shuttle</th>
      <th>Drafted (tm/rnd/yr)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2014</td>
      <td>Lavelle Westbrooks\WestLa00</td>
      <td>CB</td>
      <td>nan</td>
      <td>Georgia Southern</td>
      <td>NaN</td>
      <td>5-11</td>
      <td>186</td>
      <td>5</td>
      <td>36</td>
      <td>15</td>
      <td>121</td>
      <td>7</td>
      <td>4</td>
      <td>Cincinnati Bengals / 7th / 252nd pick / 2014</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2014</td>
      <td>Jaylen Watkins\WatkJa01</td>
      <td>CB</td>
      <td>3</td>
      <td>Florida</td>
      <td>College Stats</td>
      <td>5-11</td>
      <td>194</td>
      <td>4</td>
      <td>nan</td>
      <td>22</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
      <td>Philadelphia Eagles / 4th / 101st pick / 2014</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2014</td>
      <td>Jimmie Ward\WardJi01</td>
      <td>SS</td>
      <td>9</td>
      <td>Northern Illinois</td>
      <td>College Stats</td>
      <td>5-11</td>
      <td>193</td>
      <td>5</td>
      <td>nan</td>
      <td>9</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
      <td>San Francisco 49ers / 1st / 30th pick / 2014</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2014</td>
      <td>Jason Verrett\VerrJa00</td>
      <td>CB</td>
      <td>12</td>
      <td>TCU</td>
      <td>College Stats</td>
      <td>5-9</td>
      <td>189</td>
      <td>4</td>
      <td>39</td>
      <td>nan</td>
      <td>128</td>
      <td>7</td>
      <td>4</td>
      <td>San Diego Chargers / 1st / 25th pick / 2014</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2014</td>
      <td>Brock Vereen\VereBr00</td>
      <td>SS</td>
      <td>2</td>
      <td>Minnesota</td>
      <td>College Stats</td>
      <td>6-0</td>
      <td>199</td>
      <td>4</td>
      <td>34</td>
      <td>25</td>
      <td>117</td>
      <td>7</td>
      <td>4</td>
      <td>Chicago Bears / 4th / 131st pick / 2014</td>
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
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">combine</span> <span class="o">=</span> <span class="n">combine</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s1">&#39;Rk&#39;</span><span class="p">,</span> <span class="s1">&#39;AV&#39;</span><span class="p">,</span> <span class="s1">&#39;College&#39;</span><span class="p">],</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">)</span>

<span class="c1"># Break out info into new columns</span>
<span class="n">combine</span><span class="p">[</span><span class="s1">&#39;name&#39;</span><span class="p">],</span> <span class="n">_</span> <span class="o">=</span> <span class="n">combine</span><span class="o">.</span><span class="n">Player</span><span class="o">.</span><span class="n">str</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">&#39;</span><span class="se">\\</span><span class="s1">&#39;</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">str</span>
<span class="n">combine</span><span class="p">[</span><span class="s1">&#39;draft_team&#39;</span><span class="p">],</span> <span class="n">combine</span><span class="p">[</span><span class="s1">&#39;draft_round&#39;</span><span class="p">],</span> <span class="n">combine</span><span class="p">[</span><span class="s1">&#39;draft_pick&#39;</span><span class="p">],</span> <span class="n">combine</span><span class="p">[</span><span class="s1">&#39;draft_year&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">combine</span><span class="p">[</span><span class="s1">&#39;Drafted (tm/rnd/yr)&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">str</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">&#39;\/&#39;</span><span class="p">,</span> <span class="mi">4</span><span class="p">)</span><span class="o">.</span><span class="n">str</span>

<span class="c1"># Drop superfluous columns</span>
<span class="n">combine</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s1">&#39;Drafted (tm/rnd/yr)&#39;</span><span class="p">,</span> <span class="s1">&#39;Year&#39;</span><span class="p">,</span> <span class="s1">&#39;Player&#39;</span><span class="p">],</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="c1"># Reorder columns</span>
<span class="n">cols</span> <span class="o">=</span> <span class="n">combine</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()</span>
<span class="n">cols</span> <span class="o">=</span> <span class="n">cols</span><span class="p">[</span><span class="o">-</span><span class="mi">5</span><span class="p">:]</span> <span class="o">+</span> <span class="n">cols</span><span class="p">[:</span><span class="o">-</span><span class="mi">5</span><span class="p">]</span>
<span class="n">combine</span> <span class="o">=</span> <span class="n">combine</span><span class="p">[</span><span class="n">cols</span><span class="p">]</span>
<span class="n">combine</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[6]:</div>



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
      <th>name</th>
      <th>draft_team</th>
      <th>draft_round</th>
      <th>draft_pick</th>
      <th>draft_year</th>
      <th>Pos</th>
      <th>School</th>
      <th>Height</th>
      <th>Wt</th>
      <th>40YD</th>
      <th>Vertical</th>
      <th>BenchReps</th>
      <th>Broad Jump</th>
      <th>3Cone</th>
      <th>Shuttle</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lavelle Westbrooks</td>
      <td>Cincinnati Bengals</td>
      <td>7th</td>
      <td>252nd pick</td>
      <td>2014</td>
      <td>CB</td>
      <td>Georgia Southern</td>
      <td>5-11</td>
      <td>186</td>
      <td>5</td>
      <td>36</td>
      <td>15</td>
      <td>121</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jaylen Watkins</td>
      <td>Philadelphia Eagles</td>
      <td>4th</td>
      <td>101st pick</td>
      <td>2014</td>
      <td>CB</td>
      <td>Florida</td>
      <td>5-11</td>
      <td>194</td>
      <td>4</td>
      <td>nan</td>
      <td>22</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jimmie Ward</td>
      <td>San Francisco 49ers</td>
      <td>1st</td>
      <td>30th pick</td>
      <td>2014</td>
      <td>SS</td>
      <td>Northern Illinois</td>
      <td>5-11</td>
      <td>193</td>
      <td>5</td>
      <td>nan</td>
      <td>9</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jason Verrett</td>
      <td>San Diego Chargers</td>
      <td>1st</td>
      <td>25th pick</td>
      <td>2014</td>
      <td>CB</td>
      <td>TCU</td>
      <td>5-9</td>
      <td>189</td>
      <td>4</td>
      <td>39</td>
      <td>nan</td>
      <td>128</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Brock Vereen</td>
      <td>Chicago Bears</td>
      <td>4th</td>
      <td>131st pick</td>
      <td>2014</td>
      <td>SS</td>
      <td>Minnesota</td>
      <td>6-0</td>
      <td>199</td>
      <td>4</td>
      <td>34</td>
      <td>25</td>
      <td>117</td>
      <td>7</td>
      <td>4</td>
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
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">cols</span> <span class="o">=</span> <span class="n">combine</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()</span>

<span class="n">cols</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;player&#39;</span><span class="p">,</span> <span class="s1">&#39;draft_team&#39;</span><span class="p">,</span> <span class="s1">&#39;draft_round&#39;</span><span class="p">,</span> <span class="s1">&#39;draft_pick&#39;</span><span class="p">,</span> <span class="s1">&#39;draft_year&#39;</span><span class="p">,</span> <span class="s1">&#39;draft_position&#39;</span><span class="p">,</span> <span class="s1">&#39;college&#39;</span><span class="p">,</span> <span class="s1">&#39;draft_height&#39;</span><span class="p">,</span> 
        <span class="s1">&#39;draft_weight&#39;</span><span class="p">,</span> <span class="s1">&#39;forty&#39;</span><span class="p">,</span> <span class="s1">&#39;vertical&#39;</span><span class="p">,</span> <span class="s1">&#39;bench_reps&#39;</span><span class="p">,</span> <span class="s1">&#39;broad_jump&#39;</span><span class="p">,</span> <span class="s1">&#39;three_cone&#39;</span><span class="p">,</span> <span class="s1">&#39;shuttle&#39;</span><span class="p">]</span>
<span class="n">combine</span><span class="o">.</span><span class="n">columns</span> <span class="o">=</span> <span class="n">cols</span>
<span class="n">combine</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[7]:</div>



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
      <th>player</th>
      <th>draft_team</th>
      <th>draft_round</th>
      <th>draft_pick</th>
      <th>draft_year</th>
      <th>draft_position</th>
      <th>college</th>
      <th>draft_height</th>
      <th>draft_weight</th>
      <th>forty</th>
      <th>vertical</th>
      <th>bench_reps</th>
      <th>broad_jump</th>
      <th>three_cone</th>
      <th>shuttle</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lavelle Westbrooks</td>
      <td>Cincinnati Bengals</td>
      <td>7th</td>
      <td>252nd pick</td>
      <td>2014</td>
      <td>CB</td>
      <td>Georgia Southern</td>
      <td>5-11</td>
      <td>186</td>
      <td>5</td>
      <td>36</td>
      <td>15</td>
      <td>121</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jaylen Watkins</td>
      <td>Philadelphia Eagles</td>
      <td>4th</td>
      <td>101st pick</td>
      <td>2014</td>
      <td>CB</td>
      <td>Florida</td>
      <td>5-11</td>
      <td>194</td>
      <td>4</td>
      <td>nan</td>
      <td>22</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jimmie Ward</td>
      <td>San Francisco 49ers</td>
      <td>1st</td>
      <td>30th pick</td>
      <td>2014</td>
      <td>SS</td>
      <td>Northern Illinois</td>
      <td>5-11</td>
      <td>193</td>
      <td>5</td>
      <td>nan</td>
      <td>9</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jason Verrett</td>
      <td>San Diego Chargers</td>
      <td>1st</td>
      <td>25th pick</td>
      <td>2014</td>
      <td>CB</td>
      <td>TCU</td>
      <td>5-9</td>
      <td>189</td>
      <td>4</td>
      <td>39</td>
      <td>nan</td>
      <td>128</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Brock Vereen</td>
      <td>Chicago Bears</td>
      <td>4th</td>
      <td>131st pick</td>
      <td>2014</td>
      <td>SS</td>
      <td>Minnesota</td>
      <td>6-0</td>
      <td>199</td>
      <td>4</td>
      <td>34</td>
      <td>25</td>
      <td>117</td>
      <td>7</td>
      <td>4</td>
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
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">combine</span><span class="o">.</span><span class="n">draft_round</span> <span class="o">=</span> <span class="n">combine</span><span class="o">.</span><span class="n">draft_round</span><span class="o">.</span><span class="n">str</span><span class="o">.</span><span class="n">extract</span><span class="p">(</span><span class="s1">&#39;(\d+)&#39;</span><span class="p">)</span>
<span class="n">combine</span><span class="o">.</span><span class="n">draft_pick</span> <span class="o">=</span> <span class="n">combine</span><span class="o">.</span><span class="n">draft_pick</span><span class="o">.</span><span class="n">str</span><span class="o">.</span><span class="n">extract</span><span class="p">(</span><span class="s1">&#39;(\d+)&#39;</span><span class="p">)</span>
<span class="n">combine</span><span class="o">.</span><span class="n">draft_height</span> <span class="o">=</span> <span class="n">combine</span><span class="o">.</span><span class="n">draft_height</span><span class="o">.</span><span class="n">str</span><span class="p">[:</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span> <span class="o">*</span> <span class="mi">12</span> <span class="o">+</span> <span class="n">combine</span><span class="o">.</span><span class="n">draft_height</span><span class="o">.</span><span class="n">str</span><span class="p">[</span><span class="mi">2</span><span class="p">:]</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
<span class="n">combine</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">30</span><span class="p">)</span>
<span class="n">combine</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[8]:</div>



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
      <th>player</th>
      <th>draft_team</th>
      <th>draft_round</th>
      <th>draft_pick</th>
      <th>draft_year</th>
      <th>draft_position</th>
      <th>college</th>
      <th>draft_height</th>
      <th>draft_weight</th>
      <th>forty</th>
      <th>vertical</th>
      <th>bench_reps</th>
      <th>broad_jump</th>
      <th>three_cone</th>
      <th>shuttle</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lavelle Westbrooks</td>
      <td>Cincinnati Bengals</td>
      <td>7</td>
      <td>252</td>
      <td>2014</td>
      <td>CB</td>
      <td>Georgia Southern</td>
      <td>71</td>
      <td>186</td>
      <td>5</td>
      <td>36</td>
      <td>15</td>
      <td>121</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jaylen Watkins</td>
      <td>Philadelphia Eagles</td>
      <td>4</td>
      <td>101</td>
      <td>2014</td>
      <td>CB</td>
      <td>Florida</td>
      <td>71</td>
      <td>194</td>
      <td>4</td>
      <td>nan</td>
      <td>22</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jimmie Ward</td>
      <td>San Francisco 49ers</td>
      <td>1</td>
      <td>30</td>
      <td>2014</td>
      <td>SS</td>
      <td>Northern Illinois</td>
      <td>71</td>
      <td>193</td>
      <td>5</td>
      <td>nan</td>
      <td>9</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jason Verrett</td>
      <td>San Diego Chargers</td>
      <td>1</td>
      <td>25</td>
      <td>2014</td>
      <td>CB</td>
      <td>TCU</td>
      <td>69</td>
      <td>189</td>
      <td>4</td>
      <td>39</td>
      <td>nan</td>
      <td>128</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Brock Vereen</td>
      <td>Chicago Bears</td>
      <td>4</td>
      <td>131</td>
      <td>2014</td>
      <td>SS</td>
      <td>Minnesota</td>
      <td>72</td>
      <td>199</td>
      <td>4</td>
      <td>34</td>
      <td>25</td>
      <td>117</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Jemea Thomas</td>
      <td>New England Patriots</td>
      <td>6</td>
      <td>206</td>
      <td>2014</td>
      <td>CB</td>
      <td>Georgia Tech</td>
      <td>69</td>
      <td>192</td>
      <td>5</td>
      <td>37</td>
      <td>19</td>
      <td>125</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Vinnie Sunseri</td>
      <td>New Orleans Saints</td>
      <td>5</td>
      <td>167</td>
      <td>2014</td>
      <td>SS</td>
      <td>Alabama</td>
      <td>71</td>
      <td>210</td>
      <td>nan</td>
      <td>nan</td>
      <td>18</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Dezmen Southward</td>
      <td>Atlanta Falcons</td>
      <td>3</td>
      <td>68</td>
      <td>2014</td>
      <td>SS</td>
      <td>Wisconsin</td>
      <td>72</td>
      <td>211</td>
      <td>4</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Daniel Sorensen</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SS</td>
      <td>BYU</td>
      <td>73</td>
      <td>205</td>
      <td>5</td>
      <td>32</td>
      <td>13</td>
      <td>114</td>
      <td>6</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Bradley Roby</td>
      <td>Denver Broncos</td>
      <td>1</td>
      <td>31</td>
      <td>2014</td>
      <td>CB</td>
      <td>Ohio State</td>
      <td>71</td>
      <td>194</td>
      <td>4</td>
      <td>38</td>
      <td>17</td>
      <td>124</td>
      <td>nan</td>
      <td>4</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Marcus Roberson</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CB</td>
      <td>Florida</td>
      <td>72</td>
      <td>191</td>
      <td>5</td>
      <td>38</td>
      <td>8</td>
      <td>120</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Rashaad Reynolds</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CB</td>
      <td>Oregon State</td>
      <td>70</td>
      <td>189</td>
      <td>5</td>
      <td>38</td>
      <td>20</td>
      <td>123</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Ed Reynolds</td>
      <td>Philadelphia Eagles</td>
      <td>5</td>
      <td>162</td>
      <td>2014</td>
      <td>FS</td>
      <td>Stanford</td>
      <td>73</td>
      <td>207</td>
      <td>5</td>
      <td>32</td>
      <td>15</td>
      <td>117</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Keith Reaser</td>
      <td>San Francisco 49ers</td>
      <td>5</td>
      <td>170</td>
      <td>2014</td>
      <td>CB</td>
      <td>Florida Atlantic</td>
      <td>71</td>
      <td>189</td>
      <td>4</td>
      <td>nan</td>
      <td>22</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Loucheiz Purifoy</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CB</td>
      <td>Florida</td>
      <td>71</td>
      <td>190</td>
      <td>5</td>
      <td>36</td>
      <td>6</td>
      <td>120</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Calvin Pryor</td>
      <td>New York Jets</td>
      <td>1</td>
      <td>18</td>
      <td>2014</td>
      <td>FS</td>
      <td>Louisville</td>
      <td>71</td>
      <td>207</td>
      <td>5</td>
      <td>34</td>
      <td>18</td>
      <td>116</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Jabari Price</td>
      <td>Minnesota Vikings</td>
      <td>7</td>
      <td>225</td>
      <td>2014</td>
      <td>CB</td>
      <td>North Carolina</td>
      <td>71</td>
      <td>200</td>
      <td>4</td>
      <td>nan</td>
      <td>16</td>
      <td>nan</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Terrance Mitchell</td>
      <td>Dallas Cowboys</td>
      <td>7</td>
      <td>254</td>
      <td>2014</td>
      <td>CB</td>
      <td>Oregon</td>
      <td>71</td>
      <td>192</td>
      <td>5</td>
      <td>34</td>
      <td>nan</td>
      <td>117</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Keith McGill</td>
      <td>Oakland Raiders</td>
      <td>4</td>
      <td>116</td>
      <td>2014</td>
      <td>CB</td>
      <td>Utah</td>
      <td>75</td>
      <td>211</td>
      <td>5</td>
      <td>39</td>
      <td>nan</td>
      <td>129</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Dexter McDougle</td>
      <td>New York Jets</td>
      <td>3</td>
      <td>80</td>
      <td>2014</td>
      <td>CB</td>
      <td>Maryland</td>
      <td>70</td>
      <td>196</td>
      <td>4</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Craig Loston</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SS</td>
      <td>LSU</td>
      <td>73</td>
      <td>217</td>
      <td>5</td>
      <td>32</td>
      <td>12</td>
      <td>119</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Isaiah Lewis</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SS</td>
      <td>Michigan State</td>
      <td>70</td>
      <td>211</td>
      <td>5</td>
      <td>36</td>
      <td>15</td>
      <td>122</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Nevin Lawson</td>
      <td>Detroit Lions</td>
      <td>4</td>
      <td>133</td>
      <td>2014</td>
      <td>CB</td>
      <td>Utah State</td>
      <td>69</td>
      <td>190</td>
      <td>4</td>
      <td>33</td>
      <td>16</td>
      <td>120</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Kenny Ladler</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>FS</td>
      <td>Vanderbilt</td>
      <td>72</td>
      <td>207</td>
      <td>5</td>
      <td>36</td>
      <td>24</td>
      <td>127</td>
      <td>nan</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Lamarcus Joyner</td>
      <td>St. Louis Rams</td>
      <td>2</td>
      <td>41</td>
      <td>2014</td>
      <td>CB</td>
      <td>Florida State</td>
      <td>68</td>
      <td>184</td>
      <td>5</td>
      <td>38</td>
      <td>14</td>
      <td>124</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Dontae Johnson</td>
      <td>San Francisco 49ers</td>
      <td>4</td>
      <td>129</td>
      <td>2014</td>
      <td>CB</td>
      <td>North Carolina State</td>
      <td>74</td>
      <td>200</td>
      <td>4</td>
      <td>38</td>
      <td>12</td>
      <td>124</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Stanley Jean-Baptiste</td>
      <td>New Orleans Saints</td>
      <td>2</td>
      <td>58</td>
      <td>2014</td>
      <td>CB</td>
      <td>Nebraska</td>
      <td>75</td>
      <td>218</td>
      <td>5</td>
      <td>42</td>
      <td>13</td>
      <td>128</td>
      <td>nan</td>
      <td>4</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Kendall James</td>
      <td>Minnesota Vikings</td>
      <td>6</td>
      <td>184</td>
      <td>2014</td>
      <td>CB</td>
      <td>Maine</td>
      <td>70</td>
      <td>180</td>
      <td>4</td>
      <td>39</td>
      <td>9</td>
      <td>nan</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Bennett Jackson</td>
      <td>New York Giants</td>
      <td>6</td>
      <td>187</td>
      <td>2014</td>
      <td>CB</td>
      <td>Notre Dame</td>
      <td>72</td>
      <td>195</td>
      <td>5</td>
      <td>38</td>
      <td>13</td>
      <td>128</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Marqueston Huff</td>
      <td>Tennessee Titans</td>
      <td>4</td>
      <td>122</td>
      <td>2014</td>
      <td>FS</td>
      <td>Wyoming</td>
      <td>71</td>
      <td>196</td>
      <td>4</td>
      <td>36</td>
      <td>15</td>
      <td>118</td>
      <td>7</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>&lt;class &#39;pandas.core.frame.DataFrame&#39;&gt;
RangeIndex: 632 entries, 0 to 631
Data columns (total 15 columns):
player            632 non-null object
draft_team        436 non-null object
draft_round       436 non-null object
draft_pick        436 non-null object
draft_year        436 non-null object
draft_position    632 non-null object
college           632 non-null object
draft_height      632 non-null int64
draft_weight      632 non-null int64
forty             630 non-null float64
vertical          527 non-null float64
bench_reps        518 non-null float64
broad_jump        519 non-null float64
three_cone        408 non-null float64
shuttle           421 non-null float64
dtypes: float64(6), int64(2), object(7)
memory usage: 74.1+ KB
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">combine</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s1">&#39;~/Documents/Data Science/Data Projects/Capstone 1/data/CLEAN/combine_FINAL.csv&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
 

