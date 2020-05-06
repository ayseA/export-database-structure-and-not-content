

## How to Export Your Database Structure Without Data Content 

Often times, you want to copy your database for its structure and not data. A typical case is an outside consultant stepping into your systems and wants to look at your database as part of his/her work. The data content of your database, i.e. what’s sitting in the rows of your tables isn’t of any relevance here – your consultant hasn’t any interest in it, nor do you want your data unnecessarily exposed at this stage. 

What you can do is to simply put at use a feature which all relational databases offer – copy your database structure. This can be termed as export, dump, backup, store, .. depending on the database&context you’re in. 

This article shows how to copy your database structure without the data content in MySQL as a sample case. At the time of this writing, the set of instructions to do this in MS SQL Server and PostgreSQL as well as MySQL are in ted in your [repository settings](https://github.com/ayseA/export-database-structure-and-not-content). I’m planning on adding to this repository the corresponding instruction set for DB2 and probably some databases in the upcoming days.  

Before proceeding with the instructions, note the following names for ease of consistent reference throughout this text and the commands in the repository. Each of these names are placeholders for the actual names you’ll be using while running these commands for your case, with your own names: 

```
1. _my_own_db_: this is the database being looked at. It’s your original database – the one containing all your data, and the one you want to clone for its structure and NOT its data.
2. _`file2consultant.sql`_: this is the file your my_own_db will be cloned into in the end. When done by the instructions given here, _`file2consultant.sql`_ will contain all info about your database structure, and none of your data. Once generated, this is the file you’d be sending to your consultant in the above use-case.


     The use of _`file2consultant.sql`_ as is saves this file to the disk directory you’re running the commands in. You can save this file to some other directory just by giving the full path to its location. 

    **Eg:** To save your _`file2consultant.sql`_ at an existing directory “D:\temp-dir\”, prepend it to your filename to give the full path in the commands – “D:\temp-dir\file2consultant.sql”.  
```


### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/ayseA/export-database-structure-and-not-content/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
