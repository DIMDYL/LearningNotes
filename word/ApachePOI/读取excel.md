## 依赖

```java
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi</artifactId>
    <version>5.0.0</version>
</dependency>
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.0.0</version>
</dependency>
```

## 读取Excel

```java
public static void reed() throws Exception {
    FileInputStream in = new FileInputStream(new File("F:\\ME\\demo.xlsx"));
    // 通过输入流读取指定的excel文件
    XSSFWorkbook excel = new XSSFWorkbook(in);
    // 获取excel的第一个sheet
    XSSFSheet sheet = excel.getSheetAt(0);
    // 获取sheet页中的最后一行行号
    int last = sheet.getLastRowNum();
    for (int i = 0; i < last; i++) {
        // 获取sheet页面中的行
        XSSFRow titlrrow = sheet.getRow(i);
        // 获取第二个单元格
        XSSFCell celi1 = titlrrow.getCell(1);
        // 获取第二个单元格的值
        System.out.println(celi1.getStringCellValue());
    }
    excel.close();
    in.close();
}
```