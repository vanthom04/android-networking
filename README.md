# Android Networking

## [Thư viện Volley](https://google.github.io/volley/)

**`Các class sử dụng trong Volley:`**<br>
**RequestQueue:** Là hàng đợi giữ các Request.<br>
**Request:** là lớp cơ sở của các Request trong Volley, chứa thông tin về request HTTP<br>
**StringRequest:** Kế thừa từ Request, là class đại diện cho request trả về String.<br>
**JSONObjectRequest:** Là HTTP request có response trả về là JSONObject.<br>
**JSONArrayRequest:** Là HTTP request có response trả về là JSONArray. <br>
**ImageRequest:** Là HTTP request có response trả về là Bitmap.<br>

**`Install:`**<br>
Trước tiên chúng ta phải import thư viện này vào Android Studio. 
Copy và paste dòng dưới đây là **dependencies** trong file **build.gradle** của module **app**

```java
implementation("com.android.volley:volley:1.2.1")
```

Nhấn Async Now để Android Studio download và nạp thư viện vào project.<br>
**`Lưu ý:`** *Để sử dụng Volley chúng ta phải cấp quyền Internet trong __AndroidManifest.xml__*
#### **String Request**

## [Thư viện Retrofit](https://square.github.io/retrofit/)
Retrofit là một Rest Client cho Android và Java và được tạo ra bởi
Square. Nó giúp cho việc nhận và tải lên JSON (hoặc dữ liệu khác)
một cách khá dễ dàng tới một WebService dựa trên mô hình REST.<br>
Mở file build.gradle lên và import thư viện Retrofit và GSON. Khi
sử dụng Retrofit thì thư viện GSON sẽ giúp chúng ta convert từ
Java objects thành JSON và ngược lại.<br>
#### **Thêm thư viện Retrofit và Gson**
Trước tiên chúng ta phải import thư viện này vào Android Studio. 
Copy và paste dòng dưới đây là **dependencies** trong file **build.gradle** của module **app**
```java
implementation("com.google.code.gson:gson:2.10.1")
implementation("com.squareup.retrofit2:retrofit:2.9.0")
implementation("com.squareup.retrofit2:converter-gson:2.9.0")
```
Nhấn Async Now để Android Studio download và nạp thư viện vào project.<br>
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
            Toast.makeText(MainActivity.this, "Error", Toast.LENGTH_SHORT).show();
        }
    });
}
```