---
layout: post 
title: "TableExport Option"
date: 2017-07-15 22:34:05 +0800
categories: [Web]
excerpt: BootstrapTable之TableExport扩展插件的option说明文档
tags:
  - Web
  - 前端
  - Bootstrap
  - Export
---

All could be found in [gitHub](https://github.com/hhurz/tableExport.jquery.plugin).
Or read `README.md` in tableExport.jquery.plugin-master

```
consoleLog: false
csvEnclosure: '"'
csvSeparator: ','
csvUseBOM: true
displayTableName: false
escape: false
excelstyles: []
excelFileFormat: 'xlshtml'
fileName: 'tableExport'
htmlContent: false
ignoreColumn: []
ignoreRow: []
jsonScope: 'all'
jspdf: orientation: 'p'
       unit:'pt'
       format: 'a4'
       margins: left: 20
                right: 10
                top: 10
                bottom: 10
       onDocCreated: null
       autotable: styles: cellPadding: 2
                          rowHeight: 12
                          fontSize: 8
                          fillColor: 255
                          textColor: 50
                          fontStyle: 'normal'
                          overflow: 'ellipsize'
                          halign: 'left'
                          valign: 'middle'
                  headerStyles: fillColor: [52, 73, 94]
                                textColor: 255
                                fontStyle: 'bold'
                                halign: 'center'
                  alternateRowStyles: fillColor: 245
                  tableExport: doc: null
                               onAfterAutotable: null
                               onBeforeAutotable: null
                               onAutotableText: null
                               onTable: null
                               outputImages: true
numbers: html: decimalMark: '.'
               thousandsSeparator: ','
         output: decimalMark: '.',
                 thousandsSeparator: ','
onCellData: null
onCellHtmlData: null
onIgnoreRow: null
onMsoNumberFormat: null
outputMode: 'file'
pdfmake: enabled: false
         docDefinition: pageOrientation: 'portrait'
                        defaultStyle: font: 'Roboto'
         fonts: {}
tbodySelector: 'tr'
tfootSelector: 'tr'
theadSelector: 'tr'
tableName: 'myTableName'
type: 'csv'
worksheetName: 'WorksheetName'
```

> ignoreColumn can be either an array of indexes (i.e. [0, 2]) or field names (i.e. ["id", "name"]).
> Indexes correspond to the position of the header elements th in the DOM starting at 0. (If the th elements are removed or added to the DOM, the indexes will be shifted so use the functionality wisely!)
> Field names should correspond to the values set on the "data-field" attribute of the header elements th in the DOM.
> "Nameless" columns without data-field attribute will be named by their index number (converted to a string)
> To disable formatting of numbers in the exported output, which can be useful for csv and excel format, set the option numbers: output to false.
> Set the option excelFileFormat to 'xmlss' if you want to export in XML Spreadsheet 2003 file format. Use this format if multiple tables should be exported into a single file. Excel 2000 html format is the default excel file format which has better support of exporting table styles.
> The excelstyles option lets you define the css attributes of the original html table cells, that should be taken over when exporting to an excel worksheet (Excel 2000 html format only).
> To export in XSLX format protobi/js-xlsx forked from SheetJS/js-xlsx is used. Please note that the implementation of this format type lets you only export table data, but not any styling information of the html table.
> For jspdf options see the documentation of jsPDF and jsPDF-AutoTable resp.
There is an extended setting for jsPDF option 'format'. Setting the option value to 'bestfit' lets the tableExport plugin try to choose the minimum required paper format and orientation in which the table (or tables in multitable mode) completely fits without column adjustment.
> Also there is an extended setting for the jsPDF-AutoTable options 'fillColor', 'textColor' and 'fontStyle'. When setting these option values to 'inherit' the original css values for background and text color will be used as fill and text color while exporting to pdf. A css font-weight >= 700 results in a bold fontStyle and the italic css font-style will be used as italic fontStyle.
> When exporting to pdf the option outputImages lets you enable or disable the output of images that are located in the original html table.
> Optional html data attributes (can be applied while generating the table that you want to export)
> * data-tableexport-display
	<table style="display:none;" data-tableexport-display="always">...</table> -> a hidden table will be exported
	<td style="display:none;" data-tableexport-display="always">...</td> -> a hidden cell will be exported
	<td data-tableexport-display="none">...</td> -> this cell will not be exported
	<tr data-tableexport-display="none">...</tr> -> all cells of this row will not be exported

> * data-tableexport-msonumberformat
	<td data-tableexport-msonumberformat="\@">...</td> -> data value will be used to style excel cells with mso-number-format (Excel 2000 html format only)
	Examples:
    "\@"       excel treats cell content alway as text, even numbers
    "0"        excel will display no decimals for numbers
    "0\.000"   excel displays numbers with 3 decimals
    "0%"       excel will display a number as percent with no decimals
    "Percent"  excel will display a number as percent with 2 decimals

> * data-tableexport-value
	<th data-tableexport-value="export title">title</th> -> "export title" instead of "title" will be exported
	<td data-tableexport-value="export content">content</td> -> "export content" instead of "content" will be exported
