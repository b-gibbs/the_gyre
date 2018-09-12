--- 
title: Relax - Instructions
layout: code 
permalink: /coursework/takehomes/relax_instructions
excerpt: "" 
section: "/coursework/takehomes/relax/" 
---

<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The data is available as two attached CSV files:</p>
<ul>
<li>takehome_user_engagement.csv</li>
<li>takehome_users.csv</li>
</ul>
<p>The data has the following two tables:</p>
<ol>
<li>A user table ("takehome_users") with data on 12,000 users who signed up for the product in the last two years. This table includes:<ul>
<li>name: the user's name</li>
<li>object_id: the user's id</li>
<li>email: email address</li>
<li>creation_source: how their account was created. This takes on one of 5 values:<ul>
<li>PERSONAL_PROJECTS: invited to join another user's personal workspace</li>
<li>GUEST_INVITE: invited to an organization as a guest (limited permissions)</li>
<li>ORG_INVITE: invited to an organization (as a full member)</li>
<li>SIGNUP: signed up via the website</li>
<li>SIGNUP_GOOGLE_AUTH: signed up using Google Authentication (using a Google email account for their login id)</li>
</ul>
</li>
<li>creation_time: when they created their account</li>
<li>last_session_creation_time: unix timestamp of last login</li>
<li>opted_in_to_mailing_list: whether they have opted into receiving marketing emails</li>
<li>enabled_for_marketing_drip: whether they are on the regular marketing email drip</li>
<li>org_id: the organization (group of users) they belong to</li>
<li>invited_by_user_id: which user invited them to join (if applicable).</li>
</ul>
</li>
<li>A usage summary table ("takehome_user_engagement") that has a row for each day that a user logged into the product.</li>
</ol>
<p>Defining an "adopted user" as a user who has logged into the product on three separate days in at least one seven­day period, identify which factors predict future user adoption.
We suggest spending 1­2 hours on this, but you're welcome to spend more or less. Please send us a brief writeup of your findings (the more concise, the better ­­ no more than one page), along with any summary tables, graphs, code, or queries that can help us understand your approach. Please note any factors you considered or investigation you did, even if they did not pan out. Feel free to identify any further research or data you think would be valuable.</p>

</div>
</div>
</div>
 

