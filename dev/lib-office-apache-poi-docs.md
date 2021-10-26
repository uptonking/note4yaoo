---
title: lib-office-apache-poi-docs
tags: [apache-poi, docs]
created: '2019-08-01T16:03:46.386Z'
modified: '2021-05-13T02:43:55.877Z'
---

# lib-office-apache-poi-docs

# dev-tips

- SS Usermodel同时支持HSSF和XSSF，老的HSSF Usermodel不推荐使用，org.apache.poi.ss.usermodel 基于 x.poi.hssf.usermodel
- Sheet.getLastRowNum(): 获取sheet中最后一行数据的索引，包含，基于0开始，一般是行数-1
- getPhysicalNumberOfRows()：the number of physically defined rows in this sheet. Not include the empty row，一般是行数
- Row.getLastCellNum(): 获取该行中最后一个单元格的索引+1，不包含，基于0开始
- MissingCellPolicy默认值是RETURN_NULL_AND_BLANK 
- rowIterator and cellIterator 会跳过空行和空单元格
- 利用poi写excel

``` java
//创建工作簿
HSSFWorkbook workbook=new HSSFWorkbook();
//新建工作表
HSSFSheet sheet=workbook.createSheet("刘洋");
//创建行，行号作为参数，第一行从0开始计算
HSSFRow row=sheet.createRow(0);
//创建单元格，row已经确定行号，列好作为参数，第一列从0开始计算
HSSFCell cell=row.createCell(2);
//设置单元格（第一行第三列）
cell.setCellValue("hello word");
//写入本地文件
FileOutputStream outputStream=new FileOutputStream("d:\\工作簿.xls");
workbook.write(outputStream);
outputStream.close();
```

- 利用poi读excel

``` java
FileInputStream inputStream=new FileInputStream("d:\\工作簿.xls");
//将输入流转换为workbook
HSSFWorkbook workbook=new HSSFWorkbook(inputStream);
//获取工作表
HSSFSheet sheet=workbook.getSheetAt(0);
//获取行
HSSFRow row=sheet.getRow(0);
//获取单元格（第一行第三列）
HSSFCell cell=row.getCell(2);
System.out.println("单元格内容为:"+cell.getStringCellValue());
```

- poi操作表格索引相关
  - sheet开始于0
  - 获取有效行数：sheet.getLastRowNum(); 
  - 获取一行的有效列数：row.getLastCellNum(); 
- excel的结构   
  - HSSFWorkbook -> HSSFSheet -> HSSFRow -> HSSFCell
- poi提供6种单元格类型
  - Cell. CELL_TYPE_NUMERIC	
  - Cell. CELL_TYPE_STRING	
  - Cell. CELL_TYPE_BOOLEAN	
  - Cell. CELL_TYPE_FORMULA	
  - Cell. CELL_TYPE_ERROR	
  - Cell. CELL_TYPE_BLANK	
- 操作excel图表的3种思路
  - 定义包含图表的excel模板，通过改变数据来改变图表
  - jfreechart + poi ：先生成图表图片，再插入excel，每次修改图表都要重新生成图片插入excel
  - java调用vbs，vbs调用excel的宏。
- poi-like library
  - Apache Tika是一个通用的文件解析工具，能够提取文件的元数据和内容
    - 应用场景包括搜索引擎的索引
  - jxl / jexcelapi 纯java读写excel
    - 已停止维护
    - 不支持excel2007
    - 效率较低，但运行稳定，支持读取大文件
    - 对图形、图像的支持不如poi
  - In Apache Cocoon, there is the HSSF Serializer, which takes in XML (in the gnumeric format), and outputs an XLS file for you.

# faq

- CTWorkbook?

- 发现了这个问题，50万条数据，easyExcel耗时接近7分钟，自己直接用Apache的poi解析只耗时21秒，同一台机器；10万条数据，easyExcel耗时94秒，自己直接用poi解析用时5秒。当然我们用的是dom解析，内存消耗会大一些

- 如何判断单元格是否是日期
  - Excel stores dates as numbers therefore the only way to determine if a cell is actually stored as a date is to look at the formatting. There is a helper method in HSSFDateUtil that checks for this.
  - http://poi.apache.org/help/faq.html. 8th

# poi dev

- 使用poi的XSSFWorkbook来生成excel很占内存，当数据量很大的时候，直接导致了频繁的Full GC，最终会导致OOM。 即使最终的成功下载excel，耗时也比较高，20W行的excel大约需要18s，40w行的时候OOM
  - 解决方案是用SXSSFWorkbook
- poi 空单元格 处理策略
  - Enum Row. MissingCellPolicy
      - CREATE_NULL_AS_BLANK: If the Cell returned doesn't exist, instead of returning null, create a new Cell with a cell type of "blank". This can help avoid NullPointerExceptions
      - RETURN_NULL_AND_BLANK: return null for cells that don't really exist and return the blank Cell if it exists but its cell type is blank
      - RETURN_BLANK_AS_NULL: Even if the cell exists but has a cell type of "blank", return null. This can allow you ignore blank cells
- 用 CellIterator 遍历 row 的单元格时，当碰到空(没有定义，没有编辑过)的单元格时, CellIterator.next()读取的是空单元格右边有内容的单元格，也就是说跳过了空的单元格
  - 如果需要处理所有的单元格，即不管该单元格有没有定义或内容，那么应该用普通的for循环配合getRow(), getCell()方法和MissingCellPolicy策略来循环整个Excel文件的单元格
  - 使用 for(Row r: sheet) 遍历单元格也会跳过空单元格，因为foreach循环的本质是iterator
- 读取时兼容03和07格式不同直接用inputstream
  - https://flysnowxf.iteye.com/blog/1533644
- 数值类型的处理
  - 通过POI取出的数值默认都是double，即使excel单元格中存的是1，取出来的值也是1.0
  - 要获取整数，需要自行处理
- 日期类型的处理
  - 可以通过cell.getCellStyle().getDataFormat()来判断
  - 如果单元格数据格式是自定义的日期格式，那么通过DateUtil.isCellDateFormatted(cell)判断不出来，而且该单元格还是一个数值单元格，返回一个double值
  - poi在Cell. CELL_TYPE_NUMERIC中又具体区分了类型，Date类型就是其中一种
- POI操作目前存在的03和07两种版本的Excel有不同的实现方式，而对于相同版本的Excel又分为User Model和Event Model两种
  - http://poi.apache.org/components/spreadsheet/index.html
- excel导入导出总结
  - https://zhuanlan.zhihu.com/p/27064597
- UserModel是类似于DOM的方式
  - 将文件全部读入内存, 对文件内部的结构进行建模成一颗DOM树
  - Workbook -> Sheet -> Row -> Cell
  - 优点
    - 解析excel简单
  - 缺点
    - 一次性将文件读入内存，每行、每单元格都是对象，内存消耗大
- Event Model是类似于SAX的方式
  - 边读取边解析, 并且不会将这些数据封装成Row, Cell这样的对象，而都只是普通的数字或者是字符串，并且这些解析出来的对象是不需要一直驻留在内存中, 而是解析完使用后就可以回收
  - SharedStringsTable用来存储字符串常量，具体的单元格的值是存储实际是SST中的下标
  - xlsx的Event Model是可以指定sheet来解析的. 并且是以1为第一个sheet.
  - 如果单元格里没有值, 则不会有v标签. 在真正解析的时候要考虑到这个因素
  - User Model也是基于Event Model. 只不过是抽象层级更高. 所以理论上的Event Model是可以实现所有User Model的功能.
  - 优点
    - 内存消耗小
  - 缺点
    - 只能一次性的解析所有的sheet数据.不能分页解析.
      - 换页的时候,Cell对应的行号会变成0.我们可以通过这个方案,来判断到了第几个Sheet
    - 解析Row中数据的时候,并不会解析空Cell
    - 先解析了所有的Row,然后才解析了Cell.而不是RowCell的嵌套关系.
- Event User Model 模式
  - User Event Model不再面对Element的事件编程, 而是面向StartRow, EndRow, Cell等事件编程. 而提供的数据, 也不再像之前是原始数据, 而是全部格式化好, 方便开发者开箱即用
- misc
  - 在Excel单元格里写的19. 从Cell里get出来可能是19.0。这是因为在Excel的存储中, 数据和格式是分开存储的.
    - 如果你不使用这个单元格中使用的格式(DataFormatter)来解析单元格里的值,就会出现这种问题.
  - 读文件时尽量直接使用File，而不使用InputStream
    - When opening a workbook, either a .xls HSSFWorkbook, or a .xlsx XSSFWorkbook, the Workbook can be loaded from either a File or an InputStream. 
    - Using a File object allows for lower memory consumption, while an InputStream requires more memory as it has to buffer the whole file.
    - http://poi.apache.org/components/spreadsheet/quick-guide.html#FileInputStream

      

# Apache POI - HSSF and XSSF Limitations  

- known limitations of the POI HSSF and XSSF APIs:    

- file size & memory usage      
  - There are some inherent limits in the Excel file formats.   
  - These are defined in class SpreadsheetVersion.    
  - As long as you have enough main-memory, you should be able to handle files up to these limits.  

- Excel2007
  - The total number of available rows is 1048576 (2^20/1M)
  - The total number of available columns is 16384 (2^14/16K)
  - The maximum number of arguments to a function is 255
  - Number of conditional format conditions on a cell is unlimited (actually limited by available memory in Excel)
  - Number of cell styles is 64000
  - Length of text cell contents is 32767

- Excel97 format aka BIFF8
  - The total number of available rows is 65536 (2^16/64K)
  - The total number of available columns is 256 (2^8)
  - The maximum number of arguments to a function is 30
  - Number of conditional format conditions on a cell is 3
  - Number of cell styles is 4000
  - Length of text cell contents is 32767

- There are ways to overcome the main-memory limitations if needed:   
  - For writing very huge files, there is SXSSFWorkbook which allows to do a streaming write of data out to files.
  - For reading very huge files, take a look at the sample XLSX2CSV which shows how you can read a file in streaming fashion.

- charts   
  - HSSF has some limited support for creating a handful of very simple Chart types, but largely this isn't supported. HSSF (largely) doesn't support changing Charts.
  - XSSF has only limited chart support including making some simple changes and adding at least some line and scatter charts

- Macros  
  - Macros can not be created. The are currently no plans to support macros. 
  - However, reading and re-writing files containing macros will safely preserve the macros.  

- pivot table  
  - HSSF doesn't have support for reading or creating Pivot tables. 
  - XSSF has limited support for creating Pivot Tables, and very limited read/change support.

# poi docs

http://poi.apache.org/components/spreadsheet/index.html  

## overview

- HSSF is the POI Project's pure Java implementation of the Excel '97(-2007) file format. 
- XSSF is the POI Project's pure Java implementation of the Excel 2007 OOXML (.xlsx) file format.
- HSSF and XSSF provides ways to read and write XLS spreadsheets. They provide:
  - low level structures for those with special needs
  - an eventmodel api for efficient read-only access，只读
  - a full usermodel api for creating, reading and modifying XLS files，可读可写
- the usermodel system has a higher memory footprint than the low level eventusermodel
- as the new XSSF supported Excel 2007 OOXML (.xlsx) files are XML based, the memory footprint for processing them is higher than for the older HSSF supported (.xls) binary files.
- Since 3.8-beta3, POI provides a low-memory footprint `SXSSF` API built on top of XSSF.
  - SXSSF is an API-compatible streaming extension of XSSF to be used when very large spreadsheets have to be produced, and heap space is limited
  - SXSSF achieves its low memory footprint by limiting access to the rows that are within a sliding window, while XSSF gives access to all rows in the document.
  - Older rows that are no longer in the window become inaccessible, as they are written to the disk.
  - SXSSF limitations when compared to XSSF
    - Only a limited number of rows are accessible at a point in time.
    - Sheet.clone() is not supported.
    - Formula evaluation is not supported
    - SXSSF flushes sheet data in temporary files (a temp file per sheet) and the size of these temporary files can grow to a very large value. For example, for a 20 MB csv data the size of the temp xml becomes more than a gigabyte

## formula support

- poi aims to support the complete excel grammar for formulas. Thus, the string that you pass in to the setCellFormula call should be what you expect to type into excel. Also, note that you should NOT add a "=" to the front of the string.
- localized versions of Excel allow to enter localized function-names. 
  - However internally Excel stores the English names and thus POI only supports these and not the localized ones. 
  - Also note that only commas may be used to separate arguments, as per the Excel English style, alternate delimeters used in other localizations are not supported.
- Supported Features
  - References: single cell & area, 2D & 3D, relative & absolute
  - Literals: number, text, boolean, error and array
  - Operators: arithmetic and logical, some region operators
  - Built-in functions: over 350 recognised, 280 evaluatable
  - Add-in functions: 24 from Analysis Toolpack
  - Array Formulas: via Sheet.setArrayFormula() and Sheet.removeArrayFormula()
  - Region operators: union, intersection
- Not yet supported
  - Manipulating table formulas (In Excel, formulas that look like "{=...}" as opposed to "=...")
  - Parsing of previously uncalled add-in functions
  - Preservation of whitespace in formulas (when POI manipulates them)
- Supported Functions
  - org.apache.poi.ss.formula.eval. FunctionEval
    - getSupportedFunctionNames()
    - getNotSupportedFunctionNames()
- Formulas in Excel are stored as sequences of tokens in Reverse Polish Notation order. (逆波兰表示法，简写为RPN)
- Formula tokens in Excel are stored in one of three possible operand classes : Reference, Value and Array. 

## Formula Evaluation

- The Excel file format (both .xls and .xlsx) stores a "cached" result for every formula along with the formula itself. This means that when the file is opened, it can be quickly displayed, without needing to spend a long time calculating all of the formula results. 
- Generally you should have to create only one FormulaEvaluator instance per Workbook.
- If you do end up making changes to cells part way through evaluation, you should call notifySetFormula or notifyUpdateCell to trigger suitable cache clearance. 
- You should normally perform all of your updates to cells, before triggering the evaluation, rather than doing one cell at a time. 
- If you are using POI 3.13 final or newer, formula evaluation is possible with SXSSF, but with some caveats.
  - The biggest restriction is that, since evaluating a cell needs that cell in memory and any others it depends on, only pure-function formulas and formulas referencing nearby cells can be evaluated with SXSSF. If a formula references a cell that hasn't yet been written, or one which has already been flushed to disk, then it won't be possible to evaluate it.
  - it is suggested to evaluate formula cells just after writing them, or shortly after when cells they depend on are added. Just make sure that all cells needing or needed for evaluation are inside the window.

    

## misc

- User defined functions allow you to take code that is written in VBA and re-write in Java and use within POI.
- Record Generator was born from frustration with translating the Excel records to Java classes
  - The record generator takes XML as input and produces the following output:
    - A Java file capable of decoding and encoding the record.
    - A test class that provides a fill-in-the-blanks implementation of a test case for ensuring the record operates as designed.
  - The record generator is invoked as an Ant target (generate-records)
  - The record generation works by taking an XML file and styling it using XSLT.
  - The record generator does not handle all possible record types and goes not intend to perform this function.
  - When dealing with a non-standard record sometimes the cost-benefit of coding the record by hand will be greater than attempting modify the generator

## poi components

- POIFS is the oldest and most stable part of POI. All of our components for the binary (non-XML) Microsoft Office formats ultimately rely on it by definition.
- HSSF and XSSF for Excel Documents
- HWPF and XWPF for Word Documents
- HSLF and XSLF for PowerPoint Documents
- HPSF is our port of the OLE 2 property set format to pure Java. Property sets are mostly use to store a document's properties (title, author, date of last modification etc.)
- HDGF and XDGF for Visio Documents
- HPBF is our port of the Microsoft Publisher 98(-2007) file format to pure Java
- HMEF is our port of the Microsoft TNEF (Transport Neutral Encoding Format) file format to pure Java. TNEF is sometimes used by Outlook for encoding the message
- HSMF for Outlook Messages

## Quick Guide

- Files vs InputStreams
  - When opening a workbook, either a .xls HSSFWorkbook, or a .xlsx XSSFWorkbook, the Workbook can be loaded from either a File or an InputStream. 
  - Using a File object allows for lower memory consumption, while an InputStream requires more memory as it has to buffer the whole file.

# changelog

- ref
  - http://poi.apache.org/changes.html  

- breaking
  - POI 4.0 and later require JDK version 1.8 or later.
  - POI 3.11 and later 3.x versions require JDK version 1.6 or later.
  - POI 3.5 to 3.10 required the JDK version 1.5 or later. 
  - Versions prior to 3.5 required JDK 1.4+.

- 4.1.0-201902
  - XSSF Support GEOMEAN function
  - SVG image support in XSLF
- 4.0.0-20180907
  - Removed support for Java 6 and 7 making Java 8 the minimum version supported
  - New OOXML schema (1.4) necessary, because of incompatible XMLBeans loading not anymore through POIXMLTypeLoader
  - Remove OPOIFS* (breaks backwards compatibility)
  - XSSF Do not fail with "part already exists" when tables are created/removed (breaks backwards compatibility)
- 3.17-20170915
  - Various modules: add sanity checks and fix infinite loops / OOMs caused by fuzzed data
  - OPC: fix linebreak handling on XML signature calculation (#61182)
  - SS Common: fix number formatting (github-43/52, #60422)
  - SXSSF: fix XML processing - unicode surrogates and line breaks (#61048, #61246)
- 3.0-20070518
  - Detect Office 2007 XML documents, and throw a meaningful exception
- 2.0-20040126
- 1.0.0-20011230
- 0.1-20010828
