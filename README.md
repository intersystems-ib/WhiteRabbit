![WR logo](https://github.com/OHDSI/WhiteRabbit/blob/master/whiterabbit/src/main/resources/org/ohdsi/whiteRabbit/WhiteRabbit64.png) White Rabbit 
===========

![RiaH logo](https://github.com/OHDSI/WhiteRabbit/blob/master/rabbitinahat/src/main/resources/org/ohdsi/rabbitInAHat/RabbitInAHat64.png) Rabbit in a Hat
===========

Introduction
========
**WhiteRabbit** is a small application that can be used to analyse the structure and contents of a database as preparation for designing an ETL. It comes with **RabbitInAHat**, an application for interactive design of an ETL to the OMOP Common Data Model with the help of the the scan report generated by White Rabbit. 

# Changes in Fork

This Fork contains added support for InterSystems IRIS 2021.1



As the IRIS JDBC driver is not on maven central repo, the POM.xml uses a locally provided driver, which needs to be installed in the repo:

```
mvn install:install-file -Dfile=intersystems-jdbc-3.2.0.jar -DgroupId=com.intersystems -DartifactId=intersystems-jdbc -Dversion=3.2.0 -Dpackaging=jar
```

To Run, you need to edit the file .\iniFileExamples\WhiteRabbit-IRIS.in and change the values for the server, username, password and table schema to scan:

```
DATA_TYPE = IRIS                              # Database Vendor to use
SERVER_LOCATION = 127.0.0.1:1972/MYNAMESPACE # Format is "Server:Port/Namespace" [Optionally /jdbc.log for logging]
USER_NAME = _SYSTEM                           # User name for the database 
PASSWORD = SYS                                # Password for the database 
DATABASE_NAME = MYDBSCHEMA                    # Name of the data schema (Class Packages) used by the tables to scan.
```

Run the command line version with:

```
.\dist\bin\whiterabbit.bat -ini .\iniFileExamples\WhiteRabbit-IRIS.ini
```

To Run the GUI version, Java11 is recommended (as Java 8 does not scale well Swing applications on higher DPI displays, and the UI gets very small).

Features
========

- Can scan databases in SQL Server, Oracle, PostgreSQL, MySQL, MS Access, Amazon RedShift, Google BigQuery, SAS files and CSV files
- The scan report contains information on tables, fields, and frequency distributions of values
- Cutoff on the minimum frequency of values to protect patient privacy
- WhiteRabbit can be run with a graphical user interface or from the command prompt
- Interactive tool (Rabbit in a Hat) for designing the ETL using the scan report as basis
- Rabbit in a Hat generates ETL specification document according to OMOP template

Screenshots
===========
<table border = "">
<tr valign="top">
<td width = 50%>
  <img src="https://github.com/OHDSI/WhiteRabbit/blob/master/docs/images/WRScreenshot.png" alt="White Rabbit" title="White Rabbit" />
</td>
<td width = 50%>
 <img src="https://github.com/OHDSI/WhiteRabbit/blob/master/docs/images/RIAHScreenshot.png" alt="Rabbit in a Hat" title="Rabbit in a Hat" />
</td>
</tr><tr>
<td>White Rabbit</td><td>Rabbit in a Hat</td>
</tr>
</table>

Technology
============
White Rabbit and Rabbit in a Hat are pure Java applications. Both applications use [Apache's POI Java libraries](http://poi.apache.org/) to read and write Word and Excel files. White Rabbit uses JDBC to connect to the respective databases.

System Requirements
============
Requires Java 1.8 or higher, and read access to the database to be scanned. Java can be downloaded from
<a href="http://www.java.com" target="_blank">http://www.java.com</a>.

Dependencies
============
For the distributable packages, the only requirement is Java 8. For building the package, also Maven is needed.

Getting Started
===============
WhiteRabbit

1. Under the [Releases](https://github.com/OHDSI/WhiteRabbit/releases) tab, download `WhiteRabbit*.zip`
2. Unzip the download
3. Double-click on `bin/whiteRabbit.bat` on Windows to start White Rabbit, and `bin/whiteRabbit` on macOS and Linux.

(See [the documentation](http://ohdsi.github.io/WhiteRabbit/WhiteRabbit.html#running-from-the-command-line) for details on how to run from the command prompt instead)

Rabbit-In-A-Hat

1. Using the files downloaded for WhiteRabbit, double-click on `bin/rabbitInAHat.bat` to start Rabbit-In-A-Hat on Windows, and `bin/rabbitInAHat` on macOS and Linux.

Note: on releases earlier than version 0.8.0, open the respective `WhiteRabbit.jar` or `RabbitInAHat.jar` files instead.

Example in- and output
========
The file `examples.zip` contains a set of input and output examples for White Rabbit and Rabbit in a Hat.
These are used for testing of the main White Rabbit and Rabbit in a Hat features. An overview is given in below table.

| Folder         | Description                                                                                                                                                                                                                                                                                                                                              |
|:---------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `wr_input_csv` | csv files to test scanning on different data types and long table names.                                                                                                                                                                                                                                                                                 |
| `wr_input_sas` | sas7bdat files to test sas input                                                                                                                                                                                                                                                                                                                         |
| `wr_output`    | Scan reports created from files in `wr_input_csv`, `wr_input_sas` and [native a Synthea database loaded in Postgres](https://github.com/ohdsi/ETL-Synthea). All with default scan options.<br> This folder also includes fake data generated from the csv scan report. The csv scan report is used to test the opening a Scan Report in Rabbit in a Hat. |
| `riah_input`   | An example mapping file used to create the Rabbit in a Hat outputs.                                                                                                                                                                                                                                                                                      |
| `riah_output`  | All export formats created by Rabbit in a Hat: as word, html, markdown, sql skeleton and the R TestFramework.<br> These are all generated from `riah_input/riah_mapping_example.gz`.                                                                                                                                                                     |


Getting Involved
=============
* User guide and Help: [WhiteRabbit documentation](http://ohdsi.github.io/WhiteRabbit)
* Developer questions/comments/feedback: [OHDSI Forum](http://forums.ohdsi.org/c/developers)
* We use the [GitHub issue tracker](../../issues) for all bugs/issues/enhancements
* Historically, all files have CRLF line endings. Please configure your IDE and local git to keep line endings as is. This avoids merge conflicts.

License
=======
WhiteRabbit is licensed under Apache License 2.0

Development
===========
White Rabbit and Rabbit in a Hat are structured as a Maven package and can be developed in Eclipse. Contributions are welcome.

To generate the files ready for distribution, run `mvn install`.

### Development status

Production. This program is being used by many people.
