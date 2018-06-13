---
title: Supervised Learning
permalink: /notes/machine_learning/supervised_learning.html
---
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Imports</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="kn">import</span> <span class="nn">os</span>
                                
<span class="n">base_url</span> <span class="o">=</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">expanduser</span><span class="p">(</span><span class="s1">&#39;~/Documents/Data Science/Machine Learning/Data Sets/&#39;</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">&#39;figure.figsize&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="mi">15</span><span class="p">,</span> <span class="mi">8</span><span class="p">]</span>

<span class="o">%</span><span class="k">matplotlib</span> inline
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">base_url</span> <span class="o">+</span> <span class="s1">&#39;house-votes-84.csv&#39;</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;party&#39;</span><span class="p">,</span> <span class="s1">&#39;infants&#39;</span><span class="p">,</span> <span class="s1">&#39;water&#39;</span><span class="p">,</span> <span class="s1">&#39;budget&#39;</span><span class="p">,</span> <span class="s1">&#39;physician&#39;</span><span class="p">,</span> <span class="s1">&#39;salvador&#39;</span><span class="p">,</span> <span class="s1">&#39;religious&#39;</span><span class="p">,</span> <span class="s1">&#39;satellite&#39;</span><span class="p">,</span> <span class="s1">&#39;aid&#39;</span><span class="p">,</span> <span class="s1">&#39;missile&#39;</span><span class="p">,</span> <span class="s1">&#39;immigration&#39;</span><span class="p">,</span> <span class="s1">&#39;synfuels&#39;</span><span class="p">,</span> <span class="s1">&#39;education&#39;</span><span class="p">,</span> <span class="s1">&#39;superfund&#39;</span><span class="p">,</span> <span class="s1">&#39;crime&#39;</span><span class="p">,</span> <span class="s1">&#39;duty_free_exports&#39;</span><span class="p">,</span> <span class="s1">&#39;eaa_rsa&#39;</span><span class="p">]</span>
<span class="n">colnames</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="p">[</span><span class="mi">1</span><span class="p">:</span><span class="mi">17</span><span class="p">]</span>

<span class="k">for</span> <span class="n">c</span> <span class="ow">in</span> <span class="n">colnames</span><span class="p">:</span>
    <span class="n">df</span><span class="p">[</span><span class="n">c</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">c</span><span class="p">]</span><span class="o">.</span><span class="n">map</span><span class="p">({</span><span class="s1">&#39;n&#39;</span><span class="p">:</span><span class="mi">0</span><span class="p">,</span> <span class="s1">&#39;y&#39;</span><span class="p">:</span><span class="mi">1</span><span class="p">,</span> <span class="s1">&#39;?&#39;</span><span class="p">:</span><span class="mi">1</span><span class="p">})</span>

<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
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
      <th>party</th>
      <th>infants</th>
      <th>water</th>
      <th>budget</th>
      <th>physician</th>
      <th>salvador</th>
      <th>religious</th>
      <th>satellite</th>
      <th>aid</th>
      <th>missile</th>
      <th>immigration</th>
      <th>synfuels</th>
      <th>education</th>
      <th>superfund</th>
      <th>crime</th>
      <th>duty_free_exports</th>
      <th>eaa_rsa</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>republican</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>democrat</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>democrat</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>democrat</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>democrat</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
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
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Classification">Classification<a class="anchor-link" href="#Classification">&#182;</a></h1><h2 id="Visual-EDA---sns.countplot">Visual EDA - sns.countplot<a class="anchor-link" href="#Visual-EDA---sns.countplot">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">&#39;figure.figsize&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="mi">15</span><span class="p">,</span> <span class="mi">8</span><span class="p">]</span>

<span class="n">sns</span><span class="o">.</span><span class="n">countplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">&#39;satellite&#39;</span><span class="p">,</span> <span class="n">hue</span><span class="o">=</span><span class="s1">&#39;party&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">df</span><span class="p">,</span> <span class="n">palette</span><span class="o">=</span><span class="s1">&#39;RdBu&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xticks</span><span class="p">([</span><span class="mi">0</span><span class="p">,</span><span class="mi">1</span><span class="p">],</span> <span class="p">[</span><span class="s1">&#39;No&#39;</span><span class="p">,</span> <span class="s1">&#39;Yes&#39;</span><span class="p">]);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA38AAAHjCAYAAACTjKaeAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4yLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvhp/UCwAAIABJREFUeJzt3X20XXV97/vPF4JGHiwCgUPFEmCgBQnEEEBEEI6WIuPIow+gVgKWVJDrtefUwrHjnnJarFZBj31QLxYEuYgoCiJXbUEKiKgQMEAAUVKjpnIxgFU8IBLyu3/sRdyEgFvI2ivZv9drjDX2Wr8111rfvfkj482ca85qrQUAAICpbb1RDwAAAMDwiT8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOTBv1AM/EFlts0WbOnDnqMQAAAEbixhtvvLe1NmMi267T8Tdz5swsWLBg1GMAAACMRFX9YKLbOuwTAACgA+IPAACgA+IPAACgA+v0d/5W55FHHsnSpUvzy1/+ctSjTEnTp0/PNttskw022GDUowAAAL+FKRd/S5cuzSabbJKZM2emqkY9zpTSWst9992XpUuXZrvtthv1OAAAwG9hyh32+ctf/jKbb7658BuCqsrmm29uryoAAKyDplz8JRF+Q+RvCwAA66YpGX8AAAA8nvhbC11yySW5/fbbRz0GAAAwhYi/tczy5cvFHwAAsMaJvyFYsmRJfv/3fz/HHHNMdt1117z2ta/Ngw8+mL/6q7/KHnvskV122SXz589Pay1Jsv/+++fd7353XvGKV+Rv//Zvc+mll+Zd73pXZs+encWLF2fOnDkr3/t73/tedt9991H9agAAwDpK/A3JnXfemfnz5+eWW27Jc5/73HzkIx/JSSedlBtuuCGLFi3KQw89lMsuu2zl9v/xH/+Rq6++On/xF3+RQw45JB/4wAeycOHC7LDDDvmd3/mdLFy4MEnyiU98IvPmzRvRbwUAAKyrxN+QvOAFL8g+++yTJHnzm9+ca6+9Nv/6r/+avfbaK7NmzcqVV16Z2267beX2b3jDG570vf74j/84n/jEJ/Loo4/mwgsvzBvf+Mahzw8AAEwt4m9IVr0kQlXlxBNPzEUXXZRbb701xx9//OOul7fRRhs96XsdeeSR+fKXv5zLLrssu+++ezbffPOhzQ0AAExN4m9IfvjDH+Yb3/hGkuSCCy7Iy1/+8iTJFltskV/84he56KKLnvS1m2yySR544IGVj6dPn54//MM/zAknnJBjjz12uIMDAABTkvgbkp122innnntudt1119x///054YQTcvzxx2fWrFk57LDDssceezzpa4866qh84AMfyEte8pIsXrw4SfKmN70pVZUDDzxwsn4FAABgCpk26gGmqvXWWy8f+9jHHrd22mmn5bTTTnvCtlddddXjHu+zzz5PuNTDtddem+OOOy7rr7/+Gp8VAACY+sTfOuDwww/P4sWLc+WVV456FAAAYB0l/oZg5syZWbRo0Rp7v4svvniNvRcAANAn8QcAwMhcctPiUY8Aq3XYnB1GPcIa54QvAAAAHRB/AAAAHRB/AAAAHZjy3/m794pPrdH32+JVb1yj7/fbuOqqq3L66afnsssue8JzM2fOzIIFC7LFFlvkZS97Wa677roRTAgAAKyt7PkbstZaVqxYMamfKfwAAIBVib8hWLJkSXbaaaeceOKJmTNnTs4777zsvffemTNnTl73utflF7/4RZKxvXUnn3xy9txzz+y555656667kiTz5s3LRRddtPL9Nt5445X3f/7zn+fwww/PzjvvnLe97W2rDcvx27///e/PrFmzsttuu+WUU05Jknz84x/PHnvskd122y1HHnlkHnzwwZWf+453vCMve9nLsv322z9uBgAAYN0m/obkzjvvzFve8pZcfvnlOeuss3LFFVfkpptuyty5c/PBD35w5XbPfe5zc/311+ekk07KO9/5zt/4vtdff33OOOOM3HrrrVm8eHE+//nPP+m2X/7yl3PJJZfkW9/6Vm6++eb8+Z//eZLkiCOOyA033JCbb745O+20U84666yVr7n77rtz7bXX5rLLLlsZiwAAwLpP/A3Jtttum5e+9KX55je/mdtvvz377LNPZs+enXPPPTc/+MEPVm539NFHr/z5jW984ze+75577pntt98+66+/fo4++uhce+21T7rtFVdckWOPPTYbbrhhkmSzzTZLkixatCj77rtvZs2alfPPPz+33XbbytccdthhWW+99bLzzjvnnnvueVq/OwAAsPaZ8id8GZWNNtooydh3/v7gD/4gF1xwwWq3q6on3J82bdrKwzlba/nVr3612u1X93i81tpqn583b14uueSS7LbbbjnnnHNy1VVXrXzu2c9+9uNeDwAATA32/A3ZS1/60nz9619f+X2+Bx98MN/97ndXPn/hhReu/Ln33nsnGfsu4I033pgk+cIXvpBHHnlk5fbXX399vv/972fFihW58MIL8/KXv/xJP/vAAw/M2WefvfI7fffff3+S5IEHHsjWW2+dRx55JOeff/4a/G0BAIC11ZTf8zfKSzMkyYwZM3LOOefk6KOPzsMPP5wkOe200/LCF74wSfLwww9nr732yooVK1buHTz++ONz6KGHZs8998wrX/nKlXsRk2TvvffOKaeckltvvTX77bdfDj/88Cf97IMOOigLFy7M3Llz86xnPSsHH3xw/uZv/iZ//dd/nb322ivbbrttZs2alQceeGCIfwEAAGBtUMM6tK+qXpDkk0n+U5IVSc5srX24qjZLcmGSmUmWJHl9a+2nNXZ84oeTHJzkwSTzWms3PdVnzJ07ty1YsOBxa3fccUd22mmnNfzbDMf4a/OtS9alvzEAsHa75KbFox4BVuuwOTuMeoQJqaobW2tzJ7LtMA/7XJ7kv7XWdkry0iRvr6qdk5yS5KuttR2TfHXwOElenWTHwW1+ko8OcTYAAICuDC3+Wmt3P7bnrrX2QJI7kjw/yaFJzh1sdm6Swwb3D03yyTbmm0k2raqthzXf2mDJkiXr3F4/AABg3TQpJ3ypqplJXpLkW0m2aq3dnYwFYpItB5s9P8mPxr1s6WANAACAZ2jo8VdVGyf5XJJ3ttZ+/lSbrmbtCV9IrKr5VbWgqhYsW7ZsTY0JAAAwpQ01/qpqg4yF3/mttc8Plu957HDOwc+fDNaXJnnBuJdvk+THq75na+3M1trc1trcGTNmDG94AACAKWRo8Tc4e+dZSe5orX1w3FOXJjlmcP+YJF8Yt/6WGvPSJD977PBQAAAAnplhXudvnyR/lOTWqlo4WHt3kvcl+UxVvTXJD5O8bvDclzJ2mYe7Mnaph2PXxBBr+vTBT+eUr6eeemo23njj/Nmf/dkanWVNWLJkSa677rq88Y2jvR4iAAAwXEOLv9batVn99/iS5JWr2b4lefuw5unZ8uXLM23a6v9TL1myJJ/61KfEHwAATHGTcrbPHr3nPe/Ji170orzqVa/KnXfemSRZvHhxDjrooOy+++7Zd999853vfCdJMm/evJxwwgk54IADsv322+fqq6/Occcdl5122inz5s1b+Z4XXHBBZs2alV122SUnn3zyyvWvfOUrmTNnTnbbbbe88pVjXX3qqadm/vz5OfDAA/OWt7wlS5Ysyb777ps5c+Zkzpw5ue6665Ikp5xySr72ta9l9uzZ+dCHPjRJfx0AAGCyDfOwz27deOON+fSnP51vf/vbWb58eebMmZPdd9898+fPz8c+9rHsuOOO+da3vpUTTzwxV155ZZLkpz/9aa688spceumlec1rXpOvf/3r+ad/+qfsscceWbhwYbbccsucfPLJufHGG/O85z0vBx54YC655JLss88+Of7443PNNddku+22y/333/+4Oa699to85znPyYMPPpjLL78806dPz/e+970cffTRWbBgQd73vvfl9NNPz2WXXTaqPxcAADAJxN8QfO1rX8vhhx+eDTfcMElyyCGH5Je//GWuu+66vO51r1u53cMPP7zy/mte85pUVWbNmpWtttoqs2bNSpK8+MUvzpIlS/KDH/wg+++/fx47w+mb3vSmXHPNNVl//fWz3377ZbvttkuSbLbZZivf85BDDslznvOcJMkjjzySk046KQsXLsz666+f7373u8P9IwAAAGsV8TckYyc7/bUVK1Zk0003zcKFC1e7/bOf/ewkyXrrrbfy/mOPn+o7e621J3zWYzbaaKOV9z/0oQ9lq622ys0335wVK1Zk+vTpv9XvAwAArNt8528I9ttvv1x88cV56KGH8sADD+SLX/xiNtxww2y33Xb57Gc/m2Qs2m6++eYJv+dee+2Vq6++Ovfee28effTRXHDBBXnFK16RvffeO1dffXW+//3vJ8njDvsc72c/+1m23nrrrLfeejnvvPPy6KOPJkk22WSTPPDAA8/wNwYAANZ2U37P39O5NMMzNWfOnLzhDW/I7Nmzs+2222bfffdNkpx//vk54YQTctppp+WRRx7JUUcdld12221C77n11lvnve99bw444IC01nLwwQfn0EMPTZKceeaZOeKII7JixYpsueWWufzyy5/w+hNPPDFHHnlkPvvZz+aAAw5YuVdw1113zbRp07Lbbrtl3rx5+dM//dM19FcAAADWJjV2hYV109y5c9uCBQset3bHHXdkp512GtFEffA3BgDWlDV9TWZYU0axE+npqKobW2tzJ7Ktwz4BAAA6IP4AAAA6MCXjb10+lHVt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sAAAAFPBKOLv0iTHDO4fk+QL49bfMjjr50uT/Oyxw0MBAAB4ZoZ6ofaquiDJ/km2qKqlSf4yyfuSfKaq3prkh0leN9j8S0kOTnJXkgeTHDvM2QAAAHoy1PhrrR39JE+9cjXbtiRvH+Y8AAAAvVqbTvgCAADAkIg/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADog/AACADkyb7A+sqhcluXDc0vZJ/keSTZMcn2TZYP3drbUvTfJ4AAAAU9Kkx19r7c4ks5OkqtZP8u9JLk5ybJIPtdZOn+yZAAAAprpRH/b5yiSLW2s/GPEcAAAAU9qo4++oJBeMe3xSVd1SVWdX1fNW94Kqml9VC6pqwbJly1a3CQAAAKsYWfxV1bOSHJLks4OljybZIWOHhN6d5IzVva61dmZrbW5rbe6MGTMmZVYAAIB13Sj3/L06yU2ttXuSpLV2T2vt0dbaiiQfT7LnCGcDAACYUkYZf0dn3CGfVbX1uOcOT7Jo0icCAACYoib9bJ9JUlUbJvmDJH8ybvn9VTU7SUuyZJXnAAAAeAZGEn+ttQeTbL7K2h+NYhYAAIAejPpsnwAAAEwC8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANAB8QcAANCBaaMeABitS25aPOoRYLUOm7PDqEcAgCnFnj8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOiD8AAIAOTBvVB1fVkiQPJHk0yfLW2tyq2izJhUlmJlmS5PWttZ+OakYAAICpYtR7/g5orc1urc0dPD4lyVdbazsm+ergMQAAAM/QqONvVYcmOXdw/9wkh41wFgAAgCljlPHXkvxLVd1YVfMHa1u11u5OksHPLVd9UVXNr6oFVbVg2bJlkzguAADAumtk3/lLsk9r7cdVtWWSy6vqOxN5UWvtzCRnJsncuXPbMAcEAACYKka256+19uPBz58kuTjJnknuqaqtk2Tw8yejmg8AAGAqGUn8VdVGVbXJY/eTHJhkUZJLkxwz2OyYJF8YxXwAAABTzagO+9wqycVV9dgMn2qtfaWqbkjymap6a5IfJnndiOYDAACYUkYSf621f0uy22rW70vyysmfCAAAYGpb2y71AAAAwBCIPwAAgA6IPwAAgA6IPwAAgA6M8iLvAMAkufeKT416BFi9zfYa9QTQDXv+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOiD+AAAAOjDp8VdVL6iqf62qO6rqtqr6Pwfrp1bVv1fVwsHt4MmeDQAAYKqaNoLPXJ7kv7XWbqqqTZLcWFWXD577UGvt9BHMBAAAMKVNevy11u5Ocvfg/gNVdUeS50/2HAAAAD0Z6Xf+qmpmkpck+dZg6aSquqWqzq6q5z3Ja+ZX1YKqWrBs2bJJmhQAAGDdNrL4q6qNk3wuyTtbaz9P8tEkOySZnbE9g2es7nWttTNba3Nba3NnzJgxafMCAACsy0YSf1W1QcbC7/zW2ueTpLV2T2vt0dbaiiQfT7LnKGYDAACYikZxts9KclaSO1prHxy3vvW4zQ5PsmiyZwMAAJiqRnG2z32S/FGSW6tq4WDt3UmOrqrZSVqSJUn+ZASzAQAATEmjONvntUlqNU99abJnAQAA6MVIz/YJAADA5BB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHRB/AAAAHVjr4q+qDqqqO6vqrqo6ZdTzAACbNo5ZAAAFPklEQVQATAVrVfxV1fpJ/jHJq5PsnOToqtp5tFMBAACs+9aq+EuyZ5K7Wmv/1lr7VZJPJzl0xDMBAACs86aNeoBVPD/Jj8Y9Xppkr/EbVNX8JPMHD39RVXdO0mwwVW2R5N5RDwFAt/w7BM/MthPdcG2Lv1rNWnvcg9bOTHLm5IwDU19VLWitzR31HAD0yb9DMHnWtsM+lyZ5wbjH2yT58YhmAQAAmDLWtvi7IcmOVbVdVT0ryVFJLh3xTAAAAOu8teqwz9ba8qo6Kck/J1k/ydmttdtGPBZMdQ6jBmCU/DsEk6Raa795KwAAANZpa9thnwAAAAyB+AMAAOiA+INOVFWrqjPGPf6zqjp1hCMBMMXVmGur6tXj1l5fVV8Z5VzQK/EH/Xg4yRFVtcWoBwGgD23s5BJvS/LBqppeVRsleU+St492MuiT+IN+LM/YGdX+dNUnqmrbqvpqVd0y+Pl7kz8eAFNRa21Rki8mOTnJXyb5ZGttcVUdU1XXV9XCqvpIVa1XVdOq6ryqurWqFlXVO0Y7PUwta9WlHoCh+8ckt1TV+1dZ/4eM/WN8blUdl+Tvkhw26dMBMFX9zyQ3JflVkrlVtUuSw5O8bHCprzMzdn3nxUm2aK3NSpKq2nRUA8NUJP6gI621n1fVJ5O8I8lD457aO8kRg/vnJVk1DgHgaWut/e+qujDJL1prD1fVq5LskWRBVSXJc5L8KGPXen5RVX04yZeS/MuoZoapSPxBf/5Xxv7v6yeeYhsXAAVgTVsxuCVJJTm7tfZ/rbpRVe2a5NUZ+x+VRyaZP2kTwhTnO3/Qmdba/Uk+k+St45avy9jhNknypiTXTvZcAHTliiSvf+wkZFW1eVX9XlXNSFKttc9m7PuBc0Y5JEw19vxBn85IctK4x+9IcnZVvSvJsiTHjmQqALrQWru1qv5nkiuqar0kj2TsrKCPJjmrxo4FbRk7SQywhtTYGXgBAACYyhz2CQAA0AHxBwAA0AHxBwAA0AHxBwAA0AHxBwAA0AHxBwBPoqrmVdXvTmC7c6rqtYP7V1XV3MH9L1XVpoPbicOeFwCeivgDgCc3L8lvjL8n01o7uLX2H0k2TSL+ABgp8QdAV6pqo6r6f6vq5qpaVFVvqKr/UVU3DB6fWWNem2RukvOramFVPaeqdq+qq6vqxqr656ra+jd81pKq2iLJ+5LsMHifDwyee9fgM28ZXOwaAIZK/AHQm4OS/Li1tltrbZckX0nyD621PQaPn5Pkv7TWLkqyIMmbWmuzkyxP8vdJXtta2z3J2UneM8HPPCXJ4tba7Nbau6rqwCQ7Jtkzyewku1fVfmvylwSAVU0b9QAAMMluTXJ6Vf1tkstaa1+rqiOr6s+TbJhksyS3JfniKq97UZJdklxeVUmyfpK7n+YMBw5u3x483jhjMXjN03w/APiNxB8AXWmtfbeqdk9ycJL3VtW/JHl7krmttR9V1alJpq/mpZXkttba3mtgjEry3tba/70G3gsAJsRhnwB0ZXD2zgdba/9PktOTzBk8dW9VbZzkteM2fyDJJoP7dyaZUVV7D95ng6p68QQ/dvz7JMk/Jzlu8HmpqudX1ZZP6xcCgAmy5w+A3sxK8oGqWpHkkSQnJDksY4eDLklyw7htz0nysap6KMneGQvDv6uq38nYv6H/K2OHiD6l1tp9VfX1qlqU5MuD7/3tlOQbg0NIf5HkzUl+skZ+QwBYjWqtjXoGAAAAhsxhnwAAAB0QfwAAAB0QfwAAAB0QfwAAAB0QfwAAAB0QfwAAAB0QfwAAAB34/wFDShbbW358nAAAAABJRU5ErkJggg==
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
<h2 id="Split-data-into-training-and-testing-sets">Split data into training and testing sets<a class="anchor-link" href="#Split-data-into-training-and-testing-sets">&#182;</a></h2><div class="highlight"><pre><span></span><span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span><span class="o">=</span><span class="mf">0.3</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">21</span><span class="p">,</span> <span class="n">stratify</span><span class="o">=</span><span class="n">y</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Prep-DataFrame-for-SKLearn-fit">Prep DataFrame for SKLearn fit<a class="anchor-link" href="#Prep-DataFrame-for-SKLearn-fit">&#182;</a></h2><hr>
<h3 id="Convert-DF-to-np.array">Convert DF to np.array<a class="anchor-link" href="#Convert-DF-to-np.array">&#182;</a></h3><p>SKLearn doesn't interact with pandas, only NumPy.  DataFrames typically contain both features and targets.  Need to separate features into a 2D NumPy array ('X' by convention), and targets into a NumPy array with the same number of rows ('y' by convention):</p>
<p>Create arrays for the features and the labels</p>
<div class="highlight"><pre><span></span><span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s1">&#39;label_col&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">values</span>
<span class="n">X</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;label_col&#39;</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">values</span>
</pre></div>
<h3 id="Reshape">Reshape<a class="anchor-link" href="#Reshape">&#182;</a></h3><p>It's common to call array.reshape(-1, 1) to reshape an array before use.  The -1 is kind of a wildcard - it tells Python to make the resulting array however many rows it needs to be to accomodate the data, and one column wide.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="k-Nearest-Neighbors">k-Nearest Neighbors<a class="anchor-link" href="#k-Nearest-Neighbors">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Import KNeighborsClassifier from sklearn.neighbors</span>
<span class="kn">from</span> <span class="nn">sklearn.neighbors</span> <span class="k">import</span> <span class="n">KNeighborsClassifier</span>

<span class="c1"># Copy target column values to a numpy array</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s1">&#39;party&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">values</span>

<span class="c1"># Drop target column and copy features columns&#39; values to a 2D numpy array</span>
<span class="n">X</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;party&#39;</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">values</span>

<span class="c1"># Create a k-NN classifier with 6 neighbors</span>
<span class="n">knn</span> <span class="o">=</span> <span class="n">KNeighborsClassifier</span><span class="p">(</span><span class="n">n_neighbors</span><span class="o">=</span><span class="mi">6</span><span class="p">)</span>

<span class="c1"># Fit the classifier to the data</span>
<span class="n">knn</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
<span class="nb">type</span><span class="p">(</span><span class="n">X</span><span class="p">),</span> <span class="nb">type</span><span class="p">(</span><span class="n">y</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="n">X</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">X</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[12]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>KNeighborsClassifier(algorithm=&#39;auto&#39;, leaf_size=30, metric=&#39;minkowski&#39;,
           metric_params=None, n_jobs=1, n_neighbors=6, p=2,
           weights=&#39;uniform&#39;)</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[12]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(numpy.ndarray, numpy.ndarray)</pre>
</div>

</div>

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
      <th>party</th>
      <th>infants</th>
      <th>water</th>
      <th>budget</th>
      <th>physician</th>
      <th>salvador</th>
      <th>religious</th>
      <th>satellite</th>
      <th>aid</th>
      <th>missile</th>
      <th>immigration</th>
      <th>synfuels</th>
      <th>education</th>
      <th>superfund</th>
      <th>crime</th>
      <th>duty_free_exports</th>
      <th>eaa_rsa</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>republican</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>democrat</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>democrat</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>democrat</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>democrat</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
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
<pre>[[0 1 0 ... 1 0 1]
 [1 1 1 ... 1 0 0]
 [0 1 1 ... 0 0 1]
 ...
 [0 1 0 ... 1 0 1]
 [0 0 0 ... 1 0 1]
 [0 1 0 ... 1 1 0]]
[[0]
 [1]
 [0]
 ...
 [1]
 [1]
 [0]]
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
<h3 id="Measuring-kNN-Model-Performance">Measuring kNN Model Performance<a class="anchor-link" href="#Measuring-kNN-Model-Performance">&#182;</a></h3><div class="highlight"><pre><span></span><span class="n">knn</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">)</span>
</pre></div>
<p>The decision boundary is determined by model complexity:</p>
<ul>
<li>larger knn.score = smoother decision boundary = less complex model</li>
<li>smaller knn.score = more jagged decision boundary = more complex model = can lead to overfitting</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Regression">Regression<a class="anchor-link" href="#Regression">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Linear-Regression">Linear Regression<a class="anchor-link" href="#Linear-Regression">&#182;</a></h2><p><strong>Cost Function</strong>: measures how bad your model is -- want to minimize this.  (aka error or loss function)</p>
<p><strong>Utility Function</strong>: measures how good your model is -- want to maximize this. (aka fitness function)</p>
<p><strong>Ordinary Least Squares</strong>: To fit a line that minimizes the distance between the line and the sum of the squares of the residuals.</p>
<p><strong>Scoring Regression</strong>: .score() computes the $R^2$ score.</p>
<p>y = ax + b</p>
<ul>
<li>y = target</li>
<li>x = single feature</li>
<li>a, b = parameters of model </li>
</ul>
<p>How do we choose a and b?</p>
<p><strong>Linear regression in two dimensions (with 2 features)</strong></p>
<p>$y = a_1x_1 +a_2x_2 + b$</p>
<p>To fit a linear regression model here:</p>
<ul>
<li>Need to specify 3 variables - $a_1$, $a_2$ and $b$ </li>
</ul>
<p><strong>Linear regression in higher dimensions (with more than 2 features)</strong></p>
<p>$y = a_1x_1 + a_2x_2 + a_3x_3 + a_nx_n + b$</p>
<ul>
<li>Must specify coefficient for each feature ($a_1, a_2,...a_n$) and the variable b  </li>
</ul>
<p><strong>Linear Regression on All Features</strong></p>
<p>To calculate an out-of-the-box regression on any number of variables, pass two arrays: features and target</p>
<div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">train_test_split</span>

<span class="c1"># split data</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>

<span class="c1"># instantiate model</span>
<span class="n">reg_all</span> <span class="o">=</span> <span class="n">linear_model</span><span class="o">.</span><span class="n">LinearRegression</span><span class="p">()</span>

<span class="c1"># fit using training data</span>
<span class="n">reg_all</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># make predictions using test data</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">reg_all</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># score for accuracy</span>
<span class="n">reg_all</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">)</span>
</pre></div>
<p>This is rarely used -- it's normally customized ('regularized')</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[31]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Import necessary modules</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">train_test_split</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="k">import</span> <span class="n">mean_squared_error</span>
<span class="kn">from</span> <span class="nn">sklearn</span> <span class="k">import</span> <span class="n">linear_model</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="k">import</span> <span class="n">LinearRegression</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="k">import</span> <span class="n">Ridge</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="k">import</span> <span class="n">Lasso</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">boston</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">base_url</span> <span class="o">+</span> <span class="s1">&#39;boston.csv&#39;</span><span class="p">)</span>
<span class="n">boston</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>

<span class="c1"># create an array for features</span>
<span class="n">X</span> <span class="o">=</span> <span class="n">boston</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;MEDV&#39;</span><span class="p">,</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">values</span>

<span class="c1"># create an array for labels</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">boston</span><span class="o">.</span><span class="n">MEDV</span><span class="o">.</span><span class="n">values</span>

<span class="c1"># all rows from the Rooms column</span>
<span class="n">X_rooms</span> <span class="o">=</span> <span class="n">X</span><span class="p">[:,</span><span class="mi">5</span><span class="p">]</span>

<span class="c1"># reshape the arrays into a single column, each</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">y</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span>
<span class="n">X_rooms</span> <span class="o">=</span> <span class="n">X_rooms</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span>

<span class="c1"># instantiate and fit the model</span>
<span class="n">reg</span> <span class="o">=</span> <span class="n">linear_model</span><span class="o">.</span><span class="n">LinearRegression</span><span class="p">()</span>
<span class="n">reg</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_rooms</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>

<span class="c1"># calculate and graph the regression line</span>
<span class="n">prediction_space</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="nb">min</span><span class="p">(</span><span class="n">X_rooms</span><span class="p">),</span> <span class="nb">max</span><span class="p">(</span><span class="n">X_rooms</span><span class="p">))</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">prediction_space</span><span class="p">,</span> <span class="n">reg</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">prediction_space</span><span class="p">),</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;black&#39;</span><span class="p">,</span> <span class="n">linewidth</span><span class="o">=</span><span class="mi">3</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">X_rooms</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Value of house / 1000 ($)&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Number of rooms&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA3gAAAHjCAYAAABxUL3nAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4yLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvhp/UCwAAIABJREFUeJzs3Xl4U2XaP/DvkzQtKVvZhYqAoDACAloFX5wZFmeq4mgFcRkHFZ1xQ0CEQjPvvK/Lb8YEyiYjgsuwqKjsdWEUVGAU5gUtFGQRHJHNIALSsjVt0/b5/dGm5iTnJCdp1tPv57q8sDnJyX3SlObmfp77FlJKEBERERERUfIzxTsAIiIiIiIiigwmeERERERERAbBBI+IiIiIiMggmOAREREREREZBBM8IiIiIiIig2CCR0REREREZBBM8IiIiIiIiAyCCR4REREREZFBMMEjIiIiIiIyiJR4B6BH69atZefOneMdBhERERERUVxs27btlJSyTbD7JUWC17lzZxQWFsY7DCIiIiIiorgQQhzWcz8u0SQiIiIiIjIIJnhEREREREQGwQSPiIiIiIjIIJjgERERERERGQQTPCIiIiIiIoNggkdERERERGQQTPCIiIiIiIgMggkeERERERGRQTDBIyIiIiIiMggmeERERERERAbBBI+IiIiIiMggmOAREREREREZBBM8IiIiIiIig2CCR0REREREZBBM8IiIiIiIiAyCCR4REREREZFBMMEjIiIiIiIyiJRonlwIcQjAOQBVACqllFlCiJYAlgLoDOAQgDullMXRjIOIEkNBkRP5a/fjWIkLHTKsyM3ujpx+mfEOi+LACO8FI1xDpBjhtTDCNURSMr4eajEDUL2OQNdXUOTEs+/vQXGpGwCQYbXgmVt76r7+RH3tQokrUa9BL+/4M9ItkBI443In5bWEQ0gpo3fymgQvS0p5yuu2aQBOSykdQog8AC2klFMCnScrK0sWFhZGLU4iir6CIidsq3bB5a6qu81qMcM+vLfh/6IlJSO8F4xwDZFihNfCCNcQScn4eqjFbDEJQADuqp8/61otZoy4OhMrtzlVrw8AclfsVDzGc678kX2CXn+ivnahxJWo16CXWvzekulafAkhtkkps4LdLx5LNG8DsLj2/xcDyIlDDEQUY/lr9/v9ZetyVyF/7f44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GRgxYgTGjx+Pdu3a6RQhEREREZHxMcGjiNq3bx+eeOIJzJw5EwcOHHBqy87OxpgxYzBmzBi0atVKpwiJiIiIiOIHEzyKiB07dmDKlCmYM2cOKisrndratGmDCRMmYMSIEWjevLlOERIRERERxR8meBRWW7ZsQUlJCebPn4+amhqntk6dOqG4uBi33347mjRpolOERERERETxiwkehcX69eths9mwZMkSKKWc2nr06AGLxYJBgwYhOTlZpwiJiIiIiOIfEzwKmlIKq1atgtVqxfLly93aL7jgAlgsFlx11VVcw46IiIiIKAqY4FHA6uvr8fbbb8NqtWLNmjVu7VdffTUsFgsuuOACHaIjIiIiIkpcTPBIs9raWixcuBA2mw2bN292aktKSsJNN90Es9mMHj166BQhEREREVFiY4JHflVVVeH5559HaWkpysvLndpSU1Nxxx13oKioCJ07d9YnQCIiIiIiAsAEj3w4dOgQnn76aUybNg179uxxamvWrBlGjhyJwsJCtG3bVqcIiYiIiIjIERM8crNnzx5Mnz4dTz31FA4fPuzU1rJlS4wbNw6jRo3CKaecolOERERERETkCRM8Oqm8vByPP/44nn32WRw/ftyp7fTTT8fEiRNx9913o2nTpjpFSEREREREvjDBI2zevBklJSV4+eWXUVdX59SWl5eHSZMmYdiwYUhNTdUpQiIiIiIi0oIJXgJbu3YtrFYr3njjDbe23r17w2KxoKCggIuTExEREREZBBO8BKOUwkcffQSr1YqVK1e6tffr1w8WiwWXXXYZFycnIiIiIjIYJngJor6+Hq+//jqsVivWr1/v1n7dddfBbDajT58+OkRHREREREThwAQvzlVXV2PBggUoKSnBli1bnNqSk5Nxyy23wGw2o1u3bjpFSERERERE4aJLgiciVwKYASAZwFyllE2POOLZsWPHMHfuXEyZMgU7duxwaktLS8Ndd92FiRMnokOHDvoESEREREREYRf1BE9EkgE8BeByADsBfCkibyqlvo12LPHowIEDeOqppzBjxgzs27fPqa1FixYYNWoUxo0bh9atW+sUIRERERERRYoePXjnAvhRKfUTAIjIQgDXAWCCF4Ldu3dj2rRpePrpp3H06FGnttNOOw2FhYW49957kZmZqVOEREREREQUaXokeDkAHMcM7gRwnuubRGQEgBEA0L59++hEZkDbtm1DaWkpnn/+eVRXVzu15ebmori4GHfeeSfS09N1ipCIiIiIiKJFjwTPU+195faCUs8AeAYA8vPz3doT3ddffw2bzYZFixahvr7eqe3MM8+E2WzGzTffDJPJpFOEREREREQUbXokeDsBtHP4++kAdukQhyGtXr0aVqsV77zzjlvbeeedhwceeAADBw5EUlKSDtEREREREZGe9EjwvgTQRUQ6AqgAcDOAoTrEYRhKKbz//vuwWq347LPP3Novv/xyWCwWXHLJJVycnIiIiIgogUU9wVNK1YrIaAAfoGGZhOeUUpujHYcR1NXV4bXXXoPNZsOGDRuc2kQEN9xwAywWC3r37q1ThEREREREFEt0WQdPKfUugHf12LcRnDhxAi+++CImT56MH3/80aktJSUFt912G4qLi9G1a1edIiQiIiIiolikS4JHnh09ehTPPPMMpkyZgl27nKclZmRk4O9//zsmTJiAdu3aedkCERERERElMiZ4MeD333/Hk08+iSeffBL79+93asvKysKYMWMwduxYtGrVSqcIiYiIiIjICJjg6Wjnzp2YOnUqnnnmGRw7dsyprU2bNhg/fjzuueceNG/eXKcIiYiIiIjISJjg6WDr1q2YPHkyXnzxRdTU1Di1derUCcXFxRg+fDjS0tJ0ipCIiIiIiIyICV4UffXVV7BarViyZAmUcl67/ayzzoLFYsGgQYOQksLTQkRERESBCxIYAAAJXUlEQVREgWMmEWFKKXz66ad47LHHsHz5crf2vn37wmKx4Oqrr+YadkREREREFBImeBFSX1+Pd955B1arFf/5z3/c2q+66ipYLBZceOGFOkRHRERERETxiAlemNXW1mLhwoUoKSnBpk2bnNqSkpIwePBgmM1m9OzZU6cIiYiIiIgoXjHBC5Oqqio8//zzKC0tRXl5uVNbamoqbr/9dhQXF6Nz5876BEhERERERHGPCV6IDh06hKeffhrTp0/Hb7/95tTWtGlTjBw5EuPHj0fbtm11ipCIiIiIiBIFE7wQHD9+HHl5eW6JXcuWLTF27FiMHj0ap5xyik7RERERERFRoknSOwAjS0tLQ0FBwcm/5+TkYNq0adi+fTv++c9/MrkjIiIiIqKoYg9eiIqKivDZZ59hwoQJuPXWW5Gamqp3SERERERElKCY4IWoU6dO2LRpE9ewIyIi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
"
>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Read in the data</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">base_url</span> <span class="o">+</span> <span class="s1">&#39;gm_2008_region.csv&#39;</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>

<span class="c1"># Create arrays for features and target variable</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">life</span>
<span class="n">X</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">fertility</span>

<span class="c1"># Reshape X and y</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">y</span><span class="o">.</span><span class="n">values</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span>
<span class="n">X</span> <span class="o">=</span> <span class="n">X</span><span class="o">.</span><span class="n">values</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span>

<span class="n">X_fertility</span> <span class="o">=</span> <span class="n">X</span>

<span class="c1"># Create the regressor: reg</span>
<span class="n">reg</span> <span class="o">=</span> <span class="n">linear_model</span><span class="o">.</span><span class="n">LinearRegression</span><span class="p">()</span>

<span class="c1"># Create the prediction space to range from the minimum to the maximum of X_fertility</span>
<span class="n">prediction_space</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="nb">min</span><span class="p">(</span><span class="n">X_fertility</span><span class="p">),</span> <span class="nb">max</span><span class="p">(</span><span class="n">X_fertility</span><span class="p">))</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span>

<span class="c1"># Fit the model to the data</span>
<span class="n">reg</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_fertility</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>

<span class="c1"># Compute predictions over the prediction space: y_pred</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">reg</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">prediction_space</span><span class="p">)</span>

<span class="c1"># Print R^2 </span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;R^2 score: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">reg</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_fertility</span><span class="p">,</span> <span class="n">y</span><span class="p">)))</span>

<span class="n">g</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">&#39;fertility&#39;</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">&#39;life&#39;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">df</span><span class="p">)</span>

<span class="c1"># Plot regression line</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">prediction_space</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;black&#39;</span><span class="p">,</span> <span class="n">linewidth</span><span class="o">=</span><span class="mi">3</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>R^2 score: 0.6192442167740035
</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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iPmHH37QvHnzNH36dH322Wdu4zExMRowYIBM09Qdd9yh6OhoD4+Cugi137kA4EusqAG1EGqfYvNpNEKVnZpINGvWrLKpyNatWzV27Fg1atSocrysrEyLFy/WXXfdpbZt22rKlCk6ePBgwOMMtEDsfw2137kAEAysqAEhiE+jEarsfhDziRMntGjRIjkcDn3wwQdu44Zh6I477pBpmurfv78aNGgQhCj9h98tAOB/rKgBYYxPoxGq7H4Qc6NGjTR69Ght2bJFn3/+uX73u9+pefPmleOWZWndunW677771LJlSz3xxBP64osvghixb7H/FQDsgxU1AEDA2H1FzZOSkhItX75cDodD69atk6f/bvbo0UOZmZm67777XMonQw37XwHA/1hRAwDYjt0PYvYkLi5OQ4YM0Zo1a5SXl6fnnntOl112mcucDz74QJmZmUpKStK4ceO0bds2jwmd3VW1z7VJfGyAIwl/nIUJoCYkagCAgAn1st3WrVtrypQpysvL05o1azRkyBDFxv6SxJw4cULTp0/XjTfeqGuvvVavvvqqfvjhhyBGXDsT+3ZQbJT7GXL/KSkjkfAhOzXVAWBflD4CAFAPR44c0dy5c+VwOPTll1+6jcfFxWnQoEEyTVO9evVSVJS9PyPt+od1Onay1O26nctTQ00olgAD8B1KHwEACIAWLVpUNhXZsmWLRo8erYSEhMrxkpISvfXWW7r99tvVvn17vfjii8rPt+/KSZGHJE2yT8OXcGD3pjoA7IFEDQAAHzAMQz169NCMGTNUWFioN954QzfccIPLnLy8PD3zzDNq1aqV7r77bmVnZ6u01HNiFCyc0+h//BsD8AaJGgAAPta4cWONGzdOW7du1c6dOzVhwgQ1bdq0cryiokKrVq3SPffco8suu0yTJk3S3r17gxjxL0Kx4Uuo4d8YgDfYowYAXsjOyde0tbkqKCpWcmK8JvbtEDINMGAPp06d0tKlS+VwOLRhwwaPc2677TaZpqnBgwe7lE8GGve7//FvDEQub/eokagBQA3Odmg79yDg+NjokOpWCHvZv3+/ZsyYoZkzZ6qgoMBtvEmTJhoxYoQyMzPVrVu3IEQIAPAXmokAgI9MW5vrkqRJUnFpuaatzQ1SRAh17dq10wsvvKCDBw9qxYoVuuHXfaVzukH+9NNPev3113XdddepW7duev3111VU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tDYLYtdHtEbs+ggAAFqVtvhD99atW+W6rhYuXKjjx49HjGdkZGjy5MnKz8/Xtdde60HC2GDHxthqi19LrQlFDQAAtJjL/cGwrf/g/u9//1vLli2T67rauHFjk3MGDRokx3GUl5fXaPlka0WZiI22/rXUGlDUAABAi4jGD4acm/e13bt3q6CgQEVFRTpy5EjE+NVXX63x48fLcRz16tXLg4TwM76W/I9z1AAAQIuIxg5+bLX+tfObihw6dEgrVqzQPffco7i4r39kO3bsmJ577jndfPPN6t+/v+bMmaOTJ096mBh+wtdScFDUAADAZYnGD4ZstR4pMTFReXl5Kikp0f79+/WHP/xB3bp1azRny5YtevDBB5Wenq78/Hy9/fbbbWqbf0Tiayk4KGoAAOCyROMHQ7Za/25dunTRjBkztGfPHq1bt06jR4/WFVdccWH89OnTKiwsVE5Ojm666Sb95S9/0dGjRz1MDK/wtRQcFDUAAHBZovGDIefmNU9cXJwGDx6sRYsWqaKiQs8++6x++tOfNpqzc+dOPf7448rMzNTIkSO1Zs0a1dXVfctnRNDwtRQcbCYCAAAuGzv4ecdaq3feeUeu62rRokU6depUxJysrCzl5+dr8uTJysrK8iAlgPPY9REAAKCNOXXqlBYvXizXdbV58+aIcWOM7r77bjmOo3vvvbfR8kkALYOiBgBAG9NST7V4etY6fPjhhwqHw5o7d66++OKLiPG0tDRNmDBBoVBIPXv29CAh0DZR1AAAaENa6pBbDtNtfWpqarRq1Sq5rqt169Y1uSvk7bffLsdxNGrUKCUnJ3uQMrh4YQPfxDlqAAC0IdE4y8xPfw+ip127dhc2Fdm7d69+//vfq2vXro3mvP3228rPz1d6eroeeughbdmyhW3+o+D8CxvlVdWyksqrqjV9eZmKS8u9joZWgKIGAEAAtNQhtxym27r95Cc/0cyZM7V371699tprGjFihBISEi6Mnzx5Ui+++KL69++vW265Rc8995y+/PJLDxO3brywgctBUQMAIABa6pBbDtMNhvj4eP3617/W0qVLVV5erj//+c+68cYbG80pKyvTY489poyMDD3wwANav3696uvrPUrcOvHCBi4HRQ0AgABoqUNuOUw3eH784x/r8ccf14cffqhNmzZp0qRJuvLKKy+M19TUaNGiRRo0aJCuu+46zZo1S+XlLN1rDl7YwOWgqAEAEAAtdcgth+kGlzFGOTk5KiwsVGVlpf7+97/r1ltvbTRn7969mjFjhrKysjRs2DCtXLlS586d8yix//HCBi4Huz4CAADgW23fvl3hcFgLFizQsWPHIsY7d+6sSZMmKRQK6frrr/cgob+x6yO+ie35AQAAEDVnzpzR8uXLFQ6HtX79+ibnDBw4UKFQSCNGjGi0fBLA16Ja1Iwx+ySdlFQnqdZa29cYM1PSf0g62jDtf6y1r37X56GooS3hFTQA8De+T/9we/bsUUFBwYVlkt/UoUMHjR07Vo7jqHfv3h4kBPwrFkWtr7X284uuzZR0ylr75+aGoqihreBAWADwN75PR0dtba1Wr14t13VVUlKiurq6iDl9+vSR4zgaM2aMUlNTPUgJ+AsHXgMe4twUAPA3vk9HR0JCgoYOHari4mIdPHhQTz31lHr06NFoztatW/Xb3/5W6enpmjBhgjZu3Mhh2kAzNLeoWUlrjTHvGWMevOj6o8aY940xBcaYq5v6QGPMg8aYd40x7x49erSpKUDgcG4KAPgb36ejLz09XdOmTdNHH32kDRs2aOzYsWrXrt2F8TNnzmj+/PkaOHCgsrOz9fTTT+vw4cMeJo694tJy5cxer+7TXlHO7PUqLuVYAzRfc4tajrW2j6Qhkh4xxvxS0guSekj6maRKSf/b1Adaa1+01va11vZNS0uLRmbA9zg3BQD8je/TsRMXF6c777xTCxYsUGVlpf72t7/plltuaTTn448/1rRp09SlSxf95je/0SuvvKLa2lqPEsfG+eW15VXVspLKq6o1fXkZZQ3N1qyiZq2taPj9iKQVkvpZaz+z1tZZa+slzZHUL3YxgdaFc1MAwN/4Pt0yrr76aj366KMqLS3VO++8o4cfflhXXXXVhfG6ujoVFxdr6NCh6tatm2bMmKFPP/3Uw8TRw/JaXK7vLWrGmGRjTMr5P0u6W9IHxpj0i6b9RtIHsYkItD4cCAsA/sb36ZZljFHfvn31wgsvqKKiQkVFRbrjjjsazSkvL9esWbPUo0cPDR48WC+//LLOnDnjUeLLx/JaXK7v3fXRGHOtvnqKJkkJkhZaa2cZY+brq2WPVtI+SQ9ZayP3Z70Iuz4CAADgvF27dqmgoEBz587VkSNHIsY7duyocePGyXEc9erVy4OEP1zO7PUqb6KUZaYm6a1pd3mQCH7BgdcAAABoFc6ePauSkhKFw2GtXr1a9fX1EXP69esnx3E0evRopaSkeJDy0nAEBL4NRQ0AAACtzsGDB1VUVKRwOKz9+/dHjCcnJ2vUqFFyHEcDBgyQMcaDlM3DoepoCkUNAAAArVZ9fb1ef/11hcNhrVixQmfPno2Y07NnTzmOo/Hjx4vdxdFaUNQAAAAQCJ9//rnmz5+vcDisHTt2RIwnJibqvvvuk+M4Gjx4sOLj45v4LIA/UNQAAAAQKNZabdmyRa7ratGiRTp9+nTEnKysLOXn52vy5MnKysryICXw3ShqAAAACKyTJ09q8eLFcl1X//rXvyLGjTG6++675TiO7r33Xl1xxRUepAQiUdQAAADQJuzYsUPhcFjz5s3TF198ETHeqVMnTZw4UaFQSD179vQgIfA1ihoAAADalJqaGq1cuVKu62rdunVNzrn99tvlOI5GjRql5OTkFk4IUNQAAADQhu3bt0+FhYUqKCjQoUOHIsZTUlI0ZswYhUIh3Xrrrb7e5h/BQlEDAABAm1dXV6e1a9cqHA5r5cqVqq2tjZjTq1cvOY6jcePGqWPHjh6kRFtCUQMAAAAu8tlnn2n+/PlyXVe7d++OGG/Xrp2GDx8ux3F05513Ki4uzoOUCDqKGgAAANAEa63eeustua6rxYsXq7q6OmJO9+7dFQqFNGnSJGVmZnqQEkFFUQMAAAC+x/Hjx/Xyyy/LdV019XNqXFychgwZIsdxdM899ygxMdGDlAgSihoAAABwCbZt26ZwOKwFCxaoqqoqYrxz586aNGmSQqGQrr/+eg8SIggoagAAAMAPUF1drRUrVsh1XW3YsKHJOQMHDlQoFNKIESN05ZVXtnBCtGYUNQAAAOAyffLJJyooKFBRUZEqKysjxjt06KCxY8fKcRz17t3bg4RobShqAAAAQJTU1tbqtddek+u6euWVV1RXVxcxp0+fPnIcR2PGjFFqaqoHKdEaUNQAAACAGKioqNDcuXMVDoe1Z8+eiPH27dtr5MiRchxHd9xxB4dpoxGKGgAAABBD9fX12rhxo1zX1dKlS1VTUxMx54YbblAoFNKECRN0zTXXeJASfkNRAwAAAFrIsWPH9NJLL8l1XW3fvj1iPCEhQUOHDpXjOMrNzVVCQoIHKeEHFDUAAACghVlrtXXrVrmuq4ULF+rEiRMRczIzMzV58mTl5+ere/fuHqSElyhqAAAAgIdOnz6tJUuWKBwOa9OmTU3OGTRokBzHUV5entq3b9/CCeEFihoAAADgE7t27bqwzf/Ro0cjxjt27Kjx48crFAqpV69eHiRES6GoAQAAAD5z9uxZlZSUyHVdrVmzRvX19RFz+vXrJ8dxNHr0aKWkpHiQErFEUQMAAGjlikvL9cya3aqoqlZGapKm5mYrr3em17EQJQcPHlRRUZHC4bD2798fMZ6cnKz7779foVBIAwYMYJv/gKCoAQAAtGLFpeWavrxM1ee+Plg5KTFeTw3vRVkLmPr6er3++utyXVfFxcU6e/ZsxJyePXvKcRyNHz9eaWlpHqREtDS3qMW1RBgAAABcmmfW7G5U0iSp+lydnlmz26NEiJW4uDj96le/0j/+8Q+Vl5frr3/9q2666aZGc3bu3KnHH39cmZmZGjVqlNauXdvkskkEB0UNAADAhyqqqi/pOoKhU6dOmjJlisrKyrR582aFQiElJydfGD937pyWLFmi3Nxcde/eXU8++aQOHDjgYWLECkUNAADAhzJSky7pOoLFGKPbbrtNruuqsrJSruvqtttuazTnwIEDmjlzprp166YhQ4Zo6dKlTS6bROtEUQMAAPChqbnZSkqMb3QtKTFeU3OzPUoEr6SkpCgUCmnz5s0qKyvTlClT9KMf/ejCuLVWq1ev1siRI9WlSxf97ne/086dOz1MjGhgMxEAAIAW8EN2cGTXR3ybmpoarVy5Uq7rat26dU3OycnJUSgU0qhRoxotn4S32PURAADAJ9jBEbG0d+9eFRYWqqCgQOXl5RHjKSkpGjNmjBzHUd++fdnm32MUNQAA4Dtt9QlRzuz1Km9iE5DM1CS9Ne0uDxIhiOrq6rR27Vq5rqtVq1aptrY2Ys7NN9+sUCikcePGqWPHjh6kBNvzAwAAXzn/VKm8qlpWUnlVtaYvL1NxaeQTgKBhB0e0hPj4eA0ZMkTLli3ToUOH9Kc//UnZ2Y3f0/j+++/rscceU0ZGhh544AGtX7+ebf59iqIGAABaRFs+F4wdHNHSOnfurKlTp2rnzp168803NXHiRCUlff3fW01NjRYtWqRBgwbp+uuv16xZs5pcNgnvUNQAAECLaMtPldjBEV4xxugXv/iFioqKVFlZqRdeeEF9+zZedffpp59qxowZysrK0rBhw7Ry5UqdO3fOo8Q4j6IGAABaRFt+qpTXO1NPDe+lzNQkGX313jQ2EkFL69Chgx5++GG98847Ki0t1aOPPqrU1NQL4/X19SopKVFeXp66du2qadOm6eOPP/YwcdvGZiIAAKBFsPMh4D/V1dVasWKFXNfVhg0bmpwzcOBAOY6jESNGNFo+iR+GXR8BAIDvtNVdH4HW4JNPPlFBQYEKCwt1+PDhiPEOHTpo7NixchxHvXv39iBhMFDUAAAAAFyy2tpavfrqq3JdV6+++qrq6uoi5vTp00eO42jMmDGNlk/i+1HUAAAAAFyWiooKzZ07V+FwWHv27IkYb9++vUaOHCnHcXTHHXdwmHYzUNQAAAAAREV9fb02btwo13W1dOlS1dTURMy54YYbFAqFNGHCBF1zzTUepGwdKGoAAAAAou7YsWN66aWX5Lqutm/fHjEeHx+vYcOGyXEc5ebmKiEhwYOU/kVRAwAAABAz1lpt3bpVrutq4cKFOnHiRMSczMxMTZ48Wfn5+erevbsHKf2HogYAAACgRZw+fVpLly6V67ratGlTk3MGDRokx3GUl5en9u3bt3BC/4hqUTPG7JN0UlKdpFprbV9jTEdJ/5DUTdI+SaOstce+6/NQ1AAAAIBg27Vrl8LhsObOnaujR49GjHfs2FHjx49XKBRSr169PEjorVgUtb7W2s8vuvYnSV9aa2cbY6ZJutpa+8R3fR6KGgAAANA2nD17ViUlJXJdV2vWrFF9fX3EnH79+slxHI0ePVopKSkepGx5LVHUdku601pbaYxJl/SGtTb7uz4PRQ0AAABoew4ePKiioiKFw2Ht378/Yjw5OVn333+/QqGQBgwYEOht/qNd1PZKOibJSvq7tfZFY0yVtTb1ojnHrLVXN/GxD0p6UJKysrJ+3tSNAQAAABB89fX1ev311+W6roqLi3X27NmIOT179pTjOBo/frzS0tI8SBlb0S5qGdbaCmPMjyWtk/SfklY1p6hdjCdqAAAAACTp888/14IFC+S6rnbs2BExnpiYqLy8PDmOo8GDBysuLs6DlNHX3KLWrH9ba21Fw+9HJK2Q1E/SZw1LHtXw+5EfHhcAAABAW9KpUydNmTJFZWVl2rx5sxzHUXJy8oXxc+fOacmSJcrNzVX37t315JNP6sCBAx4mblnfW9SMMcnGmJTzf5Z0t6QPJK2SNLFh2kRJK2MVEgAAAEAwGWN02223ac6cOaqsrJTruurfv3+jOQcOHNDMmTPVrVs3DRkyRMuWLWty2WSQfO/SR2PMtfrqKZokJUhaaK2dZYz5kaTFkrIkHZA00lr75Xd9LpY+AgAAAGiODz74QOFwWPPnz9cXX3wRMZ6WlqaJEycqFArpxhtv9CDhD8OB1wAAAABavZqaGq1cuVKu62rdunVNzsnJyZHjOBo5cmSj5ZN+RFEDAAAAECj79u1TYWGhCgoKdOjQoYjxlJQUPfDAA3IcRz//+c99uc0/RQ0AAABAINXV1Wnt2rVyXVerVq1SbW1txJybb75Z8+bN0y233OJBwm9HUQOANqi4tFzPrNmtiqpqZaQmaWputvJ6Z3odCwCAmPnss880b948hcNh7d69+8L1du3aqaKiQh07dvQwXaSobs8PAPC/4tJyTV9epvKqallJ5VXVmr68TMWl5V5HAwAgZjp37qypU6dq586devPNNzVx4kQlJSVp+PDhvitpl4InagAQEDmz16u8qjriemZqkt6adpcHiQAA8Mbx48d14sQJde3a1esoEZr7RC2hJcIAAGKvoomS9l3XAQAIqg4dOqhDhw5ex7gsLH0EgIDISE26pOsAAMC/KGoAEBBTc7OVlBjf6FpSYrym5mZ7lAgAAPxQLH0EgIA4v7sjuz4CAND6UdQAIEDyemdSzAAACACWPgIAAACAz1DUAAAAAMBnKGoAAAAA4DMUNQAAAADwGYoaAAAAAPgMRQ0AAAAAfIaiBgAAAAA+Q1EDAAAAAJ+hqAEAAACAz1DUAAAAAMBnKGoAAAAA4DMUNQAAAADwGYoaAAAAAPgMRQ0AAAAAfIaiBgAAAAA+Q1EDAAAAAJ+hqAEAAACAz1DUAAAAAMBnKGoAAAAA4DMUNQAAAADwGYoaAAAAAPgMRQ0AAAAAfCbB6wAAAKm4tFzPrNmtiqpqZaQmaWputvJ6Z3odCwAAeISiBgAeKy4t1/TlZao+VydJKq+q1vTlZZJEWQMAoI1i6SMAeOyZNbsvlLTzqs/V6Zk1uz1KBAAAvEZRAwCPVVRVX9J1AAAQfBQ1APBYRmrSJV0HAADBR1EDAI9Nzc1WUmJ8o2tJifGampvtUSIAAOA1NhMBAI+d3zCEXR8BAMB5FDUA8IG83pkUMwAAcAFLHwEAAADAZyhqAAAAAOAzLH0EEFjFpeW87wsAALRKFDUAgVRcWq7py8suHCRdXlWt6cvLJImyBgAAfK/ZSx+NMfHGmFJjTEnDPxcZY/YaY7Y1/PpZ7GICwKV5Zs3uCyXtvOpzdXpmzW6PEgEAADTfpTxRe0zSTklXXXRtqrV2aXQjAcDlq6iqvqTrAAAAftKsJ2rGmC6S7pHkxjYOAERHRmrSJV0HAADwk+YufXxW0n9Lqv/G9VnGmPeNMX81xrRr6gONMQ8aY941xrx79OjRy8kKAM02NTdbSYnxja4lJcZram62R4kAAACa73uLmjFmqKQj1tr3vjE0XdKNkm6V1FHSE019vLX2RWttX2tt37S0tMvNCwDNktc7U08N76XM1CQZSZmpSXpqeC82EgEAAK1Cc96jliPpXmPM/5XUXtJVxpgF1tpxDeM1xphCSb+LVUgA+CHyemdSzAAAQKv0vU/UrLXTrbVdrLXdJI2WtN5aO84Yky5JxhgjKU/SBzFNCgAAAABtxOWco/aSMSZNkpG0TdLD0YkEAAAAAG3bJRU1a+0bkt5o+PNdMcgDAAAAAG1esw+8BgAAAAC0DIoaAAAAAPgMRQ0AAAAAfIaiBgAAAAA+Q1EDAAAAAJ+hqAEAAACAz1DUAAAAAMBnKGoAAAAA4DMUNQAAAADwGYoaAAAAAPgMRQ0AAAAAfIaiBgAAAAA+Y6y1LfeXGXNU0v5vXO4k6fMWC4GWxv0NPu5xsHF/g497HGzc32Dj/rZOP7HWpn3fpBYtak0GMOZda21fT0MgZri/wcc9Djbub/Bxj4ON+xts3N9gY+kjAAAAAPgMRQ0AAAAAfMYPRe1FrwMgpri/wcc9Djbub/Bxj4ON+xts3N8A8/w9agAAAACAxvzwRA0AAAAAcBGKGgAAAAD4jGdFzRhTYIw5Yoz5wKsMiB1jTFdjzAZjzE5jzA5jzGNeZ0L0GGPaG2O2GGO2N9zfJ73OhOgzxsQbY0qNMSVeZ0H0GWP2GWPKjDHbjDHvep0H0WeMSTXGLDXG7Gr4//EArzMhOowx2Q1fu+d/nTDGTPE6F6LLs/eoGWN+KemUpHnW2p96EgIxY4xJl5Rurd1qjEmR9J6kPGvthx5HQxQYY4ykZGvtKWNMoqRNkh6z1v7L42iIImPMf0nqK+kqa+1Qr/Mguowx+yT1tdZyWG5AGWPmSnrTWusaY66QdKW1tsrrXIguY0y8pHJJ/a21+73Og+jx7ImatXajpC+9+vsRW9baSmvt1oY/n5S0U1Kmt6kQLfYrpxr+MbHhFzsTBYgxpoukeyS5XmcBcOmMMVdJ+qWksCRZa89S0gJrkKQ9lLTg4T1qiDljTDdJvSX9P2+TIJoalsVtk3RE0jprLfc3WJ6V9N+S6r0OgpixktYaY94zxjzodRhE3bWSjkoqbFjC7Bpjkr0OhZgYLWmR1yEQfRQ1xJQx5v9IWiZpirX2hNd5ED3W2jpr7c8kdZHUzxjDEuaAMMYMlXTEWvue11kQUznW2j6Shkh6pOEtCQiOBEl9JL1gre0t6bSkad5GQrQ1LGm9V9ISr7Mg+ihqiJmG9y4tk/SStXa513kQGw1Lad6Q9GuPoyB6ciTd2/Aeppcl3WWMWeBtJESbtbai4fcjklZI6udtIkTZIUmHLlrtsFRfFTcEyxBJW621n3kdBNFHUUNMNGw2EZa001r7F6/zILqMMWnGmNSGPydJGixpl7epEC3W2unW2i7W2m76aknNemvtOI9jIYqMMckNGz2pYTnc3ZLYhTlArLWHJR00xmQ3XBokiQ29gmeMWPYYWAle/cXGmEWS7pTUyRhzSNLvrbVht4pb8QAAAJxJREFUr/Ig6nIkjZdU1vA+Jkn6H2vtqx5mQvSkS5rbsNNUnKTF1lq2cAdaj86SVnz1mpoSJC201q72NhJi4D8lvdSwPO5TSZM9zoMoMsZcKelXkh7yOgtiw7Pt+QEAAAAATWPpIwAAAAD4DEUNAAAAAHyGogYAAAAAPkNRAwAAAACfoagBAAAAgM9Q1AAAAADAZyhqAAAAAOAz/x9txicl6Lbn2QAAAABJRU5ErkJggg==
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
<p>Below, another regression is run using all of the features.  The $R^2$ score is better, but may lead to overfitting the model.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[21]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Create training and test sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>

<span class="c1"># Create the regressor: reg_all</span>
<span class="n">reg_all</span> <span class="o">=</span> <span class="n">linear_model</span><span class="o">.</span><span class="n">LinearRegression</span><span class="p">()</span>

<span class="c1"># Fit the regressor to the training data</span>
<span class="n">reg_all</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># Predict on the test data: y_pred</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">reg_all</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># Compute and print R^2 and RMSE</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;R^2: </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">reg_all</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">)))</span>
<span class="n">rmse</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">mean_squared_error</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Root Mean Squared Error: </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">rmse</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[21]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>LinearRegression(copy_X=True, fit_intercept=True, n_jobs=1, normalize=False)</pre>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>R^2: 0.7298987360907498
Root Mean Squared Error: 4.194027914110239
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
<h2 id="Regularized-Regression">Regularized Regression<a class="anchor-link" href="#Regularized-Regression">&#182;</a></h2><p>Linear regression minimizes a loss function by choosing a coefficient for EACH feature variable. Large coefficients can lead to overfitting. Regularization penalizes large coefficients to prevent overfitting.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Ridge-Regression">Ridge Regression<a class="anchor-link" href="#Ridge-Regression">&#182;</a></h3><p><strong>Ridge Regression</strong>: penalizes coefficients of a large magnitude (positive or negative) to avoid overfitting.  Lasso regression is great for feature selection, but when building regression models, Ridge regression should be the first choice.<br>
$$Ridge\ regression\ loss\ function\ =\ OLS\ function\ +\ \alpha * \sum_{i=1}^n a^2_i$$</p>
<p>OLS function + squared value of each coefficient * some constant, $\alpha$.  This penalizes models with coefficients of a large magnitude (both positive and negative).</p>
<p><strong>Tuning</strong>: We need to choose $\alpha$, which is similar to picking k in k-NN.  This is called hyperparameter tuning.  $\alpha$ controls model complexity.</p>
<ul>
<li>if $\alpha$ = 0, we get regular OLS (can lead to overfitting - eliminates regularization altogether)</li>
<li>if $\alpha$ is too high, you get a model that is too simple</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[55]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>

<span class="c1"># Setting alpha and normalizing to make sure all of our variables are in the same scale</span>
<span class="n">ridge</span> <span class="o">=</span> <span class="n">Ridge</span><span class="p">(</span><span class="n">alpha</span><span class="o">=</span><span class="mf">0.1</span><span class="p">,</span> <span class="n">normalize</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="n">ridge</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
<span class="n">ridge_pred</span> <span class="o">=</span> <span class="n">ridge</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>
<span class="n">ridge</span><span class="o">.</span><span class="n">score</span><span class="p">(</span><span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[55]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Ridge(alpha=0.1, copy_X=True, fit_intercept=True, max_iter=None,
   normalize=True, random_state=None, solver=&#39;auto&#39;, tol=0.001)</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[55]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>0.8442469959975754</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[56]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">display_plot</span><span class="p">(</span><span class="n">cv_scores</span><span class="p">,</span> <span class="n">cv_scores_std</span><span class="p">):</span>
    <span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>
    <span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">alpha_space</span><span class="p">,</span> <span class="n">cv_scores</span><span class="p">)</span>

    <span class="n">std_error</span> <span class="o">=</span> <span class="n">cv_scores_std</span> <span class="o">/</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span>

    <span class="n">ax</span><span class="o">.</span><span class="n">fill_between</span><span class="p">(</span><span class="n">alpha_space</span><span class="p">,</span> <span class="n">cv_scores</span> <span class="o">+</span> <span class="n">std_error</span><span class="p">,</span> <span class="n">cv_scores</span> <span class="o">-</span> <span class="n">std_error</span><span class="p">,</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.2</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">set_ylabel</span><span class="p">(</span><span class="s1">&#39;CV Score +/- Std Error&#39;</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">set_xlabel</span><span class="p">(</span><span class="s1">&#39;Alpha&#39;</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">axhline</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">cv_scores</span><span class="p">),</span> <span class="n">linestyle</span><span class="o">=</span><span class="s1">&#39;--&#39;</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;.5&#39;</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">set_xlim</span><span class="p">([</span><span class="n">alpha_space</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="n">alpha_space</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">]])</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">set_xscale</span><span class="p">(</span><span class="s1">&#39;log&#39;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[57]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">&#39;figure.figsize&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="mi">10</span><span class="p">,</span> <span class="mi">10</span><span class="p">]</span>

<span class="c1"># Import necessary modules</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="k">import</span> <span class="n">Ridge</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">cross_val_score</span>

<span class="c1"># Setup the array of alphas and lists to store scores</span>
<span class="n">alpha_space</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">logspace</span><span class="p">(</span><span class="o">-</span><span class="mi">4</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">50</span><span class="p">)</span>
<span class="n">ridge_scores</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">ridge_scores_std</span> <span class="o">=</span> <span class="p">[]</span>

<span class="c1"># Create a ridge regressor: ridge</span>
<span class="n">ridge</span> <span class="o">=</span> <span class="n">Ridge</span><span class="p">(</span><span class="n">normalize</span> <span class="o">=</span> <span class="kc">True</span><span class="p">)</span>

<span class="c1"># Compute scores over range of alphas</span>
<span class="k">for</span> <span class="n">alpha</span> <span class="ow">in</span> <span class="n">alpha_space</span><span class="p">:</span>

    <span class="c1"># Specify the alpha value to use: ridge.alpha</span>
    <span class="n">ridge</span><span class="o">.</span><span class="n">alpha</span> <span class="o">=</span> <span class="n">alpha</span>
    
    <span class="c1"># Perform 10-fold CV: ridge_cv_scores</span>
    <span class="n">ridge_cv_scores</span> <span class="o">=</span> <span class="n">cross_val_score</span><span class="p">(</span><span class="n">ridge</span><span class="p">,</span> <span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">cv</span><span class="o">=</span><span class="mi">10</span><span class="p">)</span>
    
    <span class="c1"># Append the mean of ridge_cv_scores to ridge_scores</span>
    <span class="n">ridge_scores</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">ridge_cv_scores</span><span class="p">))</span>
    
    <span class="c1"># Append the std of ridge_cv_scores to ridge_scores_std</span>
    <span class="n">ridge_scores_std</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">std</span><span class="p">(</span><span class="n">ridge_cv_scores</span><span class="p">))</span>

<span class="c1"># Display the plot</span>
<span class="n">display_plot</span><span class="p">(</span><span class="n">ridge_scores</span><span class="p">,</span> <span class="n">ridge_scores_std</span><span class="p">)</span>
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
<h3 id="Lasso-Regression">Lasso Regression<a class="anchor-link" href="#Lasso-Regression">&#182;</a></h3><p><strong>Lasso Regression</strong>: Very useful for identifying which features have the greatest impact on the regression.<br>
$$Lasso\ Regression\ Loss\ function = OLS\ function\ +\ \alpha * \sum_{i=1}^n \vert a_i \vert$$</p>
<ul>
<li>adds to the OLS loss function a penalty term of the absolute value of each coefficient multiplied by some $\alpha$.  <ul>
<li>known as <strong>$L1$ regularization</strong> because the regularization term is the $L1$ norm of the coefficients:  </li>
</ul>
</li>
<li>used to select the most important features of a dataset:<ul>
<li>it shrinks the coefficients of less important features to exaclty 0.</li>
<li>features whose coefficients aren't shrunk to 0 are 'selected'</li>
</ul>
</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[53]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Read in the data</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">base_url</span> <span class="o">+</span> <span class="s1">&#39;gm_2008_region.csv&#39;</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>

<span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;Region&#39;</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>

<span class="c1"># Create arrays for features and target variable</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">life</span><span class="o">.</span><span class="n">values</span>
<span class="n">X</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;life&#39;</span><span class="p">,</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">values</span>

<span class="n">X</span><span class="o">.</span><span class="n">shape</span>
<span class="n">y</span><span class="o">.</span><span class="n">shape</span>

<span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;life&#39;</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">df_columns</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">columns</span>
<span class="n">df_columns</span>

<span class="c1"># Instantiate a lasso regressor: lasso</span>
<span class="n">lasso</span> <span class="o">=</span> <span class="n">Lasso</span><span class="p">(</span><span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.4</span><span class="p">,</span> <span class="n">normalize</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="c1"># Fit the regressor to the data</span>
<span class="n">lasso</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>

<span class="c1"># Compute and print the coefficients</span>
<span class="n">lasso_coef</span> <span class="o">=</span> <span class="n">lasso</span><span class="o">.</span><span class="n">coef_</span>
<span class="nb">print</span><span class="p">(</span><span class="n">lasso_coef</span><span class="p">)</span>

<span class="c1"># Plot the coefficients</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">df_columns</span><span class="p">)),</span> <span class="n">lasso_coef</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xticks</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">df_columns</span><span class="p">)),</span> <span class="n">df_columns</span><span class="o">.</span><span class="n">values</span><span class="p">,</span> <span class="n">rotation</span><span class="o">=</span><span class="mi">60</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">margins</span><span class="p">(</span><span class="mf">0.02</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>[-0.         -0.         -0.          0.          0.          0.
 -0.         -0.07087587]
</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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v6P7vyUAjIiIiIiImAOSlgE+Su0F/C5woO2n2ntjKvVzIAFgRERERETECyRpReBNwFK2j2nHXgtMp9I+d+9zfM8nAWBERERERMSfIGkysJDt30n6KXArVf1zUeCDts9t5y3WzhmTq38Ak/oeQERERERExBi3E7CwpHuBB2zvBjP3AR4l6VFgQ+BhgLEa/EEawUdERERERDyfR4C1gLcAkyT9RavcepztqVTD96fGcuA3kBTQiIiIiIiI59FW+14HvAy4HfgJcLPt+zvnjNnUz4EEgBEREREREbMxCOgkTQVOArah+vztAkwFbgMutH1tj8N8UZICGhERERERMRud1bx9gYts32/7btufBE4B1gH+u7cBzoEEgBEREREREX/a3cD8sxx7KXCT7dt7GM8cSwpoRERERETEnyBpTeAg4EzgeuAe4BpgU9t3SpKHJLBKABgREREREfE8JG0EbABsBPwHcJXtLw5D4ZeuBIAREREREREvgKRFqCIwk2z/Zzs2NKt/kAAwIiIiIiJiwkgRmIiIiIiIiAkiAWBERERERMQEkQAwIiIiIiJigkgAGBERERERMUEkAIyIiIiIiJggEgBGRERERERMEAkAIyIiIiIiJoj/D7etZA05eeilAAAAAElFTkSuQmCC
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
<p><strong>ANSWER</strong>:  According to the lasso algorithm, it seems like 'child_mortality' is the most important feature when predicting life expectancy.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Measuring-&amp;-Tuning-Your-Models">Measuring &amp; Tuning Your Models<a class="anchor-link" href="#Measuring-&amp;-Tuning-Your-Models">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Confusion-Matrix">Confusion Matrix<a class="anchor-link" href="#Confusion-Matrix">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>Class imbalance</strong>
I build a spam classifier that predicts ALL emails are ham.  If I get 99% ham and 1% spam, my filter looks like it's 99% accurate, but it's actually terrible at its stated purpose.  So, accuracy is not always the best measure.  This is called class imbalance - when data coming in is imbalanced and it throws off accuracy ratings.</p>
<h3 id="Diagnosing-classification-problems"><strong>Diagnosing classification problems</strong><a class="anchor-link" href="#Diagnosing-classification-problems">&#182;</a></h3><p><strong>Confusion Matrix</strong>:
We're trying to detect spam, so 'spam' is the positive class, or the class of interest.</p>
<table>
<thead>
<tr>
<th></th>
<th>Predicted: Spam</th>
<th>Predicted: Ham</th>
</tr>
</thead>
<tbody>
<tr>
<td>Actual: Spam</td>
<td>True Positive</td>
<td>False Negative</td>
</tr>
<tr>
<td>Actual: Ham</td>
<td>False Positive</td>
<td>True Negative</td>
</tr>
</tbody></table><p>First term (True or False): True if the prediction was correct.<br>
Second term (Positive or Negative): positive if the predicted value is the class of interest<br>
True Positive: predicted class of interest correctly<br>
True Negative: predicted NOT the class of interest correctly<br>
False Positive: predicted class of interest INcorrectly<br>
False Negative: predicted NOT the class of interest INcorrectly</p>
<p><img src="Images/confusion_matrix_3.png" alt="confusion"></p>
<p>Confusion matrix gives you:<br>
<strong>Accuracy</strong>
$$Accuracy\ =\ \frac{tp + tn}{tp+tn+fp+fn}$$</p>
<p><strong>Precision</strong>  also known as the 'Positive Prorated Value', or 'PPV'.  In this case, this is the number of correctly labeled spam emails / all emails identified as spam.<br>
$$Precision\ =\ \frac{tp}{tp + fp}$$</p>
<p><strong>Recall</strong>: also called 'sensitivity', 'hit rate' or 'true positive rate'
$$Recall\ =\ \frac{tp}{tp + fn}$$</p>
<p><strong>F1 score</strong>: aka the 'harmonic mean' of precision and recall.
$$F1\ score\ =\ 2 * \frac{precision * recall}{precision + recall}$$</p>
<p>The $F_1$ score favors classifiers that have similar precision and recall. This is not always what you want: in some contexts you mostly care about precision, and in other contexts you really care about recall. For example, if you trained a classifier to detect videos that are safe for kids, you would probably prefer a classifier that rejects many good videos (low recall) but keeps only safe ones (high precision), rather than a classifier that has a much higher recall but lets a few really bad videos show up in your product (in such cases, you may even want to add a human pipeline to check the classifier’s video selection).</p>
<p>If you say our classifier has:<br>
High precision: our classifier has a low false positive rate - not many ham emails classified as spam<br>
High recall: our classifier predicted most spam emails correctly</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[59]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># setup</span>
<span class="n">db</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="n">base_url</span> <span class="o">+</span> <span class="s1">&#39;diabetes.csv&#39;</span><span class="p">)</span>
<span class="n">db</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>

<span class="c1"># Create arrays for the features and the response variable</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">db</span><span class="o">.</span><span class="n">diabetes</span><span class="o">.</span><span class="n">values</span>
<span class="n">X</span> <span class="o">=</span> <span class="n">db</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;diabetes&#39;</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>

<span class="n">X</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[59]:</div>



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
      <th>pregnancies</th>
      <th>glucose</th>
      <th>diastolic</th>
      <th>triceps</th>
      <th>insulin</th>
      <th>bmi</th>
      <th>dpf</th>
      <th>age</th>
      <th>diabetes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>148</td>
      <td>72</td>
      <td>35</td>
      <td>0</td>
      <td>33.6</td>
      <td>0.627</td>
      <td>50</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>85</td>
      <td>66</td>
      <td>29</td>
      <td>0</td>
      <td>26.6</td>
      <td>0.351</td>
      <td>31</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>183</td>
      <td>64</td>
      <td>0</td>
      <td>0</td>
      <td>23.3</td>
      <td>0.672</td>
      <td>32</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>89</td>
      <td>66</td>
      <td>23</td>
      <td>94</td>
      <td>28.1</td>
      <td>0.167</td>
      <td>21</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>137</td>
      <td>40</td>
      <td>35</td>
      <td>168</td>
      <td>43.1</td>
      <td>2.288</td>
      <td>33</td>
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
RangeIndex: 768 entries, 0 to 767
Data columns (total 8 columns):
pregnancies    768 non-null int64
glucose        768 non-null int64
diastolic      768 non-null int64
triceps        768 non-null int64
insulin        768 non-null int64
bmi            768 non-null float64
dpf            768 non-null float64
age            768 non-null int64
dtypes: float64(2), int64(6)
memory usage: 48.1 KB
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[61]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Import necessary modules</span>
<span class="c1"># sklearn.model_selection.train_test_split</span>
<span class="c1"># sklearn.neighbors.KNeighborsClassifier</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="k">import</span> <span class="n">classification_report</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="k">import</span> <span class="n">confusion_matrix</span>


<span class="c1"># Create training and test set</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span><span class="o">=</span><span class="mf">0.4</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>

<span class="c1"># Instantiate a k-NN classifier: knn</span>
<span class="n">knn</span> <span class="o">=</span> <span class="n">KNeighborsClassifier</span><span class="p">(</span><span class="n">n_neighbors</span><span class="o">=</span><span class="mi">6</span><span class="p">)</span>

<span class="c1"># Fit the classifier to the training data</span>
<span class="n">knn</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[61]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>KNeighborsClassifier(algorithm=&#39;auto&#39;, leaf_size=30, metric=&#39;minkowski&#39;,
           metric_params=None, n_jobs=1, n_neighbors=6, p=2,
           weights=&#39;uniform&#39;)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="predict()"><strong><code>predict()</code></strong><a class="anchor-link" href="#predict()">&#182;</a></h3><p>A method on the estimator (classifier) that predicts labels for data supplied as an argument.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[62]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Predict the labels of the test data: y_pred</span>
<span class="n">y_pred</span> <span class="o">=</span> <span class="n">knn</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># Generate the confusion matrix and classification report</span>
<span class="nb">print</span><span class="p">(</span><span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="n">classification_report</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>[[176  30]
 [ 56  46]]
             precision    recall  f1-score   support

          0       0.76      0.85      0.80       206
          1       0.61      0.45      0.52       102

avg / total       0.71      0.72      0.71       308

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
<h2 id="Cross-Validation"><a href="http://scikit-learn.org/stable/modules/cross_validation.html#cross-validation">Cross-Validation</a><a class="anchor-link" href="#Cross-Validation">&#182;</a></h2><h3 id="cross_val_score()"><a href="http://scikit-learn.org/stable/modules/generated/sklearn.model_selection.cross_val_score.html"><strong>cross_val_score()</strong></a><a class="anchor-link" href="#cross_val_score()">&#182;</a></h3><p>A test set should still be held out for final evaluation, but the validation set is no longer needed when doing CV. In the basic approach, called k-fold CV, the training set is split into k smaller sets. The following procedure is followed for each of the k “folds”:</p>
<ul>
<li>A model is trained using k-1 of the folds as training data;  </li>
<li>the resulting model is validated on the remaining part of the data (i.e., it is used as a test set to compute a performance measure such as accuracy).<br>
The performance measure reported by k-fold cross-validation is then the average of the values computed in the loop. </li>
</ul>
<p>Example: $k$ = 5.  The test data and labels are split into 5 segments ('folds').  The model is trained on 4 folds and the remaining folds' worth of data is used as test data.  The data withheld in the fifth fold is evaluated using the trained model.  The predictions are then compared to the actual labels from the fifth fold.  This process is repeated 5 times.</p>
<p>We get $k\ R^2$-scores from which we can calculate mean, median and 95% confidence intervals.</p>
<p>Imported from <code>sklearn.model_selection</code></p>
<p>Call the <code>cross_val_score</code> helper function on the estimator and the data set:</p>
<p>Parameters:<br>
<strong>estimator</strong>: any estimator object implementing <code>fit</code><br>
<strong>X</strong>: array-like data to fit<br>
<strong>y</strong>: array-like the target variable to try to predict<br>
<strong>cv</strong>: int, the number of folds<br>
<strong>scoring</strong>: A string (see <a href="http://scikit-learn.org/stable/modules/model_evaluation.html">docs</a>) or a scorer callable object / function with signature scorer(estimator, X, y).</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[29]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">cross_val_score</span>

<span class="c1"># Instantiate the model</span>
<span class="n">reg</span> <span class="o">=</span> <span class="n">linear_model</span><span class="o">.</span><span class="n">LinearRegression</span><span class="p">()</span>

<span class="c1"># Perform 3-fold CV</span>
<span class="o">%</span><span class="k">timeit</span> cvscores_3 = cross_val_score(reg, X, y, cv=3)
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;3-fold average: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">cvscores_3</span><span class="p">)))</span>

<span class="c1"># Perform 5-fold CV</span>
<span class="o">%</span><span class="k">timeit</span> cvscores_5 = cross_val_score(reg, X, y, cv=5)
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;5-fold average: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">cvscores_5</span><span class="p">)))</span>

<span class="c1"># Perform 10-fold CV</span>
<span class="o">%</span><span class="k">timeit</span> cvscores_10 = cross_val_score(reg, X, y, cv=10)
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;10-fold average: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">cvscores_10</span><span class="p">)))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>2.1 ms ± 82.8 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
3-fold average: 0.6294715754653507
3.4 ms ± 82.4 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
5-fold average: 0.6168819644425119
6.65 ms ± 77.8 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
10-fold average: 0.5883937741571185
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
<h3 id="cross_val_predict()"><a href="http://scikit-learn.org/stable/modules/generated/sklearn.model_selection.cross_val_predict.html"><strong>cross_val_predict()</strong></a><a class="anchor-link" href="#cross_val_predict()">&#182;</a></h3><p><code>cross_val_score()</code> returns an array of the evaluation scores (the accuracy) measured for each fold.<br>
<code>cross_val_predict()</code> returns the predictions made on each test fold so you can pass it to <code>confusion_matrix()</code></p>
<p>The function <code>cross_val_predict</code> has a similar interface to <code>cross_val_score</code>, but returns, for each element in the input, the prediction that was obtained for that element when it was in the test set.  <a href="http://scikit-learn.org/stable/modules/generated/sklearn.model_selection.cross_val_predict.html">Docs</a></p>
<p>Just like the <code>cross_val_score()</code> function, <code>cross_val_predict()</code> performs $k$-fold cross-validation, but instead of returning the evaluation scores, it returns the predictions made on each test fold. This means that you get a clean prediction for each instance in the training set (“clean” meaning that the prediction is made by a model that never saw the data during training). Now you are ready to get the confusion matrix using the <code>confusion_matrix()</code> function. Just pass it the target classes (<code>y_train</code>) and the predicted classes (<code>y_train_pred</code>):</p>
<div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="kn">import</span> <span class="n">cross_val_predict</span>

<span class="n">cross_val_predict</span><span class="p">(</span><span class="n">estimator</span><span class="p">,</span> <span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="bp">None</span><span class="p">,</span> <span class="n">cv</span><span class="o">=</span><span class="bp">None</span><span class="p">,</span> <span class="n">method</span><span class="o">=</span><span class="err">’</span><span class="n">predict</span><span class="err">’</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[65]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">cross_val_predict</span>

<span class="n">y_train_pred</span> <span class="o">=</span> <span class="n">cross_val_predict</span><span class="p">(</span><span class="n">knn</span><span class="p">,</span> <span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">cv</span><span class="o">=</span><span class="mi">5</span><span class="p">)</span>

<span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_train</span><span class="p">,</span> <span class="n">y_train_pred</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[65]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>array([[254,  40],
       [106,  60]])</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Precision-&amp;-Recall">Precision &amp; Recall<a class="anchor-link" href="#Precision-&amp;-Recall">&#182;</a></h2><p>Increasing precision reduces recall and vice versa.</p>
<p>As <strong>precision increases</strong>, the classifier requires greater certainty, raising the bar for what it allows through.  Theoretically, this should remove more non-members of the class of interest, BUT, some actual members of the class of interest may fall out of the pool of items classified as hits, which may cause the precision ratio to drop, even as precision increases.</p>
<p>As <strong>recall increases</strong>, the classifier is lower the bar in an effort to include more members as hits.  As recall increases, the classifier will also include more non-members, lowering the precision ratio.</p>
<p>This is called the precision/recall tradeoff.<br>
<img src="Images/precision_recall_tradeoff.png" alt="prt"></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Precision-Recall-Curve">Precision-Recall Curve<a class="anchor-link" href="#Precision-Recall-Curve">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The precision-recall curve is generated by plotting the precision and recall for different thresholds. As a reminder, precision and recall are defined as:</p>
<p>Precision: Out of all of the items classified as belonging to the class of interest, what proportion actually belong to the class of interest?
$$Precision\ =\ \frac{TP}{TP+FP}$$</p>
<p>Recall:  Out of all of the items actually in the class of interest, what proportion were classified as belonging to the class of interest?
$$Recall\ =\ \frac{TP}{TP+FN}$$</p>
<p><img src="Images/prec_recall.png" alt="Precision"></p>
<p>True Statements:</p>
<ul>
<li><p>A recall of 1 corresponds to a classifier with a low threshold in which all females who contract diabetes were correctly classified as such, at the expense of many misclassifications of those who did not have diabetes.  Observe how when the recall is high, the precision drops.</p>
</li>
<li><p>In the case when there are no true positives or true negatives, precision is 0/0, which is undefined.</p>
</li>
<li><p>When the threshold is very close to 1, precision is also 1, because the classifier is absolutely certain about its predictions.  Notice how a high precision corresponds to a low recall: The classifier has a high threshold to ensure the positive predictions it makes are correct, which means it may miss some positive labels that have lower probabilities.</p>
</li>
<li><p>True negatives do not appear at all in the definitions of precision and recall.</p>
</li>
</ul>
<p><img src="Images/pr_curve.png" alt="PR Curve"></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Receiver-Operating-Characteristic-Curve-(ROC-Curve)">Receiver Operating Characteristic Curve (ROC Curve)<a class="anchor-link" href="#Receiver-Operating-Characteristic-Curve-(ROC-Curve)">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Area-Under-ROC-Curve-('AUC')">Area Under ROC Curve ('AUC')<a class="anchor-link" href="#Area-Under-ROC-Curve-('AUC')">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Hyperparameter-Tuning">Hyperparameter Tuning<a class="anchor-link" href="#Hyperparameter-Tuning">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="GridSearchCV">GridSearchCV<a class="anchor-link" href="#GridSearchCV">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="RandomizedSearchCV">RandomizedSearchCV<a class="anchor-link" href="#RandomizedSearchCV">&#182;</a></h3>
</div>
</div>
</div>
 

