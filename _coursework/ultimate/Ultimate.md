---
title: Ultimate Take Home Challenge - Analysis
permalink: /coursework/takehomes/ultimate/
---

<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">os</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">datetime</span>

<span class="kn">from</span> <span class="nn">matplotlib</span> <span class="k">import</span> <span class="n">rcParams</span>
<span class="kn">import</span> <span class="nn">matplotlib</span> <span class="k">as</span> <span class="nn">mpl</span>

<span class="o">%</span><span class="k">matplotlib</span> inline

<span class="n">blue</span> <span class="o">=</span> <span class="s1">&#39;#3498DB&#39;</span>
<span class="n">gray</span> <span class="o">=</span> <span class="s1">&#39;#95A5A6&#39;</span>
<span class="n">red</span> <span class="o">=</span> <span class="s1">&#39;#E74C3C&#39;</span>
<span class="n">dark_gray</span> <span class="o">=</span> <span class="s1">&#39;#34495E&#39;</span>
<span class="n">green</span> <span class="o">=</span> <span class="s1">&#39;#2ECC71&#39;</span>
<span class="n">purple</span> <span class="o">=</span> <span class="s1">&#39;#9B59B6&#39;</span>
<span class="n">flatui</span> <span class="o">=</span> <span class="p">[</span><span class="n">blue</span><span class="p">,</span> <span class="n">gray</span><span class="p">,</span> <span class="n">red</span><span class="p">,</span> <span class="n">dark_gray</span><span class="p">,</span> <span class="n">green</span><span class="p">,</span> <span class="n">purple</span><span class="p">]</span>

<span class="c1"># Patches</span>
<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;patch&#39;</span><span class="p">,</span> 
       <span class="n">linewidth</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span> 
       <span class="n">facecolor</span><span class="o">=</span><span class="n">dark_gray</span><span class="p">,</span> 
       <span class="n">edgecolor</span><span class="o">=</span><span class="s1">&#39;w&#39;</span><span class="p">,</span> 
       <span class="n">force_edgecolor</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> 
       <span class="n">antialiased</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>    
  
<span class="c1"># Figure</span>
<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;figure&#39;</span><span class="p">,</span> 
       <span class="n">figsize</span><span class="o">=</span> <span class="p">(</span><span class="mi">15</span><span class="p">,</span> <span class="mi">9</span><span class="p">),</span>
       <span class="n">dpi</span><span class="o">=</span> <span class="mi">200</span><span class="p">,</span>
       <span class="n">facecolor</span><span class="o">=</span><span class="s1">&#39;w&#39;</span><span class="p">,</span> 
       <span class="n">edgecolor</span><span class="o">=</span><span class="s1">&#39;w&#39;</span><span class="p">,</span> 
       <span class="n">titlesize</span><span class="o">=</span><span class="s1">&#39;xx-large&#39;</span><span class="p">,</span>
       <span class="n">titleweight</span><span class="o">=</span><span class="mi">700</span><span class="p">)</span>

<span class="c1"># Grid</span>
<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;grid&#39;</span><span class="p">,</span> 
       <span class="n">color</span><span class="o">=</span><span class="n">dark_gray</span><span class="p">,</span>
       <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span> 
       <span class="n">linewidth</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span> 
       <span class="n">linestyle</span><span class="o">=</span><span class="s1">&#39;-&#39;</span><span class="p">)</span>

<span class="c1"># Axes</span>
<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;axes&#39;</span><span class="p">,</span> 
       <span class="n">facecolor</span><span class="o">=</span><span class="s1">&#39;w&#39;</span><span class="p">,</span>
       <span class="n">edgecolor</span><span class="o">=</span><span class="n">dark_gray</span><span class="p">,</span>
       <span class="n">linewidth</span><span class="o">=</span><span class="mf">0.5</span><span class="p">,</span>
       <span class="n">grid</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span>
       <span class="n">titlesize</span><span class="o">=</span><span class="s1">&#39;large&#39;</span><span class="p">,</span>
       <span class="n">labelsize</span><span class="o">=</span><span class="s1">&#39;large&#39;</span><span class="p">,</span>
       <span class="n">labelcolor</span><span class="o">=</span><span class="n">dark_gray</span><span class="p">,</span>
       <span class="n">axisbelow</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;axes.spines&#39;</span><span class="p">,</span>
       <span class="n">right</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span>
       <span class="n">top</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>

<span class="c1"># Ticks</span>
<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;xtick&#39;</span><span class="p">,</span> 
       <span class="n">direction</span><span class="o">=</span><span class="s1">&#39;out&#39;</span><span class="p">,</span>
       <span class="n">color</span><span class="o">=</span><span class="n">dark_gray</span><span class="p">)</span>

<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;xtick.major&#39;</span><span class="p">,</span> 
       <span class="n">size</span><span class="o">=</span><span class="mf">0.0</span><span class="p">)</span>

<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;xtick.minor&#39;</span><span class="p">,</span> 
       <span class="n">size</span><span class="o">=</span><span class="mf">0.0</span><span class="p">)</span>

<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;ytick&#39;</span><span class="p">,</span> 
       <span class="n">direction</span><span class="o">=</span><span class="s1">&#39;out&#39;</span><span class="p">,</span>
       <span class="n">color</span><span class="o">=</span><span class="n">dark_gray</span><span class="p">)</span>

<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;ytick.major&#39;</span><span class="p">,</span> 
       <span class="n">size</span><span class="o">=</span><span class="mf">0.0</span><span class="p">)</span>

<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;ytick.minor&#39;</span><span class="p">,</span> 
       <span class="n">size</span><span class="o">=</span><span class="mf">0.0</span><span class="p">)</span>

<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;legend&#39;</span><span class="p">,</span> 
       <span class="n">frameon</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span>
       <span class="n">numpoints</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span>
       <span class="n">scatterpoints</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>

<span class="n">mpl</span><span class="o">.</span><span class="n">rc</span><span class="p">(</span><span class="s1">&#39;font&#39;</span><span class="p">,</span> 
       <span class="n">size</span><span class="o">=</span><span class="mi">13</span><span class="p">,</span>
       <span class="n">weight</span><span class="o">=</span><span class="mi">400</span><span class="p">,</span>
       <span class="n">family</span><span class="o">=</span><span class="s1">&#39;sans-serif&#39;</span><span class="p">)</span>

<span class="n">rcParams</span><span class="p">[</span><span class="s1">&#39;font.sans-serif&#39;</span><span class="p">]:</span> <span class="p">[</span><span class="s1">&#39;Helvetica&#39;</span><span class="p">,</span> <span class="s1">&#39;Verdana&#39;</span><span class="p">,</span> <span class="s1">&#39;Lucida Grande&#39;</span><span class="p">]</span>

<span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s1">&#39;display.width&#39;</span><span class="p">,</span> <span class="mi">500</span><span class="p">)</span>
<span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s1">&#39;display.max_columns&#39;</span><span class="p">,</span> <span class="mi">100</span><span class="p">)</span>
<span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s1">&#39;display.notebook_repr_html&#39;</span><span class="p">,</span> <span class="kc">True</span><span class="p">)</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Part-1-&#8208;-EDA"><strong>Part 1 &#8208; EDA</strong><a class="anchor-link" href="#Part-1-&#8208;-EDA">&#182;</a></h2><p>The attached logins.json file contains (simulated) timestamps of user logins in a particular geographic location. Aggregate these login counts based on 15­minute time intervals, and visualize and describe the resulting time series of login counts in ways that best characterize the underlying patterns of the demand. Please report/illustrate important features of the demand, such as daily cycles. If there are data quality issues, please report them.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># load json data</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_json</span><span class="p">(</span><span class="s1">&#39;data/logins.json&#39;</span><span class="p">)</span>

<span class="c1"># take a look at the data</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
<span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
      <th>login_time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1970-01-01 20:13:18</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1970-01-01 20:16:10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1970-01-01 20:16:37</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1970-01-01 20:16:36</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1970-01-01 20:26:21</td>
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
RangeIndex: 93142 entries, 0 to 93141
Data columns (total 1 columns):
login_time    93142 non-null datetime64[ns]
dtypes: datetime64[ns](1)
memory usage: 727.8 KB
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">login_time</span><span class="o">.</span><span class="n">min</span><span class="p">()</span>
<span class="n">df</span><span class="o">.</span><span class="n">login_time</span><span class="o">.</span><span class="n">max</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[3]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Timestamp(&#39;1970-01-01 20:12:16&#39;)</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[3]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Timestamp(&#39;1970-04-13 18:57:38&#39;)</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># get login counts on a 15-minute time interval</span>

<span class="c1"># need datetime index to resample</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">set_index</span><span class="p">([</span><span class="s1">&#39;login_time&#39;</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># add &#39;count&#39; column</span>
<span class="n">df</span><span class="p">[</span><span class="s1">&#39;count&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="mi">0</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">resample</span><span class="p">(</span><span class="s1">&#39;15T&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">count</span><span class="p">()</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
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
      <th>login_time</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1970-01-01 20:00:00</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1970-01-01 20:15:00</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1970-01-01 20:30:00</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1970-01-01 20:45:00</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1970-01-01 21:00:00</td>
      <td>1</td>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
RangeIndex: 9788 entries, 0 to 9787
Data columns (total 2 columns):
login_time    9788 non-null datetime64[ns]
count         9788 non-null int64
dtypes: datetime64[ns](1), int64(1)
memory usage: 153.0 KB
</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># histogram</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">&#39;login_time&#39;</span><span class="p">],</span> <span class="n">df</span><span class="p">[</span><span class="s1">&#39;count&#39;</span><span class="p">])</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xticks</span><span class="p">(</span><span class="n">rotation</span> <span class="o">=</span> <span class="mi">45</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;date&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;logins&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Ultimate logins: Jan. 1 - Apr 13, 1970 (15 min. intervals)&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAZAAAAE8CAYAAADuYedZAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4zLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvIxREBQAAIABJREFUeJzsnXmYHEXZwH+V+74IhAQCCRBCQAISG/FAVO4GBRVFRWgQD8RbFAFRPFBR/EBAUBCEFrkvQdNyhQTCFZoNSQhJNudurs0mu9n7Pur7o3tme2bnnu7pmd36PU+e9HZXV79TXV1v1VtvvSWklCgUCoVCkS1DwhZAoVAoFKWJUiAKhUKhyAmlQBQKhUKRE0qBKBQKhSInlAJRKBQKRU4oBaJQKBSKnCh5BSKE+LgQYnuK6wcJIZqFEEMLKVcmCCF+KYT4lw/5nCiEKPdDJoUiFUKIh4QQ5xaBHH8TQvzcp7yahRCH+JFXkKRr6zzpvieEuKEQMhW9AhFCSCHEYXHnkja8QogKIcQpkb+llFullOOklD0ByOaLAsgXKeVSKeXcoJ8TX7YBPucTQojFQogGIUSFj/kuEULUCSFG+pWnJ++7hBDlQoheIcTFcde+6F5rEELsFkKYQogJGeY7QgjxuFv2Ugjx8bjrk9z8drv/fum5Fuk8ef9JIcQVnjRfFkJUCiFahBD/FkJMSSHLfOAY4Gn37+lCiGeEEDvdfGfFpb9PCNEZ93xfOnJSysuklL/xKa9xUsrNmaRN1B4VIXcBXxFC7Bf0g4pegSgGJS3AP4Cf+JWh27idCEjg03nkMyzJpZXA5cDyBNdeAz4ipZwIHAIMA67P4rGvAl8BdiW4djMwBpgFHA9cKIS4BGI6T+OklOOAo4Fe4An3txwF3AlcCEwDWoE7UsjxTeAB2bf6uBd4Fvhcinv+6JUhiI5cqZCi7viKlLId+B9wUdDPGlAKRAhxP3AQ8B+3t3OlEGKW22sY5qZZIoS4XgjxupvmP0KIfYQQDwghGoUQtrcnJYS4RQixzb1WJoQ40T1/BnANcL6bz0r3/EQhxD1CiCohxA73WRn1uoQQnxZCvCeEqHflnOe5dpwQ4h0hRJMQ4jEhxCNCiOvdazFDW7e3+mMhxCq31/uIEGKUe22qEOK/7jP2CiGWCiGyrgdCiEOFEC8JIWqFEDVu+U3KRIZ0SCnfklLeD2TUK8yQi4A3gfsAI+633Ccck8gLbvm+LIQ42HNdCiG+LYTYAGxIIvPtUspFQHuCa9uklDWeUz1ARr1YKWWnlPLPUspX3fvi+RROI90qpawA7gG+miS7i4BX3HQAFwD/kVK+IqVsBn4OfFYIMT7J/WcCL3tkq5ZS3gHYmfyWVAghLhZCvCaEuNmtm5uFEB92z29zR1eGJ/198fVfCHGFm64qokQzfHZ0VOHme7sQYqFbF5YJIQ51r73i3rLS/ebPd8+fLYRY4cr9unBGapG8K4QQPxVCrAJahBDXCiEej3v+LUKIW93jS4QQa91nbxZCfDOF3D9125gm4YxwT/ZcXgKclWkZ5MqAUiBSyguBrcCn3N7OH5Mk/SJOr+sA4FDgDeBeYAqwFrjOk9YGjnWvPQg8JoQYJaV8Fvgd8Ij7rGPc9CbQjdNAvB84DfhaOtmFEIcDDwE/APYFLBxFOEIIMQJ4Cqfxm+Km+0yaLL8AnAHMBuYDF7vnrwC2u8+YhqMEpSvDHUKIVD3QGJGB3wMzgHnATOCXGcoQBhcBD7j/ThdCTIu7fgHwG2AqsMJN5+Vc4IPAkbk8XAjxUSFEA9CE02P/cy75JMs+7vh9SdJdhFM/IxyFM3ICQEq5CegEDu/3ACHG4rzHbOfaLnc7KmVCiFQjFXDKdxWwD8639jCg4XxLXwH+IoQYl+Te/YGJON/0pcDtQojJWcoa4UvAr4DJwEbgtwBSyo+5149xv/lHhBDH4YyWv+nKfSfwjIg1k34JpzGfBNwP6MI1Ybqdyy+4vxdgN3A2MAG4BLjZfUYMQoi5wHcATUo5HjgdqPAkWYtjbgyUAaVAsuBeKeUmKWUDzlBvk5TyRSllN/AYTsMPgJTyX1LKWillt5Ty/4CRQML5BrdROhP4gZSyRUq5G8fE8MUMZDofWCilfEFK2QX8CRgNfBg4AcfscauUsktK+STwVpr8bpVS7pRS7gX+g6MEAbqA6cDBbl5LIyYJKeXlUsrLM5AVKeVGV9YOKeUe4CbgpAxlKChCiI8CBwOPSinLgE3Al+OSLXR74h3Az4APCSFmeq7/Xkq5V0rZlosMUspXXRPWgcCNxH7s+fAscJUQYrzbi/4qjkkrBuGMnKcB3t7vOKAhLmkDkGgEEhldNmUh263AHGA/nNHNfUKIj6RIv0VKea9r5noEp1Pya7eOPY+j3JKN3LrctF1SSgtoJsl3mgFPuqPgbpyORKp6+3XgTinlMillj5TSBDpwvtkIt7qj0DYpZSWOmTPiiPBJoFVK+SaAlHKh2zZJKeXLwPM4ptd4enDaoiOFEMOllBVuByBCE45CDZRSUCA9wPC4c8NxKkyuVHuO2xL8He3luMPita4Zph7npUxNku/BrmxV7nC2HqdHkslk1gygMvKHlLIX2IbTo5oB7PDYnnGvpcJrL2/1/KYbcXpVz7tD5KsykK0fQoj9hBAPu0PoRuBf9C+XZDL4hmt6ikzQXpMkmQE87zEjPUicGQtPebrmnL045d7vej5IKXfgNPoP+5Ef8D2cOrsBZ3L7IZwRZjwG8IT72yI04/R0vUwgsZKod/9PZt7qh5RyuafzZeE0xp9NcUv8d4iUMum3GUet2+BHyKe+ZVNvDwauiHzv7jc/k9R150GcUQk4HZnI6AMhxJlCiDfdUVs9oJOgvZFSbsSxVvwS2O1+i95njqd/58B3SkGBbMWZIPQyG09jG4dv4YXdXttPcYaYk6WUk3BeSsRkEP+sbTi9j6lSyknuvwlSyqMyeNxOnMoYebbAqYg7gCrgAPdchJnkgJSySUp5hZTyEBz7+Y/ibKeZ8nuc3z9fSjkBx8QgUt/iP9LxxolM0P4u/roQYjTO+ztJCLFLCLEL+CFwjBDCO8Sf6blnHI6pcKf3UT6KPQzHdJo37qjoAinl/m49G0Lc6NQtg88Ta74CeA+PmUM4rqwjgfUJntOCM3LrZ97KRlxCqCMBsw34red7nySlHCOlfMiTJr7uPAZ8XAhxII4p+kEA1+z1BI71YZrb3lgkKTMp5YNSysjoWgJ/8Fyeh8c8GRSloEAeAa4VQhwohBgiHDfSTxE7FPdSjePp4gfjceYz9gDDhBC/ILbHVg3MEu4ktJSyCmfI+X9CiAmuvIcKIeJNO4l4FDhLCHGyEGI4zlxFB/A6zhxND/AdIcQwIcQ5OB43WeNO+B3mKqNGN99cPGPG4/Rg64UQB+Cvx9QQ4Uy4D3f+FKPceaBcOBfn9x2JY4o4FufjWkqsl4ruzlOMwJkLWSalzHjU4c5VjcL52Ie7Mg9xr10gHJdaIZzJ+d8Cizz33ieEuC9F3iNFnwPCCDdv4V47VDhOIEOFEGcC36C/h9dncEYQi+POPwB8SjjriMYCv8Yx3yQzU1nEmSlduSL2fq+cCCHOE0KMc9/naTidjGeS/c4SIb59+TtwmRDig+77HSuEOEskd0TANfkuwZl33SKlXOteGoFTlnuAbvd9npYoDyHEXCHEJ12l044zOvN+xyfhmOcDpRQUyK9xGtFXgTrgj8AFUsrVSdL/Hkfh1Ashfpzns5/DeQnrcUY87cQORx9z/68VQkTcNy/CqQhrXHkfx5lzSImUshznA7sNqMFRkp+SjhdOJ87Q/1KchuArwH9xFEy2zAFexGn83wDukFIugag56G/pRHX//xVwHM6IbCHwZKYCiL71CQclSfIxnA/CwvGqa8NRzLlg4Mx5bZVS7or8A/4CXCD6XCsfxHGe2AsswJlUz4bnXTk/jOOH3+b+DnCU1+s4Zf4azkT01z33znTPJ6Pcze8AnDrZRt9odQHwLo7Z6fc438Z7cfcbwD/jTKC46S7DUSS7cToFqebA7sIpM2+PuM39XQDr3L8jfB9nBF2PYzr9eqSuFRIhxDVCCL8a018Cptu+fEFK+TbOu/wLzve+kcycRR4ETsFjvnIV9/dwOpN1OOatZAp3JHADTluxC8dMfg1ElbpO/xGn7wipNpQqSYQQy4C/SSnvLeAz9wKflFKuKNQzC4Hb+98upbw2hGePwDE1zHedJ4oaIcSDOM4I/w5bFkVihBDfBWZKKa8M+lkFWdiiyB/XDFaO0+O4AMct9tkCPv9UYChJ1kEocsMdXc5Lm7BIkFLGe68pigwp5W2FepZSIKXDXJyh7Ticyczz3DmXwBFCPIzjo/91dzJVoVAolAlLoVAoFLlRCpPoCoVCoShClAJRKBQKRU4UvQL5zwtLJY7raNH8K99UGboMSk4lo5JTyZlGzsApegVSVV2TPlGBaW5pDVuEjFBy+kcpyAhKTr9Rcqam6BWIQqFQKIoTpUAUCoVCkRNKgSgUCoUiJ5QCUSgUCkVOKAWiUCgUipxQCkShUCgUOaEUiEKhUChyQikQhaLImHXVQv66ZFP6hApFyCgFolAUIX94dl3YIigUaVEKRKFQKBQ5oRSIQqFQKHJCKRCFQqFQ5ERBdiTUdGMu8Ijn1CHAL4B/uudnARXAF2zLrCuETAqFQqHIj4KMQGzLLLct81jbMo8FFgCtwFPAVcAi2zLnAIvcvxUKhUJRAoRhwjoZ2GRbZiVwDmC6503g3BDkUSgUCkUOhKFAvgg85B5Psy2zCsD9f78Q5FEoFApFDhRkDiSCphsjgE8DV2d6T01dPWWr1gYnVA6Ub6oMW4SMUHL6Rxgy5lLvS6EsQcnpN4nkXDB/XuDPLagCAc4EltuWWe3+Xa3pxnTbMqs03ZgO7I6/YerkSQUpiGwpRpkSoeT0j4LJ+ODmvJ5XCmUJSk6/CUPOQpuwvkSf+QrgGcBwjw3g6QLLo1AoFIocKZgC0XRjDHAq8KTn9A3AqZpubHCv3VAoeRQKhUKRHwUzYdmW2QrsE3euFscrS6FQKBQlhlqJrlAoFIqcUApEoVAoFDmhFIhCoVAockIpEIVCoVDkhFIgCoVCocgJpUAUCoUiDda7Vcy6aiHVje1hi1JUKAWiUCgUaXjora0ArNvVFLIkxYVSIAqFQqHICaVAFIoiQkoZtgiKFIiwBSgylAJRKBQKRU4oBaJQKBRpWLqhJmwRihKlQBQKhUKRE0qBKBQKRYYINQkSg1IgCoVCocgJpUAUCoVCkRNKgSgUCoUiJ5QCUSgUigwRaiVIDEqBKBQKhSInCralraYbk4C7gfcBEvgqUA48AswCKoAv2JZZVyiZFAqFQpE7hRyB3AI8a1vmEcAxwFrgKmCRbZlzgEXu3wrFoEVFMilulBtvLAVRIJpuTAA+BtwDYFtmp22Z9cA5gOkmM4FzCyGPQqFQKPKnUCOQQ4A9wL2abryj6cbdmm6MBabZllkF4P6/X4HkUSgUihi6e3q57P4yVu9oCFuUkqFQcyDDgOOA79qWuUzTjVvI0FxVU1dP2aq1gQqXLeWbKsMWISOUnP5RKBl7PTasXOp9KZQlFKec2xs6efa9Xby7rZZbz54J9Jdz/eatjGrdE4Z4KUlUngvmzwv8uYVSINuB7bZlLnP/fhxHgVRrujHdtswqTTemA7vjb5w6eVJBCiJbilGmRCg5/aMQMvb2SnhoS17PK4WyhOKTc+LuJli4nVEjR8TItmD+PHhwMwBzDzmIBYdNDUvElIRRngUxYdmWuQvYpunGXPfUycAa4BnAcM8ZwNOFkEehUCgU+VMwN17gu8ADmm6MADYDl+AosEc13bgU2Ap8voDyKBQKhSIPCqZAbMtcAXwgwaWTCyWDQqFQKPxDrURXKBQKDymX4qh1IDEoBaJQKBSA0g7ZoxSIQqFQZIgKphiLUiAKRRGhIpmEiSr9bFEKRKFQKDyoMUbmKAWiUCgUipxQCkShUCg8KENW5igFolAoMqK6sZ32rp6wxQiQ9MYrFc49FqVAFApFRnzwd4sw/vFW2GIoigilQBQKRcYs27I3bBEURYRSIAqFQqHICaVAFAqFIkPUFEgsSoEoFAqFIieUAlEoiggpS9uJ9NG3t/GjR1aELYaiQCgFolAofOPKx1fx5Ds7whZDUSCUAlEoFAMWKSUd3f6tXRFqIUgMSoEoFIoBy4NvbWXutc+yva7Vl/yU/ohFKRCFQjFgWbiqCoDKWn8UiCKWgm1pq+lGBdAE9ADdtmV+QNONKcAjwCygAviCbZl1hZJJoRgsvL6xhqMPnMj4UcPDFqWg5OSTUNp+DAWl0COQT9iWeaxtmZG90a8CFtmWOQdY5P6tUCh8ZE9TB1++exnfe+idsEUJjUwsT8o8lT1hm7DOAUz32ATODVEWhWJAEgmAuL66OWRJSh+lY2IppAKRwPOabpRpuvEN99w02zKrANz/9yugPIpBxtMrdvCflTvDFkMRMDvq2/jlM+/R0yt5Y3NtxvclM3cN7AjE+VGwORDgI7Zl7tR0Yz/gBU031mVyU01dPWWr1gYsWnaUb6oMW4SMUHLG8v2HNwMwQzRkfW+hZOzp7WvFcqn3ieTc3dwFQGdXly/fUiZ5pEsTZHle+8JO1u5pZ87Yzui59Zu3MrJ1T8r7tjc46ds7O6Pyl2+q5IWNjdE05ZsqEY3VAUidH4nKc8H8eYE/t2AKxLbMne7/uzXdeAo4HqjWdGO6bZlVmm5MB3bH3zd18qSCFES2FKNMiVByenhwc17PKoSM3T298PCWvJ4Xf9+2va3wzDZGDB+e32/IpPyyKOOgynPMa3VAO3MPPRhecEachx96EAsOnZryvom7m2HhdkaNHBEjm2gfC2/VADD30INZMGtKIHLnSxjfekFMWJpujNV0Y3zkGDgNWA08AxhuMgN4uhDyKBTFShAOQJHJ4VIPk1Iw4oppiGfiQ020x1KoOZBpwKuabqwE3gIW2pb5LHADcKqmGxuAU92/FQqFj6jV05mRrJhU+SWnICYs2zI3A8ckOF8LnFwIGRQKxeBF5OE/NUQpkKSE7carUCgKxGAzYPn1e4co/ZEUpUAUigFOpP0bLFMgfrf3sQMQpU28KAWiUAxA2rt6uH3xRrp6esMWpeRRJqzkFHIdiEKhKBB3vbKZm15Yz9gRQzntqP3DFqegJBpoKR0QDGoEolAMQFo6uwFo7eoZtI2nXz/b64U1WMsyGUqBKIqGm15YHw349+0HlnProg0hS1S69Lor2het7VubK4t8Gv2r99nMumohje1dvuRX3L92YKAUiKJouHXRBp5xY1UtfLeKm15YH7JEpcveFqcRLqssnd0RXlrnKLuyivxkVoOEwqEUiI80tPrTc1Io8qWYTS0tHd109SQfH3QGMPFfxMUBQFdPL80d3WGLkTVKgfjEK+v3cMyvn2fphtQB2xSKVAThapvPIroIfjZuR133HD9/MXlU5GL2HAtKEX31Ppv3XfdcQLkHh1IgPvG2ayooJZOBYuCSqKHLRzk1+TQvEWFDbUfSa2GvVwnj8Us31ITw1PxRCkShUBQVfjXg2SqiZKOLYjd/hYlSIArFACTRHEgxz4sETSYBEZXXVvYoBaJQDBLyMQ2FbVbKhVwVZqrbVGTeWJQCUSiKiF6fWupSmYt7bWMNf3quPOZcse1bEq8zXttYw43PZbSh6oBHKRCFooiobmz3JZ9Ne1p8ySdCUE36BXcv4y+LNwaUex/5DBzi9dkFdy/j9sWb8hNogKAUiEJRRPjhctsvT2V1yYpUylIVZSxKgRQxDyyrZNZVC2loUwsUi4VXN9Qw66qF0ZArs65ayJWPr/Qt/yAbez9HEbct2sCsqxY6e7j7wIpt9b7k48U3LyylNZKiFEgRc99rFYB/Zg1F/jy5fDtANOQKwKNvb/ct/2JtrOLnJf76smPC6ej2R4EsKffE7MpT0xVrGQ5EMg7nrunGj4CXbMtcoenGCcCjQDdwgW2Zb2SYx1DgbWCHbZlna7oxG3gYmAIsBy60LbMz2x8x0CmyOcXBTUCN0+Nl2/nE3H2Ldu+J+DoYkTLTSf/VOxo4bL9xjBo+1F/BMiTXUm3r6qW8tslXWQYS2YxAfghscY9/D9wE/Bb4cxZ5fB9Y6/n7D8DNtmXOAeqAS7PIa8ATaUuKPYrqYCKIOYq1VY38+LGVLLj+RdZX+99YBaGSWjp7gNiRWDJqmzs4+7ZX+fFj/pn6siXXL+g3i6u47aXgJ/lLlWwUyETbMhs03RgPHAPcZlvmPcDcTG7WdONA4CzgbvdvAXwSeNxNYgLnZiHPgCfSWKkRyMCmprkvrMfeFv8H4EFWny0ZeHu1usom03mOfDtMib6XTJRooqeW1yQPuaLIbkfCbZpufBg4CnjFtsweTTcmAD0Z3v9n4EpgvPv3PkC9bZmRKG3bgQOykGfAU6TWDMUgZ09TX6Pa3euPevJzZLdpT3O/c76FR/Epn4FCNgrkJzijhU7gc+65s4G30t2o6cbZwG7bMss03fi4ezphvLf4EzV19ZStWpsgaXiUb6rsd66qeq/7fw1lqzLVqalpbXc+1DXrN9O6Z2TW9yeSsxiJl9P7voN497nkGZFxb31fL/qNd97LK88IG6pao8dbtvaZhPKR08u7a52Nubq6unOWs7q5zxPw6/94LXpctWdvwjy95yL3dnR2JX23O6v7olhv3rqTsqG5m/Lq3G0VyjdVRM+Vb6xkSGN1yvt2Njqjv/aOzqTltG7DluhxsdRNSPzeF8yfl684aclYgdiWaQEz4k4/5v5Lx0eAT2u6oQOjgAk4I5JJmm4Mc0chBwL9DKpTJ08qSEFkS7xML1evh9X1TJ82lQXzD/flGWNe2gN0csSc2Rw1Y2JOeRRj2SViwfx58ODmxMd+kWeeC+bPY2p5J+D0cI896gigIq88AVpH74HFuwCYNXMGvLknbzkjvxVg/rw58NRWhg0blnOeW2tbgW0ADB85CmgDYMrkibF5JijjbXtb4ZltjBg+POl7njFtX3jXWT0/e+YMFsw/MCc5vTLMPXQWvFgFwBGHHcyCWVNS3jZ5TzP8dzujRo7ok99TjgBHzJkNz+/s9xvzxof6Hsa3ns0IBE03JuLMeYyLu/RSqvtsy7wauNrN4+PAj23LvEDTjceA83A8sQzg6WzkGeiouDvFR1O7/5v+fOtfy33P04sfZpdk8xLdKTaGyvlZAdiJitH0dN3Tq6mobeU7nzwsbFFyJhs33ouB23G6X62eSxI4JMfn/xR4WNON64F3gHtyzEehKAirdzZEj/3yjvNu1lSMDR0kb9R7smjtB0J/yM84XeYbjtlp2JDSLZhsRiC/Bc6zLfN/+TzQtswlwBL3eDNwfD75DWTau5y5lMHghdXj02Rs0JRiI+hHgEZvDjET3llkXeh6XGxBGb0Us2zZkI0b7zDg+aAEUfRnS42/AfGKmT88W3rRTQMxtQSQqfEPx8/F6y6cLcmUkF/Rg/c090VbCNtjqhCN+12v9M2tlLIqyUaB/AG4VtMNFf4kEQFWugHSWUnJi2tTe8gUC6X4LtZX93drzZZkv9uvgWNtc/gBKAo55/jqxtLcwjaebExYPwT2B67UdKPWe8G2zIN8lUqhKAFKUJfkQW4jkIa2Lp5esSNt7t62O4gRQCTL7XWtlO9q4uR50xKkSf9cbwopZc5KZ2gJz3t4yUaBfCUwKQYCAfZeVCgTRdiMHJY4hlW6NvfHj63khTXpR5dBhIjxElEOp9/8Ci2dPVTccFZyWTL8lqXM/bP3xjzzywwYBtmsA3k5SEEUg5wS+YYC7yn7nmOwpOvc7M40knRu8/IpSfR6IjG8fMk/j3u9eqeE9UdqBaLpxs9sy/yte/zrZOlsy/yF34Ip+vCzgr1dsZe/L93MXy9YwJABMowuJNv2tkWPA/nuS6AxaWzPfH8ab29+R31bipQefCoDr3ILolidDkT+31AJvPKkpBuBeJeDzgxSEEVhuOxfZdQ0d1Lb0sm+47MPj6Loo5R7jvmwbldfmJF0ZZBpH8WbrNOnTapybZlTjSy9l/JxIAh6JFsoUioQ2zK/5Tm+JHhxFInws3qVcF0tPgZRWSarN+nqUy6TxcGMFtKniYyWJJlNkOczNzlQvsNsVqInW23eAVTZlulTt6FECdSN1/+8i21BXCl+T4PJuSHZb01XBplOjnsba7/qe4zHVBbvqrK2ldlXWykn2sG/T76UlUk2Xlgb6Xsngtj306vpxjPA5bZlloZDfwnh6wjEx7wGO6X84WdLriOQTAliUjmY9+NT+Poi68DlSjaLAr8OPAAcjhNRdy7wL+By4GgcZXS73wIWM3tbOlm9oyF9QkVoVNa2UBHQiv7dTf5vNpTtqGZXQzvlu4LfcrWQujIXt9bVOxr6rbSPKcsiVkpNHf4H6CwU2YxAfgUcZltmxC9vo6Yb3wLW25Z5pxtscYPfAhYz59z+Ktv2tjlD3SDXgQyinq7fnHTjEoC05ohcOP3Pr/ieZ7bv+oTfLwKC+X2ZkE/VrE0SWiWX+n72ba+y7/iR2D87JXGeGeRR2MnsvvZiZYY7NRYj2YxAhgCz4s4dBERWGDWTZXj4Usfr0llqFNsIupQ9UQYDyd5PPq+tratvTYYf/a89AYwIFanJpsH/M/CSphv34uwscyBwiXsenP3O3/BXPIXfBNFQr9xWT1llHV/96Gzf81YUB37Vmt9ZfTvueSfOY+ZAfHqWt6pn44WVS/6DlWxWov9R041VwOeB44Aq4FLbMp91r/8b+HcgUg56irumnnO7s8VpMSuQ+tbwg/WVMskby+zqpjcKbTKlUcyj0eKVLByyMjm5yuLZgGQpbVQ03rwYBD8xI0qtHPxaTBeIF1bMsU+uwaX2ggImm3Ugw4FrgQtx9kbfCdwP/Na2zJLq3j1ib+WnT7zL+uvPZMQwf6PTBxEULt86+0TZdq54bCXrfnNG9FyxbZdbWduaPlGWPGJvjR4HHazPL65+8t2c7/3iXW8gu9p5JJC9sXOrhbk03P419p5QJkHs3ZKHnEX2+eVMNiOQP+LsHngZUAkcDPwcmIAT6r1k+MOz5YBEliBjAAAgAElEQVQT02fqOH/DeRTj4rKbXlgPOBsKFZ90wRF5z0DxeQ0EwJub9waWd/J1IHk0okleShAjEEUwZKNAPg8cY1tmZC+Qck03lgMrKTEFEkhbotx4iw5v45bN69nV0M6E0cMYM8L5PNo6e6htLV1ffT9IVgVTVc2d9W10dCcPUJHsnQQSyiSDNJlUEb9GNanKpZTIRoEkK9+05a7pxijgFWCk+8zHbcu8TtON2cDDwBRgOXBhqZnDFMVLXWtf1Nhs1PsJv1/E+w6YwH+/eyIAX7lnGWWVdVSccLTPEpYOuaxE//ANL6XMM9k7CaLDNMonU7Vfor2yfo9POYVLNqX6GPAfTTdO13RjnqYbZ+B4XT2Wwb0dwCdtyzwGOBY4Q9ONE3C2yb3Ztsw5QB1waXbi50ep9OwDiYXle47FTbZzPqt3NEaPyyrr/BZHEUcQE97ebEYNT7whVjIZFJmRjQK5EngRJ1xJGXAbsBj4SbobbcuUtmVGNmYe7v6TwCeBx93zJnBuFvLkTJATWGWVdbyxqTZ9wgLR2ytj9mGob818LwdFcbJ0w56Cr15OHkwxMebrFekzTWbCcjNt6+zhH69uoTdHV69sQqJU1LSwcNXOtOli1pbkItQAI92GUp+MO7XE/ecNpvhRIPVY1clrKI7iOQxHCW0C6m3LjBiXtwMHxN9XU1dP2aq18afzoqvbWQG7as16Jo3OfvF8+abKmL/LVq1lZ7Uzgbl0Qw1LN9TwxJeTBS/OnvJNlQxr3p3TfW9sbY7+/e66jdHjlWvWM35k+l5ZNuT6nhKVZ755xrNidd+EeqZ5xqdLdZ/fdTRVnhc+6Kyl8NaxTMssVzkr6hKv8m5obE6Y53XPvJc2z1Vr+iIf1db1xZTbXrWbslVd/N2u4dkNjXQ01nL8gWMzktMry0Ov9r3zdRu30F03KmE6gPMf3kz8tESi31W+ua+urlhdzujh/npx+vUNASwIxBsvlnSt5z1JzsdH5U3bWtqW2QMcq+nGJOApINGv66fUp06e5HtBDH9mO9DD/CMPz3lTpQXz54H7IS+YP4+Xd5UD9bHX88XNf84hB7Pg0H1yymJL13jAUT5HH3EYPL0NgGOOPJzJY0fkLyPElEPOLOtbYBZftvnKBXDs++bCYxWZ5Rn/bO/fnjy9+CVnRnkmkCfZsV9yjt7ZCP/b0e/8hPFjY/NM8txEzJ83B55yXK33mTwRKp2glzOm7cuC+XO4c8XbQCOzDzqABe+bnjqzBL999LjxgBNocu5hszl25qSk9ao7gdyJyvHwQw6CRVUAHHPU4YwfNTzj35tIXoD9J4xil7v1bz71qBAKI550G0r5vrTYtsx6TTeWACcAkzTdGOaOQg7EWVtSMIrR5fb+Nyooq6zjz198vy/5JfV8GCCTID9+bCVHzZjAJR9JXVWDXt38o0dXMP+AiVycRg4/OfWmlwv2rCBI59kV8VQaOSx2pLy4fDd3LN7II9/4UMptmVOZsDq7e31fA5aIXQ3tfOWeZfzzq8czY9LohGmKsR3KlOBLENB0Y1935IGmG6OBU4C1OHMo57nJDODpQsgTyBSyTy3yz59+j3+viNWjpVzBgubxsu386j9rwhaDJ5fv4JcFlmPD7ub0iXwiWR3MJfR62me5Wfa4cx/DhsZ+W9978B3sijqaO9O4VsfEwoqVc+veHEP8Z/lzH317Gxt3N/PQW1uTpikVZ55EFESBANOBxW4sLRt4wbbM/wI/BX6k6cZGYB+Sm8yKmo7unpwn+oIm7JFGV08vnQXyee/o7ok2OvEU59spHQJZyZ3MNdintxWIcktynNG9UtLuiUCcis7uXrr92hs+QAoSft22zFVAP5uMbZmbcVa3F5Roo+pT/Zp7rQoPlowT/7CYXY3tBdmvYu61z3LinKncf+kHA3+Woj8d3Zk1jhG8isIbij3S7uerSIJQINniFeGOJZu48blyyq6N3bMkkZSHX/s/Dpoyhleu/ESwAuZJoUYgRUXJmf99ClgXc75ApRCZHCwUSzfUFPR5g4VkbXGvp5Pc1pmlAvHkudPjah4xN0Wu+1FXA1ndnkWmAnjGNU3H72SZLJ+te/2PD+c3g1KBDDRqmjt4a0viOEilEkQwaHLdbCioNT3rq5vY6OMcxqK11dHj59/b5Vu+2ZBPhz+RaSiqQDxVuKyyLroFbFlFHbvjOiivb+zrQBTS7JYJkd/RP4/wR0q5MqgVSKm8tnRyfvaO1/nCndnt5TXYJubP+ctrWd/T3dPLl/7+ZgDSwGk3v8IpPnpRXWq+HT3+xv1lvuUbIflCwtzrkfdObzcnYnqK5O299rm/vh49vuQ+G/3WpTF5fvnuZZ58PM/ybXF7/hnF5xG78VVpfZeDUoGEPbHsN6Uw1M2GID6i5o7sgyGW1qccLLnEwkqfpzfYZd9HmY0/Sk1z8tB5gTfGWWYf+Y3xYpVyPRuUCqSuxQnnkalHRNgUY6dk1fZ6bnq+PH3CHMj39171xKqs7fHgrC9IFYKjK0evGCkl1/93ja8mq0Lxn5U7eaJse9JGbtmWvTxqO4tT/aqmid5/VUMb1/47u71S8pXnqidW5ZlDZjS3l26k50GpQDrdhuCpd/qvrFVkxqf/8hq3vrQxfcIcyPfDf9jeltLvPhmX3GvHhOCIH6gu3ZBbBNXtdW3c/eoWLrnvrZzuD5PvPvQOVzy2MmVv/socG1pvluNH9TmEHn3AxNjrAq58fBX/ejO7dxorc/a16mFXMcbmmXU2aen0dEyKsbOYikGpQAYTSW3XJVZRs6U9S5fSTOjoys8vf6CXuV8mo6Fuq9SnP0ROa4mCWJqVbdRgb5oBZjkHBrkCKbYPetOexCaOXCfunnyvnh8+sjIfkULB2xDNumohy7dmH069Pc/GPmGeeSqlRPWtoYiiI6/YVs+sqxaytqqRDdVNzLpqYfRaJjUw21p64h8XR48TNq4eL6xUazq2JZkDHOVzoMO8ECKFF1bpUpCFhMVKsb3H1zb6u4bhwZXBbXEaJPHvxVpVxXEHTc4ujwBDbPhJZa4hNQLgf6udIIFLyvf0ixMVdKPnnUSPf5YAulMMJ96uTFzPZ04ekzRPP8gqTykzct4ptjYpHUWkogtPqlABG3c3F80ke66Vv1QqY/x2sfG/tyeHAvCjwQiq/F5c07dmIxM51+xsjIbKWberMU3q/Hlzcy3b6+J79cHWJm/jGl0H4nlmshA1ABuqE4/cG9r6Rnfv7Wzs16loaOti295W1lZlXqZ+dEyaOopn1Jkvg3oEcseSTVx5xhH9zrd19nDKTS9z+lHTuPPCDxRMnkLaSIshzEOEb/w7dnI03mRXrHHGcqGxvYuv/bNvzUa6X7Z8ax2fveN1fnrGEZx+1DTO+PPSNHfkTmTR6cvr9/ByDluu5lOlDpw8hne2Jt4kSwiRUoHcsWRTwvOPlW2PHl/3zHtx2xcIzr5tKdv2tvW/MQU5/0QhouX75b8vS5rMUVClM1syqEcgyYhM2BV8Z8EkY9wgms9ibpP9GIEUK/Huxel6tDvqnAZu9c6GlGsegiboVzBjUt9mT9FYWD4vBIx1o5ZZK494shVpoK0/g0GkQJo7url98caEPZnItfiebqIKcuNz67hveXaKpaqhjfte2wLAjvo2/vlGRb809a2d/M3Tk/LKEoQ9P+wRyGsbazJ2i81F2f03g+1J03HXK7GbCSVy68yEVA1HRlu/+khlbfI5l1RypnsFF9/7Fne+nHgkkC0PLKtk297WPi8snxreMNpv72c2APXH4DFh/c5ay4PLtjJ7av+tMb3X9KOnp3zTty92PpLbsnj2V+97m7VVjZz+vv256J5lbNrTwllHT2efcX27IV7z1Lsxe5e/tC77LWyzIWwFcoEbciKTKL25KNCK2vxX59/4XOxCyWTxxjIl0e+I3/ul3z15PbE/n73jdcp+fmrW96V7BUvK97CkPLd1Ms4D+g5f31TLF+58I7oBU1E1vDmGHcn0N5TaWHvQjECa3NWeiVYTt7hhLoLat6Kh1TE99PTK6MRefK+6KW41aq6rnlMxdEhyT5dcKYS3U6lbsFJ5GGWch0+y1LXmZgYrdIym+taumGcWSxXI1aVewoC0YQ0aBWK967goht0YxT+/qb2LWVct7BeGfMW2xBOKEe5eupmv3J14Mq61s5sP/u7FfueHeBsy9//bF2/kknszXyF98wvr+YZnEtiLX41M/Efa2dPL5Q+U8afn/Amdov32xRgPHYDzswxGmYzTbn6Zp1fERjiIlMvOhnbO+9vriW4rGCKuEdta28qxv36erbWtofb0dzbERtVt6+qJxnjbUd9WckEGE5FJ+Zbazxw0JqzI3EexuOZGvuNV2xsSXr/TY39PVKeuX7g2ad7lu5qobswsfHm8mSYdtyzakFX6XIj/iPY0dUQV7I9Pn5t3/nuaOlixrZ6TDt83em5ZnuapCOurm/n+wys459gDEl7fXpffxK3fPL58O/WtXTz5zvaU6YJu1xLNWUWcBvwKOeT3ACCbMhEBPL8YGDQjkAipJmT7DU/z+Gp6eyX1GZgLMqpTgSyCSp1pZ3cvTe3p/dX99pSB/j+3u6d/xh3dPTHy7W0Jz0MpHfG9/kzJpPyzJZk7bF1LJ3UpVsXXBVy+w4cE3xTFjjpzeye51vFUbshe6ts6S8ptvSAjEE03ZgL/BPYHeoG7bMu8RdONKcAjwCygAviCbZnZx63Ign8n6M3EVyU/ego3Pl/OX5dsYsUvEk9YBjlUTdZgZdPYf+nvb1JWWVeQrWjjueXF9TF/J3LjPf/ON2PMfMf95oXA5So0R//yeW754rHBPsQtW/ONypTJvvXA8kDFOHifMWxIEq3Yr477va9V5J1Hth2mSJK/LN7IvOkT0qY//reL+PYnDs1NuBAo1AikG7jCtsx5wAnAtzXdOBK4ClhkW+YcYJH7d6C8VdFnqojEygmiLY/MuaTq1WWKX5s/ZZNPWWX2etyvcnz07VhzSqIeWbo5omJiAFoufOf9B01Kem1IILafwvfyMzWfP7s6nB0lc6EgCsS2zCrbMpe7x03AWuAA4BzAdJOZwLmFkCdCuh5EV28v/35nRyATeEJAbXMHi3x01/3vqp20dHQXdMIx3yclsn3HD/fjRyB+xQx7Y1MtW31w9w2SXM1fqUgVwics4jsNXoLQH0F9Iuurm2I6N17RB6Irb8En0TXdmAW8H1gGTLMtswocJaPpxn7x6Wvq6ilblXzCOB+klJStWktdvRMLZ8vWnZQNbaKl0/nA2rt6+cEjK6jYtpMTZ42LuTedTB0djs149bpNdHY5o5B3122kq9tx1121ZgO/XVLFpr3pbcsbt2xnYmfiSV6vHN958B1OmjWOGROGJ0y7ak3f/h2r1m1k97i+dMl+T7rf6b1etmptjKtwJvl858F3+p0bMwyaPT4Ajc19E89lq9ZywYOb+92TLRs2b+X6JU5P74kvH5J3fvF4f29NS+4bBm2udEyudfWNlG+qyFcsAH79+DLOmef0+HfuLv6Amw2NzbS2+Tsf9N763OrQxoq+xaQr16xn8ujYJvRzbt2M1Kmd1X3l296R2TxSe3tfukzbvvJN/U2QC+bPy+jefCioAtF0YxzwBPAD2zIbNd1Ie8/UyZP8KYgEjY4QggXz5zFlTTvQzOyDZrBg/oE0tnfB4xXRdBP3mcqC+bNj8lkwf17CPCOMGDEC6OboIw5lxNI9QA9HH3EYw16sho5O5h85h90LM/MumTN7JguOiNOtSeRoFyMYO2Ei0N8EdfS8w+BpJ+7U++YeysH7jI3NJ1n+Cc5HWDB/HjzsrLI/7ugjGDZ0SML06fLxMm7MSHZ7Gt2xY0bB3o6+fHxQIIcfchC4CsSvPL14f+/O+rZouWfL7INmwOu7mTJ5InMPPRherMpbtlHj+76pl3eVA8VtDpw0cTyN3a3Q4J8SOerwQ2Bhas+zRBxy8IGAEwxz/pFz2G/8qNgEcfX95er1sNop31GjRkBT+t8wamRfumzavkIojHgKpkA03RiOozwesC3zSfd0taYb093Rx3Qg2OXXGRLfh77hf+uYPXUsHzlsavTcZfeXZZaXJ7Of/3t11FvoikdX0pTpPt1ZDOHtir1JXVK9Q+NkQ/jK2hb+9HzsJPa/39nBqu0NVDX0d0ENYrHX5j2x4TaSuTrnw+LyYKtaT6/kJ4+t5LBp49iYJFpsJkQ80Db5uB3uMyt2srW2lT+cN79kzCV+zQPmyzc83/0Vj67k6jPnceSMCVTUtPCnBFs8excnx9frZHT1Fp+JMRmF8sISwD3AWtsyb/JcegYwgBvc/58uhDwRMq2SHd29XHyvzcPfOCF67tn3sp/oWuwJ9ZBNtNNU+iN+viOlm3IGht+rn3yX1+OCSP7gkRVp7ys1/PDIScWWmmae9GH9wuqdjvJck0XI8XTsamzn2fd2cWyKiWtFepZuqGHb3jKW/OQTXPNU/+/GSZN9eJd8gzwWkkKNQD4CXAi8q+lGpDW6BkdxPKrpxqXAVuDzBZInJ4rRmyZXl/Eg+nOltoo2WPypLSLAWldK76tYZY2IlcxTLBgPsuKhIArEtsxXSf5FnRzUc71bciYimUDJ6ur5d72Z8bP9HHJHPHFuX7yRG58rZ/31Z0avZRMUMdaH3S/XYEUikm2zmi1Btj9hB9QMk1NvfsWXfKSEHz26glfjPANnXbWQZ39wIkOSOJUMFAbdSnQv8Z+Pn99TJC8/epCRHP7mhsv27ilRTI1Asdipi4Eg5m0UxcmTyxObKvON3lwKDGoFkggpJXaRvfhILzQasde7/afPJqz4/FZmuWBv1fb6pAum9jR1sGmPf5PBxcyuRn/s2P23lvWPldvqA4tA7Tel2DWpbmxnywCv74MmmGKmPLNyJ99/uLgmjVONYrIZgdieVfiZ3nbO7a+lvF5V3xdFtba5k0//5TXOmj+d2798XL+0H/r9Irp7ZSjhUQrNQ2/ltvlUPM+917d/ut/mrOc9e7MrciPV6vLI3kEDGTUCIXa1b0WNvz0+IfzvPXkbkmwm0atiQmYnvjHbRqrRE/Av8jEtTxIGpbuEgsQVI0VkrVS4+FGnP+pZHlBqKAUSEH5+7Lcu2kB1Y1/j723jn1ye+WKolhTrTu57bQvlu5qylm1PU9+S8eHuIsKquL0dFP7wOyuYiAzFjqDwG1plih9RoOMn4EsJpUDiKMaJ4Lcq9vK9h/qH/AD4xdPvZZyPSDF38sv/rEG/dWnWst2+uC88ygD3WAydUgog6SefOmZGEX6VClAKpGRo7cx/IyzvXEqiD7KnV2Y9cvL2wIq0k6gocaaMHRG2CIokqEl0D1LCSz5Fx91R73jh+GXOyXRDmlQMycB7643N/VfTpmJzTV94hhP/uDgXsUIn3XohRbhckGTrZkX4qBEIsXMKfvvvv7zeH4XkS+de2ZgUCoWPDGoFUojmdFdDhy+jB6+sfiiTRIERC8XuxtxHZcW8da1CMdgY3Aok0iq7/wdhwn9i+XZ2ezyVcsUbTC/XuQavErr4XtsJMx4Cx/9uUc73DsStaxWKUmVQK5AIkcnlYnUV9It4C9YeHxSbQqEYvAxqBdLe1cvqHX1zHqWiPh56K7fNiSKxtCLUtigFolAocmdQKxCAs297ta9nXiIa5Ib/rcvpvvau2LhHl5pv+yGOQqEYpAx6BQLFuc9HIRjgFjuFQhEwah0IUNPsmHKKcRV6qXLeX19n3ChVvRSKfGjp6GbsyOL9jtQIhL6tZlWP3D/erqxjSXn223kqFIo+lm4o7jhZSoF4UPojOLp7SmPfCYWiuCjuVqkgYyNNN/4BnA3sti3zfe65KcAjwCygAviCbZmJ44AXiL8uGfjx+8PisJ/9L2wRFAqFzxRqBHIfcEbcuauARbZlzgEWuX+Hylaf9rFWKBQKPyh2s3pBFIhtma8A8fvEngOY7rEJnFsIWRQKhULhD2FO70+zLbMKwLbMKk039kuUqKaunrJVg3MjHYVCMbjZVLmdMpl+H5jyTZX9zi2YPy8IkWIoXv8wl6mTJ+VeEA9u9lcYhUKhKCCHHnwgC46enlHaQiiMeML0wqrWdGM6gPu/P3HPXZTXj0KhKHXWeoKoFiNhKpBnAMM9NoCn/cy8lPcZVigUCoBbX9qYPlGIFMqN9yHg48BUTTe2A9cBNwCParpxKbAV+Lyfzyx27wWFQqEodQqiQGzL/FKSSycX4vkKhUKh8J+BuxJ9sEZIVCgUvrPoipPCFqEoGbgKRKFQADD/wIlhi1DSnHbkNCaPGRG2GEXJgFUgagCiUDiI+K0oFVmjSjAxA1aBKBQKhyAav79f9IEAci1elA5OzIBVIKrXpVA4BPEpjBo+YJuOhAg1BknIgK0F6nUrFA5DAtAgg8lNXghUg5KEAatAFAqFQxBtXxD646ApYwLI1R+8OnjoEKVNIigFolAMcIIwYckAhiDji3QL5Ofeq45Rwj29g2j4lYYBq0AKMQXyqWNmBP8QRdFRatNrQdjv85lj/JmeOOjfX758XM55Bo339xbzSKnQDFgFUghOmZcwAr2iSJk4ergv+YwcVlqfTRAKL58sP3FE4u9mv/Ej88g1WLy/1696NBAorS9BociDXp9MD+1dpRXpudhGTHtbOhOe92tuYe608b7k48VbhnOmjfM9/yBkLgQDVoEot7vEzJwyOmwRQqOnSF2HfnDKnOjxKfOm+Z5/EN9CPp5de1s6Ep4fNXxoznl6uedi/9eoeMvwgg8e5Hv+vzn3fb7nWQgGrgJR+iMhJ8zeJ2wRQqO1s8fX/A6c7I8yPuN9+0ePv/CBA33J08uQAL7y/AYLwX6c40f6b2LytidBrDEbPrQ0G6wBq0AKwftnTg5bhKz5ZBL7czGw4ODSKs/hQ/35fFo6+hTbs6t3+ZKnl8+833+ldFgeZpyjZkzwUZIEBOJ11nf83k7/N3nqLdLRcToGrAIpxPs4aJ/S88Y4rkgb6Q/OnsLXPjo7bDGywq+OaJdn98xaz/zAdZ860pf8PzF3X1/yqbjhrOjxfuNH5ZzPAZOCNaN6R0dembPl/z5/TMLzTe1dOefp5bHLPhQ9LlXP4AGrQBSJKVbTXq+U1LX682EWCr9WeHs7O15lMsInb6/uImudhgS8EM8vE1On511Iz9JJv+aUvPWnVNeWDFgFMq5IFyWlw+uNcUwAYbiDCGvxRW1m3nn0SrjzlU0+SJMYvxapnXDIlOixX+2gN5/lW+uix8fOnJRznn/y9J73HRese+ykMX1zDtmGjr/5/MS9/HwYluWL+cz7D0h43qvMR7sT/HP2G+dbJ8ybTzIT1i1fPNafhwXEgFUgh+2XmY122oTi8j1/7ocfix7/6hx/PDP+4fFKCUKB+GHK6+mVDM1Rto8eNjXheW9DcvysKQnTZMLD3ziBCSOdT8XbMPvVEx2WZC5l5LDcvZLOW9A375Gsx3/TF/xpvL3l/8DXPpjVvdnOz+w/IbHpzOu9lu3cVLJ5wa4ez6hDCCpuOIsXfnSSbx2HcSP7OjXJTO7nHJtYuRULoXfTNd04A7gFGArcbVvmDYV8/mH7jaO6MbFbYdiMG+mPW6N3SB+E9WB7XVveeazYVs8h+47N6d6D9hkDG1OnyWdE2tsr6XY7o14F7JcunuCRbZ+xI9lR75Rntj3psBjhabD9cixIxoGTR7Orsb3f+USxqmZPzaw+JVt/4h2BeNl/oj9zON665FUmpUSoIxBNN4YCtwNnAkcCX9J0w5eZw1Sf3h8/Nz96fMcFC9LmdfQB2Q3Lf/uZ9COHE+f09drmJBktHbbfeD7z/gP44SmHZ/X8fgRgXr32rL5wFPaWvb7kmegjWvzjj6e976sf6Zt8P8Zj9hk5bAiXuhPzs/bpa0yevPzD0eNk5gsvvbJvHsFrqx46RLD212cwZsRQVl53WvT8ZScdGj327ptx25fenzD/Q/bte//ekcPILEOm//n89OaOK07tq0vJer1netyKv/2JQxMn8jDM44KabC3H856RNcBHDx7LlWfM7Zfu8cs+xNIrP8FPTu9/DeC6Tx0VPfY6XcR/7w9+7YM8+s0PxZzz1tkII4YOiVEgXjnbXLfvLx0fu+7j08fM4P0HTeKfXz0+oYyp8NY373OPmTmJk4/YL8Zkde6xxR8qKWwT1vHARtsyN9uW2Qk8DJzjR8apeocfP6LPKyWTsASfzjLm1T5jE29/6fWG8S5G+vnZyXXmzecfy/c9C81ywTuJ6tdk3X4eU4JfLoiJzGuz9hnD+DS9M6/iOcmjmIUQ0WteCY87qM8T7bQj0y/ck0gmjXIaRu9vHTpEMHrEUNb8+oyYenTS4X3v+VRP/slip8X/6qnjnPozLMsFHOdmoAwne+pmsrd2/Ow+c99PTj8ibZ7JTHBeDt03tpP0w49M4/KPH9Yv3QdmTWHmlDFJTVXDh/WVlrc846vOhw+byr5xoVFGj3De4ZeO75uzGz5UxIz0Imt7Rg0fQnuXo0ASxb566vKP8DHPex6d4SJI73xRxGQbeeY9F2sxJqsZAXur+UHY46YDgG2ev7cDMUbUmrp6ylatzTrjVJ4n69c7k7Uzxg9PmfeY4UNo7eplXHdDwutlq9Yyapigs0fy8dnjeWlzEwDtdbsTpn/fFFgMLJgxhs76vjRNNVUxeSY6/uQhfflH5MqUtr19awvWrU9j60nBfmOHsbulm1mTRtDTsCd6/mMzR7FpTwsAsyePYEtdJwdNGsHW+sQhKyIcNmUkXb2SyvpOZkwYjrb/MFZsA+2AMYwfOYSXNjez/N11nDFnHI+trk+az8aNm6KyTZLN0fNnzhkX/XtSbxMfmjmWN7a1ULZqLUOEM7LoqE/8rrzUVe/kqIk97G6Bii1b+OCBY1i2vRVt2rCE9ad+9w6O2X80e1q6k75P6Huny99dG5V/Cs2ccMBo/lveyYYN2b2r+HCy4wIAABeLSURBVGfN3380q3a1UbZqLZ84ZByLNzczvM0zWmyuSZjPyHanrEcNE/3ynDByCI0dvZStWssR+45k3Z4OZo7siEkTz9lzJ/DOu7H5lG+qjP49dcxQalp7Yu6VzYnNyju3bo0e797R13TMmyh5Djhyv1FJv+nhbY6DwvThHbx/+mjeqWrjxIPH0r63Oprm3TXrAThp1jgm49TpCT2NSfPUD5+Atb6Rs+aOx97eSqVb5w+eNCJ6HOHoaaM5YLhjfjtgwnAqK7YAcPz0kTH5Tx8/nKqmLvYd0ppx2+ctzwgL5icOWukrUsrQ/n3gzIs+/4EzL7rb8/eFHzjzotu8ae68/0mZK83tXXJnfavs6OqRTe1dsr2rW+5papdSStnW2S07unqklFLube6QLR1dsqGtU1bWtMi9zR2ypqlddnT1yLbObimllFX1bbK2uUPWt3TKha+tlM3tXdF82jq7ZXdPr6xv6ZStHU766sY22dDWKTu6euTbFXuj+VTWtMje3l4ppZQbqpv60je0ReVpbu+Se5s7Yn5Lb2+v3FDdJLt7emVvb698a0utbGjrlHUtHXLNzga5p6ldtnR0yQ3VTbKlo0vWNnfIp5euiOa5q6FNdnU7xzvrW2V9a6fc29why3c1ytYO5zes2Fond7ly7Gpoky0dXbKts1u+XVEre3t7XRkaZU+PI//W2hbZ0tEV/S1d3T2yt7dXlu9qlL29vbKpvUu+tK46+rw1OxtkZU2LbGzrlGWVe2Vvb6/s6emVT72yIlomO+tbZU9Pr+zu6Y2WcU9Pr9zb3CHbOrtle1e3rKxpkU3tXbKr23mvUkrZ3dMrq+rbpJRSdnX3yA3VTdGya2jrjJ6P5NnV3SO31rbEpG9sc8pk427nvdS1OMdSSvnWiveiz+rt7ZU761v71beGtk5ZUdMcrReR9I1tnbLGrXetHd2yuqFNtnY4dabJ8xsjeXrP723ukDvrW6N1ua6lQza1d8mWji65ZU+zbGrvktWNbdH38GrZ6mjd6ezuiZ73lufuxnbZ3tUdfYd1LU7ZVje0Re/dXtcqO936UuuWvZRStnd1R487u3ui9XdDdWP0fGtHd/RfXUuH7Hbrizeft1euiZabN8/48oxc27S7KSqPt95VN/Z9NzvrW6P1yEtNU3s0f29dqG5si8pWVd933NzeFT1+2V7dL794KmucetTb2yvf2Vonm9q7ZI9bH+tbOmVPj/PdxNdxKWU0rRdvXcgUb3l6CLwND1uBfOgDZ170nOfvqz9w5kVXe9Pko0CCIsnLKjqUnP5RCjJKqeT0mxKXM/A2PGwTlg3M0XRjNrAD+CLw5XBFUigUCkUmhDqJbltmN/Ad4DlgLfCobZnvhSmTQqFQKDIj7BEItmVagBW2HAqFQqHIjrDdeBUKhUJRoigFolAoFIqcUApEoVAoFDmhFIhCoVAockJIn8JQBIWmG3fjrFBXKBQKReZU2JZ5X5APKHoFolAoFIriRJmwFAqFQpETSoEoFAqFIieUAlEoFApFTigFoihZNN0ojS37FIoiJd9vSCkQRVqKuKGeELYAAwlNN3LbUzhEirhulgpT0ydJjvLCKiCabswHWoChtmWuD1ueZGi6cTxO49xhW+bSsOVJhKYbpwNfAy63LXNPuvRhoemGBgwHumzLtMOWJxmabpwCnAX8xrZMf/YoDgBNN44B2gFsyywPWZykaLpxFNAKCNsyN4ctTyI03TgTeBLQbctcnEseagRSIDTdOANny96LgIc13bgkZJES4sppAh8GntV04+SQReqHphsfB/4G3F3kyuN04D/Ap4FHNd34lqYb49LcVnDcd/wPwCpy5XEm8F/gu8ATmm5cFLJICXG/oQeBHwG3arqReIP3EHFl/A3wNLBA040hmm5krQ+UAikAmm5MBa4Dvmtb5nXAlcA9xaZE3BHSzcC3bMv8NfBrYLimGweGK1k/jgBusC3zOU039td040Oabnw0bKEiaLohNN0YCVwAfMe2zKuAzwOfA76h6UbRbHbtNhofAa61LfMFTTf21XRjrtvTLwrc8hwHfA9nxPkd4DLgOk03vh6udLFouvER4EbgcuAaoBLo1nQj8SbvIaDpxknADThbafwfcB4w0bbM3mxNgkqBBIjnZbQAa4B1ALZlvgg8BVyv6cb5IYkXxSOnBL5iW+YSTTdmANfibPL137A/1LiK3Y3Ta5qFsxXAl4EHNd34URiyedF0Q9iWKW3L7ADKgfmaboyzLfNt4IfApwAjVCHpK0/bMnuBRmCG21F4HkfOF8J+5xBTns3AcmC8phvDbct8FUdBX6PpxlfClTKmfh6E02l4DRiD03H4BfB3TTc+HZZ8cRwCfNO2zDdds+p64GZNN4balpnVnIZSIMEyFsC2zDagB/g/TTfO1HTjFuBd4GLgfE03JoY8GTgawLbMd23LLNN0YwTwSeAHtmVeDHwTR/YPhiijd4J3MY4S+Qpwv22Z3wXOBi7XdOO0MITz4B1dvAHsBxyi6cYw2zLfBX4K/ETTjaNDka6PkZ7j94DDcXqif7ct8zIcs9vvNN04IQzhPHj3LNoKnAqMArAt802cb+gHbmciTCIyPWRb5suuQ8JPgV8BP8GZa/i5phsHhygjALZl3mtb5jJNNyJlewtO+zQDoqPSjFAKJCBce+1jmm78TtONC23L/AawGvgYTiNzA/Aa0AC0Zqv5fZTzNOCfmm7coOnGhQC2ZXYCT9mWeY/bA1yGMy/SG5KMkbK8XtONy2zL3ARsAT4LTNN0Y6xtmauAx3F6faEQV5bn25b5Ek7v/nvAUa6cb+HswBnat+fOzdyl6cbVmm6cbFvmCzgTvt/BMbcMdxvnfwFDQ5TzFOA2TTd+runGcbZl3gmMA+7QdGOCq5RfBlbhjJ7DkvN04E5NN67RdEMHsC2zBbjJtszbbcvcDTyLY4VoD0nGD2m6sa97PMyVsdu9vA44EKejGBmVZoRSIAHg2o/vBO7AURqnaLpxr22Z19uWeTWOHbcdp8c3E+ejCEPOM4DbgIeAPcDxmm4cDtEPANsypaYbXwJOBKpDkNFblmuAEzTduM+2zBuB+3F6+N/VdOO7wPk4I7uCk6AsT9J0Y3/bMq/EUSLfBH6t6cYPgHOA+pDk1IB/As/gdGTO13TjOndewcLp4HxK043LcLyydoQk55nA7cBSnMbtIgDbMj/vyn0zcImmG5cDJ+H0oMOQ01ueo4CzNd24yZV1u6c3fzbOKC8MGU/D6ay+p+nGDNsyuzXdGOpeE+63/n3gDPf3ZIxSIMHQATxjW+Z/gMdwvEaGa7rxKDiaX9ONc3Am1n9kW2ZdoQXUdGM8cClwtW2ZTwB3AYcCH/WkmaDphoEzGXiBbZlbCy0n/cvye8AITTf+YVvmzcDdQB2O7Lo7OikoScpyFo4ZCNsyfwQ8gdMYzwVOtS2zstByuowA7rMt83Hgj8BfgNmabvzctszv4cyBzMZRJOfalllRaAE13ZiCMw9zpW2ZDwA/Az6m6cZ5ALZlnodjHpwOnAx82rbMsCJ2x5fn33DmaW6MJHA7DdcAX7Mts6CdMNdh41TgTByl+5amGwfYltnjjuCkq+RqcEZJFdnkr9aBBICmG0fgmFMucyf70HRjInAT8Jptmf9we9a1IVZ83NFGK1DlVqgfAGNsy/ydJ83JwGbbMreEJGOysrwFWGRb5v3uuWGeIXkYcqYtSzdd2HJqwKPAee581zDgKODbwL22Zb7hphvpOgKEJed8HIXb4Ha4bgDW2pZpxqULW85k5flN4DHbMhdrunEV8G/bMteFJONMoNm2zDpNN36HM5r7kG2Z2+LSjXbnazNGjUACwK0ofwTu80w8twBvAge4aVaGqTxcGdbblrndtszI8L8TpyePphuf0XTjbNsyF4WlPFwZk5Xlazi9/Ei60Bpl9/npyvI893woppYIrtfNH4EbNN042i23jUAT4J0w7wxDvgi2Za6yLbPW817bgIPBMRdquvEx93zYciYrzzbg/W6aG8JSHu7zt+GaTG3LvAbH9BvpKHxM043PuUmznp9RCsRnNMdnXdiW+U8cf/CHNd34hFuxhgPHaroxMmSvqxg83hh1wHZNN04Ffg6sLbAcIv7vYizLVM9LUZbLwZlTCl7CqCzJ5LwfZyL/Fk03PujawLcBczwTrKHImaAORMqzHah355puwFlfUezleZimG8MLWT+TPcs1VUXe7dWurL04Cx5XRdJk+zylQHzA+9LclzDEPb4Tx2b/J003/gFcAfzCtsyOMLyuEjXQ7mHE9XQzju35F8BFIcwnDIv7W1CcZRkjp+as4k1XlmGEs/C66kbdM21nTYUJ3AM8pOnGHTiLW/8S0kguKmfEJu8pz8i19cCPgauAC0OaQ9oH+n9Hacqzq8D1s5+MnuPhnnRrgFrgNNsyN+T6MDUHkgea4yO/2bbM3W5PWXr+/zCOt9VXNN04BMd00ROG2SqNnCfgrJr9Ds4K7yXAcYUecrtzLRfhuBS+Z1vmM55rxVSWqeQsirJ0ZTkV+BawAlhjW+bjmm4MsZ3VxhqOzf6nWt+K8/owGuU0ch6P46p9LXAGzlxDWOWp4XiEfc62zIVuozzEne8qivJMI+PxOJEQfoujSK7BmfzPy2tRKZAc0Rwf9eeBlcDptuPrHbl2JI7XzY9ty1wYkogRWTKR8wrbMi333ATbMhsLLGPEQ+QPOPMak4AbbccN8iicSfRiKMtM5Ay1LN3nno5j8vsDjtfXCNsJpxIJ8rcEpxf/bKFl85KBnItx5HzOPbePbZm1Icl6Gk68sDE4Dh2Pug30fGARTgSHsMszlYwv4nhSPu+mHWE7673yQpmwckDTjTE4wQbPBV4AntJ0Yz9Pkq3AxZ5eQChkIaeluX7hOJOphZJPaE6csO/iuDPfC/wVOBaI9OQqCbkss5QzlLL0yLkv8A2cKAIP4CgLTdONz7sN9gbgbNsynw25PDOR81O2E+8sEnYlFOXh8hpO8MFPA3drTjyp0TjzhOeGWZ4eUsn4Gdsyn/eYMX1xPlAjkBzRdGM2UG1bZqumG7fjNCafsy1zV1w6EcZ8h+f5RS+nO/TeAey2HZfNX7nHtxeLjO7zS0XO6bZlVrmdhf8Br+NM6mrAC7Zl3hW2jNnICYWdLE8gp8BZJLgQJ47Zfvx/e2cfY0dVxuFnYQstpaktRhvENkEFVFA+eqjBaE3Ehp5Wo0Bra0oPNg2QiAh+BUKMlViRQLWgEJQ0MDEhVK2RWCckavwgCuGY0mgaQyIJ8mUbICAtNGC76x/vue712nYvN3fvzLnze5Kb7J2Z3T53ZzvvnDnveV/4A3ZxnoctHB0Bxiv8P9SVY3wDq8y7oXPSUhwBZ7np87E/9GdaUTyWxefSxNk24IPOh+XAzFgWWyuaLK+9Z3JcgN01PZouyK07uAPYYjaclYZ4LVo6cVW/y5w8/4RlgAH8G7g+3R2PAp/FLiaVXZAz83w7lnr/WiyLfc6H+7GabE9gabEHgPdHKwVT1Tmv1FEjkC5xtnL8ViBik1B/Bu5tz65xPmzEhuWvYPMNA294k4PnZI7Oh8uwO6ddwI3AiljNiuicPbd2Ztc4H76MTe5fDoxVcNOQs+cW4HRs5f5MYDV2cd6atu8dpGddHDUH0gXpjnMJcFm0Wjy3Y0Xmrk6PiFrsSNuXVRQ8au85iePJ6bAnsTIvG4B1FV2Uc/f8fOucO0uLXYeVP98Uy+JgBRflnD2nYenDe7AGYZfHsngw2qr998SyeHnAwaM2jgog3fMm4CMAaTj4CyyPeoXz4RjnwwnAGcDiWBa7KrPMw/NIjkdjF5bZ2EW5kuKIiWHwnAacg5UqWRPLYqCLQzvI1fN+zHMp1sjsl25ircorTXZUAOmCFLm/AZzmfFiZtu3Aho+LgekpQ+TGKi8kOXh24XhctHTdebHCvvFD5DkjWrmNj1Z5YzMEnjuwitSt+cSxaI2uBj4HUCdHBZDueQqbfF7iUhfBaPn+Y8DC9L6yom5t5OB5OMeDQKve1fMVubWTu+cYltEE1nemanL23I55nl2lWBu1cNQk+iS0pzs6qwLrgZXA41iu+leBD8eyqKRvQoscPHNwTG7y7CPyHF5HpfF24Hw4G0uN2wk8F239RGvV5lxsHcA1WJvKdwAXVvEHlYNnDo7ylGedPevuqBFIG86a3t+CnaxXsZXE34q22Ol8rJ/H+mhtSSsjB88cHEGe/UaezXLUHMj/4oGvxLJYCdyGLXTa7Hw4CcujviGWxSOu+pIFOXjm4Ajy7DfybJCjAgjgJmoXHQW8G/6b1XAXVnX1C8CWaJVCqyz5UXvPHBzlKc86e+bg2KLxAcRZOelL0ts7gVXOhxXp/dNYn+B52MrOKksr1N4zB0eQZ7+RZ7Mc22l0AEnPEe8D7nA+nJqi/AbgUufDypRD/RC2aOcMeebtKE951tkzB8dOGpuF5XxYhjVXWYYtvrkAeAyr7T8GbHQ+nALsA96Z9skzU0d5yrPOnjk4HopGjkCcD28FVmC9CB7GqlZ+3FkntL3RusytAo4HTgJWxbJ4Up55OspTnnX2zMHxsIyPjzfutXDp2tGFS9fO7tj2wMKla29OX49U7ZiLZw6O8pRnnT1zcDzcq1EjEOfDuc6HDwHvi2Xxr7RtRtp9EzDL+TAnpp7h8szbUZ7yrLNnDo6T0ZgAkp4x3oVVq7za+fADgFgW+9MhjwFnYUPFKjNFau+Zg6M85Vlnzxwcu6ERK9Gd9QbfBtwSy+I3zof5WAOW7bEs1rUddxHWaOlTwP5Bn7QcPHNwlKc86+yZg2O3NGUEMoKVAdgDkCagCmCR82FT23G/BlbHsni1opOVg2cOjiDPfiPPZjl2xVCPQJwPp8TUq8H5sAFYjxUeOx/rw/wd4DqsXMBL8szbUZ7yrLNnDo5vlKEdgTgflgM7nQ9bAWJZbABuBk7F0uSuidbb+i1YX2t5ZuwoT3nW2TMHx14YyhGI82Em9ozxZ8B5wLGxLFYf4rg1wBXAJ2NZDLwxUA6eOTimf1+efUSezXLslaEMIADOhxOBl4HpWE2Z12NZfCbtG8WGjTdgjel3yjNvR3nKs86eOTj2wtAGkHacDycAP8QyGdY4H04HTgYeiWWxu1q7CXLwzMER5Nlv5Nk/cnDslkYEEADnw5uxZ47nYXM/i2NZPFut1f+Tg2cOjiDPfiPP/pGDYzcM7SR6J+mZ4l+A2Vjbx1qerBw8c3AEefYbefaPHBy7oTEBxPkwB+vwtSSWxV+r9jkcOXjm4Ajy7Dfy7B85OHZF1cW4Bly0bHrVDsPimYOjPOVZ51cOjpO9GjMHIoQQor805hGWEEKI/qIAIoQQoicUQIQQQvSEAogQR8D5cI/z4ZtVewhRRxRAhOgDzoffOR/WV+0hxCBRABFCCNETSuMVog3nw1nAFuBdQAmMA38HNgE/AhYBo8AfgStiWTztfNgIXIv1dDgA3BPL4krnw2nA94BzgOeAr8Wy+PGAP5IQU4ZGIEIknA/HAD/HAsVc4CfARWn3UcDdwAJgPrAf+D5ALIvrgQeBK2NZHJ+Cx0zgV8C9WI+H1cAdzof3Du4TCTG1jFYtIESN+AAwDdicWoj+1PnwRYBYFi9gPR0ASKOO3x7hZy0HnohlcXd6v8P5sA24GNg1FfJCDBoFECEmOBF4pqP/9D8AnA/HAd8FLgDmpH2znA9Hx7I4eIiftQDrcd3emnQUG90IMRQogAgxwT+BtzkfRtqCyHzgceBLWPvRRbEsdjsfzgQeBUbScZ2TiU8Bv49l8bEBeAtRCQogQkzwEDYJfpXz4XbgE8C52KOqWdi8x0vOh7nA1zu+dw/WFKjFduDbzodLgPvStjOBfbEs/jZ1H0GIwaFJdCESsSxeBy4ELgVeBD6N9bEG2AzMAJ4HHgYe6Pj2W4GLnQ8vOh9ui2WxF1gCrAKeBXYDNwHHTvHHEGJgKI1XCCFET2gEIoQQoicUQIQQQvSEAogQQoieUAARQgjREwogQgghekIBRAghRE8ogAghhOgJBRAhhBA9oQAihBCiJ/4DzsxKuuNrM+UAAAAASUVORK5CYII=
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Daily-Breakdowns">Daily Breakdowns<a class="anchor-link" href="#Daily-Breakdowns">&#182;</a></h3><p>Logins ramp up as the weekend approaches and peak on Saturdays.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># break logins into days of week</span>
<span class="n">df</span><span class="p">[</span><span class="s1">&#39;day_of_week&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">login_time</span><span class="o">.</span><span class="n">dt</span><span class="o">.</span><span class="n">dayofweek</span>

<span class="c1"># sort by count</span>
<span class="n">df_wkd</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span> <span class="o">=</span> <span class="s1">&#39;count&#39;</span><span class="p">,</span> <span class="n">ascending</span> <span class="o">=</span> <span class="kc">False</span><span class="p">)</span>

<span class="c1"># extract the day of week and count, then group by day and sum all logins</span>
<span class="n">df_wkd</span> <span class="o">=</span> <span class="n">df_wkd</span><span class="p">[[</span><span class="s1">&#39;day_of_week&#39;</span><span class="p">,</span> <span class="s1">&#39;count&#39;</span><span class="p">]]</span>
<span class="n">df_wkd</span> <span class="o">=</span> <span class="n">df_wkd</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;day_of_week&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>

<span class="c1"># names for ease of reference</span>
<span class="n">df_wkd</span><span class="o">.</span><span class="n">day_of_week</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;Mon&#39;</span><span class="p">,</span> <span class="s1">&#39;Tues&#39;</span><span class="p">,</span> <span class="s1">&#39;Wed&#39;</span><span class="p">,</span> <span class="s1">&#39;Thurs&#39;</span><span class="p">,</span> <span class="s1">&#39;Fri&#39;</span><span class="p">,</span> <span class="s1">&#39;Sat&#39;</span><span class="p">,</span> <span class="s1">&#39;Sun&#39;</span><span class="p">]</span>

<span class="c1"># bar plot</span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">&#39;day_of_week&#39;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">&#39;count&#39;</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">df_wkd</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Day&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Logins&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Logins by Day of Week&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Hourly-Breakdowns">Hourly Breakdowns<a class="anchor-link" href="#Hourly-Breakdowns">&#182;</a></h3><p>Peak times are from 9pm - 4am and again at the lunch hour.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="p">[</span><span class="s1">&#39;hour&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">login_time</span><span class="o">.</span><span class="n">dt</span><span class="o">.</span><span class="n">hour</span>
<span class="n">hours</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="s1">&#39;count&#39;</span><span class="p">]]</span>
<span class="n">hours</span> <span class="o">=</span> <span class="n">hours</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;hour&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>

<span class="c1"># Monday</span>
<span class="n">mon</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">day_of_week</span> <span class="o">==</span> <span class="mi">0</span><span class="p">]</span>

<span class="c1"># create a new df to highlight logins by hour, weekends only</span>
<span class="n">mon_hours</span> <span class="o">=</span> <span class="n">mon</span><span class="p">[[</span><span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="s1">&#39;count&#39;</span><span class="p">]]</span>
<span class="n">mon_hours</span> <span class="o">=</span> <span class="n">mon_hours</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;hour&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
<span class="n">mon_hours</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[9]:</div>



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
      <th>hour</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>531</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>414</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>312</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>236</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>206</td>
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
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Tues</span>
<span class="n">tues</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">day_of_week</span> <span class="o">==</span> <span class="mi">1</span><span class="p">]</span>

<span class="c1"># create a new df to highlight logins by hour, weekends only</span>
<span class="n">tues_hours</span> <span class="o">=</span> <span class="n">tues</span><span class="p">[[</span><span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="s1">&#39;count&#39;</span><span class="p">]]</span>
<span class="n">tues_hours</span> <span class="o">=</span> <span class="n">tues_hours</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;hour&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Wed</span>
<span class="n">wed</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">day_of_week</span> <span class="o">==</span> <span class="mi">2</span><span class="p">]</span>

<span class="c1"># create a new df to highlight logins by hour, weekends only</span>
<span class="n">wed_hours</span> <span class="o">=</span> <span class="n">wed</span><span class="p">[[</span><span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="s1">&#39;count&#39;</span><span class="p">]]</span>
<span class="n">wed_hours</span> <span class="o">=</span> <span class="n">wed_hours</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;hour&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Thurs</span>
<span class="n">thurs</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">day_of_week</span> <span class="o">==</span> <span class="mi">3</span><span class="p">]</span>

<span class="c1"># create a new df to highlight logins by hour, weekends only</span>
<span class="n">thurs_hours</span> <span class="o">=</span> <span class="n">thurs</span><span class="p">[[</span><span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="s1">&#39;count&#39;</span><span class="p">]]</span>
<span class="n">thurs_hours</span> <span class="o">=</span> <span class="n">thurs_hours</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;hour&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Fri</span>
<span class="n">fri</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">day_of_week</span> <span class="o">==</span> <span class="mi">4</span><span class="p">]</span>

<span class="c1"># create a new df to highlight logins by hour, weekends only</span>
<span class="n">fri_hours</span> <span class="o">=</span> <span class="n">fri</span><span class="p">[[</span><span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="s1">&#39;count&#39;</span><span class="p">]]</span>
<span class="n">fri_hours</span> <span class="o">=</span> <span class="n">fri_hours</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;hour&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Sat</span>
<span class="n">sat</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">day_of_week</span> <span class="o">==</span> <span class="mi">5</span><span class="p">]</span>

<span class="c1"># create a new df to highlight logins by hour, weekends only</span>
<span class="n">sat_hours</span> <span class="o">=</span> <span class="n">sat</span><span class="p">[[</span><span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="s1">&#39;count&#39;</span><span class="p">]]</span>
<span class="n">sat_hours</span> <span class="o">=</span> <span class="n">sat_hours</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;hour&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Sun</span>
<span class="n">sun</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">day_of_week</span> <span class="o">==</span> <span class="mi">6</span><span class="p">]</span>

<span class="c1"># create a new df to highlight logins by hour, weekends only</span>
<span class="n">sun_hours</span> <span class="o">=</span> <span class="n">sun</span><span class="p">[[</span><span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="s1">&#39;count&#39;</span><span class="p">]]</span>
<span class="n">sun_hours</span> <span class="o">=</span> <span class="n">sun_hours</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;hour&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">18</span><span class="p">,</span><span class="mi">18</span><span class="p">))</span>

<span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">&#39;count&#39;</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">mon_hours</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;logins count&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">(</span><span class="n">ymax</span> <span class="o">=</span> <span class="mi">2200</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Monday&#39;</span><span class="p">)</span>

<span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">2</span><span class="p">)</span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">&#39;count&#39;</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">tues_hours</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;logins count&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">(</span><span class="n">ymax</span> <span class="o">=</span> <span class="mi">2200</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Tuesday&#39;</span><span class="p">)</span>

<span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">3</span><span class="p">)</span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">&#39;count&#39;</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">wed_hours</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;logins count&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">(</span><span class="n">ymax</span> <span class="o">=</span> <span class="mi">2200</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Wednesday&#39;</span><span class="p">)</span>

<span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">4</span><span class="p">)</span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">&#39;count&#39;</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">thurs_hours</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;logins count&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">(</span><span class="n">ymax</span> <span class="o">=</span> <span class="mi">2200</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Thursday&#39;</span><span class="p">)</span>

<span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">5</span><span class="p">)</span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">&#39;count&#39;</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">fri_hours</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;logins count&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">(</span><span class="n">ymax</span> <span class="o">=</span> <span class="mi">2200</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Friday&#39;</span><span class="p">)</span>

<span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">6</span><span class="p">)</span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">&#39;count&#39;</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">sat_hours</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;logins count&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">(</span><span class="n">ymax</span> <span class="o">=</span> <span class="mi">2200</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Saturday&#39;</span><span class="p">)</span>

<span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">7</span><span class="p">)</span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">&#39;hour&#39;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">&#39;count&#39;</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">sun_hours</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;logins count&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylim</span><span class="p">(</span><span class="n">ymax</span> <span class="o">=</span> <span class="mi">2200</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Sunday&#39;</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">suptitle</span><span class="p">(</span><span class="s1">&#39;Hourly Logins Counts&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Analysis">Analysis<a class="anchor-link" href="#Analysis">&#182;</a></h3><p>By far, the busiest times are early Saturday &amp; Sunday mornings.  People are going out and leaving the driving to someone else, which is great for everyone.</p>
<p>There are much smaller peaks during the nights and early mornings every day of the week.</p>
<p>There are also peaks around lunch Mondays - Fridays and steady logins during the afternoons and evenings on Saturdays and Sundays.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Part-2-&#8208;-Experiment-and-metrics-design">Part 2 &#8208; Experiment and metrics design<a class="anchor-link" href="#Part-2-&#8208;-Experiment-and-metrics-design">&#182;</a></h2><p>The neighboring cities of Gotham and Metropolis have complementary circadian rhythms: on weekdays, Ultimate Gotham is most active at night, and Ultimate Metropolis is most active during the day. On weekends, there is reasonable activity in both cities.
However, a toll bridge, with a two­way toll, between the two cities causes driver partners to tend to be exclusive to each city. The Ultimate managers of city operations for the two cities have proposed an experiment to encourage driver partners to be available in both cities, by reimbursing all toll costs.</p>
<ol>
<li>What would you choose as the key measure of success of this experiment in encouraging driver partners to serve both cities, and why would you choose this metric?</li>
<li>Describe a practical experiment you would design to compare the effectiveness of the proposed change in relation to the key measure of success. Please provide details on:
a. how you will implement the experiment
b. what statistical test(s) you will conduct to verify the significance of the
observation
c. how you would interpret the results and provide recommendations to the city
operations team along with any caveats.</li>
</ol>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Analysis">Analysis<a class="anchor-link" href="#Analysis">&#182;</a></h3><p>The only reason for reimbursing tolls would be to increase driver availability levels to reduce wait times for users.  The intended consequence is that more users would take more trips more often and that the income <strong>to the company</strong> would exceed the costs of reimbursing the tolls.</p>
<p>The key measure of success would be Ultimate's income after subtracting out the cost of paying for the tolls.  Other indicators would be the number of drivers available for pickups at all times, the number of trips across the toll bridge, and the mean time between a user requesting a car and pickup.</p>
<p>I would recommend performing an A/B test wherein a portion of the drivers are offered reimbursement and the remaining drivers continue to operate without being reimbursed for tolls.  This will allow us to control for factors such as a general growth in popularity of our service as well as seasonal changes in ridership while testing.  I would perform a $t-test$ with a confidence level of 95%, where the null hypothesis is the reimbursing drivers for tolls does not have a statistically-significant impact on Ultimate's net profits.</p>
<p>I would also suggest that this test may not be entirely dispositive.  The danger is that once toll reimbursements are extended to all drivers, the pool of available drivers may become saturated and cause some drivers to stop driving, again increasing wait times and causing users to use a different service.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Part-3:-Predictive-Modeling">Part 3: Predictive Modeling<a class="anchor-link" href="#Part-3:-Predictive-Modeling">&#182;</a></h2><p>Ultimate is interested in predicting rider retention. To help explore this question, we have provided a sample dataset of a cohort of users who signed up for an Ultimate account in January 2014. The data was pulled several months later; we consider a user retained if they were “active” (i.e. took a trip) in the preceding 30 days. We would like you to use this data set to help understand what factors are the best predictors for retention, and offer suggestions to operationalize those insights to help Ultimate.</p>
<p>The data is in the attached file ultimate_data_challenge.json. See below for a detailed description of the dataset. Please include any code you wrote for the analysis and delete the dataset when you have finished with the challenge.</p>
<p>Perform any cleaning, exploratory analysis, and/or visualizations to use the provided data for this analysis (a few sentences/plots describing your approach will suffice). What fraction of the observed users were retained?</p>
<p>Build a predictive model to help Ultimate determine whether or not a user will be active in their 6th month on the system. Discuss why you chose your approach, what alternatives you considered, and any concerns you have. How valid is your model? Include any key indicators of model performance.</p>
<p>Briefly discuss how Ultimate might leverage the insights gained from the model to improve its long­term rider retention (again, a few sentences will suffice).</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<div>
  <table>
    <thead>
      <tr>
        <th>Statistic</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>city</b></td>
        <td>The city the user signed up in</td>
      </tr>
      <tr>
        <td><b>phone</b></td>
        <td>primary device for the user</td>
      </tr>
      <tr>
        <td><b>signup_date</b></td>
        <td>date of account registration; in the form ‘YYYY MM DD’</td>
      </tr>
      <tr>
        <td><b>last_trip_date</b></td>
        <td>the last time this user completed a trip; in the form ‘YYYY MM DD’</td>
      </tr>
      <tr>
        <td><b>avg_dist</b></td>
        <td>the average distance in miles per trip taken in the first 30 days after signup</td>
      </tr>
      <tr>
        <td><b>avg_rating_by_driver</b></td>
        <td>the rider’s average rating over all of their trips</td>
      </tr>
      <tr>
        <td><b>avg_rating_of_driver</b></td>
        <td>the rider’s average rating of their drivers over all of their trips</td>
      </tr>
      <tr>
        <td><b>surge_pct</b></td>
        <td>the percent of trips taken with surge multiplier > 1</td>
      </tr>
      <tr>
        <td><b>avg_surge</b></td>
        <td>the average surge multiplier over all of this user’s trips</td>
      </tr>
      <tr>
        <td><b>trips_in_first_30_days</b></td>
        <td>the number of trips this user took in the first 30 days after signing up</td>
      </tr>
      <tr>
        <td><b>ultimate_black_user</b></td>
        <td>TRUE if the user took an Ultimate Black in their first 30 days; FALSE otherwise</td>
      </tr>
      <tr>
        <td><b>weekday_pct</b></td>
        <td>the percent of the user’s trips occurring during a weekday</td>
      </tr>
    </tbody>
  </table>
</div>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Analysis">Analysis<a class="anchor-link" href="#Analysis">&#182;</a></h3><p>As shown below, we can achieve a 76% accuracy rate using a Decision Tree algorithm that has been tuned.  Decision Trees are a white box model, meaning that the resulting algorithm is relatively easily understood by humans.  The relative importances of the features are shown below.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">json</span>

<span class="n">file</span> <span class="o">=</span> <span class="nb">open</span><span class="p">(</span><span class="s1">&#39;data/ultimate_data_challenge.json&#39;</span><span class="p">,</span> <span class="s1">&#39;r&#39;</span><span class="p">)</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">json</span><span class="o">.</span><span class="n">load</span><span class="p">(</span><span class="n">file</span><span class="p">))</span>
<span class="n">file</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>

<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[17]:</div>



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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>city</th>
      <th>last_trip_date</th>
      <th>phone</th>
      <th>signup_date</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>ultimate_black_user</th>
      <th>weekday_pct</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.67</td>
      <td>5.0</td>
      <td>4.7</td>
      <td>1.10</td>
      <td>King's Landing</td>
      <td>2014-06-17</td>
      <td>iPhone</td>
      <td>2014-01-25</td>
      <td>15.4</td>
      <td>4</td>
      <td>True</td>
      <td>46.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8.26</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-05-05</td>
      <td>Android</td>
      <td>2014-01-29</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.77</td>
      <td>5.0</td>
      <td>4.3</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-01-07</td>
      <td>iPhone</td>
      <td>2014-01-06</td>
      <td>0.0</td>
      <td>3</td>
      <td>False</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.36</td>
      <td>4.9</td>
      <td>4.6</td>
      <td>1.14</td>
      <td>King's Landing</td>
      <td>2014-06-29</td>
      <td>iPhone</td>
      <td>2014-01-10</td>
      <td>20.0</td>
      <td>9</td>
      <td>True</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.13</td>
      <td>4.9</td>
      <td>4.4</td>
      <td>1.19</td>
      <td>Winterfell</td>
      <td>2014-03-15</td>
      <td>Android</td>
      <td>2014-01-27</td>
      <td>11.8</td>
      <td>14</td>
      <td>False</td>
      <td>82.4</td>
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
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
RangeIndex: 50000 entries, 0 to 49999
Data columns (total 12 columns):
avg_dist                  50000 non-null float64
avg_rating_by_driver      49799 non-null float64
avg_rating_of_driver      41878 non-null float64
avg_surge                 50000 non-null float64
city                      50000 non-null object
last_trip_date            50000 non-null object
phone                     49604 non-null object
signup_date               50000 non-null object
surge_pct                 50000 non-null float64
trips_in_first_30_days    50000 non-null int64
ultimate_black_user       50000 non-null bool
weekday_pct               50000 non-null float64
dtypes: bool(1), float64(6), int64(1), object(4)
memory usage: 4.2+ MB
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Fill-Missing-Data">Fill Missing Data<a class="anchor-link" href="#Fill-Missing-Data">&#182;</a></h3><p>Missing ratings: people that don't rate probably didn't have strong feelings one way or the other, so fill missing values with averages<br>
Missing phones: fill with the most popular value</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># rating by driver</span>
<span class="n">df</span><span class="o">.</span><span class="n">avg_rating_by_driver</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">avg_rating_by_driver</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">avg_rating_by_driver</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
<span class="n">df</span><span class="o">.</span><span class="n">avg_rating_of_driver</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">avg_rating_of_driver</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">avg_rating_of_driver</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>

<span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
RangeIndex: 50000 entries, 0 to 49999
Data columns (total 12 columns):
avg_dist                  50000 non-null float64
avg_rating_by_driver      50000 non-null float64
avg_rating_of_driver      50000 non-null float64
avg_surge                 50000 non-null float64
city                      50000 non-null object
last_trip_date            50000 non-null object
phone                     49604 non-null object
signup_date               50000 non-null object
surge_pct                 50000 non-null float64
trips_in_first_30_days    50000 non-null int64
ultimate_black_user       50000 non-null bool
weekday_pct               50000 non-null float64
dtypes: bool(1), float64(6), int64(1), object(4)
memory usage: 4.2+ MB
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># fill missing phone</span>
<span class="n">df</span><span class="o">.</span><span class="n">phone</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[20]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>iPhone     34582
Android    15022
Name: phone, dtype: int64</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">phone</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">phone</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s1">&#39;iPhone&#39;</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
RangeIndex: 50000 entries, 0 to 49999
Data columns (total 12 columns):
avg_dist                  50000 non-null float64
avg_rating_by_driver      50000 non-null float64
avg_rating_of_driver      50000 non-null float64
avg_surge                 50000 non-null float64
city                      50000 non-null object
last_trip_date            50000 non-null object
phone                     50000 non-null object
signup_date               50000 non-null object
surge_pct                 50000 non-null float64
trips_in_first_30_days    50000 non-null int64
ultimate_black_user       50000 non-null bool
weekday_pct               50000 non-null float64
dtypes: bool(1), float64(6), int64(1), object(4)
memory usage: 4.2+ MB
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">last_trip_date</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">last_trip_date</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">signup_date</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">signup_date</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
RangeIndex: 50000 entries, 0 to 49999
Data columns (total 12 columns):
avg_dist                  50000 non-null float64
avg_rating_by_driver      50000 non-null float64
avg_rating_of_driver      50000 non-null float64
avg_surge                 50000 non-null float64
city                      50000 non-null object
last_trip_date            50000 non-null datetime64[ns]
phone                     50000 non-null object
signup_date               50000 non-null datetime64[ns]
surge_pct                 50000 non-null float64
trips_in_first_30_days    50000 non-null int64
ultimate_black_user       50000 non-null bool
weekday_pct               50000 non-null float64
dtypes: bool(1), datetime64[ns](2), float64(6), int64(1), object(2)
memory usage: 4.2+ MB
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">earliest_signup</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">signup_date</span><span class="o">.</span><span class="n">min</span><span class="p">()</span>
<span class="n">latest_signup</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">signup_date</span><span class="o">.</span><span class="n">max</span><span class="p">()</span>
<span class="n">signups_ct</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">signup_date</span><span class="o">.</span><span class="n">count</span><span class="p">()</span>
<span class="n">last_trip</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">last_trip_date</span><span class="o">.</span><span class="n">max</span><span class="p">()</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;There were </span><span class="si">{}</span><span class="s1"> signups between </span><span class="si">{}</span><span class="s1"> and </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">signups_ct</span><span class="p">,</span> <span class="n">earliest_signup</span><span class="p">,</span> <span class="n">latest_signup</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Last trip: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">last_trip</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>There were 50000 signups between 2014-01-01 00:00:00 and 2014-01-31 00:00:00
Last trip: 2014-07-01 00:00:00
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[24]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[24]:</div>



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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>weekday_pct</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>50000.000000</td>
      <td>5.000000e+04</td>
      <td>5.000000e+04</td>
      <td>50000.000000</td>
      <td>50000.000000</td>
      <td>50000.000000</td>
      <td>50000.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>5.796827</td>
      <td>4.778158e+00</td>
      <td>4.601559e+00</td>
      <td>1.074764</td>
      <td>8.849536</td>
      <td>2.278200</td>
      <td>60.926084</td>
    </tr>
    <tr>
      <th>std</th>
      <td>5.707357</td>
      <td>3.250766e-12</td>
      <td>8.473307e-13</td>
      <td>0.222336</td>
      <td>19.958811</td>
      <td>3.792684</td>
      <td>37.081503</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>4.778158e+00</td>
      <td>4.601559e+00</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2.420000</td>
      <td>4.778158e+00</td>
      <td>4.601559e+00</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>33.300000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>3.880000</td>
      <td>4.778158e+00</td>
      <td>4.601559e+00</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>66.700000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>6.940000</td>
      <td>4.778158e+00</td>
      <td>4.601559e+00</td>
      <td>1.050000</td>
      <td>8.600000</td>
      <td>3.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>160.960000</td>
      <td>4.778158e+00</td>
      <td>4.601559e+00</td>
      <td>8.000000</td>
      <td>100.000000</td>
      <td>125.000000</td>
      <td>100.000000</td>
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
<div class="prompt input_prompt">In&nbsp;[25]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># dist by phone</span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">&#39;phone&#39;</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">&#39;avg_dist&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">df</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Distance&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Phone Type&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Trip Distance by Phone Type&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[26]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># black by phone</span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">&#39;phone&#39;</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">&#39;ultimate_black_user&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">df</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Black Use&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Phone Type&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Black Use by Phone Type&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[27]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">active</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">last_trip_date</span> <span class="o">&gt;=</span> <span class="s1">&#39;2014-06-01 00:00:00&#39;</span><span class="p">]</span>
<span class="n">active</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
<span class="nb">len</span><span class="p">(</span><span class="n">active</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[27]:</div>



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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>city</th>
      <th>last_trip_date</th>
      <th>phone</th>
      <th>signup_date</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>ultimate_black_user</th>
      <th>weekday_pct</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.67</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.10</td>
      <td>King's Landing</td>
      <td>2014-06-17</td>
      <td>iPhone</td>
      <td>2014-01-25</td>
      <td>15.4</td>
      <td>4</td>
      <td>True</td>
      <td>46.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.36</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.14</td>
      <td>King's Landing</td>
      <td>2014-06-29</td>
      <td>iPhone</td>
      <td>2014-01-10</td>
      <td>20.0</td>
      <td>9</td>
      <td>True</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>10.56</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>Winterfell</td>
      <td>2014-06-06</td>
      <td>iPhone</td>
      <td>2014-01-09</td>
      <td>0.0</td>
      <td>2</td>
      <td>True</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>3.04</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.38</td>
      <td>King's Landing</td>
      <td>2014-06-08</td>
      <td>iPhone</td>
      <td>2014-01-29</td>
      <td>50.0</td>
      <td>0</td>
      <td>False</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>10.86</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>King's Landing</td>
      <td>2014-06-28</td>
      <td>Android</td>
      <td>2014-01-11</td>
      <td>0.0</td>
      <td>1</td>
      <td>True</td>
      <td>50.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[27]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>18804</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[28]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Cities: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">city</span><span class="o">.</span><span class="n">unique</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Cities: [&#34;King&#39;s Landing&#34; &#39;Astapor&#39; &#39;Winterfell&#39;]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[29]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># mark users &#39;retained&#39; in main df if rode in last 30 days</span>
<span class="n">df</span><span class="p">[</span><span class="s1">&#39;retained&#39;</span><span class="p">]</span> <span class="o">=</span>  <span class="n">df</span><span class="o">.</span><span class="n">last_trip_date</span> <span class="o">&gt;=</span> <span class="s1">&#39;2014-06-01 00:00:00&#39;</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[29]:</div>



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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>city</th>
      <th>last_trip_date</th>
      <th>phone</th>
      <th>signup_date</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>ultimate_black_user</th>
      <th>weekday_pct</th>
      <th>retained</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.67</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.10</td>
      <td>King's Landing</td>
      <td>2014-06-17</td>
      <td>iPhone</td>
      <td>2014-01-25</td>
      <td>15.4</td>
      <td>4</td>
      <td>True</td>
      <td>46.2</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8.26</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-05-05</td>
      <td>Android</td>
      <td>2014-01-29</td>
      <td>0.0</td>
      <td>0</td>
      <td>False</td>
      <td>50.0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.77</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>Astapor</td>
      <td>2014-01-07</td>
      <td>iPhone</td>
      <td>2014-01-06</td>
      <td>0.0</td>
      <td>3</td>
      <td>False</td>
      <td>100.0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.36</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.14</td>
      <td>King's Landing</td>
      <td>2014-06-29</td>
      <td>iPhone</td>
      <td>2014-01-10</td>
      <td>20.0</td>
      <td>9</td>
      <td>True</td>
      <td>80.0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.13</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.19</td>
      <td>Winterfell</td>
      <td>2014-03-15</td>
      <td>Android</td>
      <td>2014-01-27</td>
      <td>11.8</td>
      <td>14</td>
      <td>False</td>
      <td>82.4</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="EDA---Retention-by:">EDA - Retention by:<a class="anchor-link" href="#EDA---Retention-by:">&#182;</a></h3><h4 id="Phone-Type">Phone Type<a class="anchor-link" href="#Phone-Type">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[30]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">ph_ret</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s1">&#39;retained&#39;</span><span class="p">,</span> <span class="s1">&#39;phone&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;phone&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
<span class="n">ph_ret</span>

<span class="n">all_android</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">phone</span> <span class="o">==</span> <span class="s1">&#39;Android&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">phone</span><span class="o">.</span><span class="n">count</span><span class="p">()</span>
<span class="n">all_android</span>

<span class="n">all_iphone</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">phone</span> <span class="o">==</span> <span class="s1">&#39;iPhone&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">phone</span><span class="o">.</span><span class="n">count</span><span class="p">()</span>
<span class="n">all_iphone</span>

<span class="n">ph_ret</span><span class="p">[</span><span class="s1">&#39;percent&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="mi">0</span>

<span class="n">ph_ret</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">2</span><span class="p">]</span> <span class="o">=</span> <span class="n">ph_ret</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="s1">&#39;retained&#39;</span><span class="p">]</span> <span class="o">/</span> <span class="n">all_android</span> <span class="o">*</span> <span class="mi">100</span>
<span class="n">ph_ret</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">]</span> <span class="o">=</span> <span class="n">ph_ret</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="s1">&#39;retained&#39;</span><span class="p">]</span> <span class="o">/</span> <span class="n">all_iphone</span> <span class="o">*</span> <span class="mi">100</span>

<span class="n">ph_ret</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[30]:</div>



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
      <th>phone</th>
      <th>retained</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Android</td>
      <td>3146.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>iPhone</td>
      <td>15658.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[30]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>15022</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[30]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>34978</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[30]:</div>



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
      <th>phone</th>
      <th>retained</th>
      <th>percent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Android</td>
      <td>3146.0</td>
      <td>20.942617</td>
    </tr>
    <tr>
      <th>1</th>
      <td>iPhone</td>
      <td>15658.0</td>
      <td>44.765281</td>
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
<div class="prompt input_prompt">In&nbsp;[31]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">&#39;phone&#39;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">&#39;percent&#39;</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">ph_ret</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Phone&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;% Retained&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;% Retained by Phone Type&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="City">City<a class="anchor-link" href="#City">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[32]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">city</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s1">&#39;retained&#39;</span><span class="p">,</span> <span class="s1">&#39;city&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;city&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>

<span class="n">city_total</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s1">&#39;retained&#39;</span><span class="p">,</span> <span class="s1">&#39;city&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;city&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">count</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>

<span class="n">city</span> <span class="o">=</span> <span class="n">city</span><span class="o">.</span><span class="n">merge</span><span class="p">(</span><span class="n">city_total</span><span class="p">,</span> <span class="n">on</span> <span class="o">=</span> <span class="s1">&#39;city&#39;</span><span class="p">)</span>
<span class="n">city</span><span class="o">.</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;city&#39;</span><span class="p">,</span> <span class="s1">&#39;retained&#39;</span><span class="p">,</span> <span class="s1">&#39;total&#39;</span><span class="p">]</span>
<span class="n">city</span><span class="p">[</span><span class="s1">&#39;percent&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">city</span><span class="o">.</span><span class="n">retained</span> <span class="o">/</span> <span class="n">city</span><span class="o">.</span><span class="n">total</span> <span class="o">*</span> <span class="mi">100</span>
<span class="n">city</span>

<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">&#39;city&#39;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">&#39;percent&#39;</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">city</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;City&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;% Retained&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;% Retained by City&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Early-Use">Early Use<a class="anchor-link" href="#Early-Use">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[33]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">early</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s1">&#39;retained&#39;</span><span class="p">,</span> <span class="s1">&#39;trips_in_first_30_days&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;trips_in_first_30_days&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>

<span class="n">early_total</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s1">&#39;retained&#39;</span><span class="p">,</span> <span class="s1">&#39;trips_in_first_30_days&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;trips_in_first_30_days&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">count</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>

<span class="n">early</span> <span class="o">=</span> <span class="n">early</span><span class="o">.</span><span class="n">merge</span><span class="p">(</span><span class="n">early_total</span><span class="p">,</span> <span class="n">on</span> <span class="o">=</span> <span class="s1">&#39;trips_in_first_30_days&#39;</span><span class="p">)</span>
<span class="n">early</span>
<span class="n">early</span><span class="o">.</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;trips_in_first_30_days&#39;</span><span class="p">,</span> <span class="s1">&#39;retained&#39;</span><span class="p">,</span> <span class="s1">&#39;total&#39;</span><span class="p">]</span>
<span class="n">early</span><span class="p">[</span><span class="s1">&#39;percent&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">early</span><span class="o">.</span><span class="n">retained</span> <span class="o">/</span> <span class="n">early</span><span class="o">.</span><span class="n">total</span> <span class="o">*</span> <span class="mi">100</span>
<span class="n">early</span>

<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">early</span><span class="p">[</span><span class="s1">&#39;trips_in_first_30_days&#39;</span><span class="p">],</span> <span class="n">early</span><span class="p">[</span><span class="s1">&#39;percent&#39;</span><span class="p">])</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;# of Trips in First 30 Days&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;% Retained&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;% Retained by Count of Uses in First 30 Days&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[34]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s1">&#39;last_trip_date&#39;</span><span class="p">,</span> <span class="s1">&#39;signup_date&#39;</span><span class="p">],</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[35]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">get_dummies</span><span class="p">(</span><span class="n">df</span><span class="p">,</span> <span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;city&#39;</span><span class="p">,</span> <span class="s1">&#39;phone&#39;</span><span class="p">,</span> <span class="s1">&#39;ultimate_black_user&#39;</span><span class="p">])</span>
<span class="n">df</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[35]:</div>



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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>weekday_pct</th>
      <th>retained</th>
      <th>city_Astapor</th>
      <th>city_King's Landing</th>
      <th>city_Winterfell</th>
      <th>phone_Android</th>
      <th>phone_iPhone</th>
      <th>ultimate_black_user_False</th>
      <th>ultimate_black_user_True</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.67</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.10</td>
      <td>15.4</td>
      <td>4</td>
      <td>46.2</td>
      <td>True</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8.26</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>50.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.77</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>3</td>
      <td>100.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.36</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.14</td>
      <td>20.0</td>
      <td>9</td>
      <td>80.0</td>
      <td>True</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.13</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.19</td>
      <td>11.8</td>
      <td>14</td>
      <td>82.4</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>10.56</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>2</td>
      <td>100.0</td>
      <td>True</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3.95</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2.04</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>2</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4.36</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>2</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2.37</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>4.28</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>3.81</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>3</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>20.29</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>3.04</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.38</td>
      <td>50.0</td>
      <td>0</td>
      <td>50.0</td>
      <td>True</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>26.01</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>13.20</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>10.86</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>50.0</td>
      <td>True</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2.38</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>95.2</td>
      <td>True</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>6.83</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.21</td>
      <td>30.8</td>
      <td>6</td>
      <td>80.8</td>
      <td>True</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>19</th>
      <td>12.08</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.17</td>
      <td>33.3</td>
      <td>0</td>
      <td>66.7</td>
      <td>True</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2.53</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>50.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>3.31</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>11.47</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>7.74</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>True</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2.10</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.02</td>
      <td>9.1</td>
      <td>4</td>
      <td>36.4</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>14.48</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1.66</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>3.05</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.05</td>
      <td>20.0</td>
      <td>3</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>5.97</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.50</td>
      <td>100.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>True</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>11.25</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49970</th>
      <td>5.62</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>2</td>
      <td>0.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49971</th>
      <td>4.69</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>True</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>49972</th>
      <td>4.60</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.25</td>
      <td>50.0</td>
      <td>1</td>
      <td>0.0</td>
      <td>True</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49973</th>
      <td>4.07</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>2</td>
      <td>25.0</td>
      <td>True</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>49974</th>
      <td>4.63</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>2.00</td>
      <td>100.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49975</th>
      <td>2.18</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.03</td>
      <td>4.1</td>
      <td>11</td>
      <td>91.8</td>
      <td>True</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49976</th>
      <td>2.39</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>True</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49977</th>
      <td>8.71</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>4</td>
      <td>100.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49978</th>
      <td>6.02</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>50.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49979</th>
      <td>3.81</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>50.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>49980</th>
      <td>14.42</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49981</th>
      <td>5.49</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>49982</th>
      <td>15.23</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49983</th>
      <td>30.39</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49984</th>
      <td>3.50</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49985</th>
      <td>1.38</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49986</th>
      <td>0.52</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49987</th>
      <td>4.24</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>3</td>
      <td>80.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49988</th>
      <td>2.53</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>50.0</td>
      <td>True</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49989</th>
      <td>0.00</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49990</th>
      <td>3.38</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.08</td>
      <td>33.3</td>
      <td>1</td>
      <td>33.3</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>49991</th>
      <td>1.06</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.25</td>
      <td>100.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>True</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49992</th>
      <td>7.58</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0.0</td>
      <td>False</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49993</th>
      <td>2.53</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.11</td>
      <td>11.1</td>
      <td>3</td>
      <td>55.6</td>
      <td>True</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>49994</th>
      <td>2.25</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.44</td>
      <td>37.5</td>
      <td>1</td>
      <td>25.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49995</th>
      <td>5.63</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>True</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49996</th>
      <td>0.00</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49997</th>
      <td>3.86</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>False</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>49998</th>
      <td>4.58</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>2</td>
      <td>100.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>49999</th>
      <td>3.49</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>False</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>50000 rows × 15 columns</p>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[36]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">retained</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;retained&#39;</span><span class="p">,</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">)</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">y</span><span class="p">)</span>
<span class="n">df</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[36]:</div>



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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>weekday_pct</th>
      <th>city_Astapor</th>
      <th>city_King's Landing</th>
      <th>city_Winterfell</th>
      <th>phone_Android</th>
      <th>phone_iPhone</th>
      <th>ultimate_black_user_False</th>
      <th>ultimate_black_user_True</th>
      <th>retained</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.67</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.10</td>
      <td>15.4</td>
      <td>4</td>
      <td>46.2</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8.26</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>50.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.77</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>3</td>
      <td>100.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.36</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.14</td>
      <td>20.0</td>
      <td>9</td>
      <td>80.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.13</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.19</td>
      <td>11.8</td>
      <td>14</td>
      <td>82.4</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>10.56</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>2</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3.95</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2.04</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>2</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4.36</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>2</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2.37</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>10</th>
      <td>4.28</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>11</th>
      <td>3.81</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>3</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>20.29</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>13</th>
      <td>3.04</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.38</td>
      <td>50.0</td>
      <td>0</td>
      <td>50.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>14</th>
      <td>26.01</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>15</th>
      <td>13.20</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>16</th>
      <td>10.86</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>50.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2.38</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>95.2</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>18</th>
      <td>6.83</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.21</td>
      <td>30.8</td>
      <td>6</td>
      <td>80.8</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>19</th>
      <td>12.08</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.17</td>
      <td>33.3</td>
      <td>0</td>
      <td>66.7</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2.53</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>50.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>21</th>
      <td>3.31</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>22</th>
      <td>11.47</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>23</th>
      <td>7.74</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2.10</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.02</td>
      <td>9.1</td>
      <td>4</td>
      <td>36.4</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>25</th>
      <td>14.48</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1.66</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>27</th>
      <td>3.05</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.05</td>
      <td>20.0</td>
      <td>3</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>28</th>
      <td>5.97</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.50</td>
      <td>100.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>29</th>
      <td>11.25</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49970</th>
      <td>5.62</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>2</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49971</th>
      <td>4.69</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>49972</th>
      <td>4.60</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.25</td>
      <td>50.0</td>
      <td>1</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>49973</th>
      <td>4.07</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>2</td>
      <td>25.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>49974</th>
      <td>4.63</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>2.00</td>
      <td>100.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49975</th>
      <td>2.18</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.03</td>
      <td>4.1</td>
      <td>11</td>
      <td>91.8</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>49976</th>
      <td>2.39</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>49977</th>
      <td>8.71</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>4</td>
      <td>100.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49978</th>
      <td>6.02</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>50.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49979</th>
      <td>3.81</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>50.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49980</th>
      <td>14.42</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49981</th>
      <td>5.49</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49982</th>
      <td>15.23</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49983</th>
      <td>30.39</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49984</th>
      <td>3.50</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49985</th>
      <td>1.38</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49986</th>
      <td>0.52</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49987</th>
      <td>4.24</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>3</td>
      <td>80.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49988</th>
      <td>2.53</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>50.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>49989</th>
      <td>0.00</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49990</th>
      <td>3.38</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.08</td>
      <td>33.3</td>
      <td>1</td>
      <td>33.3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49991</th>
      <td>1.06</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.25</td>
      <td>100.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>49992</th>
      <td>7.58</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49993</th>
      <td>2.53</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.11</td>
      <td>11.1</td>
      <td>3</td>
      <td>55.6</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>49994</th>
      <td>2.25</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.44</td>
      <td>37.5</td>
      <td>1</td>
      <td>25.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49995</th>
      <td>5.63</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>True</td>
    </tr>
    <tr>
      <th>49996</th>
      <td>0.00</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49997</th>
      <td>3.86</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>100.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49998</th>
      <td>4.58</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>2</td>
      <td>100.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49999</th>
      <td>3.49</td>
      <td>4.778158</td>
      <td>4.601559</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
<p>50000 rows × 15 columns</p>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[37]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn</span> <span class="k">import</span> <span class="n">preprocessing</span>

<span class="c1"># create scaler</span>
<span class="n">scaler</span> <span class="o">=</span> <span class="n">preprocessing</span><span class="o">.</span><span class="n">StandardScaler</span><span class="p">()</span>

<span class="c1"># select columns to scale</span>
<span class="n">cols</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()</span>
<span class="n">cols_to_scale</span> <span class="o">=</span> <span class="n">cols</span><span class="p">[:</span><span class="mi">7</span><span class="p">]</span>
<span class="n">cols_to_scale</span>

<span class="c1"># transform numeric stats</span>
<span class="n">df</span><span class="p">[</span><span class="n">cols_to_scale</span><span class="p">]</span> <span class="o">=</span> <span class="n">scaler</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="n">cols_to_scale</span><span class="p">])</span>

<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[37]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>[&#39;avg_dist&#39;,
 &#39;avg_rating_by_driver&#39;,
 &#39;avg_rating_of_driver&#39;,
 &#39;avg_surge&#39;,
 &#39;surge_pct&#39;,
 &#39;trips_in_first_30_days&#39;,
 &#39;weekday_pct&#39;]</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[37]:</div>



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
      <th>avg_dist</th>
      <th>avg_rating_by_driver</th>
      <th>avg_rating_of_driver</th>
      <th>avg_surge</th>
      <th>surge_pct</th>
      <th>trips_in_first_30_days</th>
      <th>weekday_pct</th>
      <th>city_Astapor</th>
      <th>city_King's Landing</th>
      <th>city_Winterfell</th>
      <th>phone_Android</th>
      <th>phone_iPhone</th>
      <th>ultimate_black_user_False</th>
      <th>ultimate_black_user_True</th>
      <th>retained</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.372650</td>
      <td>-1.0</td>
      <td>-1.0</td>
      <td>0.113506</td>
      <td>0.328202</td>
      <td>0.453984</td>
      <td>-0.397131</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.431583</td>
      <td>-1.0</td>
      <td>-1.0</td>
      <td>-0.336268</td>
      <td>-0.443394</td>
      <td>-0.600689</td>
      <td>-0.294653</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.880771</td>
      <td>-1.0</td>
      <td>-1.0</td>
      <td>-0.336268</td>
      <td>-0.443394</td>
      <td>0.190316</td>
      <td>1.053741</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.602181</td>
      <td>-1.0</td>
      <td>-1.0</td>
      <td>0.293416</td>
      <td>0.558679</td>
      <td>1.772325</td>
      <td>0.514383</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.467266</td>
      <td>-1.0</td>
      <td>-1.0</td>
      <td>0.518303</td>
      <td>0.147829</td>
      <td>3.090665</td>
      <td>0.579106</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
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
<div class="prompt input_prompt">In&nbsp;[38]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s1">&#39;data/to_model.csv&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Modeling">Modeling<a class="anchor-link" href="#Modeling">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>&lt;div class = alert alert-success&gt;</p>
<p>&lt;/div&gt;</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[39]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># sklearn imports</span>
<span class="kn">from</span> <span class="nn">sklearn.dummy</span> <span class="k">import</span> <span class="n">DummyClassifier</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">train_test_split</span><span class="p">,</span> <span class="n">cross_val_score</span><span class="p">,</span> <span class="n">GridSearchCV</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="k">import</span> <span class="n">accuracy_score</span><span class="p">,</span> <span class="n">classification_report</span><span class="p">,</span> <span class="n">roc_curve</span><span class="p">,</span> <span class="n">roc_auc_score</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="k">import</span> <span class="n">precision_score</span><span class="p">,</span> <span class="n">recall_score</span><span class="p">,</span> <span class="n">f1_score</span><span class="p">,</span> <span class="n">confusion_matrix</span>

<span class="n">data</span> <span class="o">=</span> <span class="s1">&#39;data/to_model.csv&#39;</span>

<span class="c1"># set random_state SEED variable</span>
<span class="n">SEED</span> <span class="o">=</span> <span class="mi">42</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[40]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># training set breakdown</span>
<span class="n">train_success</span> <span class="o">=</span> <span class="n">y_train</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
<span class="n">train_total</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">y_train</span><span class="p">)</span>
<span class="n">train_percent</span> <span class="o">=</span> <span class="n">train_success</span> <span class="o">/</span> <span class="n">train_total</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Training Set</span><span class="se">\n</span><span class="s1">Successes:</span><span class="se">\t</span><span class="si">{}</span><span class="se">\n</span><span class="s1">Total:</span><span class="se">\t\t</span><span class="si">{}</span><span class="se">\n</span><span class="s1">Percent:</span><span class="se">\t</span><span class="si">{:.3f}</span><span class="se">\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">train_success</span><span class="p">,</span> <span class="n">train_total</span><span class="p">,</span> <span class="n">train_percent</span><span class="p">))</span>

<span class="c1"># test set breakdown</span>
<span class="n">test_success</span> <span class="o">=</span> <span class="n">y_test</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
<span class="n">test_total</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">y_test</span><span class="p">)</span>
<span class="n">test_percent</span> <span class="o">=</span> <span class="n">test_success</span> <span class="o">/</span> <span class="n">test_total</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Test Set</span><span class="se">\n</span><span class="s1">Successes:</span><span class="se">\t</span><span class="si">{}</span><span class="se">\n</span><span class="s1">Total:</span><span class="se">\t\t</span><span class="si">{}</span><span class="se">\n</span><span class="s1">Percent:</span><span class="se">\t</span><span class="si">{:.3f}</span><span class="se">\n\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">test_success</span><span class="p">,</span> <span class="n">test_total</span><span class="p">,</span> <span class="n">test_percent</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Training Set
Successes:	13183
Total:		35000
Percent:	0.377

Test Set
Successes:	5621
Total:		15000
Percent:	0.375


</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[41]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># check for balanced data set</span>

<span class="n">target_count</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">retained</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Class 0: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">target_count</span><span class="p">[</span><span class="mi">0</span><span class="p">]))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Class 1: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">target_count</span><span class="p">[</span><span class="mi">1</span><span class="p">]))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Proportion: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">round</span><span class="p">(</span><span class="n">target_count</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">/</span> <span class="n">target_count</span><span class="p">[</span><span class="mi">1</span><span class="p">]),</span> <span class="mi">2</span><span class="p">),</span> <span class="s1">&#39;: 1&#39;</span><span class="p">)</span>

<span class="n">target_count</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span><span class="o">=</span><span class="s1">&#39;bar&#39;</span><span class="p">,</span> <span class="n">title</span> <span class="o">=</span> <span class="s1">&#39;Count (target)&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Class 0: 31196
Class 1: 18804
Proportion: 2.0 : 1
</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAYAAAAEVCAYAAADpbDJPAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4zLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvIxREBQAAGcxJREFUeJzt3X+UlNWd5/H3FdRogzaKGuVHJAZnIa6adB4lJzs7TtwYfNY9mJ2MkczoNWPibBbiZM3Z1Tie0UHNMXNOfpDxx9mojJc1EYk/ibkJy7jxZNzFcMVEjGF1QDT0wopAo9CsGvDuH3Vby7a6q2m6+2nqfl7n1Omq73Ofp76l9POp5z5PdZkYIyIikp+Dqm5ARESqoQAQEcmUAkBEJFMKABGRTCkAREQypQAQEcmUAkBkPxhjjjHGPGeMeV/VvfTFGPOAMWZ21X3I6KMAkFHPGPN5Y8yTxphdxpjNxpifGmP+1Qg8bzTGfKjJsKuAf4gxvp7WecwY88Xh7q0vxpjrjDF39yrfBNxYRT8yuikAZFQzxlwBfBf4BnAcMBW4FZhTZV8AxphDAQv03uHuzzbHDtW2esQYVwFHGGM+NtTblgObAkBGLWPMkcACYF6M8YEYY3eM8fcxxh/HGP9zGnOoMea7xphN6fbdtGPGGHOJMebxXtt8+129MeYuY8wtxpifGGN2GmN+aYw5KS37RVrl6XTk8bkGLZ4J7IgxdqZ1bgT+ELg5rXNzqi80xmw0xrxmjFltjPnDun6uM8bcZ4y52xjzGnCJMeYwY4wzxnQZY9YaY/6LMaazbp0TjDH3G2NeMcZsMMZcnuqzgauBz6Xnf7qu18eAfzuo/xHSshQAMpp9HHgf8GA/Y/4amAWcDpwGnAFcsw/PMRf4W2ACsI40VRJj/Ndp+WkxxnExxnsbrPsvged6HsQY/xr4J2B+Wmd+WhRSf0cBPwR+1OucwRzgPqAd+AFwLXAi8EHgU8Cf9ww0xhwE/Bh4GpgEnA181Rjz6Rjjz6gdKd2bnv+0uudYS+2/j8jbFAAymh0NbI0x7ulnzJ8BC2KMW2KMr1DbmV+0D8/xQIxxVXqOH1DbUQ9UO7Cz2aAY490xxm0xxj0xxm8BhwJ/UDdkZYzxoRjjWzHG/wdcAHwjxtiVji6+Vze2AI6JMS6IMb4ZY3wBuB24sEkbO1O/Im8b8vlGkSG0DZhojBnbTwicALxU9/ilVBuo/1t3fzcwbh/W7QLGNxtkjPka8MXUVwSOACbWDdnYa5UTetXq738AOMEYs6OuNobakUd/xgM7moyRzOgIQEazlcDrwPn9jNlEbafYY2qqAXQDh/csMMa8f4j7WwOc3Kv2rj+vm+b7r6T2rn5CjLEdeBUwfa0DbAYm1z2eUnd/I7AhxthedxsfYyz72FaPGdSmjUTepgCQUSvG+CrwN8AtxpjzjTGHG2MONsaca4z5uzTsHuCadD3+xDS+56qcp4EPG2NOT3Pu1+1jCy9Tm4fvyyqg3RgzqZ91xgN7gFeAscaYv6F2BNCfpcDXjTET0rbn1y1bBbxmjLkynSweY4w5xRhT1D3/ielcQb0/An7a5HklMwoAGdVijN8GrqB2YvcVau+A5wMPpSE3AE9Sezf+DPBUqhFjfJ7aVUT/CPwz8K4rggbgOsAZY3YYYy5o0NubwF3UnaQFFgKfTVfwfA9YTm3H+zy16anXee+UT28LgE5gQ+r9PuCN9Jx7gX9H7VzFBmArcAdwZFr3R+nnNmPMUwApHLrT5aAibzP6QhiRwTPGHENt/v0j6QTucDzHl4ELY4x/NMj17wfujDH6oe1MDnQKAJFRxhhzPLVppJXAdOAnwM0xxu9W2pi0HF0FJDL6HAL8V2AatSt3llD79LPIkNIRgIhIpnQSWEQkUwoAEZFMHTAB8OMV/xSpfchFtyG4Pbf+pcp70E23Rjf92xzyW58OmADY/PLWqltoKbu6d1fdgkhD+rc5cg6YABARkaGlABARyZQCQEQkUwoAEZFMKQBERDKlABARyZQCQEQkUwoAEZFM6a+BDrGXtnWzacfrVbfR1C7aWLl+W9VtNHVC+/v4wNFtVbch0pIUAENs047XmXv7E1W30TLu+dIsBYDIMNEUkIhIphQAIiKZajoFVJT2fcAvgEPT+PuCd9cWpZ1G7ZuKjqL2RdwXBe/eLEp7KLAY6AC2AZ8L3r2YtvV14FJgL3B58G55qs+m9mXaY4A7gnc3DemrFBGR9xjIEcAbwCeDd6cBpwOzi9LOAr4JfCd4Nx3oorZjJ/3sCt59CPhOGkdR2pnAhcCHgdnArUVpxxSlHQPcApwLzATmprEiIjKMmh4BBO8isCs9PDjdIvBJ4POp7oDrgNuAOek+wH3AzUVpTaovCd69AWwoSrsOOCONWxe8ewGgKO2SNPa3+/PCRESkfwM6B5Deqf8a2AKsANYDO4J3e9KQTmBSuj8J2AiQlr8KHF1f77VOX3URERlGA7oMNHi3Fzi9KG078CAwo8Gwnm+eMX0s66veKITe8y02W7t2sHrN2oG0W6ld6JLFobSru5vVa7ZU3YaMoOfWv1R1Cy2l49RGu+uaffocQPBuR1Hax4BZQHtR2rHpXf5kYFMa1glMATqL0o4FjgS219V71K/TV/1tEye09/tCRosD4cNVB5JxbW10nDS16jZkhB0Iv+utoOkUUFHaY9I7f4rSHgb8G2At8HPgs2mYBR5O95elx6Tl/yOdR1gGXFiU9tB0BdF0YBUQgOlFaacVpT2E2oniZUPx4kREpG8DOQdwPPDzorRrqO2sVwTvHgGuBK5IJ3OPBu5M4+8Ejk71K4CrAIJ3zwJLqZ3c/RkwL3i3Nx1BzAeWUwuWpWmsiIgMIxNjv18aP2p8/+4H42V//pmq22hq5fpt+lMQQ+ieL83i4ycdXXUbMoJWr1mrKaCh1ej8K6BPAouIZEsBICKSKQWAiEimFAAiIplSAIiIZEoBICKSKQWAiEimFAAiIplSAIiIZEoBICKSKQWAiEimFAAiIplSAIiIZEoBICKSKQWAiEimFAAiIplSAIiIZEoBICKSKQWAiEimFAAiIplSAIiIZEoBICKSKQWAiEimFAAiIplSAIiIZGpsswFFaacAi4H3A28B3w/eLSxKex3wJeCVNPTq4J1P63wduBTYC1wevFue6rOBhcAY4I7g3U2pPg1YAhwFPAVcFLx7c6hepIiIvNdAjgD2AF8L3s0AZgHzitLOTMu+E7w7Pd16dv4zgQuBDwOzgVuL0o4pSjsGuAU4F5gJzK3bzjfTtqYDXdTCQ0REhlHTAAjebQ7ePZXu7wTWApP6WWUOsCR490bwbgOwDjgj3dYF715I7+6XAHOK0hrgk8B9aX0HnD/YFyQiIgPTdAqoXlHaE4GPAL8EPgHML0p7MfAktaOELmrh8ETdap28Exgbe9XPBI4GdgTv9jQY/7atXTtYvWbtvrRbiV20Vd1CS9nV3c3qNVuqbkNG0HPrX6q6hZbSceqMPpcNOACK0o4D7ge+Grx7rSjtbcD1QEw/vwX8BWAarB5pfLQR+xn/LhMntPf7QkaLleu3Vd1CSxnX1kbHSVOrbkNG2IHwu94KBhQARWkPprbz/0Hw7gGA4N3LdctvBx5JDzuBKXWrTwY2pfuN6luB9qK0Y9NRQP14EREZJk3PAaQ5+juBtcG7b9fVj68b9hngN+n+MuDCorSHpqt7pgOrgABML0o7rSjtIdROFC8L3kXg58Bn0/oWeHj/XpaIiDQzkCOATwAXAc8Upf11ql1N7Sqe06lN17wI/CVA8O7ZorRLgd9Su4JoXvBuL0BR2vnAcmqXgS4K3j2btnclsKQo7Q3Ar6gFjoiIDKOmARC8e5zG8/S+n3VuBG5sUPeN1gvevUDtKiERERkh+iSwiEimFAAiIplSAIiIZEoBICKSKQWAiEimFAAiIplSAIiIZEoBICKSKQWAiEimFAAiIplSAIiIZEoBICKSKQWAiEimFAAiIplSAIiIZEoBICKSKQWAiEimFAAiIplSAIiIZEoBICKSKQWAiEimFAAiIplSAIiIZEoBICKSqbHNBhSlnQIsBt4PvAV8P3i3sCjtUcC9wInAi8AFwbuuorQGWAiUwG7gkuDdU2lbFrgmbfqG4J1L9Q7gLuAwwAN/FbyLQ/QaRUSkgYEcAewBvha8mwHMAuYVpZ0JXAU8GrybDjyaHgOcC0xPt8uA2wBSYFwLnAmcAVxblHZCWue2NLZnvdn7/9JERKQ/TQMgeLe55x188G4nsBaYBMwBXBrmgPPT/TnA4uBdDN49AbQXpT0e+DSwIni3PXjXBawAZqdlRwTvVqZ3/YvrtiUiIsOk6RRQvaK0JwIfAX4JHBe82wy1kChKe2waNgnYWLdaZ6r1V+9sUH+XrV07WL1m7b60W4ldtFXdQkvZ1d3N6jVbqm5DRtBz61+quoWW0nHqjD6XDTgAitKOA+4Hvhq8e60obV9DTYNaHET9XSZOaO/3hYwWK9dvq7qFljKurY2Ok6ZW3YaMsAPhd70VDOgqoKK0B1Pb+f8gePdAKr+cpm9IP3vepnUCU+pWnwxsalKf3KAuIiLDqGkApKt67gTWBu++XbdoGdBzGGCBh+vqFxelNUVpZwGvpqmi5cA5RWknpJO/5wDL07KdRWlnpee6uG5bIiIyTAYyBfQJ4CLgmaK0v061q4GbgKVFaS8Ffgf8aVrmqV0Cuo7aZaBfAAjebS9Kez0Q0rgFwbvt6f6Xeecy0J+mm4iIDKOmARC8e5zG8/QAZzcYH4F5fWxrEbCoQf1J4JRmvYiIyNDRJ4FFRDKlABARydQ+fQ5ARA5g2zfAq53Nx1Xs5IN2w4atVbfR3JGT4ahpVXexXxQAIrl4tRPceVV30dT4qhsYKPvIAR8AmgISEcmUAkBEJFMKABGRTCkAREQypQAQEcmUAkBEJFMKABGRTCkAREQypQAQEcmUAkBEJFMKABGRTCkAREQypQAQEcmUAkBEJFMKABGRTCkAREQypQAQEcmUAkBEJFMKABGRTCkAREQy1fRL4YvSLgLOA7YE705JteuALwGvpGFXB+98WvZ14FJgL3B58G55qs8GFgJjgDuCdzel+jRgCXAU8BRwUfDuzaF6gSIi0thAjgDuAmY3qH8neHd6uvXs/GcCFwIfTuvcWpR2TFHaMcAtwLnATGBuGgvwzbSt6UAXtfAQEZFh1jQAgne/ALYPcHtzgCXBuzeCdxuAdcAZ6bYuePdCene/BJhTlNYAnwTuS+s74Px9fA0iIjIITaeA+jG/KO3FwJPA14J3XcAk4Im6MZ2pBrCxV/1M4GhgR/BuT4PxIiIyjAYbALcB1wMx/fwW8BeAaTA20vhII/Yz/j22du1g9Zq1g2p2JO2ireoWWsqu7m5Wr9lSdRst4eSDdjO+6iZayM7u3Tx/AOyTOk6d0eeyQQVA8O7lnvtFaW8HHkkPO4EpdUMnA5vS/Ub1rUB7Udqx6Sigfvy7TJzQ3u8LGS1Wrt9WdQstZVxbGx0nTa26jdawYWvVHbSU8W2H0zFt9O+T+jOoy0CL0h5f9/AzwG/S/WXAhUVpD01X90wHVgEBmF6UdlpR2kOonSheFryLwM+Bz6b1LfDwYHoSEZF9M5DLQO8BzgImFqXtBK4FzipKezq16ZoXgb8ECN49W5R2KfBbYA8wL3i3N21nPrCc2mWgi4J3z6anuBJYUpT2BuBXwJ1D9upERKRPTQMgeDe3QbnPnXTw7kbgxgZ1D/gG9ReoXSUkIiIjSJ8EFhHJlAJARCRTCgARkUwpAEREMqUAEBHJlAJARCRTCgARkUwpAEREMqUAEBHJlAJARCRTCgARkUwpAEREMqUAEBHJlAJARCRTCgARkUwpAEREMqUAEBHJlAJARCRTCgARkUwpAEREMqUAEBHJlAJARCRTCgARkUwpAEREMjW22YCitIuA84AtwbtTUu0o4F7gROBF4ILgXVdRWgMsBEpgN3BJ8O6ptI4FrkmbvSF451K9A7gLOAzwwF8F7+IQvT4REenDQI4A7gJm96pdBTwavJsOPJoeA5wLTE+3y4Db4O3AuBY4EzgDuLYo7YS0zm1pbM96vZ9LRESGQdMACN79AtjeqzwHcOm+A86vqy8O3sXg3RNAe1Ha44FPAyuCd9uDd13ACmB2WnZE8G5lete/uG5bIiIyjAZ7DuC44N1mgPTz2FSfBGysG9eZav3VOxvURURkmDU9B7CPTINaHET9PbZ27WD1mrX70drI2EVb1S20lF3d3axes6XqNlrCyQftZnzVTbSQnd27ef4A2Cd1nDqjz2WDDYCXi9IeH7zbnKZxen5DO4EpdeMmA5tS/axe9cdSfXKD8e8xcUJ7vy9ktFi5flvVLbSUcW1tdJw0teo2WsOGrVV30FLGtx1Ox7TRv0/qz2CngJYBNt23wMN19YuL0pqitLOAV9MU0XLgnKK0E9LJ33OA5WnZzqK0s9IVRBfXbUtERIbRQC4DvYfau/eJRWk7qV3NcxOwtCjtpcDvgD9Nwz21S0DXUbsM9AsAwbvtRWmvB0IatyB413Ni+cu8cxnoT9NNRESGWdMACN7N7WPR2Q3GRmBeH9tZBCxqUH8SOKVZHyIiMrT0SWARkUwpAEREMqUAEBHJlAJARCRTCgARkUwpAEREMqUAEBHJlAJARCRTCgARkUwpAEREMqUAEBHJlAJARCRTCgARkUwpAEREMqUAEBHJlAJARCRTCgARkUwpAEREMqUAEBHJlAJARCRTCgARkUwpAEREMqUAEBHJlAJARCRTY/dn5aK0LwI7gb3AnuDdx4rSHgXcC5wIvAhcELzrKkprgIVACewGLgnePZW2Y4Fr0mZvCN65/elLRESaG4ojgD8O3p0evPtYenwV8GjwbjrwaHoMcC4wPd0uA24DSIFxLXAmcAZwbVHaCUPQl4iI9GM4poDmAD3v4B1wfl19cfAuBu+eANqL0h4PfBpYEbzbHrzrAlYAs4ehLxERqbO/ARCB/16UdnVR2stS7bjg3WaA9PPYVJ8EbKxbtzPV+qqLiMgw2q9zAMAngnebitIeC6woSvu/+xlrGtRiP/V32dq1g9Vr1g6yzZGzi7aqW2gpu7q7Wb1mS9VttISTD9rN+KqbaCE7u3fz/AGwT+o4dUafy/YrAIJ3m9LPLUVpH6Q2h/9yUdrjg3eb0xRPz29vJzClbvXJwKZUP6tX/bHezzVxQnu/L2S0WLl+W9UttJRxbW10nDS16jZaw4atVXfQUsa3HU7HtNG/T+rPoKeAitK2FaUd33MfOAf4DbAMsGmYBR5O95cBFxelNUVpZwGvpimi5cA5RWknpJO/56SaiIgMo/05B3Ac8HhR2qeBVcBPgnc/A24CPlWU9p+BT6XHAB54AVgH3A78R4Dg3XbgeiCk24JUExGRYTToKaDg3QvAaQ3q24CzG9QjMK+PbS0CFg22FxER2Xf6JLCISKYUACIimVIAiIhkSgEgIpIpBYCISKYUACIimVIAiIhkSgEgIpIpBYCISKYUACIimVIAiIhkSgEgIpIpBYCISKYUACIimVIAiIhkSgEgIpIpBYCISKYUACIimVIAiIhkSgEgIpIpBYCISKYUACIimVIAiIhkSgEgIpIpBYCISKbGVt1Aj6K0s4GFwBjgjuDdTRW3JCLS0kbFEUBR2jHALcC5wExgblHamdV2JSLS2kZFAABnAOuCdy8E794ElgBzKu5JRKSljZYpoEnAxrrHncCZ9QNu/+FDd97+w4c6R7SrQTqm6gZayOVfWVp1Cy3m/KobaB2r7gDuqLqLgbgkeHdXowWjJQBMg1qsfxC8++II9SIikoXRMgXUCUypezwZ2FRRLyIiWRgtRwABmF6Udhrwf4ALgc9X25KISGsbFUcAwbs9wHxgObAWWBq8e7barkREWpuJMTYfJSIyzIrSHhq8e6PqPnIyWqaAZAQUpTXAnwEfDN4tKEo7FXh/8G5Vxa1JxorSngHcCRwJTC1KexrwxeDdV6rtrPWNiikgGTG3Ah8H5qbHO6l9AE+kSt8DzgO2AQTvngb+uNKOMqEAyMuZwbt5wOsAwbsu4JBqWxLhoODdS71qeyvpJDOaAsrL79Of3YgARWmPAd6qtiURNqZpoJj+fX4FeL7inrKgI4C8fA94EDi2KO2NwOPAN6ptSYQvA1cAU4GXgVmpJsNMVwFlpijtvwDOpvbp60eDd2srbklEKqIAyEhR2pOAzuDdG0VpzwJOBRYH73ZU25nkrCjt7fT60y8AwbvLKmgnK5oCysv9wN6itB+i9lespgE/rLYlEf4ReDTd/idwLKDPA4wAnQTOy1vBuz1Faf89sDB49/dFaX9VdVOSt+DdvfWPi9L+N2BFRe1kRUcAefl9Udq5wMXAI6l2cIX9iDQyDfhA1U3kQEcAefkC8B+AG4N3G9If37u74p4kc0Vpu3jnHMBBwHbgquo6yodOAotIZdKfJ5lC7a8AQ22aUjulEaIAyEBR2mdocJVFj+DdqSPYjsi7FKVdHbzrqLqPHGkKKA/nVd2ASD9WFaX9aPDuqaobyY2OAESkEkVpx6ar0p4BZgDrgW5qH1KMwbuPVtpgBnQEkJGitLOAv6f2y3YIMAboDt4dUWljkqtVwEfRN9VXRgGQl5upfd3mj4CPUbsc9EOVdiQ5MwDBu/VVN5IrBUBmgnfritKOCd7tBf6hKO3/qronydYxRWmv6Gth8O7bI9lMjhQAedldlPYQ4NdFaf8O2Ay0VdyT5GsMMI50JCAjTwGQl4uofdBmPvCfqF1//SeVdiQ52xy8W1B1EzlTAGSgKO3U4N3v6r516XXgb6vsSQS986+c/hZQHh7quVOU9v4qGxGpc3bVDeROAZCH+ndaH6ysC5E6wbvtVfeQOwVAHmIf90UkY/okcAaK0u7lnU9YHgbsTot6PnGpD4KJZEgBICKSKU0BiYhkSgEgIpIpBYCISKYUACIimVIAiIhk6v8Dinp6ulD6U9cAAAAASUVORK5CYII=
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Dummy-Classifier">Dummy Classifier<a class="anchor-link" href="#Dummy-Classifier">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[42]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="n">X</span><span class="o">.</span><span class="n">shape</span>
<span class="n">y</span><span class="o">.</span><span class="n">shape</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># instantiate and fit a dummy classifier</span>
<span class="n">dummy</span> <span class="o">=</span> <span class="n">DummyClassifier</span><span class="p">(</span><span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>
<span class="n">dummy</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># make predictions</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">dummy</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># SCORING</span>
<span class="c1"># accuracy</span>
<span class="n">dummy_accuracy</span> <span class="o">=</span> <span class="n">dummy</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Dummy Classifier accuracy: </span><span class="si">{:.4f}</span><span class="se">\n\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">dummy_accuracy</span><span class="p">))</span>

<span class="c1"># classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>

<span class="c1"># confusion matrix</span>
<span class="n">cm</span> <span class="o">=</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">y_pred</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">ax</span><span class="o">.</span><span class="n">matshow</span><span class="p">(</span><span class="n">cm</span><span class="p">,</span> <span class="n">cmap</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">Blues</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]):</span>
        <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">j</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">cm</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">],</span> <span class="n">va</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">,</span> <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;predicted label&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;true label&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Dummy Classifier accuracy: 0.5273


             precision    recall  f1-score   support

      False       0.62      0.63      0.62      9379
       True       0.37      0.36      0.36      5621

avg / total       0.53      0.53      0.53     15000

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Logistic-Regression">Logistic Regression<a class="anchor-link" href="#Logistic-Regression">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[43]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># imports</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="k">import</span> <span class="n">LogisticRegression</span>

<span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># instantiate &amp; fit model</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">LogisticRegression</span><span class="p">(</span><span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>
<span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># make predictions on test features</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># score predictions</span>
<span class="n">accuracy</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Logistic Regression Accuracy:</span><span class="se">\t</span><span class="si">{:.4f}</span><span class="se">\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">accuracy</span><span class="p">))</span>

<span class="c1"># classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>

<span class="c1"># confusion matrix</span>
<span class="n">cm</span> <span class="o">=</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">y_pred</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">ax</span><span class="o">.</span><span class="n">matshow</span><span class="p">(</span><span class="n">cm</span><span class="p">,</span> <span class="n">cmap</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">Blues</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]):</span>
        <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">j</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">cm</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">],</span> <span class="n">va</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">,</span> <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;predicted label&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;true label&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Logistic Regression Accuracy:	0.7143

             precision    recall  f1-score   support

      False       0.74      0.84      0.79      9379
       True       0.66      0.50      0.57      5621

avg / total       0.71      0.71      0.70     15000

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h5 id="Logistic-Regression---Tuning">Logistic Regression - Tuning<a class="anchor-link" href="#Logistic-Regression---Tuning">&#182;</a></h5>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[44]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># instantiate the learning algorithm</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">LogisticRegression</span><span class="p">(</span><span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># create a params dict</span>
<span class="n">penalty</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;l1&#39;</span><span class="p">,</span> <span class="s1">&#39;l2&#39;</span><span class="p">]</span>
<span class="n">C</span> <span class="o">=</span> <span class="p">[</span><span class="mf">0.00001</span><span class="p">,</span> <span class="mf">0.0001</span><span class="p">,</span> <span class="mf">0.001</span><span class="p">,</span> <span class="mf">0.01</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">10</span><span class="p">]</span>
<span class="n">hyperparameters</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="n">C</span> <span class="o">=</span> <span class="n">C</span><span class="p">,</span> <span class="n">penalty</span> <span class="o">=</span> <span class="n">penalty</span><span class="p">)</span>

<span class="c1"># instantiate &amp; fit grid search</span>
<span class="n">gridsearch</span> <span class="o">=</span> <span class="n">GridSearchCV</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">hyperparameters</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">5</span><span class="p">,</span> <span class="n">verbose</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>
<span class="n">best_model</span> <span class="o">=</span> <span class="n">gridsearch</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># print the best hyperparameters</span>
<span class="n">best_penalty</span> <span class="o">=</span> <span class="n">best_model</span><span class="o">.</span><span class="n">best_estimator_</span><span class="o">.</span><span class="n">get_params</span><span class="p">()[</span><span class="s1">&#39;penalty&#39;</span><span class="p">]</span>
<span class="n">best_C</span> <span class="o">=</span> <span class="n">best_model</span><span class="o">.</span><span class="n">best_estimator_</span><span class="o">.</span><span class="n">get_params</span><span class="p">()[</span><span class="s1">&#39;C&#39;</span><span class="p">]</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Best penalty: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">best_penalty</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Best C: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">best_C</span><span class="p">))</span>

<span class="c1"># build &amp; fit a tuned model</span>
<span class="n">tuned_model</span> <span class="o">=</span> <span class="n">LogisticRegression</span><span class="p">(</span><span class="n">C</span> <span class="o">=</span> <span class="n">best_C</span><span class="p">,</span> <span class="n">penalty</span> <span class="o">=</span> <span class="n">best_penalty</span><span class="p">)</span>
<span class="n">tuned_model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># make predictions on test features</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">tuned_model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># score predictions</span>
<span class="n">accuracy</span> <span class="o">=</span> <span class="n">tuned_model</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Tuned Accuracy:</span><span class="se">\t</span><span class="si">{:.4f}</span><span class="se">\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">accuracy</span><span class="p">))</span>

<span class="c1"># classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>

<span class="c1"># confusion matrix</span>
<span class="n">cm</span> <span class="o">=</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">y_pred</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">ax</span><span class="o">.</span><span class="n">matshow</span><span class="p">(</span><span class="n">cm</span><span class="p">,</span> <span class="n">cmap</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">Blues</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]):</span>
        <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">j</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">cm</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">],</span> <span class="n">va</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">,</span> <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;predicted label&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;true label&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Best penalty: l2
Best C: 0.01
Tuned Accuracy:	0.7146

             precision    recall  f1-score   support

      False       0.74      0.85      0.79      9379
       True       0.66      0.49      0.56      5621

avg / total       0.71      0.71      0.70     15000

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="LinearSVC">LinearSVC<a class="anchor-link" href="#LinearSVC">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[45]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#imports</span>
<span class="kn">from</span> <span class="nn">sklearn.svm</span> <span class="k">import</span> <span class="n">LinearSVC</span>

<span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># instantiate and fit the learning algorithm</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">LinearSVC</span><span class="p">(</span><span class="n">random_state</span><span class="o">=</span><span class="n">SEED</span><span class="p">)</span>
<span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># make predictions on test features</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># accuracy</span>
<span class="n">accuracy</span> <span class="o">=</span> <span class="n">accuracy_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Accuracy: </span><span class="si">{:.4f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">accuracy</span><span class="p">))</span>

<span class="c1"># classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>

<span class="c1"># confusion matrix</span>
<span class="n">cm</span> <span class="o">=</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">y_pred</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">ax</span><span class="o">.</span><span class="n">matshow</span><span class="p">(</span><span class="n">cm</span><span class="p">,</span> <span class="n">cmap</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">Blues</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]):</span>
        <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">j</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">cm</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">],</span> <span class="n">va</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">,</span> <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;predicted label&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;true label&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Accuracy: 0.7131
             precision    recall  f1-score   support

      False       0.73      0.85      0.79      9379
       True       0.66      0.48      0.56      5621

avg / total       0.71      0.71      0.70     15000

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAW8AAAFzCAYAAADxKIj0AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4zLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvIxREBQAAGkFJREFUeJzt3Xt4FPW9+PF3SLgJQYuKFwQqgiggAWFAEIGKiG7VUlsvqHTQao/Van961NOeeqOFora2qKBY1LrVemlrbRVW25+nVmuLsmqFiqig3EHxyj2YhD1/ZM2JmIS1kl2+4f16Hh+yM5Odz6zx7TDZTIoymQySpLA0K/QAkqTPznhLUoCMtyQFyHhLUoCMtyQFyHhLUoBKCj2AdowoER8H3AQUA3ekU8nrCjySdlFRIr4LOAFYk04lexd6nqbKM+8mIErExcA04HigJzA2SsQ9CzuVdmF3A8cVeoimzng3DQOBRelU8s10KvkR8ADwlQLPpF1UOpV8Gni/0HM0dca7aegILK/1eEV2maQmyng3DUV1LPO+B1ITZrybhhVAp1qPDwBWFWgWSXngu02ahjTQPUrEBwIrgdOBMwo7kqTGVORdBZuGKBEngClUv1XwrnQqOanAI2kXFSXi+4ERwF7A28A16VTyzoIO1QQZb0kKkNe8JSlAxluSAmS8JSlAxluSAmS8JSlAO837vCdNvT/Tr483IPu8Vr+9hv326VDoMYI2euhhhR6hSXj9zaUc3LVLoccIWsVWTmxVwsy61u00Z94frl1b6BGahPLy8kKPIAGwfsOmQo/QpO008ZYk5c54S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KA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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h5 id="LinearSVC---Tuning">LinearSVC - Tuning<a class="anchor-link" href="#LinearSVC---Tuning">&#182;</a></h5>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[46]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># instantiate and fit the learning algorithm</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">LinearSVC</span><span class="p">(</span><span class="n">random_state</span><span class="o">=</span><span class="n">SEED</span><span class="p">)</span>
<span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># make predictions on test features</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># create a params dict</span>
<span class="n">C</span> <span class="o">=</span> <span class="p">[</span><span class="mf">0.00001</span><span class="p">,</span> <span class="mf">0.0001</span><span class="p">,</span> <span class="mf">0.001</span><span class="p">,</span> <span class="mf">0.01</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">10</span><span class="p">]</span>
<span class="n">hyperparameters</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="n">C</span> <span class="o">=</span> <span class="n">C</span><span class="p">)</span>

<span class="c1"># instantiate &amp; fit grid search</span>
<span class="n">gridsearch</span> <span class="o">=</span> <span class="n">GridSearchCV</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">hyperparameters</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">5</span><span class="p">,</span> <span class="n">verbose</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>
<span class="n">best_model</span> <span class="o">=</span> <span class="n">gridsearch</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># print the best hyperparameters</span>
<span class="n">best_C</span> <span class="o">=</span> <span class="n">best_model</span><span class="o">.</span><span class="n">best_estimator_</span><span class="o">.</span><span class="n">get_params</span><span class="p">()[</span><span class="s1">&#39;C&#39;</span><span class="p">]</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Best C: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">best_C</span><span class="p">))</span>

<span class="c1"># build &amp; fit a tuned model</span>
<span class="n">tuned_model</span> <span class="o">=</span> <span class="n">LinearSVC</span><span class="p">(</span><span class="n">C</span> <span class="o">=</span> <span class="n">best_C</span><span class="p">)</span>
<span class="n">tuned_model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># make predictions on test features</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">tuned_model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># score predictions</span>
<span class="n">accuracy</span> <span class="o">=</span> <span class="n">tuned_model</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Tuned Accuracy:</span><span class="se">\t</span><span class="si">{:.4f}</span><span class="se">\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">accuracy</span><span class="p">))</span>

<span class="c1"># classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>

<span class="c1"># confusion matrix</span>
<span class="n">cm</span> <span class="o">=</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">y_pred</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">ax</span><span class="o">.</span><span class="n">matshow</span><span class="p">(</span><span class="n">cm</span><span class="p">,</span> <span class="n">cmap</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">Blues</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]):</span>
        <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">j</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">cm</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">],</span> <span class="n">va</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">,</span> <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;predicted label&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;true label&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Best C: 0.001
Tuned Accuracy:	0.7147

             precision    recall  f1-score   support

      False       0.73      0.86      0.79      9379
       True       0.67      0.47      0.55      5621

avg / total       0.71      0.71      0.70     15000

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="SVC">SVC<a class="anchor-link" href="#SVC">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[47]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.svm</span> <span class="k">import</span> <span class="n">SVC</span>

<span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># instantiate the learning algorithm</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">SVC</span><span class="p">(</span><span class="n">random_state</span><span class="o">=</span><span class="n">SEED</span><span class="p">)</span>

<span class="c1"># create a params dict</span>
<span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># accuracy</span>
<span class="n">accuracy</span> <span class="o">=</span> <span class="n">accuracy_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Accuracy: </span><span class="si">{:.4f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">accuracy</span><span class="p">))</span>

<span class="c1"># classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>

<span class="c1"># confusion matrix</span>
<span class="n">cm</span> <span class="o">=</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">y_pred</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">ax</span><span class="o">.</span><span class="n">matshow</span><span class="p">(</span><span class="n">cm</span><span class="p">,</span> <span class="n">cmap</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">Blues</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]):</span>
        <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">j</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">cm</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">],</span> <span class="n">va</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">,</span> <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;predicted label&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;true label&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Accuracy: 0.7147
             precision    recall  f1-score   support

      False       0.73      0.86      0.79      9379
       True       0.67      0.47      0.55      5621

avg / total       0.71      0.71      0.70     15000

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAW8AAAFzCAYAAADxKIj0AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4zLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvIxREBQAAGXtJREFUeJzt3Xl8FPXB+PFPCIegiTdyKDxQTwgkHANSAREVdIpnrYo+Otqqj7ePeNTHWq9KPdpaVKhaz/Wo9rD+WnU9autZUVetUq2KyE24rIrckpDfH1nTiCSsQnb5hs/79fJFdmZ25jvj8nGc3Z0U1dTUIEkKS4tCD0CS9PUZb0kKkPGWpAAZb0kKkPGWpAAZb0kKUMtCD0AbRhQnBwA3AMXA7Zl06poCD0mbqChO7gRGAQsy6VRZocfTXHnm3QxEcVIMTAAOBHoAo6M46VHYUWkTdjdwQKEH0dwZ7+ZhADAlk05NzaRTnwMPAocUeEzaRGXSqeeBjws9jubOeDcPnYFZ9R7Pzk6T1EwZ7+ahaC3TvO+B1IwZ7+ZhNrBTvcc7ApUFGoukPPDTJs1DBtglipNuwBzgaOCYwg5JUlMq8q6CzUMUJzEwjtqPCt6ZSafGFnhI2kRFcfIAMAzYDpgPXJZJp+4o6KCaIeMtSQHymrckBch4S1KAjLckBch4S1KAjLckBWij+Zz32PEP1PTp7Q3I1tfc+QvouEP7Qg8jaCMH9yr0EJqFyVNnsGv3roUeRtBWreagzVry6NrmbTRn3p8uWlToITQLK1asKPQQJAAWL1lW6CE0axtNvCVJuTPekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4y1JATLekhQg4x2Ah393L6clh3H6CYdx7RUX8vnKlcybO5tzTz2Gk48ZxTWXX8CqVavqln/hb09y6vGHclpyGNdd+cO66T++4FSO/M5eXH7RmYXYDQXupB98n44d2lPeu6xu2qWX/pg+Fb3p17eCA0aOoLKyEoD33nuPHxw/mnZt2/CLX/z8S+sZN+6X9O7Vk/LeZRx7zGhWrFiR1/1oLvIW7yhODoji5P0oTqZEcXJRvrYbuo8WzueRh+5n3K8f4Fd3P8zq1at57m9PcNct4zj0e8dx228eZYuSUp567I8ALJg3h9/dfwc/m3APN6ce5pSzLqxb13ePPoHzLh5bqF1R4I5PTuCx9BNfmnb++Rfwjzcn8fobb/KdUaO46idXArDNNttw3g8vZsx5539p+Tlz5jD+pht55dXXeGvS21RXV/PbBx/M2z40J3mJdxQnxcAE4ECgBzA6ipMe+dh2c1BdXc3nK1dSXVXFypUr2Gbb7Zj0j1cZvPf+AOw78mBefvEZAF569klGHXYUJSWlAGy19bZ166notydt222e/x1QszB06FC22WabL00rLS2t+3np0qUUFRUB0L59e3r07EWrVq2+sp6qqiqWL19OVVUVy5Yto2OnTk078GaqZZ62MwCYkkmnpgJEcfIgcAjwrzxtP1jbbb8Dhx+dcMKRI2jdejP6RoPYedcebL5FCcUta//1bdd+B/790XwAFsyrZMvSUs4/43hWr67mmBNOo//AwYXcBTVzl1zyI+679x623HJLnv7rM40u27lzZ8acdz7d/qsLbdu2Zf/9RzBixIg8jbR5yddlk87ArHqPZ2enaR0WL/6Ml198hjsffJx7//g0K1Ys5/VXXlzLkrVnPNXV1VTOnsk1N9zBhZdey40/u5wliz/L76C1SbnqqrFMnzGL0cccy4QJ4xtd9pNPPuHPf/4TUz6cxqzZlSxdupT777svTyNtXvJ15l20lmk19R8sXrqUaTNm5mk44Xjj1RfZvGQrPl60hI8XLWGXHhW88vKLfLZoEVOmTqO4uJipH7xL281LmDZjJq3bbs639ujNrDlzAdh2+w689tqrdO2+KwBz589n2bLlHutGvF6ar78W4amsnMPyFSt5fdK7X5lXVhEx5uzTOOjwowGYPHUGc+cvpO3ipXXL//UvT1BSujUz537EzLkf0af/nvz50cfYvXe/vO5HKHqX7dHgvHy9SmcDO9V7vCNQWX+Bks03p1vXLnkaTjhWLi3j6Ud/T8cdtqdNm814eMYUepaVU1NdxZxp77H3vgfy2B9S7LPfgXTr2oVBg/fh/X++Rreu32fRp5/w8cL59O3bn9IttwJg8cfzadeurce6Ef16N/wXZlO3bWlb2m7Wpu4YffDBB+yyyy4AjH/+aSrKy790/CbvsD1bbLFF3bSq5Z9x3923s8fOXWnbti3jr7+GIYO/7TFvwKrVDc/LV7wzwC5RnHQD5gBHA8fkadtB271Hb/baez/OOfkoiouL6b7zHhx40BFEg4Zy3RUXcu8d4+m+8+6M/M7hAOzRqy+VM6Zw6vGH0qJFC75/2pi6cF94ZsKsmdNZsXwZxx+xH+dceAX9BuxVyN1TQI49ZjTPPfcsH330EV277Mhll13B44+nmTz5fVq0aEGXLl351c23ADBv3jxGjdyHFcuX0aJFC268YRz/fPtfDBw4kMO/ewRR/760bNmSioo+nHzyKQXeszAV1dTUrHupDSCKkxgYBxQDd2bSqS99Zu2CsbfU7DPEkKyvaTNmela9nkYO7lXoITQLr0961zPq9bRqNQdt1pJH1zYvbxf3MulUGkjna3uS1Jz5DUtJCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAGW9JCpDxlqQAtWxoRhQnLwA161pBJp0aukFHJElapwbjDdyet1FIkr6WBuOdSadS+RyIJCl3jZ1514nipAg4CRgNbJdJp3pHcTIU6JBJp37XlAOUJH1Vrm9YXgn8APg10CU7bTbww6YYlCSpcbnG+wRgVCadepD/vIk5DejeFIOSJDUu13gXA0uyP38R7y3qTZMk5VGu8U4D10dx0gbqroH/BHikqQYmSWpYrvEeA3QCFgFbUnvG3RWveUtSQeT0aZNMOvUZcGgUJ+2pjfasTDo1r0lHJklqUM5fj4/iZCtgf2AYsG8UJ1s31aAkSY3LKd5RnAwHpgNnAxFwFjAtipN9m25okqSG5HTZBBgPnFL/CzlRnHwPmADs3hQDkyQ1LNfLJp2Ah9aY9jDQYcMOR5KUi1zjfQ9wxhrTTstOlyTlWa63hG0BnBbFyYXAHKAzsAPwcpOPUJL0FV/nlrC3NeVAJEm585awkhSgXD9tQhQnOwADgO2Aoi+mZ9KpO5tgXJKkRuR6P+9DgfuAD4CewDtAGfAiYLwlKc9y/bTJVcCJmXSqD7A0++cpwOtNNjJJUoNyjXeXTDr1+zWmpYDjN/B4JEk5yDXeC7LXvAGmR3EyCPgWtff5liTlWa7xvg0YnP35l8AzwFvAr5piUJKkxuV6S9hr6/18TxQnzwKbZ9Kpd5tqYJKkhuX8UcH6MunUzA09EElS7hr7evws/vP1+AZl0qku61omFzt22o5B/bxB4fpqtxmU9/Q4ro+lK6sKPYRmYcWqao/lepq2cDnlXUrWOq+xM+//bprhSJLWV2Nfj38unwORJOUu51+DJknaeBhvSQqQ8ZakAH2teEdx0iKKk45NNRhJUm5yvavgVtR+m/IIYBWweRQnBwMDMunUJU04PknSWuR65n0LsAjoCnyenTYROKopBiVJalyu8d4XODuTTs0l+8WdTDq1EGjfVAOTJDUs13gvovY36NSJ4qQLMHeDj0iStE65xvt24KEoTvYBWmRvCZui9nKKJCnPcr0x1bXACmAC0IraX312K3BDE41LktSIXG8JWwOMy/4jSSqwXD8qOLyheZl06m8bbjiSpFzketnkjjUebw+0BmYD3TfoiCRJ65TrZZNu9R9HcVIMXAIsbopBSZIa943ubZJJp6qBscCFG3Y4kqRcrM+NqfYHVm+ogUiScpfrG5Zr/kq0dsBmwOlNMShJUuNyfcNyzV+JthSYnEmnPtvA45Ek5WCd8c6+OXkFMDKTTq1s+iFJktZlnde8s29OdstlWUlSfuR62eQK4OYoTi6j9rPddde/M+mUb1pKUp7lGu/bs38eV29aEbURL96gI5IkrVOu8e627kUkSfmSa7y/l0mnfr7mxChOxgDXb9ghSZLWJdc3IS9tYLq/v1KSCqDRM+96dxMszv4ihqJ6s7vjvU0kqSDWddnki7sJbkbtL2D4Qg0wDzirKQYlSWpco/H+4m6CUZzck0mnjs/PkCRJ65LTNW/DLUkbF781KUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt6SFCDjLUkBMt4budmzZ3HwgfszsG8vBvUv55YJNwHw9j/fYsTwIew1oA+jv3con332Wd1z3nl7EiOGD2FQ/3L2GtCHFStWAHDV5T+mbLfu7LTD1gXZF4Vt9uxZjDpgP6I+vRjYr5ybJ9xYN+/Wm8fTr7wnA/uV8+MfXVQ3/e1/TmK/YYMZ2K+cQVFF3WvxH2+8zqCogoqy3bnwvP+lpqYm7/sTupb52EgUJ3cCo4AFmXSqLB/bbC5atmzJT66+jvKKPixevJjhQwYybPi+nHPGqVw59lr2GjKU++65m5vG/YIfXXoF1VVVnHHKCdxy+12U9Srn43//m1atWgEwMh7FSaeeTlTeo8B7pRC1LG7JVVdfR0WfvixevJi99xrIPsP3Y8GCBTz26CO89OobtGnThoULFgBQVVXF6ack3Hr73fTq/eXX4phzzuSG8TcTDdiTIw49iKefepL9Rx5QyN0LTr7OvO8G/DfzDXTo0JHyij4AlJSUsOtuuzN3biUffDCZbw8eAsCw4fvyyJ8eBiDzykR6lvWirFc5ANtsuy3FxcUARAMG0qFDxwLshZqDDh07UtGnL1D7Wtxtt92prKzkjttu5dzzLqRNmzYAbN++PQCvvfISPct60av3l1+L8+bOZfHixQwYOIiioiJGH/vfPPrInwqzUwHLS7wz6dTzwMf52FZzNnPGdCa99Rb9+g9gjx49efyxRwD408MPUTlnNgCzZ06nqKiI7x7yHYbtNYAbf/nzQg5ZzdSMGdOZ9Nab9I8G8OEHk5n49xcZPvTbxCOG8/prGQBmzZxBUVERhx0cM2RQxLjra1+LlZVz6NS5c926OnXekbmVlQXZj5Dl5bKJ1t+SJUtIjj2Kn177c0pLS7npV7/mogvG8LNrxnJAPIpWrVsDUF1dzcsTX+Kvz71E23btOHTUSMor+rL3PsMLvAdqLpYsWcJxo4/k6ut+QWlpKVXV1Xz66Sf89bm/88ZrGU447hgm/Wsy1dXVTHzpJZ59YSJt27Xj4HgEFX36UlJS8pV1FhUVFWBPwrbRxPuTTxbx1jvvFXoYG6WqqlX835iz+Pbe+9Jl5z3qjtNlV18PwKyZ09mhQyfeeuc9VhcVs0dZb2bP/wiAXhX9eeLJJ9mqfae69VWvXu2xbkQLQ9KgqqpVXHTumeyVfS2++fZ7lJRuxR69+/HWO+9T3LaUqqoqnntxItUU06OsN7PmZV+Lffrz+BNPMuLAUUybOpU33659Db708qu02qxt3WP9x5Y7dG1w3kYT76233pLynrsXehgbnZqaGk4/5fv069ePsWN/Wjd94YIFbN++PatXr+aWcddy+plnU95zdxYfdAiXnH8mu3TrQuvWrZk6+V1Oy877QnGLFh7rRhS3MN5rU1NTw6knn0j//v24+uqr66YfPXo0lTM+5MTkOKZ8MJkiYO/BgyguLubi855i1+61r8UPJ7/LGWeew77DhrDtttuyatmn9I8G8pMfnc//nHYGFWW+Jtc0beHyBuf5UcGN3CsTX+K3D9zPC889w9BB/Rk6qD9/efJxHvr9b4kqejCwbxkdOnbk2OMSAEpKSzn9rHPYd+gghg7qT++KCkYcEANw2SUX0XPXbixbtoyeu3bjmrFXFnLXFJiXJ/6dB39zP88/9wyDB/Zj8MB+PPXE4xyXnMj06VPZs38FJx5/LDffdidFRUWUlG7JmWf/L/sMGcTgPftTXtGHkQfWvhavv2E8Z51+KhVlu9Ote3c/afINFOXj85VRnDwADAO2A+YDl2XSqTvqL3PDXX+oOf7IQ5p8LM3dW++851n1evLMe8N48+33PJteT9MWLj+ovEvJo2ubl5fLJpl0anQ+tiNJmwovm0hSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgIpqamoKPQYAoji5HZhd6HFI0kZkeiadunttMzaaeEuScudlE0kKkPGWpAAZbwUvipO7ozi5KvvzkChO3s/TdmuiONm5gXnPRnFyUo7rmR7FyX7fcAzf+LkKW8tCD0DakDLp1AvAbutaLoqTE4CTMunU4CYflNQEPPPWRiWKE08opBz4F0VNLoqT6cCtwHFAR+D/Aadl0qkVUZwMA+4DbgLOBf4CHBfFySjgKuC/gH8Bp2bSqUnZ9fUB7gB2AdJATb1tDQPuy6RTO2Yf7wTcAAyh9mTlAWACcAvQKoqTJUBVJp3aKoqTNsBY4EigDfAwcG4mnVqeXdcFwJjs9i75Gvv/LeA2oDz73CeBMzLp1Kf1F4vi5MY1j0/2+Q0eC226PPNWvhwLjAS+BezKl+PXAdgG6AqcEsVJX+BO4H+AbakN/5+jOGkTxUlrauN2b/Y5vwe+u7YNRnFSDDwKzKA2fJ2BBzPp1LvAqcDETDq1RSad2ir7lGuzY6sAds4uf2l2XQcA5wP7U/sfja9znbkIuBroBOwB7ARcnsvxaexYfI3tqxnyzFv5Mj6TTs0CiOJkLLVn2l8EfDVwWSadWpmdfzJwayadeiU7PxXFycXAntSeubYCxmXSqRrgD1GcjGlgmwOoDeYFmXSqKjvtxbUtGMVJEXAy0DuTTn2cnfZT4DfA/1F7Nn5XJp16OzvvcmB0LjueSaemAFOyDxdGcXI9cNkaizV0fBo7Fs/lsn01T8Zb+TKr3s8zqI3qFxZ+cYkgqyuQRHFyVr1prbPPqQHmZMNdf31rsxMwo164G7M90A54PYqTL6YVAcXZnzsBr+ewza+I4qQ9cCO1l25KqP0/3k/WWKyh49PYsdAmzHgrX3aq93MXoLLe4zW/5jsLGJtJp8auuZIoTvYGOkdxUlQv4F2AD9eyzVlAlyhOWq4l4Gtu8yNgOdAzk07NWcu65q5lH3J1dXZ7vTPp1L+jODkUGL/GMg0dnwaPhTZtxlv5ckYUJ48Cy4CLgd82suxtwMNRnDwNvErtGfEw4HlgIlAFnB3FyQTgYGovjzyzlvW8Sm10r4ni5DKgGuiXSaf+DswHdozipHUmnfo8k06tjuLkNuCXUZycmUmnFkRx0hkoy6RTTwK/A+6K4uQeYDpfvezRmBJgEfBpdp0XrGWZho5Pg8cik04t/hpjUDPjG5bKl98ATwFTs/9c1dCCmXTqNWqv9Y6n9vLCFOCE7LzPgcOzjz8BjgL+2MB6qoGDqH3zcSa1Nz47Kjv7b8A7wLwoTj7KTvthdlsvR3HyGfA02c+MZ9Kpx4Fx2edNyf6ZqyuAvtQG/LEGxrvW49PYsdCmzRtTqcllPyp4UiaderrQY5GaC8+8JSlAxluSAuRlE0kKkGfekhQg4y1JATLekhQg4y1JATLekhQg4y1JAfr/dOo347QstLoAAAAASUVORK5CYII=
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h5 id="SVC---Tuning">SVC - Tuning<a class="anchor-link" href="#SVC---Tuning">&#182;</a></h5>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[48]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.svm</span> <span class="k">import</span> <span class="n">SVC</span>

<span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>


<span class="c1"># instantiate the learning algorithm</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">SVC</span><span class="p">(</span><span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># create a params dict</span>
<span class="n">C</span> <span class="o">=</span> <span class="p">[</span><span class="mi">100</span><span class="p">,</span> <span class="mi">150</span><span class="p">,</span> <span class="mi">200</span><span class="p">,</span> <span class="mi">300</span><span class="p">]</span>
<span class="n">gamma</span> <span class="o">=</span> <span class="p">[</span><span class="mf">0.00001</span><span class="p">,</span> <span class="mf">0.0001</span><span class="p">,</span> <span class="mf">0.001</span><span class="p">,</span> <span class="mf">0.01</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">]</span>
<span class="n">hyperparameters</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="n">C</span> <span class="o">=</span> <span class="n">C</span><span class="p">,</span> <span class="n">gamma</span> <span class="o">=</span> <span class="n">gamma</span><span class="p">)</span>

<span class="c1"># instantiate &amp; fit grid search</span>
<span class="n">gridsearch</span> <span class="o">=</span> <span class="n">GridSearchCV</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">hyperparameters</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">5</span><span class="p">,</span> <span class="n">verbose</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>
<span class="n">best_model</span> <span class="o">=</span> <span class="n">gridsearch</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># print the best hyperparameters</span>
<span class="n">best_gamma</span> <span class="o">=</span> <span class="n">best_model</span><span class="o">.</span><span class="n">best_estimator_</span><span class="o">.</span><span class="n">get_params</span><span class="p">()[</span><span class="s1">&#39;gamma&#39;</span><span class="p">]</span>
<span class="n">best_C</span> <span class="o">=</span> <span class="n">best_model</span><span class="o">.</span><span class="n">best_estimator_</span><span class="o">.</span><span class="n">get_params</span><span class="p">()[</span><span class="s1">&#39;C&#39;</span><span class="p">]</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Best gamma: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">best_gamma</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Best C: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">best_C</span><span class="p">))</span>


<span class="c1"># BUILD MODEL WITH BEST HYPERPARAMETERS</span>

<span class="c1"># instantiate &amp; fit model</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">SVC</span><span class="p">(</span><span class="n">gamma</span> <span class="o">=</span> <span class="n">best_gamma</span><span class="p">,</span> <span class="n">C</span> <span class="o">=</span> <span class="n">best_C</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>
<span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># make predictions</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># accuracy</span>
<span class="n">accuracy</span> <span class="o">=</span> <span class="n">accuracy_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Accuracy: </span><span class="si">{:.4f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">accuracy</span><span class="p">))</span>

<span class="c1"># classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>

<span class="c1"># confusion matrix</span>
<span class="n">cm</span> <span class="o">=</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">y_pred</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">ax</span><span class="o">.</span><span class="n">matshow</span><span class="p">(</span><span class="n">cm</span><span class="p">,</span> <span class="n">cmap</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">Blues</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]):</span>
        <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">j</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">cm</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">],</span> <span class="n">va</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">,</span> <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;predicted label&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;true label&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Best gamma: 0.1
Best C: 300
Accuracy: 0.7585
             precision    recall  f1-score   support

      False       0.78      0.85      0.81      9379
       True       0.71      0.61      0.65      5621

avg / total       0.75      0.76      0.75     15000

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Decision-Tree">Decision Tree<a class="anchor-link" href="#Decision-Tree">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[49]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># imports</span>
<span class="kn">from</span> <span class="nn">sklearn.tree</span> <span class="k">import</span> <span class="n">DecisionTreeClassifier</span>

<span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># instantiate &amp; train a DecisionTreeClassifier</span>
<span class="n">dt</span> <span class="o">=</span> <span class="n">DecisionTreeClassifier</span><span class="p">(</span><span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>
<span class="n">dt</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># make predictions</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">dt</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># SCORING</span>
<span class="c1"># accuracy</span>
<span class="n">accuracy_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">)</span>

<span class="c1"># classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>

<span class="c1"># confusion matrix</span>
<span class="n">cm</span> <span class="o">=</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">y_pred</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">ax</span><span class="o">.</span><span class="n">matshow</span><span class="p">(</span><span class="n">cm</span><span class="p">,</span> <span class="n">cmap</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">Blues</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]):</span>
        <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">j</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">cm</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">],</span> <span class="n">va</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">,</span> <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;predicted label&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;true label&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>             precision    recall  f1-score   support

      False       0.76      0.77      0.76      9379
       True       0.61      0.60      0.60      5621

avg / total       0.70      0.70      0.70     15000

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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UrEUGu/R2Ux65eoLozgZC0xYuyNJktak0Bchz29kuT+/UpJaQJNn3vU+TbA8/4MYyuqt3hY/20SSWsSaLpt8/mmCG1P7Axg+lwM+BM5ojqEkSU1rMt6ff5pgFCd3ZjPpd4ozkiRpTQq65m24JWnd4ndNSlKAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjLckBch4S1KAjPc6bvbs2Qwbtje9e+1E3z69ue66awE477xz6bVTT/rtsjPfGjWKBQsWrHK/WbNmsVm7tlx11ZUAvPHGG/Sv7Ff362vtN+Paa68p+vNRuKqqqhi+524M2bU/gwfszKWXXATAGaeeyJBd+7P7oEqSY45g0aJFAEy6+ufsMXgAewweQLTLTmzTaYtVHu+zzz6j1/bbcN7YM4v+XEpBRTF2EsXJbcABwEfZTNq7GPssFRUVFVxxxZVUVlaycOFCBkYDGD58BMOHj2D8+EupqKjgRz/6IZdddimXXXZ53f3OGTuWkSP3q7u94447Mm368wCsWLGCrl06c8ghhxb9+ShcG220EQ/+7lHatGlDdXU1+40YyvB9RjLusitp164dAD/50bncctP1nHXOeZx29nns3KsHAL+4YRIvvfTCKo83/uIL2W33IUV/HqWiWGfedwAji7SvktKxY0cqKysBaNu2LT169GTu3Lnss88+VFTU/tu766BdmTtnbt19/u/BB+m2bTd26rVTg4/5xBNPsG337my99dbN/wRUMsrKymjTpg0A1dXV1FRXU1ZWVhfuXC5H1dKllJWVfeG+9937G741+oi62y88P52PP5rHXsNGFGf4ElSUeGcz6dPA/GLsq5TNnDmTF154nkGDBq2y/Pbbb2fkyNp/G5cuXcLPr/g5559/QaOPc89v7ubII49s1llVmlasWMEegwewY7dODN17GAOigQCcdvIJ9Ni2C2+9+QbfO/m0Ve4ze9Z7zJo5kz323AuAlStX8rP/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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h5 id="Decision-Tree---Tuning">Decision Tree - Tuning<a class="anchor-link" href="#Decision-Tree---Tuning">&#182;</a></h5>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[50]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># instantiate the learning algorithm</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">DecisionTreeClassifier</span><span class="p">()</span>

<span class="c1"># create a params dict</span>
<span class="n">depth</span> <span class="o">=</span> <span class="p">[</span><span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">6</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">15</span><span class="p">,</span> <span class="mi">20</span><span class="p">]</span>
<span class="n">min_samples</span> <span class="o">=</span> <span class="p">[</span><span class="o">.</span><span class="mi">01</span><span class="p">,</span> <span class="o">.</span><span class="mi">025</span><span class="p">,</span> <span class="o">.</span><span class="mi">05</span><span class="p">,</span> <span class="o">.</span><span class="mi">075</span><span class="p">,</span> <span class="o">.</span><span class="mi">1</span><span class="p">,</span> <span class="o">.</span><span class="mi">2</span><span class="p">]</span>
<span class="n">hyperparameters</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="n">max_depth</span> <span class="o">=</span> <span class="n">depth</span><span class="p">,</span> <span class="n">min_samples_leaf</span> <span class="o">=</span> <span class="n">min_samples</span><span class="p">)</span>

<span class="c1"># instantiate grid search</span>
<span class="n">gridsearch</span> <span class="o">=</span> <span class="n">GridSearchCV</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">hyperparameters</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">5</span><span class="p">,</span> <span class="n">verbose</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="c1"># fit grid search</span>
<span class="n">best_model</span> <span class="o">=</span> <span class="n">gridsearch</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># print the best hyperparameters</span>
<span class="n">best_depth</span> <span class="o">=</span> <span class="n">best_model</span><span class="o">.</span><span class="n">best_estimator_</span><span class="o">.</span><span class="n">get_params</span><span class="p">()[</span><span class="s1">&#39;max_depth&#39;</span><span class="p">]</span>
<span class="n">best_min_samples</span> <span class="o">=</span> <span class="n">best_model</span><span class="o">.</span><span class="n">best_estimator_</span><span class="o">.</span><span class="n">get_params</span><span class="p">()[</span><span class="s1">&#39;min_samples_leaf&#39;</span><span class="p">]</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Best max_depth: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">best_depth</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Best min_samples_leaf: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">best_min_samples</span><span class="p">))</span>


<span class="c1"># RUN MODEL WITH BEST HYPERPARAMETERS</span>

<span class="c1"># instantiate a DecisionTreeClassifier</span>
<span class="n">tuned_model</span> <span class="o">=</span> <span class="n">DecisionTreeClassifier</span><span class="p">(</span><span class="n">max_depth</span> <span class="o">=</span> <span class="n">best_depth</span><span class="p">,</span>
                                     <span class="n">min_samples_leaf</span> <span class="o">=</span> <span class="n">best_min_samples</span><span class="p">,</span>
                                     <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># train the model</span>
<span class="n">tuned_model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># make predictions</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">tuned_model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># score accuracy</span>
<span class="n">tuned_model_accuracy</span> <span class="o">=</span> <span class="n">accuracy_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Tuned Decision Tree Accuracy:</span><span class="se">\t</span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">tuned_model_accuracy</span><span class="p">))</span>

<span class="c1"># classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>

<span class="c1"># confusion matrix</span>
<span class="n">cm</span> <span class="o">=</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">y_pred</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">ax</span><span class="o">.</span><span class="n">matshow</span><span class="p">(</span><span class="n">cm</span><span class="p">,</span> <span class="n">cmap</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">Blues</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]):</span>
        <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">j</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">cm</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">],</span> <span class="n">va</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">,</span> <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;predicted label&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;true label&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Best max_depth: 10
Best min_samples_leaf: 0.01
Tuned Decision Tree Accuracy:	0.758
             precision    recall  f1-score   support

      False       0.81      0.81      0.81      9379
       True       0.68      0.67      0.68      5621

avg / total       0.76      0.76      0.76     15000

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[57]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># calculate feature importances</span>
<span class="n">importances</span> <span class="o">=</span> <span class="n">tuned_model</span><span class="o">.</span><span class="n">feature_importances_</span>

<span class="c1"># sort feature importances in descending order</span>
<span class="n">indices</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">argsort</span><span class="p">(</span><span class="n">importances</span><span class="p">)[::</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>

<span class="c1"># rearrange feature names so they match the sorted feature importances</span>
<span class="n">names</span> <span class="o">=</span> <span class="p">[</span><span class="n">X</span><span class="o">.</span><span class="n">columns</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">indices</span><span class="p">]</span>

<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">15</span><span class="p">,</span> <span class="mi">9</span><span class="p">))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="n">X</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]),</span> <span class="n">importances</span><span class="p">[</span><span class="n">indices</span><span class="p">])</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xticks</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="n">X</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]),</span> <span class="n">names</span><span class="p">,</span> <span class="n">rotation</span> <span class="o">=</span> <span class="mi">90</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA2YAAAJ+CAYAAADYJxO8AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4zLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvIxREBQAAIABJREFUeJzs3Xu8ZnVdL/DPACo5XlC0EhEkJI0KTVxK6bFIPemyvKQmmJ2leVAzlPLkUdOs8JzyUhaaaQcvrUrBe6IuUywvJwVb4oXCSwmC4ljmHEcBHQWd88daGx7GPcwe5tnzm7Xm/X699mv2evazH76LvffzPJ/f+v2+vw3btm0LAAAA5exXugAAAIB9nWAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQ2B4NZm87+/9uS7LPfHzmwkuK1+DcnJtzm/7HnM9t7ufn3Kb54dym+eHcpvkx53O7jo9V7dFg9qX/+Mqe/M8Vd/kV3yhdwrpxbtPk3KZpzueWzPv8nNs0Obdpcm7TNOdz21WmMgIAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABR2QOkC9gaXbL4im7ZsXfrjXp6NOefCzUt/3EMOOjCHH7xx6Y8LAACUIZgl2bRla048/dzSZazZGScdJ5gBAMCMmMoIAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQmGAGAABQ2AFruVNVN/dPclqS/ZO8ou/a5+3gfg9P8oYkVd+1H1lalQAAADO20ytmVd3sn+SlSR6Q5OgkJ1Z1c/Qq97tpkqck+fCyiwQAAJiztUxlvHuSz/Zde1Hftd9OcmaSB69yv+cmeUGSrUusDwAAYPbWMpXxtkm+sHB8aZJ7LN6hqpufSHK7vmvfXtXNb+3ogb7y1S057/xPXa9C19Pl2Vi6hF1y+RVX5Lzzv1y0hs9ceEnR//56cm7T5Nyma87n59ymyblNk3Obpjmf244ce8yPrHr7WoLZhlVu27bySVU3+yX5kySP2dkD3eoWB+2wkJLOuXBz6RJ2yU02bsyxRx5Wuoy98me5LM5tmpzbdM35/JzbNDm3aXJu0zTnc9sVa5nKeGmS2y0cH5pk08LxTZP8WJL3VXVzcZLjkpxV1c3dllUkAADAnK3lilmf5Kiqbo5I8sUkJyR51NVf7NqvJbnVynFVN+9L8lu6MgIAAKzNTq+Y9V17VZKTk7wryaeSvL7v2guqujm1qpsHrXeBAAAAc7emfcz6ru2SdNvd9pwd3Pdndr8sAACAfcda1pgBAACwjgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwgQzAACAwg5Yy52qurl/ktOS7J/kFX3XPm+7rz8xya8n+U6Sy5M8vu/aTy65VgAAgFna6RWzqm72T/LSJA9IcnSSE6u6OXq7u72279of77v2LklekORFS68UAABgptYylfHuST7bd+1Ffdd+O8mZSR68eIe+a7++cLgxybbllQgAADBva5nKeNskX1g4vjTJPba/U1U3v57kqUlumORnl1IdAADAPmAtwWzDKrd9zxWxvmtfmuSlVd08KsmzkzTb3+crX92S887/1C4Xud4uz8bSJeySy6+4Iued/+WiNXzmwkuK/vfXk3ObJuc2XXM+P+c2Tc5tmpzbNM353Hbk2GN+ZNXb1xLMLk1yu4XjQ5Nsuo77n5nkZat94Va3OGiHhZR0zoWbS5ewS26ycWOOPfKw0mXslT/LZXFu0+TcpmvO5+fcpsm5TZNzm6Y5n9uuWMsasz7JUVXdHFHVzQ2TnJDkrMU7VHVz1MLhA5P82/JKBAAAmLedXjHru/aqqm5OTvKuDO3yX9V37QVV3Zya5CN9156V5OSqbu6b5MokX80q0xgBAABY3Zr2Meu7tkvSbXfbcxY+P2XJdQEAAOwz1jKVEQAAgHUkmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEAABQmmAEA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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Random-Forest">Random Forest<a class="anchor-link" href="#Random-Forest">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[58]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="k">import</span> <span class="n">RandomForestClassifier</span>

<span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># instantiate &amp; fit</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">RandomForestClassifier</span><span class="p">(</span><span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>
<span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># make predictions on the test set</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>

<span class="c1"># confusion matrix</span>
<span class="n">cm</span> <span class="o">=</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">y_pred</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">ax</span><span class="o">.</span><span class="n">matshow</span><span class="p">(</span><span class="n">cm</span><span class="p">,</span> <span class="n">cmap</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">Blues</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]):</span>
        <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">j</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">cm</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">],</span> <span class="n">va</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">,</span> <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;predicted label&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;true label&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>             precision    recall  f1-score   support

      False       0.77      0.80      0.79      9379
       True       0.65      0.61      0.63      5621

avg / total       0.73      0.73      0.73     15000

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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SVs//xYHYuHChRz2g4O57PIr2GSTTeqXX3LxRVRWVnLY4T8EoLa29jP3zeVypA+MpX37DgzYaaeSzazWp6KignETMia/Po0XJ77AhPFPc9+993DsT05Y7cd69913mPraq+yx514tMGnrV1nuAZb78KP5vPjK6+UeY61UvXQpp//seAbvMZTu2/Stf53S+//KvX/5C9eOuYWXXn0DgPXW35DnX3iJPv13BmDq628waPc9Gf+3h/nbA/dz3333sWTJYj755BO+9739+fXIUWV7XmurT5fUrHojsU3vvtxz99384803+Pq2vQD49N//Zodtt+F///IA/5w+E4CP5s1nxqzZTH7tjRXuf/efbucbg3dn6pvTSj57KHKbdm5y3VoT780325QB2/tG2spqa2s55qgRDIx2rn9TEuDhh/7GX+68nUcee4L27dvXLz/g+99n1AW/ZNQlFzFnzhzmvvcORxx2MMkRhwI3AvDkk+O46orLuff/fIe/MQsWVZd7hLXSB++/z/rrr8+m7drx6aef8vprkzn5lNO47Mqr6rfp0XFzXp76Vv3t/v16s1m7TenRrQv9+/Ve4fHOfHoc557/m88s13+8UrWgyXVrTbzVuAl//zt//MPtbLfd9gzcqe6NywsuvJBTT/k5ixcvZr999gbq3rQcff0NbLX1Nhx08MF8vf92VFZWcvU111JRUVHOp6BW4r333uXE/zqGZTU1LFu2jP0PHM5e++7X5PavT3mVIw7cl/nzPuLhBx/g0pEXMD6bBMDMGdOZPbuKQYN3K9X4rU6usXOka1oUJ3cAQ4AtgfeA87I0f0vDba7//T21xxx+QIvP0tq9+Mrr/g/mC/LIe82Y/NobHlV/Qa9ULfjuHn22GNvYupIceWdp/rBS7EeS1hV+2kSSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSAmS8JSlAxluSApSrra0t9wwARHFyM1BV7jkkaS0yPUvztzW2Yq2JtySpeJ42kaQAGW9JCpDxVvCiOLktipMLC1/vGsXJGyXab20UJ9s0sW5cFCfHFvk406M42fNzzvC576uwVZZ7AGlNytL800DvVW0XxckI4NgszQ9u8aGkFuCRt9YqUZx4QCEVwb8oanFRnEwHbgR+BHQC/gr8NEvzi6I4GQLcDlwLnAI8AvwoipPvABcCXwWmAD/J0vzkwuPtCNwC9AJSoLbBvoYAt2dpvmvhdjfgamBX6g5W7gCuA8YA60dxshCoztJ8uyhO2gAjgR8AbYB7gVOyNP9p4bHOAE4t7O/c1Xj+WwM3ATsU7vsQcEKW5uc13CyKk2tWfn0K92/ytdC6yyNvlcoPgb2BrYGvsWL8OgKbAz2AH0dxMgC4FfgvYAvqwn9fFCdtojjZgLq4/W/hPncBBzW2wyhOKoCxwAzqwtcFuDNL81OBnwDPZGl+oyzNtyvcZVRhtq8D2xS2/1XhsfYBTgeGUfePxuqcZ84BFwOdgW2BbsCvi3l9mnstVmP/aoU88lapjM7S/CyAKE5GUnekvTzgy4DzsjS/uLD+OODGLM0/V1ifj+LkF8A3qDtyXR+4KkvztcBfojg5tYl9DqQumGdkab66sGx8YxtGcZIDjgP6Z2n+w8Kyi4A/AudQdzT+uyzNv1pY92vgsGKeeJbm3wLeKtx8P4qTK4DzVtqsqdenudfiyWL2r9bJeKtUZjX4egZ1UV3u/eWnCAp6AEkUJyc1WLZB4T61wOxCuBs+XmO6ATMahLs57YG2wMQoTpYvywEVha87AxOL2OdnRHHSAbiGulM3G1P3P96PVtqsqdenuddC6zDjrVLp1uDr7sCcBrdX/jbfWcDILM2PXPlBojjZHegSxUmuQcC7A/9sZJ+zgO5RnFQ2EvCV9/kB8CnQL0vzsxt5rHcaeQ7Furiwv/5Zmv9XFCcHAKNX2qap16fJ10LrNuOtUjkhipOxwL+BXwB/ambbm4B7ozh5FHieuiPiIcBTwDNANXByFCfXAd+j7vTIE408zvPURfeSKE7OA2qAnbI0/3fgPaBrFCcbZGl+SZbml0VxchNwZRQnJ2Zpfm4UJ12A7bI0/xDwZ+B3UZz8HpjOZ097NGdjYD4wr/CYZzSyTVOvT5OvRZbmF6zGDGplfMNSpfJH4GFgWuHXhU1tmKX5F6g71zuautMLbwEjCuuWAAcWbn8EHALc08Tj1ADfpe7Nx5nUXfjskMLqx4HXgHejOPmgsOyswr6ejeLkY+BRCp8Zz9L8g8BVhfu9Vfi9WOcDA6gL+ANNzNvo69Pca6F1mxemUosrfFTw2CzNP1ruWaTWwiNvSQqQ8ZakAHnaRJIC5JG3JAXIeEtSgIy3JAXIeEtSgIy3JAXIeEtSgP4fAz02dL9pVwMAAAAASUVORK5CYII=
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h5 id="Random-Forest---Tuning">Random Forest - Tuning<a class="anchor-link" href="#Random-Forest---Tuning">&#182;</a></h5>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[59]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">data</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># instantiate the learning algorithm</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">RandomForestClassifier</span><span class="p">(</span><span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># create a params dict</span>
<span class="n">depth</span> <span class="o">=</span> <span class="p">[</span><span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">6</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">15</span><span class="p">,</span> <span class="mi">20</span><span class="p">]</span>
<span class="n">min_samples</span> <span class="o">=</span> <span class="p">[</span><span class="o">.</span><span class="mi">01</span><span class="p">,</span> <span class="o">.</span><span class="mi">025</span><span class="p">,</span> <span class="o">.</span><span class="mi">05</span><span class="p">,</span> <span class="o">.</span><span class="mi">075</span><span class="p">,</span> <span class="o">.</span><span class="mi">1</span><span class="p">,</span> <span class="o">.</span><span class="mi">2</span><span class="p">]</span>
<span class="n">est</span> <span class="o">=</span> <span class="p">[</span><span class="mi">5</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">50</span><span class="p">,</span> <span class="mi">100</span><span class="p">,</span> <span class="mi">500</span><span class="p">]</span>
<span class="n">hyperparameters</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="n">max_depth</span> <span class="o">=</span> <span class="n">depth</span><span class="p">,</span> 
                       <span class="n">min_samples_leaf</span> <span class="o">=</span> <span class="n">min_samples</span><span class="p">,</span>
                       <span class="n">n_estimators</span> <span class="o">=</span> <span class="n">est</span><span class="p">)</span>

<span class="c1"># instantiate grid search</span>
<span class="n">gridsearch</span> <span class="o">=</span> <span class="n">GridSearchCV</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">hyperparameters</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">5</span><span class="p">,</span> <span class="n">verbose</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="c1"># fit grid search</span>
<span class="n">best_model</span> <span class="o">=</span> <span class="n">gridsearch</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># print the best hyperparameters</span>
<span class="n">best_depth</span> <span class="o">=</span> <span class="n">best_model</span><span class="o">.</span><span class="n">best_estimator_</span><span class="o">.</span><span class="n">get_params</span><span class="p">()[</span><span class="s1">&#39;max_depth&#39;</span><span class="p">]</span>
<span class="n">best_min_samples</span> <span class="o">=</span> <span class="n">best_model</span><span class="o">.</span><span class="n">best_estimator_</span><span class="o">.</span><span class="n">get_params</span><span class="p">()[</span><span class="s1">&#39;min_samples_leaf&#39;</span><span class="p">]</span>
<span class="n">best_est</span> <span class="o">=</span> <span class="n">best_model</span><span class="o">.</span><span class="n">best_estimator_</span><span class="o">.</span><span class="n">get_params</span><span class="p">()[</span><span class="s1">&#39;n_estimators&#39;</span><span class="p">]</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Best max_depth: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">best_depth</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Best min_samples_leaf: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">best_min_samples</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Best n_estimators: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">best_est</span><span class="p">))</span>


<span class="c1"># BUILD MODEL WITH BEST HYPERPARAMETERS</span>

<span class="c1"># instantiate a RandomForestClassifier</span>
<span class="n">tuned_model</span> <span class="o">=</span> <span class="n">RandomForestClassifier</span><span class="p">(</span><span class="n">max_depth</span> <span class="o">=</span> <span class="n">best_depth</span><span class="p">,</span>
                                     <span class="n">min_samples_leaf</span> <span class="o">=</span> <span class="n">best_min_samples</span><span class="p">,</span>
                                     <span class="n">n_estimators</span> <span class="o">=</span> <span class="n">best_est</span><span class="p">,</span>
                                     <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># train the model</span>
<span class="n">tuned_model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># make predictions</span>
<span class="n">tuned_model_y_pred</span> <span class="o">=</span> <span class="n">tuned_model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># SCORING</span>
<span class="c1"># accuracy</span>
<span class="n">accuracy_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">tuned_model_y_pred</span><span class="p">)</span>

<span class="c1"># classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">tuned_model_y_pred</span><span class="p">))</span>

<span class="c1"># confusion matrix</span>
<span class="n">cm</span> <span class="o">=</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">tuned_model_y_pred</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">ax</span><span class="o">.</span><span class="n">matshow</span><span class="p">(</span><span class="n">cm</span><span class="p">,</span> <span class="n">cmap</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">Blues</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]):</span>
        <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">j</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">cm</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">],</span> <span class="n">va</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">,</span> <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;predicted label&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;true label&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Best max_depth: 15
Best min_samples_leaf: 0.01
Best n_estimators: 50
             precision    recall  f1-score   support

      False       0.77      0.88      0.82      9379
       True       0.73      0.57      0.64      5621

avg / total       0.76      0.76      0.75     15000

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
 

