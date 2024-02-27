# สร้าง QR Code สำหรับใช้ในการสแกน

[« กลับหน้าหลัก](../readme.md)


โดยโครงสร้างของลิ้งค์ที่ใช้สำหรับการเชื่อมต่อข้อมูลมีดังนี้

```
https://idhub.kku.ac.th/api/v1/oauth2
```

### Parameter
- **response_type** =code
- **client_id** =ได้จากระบบ KKU ID Hub
- **redirect_uri** =เป็น Callback Url ที่ตรงกันกับระบบ KKU ID Hub




เมื่อนำมารวมกันจะได้เป็น

```
https://idhub.kku.ac.th/api/v1/oauth2/auth?response_type=code&client_id=<client_id>&redirect_uri=<calback_url>
```
