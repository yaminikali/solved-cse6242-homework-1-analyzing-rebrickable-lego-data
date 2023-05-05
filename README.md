Download Link: https://assignmentchef.com/product/solved-cse6242-homework-1-analyzing-rebrickable-lego-data
<br>
In Questions 1, 2, and 3, you will perform data collection, exploration, and visualization of the extensive LEGO database available from <a href="https://www.google.com/url?q=https://rebrickable.com/&amp;sa=D&amp;ust=1574830317684000">‘Rebrickable</a>’.  In the following tasks, you will build both current and historical domain knowledge about LEGO themes, sets, and parts.

In Q1, we focus on collecting data using an API and then building a graph that shows the relationships between Sets and Parts.  From this we can gain insights into what LEGO part is used the most frequently throughout various LEGO sets.

In Q2, you will work directly with the data files to build a portion of the Rebrickable database locally using SQLite.  Next, you will explore the hierarchy of LEGO themes / sub-themes, as well as the historical growth of LEGO sets over time.

In Q3, you will visualize the growth of LEGO sets through the years.  This will serve as an introduction to D3.

Q4 focuses on cleaning and preparing data for visualization.

<h1>Q1 [40 points] Collecting and visualizing Rebrickable Lego data</h1>

<h2>Q1.1 Collecting Rebrickable Lego Data</h2>

You will use the “Rebrickable” API version 3 to: (1) download data about the Lego sets and (2) for each set, download the parts that comprise it.

You will write code using Python 3.7.x in <strong>script.py </strong>in this question.  You will need an API key to use the Rebrickable data.  Your API key will be an input to <strong>script.py </strong>so that we can run your code with our own API key to check the results.  Running the following command should generate a<strong> .gexf </strong>graph file specified in Q1.1.d.

<strong>python3 script.py &lt;API_KEY&gt;</strong>

Please refer to <a href="https://www.google.com/url?q=https://www.tutorialspoint.com/python3/python_command_line_arguments.htm&amp;sa=D&amp;ust=1574830317687000">this tutorial</a> to learn how to parse command line arguments. <strong>DO NOT</strong> leave your API key written in the code. In general, it is good practice to not store any sensitive information like API keys and passwords as part of your code.

<strong>Note:</strong> You may only use the modules and libraries provided at the top the<strong> script.py</strong> file included in the skeleton for Q1 and modules from the <a href="https://www.google.com/url?q=https://docs.python.org/3/library/&amp;sa=D&amp;ust=1574830317688000">Python Standard Library</a>.  A module for creating a <strong>.gex</strong>f graph file is included in the skeleton and also imported at the top of the <strong>script.py</strong> file.  <a href="https://www.google.com/url?q=https://pandas.pydata.org&amp;sa=D&amp;ust=1574830317688000">Pandas</a> and <a href="https://www.google.com/url?q=https://numpy.org&amp;sa=D&amp;ust=1574830317689000">Numpy</a> <strong>CANNOT</strong> be used — while we understand that they are useful libraries to learn, completing this question is not critically dependent on their functionality. In addition, to make grading more manageable and to enable our TAs to provide better, more consistent support to our students, we have decided to restrict the libraries accordingly.

How to use the Rebrickable API

○ Create a Rebrickable account and generate an API Key.  Refer to <a href="https://www.google.com/url?q=https://docs.google.com/document/d/e/2PACX-1vQkaZGXI6lvWDzrnuIRHv6SPrIxFiL_Y4-T0YZQlKnMGzlHOwcGt-LZqQoB-to6PxpDy0ZSr7GWzdUY/pub&amp;sa=D&amp;ust=1574830317689000">this</a> document for detailed instructions.

○ Refer to the API documentation at <a href="https://www.google.com/url?q=https://rebrickable.com/api/&amp;sa=D&amp;ust=1574830317690000">https://rebrickable.com/api/</a> as you work on this question.  Within the documentation you will find a helpful ‘try-it-out’ feature for interacting with the API calls.

<strong>Note</strong>: The API allows you to make <strong>1 request every second</strong>. Set appropriate timeout intervals in your code while making requests. We recommend you think about  how much time your script will run for when solving this question, so you will complete it on time.  You may be penalized for a runtime exceeding 10 minutes. When we grade, we will take into account what your code does, and aspects that may be out of your control. For example, sometimes the Rebrickable server may be under heavy load, which may significantly increase the response time (e.g., the closer it is to HW1 deadline, likely the longer the response time!).

<ol>

 <li>[10 points] Using the Rebrickable API, retrieve the top LEGO sets that have the most parts. Since this is a live database, the results may vary as you implement your solution.  Adjust the parameters of the API calls such that you retrieve at least 270 and no more than 300 sets. The sets should be ordered by the number of parts they contain.  For each set, you will need its:</li>

</ol>

<ul>

 <li>set number</li>

 <li>set name</li>

</ul>

<strong>Hints:</strong>

<ul>

 <li>Sorting on number of parts can be accomplished in the API call</li>

 <li>Adjust the min_parts parameter</li>

 <li>Set the page_size to be larger than the expected number of results to avoid pagination issues</li>

</ul>

Complete the following functions (necessary for us to grade your work).

<ul>

 <li><strong>min_parts()</strong> in <strong>py</strong></li>

</ul>

<h3>● lego_sets() in script.py</h3>

<ol>

 <li>[5 points] Retrieving Parts for Lego Sets. For each set returned in part a, use the API to get a list of all inventory parts in that set.  Since we are only interested in the parts that are used most frequently in a set, attempt to retrieve up to but no more than the top 20 parts for each set.   For each part, you will need its:

  <ul>

   <li>part color</li>

   <li>part quantity ● part name</li>

   <li>part number</li>

  </ul></li>

</ol>

To address the fact that some parts for a set have the same part_num, construct a unique id by concatenating the part number and color.  e.g.,  A part having a part_num = “3203” and a color “C9C9C9” would be concatenated into an id = “3203_C9C9C9”.  You will use this part id as the node id when you add it to the graph in part c.

<strong>Note</strong>: Not all sets have 20 different parts.  It is allowable to have fewer than 20 parts for a set.

<strong>Hint:</strong> Set the page_size parameter = 1000 when retrieving parts to avoid pagination issues.

<ol>

 <li>[10 points] Constructing a graph using the <strong>pygexf</strong> library (included in skeleton under Q1→ gexf/) . Use the <strong>pygexf</strong> module to construct a graph that can be imported into the Gephi Open Graph Viz Platform software.  You can review details about the .<strong>gexf</strong> file format <a href="https://www.google.com/url?q=https://github.com/gephi/gexf/wiki/Basic-Concepts&amp;sa=D&amp;ust=1574830317697000">here</a><a href="https://www.google.com/url?q=https://github.com/gephi/gexf/wiki/Basic-Concepts&amp;sa=D&amp;ust=1574830317697000">.</a>  You may also review a <a href="https://www.google.com/url?q=https://github.com/paulgirard/pygexf/blob/master/test/test.py&amp;sa=D&amp;ust=1574830317697000">simple</a> and a more <a href="https://www.google.com/url?q=https://github.com/paulgirard/pygexf/blob/master/test/gexf.net.dynamics_openintervals.gexf&amp;sa=D&amp;ust=1574830317697000">complex</a> graph created using the module.  Instantiate and construct a static, undirected graph as follows:</li>

</ol>

<strong>Note:</strong> script.py includes an import statement for the pygexf library.

<ol>

 <li>Declare a string-valued node attribute titled ‘Type’. Add this attribute to each node in the graph.  You will use node attributes to perform partitioning operations within Gephi.</li>

</ol>

○ For nodes representing a [Lego] <strong>set, </strong>set the attribute value = “set”

○ For nodes representing a [Lego] <strong>part, </strong>set the attribute value = “part”

<ul>

 <li>Each <strong>set</strong> should be added as a node to the graph

  <ul>

   <li>node id = set number retrieved in part a</li>

  </ul></li>

</ul>

○ node label = set name retrieved in part a

○ node color is set using RGB values of ‘0’, ‘0’, ‘0’

<ul>

 <li>Each <strong>part</strong> should be added as a node to the graph

  <ul>

   <li>node id = the part id you made by concatenating the part number and color in part b ○ node label = part name retrieved in part b</li>

  </ul></li>

</ul>

○ node color is set using the part color retrieved in part b.  RGB values must be converted from the original hexadecimal representation in the data.

<ul>

 <li>Add an edge between each <strong>part</strong> and the <strong>set</strong>(s) it belongs to.

  <ul>

   <li>edge id = construct a unique id of your choosing.</li>

  </ul></li>

</ul>

○ edge source = set number retrieved in part a

○ edge target =  the unique part id you constructed from the part number and color.

retrieved in part b

○ edge weight = part quantity retrieved in part b

<strong>Note</strong>: Ensure that you do not add the same node more than once to the graph.  <strong>pygexf</strong> has some functions that you can use to check this.

Use <strong>pygexf’s</strong> .write() command to output a file named <strong>bricks_graph.gexf</strong>

Complete the following function (necessary for us to grade your work).

<ul>

 <li><strong>gexf_graph()</strong> in <strong>py</strong></li>

</ul>

<strong>Note :</strong> Q1.2 builds on the results of Q1.1

<h2>Q1.2  Visualizing a Lego Sets and Parts Graph</h2>

<a href="https://www.google.com/url?q=http://gephi.org&amp;sa=D&amp;ust=1574830317702000">Using Gephi version 0.9.2, visualize the network of the Lego sets and their most used-parts. You can </a><a href="https://www.google.com/url?q=http://gephi.org&amp;sa=D&amp;ust=1574830317702000">download Gephi here</a><a href="https://www.google.com/url?q=http://gephi.org&amp;sa=D&amp;ust=1574830317702000">. Ensure your system fulfills all </a><a href="https://www.google.com/url?q=https://gephi.org/users/requirements/&amp;sa=D&amp;ust=1574830317703000">requirements</a><a href="https://www.google.com/url?q=http://gephi.org&amp;sa=D&amp;ust=1574830317702000"> for running Gephi.</a>

<ol>

 <li>Go through the <a href="https://www.google.com/url?q=https://gephi.org/users/quick-start/&amp;sa=D&amp;ust=1574830317703000">Gephi quick-start guide</a><a href="https://www.google.com/url?q=https://gephi.org/users/quick-start/&amp;sa=D&amp;ust=1574830317703000">.</a></li>

 <li>[2 points] Start Gephi and then use File→ Open to open <strong>gexf. </strong>Within the import report dialogue window, ensure the graph type is set to ‘undirected’. Under ‘more options…’, ensure that these boxes are checked:

  <ul>

   <li>‘Auto-Scale’</li>

   <li>‘Create missing nodes’</li>

   <li>‘Self-loops’</li>

   <li>Leave the Edges merge strategy selected to ‘Sum’. Ignore the GEXF version 1.2 deprecation warning.</li>

  </ul></li>

 <li>[8 points] Using the following guidelines, create a visually meaningful graph:

  <ul>

   <li>Keep edge crossing to a minimum, and avoid as much node overlap as possible.</li>

   <li>Keep the graph compact and symmetric if possible.</li>

   <li>Whenever possible, show node labels. If showing all node labels create too much visual complexity, try showing those for the “important” nodes. We recommend that you first run Gephi’s built-in stat functions to gain more insight about a given node.</li>

   <li>Using nodes’ spatial positions to convey information (e.g., “clusters” or groups).</li>

  </ul></li>

</ol>

Experiment with Gephi’s features, such as graph layouts, changing node size and label color, edge thickness, etc. The objective of this task is to familiarize yourself with Gephi; therefore this is a fairly open-ended task. It is not possible to create a “perfect” visualization for most graph datasets. The above guidelines are ones that generally help. However, like most design tasks, creating a visualization is about making selective design compromises. Some guidelines could create competing demands, and following all guidelines may not guarantee a “perfect” design.

<strong>Hint:</strong>

Install more Layout plugins/algorithms through Tools → Plugins → Available Plugins.  Check and install plugins in the ‘Layout’ category.

<ol>

 <li>[5 points] Using Gephi’s built-in functions, compute the following metrics for your graph:

  <ul>

   <li>Average node degree (run the function called “Average Degree”)</li>

   <li>Diameter of the graph (run the function called “Network Diameter”)</li>

   <li>Average path length (run the function called “Avg. Path Length”)</li>

  </ul></li>

</ol>

You will learn about these metrics in the “graphs” lectures.

Complete the following functions for auto-grading purposes.

<ul>

 <li><strong>avg_node_degree()</strong> in <strong>py</strong></li>

 <li><strong>graph_diameter()</strong> in <strong>py</strong></li>

 <li><strong>avg_path_length()</strong> in <strong>py</strong></li>

</ul>

<strong>      Deliverables:</strong> Place all the files listed below in the <strong>Q1</strong> folder.

<ul>

 <li><strong>py: </strong>The <strong>Python 3.7</strong> script you write that generates <strong>bricks_graph.gexf</strong> contains the</li>

</ul>

6 completed functions described in Q1.1.b, Q1.1.d, and Q1.2.d

<ul>

 <li><strong>gexf: </strong>The Gephi graph file output from <strong>script.py </strong>from Q1.1.d.</li>

 <li>an image file named “<strong>png</strong>” (or “<strong>graph.svg</strong>”) containing your visualization created in Gephi for Q1.2.c.</li>

 <li>Do not include the pygexf/ We will supply our own copy of this library during grading.</li>

</ul>

<h2><strong>Q2</strong> SQLite</h2>

<a href="https://www.google.com/url?q=http://www.sqlite.org/&amp;sa=D&amp;ust=1574830317711000">SQLite</a> is a lightweight, serverless, embedded database that can easily handle multiple gigabytes of data. It is one of the world’s most popular embedded database systems. It is convenient to share data stored in an SQLite database — just one cross-platform file which doesn’t need to be parsed explicitly (unlike CSV files, which have to be loaded and parsed).

You will modify the given <strong>Q2.SQL.txt</strong> file by adding SQL statements and SQLite commands to it.

<table width="681">

 <tbody>

  <tr>

   <td width="681">We will autograde your solution by running the following command that generates <strong>Q2.db</strong> and <strong>Q2.OUT.txt</strong> (assuming the current directory contains the data files). $ sqlite3 Q2.db &lt; Q2.SQL.txt &gt; Q2.OUT.txtSince no auto-grader is perfect, we ask that you be mindful of all the important points and notes below, which can cause the auto-grader to return an error.  Our goal is to efficiently grade your assignment and return it as quickly as we can, so you can receive feedback and learn from the experience that you’ll gain in this course.–     You will <strong>not receive any points</strong> if we are unable to generate the two output files above.–     You will <strong>lose points</strong> if you do not strictly follow the output format specified in each question below. The output format corresponds to the headers/column names for your SQL command output.We have added some lines of code to the <strong>Q2.SQL.txt</strong> file for autograding purposes. <strong>DO NOT</strong><strong>REMOVE/MODIFY THESE LINES.</strong> You will <strong>not receive any points</strong> if these statements are modified</td>

  </tr>

  <tr>

   <td width="681">in any way (our autograder will check for changes). There are clearly marked regions in the <strong>Q2.SQL.txt</strong> file where you should add your code.Examples of modifying the autograder code that can cause you to lose points:–               Putting any code or text of any kind, intentionally or unintentionally, outside the designated regions.–               Modifying, updating, or removing the provided statements / instructions / text in any way. – Leaving in unnecessary debug/print statements in your submission. You may desire to print out more output than required during your development and debugging, but make sure to remove all extra code and text before submission.Regrettably, we will not be releasing the auto-grader for your testing since that will likely invite unwanted attempts to game it. However, we have provided you with <strong>Q2.OUT.SAMPLE.txt</strong> with sample data that gives an example of how your final <strong>Q2.OUT.txt </strong>should look like after running the above command. Note that the sample data should not be submitted or relied upon for any purpose other than output reference and format checking.  Avoid printing unnecessary output in your final submission as it will affect autograding and you will <strong>lose points</strong>.</td>

  </tr>

 </tbody>

</table>

<strong>WARNING: </strong><u>Do not copy and paste</u> any code/command from this document for use in the sqlite command prompt, because the document rendering sometimes introduce hidden/special characters, causing SQL error. This might cause the autograder to fail and you will lose points if such a case. You should manually type out the commands instead.

<strong>NOTE: </strong>For the questions in this section, you must only use <a href="https://www.google.com/url?q=https://www.w3schools.com/sql/sql_join_inner.asp&amp;sa=D&amp;ust=1574830317722000">INNER JOIN</a> when performing a join between two tables. Other types of joins may result in incorrect results.

<strong>NOTE: </strong>Do not use .mode csv in your Q2.SQL.txt file.  This will cause quotes to be printed in the output of each SELECT … ; statement.

<ol>

 <li>[4 points]<em>Create tables and import data</em>.</li>

 <li>[2 points] Create three tables named:</li>

</ol>

○ sets

○ themes ○ parts

with columns having the indicated data types:

<ul>

 <li>sets</li>

</ul>

○ set_num (text)

○ name (text)

○ year (integer)

○ theme_id (integer)

○ num_parts (integer)

<ul>

 <li>themes</li>

</ul>

○ id (integer)

○ name (text)

○ parent_id (integer) ● parts

○ part_num (text)

○ name (text)

○ part_cat_id (integer)

○ part_material_id (integer)

<ol>

 <li>[2 points] Import the provided files as follows:</li>

</ol>

○ <strong> sets.csv</strong> file into the sets table

○ <strong> themes.csv</strong> file into the themes table

○ <strong> parts.csv</strong> file into the parts table

Use SQLite’s .import command for this. Only use relative paths, e.g.,

data/&lt;file&gt;.csv while importing files since absolute/local paths are specific locations that exist only on your computer and will cause the autograder to fail..

<ol>

 <li>[3 points] <em>Create indexes.</em> Create the following indexes for the tables specified below. This step increases the speed of subsequent operations; though the improvement in speed may be negligible for this small database, it is significant for larger databases.</li>

</ol>

○ sets_index for the set_num column in sets table

○ parts_index for the part_num column in parts table ○ themes_index for the id column in themes table

<ol>

 <li>[4 points] Required domain knowledge: LEGO sets belong to either a top level theme, e.g.,  ‘Castle’,‘Town’, ‘Space’ or a theme → sub-theme hierarchy, e.g.,Town → Classic Town, Town → Outback, Town → Race.

  <ol>

   <li>[2 points] <a href="https://www.google.com/url?q=https://sqlite.org/lang_createview.html&amp;sa=D&amp;ust=1574830317733000">Create a view</a> (<a href="https://www.google.com/url?q=https://www.w3schools.com/sql/sql_view.asp&amp;sa=D&amp;ust=1574830317733000">virtual table</a>) called top_level_themes that contains only the top level themes. This view must contain the id and name of any theme in the themes table that does not have a parent theme. You can check this condition by querying where the parent_id  =</li>

  </ol></li>

</ol>

‘’

<strong>NOTE: </strong>the view you create here must <strong>NOT</strong> be a ‘TEMP’ view, nor a ‘TEMPORARY’ view.

<strong>Optional Reading:</strong> <a href="https://www.google.com/url?q=http://stackoverflow.com/questions/1278521/why-do-you-create-a-view-in-a-database&amp;sa=D&amp;ust=1574830317734000">Why create views?</a>




<ol>

 <li>[2 points] After creating the view, write a query that shows the total number of top level themes as count in the view you created.</li>

</ol>

Output format and sample value:

count

57




<ol>

 <li>[4 points] <em>Finding top level themes with the most sets. </em>Using the top_level_themes view that you created in part c.i, find the 10 top level themes that have the greatest number of sets (no need to consider a top level theme’s child themes).  Sort the output descending order from highest to lowest.</li>

</ol>

Output format and sample value:                 theme,num_sets

Space,777

Town,755                 Castle,333                 …

<ol>

 <li>[7 points] <em>Calculate a percentage</em>. Continue exploring top level themes using the</li>

</ol>

top_level_themes view and the sets table. Write a query that expresses the number of sets from above as a percentage of the total number of sets that belong only to top level themes.  The total number of sets would be the sum of <u>all</u> (not limited to top 10)  num_sets from the part d.

List the themes and percentages, limiting the output only to themes with a percentage &gt;= 5.00.  Format all decimal values to 2 decimal places.

Output format and sample value: theme,percentage

Space,10.30

Town,7.33

Castle,5.00 …

<strong>Hint:</strong>

You can format your decimal output using printf()as mentioned here: <a href="https://www.google.com/url?q=https://stackoverflow.com/questions/9149063/sqlite-format-number-with-2-decimal-places-always&amp;sa=D&amp;ust=1574830317740000">https://stackoverflow.com/questions/9149063/sqlite-format-number-with-2-decimal-places-always</a>’

As a sanity check, you may manually verify (do not submit any verification code/sql) your percentage calculations against the following values that should not be included in the result:

theme,percentage

Disney Princess,1.01

Exo-Force,0.99

Collectible Minifigures,0.90

Designer Sets,0.88

Elves,0.86

<ol>

 <li>[4 points] <em>Summarize a theme and its sub-themes</em>. As LEGO released more sets, some themes were subdivided into sub-themes.  List each sub-theme and its total number of sets for the ‘Castle’ theme (Use the Castle theme with an id = 186). Sort the output by number of sets highest to lowest, then alphabetically.</li>

</ol>

Output format and sample value:

sub_theme,num_sets

City,116

Space Port,28 Extreme Team,21 …

<ol>

 <li>[6 points] Explore the growth of LEGO sets over time. From a historical standpoint,  it’s interesting tosee the cumulative number of LEGO sets that have been released over time.

  <ol>

   <li>First, create a new view called sets_years that contains the ROWID, year, and number of sets (sets_count)released each year.</li>

  </ol></li>

</ol>

Remember that creating a view will not produce any output, so you should test your view with a few simple select statements during development. One such test has already been added to the code as part of the autograding.

<ol>

 <li><em>Find the cumulative number of sets in the Rebrickable database for each year</em>. Using the view sets_years,find the cumulative number of sets for each year.  g., if the first 3 sets were released in 1949 and 4 more sets released in 1950, then the cumulative values would be:</li>

</ol>

1949,3

1950,7

Sort your output by years in ascending order.

Output format and sample value:

year,running_total

1949,3

1950,7

1951,11         …

<strong>NOTE: </strong>The output to g.ii should match the data found in Q3/q3.csv. When you work on Q3, you will build a visualization using the Q3/q3.csv that we have provided.

<ol>

 <li>[3 points] SQLite supports simple but powerful Full Text Search (FTS) for fast text-based querying (<a href="https://www.google.com/url?q=https://www.sqlite.org/fts3.html&amp;sa=D&amp;ust=1574830317748000">FTS documentation</a><a href="https://www.google.com/url?q=https://www.sqlite.org/fts3.html&amp;sa=D&amp;ust=1574830317748000">)</a>. Import lego data from the <strong>csv </strong>into a new FTS table called parts_fts with the schema:</li>

</ol>

parts_fts(part_num (text),

name (text), part_cat_id (integer), part_material_id (integer))

<strong>NOTE:</strong> Create the table using <strong>fts3</strong> or <strong>fts4</strong> only. Also note that keywords like NEAR, AND, OR and NOT are case sensitive in FTS queries.

<ol>

 <li>[1 point] Count the number of unique parts as “count_overview” whose name field begins with the prefix ‘mini’. A unique part is identified by a unique Matches are not case sensitive.  Match words that begin with that prefix only. e.g., Allowed: ‘Mini’, ‘mini’, ‘minifig’, ‘Minifig’, ‘minidoll’, ‘Minidoll’.  Disallowed: ‘undermined’, ‘administer’, etc.</li>

</ol>

Output format and sample value:

count_overview                         52

<ol>

 <li>[1 points] List the part_num’s of the unique parts as “part_num_boy_minidoll” that contain the terms ‘minidoll’ and ‘boy’ in the name field with no more than 5 intervening terms. Matches are not case sensitive. Contrary to what you did in h(i), match full words, not word parts/sub-strings.</li>

</ol>

e.g., Allowed: ‘minidoll gray hair boy’, ‘minidoll freckles boy’, ‘boy blue shirt minidoll’.  Disallowed: ‘minidoll gray hair yellow shirt blue pants boy’, ‘minidolllego blue pants boy’, ‘boylego minidoll’, etc.

Output format and sample values:

Part_num_boy_minidoll

103

104

…

<ul>

 <li>[1 points] List the part_num’s of the unique parts as “part_num_girl_minidoll” that contain the terms ‘minidoll’ and ‘girl’ in the name field with no more than 5 intervening terms. Matches are not case sensitive. Similar to what you did in h(ii), match full words, not word parts/sub-strings .</li>

</ul>

Output format and sample values: part_num_girl_minidoll

101

102 …

<strong>Deliverable: </strong>Place all the files listed below in the <strong>Q2</strong> folder.  Do <strong>NOT</strong> include the data/ directory.  We will supply our own copy of data during grading.

<ul>

 <li><strong>Q2.SQL.txt</strong>: Modified file containing all the SQL statements and SQLite commands you have used to answer parts a – h in the appropriate sequence.</li>

</ul>

<h1>Q3 D3 (v5) Warmup</h1>

Use Georgia Tech’s library to access S. Murray’s <a href="https://www.google.com/url?q=https://gatech-primo.hosted.exlibrisgroup.com/primo-explore/fulldisplay?docid%3D01GALI_GIT_ALMA51313444370002947%26context%3DL%26vid%3D01GALI_GIT%26lang%3Den_US%26search_scope%3Ddefault_scope%26adaptor%3DLocal%2520Search%2520Engine&amp;sa=D&amp;ust=1574830317756000">Interactive Data Visualization for the Web, 2nd edition</a> (free for GT students).

<ul>

 <li>You may be prompted to sign in using your GT account. Click the ‘Online Access’ and/or ‘O’Reilly Safari Ebooks’.</li>

 <li>Read chapters 4-8. You may briefly review chapters 1-3 if you require some additional background on web development.</li>

 <li>This reading is a simple but important reference that lays the groundwork for Homework 2. This assignment uses D3 version v5, while the book covers only v4. What you learn is transferable to v5. In Homework 2, you will work with D3 extensively.</li>

</ul>

<strong>Note:</strong>  We highly recommend that you use the latest Firefox browser to complete this question. We will grade your work using <strong>Firefox 68.0 (or newer)</strong>.

For this homework, the D3 library is provided to you in the <strong>lib</strong> folder. You must <strong>NOT</strong> use any D3 libraries (d3*.js) other than the ones provided.

You may need to setup an HTTP server to run your D3 visualizations (depending on which web browser you are using, as discussed in the D3 lecture (OMS students: the video “Week 5 – Data Visualization for the Web (D3) Prerequisites: Javascript and SVG”. Campus students: see <a href="https://www.google.com/url?q=https://poloclub.github.io/cse6242-2019fall-campus/slides/CSE6242-500-infovis-stolper.pdf&amp;sa=D&amp;ust=1574830317757000">lecture PDF</a><a href="https://www.google.com/url?q=https://poloclub.github.io/cse6242-2019fall-campus/slides/CSE6242-500-infovis-stolper.pdf&amp;sa=D&amp;ust=1574830317757000">.</a>). The easiest way is to use <a href="https://www.google.com/url?q=https://daanlenaerts.com/blog/2015/06/03/create-a-simple-http-server-with-python-3/&amp;sa=D&amp;ust=1574830317758000">http.server</a> for Python 3.x, or <a href="https://www.google.com/url?q=http://www.pythonforbeginners.com/modules-in-python/how-to-use-simplehttpserver/&amp;sa=D&amp;ust=1574830317758000">SimpleHTTPServer</a> for Python 2.x. <strong>Run your local HTTP server in the hw1skeleton/Q3 folder</strong>

All d3*.js files in the <strong>lib</strong> folder must be referenced using <strong>relative paths</strong>, e.g., <strong>“lib/d3/&lt;filename&gt;</strong>” in your html files (e.g., those in folders Q3, etc.). For example, since the file “Q3/index.html” uses d3, its header should contain:

<strong>&lt;script  type=”text/javascript” src=”lib/d3.v5.min.js”&gt;&lt;/script&gt; It is incorrect to use an absolute path such as:</strong>

&lt;script type=”text/javascript” src=”http://d3js.org/d3.v5.min.js”&gt;&lt;/script&gt;

The 3 files that may be used are:

<ul>

 <li>lib/d3/d3.min.js</li>

 <li>lib/d3-dsv/d3-dsv.min.js</li>

 <li>lib/d3-fetch/d3-fetch.min.js</li>

</ul>

All questions that require reading from a dataset require you to submit the dataset in the deliverables too. In your html/js code<strong>, </strong>use a <strong>relative path</strong> to read in the dataset file<strong>.</strong> For example, since Q3 requires reading data from the q3.csv file, the path should simply be ‘q3.csv’ and <strong>NOT</strong> an absolute path such as “C:/Users/polo/HW1skeleton/Q3/q3.csv”.  Absolute/local paths are specific locations that exist only on your computer, which means your code won’t run on our machines we grade (and you will lose points).

You can and are encouraged (though not required) to decouple the style, functionality and markup in the code for each question. That is, you can use separate files for css, javascript and html — this is a good programming practice in general.

<strong>Deliverables:</strong> Place all the files/folders listed below in the <strong>Q3</strong> folder

<ul>

 <li>A folder named <strong>lib</strong> containing folders <strong>d3, d3-fetch, d3-dsv</strong></li>

 <li><strong>csv</strong>: The file that we have provided you, in the hw1 skeleton under Q3 folder, which contains the data that will be loaded into the D3 plot. (Make sure you are using the provided q3.csv; do <strong>NOT</strong> use any output from Q2.g.ii .)</li>

 <li><strong>(html / css / js)</strong> : When run in a browser, it should display a barplot with the following specifications:

  <ol start="3">

   <li>[3 points] Load the data from csv using D3 fetch methods. We recommend that you use d3.dsv().</li>

   <li>[2 points] The barplot must display one bar per row in the csv dataset. Each bar corresponds to the running total of Lego sets for a given year.  The height of each bar represents the running total.  The bars are ordered by ascending time with the earliest observation at the far left.  i.e., 1949, 1950, 1951, …, 2019.</li>

   <li>[1 point] The bars must have a fixed width and some spacing in between each bar so that the bars do not overlap.</li>

   <li>[3 points] The plot must have visible X and Y axes that scale according to the generated bars;</li>

  </ol></li>

</ul>

i.e., the axes are driven by the data that they are representing.  Likewise, the ticks on these axes adjust automatically based on the values within the datasets, i.e., they must not be hard-coded.

<ol>

 <li>[1.5 points] Use a linear scale for the Y axis to represent the running_total.</li>

 <li>[3 points] Use a time scale for the X axis to represent the year. It may be necessary to use time parsing / formatting when you load and display the year The axis would be overcrowded if you display every year value so set the X-axis ticks to display one tick for every 3 years.</li>

 <li>[1 point] Set the title tag and display a title for the plot.</li>

</ol>

■ The title “Lego Sets by Year from Rebrickable” should appear above the barplot.

■ Also set the HTML title tag (i.e., &lt;title&gt;Lego Sets by Year from Rebrickable&lt;/title&gt;).

<ol>

 <li>[0.5 points] Add your GT username (usually includes a mix of letters and numbers) to the area beneath the bottom-right of the plot (see example image).</li>

</ol>

The barplot should appear similar in style to the sample data plot provided below.

<h2><strong>Q4</strong> OpenRefine</h2>

<ol start="3">

 <li>Watch the videos on the <a href="https://www.google.com/url?q=http://openrefine.org/&amp;sa=D&amp;ust=1574830317768000">OpenRefine</a>’<a href="https://www.google.com/url?q=http://openrefine.org/&amp;sa=D&amp;ust=1574830317768000">s homepage for an overview of its features</a><a href="https://www.google.com/url?q=http://openrefine.org/&amp;sa=D&amp;ust=1574830317768000">. </a>Download and install <a href="https://www.google.com/url?q=http://openrefine.org/download.html&amp;sa=D&amp;ust=1574830317769000">OpenRefine</a> (latest release: 3.2)</li>

 <li>Import Dataset:

  <ul>

   <li>Launch OpenRefine. It opens in a browser (127.0.0.1:3333).</li>

   <li>We use a products dataset from Mercari, derived from a <a href="https://www.google.com/url?q=https://www.kaggle.com/c/mercari-price-suggestion-challenge&amp;sa=D&amp;ust=1574830317770000">competition</a> on Kaggle (Mercari Price <a href="https://www.google.com/url?q=https://www.kaggle.com/c/mercari-price-suggestion-challenge/data&amp;sa=D&amp;ust=1574830317770000">Suggestion Challenge). If you are interested in the details, please refer to the </a><a href="https://www.google.com/url?q=https://www.kaggle.com/c/mercari-price-suggestion-challenge/data&amp;sa=D&amp;ust=1574830317770000">data description page</a><a href="https://www.google.com/url?q=https://www.kaggle.com/c/mercari-price-suggestion-challenge/data&amp;sa=D&amp;ust=1574830317770000">. We have sampled a subset of the dataset provided as “properties.csv”.</a></li>

   <li>Choose “Create Project” → This Computer → csv”. Click “Next”.</li>

   <li>You will now see a preview of the dataset. Click “Create Project” in the upper right corner. c. Clean/Refine the data:</li>

  </ul></li>

</ol>

<strong>Note</strong>: OpenRefine maintains a log of all changes. You can undo changes. See the “Undo/Redo” button on the upper left corner. Follow the exact format requested for the output in each one of the parts below.

<ol>

 <li>[1 point] Select the category_name column and choose ‘Facet by Blank’ (Facet -&gt; Customized Facets -&gt; Facet by blank) to filter out the records that have blank values in this column. Provide the number of rows that return True in txt. Exclude these rows.</li>

</ol>

Output format and sample values:         i.rows: 500




<ol>

 <li>[1 point] Split the column category_name into multiple columns without removing the original column. For example, a row with “Kids/Toys/Dolls &amp; Accessories” in the category_name column, would be split across the newly created columns as “Kids”, “Toys” and “Dolls &amp; Accessories”. Use the existing functionality in OpenRefine that creates multiple columns from an existing column based on a separator (i.e., in this case ‘/’) and does not remove the original category_name Provide the number of new columns that are created in this operation, not including the original category_name column.</li>

</ol>

Output format and sample values:

ii.columns: 10

<strong>Note</strong>: There are many ways of splitting the data. While we have provided a specific way to accomplish this for step ii, some methods could create columns that are completely empty.    In this dataset, none of the new columns should be completely empty. Therefore, to validate your output, you should verify that there are no columns that are completely empty by sorting and checking for null values.

<ul>

 <li>[2 points] Select the column name and apply the Text Facet (Facet → Text Facet). Cluster by using (Edit Cells → Cluster and Edit …) this opens a window where you can choose different “methods” and “keying functions” to use while clustering. Choose the keying function that produces the highest number of clusters under the “Key Collision” method. Click on ‘Select All’ and ‘Merge Selected &amp; Close’. Provide the name of the keying function that produces the highest number of clusters.</li>

</ul>

Output format and sample values:         iii.function: fingerprint

<ol>

 <li>[2 points] Replace the null values in the brand_name” with the text “Unbranded” (Edit Cells -&gt; Transform). Provide the <a href="https://www.google.com/url?q=https://github.com/OpenRefine/OpenRefine/wiki/GREL-String-Functions&amp;sa=D&amp;ust=1574830317774000">General Refine Evaluation Language</a> (GREL) expression used.</li>

</ol>

Output format and sample values:

iv.GREL_brandname: endsWith(“food”, “ood”)

<ol>

 <li>[2 points] Create a new column high_priced with the values 0 or 1 based on the “price” column with the following conditions: If the price is greater than 100, high_priced should be set as 1, else 0. Provide the GREL expression used to perform this.</li>

</ol>




Output format and sample values:

v.GREL_highpriced: endsWith(“food”, “ood”)

<ol>

 <li>[2 points] Create a new column has_offer with the values 0 or 1 based on the item_description column with the following conditions: If it contains the text “discount” or “offer” or “sale”, then set the value in has_offer as 1, else 0. Provide the GREL expression used to perform this. You will need to convert the text to lowercase before you search for the terms.</li>

</ol>

Output format and sample values:

vi.GREL_hasoffer: endsWith(“food”, “ood”)

<strong>Deliverables:</strong> Place all the files listed below in the <strong>Q4</strong> folder

<ul>

 <li><strong>csv</strong> : Export the final table as a comma-separated values (.csv) file.</li>

 <li><strong>json</strong> : Submit a list of changes made to file in json format. Use the “<em>Extract Operation History</em>” option under the Undo/Redo tab to create this file.</li>

 <li><strong>txt </strong>: A text file with answers to parts c.i, c.ii, c.iii, c.iv, c.v, c.vi. Provide each answer in a new line in the exact output format requested.</li>

</ul>

<h1>Extremely Important: folder structure and content of submission zip file</h1>

<strong>Extremely Important: </strong>We understand that some of you may work on this assignment until just prior to the deadline, rushing to submit your work before the submission window closes.  <strong>Take the time</strong> to validate that <strong>all files</strong> are present in your submission and that you do not forget to include any deliverables!  If a deliverable is not submitted, you will receive <strong>zero </strong>credit for the affected portion of the assignment — this is a very sad way to lose points, since you’ve already done the work!

You are submitting a single <strong>zip</strong> file named <strong>HW1-GTusername.zip</strong> (e.g., HW1-jdoe3.zip).

The files included in each question’s folder have been clearly specified at the end of the question’s problem description.

The zip file’s folder structure must exactly be (when unzipped):

HW1-GTusername/

Q1/ script.py bricks_graph.gexf graph.png or graph.svg

Q2/

Q2.SQL.txt

Q3/ index.(html / js / css)

q3.csv lib/ d3/ d3.min.js d3-fetch/ d3-fetch.min.js

d3-dsv/

d3-dsv.min.js

Q4/ properties_clean.csv changes.json Q4Observations.txt