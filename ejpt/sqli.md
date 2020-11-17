test inputs with ' to see if you can trigger any sql errors. if so you can then move to trying boolean conditions with (' and 1=1;-- -) and (' and 1=2;-- -)

can continue manually or use sqlmap. sqlmap -u http://example.site/view.php?id=1 : can be used to find if the parameter is injectable, you can then go on to use enumueration through sqlmap like --tables -columns --dump to get table information.

can also look for union based injection by trying UNION SEECT null;-- - and incrementing the number of nulls until it matches the amount of columns.

once again can continue manually using user() and substring() or use sqlmap.
you can tell sqlmap which injection techqnique to use sqlmap -u <url/search.php?search=n> -p search --technique=U : for union based techniques

if successfull you can start enumeration by using --users with above command to find users. and what databases there are using --dbs

when you know the database you want to find out about from --dbs you can use -D <databasename> --tables to get the tables for it

then get columns for a table by -D <databasename> -T <tablename> --columns, and then -D <databasename> -T <tablename> -C <columnname,columnname> --dump

these are done using HTTP GET verbs, but sqli can also be done using POST from input forms.

this can be done more easily from burpsuite. you can go to an input like login, record a post form input and repeat it putting a ' into the inputs one at a time. this
may create an error similar to the previous example and shows there is a vulnerability. can then go through the same initial process of trying boolean 1=1/1=2 etc.
this may changethe amount of headers sent allowing us to show that the sqli is working. now that an sqli entry point is found can go to sqlmap and enter 

sqlmap -u <url/search.php> --data=<data body from post> -p <entry point parameter> --technique=B --banner : to get the banner

can go on to do enumeration as previously shwon.

this can also be done easily by saving the item in burp and loading it into sqlmap with, sqlmap -r <saved file> -p user --technique=B --banner

searches are save in sqlmap directory to save queries from being run multiple times. if you want to empty it and run the commands again delete it.



