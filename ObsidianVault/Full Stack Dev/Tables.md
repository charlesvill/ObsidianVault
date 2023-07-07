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