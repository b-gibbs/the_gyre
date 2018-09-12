--- 
title: Relax - Data Cleaning, Feature Engineering and Modeling
layout: code 
permalink: /coursework/takehomes/relax_work
excerpt: "" 
section: "/coursework/takehomes/relax/" 
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

<span class="c1">#svg.fonttype: path</span>

<span class="n">blue</span> <span class="o">=</span> <span class="s1">&#39;#3498DB&#39;</span>
<span class="n">gray</span> <span class="o">=</span> <span class="s1">&#39;#95A5A6&#39;</span>
<span class="n">red</span> <span class="o">=</span> <span class="s1">&#39;#E74C3C&#39;</span>
<span class="n">dark_gray</span> <span class="o">=</span> <span class="s1">&#39;#34495E&#39;</span>
<span class="n">green</span> <span class="o">=</span> <span class="s1">&#39;#2ECC71&#39;</span>
<span class="n">purple</span> <span class="o">=</span> <span class="s1">&#39;#9B59B6&#39;</span>
<span class="n">flatui</span> <span class="o">=</span> <span class="p">[</span><span class="n">blue</span><span class="p">,</span> <span class="n">gray</span><span class="p">,</span> <span class="n">red</span><span class="p">,</span> <span class="n">dark_gray</span><span class="p">,</span> <span class="n">green</span><span class="p">,</span> <span class="n">purple</span><span class="p">]</span>

<span class="c1">#rcParams[&#39;axes.prop_cycle&#39;] = cycler(&#39;color&#39;, [blue, gray, red, dark_gray, green, purple])</span>

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
<h2 id="Strategy">Strategy<a class="anchor-link" href="#Strategy">&#182;</a></h2><ol>
<li>identify adopted users</li>
<li>add col for time between account creation and initial login</li>
<li>add col for mean time between logins</li>
<li>add col - org size categorical</li>
<li>add col - invited by user group size</li>
<li>drop unneeded cols</li>
<li>transform categoricals</li>
</ol>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">users</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;data/takehome_users.csv&#39;</span><span class="p">,</span>  <span class="n">encoding</span> <span class="o">=</span> <span class="s1">&#39;latin-1&#39;</span><span class="p">,</span> <span class="n">parse_dates</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;creation_time&#39;</span><span class="p">])</span>
<span class="n">users</span><span class="o">.</span><span class="n">invited_by_user_id</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>

<span class="n">users</span><span class="o">.</span><span class="n">invited_by_user_id</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">invited_by_user_id</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="n">users</span><span class="o">.</span><span class="n">invited_by_user_id</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">invited_by_user_id</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
<span class="n">users</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
<span class="n">users</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>

<span class="n">users</span><span class="o">.</span><span class="n">org_id</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[2]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>5583</pre>
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
      <th>object_id</th>
      <th>creation_time</th>
      <th>name</th>
      <th>email</th>
      <th>creation_source</th>
      <th>last_session_creation_time</th>
      <th>opted_in_to_mailing_list</th>
      <th>enabled_for_marketing_drip</th>
      <th>org_id</th>
      <th>invited_by_user_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2014-04-22 03:53:30</td>
      <td>Clausen August</td>
      <td>AugustCClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.398139e+09</td>
      <td>1</td>
      <td>0</td>
      <td>11</td>
      <td>10803</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2013-11-15 03:45:04</td>
      <td>Poole Matthew</td>
      <td>MatthewPoole@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.396238e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>316</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2013-03-19 23:14:52</td>
      <td>Bottrill Mitchell</td>
      <td>MitchellBottrill@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.363735e+09</td>
      <td>0</td>
      <td>0</td>
      <td>94</td>
      <td>1525</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2013-05-21 08:09:28</td>
      <td>Clausen Nicklas</td>
      <td>NicklasSClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.369210e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>5151</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2013-01-17 10:14:20</td>
      <td>Raw Grace</td>
      <td>GraceRaw@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.358850e+09</td>
      <td>0</td>
      <td>0</td>
      <td>193</td>
      <td>5240</td>
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
RangeIndex: 12000 entries, 0 to 11999
Data columns (total 10 columns):
object_id                     12000 non-null int64
creation_time                 12000 non-null datetime64[ns]
name                          12000 non-null object
email                         12000 non-null object
creation_source               12000 non-null object
last_session_creation_time    8823 non-null float64
opted_in_to_mailing_list      12000 non-null int64
enabled_for_marketing_drip    12000 non-null int64
org_id                        12000 non-null int64
invited_by_user_id            12000 non-null int64
dtypes: datetime64[ns](1), float64(1), int64(5), object(3)
memory usage: 937.6+ KB
</pre>
</div>
</div>

<div class="output_area">

<div class="prompt output_prompt">Out[2]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>0</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">engage</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;data/takehome_user_engagement.csv&#39;</span><span class="p">,</span> <span class="n">parse_dates</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;time_stamp&#39;</span><span class="p">])</span>
<span class="n">engage</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

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
      <th>time_stamp</th>
      <th>user_id</th>
      <th>visited</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014-04-22 03:53:30</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2013-11-15 03:45:04</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2013-11-29 03:45:04</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013-12-09 03:45:04</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2013-12-25 03:45:04</td>
      <td>2</td>
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
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># describe users DF</span>
<span class="n">registered_users_ct</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">users</span><span class="p">)</span>
<span class="n">mail_ct</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">opted_in_to_mailing_list</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
<span class="n">market_ct</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">enabled_for_marketing_drip</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;All users: </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">registered_users_ct</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Opted in to mailing list: </span><span class="si">{}</span><span class="s1"> - </span><span class="si">{:.2f}</span><span class="s1">%&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">mail_ct</span><span class="p">,</span> <span class="n">mail_ct</span><span class="o">/</span><span class="n">registered_users_ct</span> <span class="o">*</span> <span class="mi">100</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Enabled for marketing drip: </span><span class="si">{}</span><span class="s1"> - </span><span class="si">{:.2f}</span><span class="s1">%&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">market_ct</span><span class="p">,</span> <span class="n">market_ct</span><span class="o">/</span><span class="n">registered_users_ct</span> <span class="o">*</span> <span class="mi">100</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>All users: 12000
Opted in to mailing list: 2994 - 24.95%
Enabled for marketing drip: 1792 - 14.93%
</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># describe engage df</span>
<span class="n">logged_in_users_ct</span> <span class="o">=</span> <span class="n">engage</span><span class="o">.</span><span class="n">user_id</span><span class="o">.</span><span class="n">nunique</span><span class="p">()</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;There were </span><span class="si">{}</span><span class="s1"> logins from </span><span class="si">{}</span><span class="s1"> unique users&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">engage</span><span class="p">),</span> <span class="n">logged_in_users_ct</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">{}</span><span class="s1"> registered users have never logged in&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">registered_users_ct</span> <span class="o">-</span> <span class="n">logged_in_users_ct</span><span class="p">))</span>
<span class="n">engage</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
<span class="n">engage</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>There were 207917 logins from 8823 unique users
3177 registered users have never logged in
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
      <th>time_stamp</th>
      <th>user_id</th>
      <th>visited</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014-04-22 03:53:30</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2013-11-15 03:45:04</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2013-11-29 03:45:04</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013-12-09 03:45:04</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2013-12-25 03:45:04</td>
      <td>2</td>
      <td>1</td>
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
RangeIndex: 207917 entries, 0 to 207916
Data columns (total 3 columns):
time_stamp    207917 non-null datetime64[ns]
user_id       207917 non-null int64
visited       207917 non-null int64
dtypes: datetime64[ns](1), int64(2)
memory usage: 4.8 MB
</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># visited is always = 1, so drop the column</span>
<span class="n">engage</span> <span class="o">=</span> <span class="n">engage</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;visited&#39;</span><span class="p">,</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="1.-identify-adopted-users">1. identify adopted users<a class="anchor-link" href="#1.-identify-adopted-users">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">get_rolling_count</span><span class="p">(</span><span class="n">grp</span><span class="p">,</span> <span class="n">freq</span><span class="p">):</span>
    <span class="k">return</span> <span class="n">grp</span><span class="o">.</span><span class="n">rolling</span><span class="p">(</span><span class="n">freq</span><span class="p">,</span> <span class="n">on</span><span class="o">=</span><span class="s1">&#39;time_stamp&#39;</span><span class="p">)[</span><span class="s1">&#39;user_id&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">count</span><span class="p">()</span>

<span class="n">engage</span><span class="p">[</span><span class="s1">&#39;visits_7_days&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">engage</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;user_id&#39;</span><span class="p">,</span> <span class="n">as_index</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">group_keys</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">get_rolling_count</span><span class="p">,</span> <span class="s1">&#39;7D&#39;</span><span class="p">)</span>

<span class="n">engage</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">30</span><span class="p">)</span>
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
      <th>time_stamp</th>
      <th>user_id</th>
      <th>visits_7_days</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014-04-22 03:53:30</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2013-11-15 03:45:04</td>
      <td>2</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2013-11-29 03:45:04</td>
      <td>2</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013-12-09 03:45:04</td>
      <td>2</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2013-12-25 03:45:04</td>
      <td>2</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2013-12-31 03:45:04</td>
      <td>2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2014-01-08 03:45:04</td>
      <td>2</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2014-02-03 03:45:04</td>
      <td>2</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2014-02-08 03:45:04</td>
      <td>2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2014-02-09 03:45:04</td>
      <td>2</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2014-02-13 03:45:04</td>
      <td>2</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2014-02-16 03:45:04</td>
      <td>2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2014-03-09 03:45:04</td>
      <td>2</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2014-03-13 03:45:04</td>
      <td>2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2014-03-31 03:45:04</td>
      <td>2</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2013-03-19 23:14:52</td>
      <td>3</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2013-05-22 08:09:28</td>
      <td>4</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2013-01-22 10:14:20</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2013-12-19 03:37:06</td>
      <td>6</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2012-12-20 13:24:32</td>
      <td>7</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2013-01-16 22:08:03</td>
      <td>10</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2013-01-22 22:08:03</td>
      <td>10</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2013-01-30 22:08:03</td>
      <td>10</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2013-02-04 22:08:03</td>
      <td>10</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2013-02-06 22:08:03</td>
      <td>10</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2013-02-14 22:08:03</td>
      <td>10</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2013-02-17 22:08:03</td>
      <td>10</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2013-02-19 22:08:03</td>
      <td>10</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2013-02-26 22:08:03</td>
      <td>10</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2013-03-01 22:08:03</td>
      <td>10</td>
      <td>2.0</td>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">adopted</span> <span class="o">=</span> <span class="n">engage</span><span class="p">[</span><span class="n">engage</span><span class="o">.</span><span class="n">visits_7_days</span> <span class="o">&gt;=</span> <span class="mi">3</span><span class="p">]</span>
<span class="nb">len</span><span class="p">(</span><span class="n">adopted</span><span class="p">)</span>

<span class="n">adopted</span> <span class="o">=</span> <span class="n">adopted</span><span class="o">.</span><span class="n">drop_duplicates</span><span class="p">(</span><span class="s1">&#39;user_id&#39;</span><span class="p">,</span> <span class="n">keep</span> <span class="o">=</span> <span class="s1">&#39;first&#39;</span><span class="p">)</span>
<span class="n">adopted_ids</span> <span class="o">=</span> <span class="n">adopted</span><span class="o">.</span><span class="n">user_id</span><span class="o">.</span><span class="n">tolist</span><span class="p">()</span>
<span class="nb">type</span><span class="p">(</span><span class="n">adopted_ids</span><span class="p">)</span>
<span class="nb">len</span><span class="p">(</span><span class="n">adopted_ids</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[8]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>160522</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[8]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>list</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[8]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>1602</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">users</span><span class="p">[</span><span class="s1">&#39;adopted&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">object_id</span><span class="o">.</span><span class="n">isin</span><span class="p">(</span><span class="n">adopted_ids</span><span class="p">)</span>

<span class="n">users</span><span class="o">.</span><span class="n">adopted</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
<span class="n">users</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">20</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[9]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>1602</pre>
</div>

</div>

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
      <th>object_id</th>
      <th>creation_time</th>
      <th>name</th>
      <th>email</th>
      <th>creation_source</th>
      <th>last_session_creation_time</th>
      <th>opted_in_to_mailing_list</th>
      <th>enabled_for_marketing_drip</th>
      <th>org_id</th>
      <th>invited_by_user_id</th>
      <th>adopted</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2014-04-22 03:53:30</td>
      <td>Clausen August</td>
      <td>AugustCClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.398139e+09</td>
      <td>1</td>
      <td>0</td>
      <td>11</td>
      <td>10803</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2013-11-15 03:45:04</td>
      <td>Poole Matthew</td>
      <td>MatthewPoole@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.396238e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>316</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2013-03-19 23:14:52</td>
      <td>Bottrill Mitchell</td>
      <td>MitchellBottrill@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.363735e+09</td>
      <td>0</td>
      <td>0</td>
      <td>94</td>
      <td>1525</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2013-05-21 08:09:28</td>
      <td>Clausen Nicklas</td>
      <td>NicklasSClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.369210e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>5151</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2013-01-17 10:14:20</td>
      <td>Raw Grace</td>
      <td>GraceRaw@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.358850e+09</td>
      <td>0</td>
      <td>0</td>
      <td>193</td>
      <td>5240</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2013-12-17 03:37:06</td>
      <td>Cunha Eduardo</td>
      <td>EduardoPereiraCunha@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.387424e+09</td>
      <td>0</td>
      <td>0</td>
      <td>197</td>
      <td>11241</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2012-12-16 13:24:32</td>
      <td>Sewell Tyler</td>
      <td>TylerSewell@jourrapide.com</td>
      <td>SIGNUP</td>
      <td>1.356010e+09</td>
      <td>0</td>
      <td>1</td>
      <td>37</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2013-07-31 05:34:02</td>
      <td>Hamilton Danielle</td>
      <td>DanielleHamilton@yahoo.com</td>
      <td>PERSONAL_PROJECTS</td>
      <td>NaN</td>
      <td>1</td>
      <td>1</td>
      <td>74</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>2013-11-05 04:04:24</td>
      <td>Amsel Paul</td>
      <td>PaulAmsel@hotmail.com</td>
      <td>PERSONAL_PROJECTS</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>302</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>2013-01-16 22:08:03</td>
      <td>Santos Carla</td>
      <td>CarlaFerreiraSantos@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.401833e+09</td>
      <td>1</td>
      <td>1</td>
      <td>318</td>
      <td>4143</td>
      <td>True</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>2013-12-26 03:55:54</td>
      <td>Paulsen Malthe</td>
      <td>MaltheAPaulsen@gustr.com</td>
      <td>SIGNUP</td>
      <td>1.388117e+09</td>
      <td>0</td>
      <td>0</td>
      <td>69</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>2014-04-17 23:48:38</td>
      <td>Mathiesen Lærke</td>
      <td>LaerkeLMathiesen@cuvox.de</td>
      <td>ORG_INVITE</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>130</td>
      <td>9270</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>2014-03-30 16:19:38</td>
      <td>Fry Alexander</td>
      <td>AlexanderDFry@cuvox.de</td>
      <td>ORG_INVITE</td>
      <td>1.396196e+09</td>
      <td>0</td>
      <td>0</td>
      <td>254</td>
      <td>11204</td>
      <td>False</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>2012-10-11 16:14:33</td>
      <td>Rivera Bret</td>
      <td>BretKRivera@gmail.com</td>
      <td>SIGNUP</td>
      <td>1.350058e+09</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>2013-07-16 21:33:54</td>
      <td>Theiss Ralf</td>
      <td>RalfTheiss@hotmail.com</td>
      <td>PERSONAL_PROJECTS</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>175</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>2013-02-11 10:09:50</td>
      <td>Engel René</td>
      <td>ReneEngel@hotmail.com</td>
      <td>PERSONAL_PROJECTS</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>211</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>2014-04-09 14:39:38</td>
      <td>Reynolds Anthony</td>
      <td>AnthonyReynolds@jourrapide.com</td>
      <td>GUEST_INVITE</td>
      <td>1.397314e+09</td>
      <td>1</td>
      <td>0</td>
      <td>175</td>
      <td>1600</td>
      <td>False</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>2013-08-24 00:26:46</td>
      <td>Gregersen Celina</td>
      <td>CelinaAGregersen@jourrapide.com</td>
      <td>GUEST_INVITE</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>3153</td>
      <td>False</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>2013-05-24 14:56:36</td>
      <td>Collins Arlene</td>
      <td>ArleneRCollins@gmail.com</td>
      <td>SIGNUP</td>
      <td>1.369926e+09</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>2014-03-06 11:46:38</td>
      <td>Helms Mikayla</td>
      <td>lqyvjilf@uhzdq.com</td>
      <td>SIGNUP</td>
      <td>1.401364e+09</td>
      <td>0</td>
      <td>0</td>
      <td>58</td>
      <td>0</td>
      <td>True</td>
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
<h2 id="2.-add-col-for-time-between-account-creation-and-initial-login">2. add col for time between account creation and initial login<a class="anchor-link" href="#2.-add-col-for-time-between-account-creation-and-initial-login">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># get initial login datetime from engage DF</span>
<span class="n">grp</span> <span class="o">=</span> <span class="n">engage</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;user_id&#39;</span><span class="p">,</span> <span class="n">as_index</span> <span class="o">=</span> <span class="kc">False</span><span class="p">)</span><span class="o">.</span><span class="n">agg</span><span class="p">({</span><span class="s1">&#39;time_stamp&#39;</span> <span class="p">:</span> <span class="n">np</span><span class="o">.</span><span class="n">min</span><span class="p">})</span>
<span class="n">grp</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">20</span><span class="p">)</span>
<span class="n">grp</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[10]:</div>



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
      <th>user_id</th>
      <th>time_stamp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2014-04-22 03:53:30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2013-11-15 03:45:04</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2013-03-19 23:14:52</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2013-05-22 08:09:28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2013-01-22 10:14:20</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2013-12-19 03:37:06</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2012-12-20 13:24:32</td>
    </tr>
    <tr>
      <th>7</th>
      <td>10</td>
      <td>2013-01-16 22:08:03</td>
    </tr>
    <tr>
      <th>8</th>
      <td>11</td>
      <td>2013-12-27 03:55:54</td>
    </tr>
    <tr>
      <th>9</th>
      <td>13</td>
      <td>2014-03-30 16:19:38</td>
    </tr>
    <tr>
      <th>10</th>
      <td>14</td>
      <td>2012-10-12 16:14:33</td>
    </tr>
    <tr>
      <th>11</th>
      <td>17</td>
      <td>2014-04-12 14:39:38</td>
    </tr>
    <tr>
      <th>12</th>
      <td>19</td>
      <td>2013-05-25 14:56:36</td>
    </tr>
    <tr>
      <th>13</th>
      <td>20</td>
      <td>2014-03-11 11:46:38</td>
    </tr>
    <tr>
      <th>14</th>
      <td>21</td>
      <td>2013-01-22 12:27:42</td>
    </tr>
    <tr>
      <th>15</th>
      <td>22</td>
      <td>2014-02-10 06:00:46</td>
    </tr>
    <tr>
      <th>16</th>
      <td>23</td>
      <td>2012-08-18 08:30:27</td>
    </tr>
    <tr>
      <th>17</th>
      <td>24</td>
      <td>2013-09-09 22:20:03</td>
    </tr>
    <tr>
      <th>18</th>
      <td>25</td>
      <td>2014-02-25 00:11:13</td>
    </tr>
    <tr>
      <th>19</th>
      <td>27</td>
      <td>2014-01-15 17:35:11</td>
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
Int64Index: 8823 entries, 0 to 8822
Data columns (total 2 columns):
user_id       8823 non-null int64
time_stamp    8823 non-null datetime64[ns]
dtypes: datetime64[ns](1), int64(1)
memory usage: 206.8 KB
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># merge initial login column into users DF</span>

<span class="n">grp</span><span class="o">.</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;user_id&#39;</span><span class="p">,</span> <span class="s1">&#39;initial_login&#39;</span><span class="p">]</span>

<span class="n">users</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">merge</span><span class="p">(</span><span class="n">grp</span><span class="p">,</span> <span class="n">how</span> <span class="o">=</span> <span class="s1">&#39;left&#39;</span><span class="p">,</span> <span class="n">left_on</span> <span class="o">=</span> <span class="s1">&#39;object_id&#39;</span><span class="p">,</span> <span class="n">right_on</span> <span class="o">=</span> <span class="s1">&#39;user_id&#39;</span><span class="p">)</span>
<span class="n">users</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
<span class="n">users</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[11]:</div>



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
      <th>object_id</th>
      <th>creation_time</th>
      <th>name</th>
      <th>email</th>
      <th>creation_source</th>
      <th>last_session_creation_time</th>
      <th>opted_in_to_mailing_list</th>
      <th>enabled_for_marketing_drip</th>
      <th>org_id</th>
      <th>invited_by_user_id</th>
      <th>adopted</th>
      <th>user_id</th>
      <th>initial_login</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2014-04-22 03:53:30</td>
      <td>Clausen August</td>
      <td>AugustCClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.398139e+09</td>
      <td>1</td>
      <td>0</td>
      <td>11</td>
      <td>10803</td>
      <td>False</td>
      <td>1.0</td>
      <td>2014-04-22 03:53:30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2013-11-15 03:45:04</td>
      <td>Poole Matthew</td>
      <td>MatthewPoole@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.396238e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>316</td>
      <td>True</td>
      <td>2.0</td>
      <td>2013-11-15 03:45:04</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2013-03-19 23:14:52</td>
      <td>Bottrill Mitchell</td>
      <td>MitchellBottrill@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.363735e+09</td>
      <td>0</td>
      <td>0</td>
      <td>94</td>
      <td>1525</td>
      <td>False</td>
      <td>3.0</td>
      <td>2013-03-19 23:14:52</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2013-05-21 08:09:28</td>
      <td>Clausen Nicklas</td>
      <td>NicklasSClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.369210e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>5151</td>
      <td>False</td>
      <td>4.0</td>
      <td>2013-05-22 08:09:28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2013-01-17 10:14:20</td>
      <td>Raw Grace</td>
      <td>GraceRaw@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.358850e+09</td>
      <td>0</td>
      <td>0</td>
      <td>193</td>
      <td>5240</td>
      <td>False</td>
      <td>5.0</td>
      <td>2013-01-22 10:14:20</td>
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
Int64Index: 12000 entries, 0 to 11999
Data columns (total 13 columns):
object_id                     12000 non-null int64
creation_time                 12000 non-null datetime64[ns]
name                          12000 non-null object
email                         12000 non-null object
creation_source               12000 non-null object
last_session_creation_time    8823 non-null float64
opted_in_to_mailing_list      12000 non-null int64
enabled_for_marketing_drip    12000 non-null int64
org_id                        12000 non-null int64
invited_by_user_id            12000 non-null int64
adopted                       12000 non-null bool
user_id                       8823 non-null float64
initial_login                 8823 non-null datetime64[ns]
dtypes: bool(1), datetime64[ns](2), float64(2), int64(5), object(3)
memory usage: 1.2+ MB
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">users</span><span class="p">[</span><span class="s1">&#39;creation_login_gap&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="n">users</span><span class="o">.</span><span class="n">initial_login</span> <span class="o">-</span> <span class="n">users</span><span class="o">.</span><span class="n">creation_time</span><span class="p">)</span><span class="o">.</span><span class="n">dt</span><span class="o">.</span><span class="n">days</span>

<span class="n">users</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[12]:</div>



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
      <th>object_id</th>
      <th>creation_time</th>
      <th>name</th>
      <th>email</th>
      <th>creation_source</th>
      <th>last_session_creation_time</th>
      <th>opted_in_to_mailing_list</th>
      <th>enabled_for_marketing_drip</th>
      <th>org_id</th>
      <th>invited_by_user_id</th>
      <th>adopted</th>
      <th>user_id</th>
      <th>initial_login</th>
      <th>creation_login_gap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2014-04-22 03:53:30</td>
      <td>Clausen August</td>
      <td>AugustCClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.398139e+09</td>
      <td>1</td>
      <td>0</td>
      <td>11</td>
      <td>10803</td>
      <td>False</td>
      <td>1.0</td>
      <td>2014-04-22 03:53:30</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2013-11-15 03:45:04</td>
      <td>Poole Matthew</td>
      <td>MatthewPoole@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.396238e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>316</td>
      <td>True</td>
      <td>2.0</td>
      <td>2013-11-15 03:45:04</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2013-03-19 23:14:52</td>
      <td>Bottrill Mitchell</td>
      <td>MitchellBottrill@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.363735e+09</td>
      <td>0</td>
      <td>0</td>
      <td>94</td>
      <td>1525</td>
      <td>False</td>
      <td>3.0</td>
      <td>2013-03-19 23:14:52</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2013-05-21 08:09:28</td>
      <td>Clausen Nicklas</td>
      <td>NicklasSClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.369210e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>5151</td>
      <td>False</td>
      <td>4.0</td>
      <td>2013-05-22 08:09:28</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2013-01-17 10:14:20</td>
      <td>Raw Grace</td>
      <td>GraceRaw@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.358850e+09</td>
      <td>0</td>
      <td>0</td>
      <td>193</td>
      <td>5240</td>
      <td>False</td>
      <td>5.0</td>
      <td>2013-01-22 10:14:20</td>
      <td>5.0</td>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">users</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
Int64Index: 12000 entries, 0 to 11999
Data columns (total 14 columns):
object_id                     12000 non-null int64
creation_time                 12000 non-null datetime64[ns]
name                          12000 non-null object
email                         12000 non-null object
creation_source               12000 non-null object
last_session_creation_time    8823 non-null float64
opted_in_to_mailing_list      12000 non-null int64
enabled_for_marketing_drip    12000 non-null int64
org_id                        12000 non-null int64
invited_by_user_id            12000 non-null int64
adopted                       12000 non-null bool
user_id                       8823 non-null float64
initial_login                 8823 non-null datetime64[ns]
creation_login_gap            8823 non-null float64
dtypes: bool(1), datetime64[ns](2), float64(3), int64(5), object(3)
memory usage: 1.3+ MB
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
<h2 id="3.-add-col-for-mean-time-between-logins">3. add col for mean time between logins<a class="anchor-link" href="#3.-add-col-for-mean-time-between-logins">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">gap</span> <span class="o">=</span> <span class="n">engage</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;user_id&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">time_stamp</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">x</span> <span class="o">-</span> <span class="n">x</span><span class="o">.</span><span class="n">shift</span><span class="p">())</span><span class="o">.</span><span class="n">dt</span><span class="o">.</span><span class="n">days</span>
<span class="n">gaps</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">gap</span><span class="p">)</span>
<span class="n">gaps</span><span class="o">.</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;mean_gap_length&#39;</span><span class="p">]</span>
<span class="n">gaps</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
<span class="n">gaps</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[14]:</div>



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
      <th>mean_gap_length</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>14.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16.0</td>
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
RangeIndex: 207917 entries, 0 to 207916
Data columns (total 1 columns):
mean_gap_length    199094 non-null float64
dtypes: float64(1)
memory usage: 1.6 MB
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">engage</span> <span class="o">=</span> <span class="n">engage</span><span class="o">.</span><span class="n">merge</span><span class="p">(</span><span class="n">gaps</span><span class="p">,</span> <span class="n">left_index</span> <span class="o">=</span> <span class="kc">True</span><span class="p">,</span> <span class="n">right_index</span> <span class="o">=</span> <span class="kc">True</span><span class="p">)</span>
<span class="n">engage</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[15]:</div>



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
      <th>time_stamp</th>
      <th>user_id</th>
      <th>visits_7_days</th>
      <th>mean_gap_length</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014-04-22 03:53:30</td>
      <td>1</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2013-11-15 03:45:04</td>
      <td>2</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2013-11-29 03:45:04</td>
      <td>2</td>
      <td>1.0</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013-12-09 03:45:04</td>
      <td>2</td>
      <td>1.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2013-12-25 03:45:04</td>
      <td>2</td>
      <td>1.0</td>
      <td>16.0</td>
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
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">gap_mean</span> <span class="o">=</span> <span class="n">engage</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;user_id&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">agg</span><span class="p">({</span><span class="s1">&#39;mean_gap_length&#39;</span> <span class="p">:</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">})</span>
<span class="n">gap_mean</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[16]:</div>



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
      <th>mean_gap_length</th>
    </tr>
    <tr>
      <th>user_id</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10.461538</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
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
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># merge mean login gap column into users DF</span>

<span class="n">users</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">merge</span><span class="p">(</span><span class="n">gap_mean</span><span class="p">,</span> <span class="n">how</span> <span class="o">=</span> <span class="s1">&#39;left&#39;</span><span class="p">,</span> <span class="n">left_on</span> <span class="o">=</span> <span class="s1">&#39;object_id&#39;</span><span class="p">,</span> <span class="n">right_on</span> <span class="o">=</span> <span class="s1">&#39;user_id&#39;</span><span class="p">)</span>
<span class="n">users</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
<span class="n">users</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
      <th>object_id</th>
      <th>creation_time</th>
      <th>name</th>
      <th>email</th>
      <th>creation_source</th>
      <th>last_session_creation_time</th>
      <th>opted_in_to_mailing_list</th>
      <th>enabled_for_marketing_drip</th>
      <th>org_id</th>
      <th>invited_by_user_id</th>
      <th>adopted</th>
      <th>user_id</th>
      <th>initial_login</th>
      <th>creation_login_gap</th>
      <th>mean_gap_length</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2014-04-22 03:53:30</td>
      <td>Clausen August</td>
      <td>AugustCClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.398139e+09</td>
      <td>1</td>
      <td>0</td>
      <td>11</td>
      <td>10803</td>
      <td>False</td>
      <td>1.0</td>
      <td>2014-04-22 03:53:30</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2013-11-15 03:45:04</td>
      <td>Poole Matthew</td>
      <td>MatthewPoole@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.396238e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>316</td>
      <td>True</td>
      <td>2.0</td>
      <td>2013-11-15 03:45:04</td>
      <td>0.0</td>
      <td>10.461538</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2013-03-19 23:14:52</td>
      <td>Bottrill Mitchell</td>
      <td>MitchellBottrill@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.363735e+09</td>
      <td>0</td>
      <td>0</td>
      <td>94</td>
      <td>1525</td>
      <td>False</td>
      <td>3.0</td>
      <td>2013-03-19 23:14:52</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2013-05-21 08:09:28</td>
      <td>Clausen Nicklas</td>
      <td>NicklasSClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.369210e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>5151</td>
      <td>False</td>
      <td>4.0</td>
      <td>2013-05-22 08:09:28</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2013-01-17 10:14:20</td>
      <td>Raw Grace</td>
      <td>GraceRaw@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.358850e+09</td>
      <td>0</td>
      <td>0</td>
      <td>193</td>
      <td>5240</td>
      <td>False</td>
      <td>5.0</td>
      <td>2013-01-22 10:14:20</td>
      <td>5.0</td>
      <td>NaN</td>
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
Int64Index: 12000 entries, 0 to 11999
Data columns (total 15 columns):
object_id                     12000 non-null int64
creation_time                 12000 non-null datetime64[ns]
name                          12000 non-null object
email                         12000 non-null object
creation_source               12000 non-null object
last_session_creation_time    8823 non-null float64
opted_in_to_mailing_list      12000 non-null int64
enabled_for_marketing_drip    12000 non-null int64
org_id                        12000 non-null int64
invited_by_user_id            12000 non-null int64
adopted                       12000 non-null bool
user_id                       8823 non-null float64
initial_login                 8823 non-null datetime64[ns]
creation_login_gap            8823 non-null float64
mean_gap_length               2588 non-null float64
dtypes: bool(1), datetime64[ns](2), float64(4), int64(5), object(3)
memory usage: 1.4+ MB
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
<h2 id="4.-add-col-org-id-size">4. add col org id size<a class="anchor-link" href="#4.-add-col-org-id-size">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># orgs = users[(users.org_id &gt; 10) &amp; (users.org_id &lt; 20)]</span>
<span class="n">orgs</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">org_id</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span>
<span class="n">orgs</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span>
<span class="n">orgs</span><span class="o">.</span><span class="n">tail</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[18]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>0     319
1     233
2     201
3     168
4     159
6     138
5     128
9     124
7     119
10    104
Name: org_id, dtype: int64</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[18]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>396    9
400    8
397    8
386    7
416    2
Name: org_id, dtype: int64</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">one</span> <span class="o">=</span> <span class="n">users</span><span class="p">[</span><span class="n">users</span><span class="o">.</span><span class="n">org_id</span> <span class="o">==</span> <span class="mi">396</span><span class="p">]</span>
<span class="n">one</span><span class="o">.</span><span class="n">shape</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[19]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(9, 15)</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">o</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">orgs</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
<span class="n">o</span><span class="o">.</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;org_id&#39;</span><span class="p">,</span> <span class="s1">&#39;user_count&#39;</span><span class="p">]</span>
<span class="n">o</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
RangeIndex: 417 entries, 0 to 416
Data columns (total 2 columns):
org_id        417 non-null int64
user_count    417 non-null int64
dtypes: int64(2)
memory usage: 6.6 KB
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">org_size</span><span class="p">(</span><span class="n">ct</span><span class="p">):</span>
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

<span class="n">o</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[21]:</div>



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
      <th>org_id</th>
      <th>user_count</th>
      <th>org_size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>319</td>
      <td>XL</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>233</td>
      <td>XL</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>201</td>
      <td>XL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>168</td>
      <td>L</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>159</td>
      <td>L</td>
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
<div class="prompt input_prompt">In&nbsp;[22]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">org_size_dict</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">o</span><span class="o">.</span><span class="n">org_id</span><span class="p">,</span> <span class="n">o</span><span class="o">.</span><span class="n">org_size</span><span class="p">))</span>
<span class="nb">len</span><span class="p">(</span><span class="n">org_size_dict</span><span class="p">)</span>
<span class="n">org_size_dict</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">nan</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[22]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>417</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">users</span><span class="p">[</span><span class="s1">&#39;org_size&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">org_id</span><span class="o">.</span><span class="n">map</span><span class="p">(</span><span class="n">org_size_dict</span><span class="p">)</span>
<span class="n">users</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[23]:</div>



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
      <th>object_id</th>
      <th>creation_time</th>
      <th>name</th>
      <th>email</th>
      <th>creation_source</th>
      <th>last_session_creation_time</th>
      <th>opted_in_to_mailing_list</th>
      <th>enabled_for_marketing_drip</th>
      <th>org_id</th>
      <th>invited_by_user_id</th>
      <th>adopted</th>
      <th>user_id</th>
      <th>initial_login</th>
      <th>creation_login_gap</th>
      <th>mean_gap_length</th>
      <th>org_size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2014-04-22 03:53:30</td>
      <td>Clausen August</td>
      <td>AugustCClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.398139e+09</td>
      <td>1</td>
      <td>0</td>
      <td>11</td>
      <td>10803</td>
      <td>False</td>
      <td>1.0</td>
      <td>2014-04-22 03:53:30</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2013-11-15 03:45:04</td>
      <td>Poole Matthew</td>
      <td>MatthewPoole@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.396238e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>316</td>
      <td>True</td>
      <td>2.0</td>
      <td>2013-11-15 03:45:04</td>
      <td>0.0</td>
      <td>10.461538</td>
      <td>XL</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2013-03-19 23:14:52</td>
      <td>Bottrill Mitchell</td>
      <td>MitchellBottrill@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.363735e+09</td>
      <td>0</td>
      <td>0</td>
      <td>94</td>
      <td>1525</td>
      <td>False</td>
      <td>3.0</td>
      <td>2013-03-19 23:14:52</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>XS</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2013-05-21 08:09:28</td>
      <td>Clausen Nicklas</td>
      <td>NicklasSClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.369210e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>5151</td>
      <td>False</td>
      <td>4.0</td>
      <td>2013-05-22 08:09:28</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>XL</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2013-01-17 10:14:20</td>
      <td>Raw Grace</td>
      <td>GraceRaw@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.358850e+09</td>
      <td>0</td>
      <td>0</td>
      <td>193</td>
      <td>5240</td>
      <td>False</td>
      <td>5.0</td>
      <td>2013-01-22 10:14:20</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>XS</td>
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
<h2 id="5.-add-col-for-bool---invited-by-user">5. add col for bool - invited by user<a class="anchor-link" href="#5.-add-col-for-bool---invited-by-user">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[24]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">invites</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">invited_by_user_id</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span>
<span class="n">invites</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[24]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>0        5583
10741      13
2527       12
11770      11
2308       11
Name: invited_by_user_id, dtype: int64</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">i</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">invites</span><span class="p">)</span><span class="o">.</span><span class="n">reset_index</span><span class="p">()</span>
<span class="n">i</span><span class="o">.</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;inviter_id&#39;</span><span class="p">,</span> <span class="s1">&#39;user_count&#39;</span><span class="p">]</span>
<span class="n">i</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
RangeIndex: 2565 entries, 0 to 2564
Data columns (total 2 columns):
inviter_id    2565 non-null int64
user_count    2565 non-null int64
dtypes: int64(2)
memory usage: 40.2 KB
</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">group_size</span><span class="p">(</span><span class="n">ct</span><span class="p">):</span>
    <span class="n">rtn</span> <span class="o">=</span> <span class="s1">&#39;XS&#39;</span>
    <span class="k">if</span> <span class="n">ct</span> <span class="o">&gt;</span> <span class="mi">11</span><span class="p">:</span>
        <span class="n">rtn</span> <span class="o">=</span> <span class="s1">&#39;XL&#39;</span>
    <span class="k">elif</span> <span class="n">ct</span> <span class="o">&gt;</span> <span class="mi">8</span><span class="p">:</span>
        <span class="n">rtn</span> <span class="o">=</span> <span class="s1">&#39;L&#39;</span>
    <span class="k">elif</span> <span class="n">ct</span> <span class="o">&gt;</span> <span class="mi">5</span><span class="p">:</span>
        <span class="n">rtn</span> <span class="o">=</span> <span class="s1">&#39;M&#39;</span>
    <span class="k">elif</span> <span class="n">ct</span> <span class="o">&gt;</span> <span class="mi">3</span><span class="p">:</span>
        <span class="n">rtn</span> <span class="o">=</span> <span class="s1">&#39;S&#39;</span>
    <span class="k">elif</span> <span class="n">ct</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>
        <span class="n">rtn</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">nan</span>
    <span class="k">return</span> <span class="n">rtn</span>

<span class="n">i</span><span class="p">[</span><span class="s1">&#39;group_size&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">i</span><span class="o">.</span><span class="n">user_count</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">group_size</span><span class="p">)</span>

<span class="n">i</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[26]:</div>



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
      <th>inviter_id</th>
      <th>user_count</th>
      <th>group_size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>5583</td>
      <td>XL</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10741</td>
      <td>13</td>
      <td>XL</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2527</td>
      <td>12</td>
      <td>XL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11770</td>
      <td>11</td>
      <td>L</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2308</td>
      <td>11</td>
      <td>L</td>
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
<div class="prompt input_prompt">In&nbsp;[27]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">group_size_dict</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">i</span><span class="o">.</span><span class="n">inviter_id</span><span class="p">,</span> <span class="n">i</span><span class="o">.</span><span class="n">group_size</span><span class="p">))</span>
<span class="nb">len</span><span class="p">(</span><span class="n">group_size_dict</span><span class="p">)</span>
<span class="n">group_size_dict</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">nan</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[27]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>2565</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">users</span><span class="p">[</span><span class="s1">&#39;group_size&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">invited_by_user_id</span><span class="o">.</span><span class="n">map</span><span class="p">(</span><span class="n">group_size_dict</span><span class="p">)</span>
<span class="n">users</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[28]:</div>



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
      <th>object_id</th>
      <th>creation_time</th>
      <th>name</th>
      <th>email</th>
      <th>creation_source</th>
      <th>last_session_creation_time</th>
      <th>opted_in_to_mailing_list</th>
      <th>enabled_for_marketing_drip</th>
      <th>org_id</th>
      <th>invited_by_user_id</th>
      <th>adopted</th>
      <th>user_id</th>
      <th>initial_login</th>
      <th>creation_login_gap</th>
      <th>mean_gap_length</th>
      <th>org_size</th>
      <th>group_size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2014-04-22 03:53:30</td>
      <td>Clausen August</td>
      <td>AugustCClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.398139e+09</td>
      <td>1</td>
      <td>0</td>
      <td>11</td>
      <td>10803</td>
      <td>False</td>
      <td>1.0</td>
      <td>2014-04-22 03:53:30</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>S</td>
      <td>XS</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2013-11-15 03:45:04</td>
      <td>Poole Matthew</td>
      <td>MatthewPoole@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.396238e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>316</td>
      <td>True</td>
      <td>2.0</td>
      <td>2013-11-15 03:45:04</td>
      <td>0.0</td>
      <td>10.461538</td>
      <td>XL</td>
      <td>XS</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2013-03-19 23:14:52</td>
      <td>Bottrill Mitchell</td>
      <td>MitchellBottrill@gustr.com</td>
      <td>ORG_INVITE</td>
      <td>1.363735e+09</td>
      <td>0</td>
      <td>0</td>
      <td>94</td>
      <td>1525</td>
      <td>False</td>
      <td>3.0</td>
      <td>2013-03-19 23:14:52</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>XS</td>
      <td>L</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2013-05-21 08:09:28</td>
      <td>Clausen Nicklas</td>
      <td>NicklasSClausen@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.369210e+09</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>5151</td>
      <td>False</td>
      <td>4.0</td>
      <td>2013-05-22 08:09:28</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>XL</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2013-01-17 10:14:20</td>
      <td>Raw Grace</td>
      <td>GraceRaw@yahoo.com</td>
      <td>GUEST_INVITE</td>
      <td>1.358850e+09</td>
      <td>0</td>
      <td>0</td>
      <td>193</td>
      <td>5240</td>
      <td>False</td>
      <td>5.0</td>
      <td>2013-01-22 10:14:20</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>XS</td>
      <td>S</td>
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
<h2 id="6.-drop-unneeded-cols">6. drop unneeded cols<a class="anchor-link" href="#6.-drop-unneeded-cols">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[29]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">users</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s1">&#39;object_id&#39;</span><span class="p">,</span> <span class="s1">&#39;creation_time&#39;</span><span class="p">,</span> <span class="s1">&#39;name&#39;</span><span class="p">,</span> <span class="s1">&#39;email&#39;</span><span class="p">,</span> <span class="s1">&#39;last_session_creation_time&#39;</span><span class="p">,</span> 
                    <span class="s1">&#39;invited_by_user_id&#39;</span><span class="p">,</span> <span class="s1">&#39;org_id&#39;</span><span class="p">,</span> <span class="s1">&#39;user_id&#39;</span><span class="p">,</span> <span class="s1">&#39;initial_login&#39;</span><span class="p">],</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[30]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">y</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">adopted</span>
<span class="n">users</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;adopted&#39;</span><span class="p">,</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">)</span>

<span class="n">users</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
<span class="n">users</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
      <th>creation_source</th>
      <th>opted_in_to_mailing_list</th>
      <th>enabled_for_marketing_drip</th>
      <th>creation_login_gap</th>
      <th>mean_gap_length</th>
      <th>org_size</th>
      <th>group_size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GUEST_INVITE</td>
      <td>1</td>
      <td>0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>S</td>
      <td>XS</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ORG_INVITE</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>10.461538</td>
      <td>XL</td>
      <td>XS</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ORG_INVITE</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>XS</td>
      <td>L</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GUEST_INVITE</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>XL</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GUEST_INVITE</td>
      <td>0</td>
      <td>0</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>XS</td>
      <td>S</td>
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
Int64Index: 12000 entries, 0 to 11999
Data columns (total 7 columns):
creation_source               12000 non-null object
opted_in_to_mailing_list      12000 non-null int64
enabled_for_marketing_drip    12000 non-null int64
creation_login_gap            8823 non-null float64
mean_gap_length               2588 non-null float64
org_size                      11681 non-null object
group_size                    6417 non-null object
dtypes: float64(2), int64(2), object(3)
memory usage: 750.0+ KB
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
<h2 id="7.-transform-categoricals">7. transform categoricals<a class="anchor-link" href="#7.-transform-categoricals">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[31]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">users</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">get_dummies</span><span class="p">(</span><span class="n">users</span><span class="p">,</span> <span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;creation_source&#39;</span><span class="p">,</span> <span class="s1">&#39;org_size&#39;</span><span class="p">,</span> <span class="s1">&#39;group_size&#39;</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[32]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">users</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">y</span><span class="p">)</span>
<span class="n">users</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[32]:</div>



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
      <th>opted_in_to_mailing_list</th>
      <th>enabled_for_marketing_drip</th>
      <th>creation_login_gap</th>
      <th>mean_gap_length</th>
      <th>creation_source_GUEST_INVITE</th>
      <th>creation_source_ORG_INVITE</th>
      <th>creation_source_PERSONAL_PROJECTS</th>
      <th>creation_source_SIGNUP</th>
      <th>creation_source_SIGNUP_GOOGLE_AUTH</th>
      <th>org_size_L</th>
      <th>org_size_M</th>
      <th>org_size_S</th>
      <th>org_size_XL</th>
      <th>org_size_XS</th>
      <th>group_size_L</th>
      <th>group_size_M</th>
      <th>group_size_S</th>
      <th>group_size_XL</th>
      <th>group_size_XS</th>
      <th>adopted</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>10.461538</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>0</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
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
<div class="prompt input_prompt">In&nbsp;[33]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">users</span><span class="o">.</span><span class="n">mean_gap_length</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">mean_gap_length</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">100</span><span class="p">)</span>

<span class="n">users</span><span class="o">.</span><span class="n">creation_login_gap</span> <span class="o">=</span> <span class="n">users</span><span class="o">.</span><span class="n">creation_login_gap</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">100</span><span class="p">)</span>

<span class="n">users</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
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
Int64Index: 12000 entries, 0 to 11999
Data columns (total 20 columns):
opted_in_to_mailing_list              12000 non-null int64
enabled_for_marketing_drip            12000 non-null int64
creation_login_gap                    12000 non-null float64
mean_gap_length                       12000 non-null float64
creation_source_GUEST_INVITE          12000 non-null uint8
creation_source_ORG_INVITE            12000 non-null uint8
creation_source_PERSONAL_PROJECTS     12000 non-null uint8
creation_source_SIGNUP                12000 non-null uint8
creation_source_SIGNUP_GOOGLE_AUTH    12000 non-null uint8
org_size_L                            12000 non-null uint8
org_size_M                            12000 non-null uint8
org_size_S                            12000 non-null uint8
org_size_XL                           12000 non-null uint8
org_size_XS                           12000 non-null uint8
group_size_L                          12000 non-null uint8
group_size_M                          12000 non-null uint8
group_size_S                          12000 non-null uint8
group_size_XL                         12000 non-null uint8
group_size_XS                         12000 non-null uint8
adopted                               12000 non-null bool
dtypes: bool(1), float64(2), int64(2), uint8(15)
memory usage: 976.2 KB
</pre>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">users</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s1">&#39;data/modeling.csv&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Modeling">Modeling<a class="anchor-link" href="#Modeling">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[35]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># sklearn imports</span>
<span class="kn">from</span> <span class="nn">sklearn.dummy</span> <span class="k">import</span> <span class="n">DummyClassifier</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">train_test_split</span><span class="p">,</span> <span class="n">cross_val_score</span><span class="p">,</span> <span class="n">GridSearchCV</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="k">import</span> <span class="n">accuracy_score</span><span class="p">,</span> <span class="n">classification_report</span><span class="p">,</span> <span class="n">roc_curve</span><span class="p">,</span> <span class="n">roc_auc_score</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="k">import</span> <span class="n">confusion_matrix</span>

<span class="n">test_file_url</span> <span class="o">=</span> <span class="s1">&#39;~/Documents/Data Science/Data Projects/Take Home Challenge/relax_challenge/data/modeling.csv&#39;</span>
<span class="c1"># set random_state SEED variable</span>
<span class="n">SEED</span> <span class="o">=</span> <span class="mi">42</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[36]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">test_file_url</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

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
Successes:	1116
Total:		8400
Percent:	0.133

Test Set
Successes:	486
Total:		3600
Percent:	0.135


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
<h2 id="Dummy-Classifier">Dummy Classifier<a class="anchor-link" href="#Dummy-Classifier">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[37]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">test_file_url</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

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
<pre>Dummy Classifier accuracy: 0.7644


             precision    recall  f1-score   support

      False       0.86      0.87      0.86      3114
       True       0.12      0.12      0.12       486

avg / total       0.76      0.76      0.76      3600

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
<h2 id="SMOTE">SMOTE<a class="anchor-link" href="#SMOTE">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[38]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#imports</span>
<span class="kn">from</span> <span class="nn">imblearn.over_sampling</span> <span class="k">import</span> <span class="n">SMOTE</span>

<span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">test_file_url</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># SMOTE IT!</span>
<span class="n">smote</span> <span class="o">=</span> <span class="n">SMOTE</span><span class="p">(</span><span class="n">ratio</span><span class="o">=</span><span class="s1">&#39;minority&#39;</span><span class="p">)</span>
<span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span> <span class="o">=</span> <span class="n">smote</span><span class="o">.</span><span class="n">fit_sample</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># training set breakdown</span>
<span class="n">train_success</span> <span class="o">=</span> <span class="n">y_train_sm</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
<span class="n">train_total</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">y_train_sm</span><span class="p">)</span>
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
Successes:	7284
Total:		14568
Percent:	0.500

Test Set
Successes:	486
Total:		3600
Percent:	0.135


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
<h2 id="Dummy-Classifier">Dummy Classifier<a class="anchor-link" href="#Dummy-Classifier">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[39]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">test_file_url</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># SMOTE IT!</span>
<span class="n">smote</span> <span class="o">=</span> <span class="n">SMOTE</span><span class="p">(</span><span class="n">ratio</span><span class="o">=</span><span class="s1">&#39;minority&#39;</span><span class="p">)</span>
<span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span> <span class="o">=</span> <span class="n">smote</span><span class="o">.</span><span class="n">fit_sample</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># instantiate and fit a dummy classifier</span>
<span class="n">dummy</span> <span class="o">=</span> <span class="n">DummyClassifier</span><span class="p">(</span><span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>
<span class="n">dummy</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span><span class="p">)</span>

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
<pre>Dummy Classifier accuracy: 0.5122


             precision    recall  f1-score   support

      False       0.87      0.51      0.64      3114
       True       0.14      0.53      0.23       486

avg / total       0.77      0.51      0.59      3600

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
<h2 id="Logistic-Regression">Logistic Regression<a class="anchor-link" href="#Logistic-Regression">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[40]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># imports</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="k">import</span> <span class="n">LogisticRegression</span>

<span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">test_file_url</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># SMOTE IT!</span>
<span class="n">smote</span> <span class="o">=</span> <span class="n">SMOTE</span><span class="p">(</span><span class="n">ratio</span><span class="o">=</span><span class="s1">&#39;minority&#39;</span><span class="p">)</span>
<span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span> <span class="o">=</span> <span class="n">smote</span><span class="o">.</span><span class="n">fit_sample</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># instantiate &amp; fit model</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">LogisticRegression</span><span class="p">(</span><span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>
<span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span><span class="p">)</span>

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
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;true label&#39;</span><span class="p">)</span>

<span class="c1"># take a look at feature importance</span>
<span class="c1"># imp = pd.Series(model.feature_importances_, index=X.columns)</span>
<span class="c1"># imp = imp.sort_values(ascending=False)</span>
<span class="c1"># print(imp);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[40]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>LogisticRegression(C=1.0, class_weight=None, dual=False, fit_intercept=True,
          intercept_scaling=1, max_iter=100, multi_class=&#39;ovr&#39;, n_jobs=1,
          penalty=&#39;l2&#39;, random_state=42, solver=&#39;liblinear&#39;, tol=0.0001,
          verbose=0, warm_start=False)</pre>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Logistic Regression Accuracy:	0.9547

             precision    recall  f1-score   support

      False       1.00      0.95      0.97      3114
       True       0.76      0.98      0.85       486

avg / total       0.96      0.95      0.96      3600

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt output_prompt">Out[40]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.image.AxesImage at 0x11b9d22e8&gt;</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[40]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Text(0,0,&#39;2960&#39;)</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[40]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Text(1,0,&#39;154&#39;)</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[40]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Text(0,1,&#39;9&#39;)</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[40]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Text(1,1,&#39;477&#39;)</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[40]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Text(0.5,0,&#39;predicted label&#39;)</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[40]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Text(0,0.5,&#39;true label&#39;)</pre>
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
<h2 id="LinearSVC">LinearSVC<a class="anchor-link" href="#LinearSVC">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[41]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#imports</span>
<span class="kn">from</span> <span class="nn">sklearn.svm</span> <span class="k">import</span> <span class="n">LinearSVC</span>

<span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">test_file_url</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># SMOTE IT!</span>
<span class="n">smote</span> <span class="o">=</span> <span class="n">SMOTE</span><span class="p">(</span><span class="n">ratio</span><span class="o">=</span><span class="s1">&#39;minority&#39;</span><span class="p">)</span>
<span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span> <span class="o">=</span> <span class="n">smote</span><span class="o">.</span><span class="n">fit_sample</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># instantiate and fit the learning algorithm</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">LinearSVC</span><span class="p">(</span><span class="n">random_state</span><span class="o">=</span><span class="n">SEED</span><span class="p">)</span>
<span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span><span class="p">)</span>

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
<pre>Accuracy: 0.9486
             precision    recall  f1-score   support

      False       1.00      0.94      0.97      3114
       True       0.73      0.99      0.84       486

avg / total       0.96      0.95      0.95      3600

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
<h2 id="SVC">SVC<a class="anchor-link" href="#SVC">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[42]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.svm</span> <span class="k">import</span> <span class="n">SVC</span>

<span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">test_file_url</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># SMOTE IT!</span>
<span class="n">smote</span> <span class="o">=</span> <span class="n">SMOTE</span><span class="p">(</span><span class="n">ratio</span><span class="o">=</span><span class="s1">&#39;minority&#39;</span><span class="p">)</span>
<span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span> <span class="o">=</span> <span class="n">smote</span><span class="o">.</span><span class="n">fit_sample</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># instantiate the learning algorithm</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">SVC</span><span class="p">(</span><span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># create a params dict</span>
<span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span><span class="p">)</span>

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
<pre>Accuracy: 0.9486
             precision    recall  f1-score   support

      False       1.00      0.94      0.97      3114
       True       0.73      0.99      0.84       486

avg / total       0.96      0.95      0.95      3600

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
<h2 id="Random-Forest">Random Forest<a class="anchor-link" href="#Random-Forest">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[43]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="k">import</span> <span class="n">RandomForestClassifier</span>

<span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">test_file_url</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># SMOTE IT!</span>
<span class="n">smote</span> <span class="o">=</span> <span class="n">SMOTE</span><span class="p">(</span><span class="n">ratio</span><span class="o">=</span><span class="s1">&#39;minority&#39;</span><span class="p">)</span>
<span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span> <span class="o">=</span> <span class="n">smote</span><span class="o">.</span><span class="n">fit_sample</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># instantiate &amp; fit</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">RandomForestClassifier</span><span class="p">(</span><span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>
<span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span><span class="p">)</span>

<span class="c1"># make predictions on the test set</span>
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
<pre>Accuracy: 0.9628
             precision    recall  f1-score   support

      False       0.98      0.98      0.98      3114
       True       0.87      0.85      0.86       486

avg / total       0.96      0.96      0.96      3600

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
<h3 id="Random-Forest---Tuning">Random Forest - Tuning<a class="anchor-link" href="#Random-Forest---Tuning">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[46]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># import data and split into features matrix and target vector</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">test_file_url</span><span class="p">,</span> <span class="n">index_col</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>

<span class="n">X</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[:</span><span class="o">-</span><span class="mi">1</span><span class="p">]],</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()[</span><span class="o">-</span><span class="mi">1</span><span class="p">]]</span>

<span class="c1"># split features and target into train and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="o">.</span><span class="mi">3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">)</span>

<span class="c1"># SMOTE IT!</span>
<span class="n">smote</span> <span class="o">=</span> <span class="n">SMOTE</span><span class="p">(</span><span class="n">ratio</span><span class="o">=</span><span class="s1">&#39;minority&#39;</span><span class="p">)</span>
<span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span> <span class="o">=</span> <span class="n">smote</span><span class="o">.</span><span class="n">fit_sample</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

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
<span class="n">best_model</span> <span class="o">=</span> <span class="n">gridsearch</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span><span class="p">)</span>

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
                                     <span class="n">random_state</span> <span class="o">=</span> <span class="n">SEED</span><span class="p">,</span>
                                     <span class="n">n_jobs</span> <span class="o">=</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span>

<span class="c1"># train the model</span>
<span class="n">tuned_model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train_sm</span><span class="p">,</span> <span class="n">y_train_sm</span><span class="p">)</span>

<span class="c1"># make predictions</span>
<span class="n">tuned_model_y_pred</span> <span class="o">=</span> <span class="n">tuned_model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># SCORING</span>
<span class="c1"># accuracy</span>
<span class="n">acc</span> <span class="o">=</span> <span class="n">accuracy_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">tuned_model_y_pred</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Accuracy: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">acc</span><span class="p">))</span>

<span class="c1"># classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">tuned_model_y_pred</span><span class="p">))</span>

<span class="c1"># confusion matrix</span>
<span class="n">cm</span> <span class="o">=</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span> <span class="o">=</span> <span class="n">tuned_model_y_pred</span><span class="p">)</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">6</span><span class="p">))</span>
<span class="n">ax</span><span class="o">.</span><span class="n">matshow</span><span class="p">(</span><span class="n">cm</span><span class="p">,</span> <span class="n">cmap</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">cm</span><span class="o">.</span><span class="n">Blues</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]):</span>
    <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">cm</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]):</span>
        <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">j</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">i</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">cm</span><span class="p">[</span><span class="n">i</span><span class="p">,</span> <span class="n">j</span><span class="p">],</span> <span class="n">va</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">,</span> <span class="n">ha</span><span class="o">=</span><span class="s1">&#39;center&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;predicted&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;actual&#39;</span><span class="p">)</span>

<span class="c1"># take a look at feature importance</span>
<span class="n">imp</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">tuned_model</span><span class="o">.</span><span class="n">feature_importances_</span><span class="p">,</span> <span class="n">index</span><span class="o">=</span><span class="n">X</span><span class="o">.</span><span class="n">columns</span><span class="p">)</span>
<span class="n">imp</span> <span class="o">=</span> <span class="n">imp</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">imp</span><span class="p">);</span>
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
Best n_estimators: 50
Accuracy: 0.9602777777777778
             precision    recall  f1-score   support

      False       1.00      0.96      0.98      3114
       True       0.79      0.97      0.87       486

avg / total       0.97      0.96      0.96      3600

mean_gap_length                       0.796703
creation_login_gap                    0.137101
org_size_XS                           0.028182
creation_source_PERSONAL_PROJECTS     0.008612
org_size_S                            0.007128
opted_in_to_mailing_list              0.006436
enabled_for_marketing_drip            0.003102
org_size_XL                           0.002895
org_size_M                            0.002877
group_size_S                          0.001662
group_size_XS                         0.001148
org_size_L                            0.001022
creation_source_ORG_INVITE            0.000852
creation_source_GUEST_INVITE          0.000712
creation_source_SIGNUP                0.000564
group_size_M                          0.000417
creation_source_SIGNUP_GOOGLE_AUTH    0.000393
group_size_L                          0.000193
group_size_XL                         0.000000
dtype: float64
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
 

