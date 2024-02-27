# สร้าง URL หรือเพจสำหรับรับข้อมูล Callback


[« กลับหน้าหลัก](../README.md)


ในการสร้าง URL ในการรับข้อมูลจะต้องตรงกันกับ URL ที่กำหนดในช่อง  CALLBACK URL ในระบบ KKU IDHub

ซึ่งข้อมูลที่ได้รับจาก Callback ของ IDHub ผ่าน GET Parameter หรือ ​Query String จะมี  2 อย่างได้แก่
- code
- state *ผู้ใช้งานกำหนดเองในขั้นตอนการสร้างลิ้งค์ Login*

การตรวจสอบหรือดึงข้อมูลผู้ Login สามารถทำได้โดยการ ***POST Request*** ไปที่ 
```
https://idhub.kku.ac.th/api/v1/oauth2/token
```



โดยการตรวจสอบข้อมูลจะแบ่งออกเป็น 2 รูปแบบได้แก่
- [รูปแบบ Scope ทั่วไป](_3.2_callbackUriScope.md)
- [Open ID *(JWT Token)*](_3.1_callbackUriOpenID.md)

ซึ่งทั้งสองแบบจะใช้การพัฒนาโปรแกรมที่แตกต่างกัน สามารถใช้งานได้ตามความเหมาะสม



ทำการเพิ่ม Route โดยตัวอย่างโค้ดต่อไปนี้

```javascript
const axios = require('axios');
const qs = require('qs');

app.get('/thaid-callback', async (req, res) => {

  let code = req.query.code
  let state = req.query.state

  try {
    let data = qs.stringify({
      'client_id': '<CLIENT_ID>',
      'client_secret': '<CLIENT_SECRET>',
      'grant_type': 'authorization_code',
      'response_type': 'code',
      'redirect_uri': '<Recirect URL>',
      'code': code
    });

    let config = {
      method: 'post',
      url: 'https://idhub.kku.ac.th/api/v1/oauth2/token',
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded',
        'cache-control': 'no-cache'
      },
      data: data
    };

    axios.request(config)
      .then((response) => {

        req.session.userData = response.data
        console.log(response.data)



      })
      .catch((error) => {
        console.log("Error", error.response.data);
        res.send(error.response.data.message);
      });

  } catch (error) {
    console.error(error);
    res.status(500).send(error);
  }
})
```