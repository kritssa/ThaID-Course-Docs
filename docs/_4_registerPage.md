# หน้าลงทะเบียนพร้อมแสดงข้อมูลที่ได้รับจากระบบ KKU IDHub


[« กลับหน้าหลัก](../README.md)


ทำการสร้าง Route สำหรับหน้า Register
โดยตัวอย่างโค้ดต่อไปนี้

```javascript
app.get('/register', (req, res) => {

  console.log("Data", req.session.userData)
  let data = req.session.userData
  res.render(__dirname + "/public/register.html", data);
});
```

จากนั้นทำการสร้าง View สำหรับหน้า Register ดังนี้

```html
<!DOCTYPE html>
<html>

<head>
    <title>ลงทะเบียน</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
</head>

<body>

   
    <div class="container mt-5 ">
        <h1>แบบฟอร์มการลงทะเบียน</h1>
        <h5>มหาวิทยาลัยขอนแก่น</h5>


        <div class="row mt-5">
            <div class="col-4">
                <div class="mb-3">
                    <label for="titleTh" class="form-label">คำนำหน้า</label>
                    <input type="text" class="form-control" id="titleTh" value="<%=titleTh %>" disabled readonly>

                </div>
            </div>
            <div class="col-4">
                <div class="mb-3">
                    <label for="given_name" class="form-label">ชื่อ (ภาษาไทย)</label>
                    <input type="text" class="form-control" id="given_name" value="<%= given_name %>" disabled readonly>
                </div>
            </div>
            <div class="col-4">
                <div class="mb-3">
                    <label for="family_name" class="form-label">นามสกุล (ภาษาไทย)</label>
                    <input type="text" class="form-control" id="family_name" value="<%= family_name %>" disabled
                        readonly>
                </div>
            </div>

            <div class="col-4">
                <div class="mb-3">
                    <label for="titleTh" class="form-label">คำนำหน้า (ภาษาอังกฤษ)</label>
                    <input type="text" class="form-control" id="titleTh" value="<%=titleEn %>" disabled readonly>

                </div>
            </div>
            <div class="col-4">
                <div class="mb-3">
                    <label for="given_name" class="form-label">ชื่อ (ภาษาอังกฤษ)</label>
                    <input type="text" class="form-control disabled" id="given_name" value="<%= given_name_en %>"
                        disabled readonly>
                </div>
            </div>
            <div class="col-4">
                <div class="mb-3">
                    <label for="family_name" class="form-label">นามสกุล (ภาษาอังกฤษ)</label>
                    <input type="text" class="form-control" id="family_name" value="<%= family_name_en %>" disabled
                        readonly>
                </div>
            </div>
            <div class="col-12">
                <div class="mb-3">
                    <label for="address" class="form-label">ที่อยู่</label>
                    <textarea class="form-control" id="address"><%= address.formatted %></textarea>

                </div>
            </div>
            
            <div class="col-12 mt-4">
                <button type="button" class="btn btn-primary btn-lg">
                    ลงทะเบียน
                </button>
            </div>
        </div>
    </div>

</body>

</html>
```


ทำการเพิ่มการแสดงแผนที่จากข้อมูลที่อยู่ ด้วย Google Map API

```html

 <script>

        let map;
        let marker;
        let geocoder;
        let responseDiv;
        let response;

        function initMap() {
            map = new google.maps.Map(document.getElementById("map"), {
                zoom: 15,
                center: { lat: 13.7250482, lng: 100.3034428 },
                mapTypeControl: false,
            });
            geocoder = new google.maps.Geocoder();

            marker = new google.maps.Marker({
                map,
                draggable: true,
            });
            geocode({ address: "<%= address.formatted %>" })
            clear();
        }

        function clear() {
            marker.setMap(null);
        }

        function geocode(request) {
            clear();
            geocoder
                .geocode(request)
                .then((result) => {
                    const { results } = result;

                    map.setCenter(results[0].geometry.location);
                    marker.setPosition(results[0].geometry.location);
                    marker.setMap(map);
                    return results;
                })
                .catch((e) => {
                    alert("Geocode was not successful for the following reason: " + e);
                });
        }

        window.initMap = initMap;
    </script>


    <div class="col-12">
      <div class="mb-3">
        <label for="map" class="form-label">แผนที่</label>
      </div>
      <div id="map" style="height: 350px;">
      </div>
      <script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyBVPtwi0hDxww33nHMufUUvX9K5zqi9SD4&callback=initMap&v=weekly&solution_channel=GMP_CCS_geocodingservice_v1" defer></script>
    </div>
```