# หลักสูตรการอบรมThaiD Connect และ KKU ID Hub สำหรับนักพัฒนาซอฟต์แวร์
## วันที่ 27 กุมภาพันธ์ 2567

[« กลับหน้าหลัก](../README.md)

**ติดตั้งโปรแกรม**
- NodeJS  https://nodejs.org/en/download
- VSCode https://code.visualstudio.com/download
- Postman https://www.postman.com/downloads/



**ติดตั้ง ExpressJS Framework**

โดยใช้คำสั่งต่อไปนี้:
```javascript
npm init
npm install express --save
npm install axios
npm install express-session
npm install ejs
npm install jwt-decode
```

สร้าง Folder ใหม่ในชื่อ **public** เพื่อใช้สำหรับการสร้างไฟล์ HTML และสร้างไฟล์ index.html 
```html
<!DOCTYPE html>
<html>
<head>
<title>Hello</title>
</head>
<body>

<h1>Hello KKU</h1>

</body>
</html>
```


**เริ่มต้นรันโปรแกรม**

สร้างไฟล์ index.js 
```javascript
const express = require('express');
const app = express();
const path = require('path');


app.engine('html', require('ejs').renderFile);

app.get("/", (req, res) => {
  res.render(__dirname + "/public/index.html", {

  });
})

app.listen(3000, () => {
  console.log('Server started on http://localhost:3000');
});
```

รัน WebServer ด้วยคำสั่ง
```
node index.js
```
จากนั้นทดลองเปิดใช้งานที่ 
> http://localhost:3000