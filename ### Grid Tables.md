### Grid Tables

Grid tables are made up of special characters which form the rows and columns, and also change table and style variables.

Complex information can be conveyed by using the following features not found in other table styles:
* spanning columns
* adding footers
* adding intra-cellular body elements

Grid table syntax uses the characters "-", "=", "|", and "+" to represent the table outline:
* Hyphens (-) separate horizontal rows.
* Equals signs (=) produce a header when used to create the row under the header text.
* Equals signs (=) create a footer when used to enclose the last row of the table.
* Vertical bars (|) separate columns and also adjusts the depth of a row. 
* Plus signs (+) indicates a juncture between horizontal and parallel lines.

Note: Inserting a colon (:) at the boundaries of the separator line after the header will change text alignment. If there is no header, insert colons into the top line.

Sample grid table:

+-------------------+------------+----------+----------+
| Header 1          | Header 2   | Header 3 | Header 4 |
|                   |            |          |          |
+:=================:+:==========:+:========:+:========:+
| row 1, column 1   | column 2   | column 3 | column 4 |
+-------------------+------------+----------+----------+
| row 2             | cells span columns               |
+-------------------+------------+---------------------+
| row 3             | cells      | - body              |
+-------------------+ span rows  | - elements          |
| row 4             |            | - here              |
+===================+============+=====================+
| Footer                                               |
+===================+============+=====================+
