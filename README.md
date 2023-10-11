# Android Networking

## Json
#### Các kiểu dữ liệu Json
- Number
- String
- Boolean
- Null
- Object
- Array

#### Định dạng dữ liệu Json
- Cú pháp json theo các qui định sau:
    - Dữ liệu gồm các cặp tên/giá trị
    - Dữ liệu được phân cách dấu phẩy "**,**"
    - Dấu ngoặc nhọn "**{ }**" dùng để giữ các đối tượng (object).
    - Dấu ngoặc vuông "**[ ]**" dùng để giữ các mảng (array)

- Dữ liệu được viết là các **cặp tên/giá trị**. Một cặp tên/giá trị gồm 1 trường tên đặt trong dấu nháy kép, 
tiếp theo là dấu hai chấm và tiếp theo là giá trị (giá trị có dấu nháy kép hay không tùy theo kiểu dữ liệu).

**Ví dụ:**
```json
"name": "json"
"age": 18
```

- Đối tượng JSON (JSON Object): được viết trong cặp dấu ngoặc nhọn "**{ }**". 
Trong một đối tượng có có nhiều cặp tên / giá trị phân cách nhau bằng dấu phẩy "**,**".

**Ví dụ:**
```json
{
    "id": 1,
    "name": "json",
    "age": 18,
    "isStudent": true
}
```

- Mảng JSON (JSON Array): được bọc trong dấu ngoặc vuông "**[ ]**".
Một mảng có thể chứa nhiều đối tượng (object).

**Ví dụ:**
```json
{
    "persons": [
        {
            "name": "Nguyen Van A",
            "age": 19
        },
        {
            "name": "Nguyen Van B",
            "age": 20
        }
    ]
}
```

#### Json Parser
- Tạo đối tượng JSONObject
```java
JSONObject jsonObject = new JSONObject(result);
```

- Lấy chuỗi
```java
String jsonString = jsonObject.getString("TenChuoi");
```

- Lấy boolean
```java
String jsonBoolean = jsonObject.getBoolean("TenBoolean");
```

- Lấy mảng
```java
JSONArray jsonArray = jsonObject.getJSONArray("TenArray");
```

- Lấy item từ mảng
```java
for (int i = 0; i < jsonArray.length; i++) {
    JSONObject object = jsonArray.getJSONObject(i);
    String item = object.getString("StringNameArray");
}
```

## [Thư viện Volley](https://google.github.io/volley/)

#### Các class sử dụng trong Volley:
- **RequestQueue:** Là hàng đợi giữ các Request.<br>
- **Request:** là lớp cơ sở của các Request trong Volley, chứa thông tin về request HTTP<br>
- **StringRequest:** Kế thừa từ Request, là class đại diện cho request trả về String.<br>
- **JSONObjectRequest:** Là HTTP request có response trả về là JSONObject.<br>
- **JSONArrayRequest:** Là HTTP request có response trả về là JSONArray. <br>
- **ImageRequest:** Là HTTP request có response trả về là Bitmap.<br>

#### Thêm thư viện Volley
Trước tiên chúng ta phải import thư viện này vào Android Studio. 
Copy và paste dòng dưới đây là **dependencies** trong file & **`build.gradle`** của module **app**

```java
implementation("com.android.volley:volley:1.2.1")
```

Nhấn **Async Now** để Android Studio download và nạp thư viện vào project.<br>
**Lưu ý:** *Để sử dụng Volley chúng ta phải cấp quyền Internet trong __`AndroidManifest.xml`__*
#### String Request
```java
// Instantiate the RequestQueue
RequestQueue queue = Volley.newRequestQueue(this);
String url = "https://www.google.com/";

// Request a string response from the provided URL.
StringRequest stringRequest = new StringRequest(
    Request.Method.GET, 
    url,
    new Response.Listener<String>() {
        @Override
        public void onResponse(String response) {
            // Display the first 500 character of the response string.
            textView.setText("Response is: " + response.substring(0, 500));
        }
    },
    new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            textView.setText(String.valueOf(error));
        }
    }
);

// Add the request to the RequestQueue
queue.add(stringRequest);
```

#### Json Object Request
```java
// Instantiate the RequestQueue
RequestQueue queue = Volley.newRequestQueue(this);
String url = "https://www.google.com/";

JsonObjectRequest jsonObjectRequest = new JsonObjectRequest(
    Request.Method.GET,
    url,
    null,
    new Response.Listener<JSONObject>() {
        @Override
        public void onResponse(JSONObject response) {
            textView.setText("Response: " + response.toString());
        }
    },
    new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            // TODO: Handle error

        }
    }
);

// Add the request to the RequestQueue
queue.add(jsonObjectRequest);
```

#### Json Array Request
```java
// Instantiate the RequestQueue
RequestQueue queue = Volley.newRequestQueue(this);
String url = "https://www.google.com/";

JsonArrayRequest jsonArrayRequest = new JsonArrayRequest(
    Request.Method.GET,
    url,
    null,
    new Response.Listener<JSONArray>() {
        @Override
        public void onResponse(JSONArray response) {
            for (int i = 0; i < response.length; i++) {
                // TODO: Get data in response

            }
        }
    },
    new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            // TODO: Handle error

        }
    }
);

// Add the request to the RequestQueue
queue.add(jsonArrayRequest);
```

#### String Request with method POST
```java
// Instantiate the RequestQueue
RequestQueue queue = Volley.newRequestQueue(this);
String url = "http://localhost:3000/users";

StringRequest stringRequest = new StringRequest(
    Request.Method.POST,
    url,
    new Response.Listener<String>() {
        @Override
        public void onResponse(String response) {
            textView.setText(response);
        }
    },
    new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            // TODO: Handler error
            Toast.makeText(MainActivity.this, "Error", Toast.LENGTH_SHORT).show();
        }
    }
) {
    @Nullable
    @Override
    protected Map<String, String> getParams() throws AuthFailureError {
        Map<String, String> params = new HashMap<String, String>();
        params.put("username", "admin");
        params.put("email", "example@gmail.com");
        params.put("password", "abc123");
        return params;
    }
};

// Add the request to the RequestQueue
queue.add(stringRequest);
```

#### Json Object Request with method POST
```java
// Instantiate the RequestQueue
RequestQueue queue = Volley.newRequestQueue(this);
String url = "https://www.google.com/";

JSONObject parameters = new JSONObject();
try {
    parameters.put("username", "admin");
    parameters.put("email", "example@gmail.com");
    parameters.put("password", "abc123");
} catch (JSONException e) {
    e.printStackTrace();
}

JsonObjectRequest jsonObjectRequest = new JsonObjectRequest(
    Request.Method.POST,
    url,
    parameters,
    new Response.Listener<JSONObject>() {
        @Override
        public void onResponse(JSONObject response) {
            String content = "";
            try {
                content += response.getString("username") + "\n";
                content += response.getString("email") + "\n";
                content += response.getString("password") + "\n";
                textView.setText(content);
            } catch (JSONException e) {
                e.printStackTrace();
            }
        }
    },
    new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            // TODO: Handler error
            Toast.makeText(MainActivity.this, "Error", Toast.LENGTH_SHORT).show();
        }
    }
);

// Add the request to the RequestQueue
queue.add(stringRequest);
```

## [Thư viện Retrofit](https://square.github.io/retrofit/)
- **Retrofit** là một Rest Client cho Android và Java và được tạo ra bởi Square. 
Nó giúp cho việc nhận và tải lên JSON (hoặc dữ liệu khác) một cách khá dễ dàng tới một WebService dựa trên mô hình REST.<br>
- Mở file **`build.gradle`** lên và import thư viện **Retrofit** và **GSON**. 
Khi sử dụng **Retrofit** thì thư viện **GSON** sẽ giúp chúng ta convert từ Java objects thành JSON và ngược lại.<br>
#### Thêm thư viện Retrofit và Gson
Trước tiên chúng ta phải import thư viện này vào Android Studio. 
Copy và paste dòng dưới đây là **dependencies** trong file **`build.gradle`** của module **app**
```java
implementation("com.google.code.gson:gson:2.10.1")
implementation("com.squareup.retrofit2:retrofit:2.9.0")
implementation("com.squareup.retrofit2:converter-gson:2.9.0")
```
Nhấn **Async Now** để Android Studio download và nạp thư viện vào project.<br><br>

#### Gọi API lấy dữ liệu
```java
public interface ApiPlaceholder {
    Gson gson = new Gson();
    Retrofit retrofit = new Retrofit.Builder()
            .baseUrl("https://jsonplaceholder.typicode.com/")
            .addConverterFactory(GsonConverterFactory.create(gson))
            .build();
    ApiPlaceholder apiService = retrofit.create(ApiPlaceholder.class);

    @GET("posts/{id}")
    Call<Post> getPostId(@Path("id") int id);

    @GET("posts")
    Call<ArrayList<Post>> getPosts();

    @POST("posts")
    Call<Post> postPost(@Body Info info);

}
```

#### Gọi phương thức đã viết
- Lấy dữ liệu theo từng **id**
```java
public void retrofitCallApi() {
    ApiPlaceholder.apiService.getPostId(1).enqueue(new Callback<Post>() {
        @Override
        public void onResponse(Call<Post> call, Response<Post> response) {
            Post data = response.body();

            userId.setText(String.valueOf(data.getUserId()));
            id.setText(String.valueOf(data.getId()));
            title.setText(data.getTitle());
            body.setText(data.getBody());
        }

        @Override
        public void onFailure(Call<Post> call, Throwable t) {
            // TODO: Handle error
            // Alert error
            Toast.makeText(MainActivity.this, "Error", Toast.LENGTH_SHORT).show();
        }
    });
}
```
<br>

- Lấy tất cả dữ liệu và lưu vào ArrayList
```java
ApiPlaceholder.apiService.getPosts().enqueue(new Callback<ArrayList<Post>>() {
    @Override
    public void onResponse(Call<ArrayList<Post>> call, Response<ArrayList<Post>> response) {
        ArrayList<Post> data = response.body();
        // TODO: process returned data

    }

    @Override
    public void onFailure(Call<ArrayList<Post>> call, Throwable t) {
        // TODO: Handle error
        // Alert error
        Toast.makeText(MainActivity.this, "Error", Toast.LENGTH_SHORT).show();
    }
});
```
<br>

- POST dữ liệu
```java
// Khởi tạo đối tượng info và gán các dữ liệu muốn POST lên server
Info info = new Info(101, "title 101", "body 101");

ApiPlaceholder.apiService.postPost(info).enqueue(new Callback<Post>() {
    @Override
    public void onResponse(Call<Post> call, Response<Post> response) {
        // Alert message
        String message = String.valueOf(response.body().getId());
        Toast.makeText(MainActivity.this, message, Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onFailure(Call<Post> call, Throwable t) {
        // TODO: Handle error
        // Alert error
        Toast.makeText(MainActivity.this, "Error", Toast.LENGTH_SHORT).show();
    }
});
```

## Web API (Application Programming Interface)
#### Xây dựng Web API
1. **Tạo Database**

**Tạo database:**
```sql
create database <database name>
```

**Truy xuất Database:**
```sql
use <database name>
```

**Tạo table:**
```sql
create table <table name>(...)
```

**Các lệnh SQL cơ bản:**
- **SELECT** được dùng khi bạn muốn đọc (hoặc lựa chọn) dữ liệu của bạn.
- **INSERT** được dùng khi bạn muốn thêm (hoặc chèn) dữ liệu mới.
- **UPDATE** được sử dụng khi bạn muốn thay đổi (hoặc cập nhật) dữ liệu sẵn có.
- **DELETE** được sử dụng khi bạn muốn loại bỏ (hoặc xóa) dữ liệu sẵn có.
a

2. **Tạo Web API (PHP)**

3. **Kết nối Android với Web API (PHP)**
