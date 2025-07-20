# QRGenerator
Thư viện tạo mã QR và lưu mã QR dưới dạng hình ảnh

[![](https://jitpack.io/v/androidmads/QRGenerator.svg?style=for-the-badge)](https://jitpack.io/#androidmads/QRGenerator)

[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-QR%20Generator-green.svg?style=for-the-badge)](https://android-arsenal.com/details/1/3890)

[![CSharpCorner](https://img.shields.io/badge/C%23-Corner-blue.svg?style=for-the-badge)](https://www.c-sharpcorner.com/article/how-to-generate-qr-code-in-android/)

[![St ckOverflow](https://img.shields.io/badge/stack%20overflow-FE7A16?logo=stack-overflow&logoColor=white&style=for-the-badge)](https://rb.gy/vol1bm)

[![Androidmads](https://img.shields.io/badge/Androidmads-Blog-09BBB2?style=for-the-badge)](https://www.androidmads.info/2018/07/how-to-generate-qr-code-in-android.html)

### Cách nhập thư viện:
Thêm nó vào thư mục gốc build.gradle của bạn ở cuối kho lưu trữ:

<b>Build.gradle cấp ứng dụng:</b>
``` groovy
allprojects {
repositories {
...
maven { url 'https://jitpack.io' }
}
}
```
<b>Cấp mô-đun build.gradle:</b>
```groovy
dependencies {
implementation 'com.github.androidmads:QRGenerator:1.0.4'
}
```
<b>settings.gradle:</b>
```
dependencyResolutionManagement {
repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
repositories {
google()
mavenCentral()
maven(url = "https://jitpack.io")
}
}
```
Hoạt động:
```
import androidmads.library.qrgenerator.QRGContents;
import androidmads.library.qrgenearator.QRGEncoder;

```

### Tính năng:
1. Màu mã QR có thể thay đổi động
2. Hỗ trợ Android X
3. Hỗ trợ tối thiểu từ phiên bản 14
4. Có thể kiểm soát lề của mã QR

### Quyền:

Thêm Quyền này để lưu mã đã tạo
```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```
### Cách sử dụng Thư viện này:

Sau khi nhập thư viện này, hãy sử dụng các dòng sau để sử dụng thư viện.
Các dòng sau được sử dụng để tạo Mã QR
```java
// Khởi tạo Bộ mã hóa QR với giá trị cần mã hóa, kiểu dữ liệu bạn yêu cầu và Kích thước
QRGEncoder qrgEncoder = new QRGEncoder(inputValue, null, QRGContents.Type.TEXT, smallerDimension);
qrgEncoder.setColorBlack(Color.RED);
qrgEncoder.setColorWhite(Color.BLUE);

try {
// Lấy Mã QR dưới dạng Bitmap
bitmap = qrgEncoder.getBitmap();
// Đặt Bitmap thành ImageView
qrImage.setImageBitmap(bitmap);

} catch (WriterException e) {
Log.v(TAG, e.toString());

}
```
Các dòng sau được sử dụng để tạo Mã QR không có lề/đường viền mặc định
```java
// Khởi tạo Bộ mã hóa QR với giá trị cần mã hóa, kiểu dữ liệu bạn yêu cầu và Kích thước
QRGEncoder qrgEncoder = new QRGEncoder(inputValue, null, QRGContents.Type.TEXT, smallerDimension);
qrgEncoder.setColorBlack(Color.RED);
qrgEncoder.setColorWhite(Color.BLUE);
try {
// Lấy Mã QR dưới dạng Bitmap
bitmap = qrgEncoder.getBitmap(0);

// Đặt Bitmap thành ImageView
qrImage.setImageBitmap(bitmap);

} catch (WriterException e) {
Log.v(TAG, e.toString());
}
```
Các dòng sau được sử dụng để tạo Mã vạch
```java
BarcodeEncoder barcodeEncoder = new BarcodeEncoder(inputValue, BarcodeFormat.CODE_128, 800);
bitmap = barcodeEncoder.getBitmap(2); // Khoảng cách 2 pixel
// Bây giờ bạn có thể sử dụng bitmap này khi cần, ví dụ: hiển thị nó trong ImageView
qrImage.setImageBitmap(bitmap);
```

Lưu Mã QR dưới dạng Hình ảnh
```java
// Lưu với vị trí, giá trị, bitmap được trả về và loại Hình ảnh (JPG/PNG).
QRGSaver qrgSaver = new QRGSaver();
qrgSaver.save(savePath, edtValue.getText().toString().trim(), bitmap, QRGContents.ImageType.IMAGE_JPEG);
```
