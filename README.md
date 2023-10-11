# Android Networking

## [Thư viện Volley](https://google.github.io/volley/)

`Các class sử dụng trong Volley:`<br>
**RequestQueue:** Là hàng đợi giữ các Request.<br>
**Request:** là lớp cơ sở của các Request trong Volley, chứa thông tin về request HTTP<br>
**StringRequest:** Kế thừa từ Request, là class đại diện cho request trả về String.<br>
**JSONObjectRequest:** Là HTTP request có response trả về là JSONObject.<br>
**JSONArrayRequest:** Là HTTP request có response trả về là JSONArray. <br>
**ImageRequest:** Là HTTP request có response trả về là Bitmap.<br>

`Install:`<br>

Trước tiên chúng ta phải import thư viện này vào Android Studio. 
Copy và paste dòng dưới đây là **dependencies** trong file **build.gradle** của module **app**

```java
implementation("com.android.volley:volley:1.2.1")
```

Nhấn Async Now để Android Studio download và nạp thư viện vào project.<br>
**`Lưu ý:`** *Để sử dụng Volley chúng ta phải cấp quyền Internet trong __AndroidManifest.xml__*
> **String Request**
## []()
