# Grep
> `grep` is a command that can help you analyze a lot of data at once.

For this week, we learned how to use the `grep` command.
I walked along with the steps in the examples, then did my own search with the examples.

## Example
I first searches scopus for "auditory processing disorder" and got 1,628 results.
I downloaded the first page of results (10 total).

## First query: `grep "^@" scopus2.bib`
This query pulled up the everything after the @ symbol, which was the format of each source and and the author/year.
To get just the @ and the format, I used the command `grep -Eio "^@(A|B)[A-Z]*" scopus2.bib | sort`
> The `-E` extends `grep`'s regular expression engine.
> The `-i` is used to turn off case sensitivity.
> The `-o` returns only matching results from the lines.
> The `(A|B)` tells `grep` to search only for letters after the @ sign that start with A or B (not necessary since I have all articles and no books).
> The `[A-Z]*` matches any letters after the initial A or B characters.
> The `|` is called piping and it takes the results of the query and applies the next command to it.
> The `sort` command sorts the results alphabetically.

<img width="350" alt="Screenshot 2024-02-19 at 8 58 38 PM" src="https://github.com/JessieS444/syslib/assets/157999229/4653dafd-01b3-4557-9e41-08f027dfe2ea">


## Second query: `grep -Eio "^@(A|B)[A-Z]*" scopus2.bib | sort | uniq -c`
This query does everything that the last one does, but the additional piped `uniq -c` command deduplicates each result (and gives you a count of each result).

<img width="590" alt="Screenshot 2024-02-19 at 8 48 13 PM" src="https://github.com/JessieS444/syslib/assets/157999229/0fcb2214-7917-408d-922a-ede1e3a6cbe6">



## Third query: `grep "journal" scopus2.bib`
This query gets a list of all the journal titles that the articles were in.

<img width="531" alt="Screenshot 2024-02-19 at 8 48 28 PM" src="https://github.com/JessieS444/syslib/assets/157999229/0c762c9c-705e-4f43-b419-7d272a2a8c7e">


## Fourth query: 
```
grep "journal =" scopus2.bib | cut -d"=" -f2 | \
sed 's/ {//' | sed 's/},//' | \
sort | uniq -c | sort`
```
This query has a lot going on so I gotta break that down.
First of all, it is a multi line query as shown by the `\`.
> The `cut` command takes the results of the grep command and removes the first column based on the comma as the column delimiter.
> The first `sed` command removes the space and opening curly brace and replaces it with nothing.
> The second `sed` command removes the closing curly brace and comma and replaces it with nothing.
> The last section sorts the list alphabetically, deduplicates and counts the results, and then sorts it numerically.

<img width="959" alt="Screenshot 2024-02-19 at 8 48 58 PM" src="https://github.com/JessieS444/syslib/assets/157999229/6dd00376-2c18-49a0-afa5-ac49ce01567e">

