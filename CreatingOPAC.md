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
6. I went to my website with my IP and accessed the mylibrary.html page: http://34.125.133.35/mylibrary.html
7. My return to search page already had the correct mylibrary.html because the code was changed since the video, so I did not have to change the opacbb.php to mylibrary.html in the search.php nano file.
8. I searched on my basic OPAC for millet (adjusting the dates to be broad) and pulled up the record that we put in last week.

The http://34.125.133.35/mylibrary.html webpage that we created is an extremely basic version of the UK infocat search (an OPAC/discovery system)
