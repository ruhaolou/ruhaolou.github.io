**Building Web Dictionary**

In this website, I am aiming to create a web dictionary using APIs. This webpage automatically save words searched by the users in the database. Users can edit or delete specific words from the search history. This webpage is made for learning objectives.

The webpage uses C-panel data storage as well as API search panel. Each page contains html and php to generate codes.  It is made to be simple and can be easily understood by all individuals.

If you are here to learn about this basic coding sequence, by the end of this article, you will understand how to:

- --Use API in your web servers.
- --Create, Read, Update and Delete from SQL using PHP.
- --Adding bootstrap function.

**Flow**

- --User interact with the webpage by searching words user want to know more about
- --Words inserted will go through API to check if definitions, audio, and images exist in the server.
- --If found, result will be extracted to the page front. (if not found, result will not show)
- --This result will then be recorded into the database.
- --If user click &quot;History&quot; from top right hyper link, it will take user to a new page.
- --On a new page, named &quot;History&quot;, user will see all searched history recorded in the database. This data is extracted from the SQL and displayed on the screen with PHP.
- --On each search row, user have options to either delete or edit search history.
- --Delete hyperlink will delete selected search row from the database and automatically refresh the history page. (you will see result right away)
- --Edit hyperlink on the other hand takes user to a new page which let user input words and definitions, updated by submission button.
- --After submission button, webpage will show results of its update on the screen. (this is done by reading SQL with PHP).

**Featured Technologies**

- --PHP: connecting user input to SQL, reading from SQL, updating and deleting from SQL
- --Html: basic structure of the page
- --Bootstrap: package of visual attributes of the page
- --CSS: visual attribute that supports Bootstrap.

**Video on how it works**

[![](http://img.youtube.com/vi/6-YAkirhOQU/0.jpg)](http://www.youtube.com/watch?v=6-YAkirhOQU "")


**Steps**

**API Settings**

1. Create an API account from https://dictionaryapi.com/. Follow their instructions to register for an API for Merriam-Webster&#39;s Collegiate which comes with Audio.

 
1. Read API documentation to know how to use it. Then use &quot;Your Key&quot; to see what you need to add in your API. Create **heart.php** file. Use them inside application you in your file.

1. Install JSON Viewer on google chrome. Then open **heart.php** file on google chrome.
2. In **heart.php** file, convert JSON to Array in following code.

 $arr = json\_decode($output, true);

1. Print $arr in **heart.php** and see the structure of data:

print\_r($arr)

1. To access each data part, understand array structure of the data. Input following code in your **dictionary.php f**

audio\_file = $arr[0][hwi][prs][0][sound][audio]



1. Open heart.php on webpage and take a look at the structure. From organized Jason file, find  definition, image and caption of the word.
2. Update **dictionary.php** using heart.php &#39;s result for definition, word, image, audio, and caption in. This helps you connect your file to the server. By the end of this instruction, this is what your **dictionary.php** page will look like.

**SQL Create &amp; Read**

1. In your C-Panel, make New database and User account.
2. Go to phpMyAdmin and click SQL.
3. Go to the side bar and select the data base you created. Then click on New.



1. This will take you to this page. You will then fill out the form

1. This will take you to this page. You will then fill out the form

Once set, go back to **dictionary.php** file and start coding.

1. From start of the php file, make sure your page is connected to your database using the following code.

$host=&quot;localhost&quot;;

$user=&quot;insert username&quot;;

$password=&quot;insert password&quot;;

$database=&quot;insert database&quot;;

$conn = new mysqli($host, $user, $password, $database);

if ($conn-\&gt;connect\_error)

{

die(&quot;Connection failed: &quot; . $conn-\&gt;connect\_error);

}

1. In your dictionary.php, after display function, write another \&lt;?php ?\&gt; that will INSERT in your database using the following codes.

$sql= &quot;INSERT INTO `Dictionary` (`word`, `definition`, `audio`, `image`, `caption`) VALUES (&#39;$word&#39;, &#39;$def&#39;, &#39;$img\_url&#39;, &#39;$audio\_url&#39;, &#39;$imp\_cap&#39;);&quot;;

1. Your SQL create is all set.

1. Now make another page called **history.php** that will read your information from your database. Like create, first connect your php file to database.
2.  Then Extract database row per row using loop function. Following is an example after you connect your file to SQL.

$sqls = &quot;SELECT \* from Dictionary&quot;;

            $results=$conn-\&gt; query($sqls);

            try{

                    $dbh = new PDO(&quot;mysql:host=$host;dbname=$database&quot;, $user, $password);

                    $result =$dbh-\&gt;query(&#39;SELECT \* from Dictionary&#39;);

                    foreach($result as $row){

                        $words = $row[&#39;word&#39;];

                        $def = $row[&#39;definition&#39;];

                        $id = $row[&#39;id&#39;];

                        $edit = &quot;\&lt;a href = &#39;edit.php?id=$id&amp;edit=true&#39;\&gt;Edit\&lt;/a\&gt;&quot;;

                        $delete = &quot;\&lt;a href = &#39;delete.php?id=$id&amp;delete=true&#39;\&gt;Delete\&lt;/a\&gt;&quot;;

                        echo &quot;\&lt;tr\&gt;\&lt;td\&gt;&quot;. $words .&quot;\&lt;/td\&gt;\&lt;td\&gt;&quot;. $def . &quot;\&lt;/td\&gt;\&lt;td\&gt;&quot;. $edit . &quot;\&lt;/td\&gt;\&lt;td\&gt;&quot;. $delete . &quot;\&lt;/td\&gt;\&lt;tr\&gt;\&lt;/br\&gt;&quot;;

                    }

1. SQL read is all set.

**SQL Update &amp; Delete**

1. Create edit.php and delete.php.
2. In your history.php, create hyperlink that will take you to edit.php and delete.php. Incorporate it in the read loop. Example for following.

&#39;edit.php?id=$id&amp;edit=true&#39;\&gt;Edit\&lt;/a\&gt;&quot;;

$delete = &quot;\&lt;a href = &#39;delete.php?id=$id&amp;delete=true&#39;\&gt;Delete\&lt;/a\&gt;&quot;;

echo &quot;\&lt;tr\&gt;\&lt;td\&gt;&quot;. $words .&quot;\&lt;/td\&gt;\&lt;td\&gt;&quot;. $def . &quot;\&lt;/td\&gt;\&lt;td\&gt;&quot;. $edit . &quot;\&lt;/td\&gt;\&lt;td\&gt;&quot;. $delete . &quot;\&lt;/td\&gt;\&lt;tr\&gt;\&lt;/br\&gt;&quot;;

1. In your edit.php, create a user insert section using html and php function that will connect to your database.
2. Write function that will take result from history.php to edit.php.
3. Then from that result find a match from SQL you connected to.
4. When found, update user input into the database. Following is an example of what codes will looks like in your page.

if ( isset ($\_POST[&#39;newname&#39;]))

        {

            $newname = $\_POST[&#39;newname&#39;];

            $definition = $\_POST[&#39;definition&#39;];

            $id = $\_POST[&#39;id&#39;];

            //$ids = $\_POST[&#39;ids&#39;];

            $sql = &quot;UPDATE Dictionary SET word=&#39;$newname&#39;, definition=&#39;$definition&#39; WHERE id=$id&quot;;

            //$sqld = &quot;UPDATE Dictionary SET definition=&#39;$definition&#39; WHERE id=$id&quot;;

            //echo $sql.&#39;\&lt;br\&gt;&#39;;

            //echo $sqld.&#39;\&lt;br\&gt;&#39;;

            $result =$dbh-\&gt;query($sql);

            //echo $result;

            $res =$dbh-\&gt;query($sqld);

            $row[&#39;word&#39;]= $newname;

            $row[&#39;definition&#39;]= $definition;

            //echo &quot;$definition&quot;;

        }

      if (isset($\_GET[&#39;edit&#39;]) || isset ($\_POST[&#39;newname&#39;]) )

        {

            //echo &quot;hello&quot;;

            $id = $\_GET[&#39;id&#39;];

            //echo $id.&quot;----\&lt;br\&gt;&quot;;

            $sql = &quot;SELECT \* FROM Dictionary WHERE id=$id&quot;;

                    $result =$dbh-\&gt;query($sql);



                    foreach($result as $row){

                        $wo= $row[&#39;word&#39;];

                        $de = $row[&#39;definition&#39;];

                        echo &quot;\&lt;h4\&gt; Updated Result \&lt;/h4\&gt;&quot;;

                        echo &quot;\&lt;table\&gt;&quot;;

                        echo &quot;\&lt;tr\&gt;&quot;;

                        echo &quot;\&lt;th\&gt;Words\&lt;/th\&gt;&quot;;

                        echo &quot;\&lt;th\&gt;Definition\&lt;/th\&gt;&quot;;

                        echo &quot;\&lt;tr\&gt;\&lt;td\&gt;&quot;. $wo.&quot;\&lt;/td\&gt;\&lt;td &quot;. $de. &quot;\&lt;/td\&gt;\&lt;tr\&gt;\&lt;/br\&gt;&quot;;

                        echo &quot;\&lt;/tr\&gt;&quot;;

                        echo &quot;\&lt;/table\&gt;&quot;;

                        //echo $row[&#39;word&#39;].&#39;\&lt;br\&gt;&#39; ;

                        //echo $row[&#39;definition&#39;].&#39;\&lt;br\&gt;&#39; ;

                        echo &quot;\&lt;/br\&gt;&quot;;

                    }

        }

1. SQL update is all set.
2. Go to delete.php you created.
3. In the file, write code that will connect to your SQL.
4. Next, code a line that will read selected id from history and delete a row that match with same id extracted from history.php. following is an example.

if( isset ($\_GET[&#39;delete&#39;]))

    {

        $id = $\_GET[&#39;id&#39;];

        echo &#39;$id&#39;;

        $sql = &quot;DELETE FROM Dictionary WHERE id=&#39;$id&#39;&quot;;

        //$res= mysql\_query($sql) or die(&quot;Failed&quot;.mysql\_error());

        //$row[&#39;id&#39;]= &#39;&#39;;

        $result =$dbh-\&gt;query($sql);

                    foreach($result as $row){

                        echo $row[&#39;word&#39;].&#39;\&lt;br\&gt;&#39; ;

                        echo $row[&#39;definition&#39;].&#39;\&lt;br\&gt;&#39; ;

                        echo &quot;\&lt;/br\&gt;&quot;;

                    }

        echo &quot;\&lt;meta http-equiv=&#39;refresh&#39; content=&#39;0;url=history.php&#39;\&gt;&quot;;

    }

1. SQL delete is all set.

**Add Bootstraps and CSS**

1. On every header section, add link to CSS and Bootstraps.

Following is an example

link rel=&quot;stylesheet&quot; href=&quot;https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css&quot; \&gt;

link rel=&quot;stylesheet&quot; href=&quot;ab.css&quot;\&gt;

**Work Cited.**

Tofighi, Ghassem &quot;Lab7&quot;.PDF file
