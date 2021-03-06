<h1 class="iconed" id="toc_0"><i class="fa fa-hand-o-right"></i>Introduction</h1>

This tutorial will show you how to create a custom web API that exposes data stored in an Address Book SQL database.

<h1 class="iconed" id="toc_0"><i class="fa fa-flag-checkered"></i>Requirements</h1>

To follow this tutorial, you will need:

*   a web browser,
*   20 minutes of your time,
*   your SQL database login details.

<h1 class="numbered" id="toc_1"><i>1</i>Prepare the SQL Data Source</h1>

In this tutorial example, we create an SQL table named **T_CONTACT** with the following fields:

<li>**ID** (varchar): primary key</li>
<li>**FIRST_NAME** (varchar): first name</li>
<li>**LAST_NAME** (varchar): last name</li>
<li>**NUMBER** (int): street number</li>
<li>**STREET_NAME** (varchar): street name</li>
<li>**POSTCODE** (varchar): postcode</li>
<li>**CITY** (varchar): city</li>

>**Note:** The currently supported column types are the following: INT, INTEGER, MEDIUMINT, DATE, DATETIME, TIMESTAMP, TIME, BIGINT, BOOLEAN, DECIMAL, DOUBLE, FLOAT, NUMERIC, SMALLINT, TINYINT and VARCHAR.

Connect the database engine using the MySQL console:

<pre class="language-bash"><code class="language-bash">$ mysql -u root -p </code></pre>

Create a database and switch to it:

<pre class="language-sql"><code class="language-sql">&gt;mysql&gt; create database apispark;
Query OK, 1 row affected (0.01 sec)
mysql&gt; use apispark;
Database changed
</code></pre>

Create an InnoDB table named T_ADDRESS with fields previously listed:

<pre class="language-sql"><code class="language-sql">CREATE TABLE T_CONTACT (
	  ID VARCHAR(255),
	  FIRST_NAME VARCHAR (255),
	  LAST_NAME VARCHAR (255),
	  NUMBER INT,
	  STREET_NAME VARCHAR (255),
	  POSTCODE VARCHAR (255),
	  CITY VARCHAR (255),
	  PRIMARY KEY(ID)
	) ENGINE = InnoDB;
</code></pre>

Create a new user and grant him full rights on the database. Replace username and password by the values you like:

<pre class="language-sql"><code class="language-sql">CREATE USER 'username'@'%' IDENTIFIED BY "password";
GRANT ALL PRIVILEGES on apispark.T_CONTACT TO 'username'@'%';
FLUSH PRIVILEGES;
</code></pre>

>**Note:** you can grant privileges on all tables by replacing T_CONTACT by \* and on all databases by replacing apispark by \*.

<h1 class="numbered" id="toc_2"><i>2</i>Create a SQL Wrapper</h1>

If you have not already done so, sign in to your APISpark account and open your **Dashboard**.

Create a new Entity Store. Click on **+ Entity Store**, select the "SQL wrapper" **Type** and enter the **Name** "mySQLwrapper".

Input a description if you wish.

![Create an SQL Wrapper](images/create-sql-wrapper.jpg "Create an SQL Wrapper")

From the **Connection settings** section, select the appropriate **Driver** (database type) and input the **Host name**, **Port number**, **Database**, **User** name and **Password**.

Click on the **Test connection** button to test the connection.

>**Note:** depending on your configuration, you may need to configure your firewall in order to authorize APISpark IP addresses to access your database from the internet. Feel free to contact the <a href="http://support.restlet.com/" target="_blank">Help Desk</a> if you need help.

Click on **Add** to create the Wrapper. You will be taken to the Wrapper's **Overview** tab.

![Add a Catalog](images/settings-tab.jpg "Add a Catalog")

This automatically creates entities based on the imported tables. APISpark automatically renames the entities and their properties during this operation.

>**Note:** You can change the database you are connected to with the **Change database** button. If you want to retrieve your database original structure after you have made changes, click the **Synchronize** button. This will synchronize your Entity Store with your SQL database again.

Our Entity Store now contains an Entity called *Contact*.

![New entities](images/new-sql-entities.jpg "New SQL entities")

The *Contact* entity’s properties correspond to the columns present in the matching database table.

Click on the **Deploy** button to deploy the Wrapper.

<h1 class="numbered" id="toc_3"><i>3</i>Export a Web API</h1>

From the Wrapper's **Overview** page, click on the cog button on the left of the **Deploy** button and select **Export web API**.

![Export web API](images/export-api-from-sql.jpg "Export web API")

Give your new API a name. We named ours **My Address Book API**.

![Create web API](images/create-api-from-sql.jpg "Create web API")

The domain will be created automatically but may not be available anymore so make sure to adjust it.

Click on **Add** to create the API. You will be taken to the API's **Overview** page.

Deploy the API by clicking the **Deploy** button.

![Deploy button](images/deploy-button-address-book.jpg "Deploy button")

<h1 class="numbered" id="toc_4"><i>4</i>Invoke the Web API</h1>

Using a web API does not impose any particular programming language. It can even be done from a web browser. However, to test your API, APISpark offers an integration of the Swagger UI that provides a graphical user interface to perform HTTP calls.

From the **Overview** tab of your API, select the appropriate Endpoint.  
From the left panel, click on the Resource and the Method chosen and click on the **swagger** button.

![Try it out!](images/02swagger-button.jpg "Try it out!")

The Swagger UI opens in a new tab.  
Your credentials are pre-filled in the two fields on top of the screen.

![Swagger UI](images/02swagger-ui.jpg "Swagger UI")

Scroll down to the bottom of the page and click on the **Try it out!** button to invoke your API.

![Swagger Try it out button](images/02swagger-try-it-out-button.jpg "Swagger Try it out button")

Any POST requests made to the API will result in new data being created in your SQL database. Likewise, any data manually inserted via your SQL DBMS is visible via the custom web API.

>**Note:** APISpark lets you generate custom Client SDKs for you API. Supported environments include Java, Android, iOS and JavaScript (AJAX or Node.js).

Congratulations on completing this tutorial! If you have questions or suggestions, feel free to contact the <a href="http://support.restlet.com/" target="_blank">Help Desk</a>.
