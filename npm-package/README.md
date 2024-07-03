# npm-package

##1. Multer

```bash
const multer = require('multer');
const path = require('path');

const upload = './images/'

const file_ext = path.extname('822588-Burqa-istock.jpg');
console.log(file_ext); //.jpg

const fileName = '822588-Burqa-istock.jpg'.replace(file_ext, '');
console.log(fileName); // 822588-Burqa-istock

const fileLower = '822588-Burqa-istock.jpg'.replace(file_ext, '').toLowerCase();
console.log(fileLower); // 822588-burqa-istock

const fileSplit = '822588-Burqa-istock.jpg'.replace(file_ext, '').toLowerCase().split(" ");
console.log(fileSplit); // [ '822588-burqa-istock' ]

const fileJoin = '822588-Burqa-istock.jpg'.replace(file_ext, '').toLowerCase().split(" ").join("-");
console.log(fileJoin); // 822588-Burqa-istock

const fileDate = '822588-Burqa-istock.jpg'.replace(file_ext, '').toLowerCase().split(" ").join("-") + "-" + Date.now();
console.log(fileDate); // 822588-burqa-istock-1658059040550
```
