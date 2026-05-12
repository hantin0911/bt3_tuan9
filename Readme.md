# Bài 3: CI/CD Automation

Dự án này triển khai hệ thống quản lý ngân hàng (Bank System) với cấu trúc Maven, tích hợp logging SLF4J/Logback và Unit Tests. Ngoài ra, dự án còn bao gồm quy trình CI/CD tự động hóa qua GitHub Actions.

## Cấu trúc dự án
- `src/main/java/banksystem`: Mã nguồn chính của hệ thống.
- `src/test/java/banksystem`: Các bài kiểm thử đơn vị (Unit Tests) sử dụng JUnit 5.
- `src/main/resources/logback.xml`: Cấu hình logging.
- `pom.xml`: Cấu hình Maven project và dependencies.
- `.github/workflows/main.yml`: Cấu hình workflow GitHub Actions.

## Tính năng CI/CD
Workflow GitHub Actions được thiết lập để:
1.  Kích hoạt khi có `push` hoặc `pull_request` vào nhánh `main` hoặc `master`.
2.  Kiểm tra code trên môi trường `ubuntu-latest`.
3.  Cài đặt JDK 17.
4.  Chạy các pha build của Maven: `test` và `package`.
5.  Upload tệp JAR được build thành công lên mục Artifacts của GitHub Actions.

## Hướng dẫn kiểm thử và Debug
### 1. Cách gây lỗi build cố ý
Để kiểm tra tính năng tự động hóa, bạn có thể:
- Sửa đổi một hàm trong mã nguồn khiến Unit Test bị lỗi (ví dụ: đổi `balance += amount` thành `balance -= amount` trong `doDepositing`).
- Viết sai cú pháp Java trong bất kỳ tệp nào.
- Sửa đổi giá trị mong đợi trong `AccountTest.java` thành một giá trị sai.

### 2. Cách Debug trên GitHub Actions
Khi build thất bại:
1.  Truy cập tab **Actions** trên repository GitHub của bạn.
2.  Chọn lần chạy workflow bị lỗi (có dấu X đỏ).
3.  Nhấn vào job **build**.
4.  Mở rộng các bước bị lỗi (thường là `Build with Maven`) để xem log chi tiết. Maven sẽ thông báo cụ thể test nào bị fail hoặc lỗi cú pháp ở dòng nào.

## Cách chạy cục bộ
Sử dụng script `run.sh`:
```bash
./run.sh
```
Hoặc dùng Maven trực tiếp:
```bash
mvn clean test
mvn package
```
