---
title: NFL Cleaner Notebook
layout: code
permalink: /coursework/projects/nfl_defensive_back/nfl_cleaner_notebook
excerpt: ""
section: "/coursework/projects/nfl_defensive_back/#nfl_cleaner.ipynb"
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">nfl</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;~/Documents/Data Science/Data Projects/Capstone 1/data/nfl/nfl_profiles.csv&#39;</span><span class="p">,</span> <span class="n">index_col</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
<span class="n">nfl</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
<span class="n">nfl</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


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
      <th>birth_date</th>
      <th>college</th>
      <th>first_name</th>
      <th>height</th>
      <th>high_school</th>
      <th>last_name</th>
      <th>name</th>
      <th>position</th>
      <th>pref_name</th>
      <th>season_count</th>
      <th>seasons</th>
      <th>weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>18</th>
      <td>1988-12-14</td>
      <td>Fordham</td>
      <td>Isa</td>
      <td>73</td>
      <td>Union (NJ)</td>
      <td>Abdul-Quddus</td>
      <td>Isa Abdul-Quddus</td>
      <td>FS</td>
      <td>Isa</td>
      <td>6</td>
      <td>[2011, 2012, 2013, 2014, 2015, 2016]</td>
      <td>203</td>
    </tr>
    <tr>
      <th>194</th>
      <td>1985-07-27</td>
      <td>Washington State</td>
      <td>Husain</td>
      <td>72</td>
      <td>Pomona (CA)</td>
      <td>Abdullah</td>
      <td>Husain Abdullah</td>
      <td>FS</td>
      <td>Husain</td>
      <td>7</td>
      <td>[2008, 2009, 2010, 2011, 2013, 2014, 2015]</td>
      <td>204</td>
    </tr>
    <tr>
      <th>581</th>
      <td>1983-08-20</td>
      <td>Washington State</td>
      <td>Hamza</td>
      <td>74</td>
      <td>NaN</td>
      <td>Abdullah</td>
      <td>None Abdullah</td>
      <td>S</td>
      <td>NaN</td>
      <td>7</td>
      <td>[2005, 2006, 2007, 2008, 2009, 2010, 2011]</td>
      <td>216</td>
    </tr>
    <tr>
      <th>1203</th>
      <td>1992-02-06</td>
      <td>Southern Methodist</td>
      <td>Kenneth</td>
      <td>72</td>
      <td>Grant (OR)</td>
      <td>Acker</td>
      <td>Kenneth Acker</td>
      <td>CB</td>
      <td>Kenneth</td>
      <td>3</td>
      <td>[2015, 2016, 2017]</td>
      <td>195</td>
    </tr>
    <tr>
      <th>47</th>
      <td>1995-10-17</td>
      <td>Louisiana State</td>
      <td>Jamal</td>
      <td>73</td>
      <td>Carrollton Hebron (TX)</td>
      <td>Adams</td>
      <td>Jamal Adams</td>
      <td>SS</td>
      <td>Jamal</td>
      <td>1</td>
      <td>[2017]</td>
      <td>213</td>
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
Int64Index: 1308 entries, 18 to 535
Data columns (total 12 columns):
birth_date      1297 non-null object
college         1301 non-null object
first_name      1308 non-null object
height          1308 non-null int64
high_school     863 non-null object
last_name       1308 non-null object
name            1308 non-null object
position        1308 non-null object
pref_name       648 non-null object
season_count    1308 non-null int64
seasons         1308 non-null object
weight          1302 non-null float64
dtypes: float64(1), int64(2), object(9)
memory usage: 132.8+ KB
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">cols</span> <span class="o">=</span> <span class="n">nfl</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()</span>
<span class="n">cols</span>
<span class="n">cols</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;name&#39;</span><span class="p">,</span> <span class="s1">&#39;first_name&#39;</span><span class="p">,</span> <span class="s1">&#39;last_name&#39;</span><span class="p">,</span> <span class="s1">&#39;pref_name&#39;</span><span class="p">,</span> <span class="s1">&#39;position&#39;</span><span class="p">,</span> <span class="s1">&#39;height&#39;</span><span class="p">,</span> <span class="s1">&#39;weight&#39;</span><span class="p">,</span> <span class="s1">&#39;birth_date&#39;</span><span class="p">,</span> 
        <span class="s1">&#39;high_school&#39;</span><span class="p">,</span> <span class="s1">&#39;college&#39;</span><span class="p">,</span> <span class="s1">&#39;season_count&#39;</span><span class="p">,</span> <span class="s1">&#39;seasons&#39;</span><span class="p">]</span>
<span class="n">nfl</span> <span class="o">=</span> <span class="n">nfl</span><span class="p">[</span><span class="n">cols</span><span class="p">]</span>

<span class="n">nfl</span> <span class="o">=</span> <span class="n">nfl</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">nfl</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[3]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>[&#39;birth_date&#39;,
 &#39;college&#39;,
 &#39;first_name&#39;,
 &#39;height&#39;,
 &#39;high_school&#39;,
 &#39;last_name&#39;,
 &#39;name&#39;,
 &#39;position&#39;,
 &#39;pref_name&#39;,
 &#39;season_count&#39;,
 &#39;seasons&#39;,
 &#39;weight&#39;]</pre>
</div>

</div>

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
      <th>name</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>pref_name</th>
      <th>position</th>
      <th>height</th>
      <th>weight</th>
      <th>birth_date</th>
      <th>high_school</th>
      <th>college</th>
      <th>season_count</th>
      <th>seasons</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Isa Abdul-Quddus</td>
      <td>Isa</td>
      <td>Abdul-Quddus</td>
      <td>Isa</td>
      <td>FS</td>
      <td>73</td>
      <td>203</td>
      <td>1988-12-14</td>
      <td>Union (NJ)</td>
      <td>Fordham</td>
      <td>6</td>
      <td>[2011, 2012, 2013, 2014, 2015, 2016]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Husain Abdullah</td>
      <td>Husain</td>
      <td>Abdullah</td>
      <td>Husain</td>
      <td>FS</td>
      <td>72</td>
      <td>204</td>
      <td>1985-07-27</td>
      <td>Pomona (CA)</td>
      <td>Washington State</td>
      <td>7</td>
      <td>[2008, 2009, 2010, 2011, 2013, 2014, 2015]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>None Abdullah</td>
      <td>Hamza</td>
      <td>Abdullah</td>
      <td>NaN</td>
      <td>S</td>
      <td>74</td>
      <td>216</td>
      <td>1983-08-20</td>
      <td>NaN</td>
      <td>Washington State</td>
      <td>7</td>
      <td>[2005, 2006, 2007, 2008, 2009, 2010, 2011]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kenneth Acker</td>
      <td>Kenneth</td>
      <td>Acker</td>
      <td>Kenneth</td>
      <td>CB</td>
      <td>72</td>
      <td>195</td>
      <td>1992-02-06</td>
      <td>Grant (OR)</td>
      <td>Southern Methodist</td>
      <td>3</td>
      <td>[2015, 2016, 2017]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Jamal Adams</td>
      <td>Jamal</td>
      <td>Adams</td>
      <td>Jamal</td>
      <td>SS</td>
      <td>73</td>
      <td>213</td>
      <td>1995-10-17</td>
      <td>Carrollton Hebron (TX)</td>
      <td>Louisiana State</td>
      <td>1</td>
      <td>[2017]</td>
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
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">nfl</span> <span class="o">=</span> <span class="n">nfl</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;name&#39;</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">nfl</span><span class="o">.</span><span class="n">pref_name</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">nfl</span><span class="o">.</span><span class="n">first_name</span><span class="p">,</span> <span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">nfl</span><span class="p">[</span><span class="s1">&#39;player&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">nfl</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="p">[</span><span class="s1">&#39;pref_name&#39;</span><span class="p">,</span> <span class="s1">&#39;last_name&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="s1">&#39; &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">x</span><span class="p">),</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">cols</span> <span class="o">=</span> <span class="n">nfl</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()</span>
<span class="n">cols</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;player&#39;</span><span class="p">,</span> <span class="s1">&#39;first_name&#39;</span><span class="p">,</span> <span class="s1">&#39;last_name&#39;</span><span class="p">,</span> <span class="s1">&#39;pref_name&#39;</span><span class="p">,</span> <span class="s1">&#39;position&#39;</span><span class="p">,</span> <span class="s1">&#39;height&#39;</span><span class="p">,</span> <span class="s1">&#39;weight&#39;</span><span class="p">,</span> <span class="s1">&#39;birth_date&#39;</span><span class="p">,</span> 
        <span class="s1">&#39;high_school&#39;</span><span class="p">,</span> <span class="s1">&#39;college&#39;</span><span class="p">,</span> <span class="s1">&#39;season_count&#39;</span><span class="p">,</span> <span class="s1">&#39;seasons&#39;</span><span class="p">]</span>
<span class="n">nfl</span> <span class="o">=</span> <span class="n">nfl</span><span class="p">[</span><span class="n">cols</span><span class="p">]</span>
<span class="nb">len</span><span class="p">(</span><span class="n">nfl</span><span class="p">)</span>
<span class="n">nfl</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[4]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>1308</pre>
</div>

</div>

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
      <th>player</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>pref_name</th>
      <th>position</th>
      <th>height</th>
      <th>weight</th>
      <th>birth_date</th>
      <th>high_school</th>
      <th>college</th>
      <th>season_count</th>
      <th>seasons</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Isa Abdul-Quddus</td>
      <td>Isa</td>
      <td>Abdul-Quddus</td>
      <td>Isa</td>
      <td>FS</td>
      <td>73</td>
      <td>203</td>
      <td>1988-12-14</td>
      <td>Union (NJ)</td>
      <td>Fordham</td>
      <td>6</td>
      <td>[2011, 2012, 2013, 2014, 2015, 2016]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Husain Abdullah</td>
      <td>Husain</td>
      <td>Abdullah</td>
      <td>Husain</td>
      <td>FS</td>
      <td>72</td>
      <td>204</td>
      <td>1985-07-27</td>
      <td>Pomona (CA)</td>
      <td>Washington State</td>
      <td>7</td>
      <td>[2008, 2009, 2010, 2011, 2013, 2014, 2015]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Hamza Abdullah</td>
      <td>Hamza</td>
      <td>Abdullah</td>
      <td>Hamza</td>
      <td>S</td>
      <td>74</td>
      <td>216</td>
      <td>1983-08-20</td>
      <td>NaN</td>
      <td>Washington State</td>
      <td>7</td>
      <td>[2005, 2006, 2007, 2008, 2009, 2010, 2011]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kenneth Acker</td>
      <td>Kenneth</td>
      <td>Acker</td>
      <td>Kenneth</td>
      <td>CB</td>
      <td>72</td>
      <td>195</td>
      <td>1992-02-06</td>
      <td>Grant (OR)</td>
      <td>Southern Methodist</td>
      <td>3</td>
      <td>[2015, 2016, 2017]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Jamal Adams</td>
      <td>Jamal</td>
      <td>Adams</td>
      <td>Jamal</td>
      <td>SS</td>
      <td>73</td>
      <td>213</td>
      <td>1995-10-17</td>
      <td>Carrollton Hebron (TX)</td>
      <td>Louisiana State</td>
      <td>1</td>
      <td>[2017]</td>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># convert object to list of strings</span>
<span class="n">nfl</span><span class="p">[</span><span class="s1">&#39;seasons&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">nfl</span><span class="o">.</span><span class="n">seasons</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">x</span><span class="p">[</span><span class="mi">1</span><span class="p">:</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">&#39;,&#39;</span><span class="p">))</span>

<span class="c1"># convert list of strings to list of ints</span>
<span class="n">nfl</span><span class="p">[</span><span class="s1">&#39;seasons&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">nfl</span><span class="p">[</span><span class="s1">&#39;seasons&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">t</span><span class="p">:</span> <span class="nb">list</span><span class="p">(</span><span class="nb">map</span><span class="p">(</span><span class="nb">int</span><span class="p">,</span> <span class="n">t</span><span class="p">)))</span>

<span class="c1"># add column for last season played</span>
<span class="n">nfl</span><span class="p">[</span><span class="s1">&#39;last_season&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">nfl</span><span class="p">[</span><span class="s1">&#39;seasons&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="nb">max</span><span class="p">(</span><span class="n">x</span><span class="p">))</span>

<span class="c1"># add column for first season played</span>
<span class="n">nfl</span><span class="p">[</span><span class="s1">&#39;rookie&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">nfl</span><span class="p">[</span><span class="s1">&#39;seasons&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="nb">min</span><span class="p">(</span><span class="n">x</span><span class="p">))</span>
<span class="n">nfl</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

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
      <th>player</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>pref_name</th>
      <th>position</th>
      <th>height</th>
      <th>weight</th>
      <th>birth_date</th>
      <th>high_school</th>
      <th>college</th>
      <th>season_count</th>
      <th>seasons</th>
      <th>last_season</th>
      <th>rookie</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Isa Abdul-Quddus</td>
      <td>Isa</td>
      <td>Abdul-Quddus</td>
      <td>Isa</td>
      <td>FS</td>
      <td>73</td>
      <td>203</td>
      <td>1988-12-14</td>
      <td>Union (NJ)</td>
      <td>Fordham</td>
      <td>6</td>
      <td>[2011, 2012, 2013, 2014, 2015, 2016]</td>
      <td>2016</td>
      <td>2011</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Husain Abdullah</td>
      <td>Husain</td>
      <td>Abdullah</td>
      <td>Husain</td>
      <td>FS</td>
      <td>72</td>
      <td>204</td>
      <td>1985-07-27</td>
      <td>Pomona (CA)</td>
      <td>Washington State</td>
      <td>7</td>
      <td>[2008, 2009, 2010, 2011, 2013, 2014, 2015]</td>
      <td>2015</td>
      <td>2008</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Hamza Abdullah</td>
      <td>Hamza</td>
      <td>Abdullah</td>
      <td>Hamza</td>
      <td>S</td>
      <td>74</td>
      <td>216</td>
      <td>1983-08-20</td>
      <td>NaN</td>
      <td>Washington State</td>
      <td>7</td>
      <td>[2005, 2006, 2007, 2008, 2009, 2010, 2011]</td>
      <td>2011</td>
      <td>2005</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kenneth Acker</td>
      <td>Kenneth</td>
      <td>Acker</td>
      <td>Kenneth</td>
      <td>CB</td>
      <td>72</td>
      <td>195</td>
      <td>1992-02-06</td>
      <td>Grant (OR)</td>
      <td>Southern Methodist</td>
      <td>3</td>
      <td>[2015, 2016, 2017]</td>
      <td>2017</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Jamal Adams</td>
      <td>Jamal</td>
      <td>Adams</td>
      <td>Jamal</td>
      <td>SS</td>
      <td>73</td>
      <td>213</td>
      <td>1995-10-17</td>
      <td>Carrollton Hebron (TX)</td>
      <td>Louisiana State</td>
      <td>1</td>
      <td>[2017]</td>
      <td>2017</td>
      <td>2017</td>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># split birth date into 3 columns</span>
<span class="n">nfl</span><span class="p">[</span><span class="s1">&#39;birth_year&#39;</span><span class="p">],</span> <span class="n">nfl</span><span class="p">[</span><span class="s1">&#39;birth_month&#39;</span><span class="p">],</span> <span class="n">nfl</span><span class="p">[</span><span class="s1">&#39;birth_day&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">nfl</span><span class="o">.</span><span class="n">birth_date</span><span class="o">.</span><span class="n">str</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">&#39;-&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">str</span>
<span class="n">_</span><span class="p">,</span> <span class="n">nfl</span><span class="p">[</span><span class="s1">&#39;hs_state&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">nfl</span><span class="o">.</span><span class="n">high_school</span><span class="o">.</span><span class="n">str</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">&#39;(&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">str</span>

<span class="c1"># clean state for HS</span>
<span class="n">nfl</span><span class="o">.</span><span class="n">hs_state</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="n">nfl</span><span class="o">.</span><span class="n">hs_state</span><span class="o">.</span><span class="n">str</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">&#39;)&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">str</span>
<span class="n">nfl</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
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
      <th>player</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>pref_name</th>
      <th>position</th>
      <th>height</th>
      <th>weight</th>
      <th>birth_date</th>
      <th>high_school</th>
      <th>college</th>
      <th>season_count</th>
      <th>seasons</th>
      <th>last_season</th>
      <th>rookie</th>
      <th>birth_year</th>
      <th>birth_month</th>
      <th>birth_day</th>
      <th>hs_state</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Isa Abdul-Quddus</td>
      <td>Isa</td>
      <td>Abdul-Quddus</td>
      <td>Isa</td>
      <td>FS</td>
      <td>73</td>
      <td>203</td>
      <td>1988-12-14</td>
      <td>Union (NJ)</td>
      <td>Fordham</td>
      <td>6</td>
      <td>[2011, 2012, 2013, 2014, 2015, 2016]</td>
      <td>2016</td>
      <td>2011</td>
      <td>1988</td>
      <td>12</td>
      <td>14</td>
      <td>NJ</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Husain Abdullah</td>
      <td>Husain</td>
      <td>Abdullah</td>
      <td>Husain</td>
      <td>FS</td>
      <td>72</td>
      <td>204</td>
      <td>1985-07-27</td>
      <td>Pomona (CA)</td>
      <td>Washington State</td>
      <td>7</td>
      <td>[2008, 2009, 2010, 2011, 2013, 2014, 2015]</td>
      <td>2015</td>
      <td>2008</td>
      <td>1985</td>
      <td>07</td>
      <td>27</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Hamza Abdullah</td>
      <td>Hamza</td>
      <td>Abdullah</td>
      <td>Hamza</td>
      <td>S</td>
      <td>74</td>
      <td>216</td>
      <td>1983-08-20</td>
      <td>NaN</td>
      <td>Washington State</td>
      <td>7</td>
      <td>[2005, 2006, 2007, 2008, 2009, 2010, 2011]</td>
      <td>2011</td>
      <td>2005</td>
      <td>1983</td>
      <td>08</td>
      <td>20</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kenneth Acker</td>
      <td>Kenneth</td>
      <td>Acker</td>
      <td>Kenneth</td>
      <td>CB</td>
      <td>72</td>
      <td>195</td>
      <td>1992-02-06</td>
      <td>Grant (OR)</td>
      <td>Southern Methodist</td>
      <td>3</td>
      <td>[2015, 2016, 2017]</td>
      <td>2017</td>
      <td>2015</td>
      <td>1992</td>
      <td>02</td>
      <td>06</td>
      <td>OR</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Jamal Adams</td>
      <td>Jamal</td>
      <td>Adams</td>
      <td>Jamal</td>
      <td>SS</td>
      <td>73</td>
      <td>213</td>
      <td>1995-10-17</td>
      <td>Carrollton Hebron (TX)</td>
      <td>Louisiana State</td>
      <td>1</td>
      <td>[2017]</td>
      <td>2017</td>
      <td>2017</td>
      <td>1995</td>
      <td>10</td>
      <td>17</td>
      <td>TX</td>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># clean up column names and sort order</span>
<span class="n">cols</span> <span class="o">=</span> <span class="n">nfl</span><span class="o">.</span><span class="n">columns</span>

<span class="n">cols</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;player&#39;</span><span class="p">,</span> <span class="s1">&#39;last_name&#39;</span><span class="p">,</span> <span class="s1">&#39;first_name&#39;</span><span class="p">,</span> <span class="s1">&#39;pref_name&#39;</span><span class="p">,</span> <span class="s1">&#39;position&#39;</span><span class="p">,</span> <span class="s1">&#39;height&#39;</span><span class="p">,</span> <span class="s1">&#39;weight&#39;</span><span class="p">,</span> <span class="s1">&#39;birth_date&#39;</span><span class="p">,</span> <span class="s1">&#39;birth_year&#39;</span><span class="p">,</span>
        <span class="s1">&#39;birth_month&#39;</span><span class="p">,</span> <span class="s1">&#39;birth_day&#39;</span><span class="p">,</span> <span class="s1">&#39;hs_state&#39;</span><span class="p">,</span> <span class="s1">&#39;high_school&#39;</span><span class="p">,</span> <span class="s1">&#39;college&#39;</span><span class="p">,</span> <span class="s1">&#39;season_count&#39;</span><span class="p">,</span> <span class="s1">&#39;rookie&#39;</span><span class="p">,</span> <span class="s1">&#39;last_season&#39;</span><span class="p">,</span> 
        <span class="s1">&#39;seasons&#39;</span><span class="p">]</span>
<span class="n">nfl</span> <span class="o">=</span> <span class="n">nfl</span><span class="p">[</span><span class="n">cols</span><span class="p">]</span>

<span class="c1"># reset index</span>
<span class="n">nfl</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="n">nfl</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
<span class="n">nfl</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
      <th>last_name</th>
      <th>first_name</th>
      <th>pref_name</th>
      <th>position</th>
      <th>height</th>
      <th>weight</th>
      <th>birth_date</th>
      <th>birth_year</th>
      <th>birth_month</th>
      <th>birth_day</th>
      <th>hs_state</th>
      <th>high_school</th>
      <th>college</th>
      <th>season_count</th>
      <th>rookie</th>
      <th>last_season</th>
      <th>seasons</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Isa Abdul-Quddus</td>
      <td>Abdul-Quddus</td>
      <td>Isa</td>
      <td>Isa</td>
      <td>FS</td>
      <td>73</td>
      <td>203</td>
      <td>1988-12-14</td>
      <td>1988</td>
      <td>12</td>
      <td>14</td>
      <td>NJ</td>
      <td>Union (NJ)</td>
      <td>Fordham</td>
      <td>6</td>
      <td>2011</td>
      <td>2016</td>
      <td>[2011, 2012, 2013, 2014, 2015, 2016]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Husain Abdullah</td>
      <td>Abdullah</td>
      <td>Husain</td>
      <td>Husain</td>
      <td>FS</td>
      <td>72</td>
      <td>204</td>
      <td>1985-07-27</td>
      <td>1985</td>
      <td>07</td>
      <td>27</td>
      <td>CA</td>
      <td>Pomona (CA)</td>
      <td>Washington State</td>
      <td>7</td>
      <td>2008</td>
      <td>2015</td>
      <td>[2008, 2009, 2010, 2011, 2013, 2014, 2015]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Hamza Abdullah</td>
      <td>Abdullah</td>
      <td>Hamza</td>
      <td>Hamza</td>
      <td>S</td>
      <td>74</td>
      <td>216</td>
      <td>1983-08-20</td>
      <td>1983</td>
      <td>08</td>
      <td>20</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Washington State</td>
      <td>7</td>
      <td>2005</td>
      <td>2011</td>
      <td>[2005, 2006, 2007, 2008, 2009, 2010, 2011]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kenneth Acker</td>
      <td>Acker</td>
      <td>Kenneth</td>
      <td>Kenneth</td>
      <td>CB</td>
      <td>72</td>
      <td>195</td>
      <td>1992-02-06</td>
      <td>1992</td>
      <td>02</td>
      <td>06</td>
      <td>OR</td>
      <td>Grant (OR)</td>
      <td>Southern Methodist</td>
      <td>3</td>
      <td>2015</td>
      <td>2017</td>
      <td>[2015, 2016, 2017]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Jamal Adams</td>
      <td>Adams</td>
      <td>Jamal</td>
      <td>Jamal</td>
      <td>SS</td>
      <td>73</td>
      <td>213</td>
      <td>1995-10-17</td>
      <td>1995</td>
      <td>10</td>
      <td>17</td>
      <td>TX</td>
      <td>Carrollton Hebron (TX)</td>
      <td>Louisiana State</td>
      <td>1</td>
      <td>2017</td>
      <td>2017</td>
      <td>[2017]</td>
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
RangeIndex: 1308 entries, 0 to 1307
Data columns (total 18 columns):
player          1308 non-null object
last_name       1308 non-null object
first_name      1308 non-null object
pref_name       1308 non-null object
position        1308 non-null object
height          1308 non-null int64
weight          1302 non-null float64
birth_date      1297 non-null object
birth_year      1297 non-null object
birth_month     1297 non-null object
birth_day       1297 non-null object
hs_state        830 non-null object
high_school     863 non-null object
college         1301 non-null object
season_count    1308 non-null int64
rookie          1308 non-null int64
last_season     1308 non-null int64
seasons         1308 non-null object
dtypes: float64(1), int64(4), object(13)
memory usage: 184.0+ KB
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">nfl</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s1">&#39;/Users/brad/Documents/Data Science/Data Projects/Capstone 1/data/CLEAN/nfl_FINAL.csv&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
 

