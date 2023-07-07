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

	<th>Age</td>
	
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
- #### testing 
- asdfasf 
- Testing testing from bill-bo-baggins
- 