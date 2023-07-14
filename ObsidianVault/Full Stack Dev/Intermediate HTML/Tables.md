reference: https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables/Advanced#active_learning_adding_table_structure


#### Design Flow
- Tables are populated by rows, this needs to be taken in consideration when placing information in specific columns
#### Syntax

```html
<table>

<tr>

	<th>Breed</td>
	
	<td>Jack Russell</td>
	
	<td>Poodle</td>
	
	<td>Streetdog</td>
	
	<td>Cocker Spaniel</td>

</tr>

<tr>

	<th>Age</tddd an exclamation mark ( ! ) in front of an Internal link. You can embed files in any of the Accepted file for>
	
	<td>16</td>
	
	<td>9</td>
	
	<td>10</td>
	
	<td>5</td>

</tr>

<tr>
	
	<th>Owner</td>
	
	<td>Mother-in-law</td>
	
	<td>Me</td>
	
	<td>Me</td>
	
	<td>Sister-in-law</td>
	
</tr>

</table>
```
- here you can see  this rough output: ![[Pasted image 20230627115812.png]]
- tr indicates a row, td indicates "table data" and is an individual cell.
- Headers are handled with the `<th></th>` tag wherever a header is supposed to exist
- colspan and rowspan both allow cells to stretch or span into their respective neighboring cells. it's an attribute `<td colspan="2"></td>`. ex: ![[Pasted image 20230627125830.png]]

#### Editing Entire Column Style

- use the `<colgroup>` tag and a `<col>` for each column. 
- each column styled or not will need to be accounted for, empty columns can be left at `<col>` and styled ones look like: `<col style="background-color"/>`
- Place at  the top right underneath the table tag or a caption tag
	- ex: 
		- if you have two columns and want the second styled, you need a `<colgroup>` and `<col>` nested inside and `<col style="backgroundcolor: yellow;">` to accomplish this.
		- result: ![[Pasted image 20230707124341.png]]
### Advanced  Html tables

#### captions 
- use the tag `<caption>` inside of the table element right below the table tag.
	- This allows the screen readers and readers to determine before reading the cells of the table if the information will be pertinent for their use. 

#### Headers, footers, body table tags
- useful for styling but does not add anything visual or accessibility for screen readers on its own. 
	- thead, tbody, and tfoot must wrap the part of the table that is the header, body, and footer respectively. 
		- *note: for thead, did not encounter the use of it for headings on column, only on the row header.

#### Scope Attribute
- used to denote a header for either a column or a row as a group that is to be read together in the same context for the purpose of screen readers. 
- added to the `<th>` element example: 

 ``` html 
	  <thead>
  <tr>
    <th scope="col">Purchase</th>
    <th scope="col">Location</th>
    <th scope="col">Date</th>
    <th scope="col">Evaluation</th>
    <th scope="col">Cost (€)</th>
  </tr>
</thead>

```
- there are also `colgroup`, and `rowgroup` attributes instead that could be used for a header that spans over multiple columns but defined the header columns below it (eg. a clothes colgroup that defines the three shoes, hats, shirts header columns right below it)
	- note: the individual row or columns below the group are marked with `<th scope="col/row">` 
- You can also use `id` and `headers` attributes but look into the article above as a reference.[[Tables]]. 

##### Blank spaces
- use the `&nbsp;` as the content of the cell to leave a blank space and you can use `colspan` and `rowspan` to expand the blank cells.

#### Example Project
```html 
<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="utf-8">

<meta name="viewport" content="width=device-width">

<title>Table template</title>

<link href="minimal-table.css" rel="stylesheet" type="text/css">

</head>

<body>

<h1>Planets Table</h1>

  

<table>

<caption>Data about the planets of our solar system</caption>

<colgroup>

<col>

<col>

<col style="border-style: solid; border-color: black; border-width: 2px;"

</colgroup>

  

<thead>

<tr>

<td colspan="2">&nbsp;</td>

<th scope="col">Name</th>

<th scope="col">Mass (10<sup>24</sup>kg)</th>

<th scope="col">Diameter (km)</th>

<th scope="col">Density (kg/m<sup>3</sup>)</th>

<th scope="col">Gravity (m/s<sup>2</sup>)</th>

<th scope="col">Length of day (hours)</th>

<th scope="col">Distance from Sun (10<sup>6</sup>km)</th>

<th scope="col">Mean temperature (°C)</th>

<th scope="col">Number of moons</th>

<th scope="col">Notes</th>

</tr>

</thead>

<tbody>

<tr>

<th rowspan="4" colspan="2">terrestrial Planets</th>

<td>Mercury</td>

<td>0.330</td>

<td>4,879</td>

<td>5427</td>

<td>3.7</td>

<td>4222.6</td>

<td>57.9</td>

<td>167</td>

<td>0</td>

<td>Closest to the Sun</td>

</tr>

<tr>

<td>Venus</td>

<td>0.330</td>

<td>4,879</td>

<td>5427</td>

<td>3.7</td>

<td>4222.6</td>

<td>57.9</td>

<td>167</td>

<td>0</td>

<td></td>

</tr>

<tr>

<td>Earth</td>

<td>5.97</td>

<td>12,756</td>

<td>5514</td>

<td>9.8</td>

<td>4.0</td>

<td>149.6</td>

<td>15</td>

<td>1</td>

<td>Our world</td>

</tr>

<tr>

<td>Mars</td>

<td>0.642</td>

<td>6,792</td>

<td>3933</td>

<td>3.7 2</td>

<td>4.7</td>

<td>227.9</td>

<td>-65</td>

<td>2</td>

<td>The red planet</td>

</tr>

<tr>

<th rowspan="4">Jovian Planets</th>

<th rowspan="2">Gas Giants</th>

<td>Jupiter</td>

<td>1898</td>

<td>142,984</td>

<td>1326</td>

<td>23.1</td>

<td>9.9</td>

<td>778.6</td>

<td>-110</td>

<td>67</td>

<td>The largest planet</td>

</tr>

<tr>

<td>Saturn</td>

<td>568</td>

<td>120,536</td>

<td>687</td>

<td>9.0</td>

<td>10.7</td>

<td>1433.5</td>

<td>-140</td>

<td>62</td>

<td></td>

</tr>

<tr>

<th rowspan="2">Ice Giants</th>

<td>Uranus</td>

<td>86.8</td>

<td>51,118</td>

<td>1271</td>

<td>8.7</td>

<td>17.2</td>

<td>2872.5</td>

<td>-195</td>

<td>27</td>

<td></td>

</tr>

<tr>

<TD>Neptune</TD>

<TD>102</TD>

<TD>49,528</TD>

<TD>1638</TD>

<TD>11.0</TD>

<TD>16.1</TD>

<TD>4495.1</TD>

<TD>-200</TD>

<TD>14</TD>

<td></td>

</tr>

<tr>

<th colspan="2">Dwarf Planets</th>

<td>Pluto</td>

<td>0.0146</td>

<td>2,370</td>

<td>2095</td>

<td>0.7</td>

<td>153.3</td>

<td>5906.4</td>

<td>-225</td>

<td>5</td>

<td>Declassified as a planet in 2006, but this <a href="http://www.usatoday.com/story/tech/2014/10/02/pluto-planet-solar-system/16578959/">remains controversial</a></td>

</tr>

</tbody>

</table>

  
  
  

</body>

</html>
```

the output with some basic css styling see [[StylingTables]]

![[Pasted image 20230707124826.png]]

##### Good Habits to have
see resource on best practices on tables https://pencilandpaper.io/articles/ux-pattern-analysis-enterprise-data-tables/
