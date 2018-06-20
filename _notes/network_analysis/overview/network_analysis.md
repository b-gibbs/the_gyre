---
title: Network Analysis
permalink: /notes/network_analysis/overview/
---

<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Network-Analysis">Network Analysis<a class="anchor-link" href="#Network-Analysis">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">networkx</span> <span class="k">as</span> <span class="nn">nx</span>
<span class="kn">import</span> <span class="nn">os</span>

<span class="n">base_url</span> <span class="o">=</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">expanduser</span><span class="p">(</span><span class="s1">&#39;~/Documents/Data Science/DataCamp/Slides/17 Network Analysis/data/&#39;</span><span class="p">)</span>

<span class="n">G_amrev</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">read_edgelist</span><span class="p">(</span><span class="n">base_url</span> <span class="o">+</span> <span class="s1">&#39;american-revolution.csv&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">G_github</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">read_edgelist</span><span class="p">(</span><span class="n">base_url</span> <span class="o">+</span> <span class="s1">&#39;github.p&#39;</span><span class="p">)</span>
<span class="n">G_uci</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">read_edgelist</span><span class="p">(</span><span class="n">base_url</span> <span class="o">+</span> <span class="s1">&#39;uci_forum.p&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Introduction">Introduction<a class="anchor-link" href="#Introduction">&#182;</a></h2><p>A network <strong>graph</strong> consists of <strong>nodes</strong> connected by <strong>edges</strong>.</p>
<ul>
<li>Nodes and edges may each contain metadata.</li>
<li><p>Networks model relationships between entities:</p>
<ul>
<li>social</li>
<li>transportation  </li>
</ul>
</li>
<li><p>Analyzing networks can provide insights into:</p>
<ul>
<li>important entities: influencers in a social network</li>
<li>pathfinding: most efficient path</li>
<li>clustering: finding communities</li>
</ul>
</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Types-of-Network-Graphs">Types of Network Graphs<a class="anchor-link" href="#Types-of-Network-Graphs">&#182;</a></h2><h3 id="Undirected-(Graph)">Undirected (Graph)<a class="anchor-link" href="#Undirected-(Graph)">&#182;</a></h3><ul>
<li>Facebook social graph</li>
<li>one bidirectional mapping between two entities</li>
</ul>
<h3 id="Directed-(DiGraph)">Directed (DiGraph)<a class="anchor-link" href="#Directed-(DiGraph)">&#182;</a></h3><ul>
<li>Twitter social graph</li>
<li>one unidirectional mapping between two entities</li>
</ul>
<h3 id="MultiGraph">MultiGraph<a class="anchor-link" href="#MultiGraph">&#182;</a></h3><ul>
<li>multiple bidirectional maps between two entities</li>
</ul>
<h3 id="MutliDiGraph">MutliDiGraph<a class="anchor-link" href="#MutliDiGraph">&#182;</a></h3><ul>
<li>trip records from one bike sharing station to another</li>
<li>multiple unidirectional edges between two entities</li>
</ul>
<h3 id="Self-loops">Self-loops<a class="anchor-link" href="#Self-loops">&#182;</a></h3><ul>
<li>nodes that connect back to themselves</li>
<li>a round-trip bike trip from a bike station back to the same bike station</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Network-Analysis-Basics">Network Analysis Basics<a class="anchor-link" href="#Network-Analysis-Basics">&#182;</a></h2><h3 id="import">import<a class="anchor-link" href="#import">&#182;</a></h3><div class="highlight"><pre><span></span><span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">networkx</span> <span class="kn">as</span> <span class="nn">nx</span>
<span class="kn">import</span> <span class="nn">nxviz</span> <span class="kn">as</span> <span class="nn">nv</span>
</pre></div>
<h3 id="instantiate">instantiate<a class="anchor-link" href="#instantiate">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># undirected graph</span>
<span class="n">G</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">Graph</span><span class="p">()</span>

<span class="c1"># directed graph</span>
<span class="n">D</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">DiGraph</span><span class="p">()</span>

<span class="c1"># Multi-edge graph</span>
<span class="n">M</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">MultiGraph</span><span class="p">()</span>

<span class="c1"># Multi-edge directed graph</span>
<span class="n">MD</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">MultDiiGraph</span><span class="p">()</span>

<span class="c1"># Barbell graph</span>
<span class="n">BB</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">barbell_graph</span><span class="p">(</span><span class="n">m1</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">m2</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>

<span class="c1"># Erdos Renyi Graph</span>
<span class="c1"># n = number of nodes in the graph</span>
<span class="c1"># p = probability of an edge between any two nodes</span>
<span class="n">G</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">erdos_renyi_graph</span><span class="p">(</span><span class="n">n</span><span class="o">=</span><span class="mi">20</span><span class="p">,</span> <span class="n">p</span><span class="o">=</span><span class="mf">0.2</span><span class="p">)</span>
</pre></div>
<h3 id="fetch-graph-info">fetch graph info<a class="anchor-link" href="#fetch-graph-info">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># returns a list of all nodes</span>
<span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">()</span>

<span class="c1"># returns node 1</span>
<span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span>

<span class="c1"># returns a tuple containing node 1 name + dict of metadata</span>
<span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)[</span><span class="mi">1</span><span class="p">]</span>

<span class="c1"># returns an int count of nodes</span>
<span class="nb">len</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">())</span>

<span class="c1"># returns metadata for all nodes</span>
<span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>

<span class="c1"># returns a list of all edges</span>
<span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">()</span>



<span class="c1"># returns an int count of edges</span>
<span class="nb">len</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">())</span>

<span class="c1"># returns the graph&#39;s type</span>
<span class="nb">type</span><span class="p">(</span><span class="n">MD</span><span class="p">)</span>
</pre></div>
<h3 id="adding-nodes">adding nodes<a class="anchor-link" href="#adding-nodes">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># add multiple nodes from a list </span>
<span class="n">G</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">([</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">])</span>

<span class="c1"># add dict to node 1&#39;s metadata</span>
<span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="mi">1</span><span class="p">][</span><span class="s1">&#39;label&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s1">&#39;blue&#39;</span>

<span class="c1"># add degree centrality score to each node&#39;s metadata dictionary</span>
<span class="n">dcs</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>
<span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">():</span>
    <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;centrality&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">dcs</span><span class="p">[</span><span class="n">n</span><span class="p">]</span>
</pre></div>
<h3 id="adding-edges">adding edges<a class="anchor-link" href="#adding-edges">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># add an edge between nodes 1 and 2</span>
<span class="n">G</span><span class="o">.</span><span class="n">add_edge</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span>

<span class="c1"># add multiple edges</span>
<span class="n">G</span><span class="o">.</span><span class="n">add_edges_from</span><span class="p">([(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">),</span> <span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">3</span><span class="p">)])</span>
</pre></div>
<h3 id="fetching">fetching<a class="anchor-link" href="#fetching">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># nodes</span>
<span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">()</span>

<span class="c1"># node 1</span>
<span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span>

<span class="c1"># edges</span>
<span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">()</span>

<span class="c1"># fetch metadata for all nodes</span>
<span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>

<span class="c1"># fetch metadata for all edges</span>
<span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
<span class="c1"># Returns a list of all nodes as tuple + dict -&gt; (1, 4, {&#39;date&#39; : datetime.date(2012, 11, 17)})</span>
</pre></div>
<h3 id="fetching-nodes-&amp;-edges-that-meet-criteria">fetching nodes &amp; edges that meet criteria<a class="anchor-link" href="#fetching-nodes-&amp;-edges-that-meet-criteria">&#182;</a></h3><div class="highlight"><pre><span></span><span class="n">noi</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">T</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;occupation&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;scientist&#39;</span><span class="p">]</span>

<span class="n">eoi</span> <span class="o">=</span> <span class="p">[(</span><span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">)</span> <span class="k">for</span> <span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">T</span><span class="o">.</span><span class="n">edges</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;date&#39;</span><span class="p">]</span> <span class="o">&lt;</span> <span class="n">date</span><span class="p">(</span><span class="mi">2010</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">)]</span>
</pre></div>
<h3 id="List-comprehension-syntax:">List comprehension syntax:<a class="anchor-link" href="#List-comprehension-syntax:">&#182;</a></h3><p>[ <i>output expression</i> <strong>for</strong> <i>iterator</i> <strong>in</strong> <i>iterable</i> <strong>if</strong> <i>predicate expression</i> ]<br>
<strong>OR</strong><br>
[ <i>output expression</i> <strong>for</strong> <i>iterator</i> <strong>in</strong> <i>iterable</i>]</p>
<h3 id="weighting-an-edge">weighting an edge<a class="anchor-link" href="#weighting-an-edge">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># identify the edge by naming the nodes, set &#39;2&#39; as the value for the &#39;weight&#39; key in the metadata dictionary for the edge</span>
<span class="n">T</span><span class="o">.</span><span class="n">edge</span><span class="p">[</span><span class="mi">1</span><span class="p">][</span><span class="mi">10</span><span class="p">][</span><span class="s1">&#39;weight&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="mi">2</span>
</pre></div>
<h3 id="iterating-edges-with-metadata">iterating edges with metadata<a class="anchor-link" href="#iterating-edges-with-metadata">&#182;</a></h3><div class="highlight"><pre><span></span><span class="k">for</span> <span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">T</span><span class="o">.</span><span class="n">edges</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">):</span>
</pre></div>
<p>where <code>(u, v)</code> are the nodes connected by the edge used to identify the edge and <code>d</code> is the edge's metadata dictionary.</p>
<h3 id="self-loops">self-loops<a class="anchor-link" href="#self-loops">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># get a count of all self-loops in a graph</span>
<span class="n">G</span><span class="o">.</span><span class="n">number_of_selfloops</span><span class="p">()</span>

<span class="c1"># Define find_selfloop_nodes()</span>
<span class="k">def</span> <span class="nf">find_selfloop_nodes</span><span class="p">(</span><span class="n">G</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Finds all nodes that have self-loops in the graph G.</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">nodes_in_selfloops</span> <span class="o">=</span> <span class="p">[]</span>

    <span class="c1"># Iterate over all the edges of G</span>
    <span class="k">for</span> <span class="n">u</span><span class="p">,</span> <span class="n">v</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">():</span>

    <span class="c1"># Check if node u and node v are the same</span>
        <span class="k">if</span> <span class="n">u</span> <span class="o">==</span> <span class="n">v</span><span class="p">:</span>

            <span class="c1"># Append node u to nodes_in_selfloops</span>
            <span class="n">nodes_in_selfloops</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">u</span><span class="p">)</span>

    <span class="k">return</span> <span class="n">nodes_in_selfloops</span>

<span class="c1"># Check whether number of self loops equals the number of nodes in self loops</span>
<span class="k">assert</span> <span class="n">T</span><span class="o">.</span><span class="n">number_of_selfloops</span><span class="p">()</span> <span class="o">==</span> <span class="nb">len</span><span class="p">(</span><span class="n">find_selfloop_nodes</span><span class="p">(</span><span class="n">T</span><span class="p">))</span>
</pre></div>
<h3 id="checking-for-the-existence-of-an-edge-between-two-nodes">checking for the existence of an edge between two nodes<a class="anchor-link" href="#checking-for-the-existence-of-an-edge-between-two-nodes">&#182;</a></h3><div class="highlight"><pre><span></span><span class="k">if</span> <span class="n">G</span><span class="o">.</span><span class="n">has_edge</span><span class="p">(</span><span class="n">n1</span><span class="p">,</span> <span class="n">n2</span><span class="p">):</span>
</pre></div>
<p>OR</p>
<div class="highlight"><pre><span></span><span class="k">if</span> <span class="ow">not</span> <span class="n">G</span><span class="o">.</span><span class="n">has_edge</span><span class="p">(</span><span class="n">n1</span><span class="p">,</span> <span class="n">n2</span><span class="p">):</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Visualizing-Networks">Visualizing Networks<a class="anchor-link" href="#Visualizing-Networks">&#182;</a></h2><h3 id="Basic">Basic<a class="anchor-link" href="#Basic">&#182;</a></h3><div class="highlight"><pre><span></span><span class="n">nx</span><span class="o">.</span><span class="n">draw</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Matrix-Plot">Matrix Plot<a class="anchor-link" href="#Matrix-Plot">&#182;</a></h3><ul>
<li>Undirected graphs are symmetrical since the edges are bidirectional, leads to a stripe along the diagonal from upper-left to lower-right</li>
<li>Directed graphs are most likely NOT symmetrical, since edges are unidirectional  </li>
<li>nodes are the rows and columns of the matrix, and cells are filled in according to whether an edge exists between the pairs of nodes</li>
</ul>
<div class="highlight"><pre><span></span><span class="c1"># Import nxviz</span>
<span class="kn">import</span> <span class="nn">nxviz</span> <span class="kn">as</span> <span class="nn">nv</span>

<span class="c1"># Create the MatrixPlot object: m</span>
<span class="n">m</span> <span class="o">=</span> <span class="n">nv</span><span class="o">.</span><span class="n">MatrixPlot</span><span class="p">(</span><span class="n">T</span><span class="p">)</span>

<span class="c1"># Draw m to the screen</span>
<span class="n">m</span><span class="o">.</span><span class="n">draw</span><span class="p">()</span>

<span class="c1"># Display the plot</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="c1"># Convert T to a matrix format: A</span>
<span class="n">A</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">to_numpy_matrix</span><span class="p">(</span><span class="n">T</span><span class="p">)</span>

<span class="c1"># Convert A back to the NetworkX form as a directed graph: T_conv</span>
<span class="n">T_conv</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">from_numpy_matrix</span><span class="p">(</span><span class="n">A</span><span class="p">,</span> <span class="n">create_using</span><span class="o">=</span><span class="n">nx</span><span class="o">.</span><span class="n">DiGraph</span><span class="p">())</span>

<span class="c1"># Check that the `category` metadata field is lost from each node</span>
<span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">T_conv</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">):</span>
    <span class="k">assert</span> <span class="s1">&#39;category&#39;</span> <span class="ow">not</span> <span class="ow">in</span> <span class="n">d</span><span class="o">.</span><span class="n">keys</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Arc-Plot">Arc Plot<a class="anchor-link" href="#Arc-Plot">&#182;</a></h3><ul>
<li>nodes are ordered along one axis</li>
<li>edges are drawn using circular arcs from one node to another</li>
<li>if plot is ordered by a criteria or grouped by a location, an arc plot makes it possible to see relationships between connectivity and the sorted or grouped property</li>
</ul>
<div class="highlight"><pre><span></span><span class="c1"># Import necessary modules</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="kn">from</span> <span class="nn">nxviz</span> <span class="kn">import</span> <span class="n">ArcPlot</span>

<span class="c1"># Create the un-customized ArcPlot object: a</span>
<span class="n">a</span> <span class="o">=</span> <span class="n">ArcPlot</span><span class="p">(</span><span class="n">T</span><span class="p">)</span>

<span class="c1"># Draw a to the screen</span>
<span class="n">a</span><span class="o">.</span><span class="n">draw</span><span class="p">()</span>

<span class="c1"># Display the plot</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="c1"># Create the customized ArcPlot object: a2</span>
<span class="n">a2</span> <span class="o">=</span> <span class="n">ArcPlot</span><span class="p">(</span><span class="n">T</span><span class="p">,</span> <span class="n">node_order</span><span class="o">=</span><span class="s1">&#39;category&#39;</span><span class="p">,</span> <span class="n">node_color</span><span class="o">=</span><span class="s1">&#39;category&#39;</span><span class="p">)</span>

<span class="c1"># Draw a2 to the screen</span>
<span class="n">a2</span><span class="o">.</span><span class="n">draw</span><span class="p">()</span>

<span class="c1"># Display the plot</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Circos-Plot">Circos Plot<a class="anchor-link" href="#Circos-Plot">&#182;</a></h3><ul>
<li>transformation of the arc plot such that the two ends of the arc plot are joined together in a circle</li>
<li>aesthetic and compact version of the arc plot</li>
</ul>
<div class="highlight"><pre><span></span><span class="c1"># import</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="kn">from</span> <span class="nn">nxviz</span> <span class="kn">import</span> <span class="n">CircosPlot</span>

<span class="c1"># instantiate</span>
<span class="n">c</span> <span class="o">=</span> <span class="n">CircosPlot</span><span class="p">(</span><span class="n">T</span><span class="p">)</span>

<span class="c1"># draw c to the screen</span>
<span class="n">c</span><span class="o">.</span><span class="n">draw</span><span class="p">()</span>

<span class="c1"># display the plot</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Measuring-a-Node's-Importance">Measuring a Node's Importance<a class="anchor-link" href="#Measuring-a-Node's-Importance">&#182;</a></h2><p>There are two ways to measure a node's importance in a network:</p>
<ol>
<li>degree centrality - how many neighbors does a node have?</li>
<li>betweenness centrality - how many shortest paths pass through the node?</li>
</ol>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Degree-Centrality">Degree Centrality<a class="anchor-link" href="#Degree-Centrality">&#182;</a></h2><p><strong>neighbor node</strong>: connected node<br>
<strong>degree</strong>: the number of neighbors the node has<br>
<strong>degree centrality</strong>:  the number of neighbors the node has / count of all nodes in graph (-1 if self-loops aren't allowed)</p>
<h3 id="fetch-a-list-of-a-node's-neighbors">fetch a list of a node's neighbors<a class="anchor-link" href="#fetch-a-list-of-a-node's-neighbors">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># fetch a list of node 1&#39;s neighbors</span>
<span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
</pre></div>
<h3 id="get-degree-centrality-for-each-node-in-a-graph">get degree centrality for each node in a graph<a class="anchor-link" href="#get-degree-centrality-for-each-node-in-a-graph">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># print a dictionary with each node as a key and its degree centrality rating as its value</span>
<span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>
</pre></div>
<h3 id="fetch-nodes-with-$n$-neighbors">fetch nodes with $n$ neighbors<a class="anchor-link" href="#fetch-nodes-with-$n$-neighbors">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Define nodes_with_m_nbrs()</span>
<span class="k">def</span> <span class="nf">nodes_with_m_nbrs</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">m</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Returns all nodes in graph G that have m neighbors.</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">nodes</span> <span class="o">=</span> <span class="nb">set</span><span class="p">()</span>

    <span class="c1"># Iterate over all nodes in G</span>
    <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">():</span>

        <span class="c1"># Check if the number of neighbors of n matches m</span>
        <span class="k">if</span> <span class="nb">len</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">n</span><span class="p">))</span> <span class="o">==</span> <span class="n">m</span><span class="p">:</span>

            <span class="c1"># Add the node n to the set</span>
            <span class="n">nodes</span><span class="o">.</span><span class="n">add</span><span class="p">(</span><span class="n">n</span><span class="p">)</span>

    <span class="c1"># Return the nodes with m neighbors</span>
    <span class="k">return</span> <span class="n">nodes</span>

<span class="c1"># Compute and print all nodes in T that have 6 neighbors</span>
<span class="n">six_nbrs</span> <span class="o">=</span> <span class="n">nodes_with_m_nbrs</span><span class="p">(</span><span class="n">T</span><span class="p">,</span> <span class="mi">6</span><span class="p">)</span>
<span class="k">print</span><span class="p">(</span><span class="n">six_nbrs</span><span class="p">)</span>
</pre></div>
<h3 id="compute-degree-&amp;-plot-hist-of-network">compute degree &amp; plot hist of network<a class="anchor-link" href="#compute-degree-&amp;-plot-hist-of-network">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Compute the degree of every node: degrees</span>
<span class="n">degrees</span> <span class="o">=</span> <span class="p">[</span><span class="nb">len</span><span class="p">(</span><span class="n">T</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">n</span><span class="p">))</span> <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">T</span><span class="o">.</span><span class="n">nodes</span><span class="p">()]</span>  

<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">degrees</span><span class="p">)</span>
</pre></div>
<h3 id="compute-degree_centrality-&amp;-plot-hist-of-network">compute degree_centrality &amp; plot hist of network<a class="anchor-link" href="#compute-degree_centrality-&amp;-plot-hist-of-network">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Compute the degree centrality of a network</span>
<span class="n">deg_cent</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>  

<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">deg_cent</span><span class="o">.</span><span class="n">values</span><span class="p">()))</span>
</pre></div>
<h3 id="plot-scatter-of-degree-vs.-degree_centrality">plot scatter of degree vs. degree_centrality<a class="anchor-link" href="#plot-scatter-of-degree-vs.-degree_centrality">&#182;</a></h3><div class="highlight"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">degrees</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="nb">list</span><span class="p">(</span><span class="n">deg_cent</span><span class="o">.</span><span class="n">values</span><span class="p">()))</span>
</pre></div>
<h3 id="find-nodes-with-highest-degree-centrality">find nodes with highest degree centrality<a class="anchor-link" href="#find-nodes-with-highest-degree-centrality">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Define find_nodes_with_highest_deg_cent()</span>
<span class="k">def</span> <span class="nf">find_nodes_with_highest_deg_cent</span><span class="p">(</span><span class="n">G</span><span class="p">):</span>

    <span class="c1"># Compute the degree centrality of G: deg_cent</span>
    <span class="n">deg_cent</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>

    <span class="c1"># Compute the maximum degree centrality: max_dc</span>
    <span class="n">max_dc</span> <span class="o">=</span> <span class="nb">max</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">deg_cent</span><span class="o">.</span><span class="n">values</span><span class="p">()))</span>

    <span class="n">nodes</span> <span class="o">=</span> <span class="nb">set</span><span class="p">()</span>

    <span class="c1"># Iterate over the degree centrality dictionary</span>
    <span class="k">for</span> <span class="n">k</span><span class="p">,</span> <span class="n">v</span> <span class="ow">in</span> <span class="n">deg_cent</span><span class="o">.</span><span class="n">items</span><span class="p">():</span>

        <span class="c1"># Check if the current value has the maximum degree centrality</span>
        <span class="k">if</span> <span class="n">v</span> <span class="o">==</span> <span class="n">max_dc</span><span class="p">:</span>

            <span class="c1"># Add the current node to the set of nodes</span>
            <span class="n">nodes</span><span class="o">.</span><span class="n">add</span><span class="p">(</span><span class="n">k</span><span class="p">)</span>

    <span class="k">return</span> <span class="n">nodes</span>

<span class="c1"># Find the node(s) that has the highest degree centrality in T: top_dc</span>
<span class="n">top_dc</span> <span class="o">=</span> <span class="n">find_nodes_with_highest_deg_cent</span><span class="p">(</span><span class="n">T</span><span class="p">)</span>
<span class="k">print</span><span class="p">(</span><span class="n">top_dc</span><span class="p">)</span>

<span class="c1"># Write the assertion statement</span>
<span class="k">for</span> <span class="n">node</span> <span class="ow">in</span> <span class="n">top_dc</span><span class="p">:</span>
    <span class="k">assert</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">T</span><span class="p">)[</span><span class="n">node</span><span class="p">]</span> <span class="o">==</span> <span class="nb">max</span><span class="p">(</span><span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">T</span><span class="p">)</span><span class="o">.</span><span class="n">values</span><span class="p">())</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Betweenness-Centrality">Betweenness Centrality<a class="anchor-link" href="#Betweenness-Centrality">&#182;</a></h2><p><strong>all shortest paths</strong>: set of paths such that each path is the shortest path between a given pair of nodes</p>
<p><strong>betweenness centrality</strong>:  number of <strong>shortest paths</strong> that pass through the node / all possible shortest paths</p>
<ul>
<li>captures bottleneck nodes in a graph</li>
<li>identifies bridges between two networks (information transfer links)</li>
</ul>
<h3 id="fetch-betweenness-centrality-ratios">fetch betweenness centrality ratios<a class="anchor-link" href="#fetch-betweenness-centrality-ratios">&#182;</a></h3><div class="highlight"><pre><span></span><span class="n">nx</span><span class="o">.</span><span class="n">betweenness_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>
</pre></div>
<h3 id="find-nodes-with-highest-betweenness-centrality">find nodes with highest betweenness centrality<a class="anchor-link" href="#find-nodes-with-highest-betweenness-centrality">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Define find_node_with_highest_bet_cent()</span>
<span class="k">def</span> <span class="nf">find_node_with_highest_bet_cent</span><span class="p">(</span><span class="n">G</span><span class="p">):</span>

    <span class="c1"># Compute betweenness centrality: bet_cent</span>
    <span class="n">bet_cent</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">betweenness_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>

    <span class="c1"># Compute maximum betweenness centrality: max_bc</span>
    <span class="n">max_bc</span> <span class="o">=</span> <span class="nb">max</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">bet_cent</span><span class="o">.</span><span class="n">values</span><span class="p">()))</span>

    <span class="n">nodes</span> <span class="o">=</span> <span class="nb">set</span><span class="p">()</span>

    <span class="c1"># Iterate over the betweenness centrality dictionary</span>
    <span class="k">for</span> <span class="n">k</span><span class="p">,</span> <span class="n">v</span> <span class="ow">in</span> <span class="n">bet_cent</span><span class="o">.</span><span class="n">items</span><span class="p">():</span>

        <span class="c1"># Check if the current value has the maximum betweenness centrality</span>
        <span class="k">if</span> <span class="n">v</span> <span class="o">==</span> <span class="n">max_bc</span><span class="p">:</span>

            <span class="c1"># Add the current node to the set of nodes</span>
            <span class="n">nodes</span><span class="o">.</span><span class="n">add</span><span class="p">(</span><span class="n">k</span><span class="p">)</span>

    <span class="k">return</span> <span class="n">nodes</span>

<span class="c1"># Use that function to find the node(s) that has the highest betweenness centrality in the network: top_bc</span>
<span class="n">top_bc</span> <span class="o">=</span> <span class="n">find_node_with_highest_bet_cent</span><span class="p">(</span><span class="n">T</span><span class="p">)</span>

<span class="c1"># Write an assertion statement that checks that the node(s) is/are correctly identified.</span>
<span class="k">for</span> <span class="n">node</span> <span class="ow">in</span> <span class="n">top_bc</span><span class="p">:</span>
    <span class="k">assert</span> <span class="n">nx</span><span class="o">.</span><span class="n">betweenness_centrality</span><span class="p">(</span><span class="n">T</span><span class="p">)[</span><span class="n">node</span><span class="p">]</span> <span class="o">==</span> <span class="nb">max</span><span class="p">(</span><span class="n">nx</span><span class="o">.</span><span class="n">betweenness_centrality</span><span class="p">(</span><span class="n">T</span><span class="p">)</span><span class="o">.</span><span class="n">values</span><span class="p">())</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Path-Finding">Path Finding<a class="anchor-link" href="#Path-Finding">&#182;</a></h2><h3 id="Uses:">Uses:<a class="anchor-link" href="#Uses:">&#182;</a></h3><ul>
<li>optimization - finding the shortest transport path</li>
<li>modeling - spread of disease or information</li>
<li>also useful in determining a node's importance in a network  </li>
</ul>
<h3 id="Breadth-first-search-algorithm-(BFS)">Breadth-first search algorithm (BFS)<a class="anchor-link" href="#Breadth-first-search-algorithm-(BFS)">&#182;</a></h3><p>Find the shortest path between start node and dest node by iterating through neighbors.</p>
<div class="highlight"><pre><span></span><span class="k">def</span> <span class="nf">path_exists</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">node1</span><span class="p">,</span> <span class="n">node2</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    This function checks whether a path exists between two nodes (node1, node2) in graph G.</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">visited_nodes</span> <span class="o">=</span> <span class="nb">set</span><span class="p">()</span>
    <span class="n">queue</span> <span class="o">=</span> <span class="p">[</span><span class="n">node1</span><span class="p">]</span>

    <span class="k">for</span> <span class="n">node</span> <span class="ow">in</span> <span class="n">queue</span><span class="p">:</span>  
        <span class="n">neighbors</span> <span class="o">=</span> <span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">node</span><span class="p">)</span>
        <span class="k">if</span> <span class="n">node2</span> <span class="ow">in</span> <span class="n">neighbors</span><span class="p">:</span>
            <span class="k">print</span><span class="p">(</span><span class="s1">&#39;Path exists between nodes {0} and {1}&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">node1</span><span class="p">,</span> <span class="n">node2</span><span class="p">))</span>
            <span class="k">return</span> <span class="bp">True</span>
            <span class="k">break</span>

        <span class="k">else</span><span class="p">:</span>
            <span class="n">visited_nodes</span><span class="o">.</span><span class="n">add</span><span class="p">(</span><span class="n">node</span><span class="p">)</span>
            <span class="n">queue</span><span class="o">.</span><span class="n">extend</span><span class="p">([</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">neighbors</span> <span class="k">if</span> <span class="n">n</span> <span class="ow">not</span> <span class="ow">in</span> <span class="n">visited_nodes</span><span class="p">])</span>

        <span class="c1"># Check to see if the final element of the queue has been reached</span>
        <span class="k">if</span> <span class="n">node</span> <span class="o">==</span> <span class="n">queue</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">]:</span>
            <span class="k">print</span><span class="p">(</span><span class="s1">&#39;Path does not exist between nodes {0} and {1}&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">node1</span><span class="p">,</span> <span class="n">node2</span><span class="p">))</span>

            <span class="c1"># Place the appropriate return statement</span>
            <span class="k">return</span> <span class="bp">False</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Cliques">Cliques<a class="anchor-link" href="#Cliques">&#182;</a></h2><p><strong>Clique</strong>: all nodes are directly joined.
<strong>Triangle</strong>: smallest possible clique.</p>
<ul>
<li>example: friend recommendation systems</li>
</ul>
<h3 id="Count-the-number-of-triangles-each-node-in-a-graph-in-involved-in">Count the number of triangles each node in a graph in involved in<a class="anchor-link" href="#Count-the-number-of-triangles-each-node-in-a-graph-in-involved-in">&#182;</a></h3><div class="highlight"><pre><span></span><span class="n">nx</span><span class="o">.</span><span class="n">triangles</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>
</pre></div>
<h3 id="itertools.combinations-to-check-combinations-of-nodes">itertools.combinations to check combinations of nodes<a class="anchor-link" href="#itertools.combinations-to-check-combinations-of-nodes">&#182;</a></h3><p>-iterates over every pair in the network (G.nodes(), 2) - the 2 tells it to look at pairs</p>
<div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">itertools</span> <span class="kn">import</span> <span class="n">combinations</span>

<span class="k">for</span> <span class="n">n1</span><span class="p">,</span> <span class="n">n2</span> <span class="ow">in</span> <span class="n">combinations</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(),</span> <span class="mi">2</span><span class="p">):</span>
    <span class="k">print</span><span class="p">(</span><span class="n">n1</span><span class="p">,</span> <span class="n">n2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="check-to-see-whether-given-node-is-a-member-of-a-triangle">check to see whether given node is a member of a triangle<a class="anchor-link" href="#check-to-see-whether-given-node-is-a-member-of-a-triangle">&#182;</a></h3><div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">itertools</span> <span class="kn">import</span> <span class="n">combinations</span>

<span class="c1"># Define is_in_triangle() </span>
<span class="k">def</span> <span class="nf">is_in_triangle</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">n</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Checks whether a node `n` in graph `G` is in a triangle relationship or not. </span>

<span class="sd">    Returns a boolean.</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">in_triangle</span> <span class="o">=</span> <span class="bp">False</span>

    <span class="c1"># Iterate over all possible triangle relationship combinations</span>
    <span class="k">for</span> <span class="n">n1</span><span class="p">,</span> <span class="n">n2</span> <span class="ow">in</span> <span class="n">combinations</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">n</span><span class="p">),</span> <span class="mi">2</span><span class="p">):</span>

        <span class="c1"># Check if an edge exists between n1 and n2</span>
        <span class="k">if</span> <span class="n">G</span><span class="o">.</span><span class="n">has_edge</span><span class="p">(</span><span class="n">n1</span><span class="p">,</span> <span class="n">n2</span><span class="p">):</span>
            <span class="n">in_triangle</span> <span class="o">=</span> <span class="bp">True</span>
            <span class="k">break</span>
    <span class="k">return</span> <span class="n">in_triangle</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Find-all-nodes-in-a-triangle-relationship-with-a-given-node">Find all nodes in a triangle relationship with a given node<a class="anchor-link" href="#Find-all-nodes-in-a-triangle-relationship-with-a-given-node">&#182;</a></h3><div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">itertools</span> <span class="kn">import</span> <span class="n">combinations</span>

<span class="c1"># Write a function that identifies all nodes in a triangle relationship with a given node.</span>
<span class="k">def</span> <span class="nf">nodes_in_triangle</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">n</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Returns the nodes in a graph `G` that are involved in a triangle relationship with the node `n`.</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">triangle_nodes</span> <span class="o">=</span> <span class="nb">set</span><span class="p">([</span><span class="n">n</span><span class="p">])</span>

    <span class="c1"># Iterate over all possible triangle relationship combinations</span>
    <span class="k">for</span> <span class="n">n1</span><span class="p">,</span> <span class="n">n2</span> <span class="ow">in</span> <span class="n">combinations</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">n</span><span class="p">),</span> <span class="mi">2</span><span class="p">):</span>

        <span class="c1"># Check if n1 and n2 have an edge between them</span>
        <span class="k">if</span> <span class="n">G</span><span class="o">.</span><span class="n">has_edge</span><span class="p">(</span><span class="n">n1</span><span class="p">,</span> <span class="n">n2</span><span class="p">):</span>

            <span class="c1"># Add n1 to triangle_nodes</span>
            <span class="n">triangle_nodes</span><span class="o">.</span><span class="n">add</span><span class="p">(</span><span class="n">n1</span><span class="p">)</span>

            <span class="c1"># Add n2 to triangle_nodes</span>
            <span class="n">triangle_nodes</span><span class="o">.</span><span class="n">add</span><span class="p">(</span><span class="n">n2</span><span class="p">)</span>

    <span class="k">return</span> <span class="n">triangle_nodes</span>

<span class="c1"># Write the assertion statement</span>
<span class="k">assert</span> <span class="nb">len</span><span class="p">(</span><span class="n">nodes_in_triangle</span><span class="p">(</span><span class="n">T</span><span class="p">,</span> <span class="mi">1</span><span class="p">))</span> <span class="o">==</span> <span class="mi">35</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Find-all-open-triangles-in-a-graph">Find all open triangles in a graph<a class="anchor-link" href="#Find-all-open-triangles-in-a-graph">&#182;</a></h3><p>Think of a LinkedIn network recommender system - if A knows B &amp; C, it's probable that B &amp; C also know one another</p>
<div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">itertools</span> <span class="kn">import</span> <span class="n">combinations</span>

<span class="c1"># Define node_in_open_triangle()</span>
<span class="k">def</span> <span class="nf">node_in_open_triangle</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">n</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Checks whether pairs of neighbors of node `n` in graph `G` are in an &#39;open triangle&#39; relationship with node `n`.</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">in_open_triangle</span> <span class="o">=</span> <span class="bp">False</span>

    <span class="c1"># Iterate over all possible triangle relationship combinations</span>
    <span class="k">for</span> <span class="n">n1</span><span class="p">,</span> <span class="n">n2</span> <span class="ow">in</span> <span class="n">combinations</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">n</span><span class="p">),</span> <span class="mi">2</span><span class="p">):</span>

        <span class="c1"># Check if n1 and n2 do NOT have an edge between them</span>
        <span class="k">if</span> <span class="ow">not</span> <span class="n">G</span><span class="o">.</span><span class="n">has_edge</span><span class="p">(</span><span class="n">n1</span><span class="p">,</span> <span class="n">n2</span><span class="p">):</span>

            <span class="n">in_open_triangle</span> <span class="o">=</span> <span class="bp">True</span>

            <span class="k">break</span>

    <span class="k">return</span> <span class="n">in_open_triangle</span>

<span class="c1"># Compute the number of open triangles in T</span>
<span class="n">num_open_triangles</span> <span class="o">=</span> <span class="mi">0</span>

<span class="c1"># Iterate over all the nodes in T</span>
<span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">T</span><span class="o">.</span><span class="n">nodes</span><span class="p">():</span>

    <span class="c1"># Check if the current node is in an open triangle</span>
    <span class="k">if</span> <span class="n">node_in_open_triangle</span><span class="p">(</span><span class="n">T</span><span class="p">,</span> <span class="n">n</span><span class="p">):</span>

        <span class="c1"># Increment num_open_triangles</span>
        <span class="n">num_open_triangles</span> <span class="o">+=</span> <span class="mi">1</span>

<span class="k">print</span><span class="p">(</span><span class="n">num_open_triangles</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>Maximal Clique</strong>: a clique that cannot be extended by adding an adjacent edge.  Useful when trying to find communities.</p>
<p><img src="images/maximal_clique.png" width="200px"/></p>
<p><strong>Community</strong>:</p>
<p><code>find_cliques</code>: will find only maximal cliques</p>
<p>Given the barbell graph below, <code>find_cliques</code> will find 4 maximal cliques -- remember that edges are also cliques</p>
<p><img src="images/Barbell_Graph.png" width="600px"/></p>
<p><img src="images/find_cliques.png" width="800px"/></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="find-all-maximal-cliques-of-size-=-n">find all maximal cliques of size = n<a class="anchor-link" href="#find-all-maximal-cliques-of-size-=-n">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Define maximal_cliques()</span>
<span class="k">def</span> <span class="nf">maximal_cliques</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">size</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Finds all maximal cliques in graph `G` that are of size `size`.</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">mcs</span> <span class="o">=</span> <span class="p">[]</span>
    <span class="k">for</span> <span class="n">clique</span> <span class="ow">in</span> <span class="n">nx</span><span class="o">.</span><span class="n">find_cliques</span><span class="p">(</span><span class="n">G</span><span class="p">):</span>
        <span class="k">if</span> <span class="nb">len</span><span class="p">(</span><span class="n">clique</span><span class="p">)</span> <span class="o">==</span> <span class="n">size</span><span class="p">:</span>
            <span class="n">mcs</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">clique</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">mcs</span>

<span class="c1"># Check that there are 33 maximal cliques of size 3 in the graph T</span>
<span class="k">assert</span> <span class="nb">len</span><span class="p">(</span><span class="n">maximal_cliques</span><span class="p">(</span><span class="n">T</span><span class="p">,</span> <span class="mi">3</span><span class="p">))</span> <span class="o">==</span> <span class="mi">33</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Subgraphs">Subgraphs<a class="anchor-link" href="#Subgraphs">&#182;</a></h2><p>Subgraphs allow you to view portions of a large graph for:</p>
<ul>
<li>paths</li>
<li>communities / cliques</li>
<li>degrees of separation from a node</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">networkx</span> <span class="k">as</span> <span class="nn">nx</span>
<span class="kn">import</span> <span class="nn">nxviz</span> <span class="k">as</span> <span class="nn">nv</span>

<span class="n">G</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">erdos_renyi_graph</span><span class="p">(</span><span class="n">n</span><span class="o">=</span><span class="mi">20</span><span class="p">,</span> <span class="n">p</span><span class="o">=</span><span class="mf">0.2</span><span class="p">)</span>
<span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">()</span>
<span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">()</span>
<span class="n">nodes</span> <span class="o">=</span> <span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="mi">8</span><span class="p">)</span>
<span class="n">nodes</span>
<span class="n">g_eight</span> <span class="o">=</span> <span class="n">G</span><span class="o">.</span><span class="n">subgraph</span><span class="p">(</span><span class="n">nodes</span><span class="p">)</span>
<span class="n">g_eight</span><span class="o">.</span><span class="n">edges</span><span class="p">()</span>

<span class="n">G</span>
<span class="n">g_eight</span>

<span class="n">nx</span><span class="o">.</span><span class="n">draw</span><span class="p">(</span><span class="n">g_eight</span><span class="p">,</span> <span class="n">with_labels</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[11]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>NodeView((0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19))</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[11]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>EdgeView([(0, 1), (0, 3), (0, 7), (0, 8), (0, 14), (1, 2), (2, 3), (2, 12), (2, 16), (3, 4), (3, 8), (3, 13), (3, 18), (4, 18), (5, 13), (6, 12), (6, 13), (7, 9), (7, 10), (7, 12), (7, 14), (8, 19), (9, 15), (10, 13), (10, 18), (11, 12), (11, 13), (11, 17), (11, 18), (12, 13), (13, 18), (15, 16), (16, 17)])</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[11]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&lt;dict_keyiterator at 0x1a1e40a188&gt;</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[11]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>EdgeView([(0, 3)])</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[11]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&lt;networkx.classes.graph.Graph at 0x1a1e40bb38&gt;</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[11]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&lt;networkx.classes.graphviews.SubGraph at 0x1a1e40bd30&gt;</pre>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAeEAAAFCCAYAAADGwmVOAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4yLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvhp/UCwAADDNJREFUeJzt3V+IXulBx/HfO5OQzDQlGyWLqBAXa290I2ICRUQC3rhRhKxiLXixW6wQha4XqRAprBUhXuRO7YJUCCgKli3rhVm2/k0v9GJyockKYu3NIr2YQJdUNzNpknm9OJnuZHYm/3Zmfu/M+/nAQOY95z08JJDvOc95zvuOxuPxOADAjptpDwAAppUIA0CJCANAiQgDQIkIA0CJCANAiQgDQIkIA0CJCANAiQgDQIkIA0CJCANAiQgDQIkIA0CJCANAiQgDQIkIA0CJCANAyb72AOCJLS4mly4l164lN28mhw8nx48nL7+cHD3aHh3AYxuNx+NxexDwWBYWkgsXkjffHH5fXn5/29xcMh4nL7yQnD+fnDzZGSPAExBhdofXXkvOnUuWlobYbmY0GoJ88WJy9uzOjQ/gKZiOZvKtBvjWrUfvOx4P+507N/wuxMAEszCLybawkD9+5ZWcuHUrB5K8tG7zl5J8LMmhJD+X5JurG1ZDfPXqjg0V4EmJMJPtwoV8/507+XyST6/bdCXJ7yb5myTfSvJckk+t3WFpabiHDDCh3BNmci0uJseOfXcB1ueT/E+SS/c3n0uylORP7v/+zSQ/kOS/k/zw6jEOHkzeeceqaWAiuRJmcl269NDN4/s/a39PkrfX7jQaPfI4AC0izOS6du3Bx5DWOZ3kr5Ncy3BF/PtJRkkeWL61tJRcv76NgwR4eiLM5Lp586GbfzbJF5L8UpJjSX4oyUeT/OD6Hd99d+vHBrAFRJjJdfjwI3f5rSRfT7KYIcZ3k/zY+p2OHNnqkQFsCRFmch0/nhw8mLtJlpPcu/+znHz3tbcz3At+J8lvJHklyQPJnZtLnn9+J0cN8NisjmZy3V8d/XvLy/nCuk2vJvntJD+T5BsZpqFfTvIHSWbX7mh1NDDBRJjJ9uKLyRtvPPyjKjczGiVnziSvv7714wLYAiLMZFtYSE6deryPrFxvfj65ciU5cWLLhwWwFdwTZrKdPDl8GcP8/JO9b35+eJ8AAxPMFzgw+Va/hMG3KAF7jOlodo+rV4fPgr58eYjt0tL721a/T/j06eH7hF0BA7uACLP73LgxfBTl9evDB3EcOTI8hvTSS1ZBA7uKCANAiYVZAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAUCLCAFAiwgBQIsIAULKvPYCJsLiYXLqUXLuW3LyZHD6cHD+evPxycvRoe3QA7FGj8Xg8bg+iZmEhuXAhefPN4ffl5fe3zc0l43HywgvJ+fPJyZOdMQKwZ01vhF97LTl3LllaGmK7mdFoCPLFi8nZszs3PgD2vOmcjl4N8K1bj953PB72O3du+F2IAdgi03clvLCQnDr1eAFeb34+uXIlOXFiy4cFwPSZvtXRFy4MU9DrfCvJmSQfSXIsyV9u9N6lpeH9ALAFputKeHExOXbswQVY930qyUqSP0vyb0l+Psm/JPnR9TsePJi8845V0wB8aNN1T/jSpQ1ffi/J60neTnIoyU8n+cUkf57kD9fvPBoNx/nc57ZrlAB8GLvosdPpivC1axteBf9XktkkH1/z2o8nubLRMZaWkuvXt2V4AHwID3vs9CtfSV59deIeO52uCN+8ueHL/5fk8LrXDif5300O83df/nI+87WvZf/+/dm3b1/27du36Z8ftu1p9tuuY8/OzmY0Gm3hXzbADnrUY6era4HeeCN5662Jeex0uiJ8eH1qB4eSfHvda99O8tFNDvNTp0/nny5ezN27d3P37t3cuXNnwz8/bNvD3nP79u28995723Lszbbdu3fvgWhPwsnDdp7MzMxM35pE2LN28WOn0xXh48eT11//wJT0x5PcTfL1JD9y/7V/zwaLspJkbi4f+cQn8txzz23nSHfcyspK7t2799Sx/zAnBbdv397RE447d+5kZmZmok44tvPYZjnY0xYWNgzwryX5hwxrfr4vye8k+fW1O6yG+OTJ6mOnVkff96tJRkm+lGF19OlYHb1XjcfjrKysVE44GsdeWVmZqJOC7T62WY4p8+KLwxTzupT9R5KPJTmQ5D+TnEryt0l+cu1Oo1Fy5sxwcVYyXVfCzz473JTf4B/si0k+neTZJN+b5LVsEODRKDl9WoB3udFolNnZ2czOzubAgQPt4Wy7zWY5duKkYHl5ecdPZtbOckzCScF2HnvqZzkWF4dFWBtcS679/3t0/+cbWRfh8Ti5fDm5caP2//p0RTgZVsW99dYHpi6+J8kbj3rv3NzwfthFZmZmMjMzk/3792dubq49nG212SzHXj3hWDvLsVtOHj7MeD5wwrHJY6erfjPJpSRLSX4iwwznB5QfO52+CJ88OayKe9yb+Kvm54f3+chKmFjTOsvRuD2ytLS0oycca2c5VgP9p0tL+ZXvfGfTv58vJvmjJP+a5J8zTE1/QPmx0+mLcPL+ajjfogTsYmtnOfa61VmOtVGe++Qnk69+9aHvm83wAUx/keE242c32undd7d8vI9relcwnD07fBnDmTPDYqv103Rzc8PrZ84M+wkwQM3qLMfBgwdz6NChPPPMMznwBPdx72a4J7yhI0e2YohPZTqvhFedODGsirtxY7gncP36cEZ05Ejy/PPJSy9ZhAUwqTZ57HQxyT8m+YUkc0n+PslfZZMv5pmbG/6/L5muR5QA2Ds2eez0RpJfzvB5DysZvhnvs0k+s9Exyo+dTveVMAC71yaPnR7NJp/9v94EPHbqShiA3WthITl16smedlk1Pz+s+Sk+9TK9C7MA2P1WHzudn3+y903IY6emowHY3XbxY6emowHYG65eHb5P+PLlIbarX1+YDOEdj4d7wOfP16+AV4kwAHvLLnrsVIQBoMTCLAAoEWEAKBFhACgRYQAoEWEAKBFhACgRYQAoEWEAKBFhACgRYQAoEWEAKBFhACgRYQAoEWEAKBFhACgRYQAoEWEAKBFhACgRYQAoEWEAKBFhACgRYQAoEWEAKBFhACgRYQAoEWEAKBFhACgRYQAoEWEAKBFhACgRYQAo+X9mhle0cOjPeAAAAABJRU5ErkJggg==
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
<h3 id="Draw-a-subgraph-given-a-list-of-nodes">Draw a subgraph given a list of nodes<a class="anchor-link" href="#Draw-a-subgraph-given-a-list-of-nodes">&#182;</a></h3><div class="highlight"><pre><span></span><span class="n">nodes_of_interest</span> <span class="o">=</span> <span class="p">[</span><span class="mi">29</span><span class="p">,</span> <span class="mi">38</span><span class="p">,</span> <span class="mi">42</span><span class="p">]</span>

<span class="c1"># Define get_nodes_and_nbrs()</span>
<span class="k">def</span> <span class="nf">get_nodes_and_nbrs</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">nodes_of_interest</span><span class="p">):</span>
    <span class="sd">&quot;&quot;&quot;</span>
<span class="sd">    Returns a subgraph of the graph `G` with only the `nodes_of_interest` and their neighbors.</span>
<span class="sd">    &quot;&quot;&quot;</span>
    <span class="n">nodes_to_draw</span> <span class="o">=</span> <span class="p">[]</span>

    <span class="c1"># Iterate over the nodes of interest</span>
    <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">nodes_of_interest</span><span class="p">:</span>

        <span class="c1"># Append the nodes of interest to nodes_to_draw</span>
        <span class="n">nodes_to_draw</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">n</span><span class="p">)</span>

        <span class="c1"># Iterate over all the neighbors of node n</span>
        <span class="k">for</span> <span class="n">nbr</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">n</span><span class="p">):</span>

            <span class="c1"># Append the neighbors of n to nodes_to_draw</span>
            <span class="n">nodes_to_draw</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">nbr</span><span class="p">)</span>

    <span class="k">return</span> <span class="n">G</span><span class="o">.</span><span class="n">subgraph</span><span class="p">(</span><span class="n">nodes_to_draw</span><span class="p">)</span>

<span class="c1"># Extract the subgraph with the nodes of interest: T_draw</span>
<span class="n">T_draw</span> <span class="o">=</span> <span class="n">get_nodes_and_nbrs</span><span class="p">(</span><span class="n">T</span><span class="p">,</span> <span class="n">nodes_of_interest</span><span class="p">)</span>

<span class="c1"># Draw the subgraph to the screen</span>
<span class="n">nx</span><span class="o">.</span><span class="n">draw</span><span class="p">(</span><span class="n">T_draw</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Draw-a-subgraph-for-nodes-with-particular-metadata">Draw a subgraph for nodes with particular metadata<a class="anchor-link" href="#Draw-a-subgraph-for-nodes-with-particular-metadata">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Extract the nodes of interest: nodes</span>
<span class="n">nodes</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">T</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;occupation&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;celebrity&#39;</span><span class="p">]</span>

<span class="c1"># Create the set of nodes: nodeset</span>
<span class="n">nodeset</span> <span class="o">=</span> <span class="nb">set</span><span class="p">(</span><span class="n">nodes</span><span class="p">)</span>

<span class="c1"># Iterate over nodes</span>
<span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">nodes</span><span class="p">:</span>

    <span class="c1"># Compute the neighbors of n: nbrs</span>
    <span class="n">nbrs</span> <span class="o">=</span> <span class="n">T</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">n</span><span class="p">)</span>

    <span class="c1"># Compute the union of nodeset and nbrs: nodeset</span>
    <span class="n">nodeset</span> <span class="o">=</span> <span class="n">nodeset</span><span class="o">.</span><span class="n">union</span><span class="p">(</span><span class="n">nbrs</span><span class="p">)</span>

<span class="c1"># Compute the subgraph using nodeset: T_sub</span>
<span class="n">T_sub</span> <span class="o">=</span> <span class="n">T</span><span class="o">.</span><span class="n">subgraph</span><span class="p">(</span><span class="n">nodeset</span><span class="p">)</span>

<span class="c1"># Draw T_sub to the screen</span>
<span class="n">nx</span><span class="o">.</span><span class="n">draw</span><span class="p">(</span><span class="n">T_sub</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Case-Study:-Github-user-collaboration-network">Case Study: Github user collaboration network<a class="anchor-link" href="#Case-Study:-Github-user-collaboration-network">&#182;</a></h2><h3 id="degree-dist-plot">degree dist plot<a class="anchor-link" href="#degree-dist-plot">&#182;</a></h3><div class="highlight"><pre><span></span><span class="n">h</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>

<span class="n">d</span><span class="o">=</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">h</span><span class="o">.</span><span class="n">values</span><span class="p">()))</span>

<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">d</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="betweenness-dist-plot">betweenness dist plot<a class="anchor-link" href="#betweenness-dist-plot">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Plot the degree distribution of the GitHub collaboration network</span>
<span class="n">h</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">betweenness_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>
<span class="n">b</span> <span class="o">=</span> <span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">h</span><span class="o">.</span><span class="n">values</span><span class="p">()))</span>

<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">b</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="ArcPlot">ArcPlot<a class="anchor-link" href="#ArcPlot">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Import necessary modules</span>
<span class="kn">from</span> <span class="nn">nxviz.plots</span> <span class="kn">import</span> <span class="n">ArcPlot</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>

<span class="c1"># Iterate over all the nodes in G, including the metadata</span>
<span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">):</span>

    <span class="c1"># Calculate the degree of each node: G.node[n][&#39;degree&#39;]</span>
    <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;degree&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">n</span><span class="p">)</span>

<span class="c1"># Create the ArcPlot object: a</span>
<span class="n">a</span> <span class="o">=</span> <span class="n">ArcPlot</span><span class="p">(</span><span class="n">graph</span><span class="o">=</span><span class="n">G</span><span class="p">,</span> <span class="n">node_order</span><span class="o">=</span><span class="s1">&#39;degree&#39;</span><span class="p">)</span>

<span class="c1"># Draw the ArcPlot to the screen</span>
<span class="n">a</span><span class="o">.</span><span class="n">draw</span><span class="p">()</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/github_arcplot.png" alt=""></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="CircosPlot">CircosPlot<a class="anchor-link" href="#CircosPlot">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Import necessary modules</span>
<span class="kn">from</span> <span class="nn">nxviz</span> <span class="kn">import</span> <span class="n">CircosPlot</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span> 

<span class="c1"># Iterate over all the nodes, including the metadata</span>
<span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">):</span>

    <span class="c1"># Calculate the degree of each node: G.node[n][&#39;degree&#39;]</span>
    <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;degree&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">n</span><span class="p">)</span>

<span class="c1"># Create the CircosPlot object: c</span>
<span class="n">c</span> <span class="o">=</span> <span class="n">CircosPlot</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">node_order</span><span class="o">=</span><span class="s1">&#39;degree&#39;</span><span class="p">,</span> <span class="n">node_grouping</span><span class="o">=</span><span class="s1">&#39;grouping&#39;</span><span class="p">,</span> <span class="n">node_color</span><span class="o">=</span><span class="s1">&#39;grouping&#39;</span><span class="p">)</span>

<span class="c1"># Draw the CircosPlot object to the screen</span>
<span class="n">c</span><span class="o">.</span><span class="n">draw</span><span class="p">()</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/github_circosplot.png" width="400"></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Cliques">Cliques<a class="anchor-link" href="#Cliques">&#182;</a></h3><p><strong>clique</strong>: group of nodes that are fully connected to one another.</p>
<ul>
<li>simplest clique is an edge</li>
<li>simplest complex clique is a triangle</li>
</ul>
<p><strong>maximal clique</strong>: a clique that cannot be extended by adding another node in the graph</p>
<h3 id="find-all-maximal-cliques">find all maximal cliques<a class="anchor-link" href="#find-all-maximal-cliques">&#182;</a></h3><div class="highlight"><pre><span></span><span class="n">nx</span><span class="o">.</span><span class="n">find_cliques</span><span class="p">(</span><span class="n">g</span><span class="p">)</span>
</pre></div>
<h3 id="find-length-of-each-maximal-clique">find length of each maximal clique<a class="anchor-link" href="#find-length-of-each-maximal-clique">&#182;</a></h3><div class="highlight"><pre><span></span><span class="k">for</span> <span class="n">clique</span> <span class="ow">in</span> <span class="n">nx</span><span class="o">.</span><span class="n">find_cliques</span><span class="p">(</span><span class="n">G</span><span class="p">):</span>
    <span class="k">print</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">clique</span><span class="p">))</span>
</pre></div>
<h3 id="find-len-of-all-maximal-cliques">find len of all maximal cliques<a class="anchor-link" href="#find-len-of-all-maximal-cliques">&#182;</a></h3><p>The key here is that <code>nx.find_cliques()</code> returns a generator, which needs to be converted to list before calling <code>list()</code></p>
<div class="highlight"><pre><span></span><span class="c1"># Calculate the maximal cliques in G: cliques</span>
<span class="n">cliques</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">find_cliques</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>

<span class="c1"># Count and print the number of maximal cliques in G</span>
<span class="k">print</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">cliques</span><span class="p">)))</span>
</pre></div>
<h3 id="create-subplot-of-largest-maximal-clique-&amp;-Circos-plot-it">create subplot of largest maximal clique &amp; Circos plot it<a class="anchor-link" href="#create-subplot-of-largest-maximal-clique-&amp;-Circos-plot-it">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Find the author(s) that are part of the largest maximal clique: largest_clique</span>
<span class="n">largest_clique</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">nx</span><span class="o">.</span><span class="n">find_cliques</span><span class="p">(</span><span class="n">G</span><span class="p">),</span> <span class="n">key</span><span class="o">=</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span><span class="nb">len</span><span class="p">(</span><span class="n">x</span><span class="p">))[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>

<span class="c1"># Create the subgraph of the largest_clique: G_lc</span>
<span class="n">G_lc</span> <span class="o">=</span> <span class="n">G</span><span class="o">.</span><span class="n">subgraph</span><span class="p">(</span><span class="n">largest_clique</span><span class="p">)</span>

<span class="c1"># Create the CircosPlot object: c</span>
<span class="n">c</span> <span class="o">=</span> <span class="n">CircosPlot</span><span class="p">(</span><span class="n">G_lc</span><span class="p">)</span>

<span class="c1"># Draw the CircosPlot to the screen</span>
<span class="n">c</span><span class="o">.</span><span class="n">draw</span><span class="p">()</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/github_circosplot_2.png" width="400"></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Tasks">Tasks<a class="anchor-link" href="#Tasks">&#182;</a></h3><h4 id="find-important-users">find important users<a class="anchor-link" href="#find-important-users">&#182;</a></h4><p>Degree Centrality</p>
<div class="highlight"><pre><span></span><span class="c1"># Compute the degree centralities of G: deg_cent</span>
<span class="n">deg_cent</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>

<span class="c1"># Compute the maximum degree centrality: max_dc</span>
<span class="n">max_dc</span> <span class="o">=</span> <span class="nb">max</span><span class="p">(</span><span class="n">deg_cent</span><span class="o">.</span><span class="n">values</span><span class="p">())</span>

<span class="c1"># Find the user(s) that have collaborated the most: prolific_collaborators</span>
<span class="n">prolific_collaborators</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">dc</span> <span class="ow">in</span> <span class="n">deg_cent</span><span class="o">.</span><span class="n">items</span><span class="p">()</span> <span class="k">if</span> <span class="n">n</span> <span class="o">==</span> <span class="n">max_dc</span><span class="p">]</span>

<span class="c1"># Print the most prolific collaborator(s)</span>
<span class="k">print</span><span class="p">(</span><span class="n">prolific_collaborators</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="find-largest-communities">find largest communities<a class="anchor-link" href="#find-largest-communities">&#182;</a></h4><p>Maximal Cliques</p>
<div class="highlight"><pre><span></span><span class="c1"># Import necessary modules</span>
<span class="kn">from</span> <span class="nn">nxviz</span> <span class="kn">import</span> <span class="n">ArcPlot</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>

<span class="c1"># Identify the largest maximal clique: largest_max_clique</span>
<span class="n">largest_max_clique</span> <span class="o">=</span> <span class="nb">set</span><span class="p">(</span><span class="nb">sorted</span><span class="p">(</span><span class="n">nx</span><span class="o">.</span><span class="n">find_cliques</span><span class="p">(</span><span class="n">G</span><span class="p">),</span> <span class="n">key</span><span class="o">=</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="nb">len</span><span class="p">(</span><span class="n">x</span><span class="p">))[</span><span class="o">-</span><span class="mi">1</span><span class="p">])</span>

<span class="c1"># Create a subgraph from the largest_max_clique: G_lmc</span>
<span class="n">G_lmc</span> <span class="o">=</span> <span class="n">G</span><span class="o">.</span><span class="n">subgraph</span><span class="p">(</span><span class="n">largest_max_clique</span><span class="p">)</span>

<span class="c1"># Go out 1 degree of separation</span>
<span class="k">for</span> <span class="n">node</span> <span class="ow">in</span> <span class="n">G_lmc</span><span class="o">.</span><span class="n">nodes</span><span class="p">():</span>
    <span class="n">G_lmc</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">node</span><span class="p">))</span>
    <span class="n">G_lmc</span><span class="o">.</span><span class="n">add_edges_from</span><span class="p">(</span><span class="nb">zip</span><span class="p">([</span><span class="n">node</span><span class="p">]</span><span class="o">*</span><span class="nb">len</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">node</span><span class="p">)),</span> <span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">node</span><span class="p">)))</span>

<span class="c1"># Record each node&#39;s degree centrality score</span>
<span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">G_lmc</span><span class="o">.</span><span class="n">nodes</span><span class="p">():</span>
    <span class="n">G_lmc</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;degree centrality&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G_lmc</span><span class="p">)[</span><span class="n">n</span><span class="p">]</span>

<span class="c1"># Create the ArcPlot object: a</span>
<span class="n">a</span> <span class="o">=</span> <span class="n">ArcPlot</span><span class="p">(</span><span class="n">G_lmc</span><span class="p">,</span> <span class="n">node_order</span><span class="o">=</span><span class="s1">&#39;degree centrality&#39;</span><span class="p">)</span>

<span class="c1"># Draw the ArcPlot to the screen</span>
<span class="n">a</span><span class="o">.</span><span class="n">draw</span><span class="p">()</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/github_arcplot_2.png" width="400"></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Build-recommendation-systems">Build recommendation systems<a class="anchor-link" href="#Build-recommendation-systems">&#182;</a></h4><p>Look for open triangles</p>
<div class="highlight"><pre><span></span><span class="c1"># Import necessary modules</span>
<span class="kn">from</span> <span class="nn">itertools</span> <span class="kn">import</span> <span class="n">combinations</span>
<span class="kn">from</span> <span class="nn">collections</span> <span class="kn">import</span> <span class="n">defaultdict</span>

<span class="c1"># Initialize the defaultdict: recommended</span>
<span class="n">recommended</span> <span class="o">=</span> <span class="n">defaultdict</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>

<span class="c1"># Iterate over all the nodes in G</span>
<span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">):</span>

    <span class="c1"># Iterate over all possible triangle relationship combinations</span>
    <span class="k">for</span> <span class="n">n1</span><span class="p">,</span> <span class="n">n2</span> <span class="ow">in</span> <span class="n">combinations</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">n</span><span class="p">),</span> <span class="mi">2</span><span class="p">):</span>

        <span class="c1"># Check whether n1 and n2 do not have an edge</span>
        <span class="k">if</span> <span class="ow">not</span> <span class="n">G</span><span class="o">.</span><span class="n">has_edge</span><span class="p">(</span><span class="n">n1</span><span class="p">,</span> <span class="n">n2</span><span class="p">):</span>

            <span class="c1"># Increment recommended</span>
            <span class="n">recommended</span><span class="p">[(</span><span class="n">n1</span><span class="p">,</span> <span class="n">n2</span><span class="p">)]</span> <span class="o">+=</span> <span class="mi">1</span>

<span class="c1"># Identify the top 10 pairs of users</span>
<span class="n">all_counts</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="n">recommended</span><span class="o">.</span><span class="n">values</span><span class="p">())</span>
<span class="n">top10_pairs</span> <span class="o">=</span> <span class="p">[</span><span class="n">pair</span> <span class="k">for</span> <span class="n">pair</span><span class="p">,</span> <span class="n">count</span> <span class="ow">in</span> <span class="n">recommended</span><span class="o">.</span><span class="n">items</span><span class="p">()</span> <span class="k">if</span> <span class="n">count</span> <span class="o">&gt;</span> <span class="n">all_counts</span><span class="p">[</span><span class="o">-</span><span class="mi">10</span><span class="p">]]</span>
<span class="k">print</span><span class="p">(</span><span class="n">top10_pairs</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>Network</strong> = Graph = (nodes, edges)</p>
<ul>
<li>directed or undirected<ul>
<li>undirected = Facebook (bilateral)</li>
<li>directed = Twitter (unilateral)</li>
</ul>
</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<div class="highlight"><pre><span></span><span class="c1"># Create the CircosPlot object: c</span>
<span class="n">c</span> <span class="o">=</span> <span class="n">CircosPlot</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">node_color</span><span class="o">=</span><span class="s1">&#39;bipartite&#39;</span><span class="p">,</span> <span class="n">node_grouping</span><span class="o">=</span><span class="s1">&#39;bipartite&#39;</span><span class="p">,</span> <span class="n">node_order</span><span class="o">=</span><span class="s1">&#39;centrality&#39;</span><span class="p">)</span>

<span class="c1"># Draw c to the screen</span>
<span class="n">c</span><span class="o">.</span><span class="n">draw</span><span class="p">()</span>

<span class="c1"># Display the plot</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/circosplot_3.png" width=400></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="bipartite-graph">bipartite graph<a class="anchor-link" href="#bipartite-graph">&#182;</a></h2><p><strong>bipartite graph</strong>: a graph that is partitioned into two sets; nodes are only connected across sets.</p>
<ul>
<li>customers and the products they buy are two partitions in one graph.  Customers are connected by edges to the products they've purchased, but not connected to other customers.</li>
<li>it's customary to indicate which partition a node belongs to by adding a <code>bipartite=[partition]</code> entry in the node's dictionary</li>
</ul>
<h3 id="degree-centrality-in-bipartite-graphs">degree centrality in bipartite graphs<a class="anchor-link" href="#degree-centrality-in-bipartite-graphs">&#182;</a></h3><p>Normally, degree centrality is:
$$\frac{\#\ of\ neighbors}{\#\ of\ possible\ neighbors}$$</p>
<p>In a bipartite graph, the denominator is the number of members in the other partition:
$$\frac{\#\ of\ neighbors}{\#\ of\ nodes\ in\ other\ partition}$$</p>
<div class="highlight"><pre><span></span><span class="n">cust_nodes</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;customers&#39;</span><span class="p">]</span>

<span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">cust_nodes</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="retrieving-nodes-from-a-partition">retrieving nodes from a partition<a class="anchor-link" href="#retrieving-nodes-from-a-partition">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Define get_nodes_from_partition()</span>
<span class="k">def</span> <span class="nf">get_nodes_from_partition</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">partition</span><span class="p">):</span>
    <span class="c1"># Initialize an empty list for nodes to be returned</span>
    <span class="n">nodes</span> <span class="o">=</span> <span class="p">[]</span>
    <span class="c1"># Iterate over each node in the graph G</span>
    <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">():</span>
        <span class="c1"># Check that the node belongs to the particular partition</span>
        <span class="k">if</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="n">partition</span><span class="p">:</span>
            <span class="c1"># If so, append it to the list of nodes</span>
            <span class="n">nodes</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">n</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">nodes</span>

<span class="c1"># Print the number of nodes in the &#39;projects&#39; partition</span>
<span class="k">print</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">get_nodes_from_partition</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="s1">&#39;projects&#39;</span><span class="p">)))</span>

<span class="c1"># Print the number of nodes in the &#39;users&#39; partition</span>
<span class="k">print</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">get_nodes_from_partition</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="s1">&#39;users&#39;</span><span class="p">)))</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="degree-centrality-distribution">degree centrality distribution<a class="anchor-link" href="#degree-centrality-distribution">&#182;</a></h3><p><strong>degree centrality distribution</strong> is the list of degree centrality scores for all nodes in the graph</p>
<div class="highlight"><pre><span></span><span class="c1"># Get the &#39;users&#39; nodes: user_nodes</span>
<span class="n">user_nodes</span> <span class="o">=</span> <span class="n">get_nodes_from_partition</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="s1">&#39;users&#39;</span><span class="p">)</span>

<span class="c1"># Compute the degree centralities: dcs</span>
<span class="n">dcs</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>

<span class="c1"># Get the degree centralities for user_nodes: user_dcs</span>
<span class="n">user_dcs</span> <span class="o">=</span> <span class="p">[</span><span class="n">dcs</span><span class="p">[</span><span class="n">n</span><span class="p">]</span> <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">user_nodes</span><span class="p">]</span>

<span class="c1"># Plot the degree distribution of users_dcs</span>
<span class="n">plt</span><span class="o">.</span><span class="n">yscale</span><span class="p">(</span><span class="s1">&#39;log&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="n">user_dcs</span><span class="p">,</span> <span class="n">bins</span><span class="o">=</span><span class="mi">20</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/deg_cent_hist.png" width=400></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Bipartite-Graphs-and-Recommendation-Systems">Bipartite Graphs and Recommendation Systems<a class="anchor-link" href="#Bipartite-Graphs-and-Recommendation-Systems">&#182;</a></h2><p>Unipartite - connect users to users
Bipartite - recommendation systems are based on set overlap between highly-similar nodes on one partition.</p>
<ul>
<li>Users 1, 2 &amp; 3 are connected to Repo 2.  User 3 is also connected to Repo 1.  We can recommend Repo 1 to Users 1 &amp; 2.</li>
</ul>
<p><strong>Node sets</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[42]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># create the graph</span>

<span class="n">G</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">Graph</span><span class="p">()</span>

<span class="n">G</span><span class="o">.</span><span class="n">add_node</span><span class="p">(</span><span class="s1">&#39;user 1&#39;</span><span class="p">)</span>

<span class="n">G</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">([</span><span class="s1">&#39;user 2&#39;</span><span class="p">,</span> <span class="s1">&#39;user 3&#39;</span><span class="p">])</span>

<span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">():</span>
    <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s1">&#39;users&#39;</span>

<span class="n">users</span> <span class="o">=</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">()</span> <span class="k">if</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;users&#39;</span><span class="p">)</span>

<span class="n">G</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">([</span><span class="s1">&#39;repo 1&#39;</span><span class="p">,</span> <span class="s1">&#39;repo 2&#39;</span><span class="p">,</span> <span class="s1">&#39;repo 3&#39;</span><span class="p">])</span>
<span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="s1">&#39;repo 1&#39;</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s1">&#39;repos&#39;</span>
<span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="s1">&#39;repo 2&#39;</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s1">&#39;repos&#39;</span>
<span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="s1">&#39;repo 3&#39;</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s1">&#39;repos&#39;</span>

<span class="n">G</span><span class="o">.</span><span class="n">add_edges_from</span><span class="p">([(</span><span class="s1">&#39;user 1&#39;</span><span class="p">,</span> <span class="s1">&#39;repo 3&#39;</span><span class="p">),</span> <span class="p">(</span><span class="s1">&#39;user 2&#39;</span><span class="p">,</span> <span class="s1">&#39;repo 3&#39;</span><span class="p">),</span> <span class="p">(</span><span class="s1">&#39;user 3&#39;</span><span class="p">,</span> <span class="s1">&#39;repo 3&#39;</span><span class="p">),</span> <span class="p">(</span><span class="s1">&#39;user 3&#39;</span><span class="p">,</span> <span class="s1">&#39;repo 2&#39;</span><span class="p">)])</span>

<span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[42]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>NodeDataView({&#39;user 1&#39;: {&#39;bipartite&#39;: &#39;users&#39;}, &#39;user 2&#39;: {&#39;bipartite&#39;: &#39;users&#39;}, &#39;user 3&#39;: {&#39;bipartite&#39;: &#39;users&#39;}, &#39;repo 1&#39;: {&#39;bipartite&#39;: &#39;repos&#39;}, &#39;repo 2&#39;: {&#39;bipartite&#39;: &#39;repos&#39;}, &#39;repo 3&#39;: {&#39;bipartite&#39;: &#39;repos&#39;}})</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[42]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>EdgeView([(&#39;user 1&#39;, &#39;repo 3&#39;), (&#39;user 2&#39;, &#39;repo 3&#39;), (&#39;user 3&#39;, &#39;repo 3&#39;), (&#39;user 3&#39;, &#39;repo 2&#39;)])</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[53]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># fetch neighbors</span>
<span class="n">user1_nbrs</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="s1">&#39;user 1&#39;</span><span class="p">))</span>
<span class="n">user1_nbrs</span>

<span class="n">user3_nbrs</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="s1">&#39;user 3&#39;</span><span class="p">))</span>
<span class="n">user3_nbrs</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[53]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>[&#39;repo 3&#39;]</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[53]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>[&#39;repo 3&#39;, &#39;repo 2&#39;]</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[55]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># find intersection of neighbors for users 1 &amp; 3</span>
<span class="nb">set</span><span class="p">(</span><span class="n">user1_nbrs</span><span class="p">)</span><span class="o">.</span><span class="n">intersection</span><span class="p">(</span><span class="n">user3_nbrs</span><span class="p">)</span>

<span class="c1"># find difference of neighbors for users 1 &amp; 3 -- repos to recommend</span>
<span class="c1"># notice that order of args matters</span>
<span class="nb">set</span><span class="p">(</span><span class="n">user1_nbrs</span><span class="p">)</span><span class="o">.</span><span class="n">difference</span><span class="p">(</span><span class="n">user3_nbrs</span><span class="p">)</span>
<span class="nb">set</span><span class="p">(</span><span class="n">user3_nbrs</span><span class="p">)</span><span class="o">.</span><span class="n">difference</span><span class="p">(</span><span class="n">user1_nbrs</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[55]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>{&#39;repo 3&#39;}</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[55]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>set()</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[55]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>{&#39;repo 2&#39;}</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="return-repos-shared-by-2-users">return repos shared by 2 users<a class="anchor-link" href="#return-repos-shared-by-2-users">&#182;</a></h3><div class="highlight"><pre><span></span><span class="k">def</span> <span class="nf">shared_partition_nodes</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">node1</span><span class="p">,</span> <span class="n">node2</span><span class="p">):</span>
    <span class="c1"># Check that the nodes belong to the same partition</span>
    <span class="k">assert</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">node1</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">node2</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span>

    <span class="c1"># Get neighbors of node 1: nbrs1</span>
    <span class="n">nbrs1</span> <span class="o">=</span> <span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">node1</span><span class="p">)</span>
    <span class="c1"># Get neighbors of node 2: nbrs2</span>
    <span class="n">nbrs2</span> <span class="o">=</span> <span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">node2</span><span class="p">)</span>

    <span class="c1"># Compute the overlap using set intersections</span>
    <span class="n">overlap</span> <span class="o">=</span> <span class="nb">set</span><span class="p">(</span><span class="n">nbrs1</span><span class="p">)</span><span class="o">.</span><span class="n">intersection</span><span class="p">(</span><span class="n">nbrs2</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">overlap</span>

<span class="c1"># Print the number of shared repositories between users &#39;u7909&#39; and &#39;u2148&#39;</span>
<span class="k">print</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">shared_partition_nodes</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="s1">&#39;u7909&#39;</span><span class="p">,</span> <span class="s1">&#39;u2148&#39;</span><span class="p">)))</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="user-similarity-metric">user similarity metric<a class="anchor-link" href="#user-similarity-metric">&#182;</a></h3><p>Function to calculate the metric of similarity:</p>
<p>$$\frac{\#\ projects\ shared\ by\ 2\ users}{total\ \#\ of\ projects\ in\ other\ partitiion}$$</p>
<div class="highlight"><pre><span></span><span class="k">def</span> <span class="nf">user_similarity</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">user1</span><span class="p">,</span> <span class="n">user2</span><span class="p">,</span> <span class="n">proj_nodes</span><span class="p">):</span>
    <span class="c1"># Check that the nodes belong to the &#39;users&#39; partition</span>
    <span class="k">assert</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">user1</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;users&#39;</span>
    <span class="k">assert</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">user2</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;users&#39;</span>

    <span class="c1"># Get the set of nodes shared between the two users</span>
    <span class="n">shared_nodes</span> <span class="o">=</span> <span class="n">shared_partition_nodes</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">user1</span><span class="p">,</span> <span class="n">user2</span><span class="p">)</span>

    <span class="c1"># Return the fraction of nodes in the projects partition</span>
    <span class="k">return</span> <span class="nb">len</span><span class="p">(</span><span class="n">shared_nodes</span><span class="p">)</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">proj_nodes</span><span class="p">)</span>

<span class="c1"># Compute the similarity score between users &#39;u4560&#39; and &#39;u1880&#39;</span>
<span class="n">project_nodes</span> <span class="o">=</span> <span class="n">get_nodes_from_partition</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="s1">&#39;projects&#39;</span><span class="p">)</span>
<span class="n">similarity_score</span> <span class="o">=</span> <span class="n">user_similarity</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="s1">&#39;u4560&#39;</span><span class="p">,</span> <span class="s1">&#39;u1880&#39;</span><span class="p">,</span> <span class="n">project_nodes</span><span class="p">)</span>

<span class="k">print</span><span class="p">(</span><span class="n">similarity_score</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="find-users-most-similar-to-a-given-user">find users most similar to a given user<a class="anchor-link" href="#find-users-most-similar-to-a-given-user">&#182;</a></h3><div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">collections</span> <span class="kn">import</span> <span class="n">defaultdict</span>

<span class="k">def</span> <span class="nf">most_similar_users</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">user</span><span class="p">,</span> <span class="n">user_nodes</span><span class="p">,</span> <span class="n">proj_nodes</span><span class="p">):</span>
    <span class="c1"># Data checks</span>
    <span class="k">assert</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">user</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;users&#39;</span>

    <span class="c1"># Get other nodes from user partition</span>
    <span class="n">user_nodes</span> <span class="o">=</span> <span class="nb">set</span><span class="p">(</span><span class="n">user_nodes</span><span class="p">)</span>
    <span class="n">user_nodes</span><span class="o">.</span><span class="n">remove</span><span class="p">(</span><span class="n">user</span><span class="p">)</span>

    <span class="c1"># Create the dictionary: similarities</span>
    <span class="n">similarities</span> <span class="o">=</span> <span class="n">defaultdict</span><span class="p">(</span><span class="nb">list</span><span class="p">)</span>
    <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">user_nodes</span><span class="p">:</span>
        <span class="n">similarity</span> <span class="o">=</span> <span class="n">user_similarity</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">user</span><span class="p">,</span> <span class="n">n</span><span class="p">,</span> <span class="n">proj_nodes</span><span class="p">)</span>
        <span class="n">similarities</span><span class="p">[</span><span class="n">similarity</span><span class="p">]</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">n</span><span class="p">)</span>

    <span class="c1"># Compute maximum similarity score: max_similarity</span>
    <span class="n">max_similarity</span> <span class="o">=</span> <span class="nb">max</span><span class="p">(</span><span class="n">similarities</span><span class="o">.</span><span class="n">keys</span><span class="p">())</span>

    <span class="c1"># Return list of users that share maximal similarity</span>
    <span class="k">return</span> <span class="n">similarities</span><span class="p">[</span><span class="n">max_similarity</span><span class="p">]</span>

<span class="n">user_nodes</span> <span class="o">=</span> <span class="n">get_nodes_from_partition</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="s1">&#39;users&#39;</span><span class="p">)</span>
<span class="n">project_nodes</span> <span class="o">=</span> <span class="n">get_nodes_from_partition</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="s1">&#39;projects&#39;</span><span class="p">)</span>

<span class="k">print</span><span class="p">(</span><span class="n">most_similar_users</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="s1">&#39;u4560&#39;</span><span class="p">,</span> <span class="n">user_nodes</span><span class="p">,</span> <span class="n">project_nodes</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="recommend-repositories">recommend repositories<a class="anchor-link" href="#recommend-repositories">&#182;</a></h3><div class="highlight"><pre><span></span><span class="k">def</span> <span class="nf">recommend_repositories</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">from_user</span><span class="p">,</span> <span class="n">to_user</span><span class="p">):</span>
    <span class="c1"># Get the set of repositories that from_user has contributed to</span>
    <span class="n">from_repos</span> <span class="o">=</span> <span class="nb">set</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">from_user</span><span class="p">))</span>
    <span class="c1"># Get the set of repositories that to_user has contributed to</span>
    <span class="n">to_repos</span> <span class="o">=</span> <span class="nb">set</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">to_user</span><span class="p">))</span>

    <span class="c1"># Identify repositories that the from_user is connected to that the to_user is not connected to</span>
    <span class="k">return</span> <span class="n">from_repos</span><span class="o">.</span><span class="n">difference</span><span class="p">(</span><span class="n">to_repos</span><span class="p">)</span>

<span class="c1"># Print the repositories to be recommended</span>
<span class="k">print</span><span class="p">(</span><span class="n">recommend_repositories</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="s1">&#39;u7909&#39;</span><span class="p">,</span> <span class="s1">&#39;u2148&#39;</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Bipartite-Graph-Projections-&amp;-Matrix-Operations">Bipartite Graph Projections &amp; Matrix Operations<a class="anchor-link" href="#Bipartite-Graph-Projections-&amp;-Matrix-Operations">&#182;</a></h2><p><strong>projection</strong>: may be useful to investigate the relationships between nodes on one partition conditioned on the connections to the nodes in the other partition.</p>
<ul>
<li>e.g., Which customers are relationed to one another, based on the products they've both bought?  If Cust 1 &amp; 2 bought Product 3, the customer projection would show Custs 1 &amp; 2 connected by a single edge.</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="importing-a-graph">importing a graph<a class="anchor-link" href="#importing-a-graph">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Read in the data: g</span>
<span class="n">G</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">read_edgelist</span><span class="p">(</span><span class="n">base_url</span> <span class="o">+</span> <span class="s1">&#39;american-revolution.csv&#39;</span><span class="p">)</span>

<span class="c1"># Assign nodes to &#39;clubs&#39; or &#39;people&#39; partitions</span>
<span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">):</span>
    <span class="k">if</span> <span class="s1">&#39;.&#39;</span> <span class="ow">in</span> <span class="n">n</span><span class="p">:</span>
        <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s1">&#39;people&#39;</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="s1">&#39;clubs&#39;</span>

<span class="c1"># Print the edges of the graph</span>
<span class="k">print</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">())</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="computing-projection">computing projection<a class="anchor-link" href="#computing-projection">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Prepare the nodelists needed for computing projections: people, clubs</span>
<span class="n">people</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">()</span> <span class="k">if</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;people&#39;</span><span class="p">]</span>
<span class="n">clubs</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;clubs&#39;</span><span class="p">]</span>

<span class="c1"># Compute the people and clubs projections: peopleG, clubsG</span>
<span class="n">peopleG</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">projected_graph</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">people</span><span class="p">)</span>
<span class="n">clubsG</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">projected_graph</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">clubs</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="list-comprehension-to-collect-nodes-in-a-partition">list comprehension to collect nodes in a partition<a class="anchor-link" href="#list-comprehension-to-collect-nodes-in-a-partition">&#182;</a></h3><p>Without using <code>(data=True)</code> - find each node (<code>[n]</code>) then take the key of the node (<code>[bipartite]</code>)</p>
<div class="highlight"><pre><span></span><span class="n">people</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">()</span> <span class="k">if</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;people&#39;</span><span class="p">]</span>
</pre></div>
<p>Using <code>(data=True)</code> iterate the node and its dictionary as <code>n, d</code> then ask <code>d</code> for its key <code>bipartite</code></p>
<div class="highlight"><pre><span></span><span class="n">clubs</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;clubs&#39;</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="plot-degree-centrality-on-projection">plot degree centrality on projection<a class="anchor-link" href="#plot-degree-centrality-on-projection">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Plot the degree centrality distribution of both node partitions from the original graph</span>
<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>
<span class="n">original_dc</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">people</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">original_dc</span><span class="o">.</span><span class="n">values</span><span class="p">()),</span> <span class="n">alpha</span><span class="o">=</span><span class="mf">0.5</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">yscale</span><span class="p">(</span><span class="s1">&#39;log&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Bipartite degree centrality&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>


<span class="c1"># Plot the degree centrality distribution of the peopleG graph</span>
<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>  
<span class="n">people_dc</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">peopleG</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">people_dc</span><span class="o">.</span><span class="n">values</span><span class="p">()))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">yscale</span><span class="p">(</span><span class="s1">&#39;log&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Degree centrality of people partition&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="c1"># Plot the degree centrality distribution of the clubsG graph</span>
<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span> 
<span class="n">clubs_dc</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">clubsG</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">clubs_dc</span><span class="o">.</span><span class="n">values</span><span class="p">()))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">yscale</span><span class="p">(</span><span class="s1">&#39;log&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Degree centrality of clubs partition&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Bipartite-Adjacency-Graph-Matrices">Bipartite Adjacency Graph Matrices<a class="anchor-link" href="#Bipartite-Adjacency-Graph-Matrices">&#182;</a></h2><p>Bipartite graphs represented in a matrix graph</p>
<ul>
<li>one partition as rows</li>
<li>the other partition as columns</li>
</ul>
<p>Are often asymmetric bc there are more ways to construct an asymmetic bipartite graph than a symmetric one.</p>
<h3 id="bipartite-biadjacency-matrix">bipartite biadjacency matrix<a class="anchor-link" href="#bipartite-biadjacency-matrix">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># returns a sparse matrix version of the graph</span>
<span class="n">bipartite</span><span class="o">.</span><span class="n">biadjacency_matrix</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">row_order</span><span class="o">=</span><span class="n">x</span><span class="p">,</span> <span class="p">[</span><span class="n">column_order</span><span class="o">=</span><span class="n">y</span><span class="p">])</span>
</pre></div>
<h3 id="separate-nodes-into-partitions-&amp;-compute-adjacency-matrix">separate nodes into partitions &amp; compute adjacency matrix<a class="anchor-link" href="#separate-nodes-into-partitions-&amp;-compute-adjacency-matrix">&#182;</a></h3><div class="highlight"><pre><span></span><span class="n">cust_nodes</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">()</span> <span class="k">if</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;customers&#39;</span><span class="p">]</span>
<span class="n">prod_nodes</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">()</span> <span class="k">if</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;products&#39;</span><span class="p">]</span>

<span class="n">mat</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">biadjacency_matrix</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">row_order</span><span class="o">=</span><span class="n">cust_nodes</span><span class="p">,</span> <span class="n">column_order</span><span class="o">=</span><span class="n">prod_nodes</span><span class="p">)</span>
</pre></div>
<h2 id="Matrix-projection">Matrix projection<a class="anchor-link" href="#Matrix-projection">&#182;</a></h2><p>Projection is computable using matrix multiplication - matrix @ matrix.T = projection</p>
<ul>
<li>multiply</li>
</ul>
<p><img src="images/matrix_mult_1.png" width=400></p>
<p>sum_r_1 + sum_c_1 = r1_c1
(0+1) * (0+1) = 1</p>
<ol>
<li>add the values of row 1 = sum_r_1 </li>
<li>add the values of column 1 = sum_c_1</li>
<li>r1_c1 of projection matrix = sum_r_1 * sum_c_1</li>
</ol>
<p><img src="images/matrix_mult_2.png" width=400></p>
<p>row_1 * col_2 = r_1_c_2</p>
<p><img src="images/matrix_mult_3.png" width=400></p>
<p><img src="images/matrix_mult_4.png" width=400></p>
<p><img src="images/matrix_mult_5.png" width=400></p>
<p><img src="images/matrix_mult_6.png" width=400></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="compute-adjacency-matrix">compute adjacency matrix<a class="anchor-link" href="#compute-adjacency-matrix">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Get the list of people and list of clubs from the graph: people_nodes, clubs_nodes</span>
<span class="n">people_nodes</span> <span class="o">=</span> <span class="n">get_nodes_from_partition</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="s1">&#39;people&#39;</span><span class="p">)</span>
<span class="n">clubs_nodes</span> <span class="o">=</span> <span class="n">get_nodes_from_partition</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="s1">&#39;clubs&#39;</span><span class="p">)</span>

<span class="c1"># Compute the biadjacency matrix: bi_matrix</span>
<span class="n">bi_matrix</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">biadjacency_matrix</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">row_order</span><span class="o">=</span><span class="n">people_nodes</span><span class="p">,</span> <span class="n">column_order</span><span class="o">=</span><span class="n">clubs_nodes</span><span class="p">)</span>

<span class="c1"># Compute the user-user projection: user_matrix</span>
<span class="n">user_matrix</span> <span class="o">=</span> <span class="n">bi_matrix</span> <span class="err">@</span> <span class="n">bi_matrix</span><span class="o">.</span><span class="n">T</span>

<span class="k">print</span><span class="p">(</span><span class="n">user_matrix</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="find-shared-membership:-Transposition">find shared membership: Transposition<a class="anchor-link" href="#find-shared-membership:-Transposition">&#182;</a></h3><p>Find the names of people who were members of the most clubs</p>
<div class="highlight"><pre><span></span><span class="c1"># Find out the names of people who were members of the most number of clubs</span>
<span class="n">diag</span> <span class="o">=</span> <span class="n">user_matrix</span><span class="o">.</span><span class="n">diagonal</span><span class="p">()</span> 
<span class="n">indices</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">where</span><span class="p">(</span><span class="n">diag</span> <span class="o">==</span> <span class="n">diag</span><span class="o">.</span><span class="n">max</span><span class="p">())[</span><span class="mi">0</span><span class="p">]</span>  
<span class="k">print</span><span class="p">(</span><span class="s1">&#39;Number of clubs: {0}&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">diag</span><span class="o">.</span><span class="n">max</span><span class="p">()))</span>
<span class="k">print</span><span class="p">(</span><span class="s1">&#39;People with the most memberships:&#39;</span><span class="p">)</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">indices</span><span class="p">:</span>
    <span class="k">print</span><span class="p">(</span><span class="s1">&#39;- {0}&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">people_nodes</span><span class="p">[</span><span class="n">i</span><span class="p">]))</span>

<span class="c1"># Set the diagonal to zero and convert it to a coordinate matrix format</span>
<span class="n">user_matrix</span><span class="o">.</span><span class="n">setdiag</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="n">users_coo</span> <span class="o">=</span> <span class="n">user_matrix</span><span class="o">.</span><span class="n">tocoo</span><span class="p">()</span>

<span class="c1"># Find pairs of users who shared membership in the most number of clubs</span>
<span class="n">indices</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">where</span><span class="p">(</span><span class="n">users_coo</span><span class="o">.</span><span class="n">data</span> <span class="o">==</span> <span class="n">users_coo</span><span class="o">.</span><span class="n">data</span><span class="o">.</span><span class="n">max</span><span class="p">())[</span><span class="mi">0</span><span class="p">]</span>
<span class="k">print</span><span class="p">(</span><span class="s1">&#39;People with most shared memberships:&#39;</span><span class="p">)</span>
<span class="k">for</span> <span class="n">idx</span> <span class="ow">in</span> <span class="n">indices</span><span class="p">:</span>
    <span class="k">print</span><span class="p">(</span><span class="s1">&#39;- {0}, {1}&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">people_nodes</span><span class="p">[</span><span class="n">users_coo</span><span class="o">.</span><span class="n">row</span><span class="p">[</span><span class="n">idx</span><span class="p">]],</span> <span class="n">people_nodes</span><span class="p">[</span><span class="n">users_coo</span><span class="o">.</span><span class="n">col</span><span class="p">[</span><span class="n">idx</span><span class="p">]]))</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="representing-network-data-in-pandas">representing network data in pandas<a class="anchor-link" href="#representing-network-data-in-pandas">&#182;</a></h2><p>Create lists of tuples for each nodes and edges extracted from a graph, use each to create a DataFrame, save each list to .csv</p>
<div class="highlight"><pre><span></span><span class="c1"># start from a graph</span>
<span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>

<span class="n">Out</span><span class="p">:</span> <span class="p">[(</span><span class="mi">0</span><span class="p">,</span> <span class="p">{</span><span class="s1">&#39;bipartite&#39;</span><span class="p">:</span> <span class="mi">0</span><span class="p">}),</span>
      <span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="p">{</span><span class="s1">&#39;bipartite&#39;</span><span class="p">:</span> <span class="mi">0</span><span class="p">}),</span>
      <span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="p">{</span><span class="s1">&#39;bipartite&#39;</span><span class="p">:</span> <span class="mi">0</span><span class="p">}),</span>
      <span class="o">...</span><span class="p">]</span>

<span class="c1"># create empty list to hold to-be-created nodes</span>
<span class="n">nodelist</span> <span class="o">=</span> <span class="p">[]</span>

<span class="c1"># iterate through graph, creating tuples for node name + dictionary for metadata</span>
<span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">):</span>
    <span class="n">node_data</span> <span class="o">=</span> <span class="nb">dict</span><span class="p">()</span>
    <span class="n">node_data</span><span class="p">[</span><span class="s1">&#39;node&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">n</span>   <span class="c1"># make sure this is not a key in the node&#39;s metadata dictionary</span>
    <span class="n">node_data</span><span class="o">.</span><span class="n">update</span><span class="p">(</span><span class="n">d</span><span class="p">)</span>
    <span class="n">nodelist</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">node_data</span><span class="p">)</span>

<span class="c1"># create a new DataFrame object and add nodelist data</span>
<span class="c1"># keys become columns, values become rows</span>
<span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">nodelist</span><span class="p">)</span>

<span class="c1"># write to .csv</span>
<span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">nodelist</span><span class="p">)</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s1">&#39;my_file.csv&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="write-nodes-to-disk">write nodes to disk<a class="anchor-link" href="#write-nodes-to-disk">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Initialize a list to store each edge as a record: nodelist</span>
<span class="n">nodelist</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G_people</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">):</span>
    <span class="c1"># nodeinfo stores one &quot;record&quot; of data as a dict</span>
    <span class="n">nodeinfo</span> <span class="o">=</span> <span class="p">{</span><span class="s1">&#39;person&#39;</span><span class="p">:</span> <span class="n">n</span><span class="p">}</span> 

    <span class="c1"># Update the nodeinfo dictionary </span>
    <span class="n">nodeinfo</span><span class="o">.</span><span class="n">update</span><span class="p">(</span><span class="n">d</span><span class="p">)</span>

    <span class="c1"># Append the nodeinfo to the node list</span>
    <span class="n">nodelist</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">nodeinfo</span><span class="p">)</span>


<span class="c1"># Create a pandas DataFrame of the nodelist: node_df</span>
<span class="n">node_df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">nodelist</span><span class="p">)</span>
<span class="k">print</span><span class="p">(</span><span class="n">node_df</span><span class="o">.</span><span class="n">head</span><span class="p">())</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="write-edges-to-disk">write edges to disk<a class="anchor-link" href="#write-edges-to-disk">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Initialize a list to store each edge as a record: edgelist</span>
<span class="n">edgelist</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">n1</span><span class="p">,</span> <span class="n">n2</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G_people</span><span class="o">.</span><span class="n">edges</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">):</span>
    <span class="c1"># Initialize a dictionary that shows edge information: edgeinfo</span>
    <span class="n">edgeinfo</span> <span class="o">=</span> <span class="p">{</span><span class="s1">&#39;node1&#39;</span><span class="p">:</span><span class="n">n1</span><span class="p">,</span> <span class="s1">&#39;node2&#39;</span><span class="p">:</span><span class="n">n2</span><span class="p">}</span>

    <span class="c1"># Update the edgeinfo data with the edge metadata</span>
    <span class="n">edgeinfo</span><span class="o">.</span><span class="n">update</span><span class="p">(</span><span class="n">d</span><span class="p">)</span>

    <span class="c1"># Append the edgeinfo to the edgelist</span>
    <span class="n">edgelist</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">edgeinfo</span><span class="p">)</span>

<span class="c1"># Create a pandas DataFrame of the edgelist: edge_df</span>
<span class="n">edge_df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">edgelist</span><span class="p">)</span>
<span class="k">print</span><span class="p">(</span><span class="n">edge_df</span><span class="o">.</span><span class="n">head</span><span class="p">())</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="graph-differences">graph differences<a class="anchor-link" href="#graph-differences">&#182;</a></h2><p>Time series analysis - how some number changes as a function of time
Rate of change of things over a sliding window of time</p>
<p><strong>evolving graphs</strong></p>
<ul>
<li>examples<ul>
<li>graphs that change over time - communication networks<ul>
<li>assumptions:<ul>
<li>edge changes over time; assume that nodes stay constant</li>
<li>both edges and nodes change over time
<strong>graph differences</strong>: if a node set doesn't change: changing only the edge set will result in a change in the graph            </li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="list-of-graphs">list of graphs<a class="anchor-link" href="#list-of-graphs">&#182;</a></h3><div class="highlight"><pre><span></span><span class="n">months</span> <span class="o">=</span> <span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="mi">11</span><span class="p">)</span>

<span class="c1"># Initialize an empty list: Gs</span>
<span class="n">Gs</span> <span class="o">=</span> <span class="p">[]</span> 
<span class="k">for</span> <span class="n">month</span> <span class="ow">in</span> <span class="n">months</span><span class="p">:</span>
    <span class="c1"># Instantiate a new undirected graph: G</span>
    <span class="n">G</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">Graph</span><span class="p">()</span>

    <span class="c1"># Add in all nodes that have ever shown up to the graph</span>
    <span class="n">G</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">(</span><span class="n">data</span><span class="p">[</span><span class="s1">&#39;sender&#39;</span><span class="p">])</span>
    <span class="n">G</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">(</span><span class="n">data</span><span class="p">[</span><span class="s1">&#39;recipient&#39;</span><span class="p">])</span>

    <span class="c1"># Filter the DataFrame so that there&#39;s only the given month</span>
    <span class="n">df_filtered</span> <span class="o">=</span> <span class="n">data</span><span class="p">[</span><span class="n">data</span><span class="p">[</span><span class="s1">&#39;month&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="n">month</span><span class="p">]</span>

    <span class="c1"># Add edges from filtered DataFrame</span>
    <span class="n">G</span><span class="o">.</span><span class="n">add_edges_from</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">df_filtered</span><span class="p">[</span><span class="s1">&#39;sender&#39;</span><span class="p">],</span> <span class="n">df_filtered</span><span class="p">[</span><span class="s1">&#39;recipient&#39;</span><span class="p">]))</span>

    <span class="c1"># Append G to the list of graphs</span>
    <span class="n">Gs</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>

<span class="k">print</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">Gs</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="graph-differences-over-time">graph differences over time<a class="anchor-link" href="#graph-differences-over-time">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Instantiate a list of graphs that show edges added: added</span>
<span class="n">added</span> <span class="o">=</span> <span class="p">[]</span>
<span class="c1"># Instantiate a list of graphs that show edges removed: removed</span>
<span class="n">removed</span> <span class="o">=</span> <span class="p">[]</span>
<span class="c1"># Here&#39;s the fractional change over time</span>
<span class="n">fractional_changes</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">window</span> <span class="o">=</span> <span class="mi">1</span>  
<span class="n">i</span> <span class="o">=</span> <span class="mi">0</span>      

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">Gs</span><span class="p">)</span> <span class="o">-</span> <span class="n">window</span><span class="p">):</span>
    <span class="n">g1</span> <span class="o">=</span> <span class="n">Gs</span><span class="p">[</span><span class="n">i</span><span class="p">]</span>
    <span class="n">g2</span> <span class="o">=</span> <span class="n">Gs</span><span class="p">[</span><span class="n">i</span> <span class="o">+</span> <span class="n">window</span><span class="p">]</span>

    <span class="c1"># Compute graph difference here</span>
    <span class="n">added</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">nx</span><span class="o">.</span><span class="n">difference</span><span class="p">(</span><span class="n">g2</span><span class="p">,</span> <span class="n">g1</span><span class="p">))</span>   
    <span class="n">removed</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">nx</span><span class="o">.</span><span class="n">difference</span><span class="p">(</span><span class="n">g1</span><span class="p">,</span> <span class="n">g2</span><span class="p">))</span>

    <span class="c1"># Compute change in graph size over time</span>
    <span class="n">fractional_changes</span><span class="o">.</span><span class="n">append</span><span class="p">((</span><span class="nb">len</span><span class="p">(</span><span class="n">g2</span><span class="o">.</span><span class="n">edges</span><span class="p">())</span> <span class="o">-</span> <span class="nb">len</span><span class="p">(</span><span class="n">g1</span><span class="o">.</span><span class="n">edges</span><span class="p">()))</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">g1</span><span class="o">.</span><span class="n">edges</span><span class="p">()))</span>

<span class="c1"># Print the fractional change</span>
<span class="k">print</span><span class="p">(</span><span class="n">fractional_changes</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="plot-number-of-edge-changes-over-time">plot number of edge changes over time<a class="anchor-link" href="#plot-number-of-edge-changes-over-time">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Import matplotlib</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>

<span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>
<span class="n">ax1</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">111</span><span class="p">)</span>

<span class="c1"># Plot the number of edges added over time</span>
<span class="n">edges_added</span> <span class="o">=</span> <span class="p">[</span><span class="nb">len</span><span class="p">(</span><span class="n">g</span><span class="o">.</span><span class="n">edges</span><span class="p">())</span> <span class="k">for</span> <span class="n">g</span> <span class="ow">in</span> <span class="n">added</span><span class="p">]</span>
<span class="n">plot1</span> <span class="o">=</span> <span class="n">ax1</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">edges_added</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">&#39;added&#39;</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;orange&#39;</span><span class="p">)</span>

<span class="c1"># Plot the number of edges removed over time</span>
<span class="n">edges_removed</span> <span class="o">=</span> <span class="p">[</span><span class="nb">len</span><span class="p">(</span><span class="n">g</span><span class="o">.</span><span class="n">edges</span><span class="p">())</span> <span class="k">for</span> <span class="n">g</span> <span class="ow">in</span> <span class="n">removed</span><span class="p">]</span>
<span class="n">plot2</span> <span class="o">=</span> <span class="n">ax1</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">edges_removed</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">&#39;removed&#39;</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;purple&#39;</span><span class="p">)</span>

<span class="c1"># Set yscale to logarithmic scale</span>
<span class="n">ax1</span><span class="o">.</span><span class="n">set_yscale</span><span class="p">(</span><span class="s1">&#39;log&#39;</span><span class="p">)</span>  
<span class="n">ax1</span><span class="o">.</span><span class="n">legend</span><span class="p">()</span>

<span class="c1"># 2nd axes shares x-axis with 1st axes object</span>
<span class="n">ax2</span> <span class="o">=</span> <span class="n">ax1</span><span class="o">.</span><span class="n">twinx</span><span class="p">()</span>

<span class="c1"># Plot the fractional changes over time</span>
<span class="n">plot3</span> <span class="o">=</span> <span class="n">ax2</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">fractional_changes</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">&#39;fractional change&#39;</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;green&#39;</span><span class="p">)</span>

<span class="c1"># Here, we create a single legend for both plots</span>
<span class="n">lines1</span><span class="p">,</span> <span class="n">labels1</span> <span class="o">=</span> <span class="n">ax1</span><span class="o">.</span><span class="n">get_legend_handles_labels</span><span class="p">()</span>
<span class="n">lines2</span><span class="p">,</span> <span class="n">labels2</span> <span class="o">=</span> <span class="n">ax2</span><span class="o">.</span><span class="n">get_legend_handles_labels</span><span class="p">()</span>
<span class="n">ax2</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">lines1</span> <span class="o">+</span> <span class="n">lines2</span><span class="p">,</span> <span class="n">labels1</span> <span class="o">+</span> <span class="n">labels2</span><span class="p">,</span> <span class="n">loc</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">axhline</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;green&#39;</span><span class="p">,</span> <span class="n">linestyle</span><span class="o">=</span><span class="s1">&#39;--&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/edge_changes_over_time.png" width=600></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="evolving-graph-statistics">evolving graph statistics<a class="anchor-link" href="#evolving-graph-statistics">&#182;</a></h3><p><strong>evolving graph statistics</strong>: graph summary stats, such as the number of nodes or edges, change over time (as in communication networks).  Degree (centrality &amp; betweenness) may also change over time.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="cumulative-distribution-of-changes-in-degree-centrality-over-time">cumulative distribution of changes in degree centrality over time<a class="anchor-link" href="#cumulative-distribution-of-changes-in-degree-centrality-over-time">&#182;</a></h2><p>Plotting the Empirical Cumulative Distribution Function ("ECDF") may be clearer than plotting with a histogram.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="number-of-edges-over-time">number of edges over time<a class="anchor-link" href="#number-of-edges-over-time">&#182;</a></h3><div class="highlight"><pre><span></span><span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>

<span class="c1"># Create a list of the number of edges per month</span>
<span class="n">edge_sizes</span> <span class="o">=</span> <span class="p">[</span><span class="nb">len</span><span class="p">(</span><span class="n">g</span><span class="o">.</span><span class="n">edges</span><span class="p">())</span> <span class="k">for</span> <span class="n">g</span> <span class="ow">in</span> <span class="n">Gs</span><span class="p">]</span>

<span class="c1"># Plot edge sizes over time</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">edge_sizes</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Time elapsed from first month (in months).&#39;</span><span class="p">)</span> 
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Number of edges&#39;</span><span class="p">)</span>                           
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/num_edges_over_time.png" width=600></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="degree-centrality-over-time">degree centrality over time<a class="anchor-link" href="#degree-centrality-over-time">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Create a list of degree centrality scores month-by-month</span>
<span class="n">cents</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">G</span> <span class="ow">in</span> <span class="n">Gs</span><span class="p">:</span>
    <span class="n">cent</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span>
    <span class="n">cents</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">cent</span><span class="p">)</span>


<span class="c1"># Plot ECDFs over time</span>
<span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">cents</span><span class="p">)):</span>
    <span class="n">x</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">ECDF</span><span class="p">(</span><span class="n">cents</span><span class="p">[</span><span class="n">i</span><span class="p">]</span><span class="o">.</span><span class="n">values</span><span class="p">())</span> 
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">&#39;Month {0}&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">i</span><span class="o">+</span><span class="mi">1</span><span class="p">))</span> 
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">()</span>   
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Summarizing evolving node statistics
how have purchasing patterns changed over time?
we've identified cust_1 as a node of interest ("NOI").  Now, we want to zoom in on that node and look at changes over time.</p>
<div class="highlight"><pre><span></span><span class="n">Gs</span> <span class="o">=</span> <span class="p">[</span><span class="o">...</span><span class="p">]</span>
<span class="n">noi</span> <span class="o">=</span> <span class="s1">&#39;customer1&#39;</span>
<span class="n">degs</span><span class="o">=</span><span class="p">[]</span>
<span class="k">for</span> <span class="n">g</span> <span class="ow">in</span> <span class="n">Gs</span><span class="p">:</span>
    <span class="c1"># get the degree of the node</span>
    <span class="n">degs</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">g</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">noi</span><span class="p">)))</span>

<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">degs</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="find-nodes-with-top-degree-centralities">find nodes with top degree centralities<a class="anchor-link" href="#find-nodes-with-top-degree-centralities">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Get the top 5 unique degree centrality scores: top_dcs</span>
<span class="n">top_dcs</span> <span class="o">=</span> <span class="nb">sorted</span><span class="p">(</span><span class="nb">set</span><span class="p">(</span><span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span><span class="o">.</span><span class="n">values</span><span class="p">()),</span> <span class="n">reverse</span><span class="o">=</span><span class="bp">True</span><span class="p">)[</span><span class="mi">0</span><span class="p">:</span><span class="mi">5</span><span class="p">]</span>

<span class="c1"># Create list of nodes that have the top 5 highest overall degree centralities</span>
<span class="n">top_connected</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">dc</span> <span class="ow">in</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">)</span><span class="o">.</span><span class="n">items</span><span class="p">():</span>
    <span class="k">if</span> <span class="n">dc</span> <span class="ow">in</span> <span class="n">top_dcs</span><span class="p">:</span>
        <span class="n">top_connected</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">n</span><span class="p">)</span>

<span class="c1"># Print the number of nodes that share the top 5 degree centrality scores</span>
<span class="k">print</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">top_connected</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="visualizing-connectivity">visualizing connectivity<a class="anchor-link" href="#visualizing-connectivity">&#182;</a></h3><p>'defaultdict' is the preferred option here, as a regular Python dictionary would throw a KeyError if you try to get an item with a key that is not currently in the dictionary.</p>
<h3 id="initializing-a-default-dict-of-lists">initializing a default dict of lists<a class="anchor-link" href="#initializing-a-default-dict-of-lists">&#182;</a></h3><p><code>d = defaultdict(list)</code></p>
<div class="highlight"><pre><span></span><span class="c1"># Import necessary modules</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="kn">from</span> <span class="nn">collections</span> <span class="kn">import</span> <span class="n">defaultdict</span>

<span class="c1"># Create a defaultdict in which the keys are nodes and the values are a list of connectivity scores over time</span>
<span class="n">connectivity</span> <span class="o">=</span> <span class="n">defaultdict</span><span class="p">(</span><span class="nb">list</span><span class="p">)</span>
<span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">top_connected</span><span class="p">:</span>
    <span class="k">for</span> <span class="n">g</span> <span class="ow">in</span> <span class="n">Gs</span><span class="p">:</span>
        <span class="n">connectivity</span><span class="p">[</span><span class="n">n</span><span class="p">]</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">g</span><span class="o">.</span><span class="n">neighbors</span><span class="p">(</span><span class="n">n</span><span class="p">)))</span>

<span class="c1"># Plot the connectivity for each node</span>
<span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span> 
<span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">conn</span> <span class="ow">in</span> <span class="n">connectivity</span><span class="o">.</span><span class="n">items</span><span class="p">():</span> 
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">conn</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="n">n</span><span class="p">)</span> 
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">()</span>  
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/connectivity.png" width=600></p>
<p><strong>ANSWER</strong>: Notice how there seems to be two distinct clusters of nodes that behave slightly differently: nodes 32, 9 and 41 are one group, and the nodes 400, 105, and 103 are the other. There may be something interesting to investigate going forward!</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Case-Study">Case Study<a class="anchor-link" href="#Case-Study">&#182;</a></h2><p>College forum postings over 6 months
Bipartite graph of students and foums.  Edge exists where a student posts to a forum.</p>
<p>Assume we have a DataFrame of edgelists - customers and products and the edges between them.</p>
<div class="highlight"><pre><span></span><span class="n">G</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">Graph</span><span class="p">()</span>

<span class="c1"># extract column labeled &#39;products&#39;, add nodes to graph with dictionary entry bipartite=&#39;products&#39;</span>
<span class="n">G</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">&#39;products&#39;</span><span class="p">],</span> <span class="n">bipartite</span><span class="o">=</span><span class="s1">&#39;products&#39;</span><span class="p">)</span>

<span class="c1"># extract column labeled &#39;customers&#39;, add nodes to graph with dictionary entry bipartite=&#39;customers&#39;</span>
<span class="n">G</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">&#39;customers&#39;</span><span class="p">]</span><span class="o">.</span> <span class="n">bipartite</span><span class="o">=</span><span class="s1">&#39;customers&#39;</span><span class="p">)</span>

<span class="c1"># nodes have been created, but no edges - use zip function to create edges</span>
<span class="n">G</span><span class="o">.</span><span class="n">add_edges_from</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">&#39;customers&#39;</span><span class="p">],</span> <span class="n">df</span><span class="p">[</span><span class="s1">&#39;products&#39;</span><span class="p">]))</span>

<span class="c1"># bipartite graph has been constructed in memory, now, we create the bipartite projections</span>
<span class="c1"># use list comprehension to create a container of nodes for each projection</span>
<span class="n">cust_nodes</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">()</span> <span class="k">if</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="n">bipartite</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;customers&#39;</span><span class="p">]</span>
<span class="n">prod_nodes</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">()</span> <span class="k">if</span> <span class="n">G</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="n">bipartite</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;products&#39;</span><span class="p">]</span>

<span class="n">prodG</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">projected_graph</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">nodes</span><span class="o">=</span><span class="n">prod_nodes</span><span class="p">)</span>
<span class="n">custG</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">projected_graph</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">nodes</span><span class="o">=</span><span class="n">cust_nodes</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="create-graph-from-a-DataFrame">create graph from a DataFrame<a class="anchor-link" href="#create-graph-from-a-DataFrame">&#182;</a></h3><div class="highlight"><pre><span></span><span class="kn">import</span> <span class="nn">networkx</span> <span class="kn">as</span> <span class="nn">nx</span>

<span class="c1"># Instantiate a new Graph: G</span>
<span class="n">G</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">Graph</span><span class="p">()</span>

<span class="c1"># Add nodes from each of the partitions</span>
<span class="n">G</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">(</span><span class="n">data</span><span class="p">[</span><span class="s1">&#39;student&#39;</span><span class="p">],</span> <span class="n">bipartite</span><span class="o">=</span><span class="s1">&#39;student&#39;</span><span class="p">)</span>
<span class="n">G</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">(</span><span class="n">data</span><span class="p">[</span><span class="s1">&#39;forum&#39;</span><span class="p">],</span> <span class="n">bipartite</span><span class="o">=</span><span class="s1">&#39;forum&#39;</span><span class="p">)</span>

<span class="c1"># Add in each edge along with the date the edge was created</span>
<span class="k">for</span> <span class="n">r</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">data</span><span class="o">.</span><span class="n">iterrows</span><span class="p">():</span>
    <span class="n">G</span><span class="o">.</span><span class="n">add_edge</span><span class="p">(</span><span class="n">d</span><span class="p">[</span><span class="s1">&#39;student&#39;</span><span class="p">],</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;forum&#39;</span><span class="p">],</span> <span class="n">date</span><span class="o">=</span><span class="n">d</span><span class="p">[</span><span class="s1">&#39;date&#39;</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="visualize-the-degree-centrality-distribution-of-the-students-projection">visualize the degree centrality distribution of the students projection<a class="anchor-link" href="#visualize-the-degree-centrality-distribution-of-the-students-projection">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Get the student partition&#39;s nodes: student_nodes</span>
<span class="n">student_nodes</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;student&#39;</span><span class="p">]</span>

<span class="c1"># Create the students nodes projection as a graph: G_students</span>
<span class="n">G_students</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">projected_graph</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">nodes</span><span class="o">=</span><span class="n">student_nodes</span><span class="p">)</span>

<span class="c1"># Calculate the degree centrality using nx.degree_centrality: dcs</span>
<span class="n">dcs</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G_students</span><span class="p">)</span>

<span class="c1"># Plot the histogram of degree centrality values</span>
<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">dcs</span><span class="o">.</span><span class="n">values</span><span class="p">()))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">yscale</span><span class="p">(</span><span class="s1">&#39;log&#39;</span><span class="p">)</span>  
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/deg_cent_students.png" width=600></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="visualize-the-degree-centrality-distirbution-of-the-forums-projection">visualize the degree centrality distirbution of the forums projection<a class="anchor-link" href="#visualize-the-degree-centrality-distirbution-of-the-forums-projection">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Get the forums partition&#39;s nodes: forum_nodes</span>
<span class="n">forum_nodes</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;bipartite&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="s1">&#39;forum&#39;</span><span class="p">]</span>

<span class="c1"># Create the forum nodes projection as a graph: G_forum</span>
<span class="n">G_forum</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">projected_graph</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">nodes</span><span class="o">=</span><span class="n">forum_nodes</span><span class="p">)</span>

<span class="c1"># Calculate the degree centrality using nx.degree_centrality: dcs</span>
<span class="n">dcs</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G_forum</span><span class="p">)</span>

<span class="c1"># Plot the histogram of degree centrality values</span>
<span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">dcs</span><span class="o">.</span><span class="n">values</span><span class="p">()))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">yscale</span><span class="p">(</span><span class="s1">&#39;log&#39;</span><span class="p">)</span> 
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/deg_cent_forums.png" width=600></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Time-based-Filtering">Time-based Filtering<a class="anchor-link" href="#Time-based-Filtering">&#182;</a></h2><h3 id="filtering-edges">filtering edges<a class="anchor-link" href="#filtering-edges">&#182;</a></h3><p>example:
10 salespeople 0-9
10 customers 10-19
each edge has a dictionary with an entry for 'sale_count' : 14, the number of sales made by a salesperson to that customer.</p>
<p>We want to filter only those relationships with sales_count &gt; 10</p>
<div class="highlight"><pre><span></span><span class="c1"># d is used in the condition, but not returned.  Only (u, v) is returned</span>
<span class="p">[(</span><span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">)</span> <span class="k">for</span> <span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;sale_count&#39;</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">10</span><span class="p">]</span>
</pre></div>
<h3 id="datetime">datetime<a class="anchor-link" href="#datetime">&#182;</a></h3><div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">datetime</span> <span class="kn">import</span> <span class="n">datetime</span><span class="p">,</span> <span class="n">timedelta</span>

<span class="n">year</span> <span class="o">=</span> <span class="mi">2011</span>
<span class="n">month</span> <span class="o">=</span> <span class="mi">11</span>
<span class="n">day1</span> <span class="o">=</span> <span class="mi">10</span>
<span class="n">day2</span> <span class="o">=</span> <span class="mi">6</span>

<span class="n">date1</span> <span class="o">=</span> <span class="n">datetime</span><span class="p">(</span><span class="n">year</span><span class="p">,</span> <span class="n">month</span><span class="p">,</span> <span class="n">day1</span><span class="p">)</span>
<span class="n">date2</span> <span class="o">=</span> <span class="n">datetime</span><span class="p">(</span><span class="n">year</span><span class="p">,</span> <span class="n">month</span><span class="p">,</span> <span class="n">day2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="time-filter-on-edges">time filter on edges<a class="anchor-link" href="#time-filter-on-edges">&#182;</a></h3><div class="highlight"><pre><span></span><span class="kn">import</span> <span class="nn">networkx</span> <span class="kn">as</span> <span class="nn">nx</span>
<span class="kn">from</span> <span class="nn">datetime</span> <span class="kn">import</span> <span class="n">datetime</span>

<span class="c1"># Instantiate a new graph: G_sub</span>
<span class="n">G_sub</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">Graph</span><span class="p">()</span>

<span class="c1"># Add nodes from the original graph</span>
<span class="n">G_sub</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">))</span>

<span class="c1"># Add edges using a list comprehension with one conditional on the edge dates, that the date of the edge is earlier than 2004-05-16.</span>
<span class="n">G_sub</span><span class="o">.</span><span class="n">add_edges_from</span><span class="p">([(</span><span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span><span class="p">)</span> <span class="k">for</span> <span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;date&#39;</span><span class="p">]</span> <span class="o">&lt;</span> <span class="n">datetime</span><span class="p">(</span><span class="mi">2004</span><span class="p">,</span><span class="mi">5</span><span class="p">,</span><span class="mi">16</span><span class="p">)])</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="visualize-filtered-graph-using-nxviz">visualize filtered graph using nxviz<a class="anchor-link" href="#visualize-filtered-graph-using-nxviz">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Compute degree centrality scores of each node</span>
<span class="n">dcs</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G</span><span class="p">,</span> <span class="n">nodes</span><span class="o">=</span><span class="n">forum_nodes</span><span class="p">)</span>
<span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G_sub</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">):</span>
    <span class="n">G_sub</span><span class="o">.</span><span class="n">node</span><span class="p">[</span><span class="n">n</span><span class="p">][</span><span class="s1">&#39;dc&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">dcs</span><span class="p">[</span><span class="n">n</span><span class="p">]</span>

<span class="c1"># Create the CircosPlot object: c</span>
<span class="n">c</span> <span class="o">=</span> <span class="n">CircosPlot</span><span class="p">(</span><span class="n">G_sub</span><span class="p">,</span> <span class="n">node_color</span><span class="o">=</span><span class="s1">&#39;bipartite&#39;</span><span class="p">,</span> <span class="n">node_grouping</span><span class="o">=</span><span class="s1">&#39;bipartite&#39;</span><span class="p">,</span> <span class="n">node_order</span><span class="o">=</span><span class="s1">&#39;dc&#39;</span><span class="p">)</span>

<span class="c1"># Draw c to screen</span>
<span class="n">c</span><span class="o">.</span><span class="n">draw</span><span class="p">()</span>

<span class="c1"># Display the plot</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/circosplot_dc.png" width=600></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Time-Series-Analysis">Time Series Analysis<a class="anchor-link" href="#Time-Series-Analysis">&#182;</a></h2><h3 id="datetime-math">datetime math<a class="anchor-link" href="#datetime-math">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[22]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">datetime</span> <span class="k">import</span> <span class="n">timedelta</span><span class="p">,</span> <span class="n">datetime</span>

<span class="n">day1</span> <span class="o">=</span> <span class="n">datetime</span><span class="p">(</span><span class="mi">2011</span><span class="p">,</span> <span class="mi">11</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">0</span><span class="p">)</span>
<span class="n">days</span><span class="o">=</span><span class="mi">4</span>
<span class="n">td</span> <span class="o">=</span> <span class="n">timedelta</span><span class="p">(</span><span class="n">days</span><span class="p">)</span>
<span class="n">day2</span> <span class="o">=</span> <span class="n">day1</span> <span class="o">+</span> <span class="n">td</span>

<span class="n">day1</span>
<span class="n">day2</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[22]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>datetime.datetime(2011, 11, 20, 0, 0)</pre>
</div>

</div>

<div class="output_area">

<div class="prompt output_prompt">Out[22]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>datetime.datetime(2011, 11, 24, 0, 0)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="plot-number-of-posts-being-made-over-time">plot number of posts being made over time<a class="anchor-link" href="#plot-number-of-posts-being-made-over-time">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Define current day and timedelta of 2 days</span>
<span class="n">curr_day</span> <span class="o">=</span> <span class="n">dayone</span>
<span class="n">td</span> <span class="o">=</span> <span class="n">timedelta</span><span class="p">(</span><span class="n">days</span><span class="o">=</span><span class="mi">2</span><span class="p">)</span>

<span class="c1"># Initialize an empty list of posts by day</span>
<span class="n">n_posts</span> <span class="o">=</span> <span class="p">[]</span>
<span class="k">while</span> <span class="n">curr_day</span> <span class="o">&lt;</span> <span class="n">lastday</span><span class="p">:</span>
    <span class="k">if</span> <span class="n">curr_day</span><span class="o">.</span><span class="n">day</span> <span class="o">==</span> <span class="mi">1</span><span class="p">:</span>
        <span class="k">print</span><span class="p">(</span><span class="n">curr_day</span><span class="p">)</span> 
    <span class="c1"># Filter edges such that they are within the sliding time window: edges</span>
    <span class="n">edges</span> <span class="o">=</span> <span class="p">[(</span><span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span><span class="p">)</span> <span class="k">for</span> <span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;date&#39;</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="n">curr_day</span> <span class="ow">and</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;date&#39;</span><span class="p">]</span> <span class="o">&lt;</span> <span class="n">curr_day</span> <span class="o">+</span> <span class="n">td</span><span class="p">]</span>

    <span class="c1"># Append number of edges to the n_posts list</span>
    <span class="n">n_posts</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">edges</span><span class="p">))</span>

    <span class="c1"># Increment the curr_day by the time delta</span>
    <span class="n">curr_day</span> <span class="o">+=</span> <span class="n">td</span>

<span class="c1"># Create the plot</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">n_posts</span><span class="p">)</span>  
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Days elapsed&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Number of posts&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/posts_over_time.png" width=600></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="extract-mean-deg_cent-day-by-day-on-the-students-partition">extract mean deg_cent day-by-day on the students partition<a class="anchor-link" href="#extract-mean-deg_cent-day-by-day-on-the-students-partition">&#182;</a></h3><div class="highlight"><pre><span></span><span class="kn">from</span> <span class="nn">datetime</span> <span class="kn">import</span> <span class="n">datetime</span><span class="p">,</span> <span class="n">timedelta</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">networkx</span> <span class="kn">as</span> <span class="nn">nx</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>

<span class="c1"># Initialize a new list: mean_dcs</span>
<span class="n">mean_dcs</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">curr_day</span> <span class="o">=</span> <span class="n">dayone</span>
<span class="n">td</span> <span class="o">=</span> <span class="n">timedelta</span><span class="p">(</span><span class="n">days</span><span class="o">=</span><span class="mi">2</span><span class="p">)</span>

<span class="k">while</span> <span class="n">curr_day</span> <span class="o">&lt;</span> <span class="n">lastday</span><span class="p">:</span>
    <span class="k">if</span> <span class="n">curr_day</span><span class="o">.</span><span class="n">day</span> <span class="o">==</span> <span class="mi">1</span><span class="p">:</span>
        <span class="k">print</span><span class="p">(</span><span class="n">curr_day</span><span class="p">)</span>  
    <span class="c1"># Instantiate a new graph containing a subset of edges: G_sub</span>
    <span class="n">G_sub</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">Graph</span><span class="p">()</span>
    <span class="c1"># Add nodes from G</span>
    <span class="n">G_sub</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">))</span>
    <span class="c1"># Add in edges that fulfill the criteria</span>
    <span class="n">G_sub</span><span class="o">.</span><span class="n">add_edges_from</span><span class="p">([(</span><span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span><span class="p">)</span> <span class="k">for</span> <span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;date&#39;</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="n">curr_day</span> <span class="ow">and</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;date&#39;</span><span class="p">]</span> <span class="o">&lt;</span> <span class="n">curr_day</span> <span class="o">+</span> <span class="n">td</span><span class="p">])</span>

    <span class="c1"># Get the students projection</span>
    <span class="n">G_student_sub</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">projected_graph</span><span class="p">(</span><span class="n">G_sub</span><span class="p">,</span> <span class="n">nodes</span><span class="o">=</span><span class="n">student_nodes</span><span class="p">)</span>
    <span class="c1"># Compute the degree centrality of the students projection</span>
    <span class="n">dc</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G_student_sub</span><span class="p">)</span>
    <span class="c1"># Append mean degree centrality to the list mean_dcs</span>
    <span class="n">mean_dcs</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">dc</span><span class="o">.</span><span class="n">values</span><span class="p">())))</span>
    <span class="c1"># Increment the time</span>
    <span class="n">curr_day</span> <span class="o">+=</span> <span class="n">td</span>

<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">mean_dcs</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Time elapsed&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Degree centrality.&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/deg_cent_over_time.png" width=600></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="dictionary-comprehension">dictionary comprehension<a class="anchor-link" href="#dictionary-comprehension">&#182;</a></h3><p>format: {key: val for key, val in dict.items() if ...}</p>
<h3 id="find-the-most-popular-forums-by-day">find the most popular forums by day<a class="anchor-link" href="#find-the-most-popular-forums-by-day">&#182;</a></h3><div class="highlight"><pre><span></span><span class="c1"># Import necessary modules</span>
<span class="kn">from</span> <span class="nn">datetime</span> <span class="kn">import</span> <span class="n">timedelta</span>
<span class="kn">import</span> <span class="nn">networkx</span> <span class="kn">as</span> <span class="nn">nx</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>

<span class="c1"># Instantiate a list to hold the list of most popular forums by day: most_popular_forums</span>
<span class="n">most_popular_forums</span> <span class="o">=</span> <span class="p">[]</span>
<span class="c1"># Instantiate a list to hold the degree centrality scores of the most popular forums: highest_dcs</span>
<span class="n">highest_dcs</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">curr_day</span> <span class="o">=</span> <span class="n">dayone</span>  
<span class="n">td</span> <span class="o">=</span> <span class="n">timedelta</span><span class="p">(</span><span class="n">days</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>  

<span class="k">while</span> <span class="n">curr_day</span> <span class="o">&lt;</span> <span class="n">lastday</span><span class="p">:</span>  
    <span class="k">if</span> <span class="n">curr_day</span><span class="o">.</span><span class="n">day</span> <span class="o">==</span> <span class="mi">1</span><span class="p">:</span> 
        <span class="k">print</span><span class="p">(</span><span class="n">curr_day</span><span class="p">)</span> 
    <span class="c1"># Instantiate new graph: G_sub</span>
    <span class="n">G_sub</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">Graph</span><span class="p">()</span>

    <span class="c1"># Add in nodes from original graph G</span>
    <span class="n">G_sub</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">))</span>

    <span class="c1"># Add in edges from the original graph G that fulfill the criteria</span>
    <span class="n">G_sub</span><span class="o">.</span><span class="n">add_edges_from</span><span class="p">([(</span><span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span><span class="p">)</span> <span class="k">for</span> <span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;date&#39;</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="n">curr_day</span> <span class="ow">and</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;date&#39;</span><span class="p">]</span> <span class="o">&lt;</span> <span class="n">curr_day</span> <span class="o">+</span> <span class="n">td</span><span class="p">])</span>

    <span class="c1"># CODE CONTINUES ON NEXT EXERCISE</span>
    <span class="n">curr_day</span> <span class="o">+=</span> <span class="n">td</span>
</pre></div>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="part-2">part 2<a class="anchor-link" href="#part-2">&#182;</a></h3><p>Continued from cell above.</p>
<div class="highlight"><pre><span></span><span class="c1"># Import necessary modules</span>
<span class="kn">from</span> <span class="nn">datetime</span> <span class="kn">import</span> <span class="n">timedelta</span>
<span class="kn">import</span> <span class="nn">networkx</span> <span class="kn">as</span> <span class="nn">nx</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>

<span class="n">most_popular_forums</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">highest_dcs</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">curr_day</span> <span class="o">=</span> <span class="n">dayone</span> 
<span class="n">td</span> <span class="o">=</span> <span class="n">timedelta</span><span class="p">(</span><span class="n">days</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>  

<span class="k">while</span> <span class="n">curr_day</span> <span class="o">&lt;</span> <span class="n">lastday</span><span class="p">:</span>  
    <span class="k">if</span> <span class="n">curr_day</span><span class="o">.</span><span class="n">day</span> <span class="o">==</span> <span class="mi">1</span><span class="p">:</span>  
        <span class="k">print</span><span class="p">(</span><span class="n">curr_day</span><span class="p">)</span>  
    <span class="n">G_sub</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">Graph</span><span class="p">()</span>
    <span class="n">G_sub</span><span class="o">.</span><span class="n">add_nodes_from</span><span class="p">(</span><span class="n">G</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">))</span>   
    <span class="n">G_sub</span><span class="o">.</span><span class="n">add_edges_from</span><span class="p">([(</span><span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span><span class="p">)</span> <span class="k">for</span> <span class="n">u</span><span class="p">,</span> <span class="n">v</span><span class="p">,</span> <span class="n">d</span> <span class="ow">in</span> <span class="n">G</span><span class="o">.</span><span class="n">edges</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span> <span class="k">if</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;date&#39;</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="n">curr_day</span> <span class="ow">and</span> <span class="n">d</span><span class="p">[</span><span class="s1">&#39;date&#39;</span><span class="p">]</span> <span class="o">&lt;</span> <span class="n">curr_day</span> <span class="o">+</span> <span class="n">td</span><span class="p">])</span>

    <span class="c1"># Get the degree centrality </span>
    <span class="n">dc</span> <span class="o">=</span> <span class="n">nx</span><span class="o">.</span><span class="n">bipartite</span><span class="o">.</span><span class="n">degree_centrality</span><span class="p">(</span><span class="n">G_sub</span><span class="p">,</span> <span class="n">forum_nodes</span><span class="p">)</span>
    <span class="c1"># Filter the dictionary such that there&#39;s only forum degree centralities</span>
    <span class="n">forum_dcs</span> <span class="o">=</span> <span class="p">{</span><span class="n">n</span><span class="p">:</span><span class="n">dc</span> <span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">dc</span> <span class="ow">in</span> <span class="n">dc</span><span class="o">.</span><span class="n">items</span><span class="p">()</span> <span class="k">if</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">forum_nodes</span><span class="p">}</span>
    <span class="c1"># Identify the most popular forum(s) </span>
    <span class="n">most_popular_forum</span> <span class="o">=</span> <span class="p">[</span><span class="n">n</span> <span class="k">for</span> <span class="n">n</span><span class="p">,</span> <span class="n">dc</span> <span class="ow">in</span> <span class="n">forum_dcs</span><span class="o">.</span><span class="n">items</span><span class="p">()</span> <span class="k">if</span> <span class="n">dc</span> <span class="o">==</span> <span class="nb">max</span><span class="p">(</span><span class="n">forum_dcs</span><span class="o">.</span><span class="n">values</span><span class="p">())</span> <span class="ow">and</span> <span class="n">dc</span> <span class="o">!=</span> <span class="mi">0</span><span class="p">]</span> 
    <span class="n">most_popular_forums</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">most_popular_forum</span><span class="p">)</span> 
    <span class="c1"># Store the highest dc values in highest_dcs</span>
    <span class="n">highest_dcs</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="nb">max</span><span class="p">(</span><span class="n">forum_dcs</span><span class="o">.</span><span class="n">values</span><span class="p">()))</span>

    <span class="n">curr_day</span> <span class="o">+=</span> <span class="n">td</span>  

<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span> 
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">([</span><span class="nb">len</span><span class="p">(</span><span class="n">forums</span><span class="p">)</span> <span class="k">for</span> <span class="n">forums</span> <span class="ow">in</span> <span class="n">most_popular_forums</span><span class="p">],</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;blue&#39;</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">&#39;Forums&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Number of Most Popular Forums&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">highest_dcs</span><span class="p">,</span> <span class="n">color</span><span class="o">=</span><span class="s1">&#39;orange&#39;</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s1">&#39;DC Score&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Top Degree Centrality Score&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
<p><img src="images/most_pop_forums.png" width=600></p>
<p><img src="images/top_dcs.png" width=600></p>

</div>
</div>
</div>
 

