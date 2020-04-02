# vue_excel_export
Vue 导出表格内容至 Excel

<br><hr>
### 1. 安装三个依赖包
```shell
  npm install -S file-saver
  npm install -S xlsx
  npm install -D script-loader
```

### 2. 在项目中创建一个文件夹（比如vendor，一般是在src目录下创建）
把 `Blob.js` 和 `Export2Excel.js` 这两个文件夹放到新建的文件夹内。

### 3. 在页面中使用
`Export2Excel.js` 暴露了两个接口 `export_table_to_excel` 和 `export_json_to_excel`, 我们常用 `export_json_to_excel`。

```js
handleDownload() {
      console.log("导出文件");
      require.ensure([], () => {
        const { export_json_to_excel } = require("@/vendor/Export2Excel");
        const tHeader = ["姓名", "年龄"];   // Excel表头内容
        const filterVal = ["name", "age"];  // 页面表格的表头字段
        const list = this.desserts;   // this.desserts 为页面中的表格内容
        const data = this.formatJson(filterVal, list);
        export_json_to_excel(tHeader, data, "列表excel");   // 第三个参数为导出下载下来的Excel的名字
      });
    },
    formatJson(filterVal, jsonData) {
      return jsonData.map(v => filterVal.map(j => v[j]));
    }
  }
```