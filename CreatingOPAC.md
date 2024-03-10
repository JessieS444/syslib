# Creating a Bare Bones OPAC

A real OPAC and ILS would be a lot more complex than this, but what we did is the basic bones of it.
In reality there would be dozens of tables.

1. First, I went to the /var/www/html directory.
2. I created the nano file "mylibrary.html" and added the html provided for the search page.
   ```
   <html>
   <head>
   <title>MySQL Server Example</title>
   </head>
   <body>

   <h1>A Basic OPAC</h1>

   <p>In the form below,
   <b>optionally</b> enter text in the search field.
   You can search by author, title, or publisher.
   Capitalization is not necessary.
   It's okay to enter partial information,
   like part of an author's, title's, or publisher's name.</p>

   <p>The date fields are <b>required</b>.
   You can use the date fields to limit results.
   I added some extra records,
   which you can view to know what you can query:</p>

   <p><a href="http://11.111.222.222/opac.php">http://11.111.222.222/opac.php</a></p>

   <p>This is very much a toy,
   stripped down
   <a href="https://en.wikipedia.org/wiki/Online_public_access_catalog">OPAC</a>.
   The records are basic.
   Not only do they not conform to
   <a href="https://www.loc.gov/marc/">MARC</a>,
   but they don't even conform to something
   as simple as
   <a href="https://www.dublincore.org/">Dublin Core</a>.

   <p>I also don't provide options
   to select different fields,
   like author, title, or publisher fields.
   Instead the search field below searches
   all the fields
   (author, title, publisher)
   in our <b>books</b> table.</p>

   <p>The key idea is to get a sense
   of how an OPAC works, though.</p>

   <h2>My Basic Library OPAC</h2>
   <form method="post" action="search.php">
    <label for="search">Search:</label>
    <input type="text" name="search" id="search">
    <br>
    <label for="start_date">Start Date:</label>
    <input type="date" name="start_date" id="start_date">
    <br>
    <label for="end_date">End Date:</label>
    <input type="date" name="end_date" id="end_date">
    <br>
    <input type="submit" value="Search">
   </form>

   </body>
   </html>
   ```

4. Next, I modified the nano file to include my IP address rather than the default one. I used nano instead of vi because I am more comfortable in nano.
5. I next created a new nano file for the PHP search script titled search.php. I pasted the provided PHP and again changed the default 11.111.222.222 to my own IP address.

```
<?php
// Load MySQL credentials
require_once 'login.php';

// Establish connection
$conn = mysqli_connect($db_hostname, $db_username, $db_password) or
  die("Unable to connect");

// Open database
mysqli_select_db($conn, $db_database) or
  die("Could not open database '$db_database'");

// Check if search query was submitted
if (isset($_POST['search'])) {
    // Sanitize user input to prevent SQL injection attacks
    $search = mysqli_real_escape_string($conn, $_POST['search']);

    // Get the start and end dates for the date range
    $start_date = mysqli_real_escape_string($conn, $_POST['start_date']);
    $end_date = mysqli_real_escape_string($conn, $_POST['end_date']);

    // Build the MySQL query with a WHERE
    // clause that includes the date range filter
    $query = "SELECT * FROM books WHERE
        (author LIKE '%$search%' OR
        title LIKE '%$search%' OR
        publisher LIKE '%$search%') AND
        copyright BETWEEN '$start_date' AND '$end_date'";

    // Execute the query
    $result = mysqli_query($conn, $query);

    // Check if any results were returned
    if (mysqli_num_rows($result) > 0) {
        // Loop through the results and output them
        while ($row = mysqli_fetch_assoc($result)) {
            echo "ID: " . $row["id"] . "<br>";
            echo "Author: " . $row["author"] . "<br>";
            echo "Title: " . $row["title"] . "<br>";
            echo "Publisher: " . $row["publisher"] . "<br>";
            echo "Copyright: " . $row["copyright"] . "<br><br>";
        }
    } else {
        echo "No results found.";
    }

    // Free up memory by closing the MySQL result set
    mysqli_free_result($result);
}

// Close the MySQL connection
mysqli_close($conn);

echo "<p>Return to search page: <a href='http://11.111.222.222/mylibrary.html'>http://11.111.222.222/mylibrary.html</a></p>";

?>
```

7. I went to my website with my IP and accessed the mylibrary.html page: http://34.125.133.35/mylibrary.html
8. My return to search page already had the correct mylibrary.html because the code was changed since the video, so I did not have to change the opacbb.php to mylibrary.html in the search.php nano file.
9. I searched on my basic OPAC for millet (adjusting the dates to be broad) and pulled up the record that we put in last week.

The http://34.125.133.35/mylibrary.html webpage that we created is an extremely basic version of the UK infocat search (an OPAC/discovery system)

## MySQL Modifications and Testing Queries

1. I switched over to MySQL using `mysql -u opacuser -p`
2. I switched to the opacdb database using `use opacdb;`
3. I added the suggested new records using:
``` 
insert into books
(author, title, publisher, copyright) values
('Emma Donoghue', 'Room', 'Little, Brown \& Company', '2010-08-06'),
('Zadie Smith', 'White Teeth', 'Hamish Hamilton', '2000-01-27');
```
5. I tested the queried on my webpage:
   input "room" and added the dates "01/01/2009" to today
   got the following result that I was aiming for:
   ![image](https://github.com/JessieS444/syslib/assets/157999229/ddef8870-4164-4206-8220-afc19fa1fa33)

   input "white teeth" and the dates "01/01/1999" to today
   got the following result:
   ![image](https://github.com/JessieS444/syslib/assets/157999229/d178e4b8-f4c6-4306-a668-7f4eef02551c)

   input "donoghue" and "01/01/2009" to today:
   ![image](https://github.com/JessieS444/syslib/assets/157999229/e9a5a8aa-cd18-4ef3-a68f-79088a84765d)

   input "hamish hamilton: and "01/01/1999" to today:
   ![image](https://github.com/JessieS444/syslib/assets/157999229/37e79875-26bc-4f47-827a-de07a0226702)

   I just input the "01/01/1999" to today"
   ![image](https://github.com/JessieS444/syslib/assets/157999229/ee7518fc-43fe-481d-9972-8e6e7e850ee1)




## Overview

I feel like this week we implemented a lot of the stuff we set up last week. We set up some nano files and added the provided code to make the web pages into an OPAC. Then I added item record into MySQL and tested different queries to see if they worked (they did). This week I didn't find to be too difficult and I felt like I understood and remembered the needed stuff from the last few weeks.
