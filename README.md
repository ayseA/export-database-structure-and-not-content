# How to Export Your Database Structure Without Data Content

Often times, you want to copy your database for its structure and not data. A typical case is an outside consultant stepping into your systems and wants to look at your database as part of his/her work. The data content of your database, i.e. what’s sitting in the rows of your tables isn’t of any relevance here – your consultant hasn’t any interest in it, nor do you want your data unnecessarily exposed at this stage. 

What you can do is to simply put at use a feature which all relational databases offer – copy your database structure. This can be termed as export, dump, backup, store, .. depending on the database&context you’re in. 

This article shows how to copy your database structure without the data content in MySQL as a sample case. At the time of this writing, the set of instructions to do this in MS SQL Server and PostgreSQL as well as MySQL are [here](https://github.com/ayseA/export-database-structure-and-not-content). I’m planning on adding to this repository the corresponding instruction set for DB2 and probably some databases in the upcoming days.

Before proceeding with the instructions, note the following names for ease of consistent reference throughout this text and the commands in the repository. Each of these names are placeholders for the actual names you’ll be using while running these commands for your case, with your own names: 

* _**`my_own_db`**_: this is the database being looked at. It’s your original database – the one containing all your data, and the one you want to clone for its structure and NOT its data.
* _**`file2consultant.sql`**_: this is the file your my_own_db will be cloned into in the end. When done by the instructions given here, _`file2consultant.sql`_ will contain all info about your database structure, and none of your data. Once generated, this is the file you’d be sending to your consultant in the above use-case.


     The use of _`file2consultant.sql`_ as is saves this file to the disk directory you’re running the commands in. You can save this file to some other directory just by giving the full path to its location. 

    **Eg:** To save your _`file2consultant.sql`_ at an existing directory “_D:\temp-dir_”, prepend it to your filename to give the full path in the commands – “_D:\temp-dir\file2consultant.sql_”. 

* _**`structure_copy_db`**_: as its name implies, this name is the placeholder for the name of the database that ends up being the structure-copy of _`my_own_db`_. Unlike MS SQL Server, the import command of MySQL doesn’t create the database being imported to. So, you need to create this database yourself before running your import command. Once the import operation is successfully completed, you’ll see in _`structure_copy_db`_ all you see in _`my_own_db`_, except that all the tables are empty.

* _**`yourDBuserName`**_: the username you use for accessing your database.

## MySQL commands

In this article, we take MySQL as the case/example and show the commands for MySQL only.

When you run the commands on command-line interface (CLI) of your operating system (OS), you’ll be prompted to enter your user password. Your database system wants to authenticate you before letting you run commands on its engine. Enter your password – the one for _`yourDBuserName`_ when asked.

If you get an error message saying that the command isn’t recognized, it means you didn’t add your database installation location to the path-list of your machine. To resolve this, you can do one of the following:

1. add the `bin` directory of your database installation to the paths list in your OS

2. goto the `bin` directory of your database system and run the commands there
3. give your OS the full path of the command you're running. That is, prepend each command with the full path to your database `bin` directory

    **Eg:** on Windows CLI for MySQL command, run 
     
     ``` 
     C:\Program Files\MySQL\MySQL Server 5.7\bin\mysqldump” -u yourDBuserName -p -d my_own_db > file2consultant.sql 
     ```

     instead of 
 
   ``` 
   mysqldump -u yourDBuserName -p -d my_own_db > file2consultant.sql
   ```
     

### Create _`file2consultant.sql`_

To copy the structure of your database to a disk location, run the following on your OS/CLI:
    
   ``` 
   mysqldump -u yourDBuserName -p -d my_own_db > file2consultant.sql
   ```
     
It now created a file _`file2consultant.sql`_ in the directory that you ran it. This file is ready as you wanted, i.e. contains all structure and no data of _`my_own_db`_. You now can send _`file2consultant.sql`_ as is to your consultant. In this command, the `'-d'` switch is the one that makes sure your data isn’t copied during the process. So, make sure to include this switch unless you’re looking for a full copy.

> In MySQL Workbench, the feature that corresponds to this command is at 
> Server (top bar) > Data Export. 
> In the panel that opens, see the drop-down menu that shows 
> “Dump Structure and Data” as default, and change it to “Dump Structure.”

### Verify _`file2consultant.sql`_


Once you successfully ran the above command, a structure-copy of _`my_own_db`_ is generated into file _`file2consultant.sql`_.

You still may want to make sure that _`file2consultant.sql`_ is what you want. The best way to do that is to import it to an empty database, just as your consultant will do. First, make sure that there exists and empty database to import it into. So, create _`structure_copy_db`_ if you haven’t already – you can do so by running the following in your OS command line:

```
mysql -u yourDBuserName -p -e "CREATE DATABASE structure_copy_db"
```
Now you are ready to import to a database on your MySQL engine:
```
mysql -u yourDBuserName -p structure_copy_db < file2consultant.sql
```



All done now. Just go into _`structure_copy_db`_ and see what is/not in it. What you see in it is what _`file2consultant.sql`_ contains, nothing more and nothing less.

  
  

## Conclusion

  

In this article, we covered how to export a MySQL database into an external, independent file that can be used in another MySQL environment to duplicate the original database for its structure only.

  

The instructions shown here work for MySQL only. However, all relational database systems have features to structure-copy a database just as we’ve done here. 	Keep an eye on [this](https://github.com/ayseA/export-database-structure-and-not-content) repository which currently contains the corresponding commands for  [MS SQL Server](https://github.com/ayseA/export-database-structure-and-not-content/blob/master/SQL-Server) and [PostgreSQL](https://github.com/ayseA/export-database-structure-and-not-content/blob/master/psql) also.
