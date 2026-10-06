# Hiepcar -- Website hỗ trợ tìm kiếm và cho thuê xe

Hiepcar là đồ án học tập cá nhân xây dựng website hỗ trợ tìm kiếm, xem
thông tin và đặt thuê xe trực tuyến. Hệ thống có khu vực người dùng/chủ
xe và khu vực quản trị viên.

## 1. Công nghệ sử dụng

-   **Frontend:** ReactJS, TypeScript, Vite
-   **Backend:** Node.js, ExpressJS
-   **Cơ sở dữ liệu:** MongoDB, Mongoose
-   **Xác thực và phân quyền:** JWT
-   **Giao tiếp Frontend -- Backend:** RESTful API, Axios
-   **Quản lý mã nguồn:** Git và GitHub

## 2. Chức năng chính

### Người dùng

-   Đăng ký, đăng nhập và đăng xuất.
-   Tìm kiếm, lọc và xem thông tin xe.
-   Đặt thuê xe và theo dõi lịch sử/trạng thái đặt xe.
-   Quản lý thông tin cá nhân.
-   Thêm hoặc xóa xe yêu thích.
-   Gửi đánh giá theo điều kiện của hệ thống.

### Chủ xe

-   Đăng xe cho thuê và tải ảnh xe lên.
-   Xem danh sách xe của mình.
-   Chỉnh sửa thông tin và quản lý trạng thái xe.

### Quản trị viên

-   Xem trang tổng quan.
-   Quản lý người dùng.
-   Quản lý xe và xử lý trạng thái duyệt xe.
-   Quản lý đơn đặt xe.
-   Xem báo cáo/thống kê.

> Chức năng thực tế có thể phụ thuộc vào cấu hình và trạng thái hiện tại
> của mã nguồn.

## 3. Cấu trúc dự án

``` text
Hiepcar/
└── Hiepcar/
    ├── backend/       # API Node.js/Express và kết nối MongoDB
    └── client/        # Giao diện ReactJS/TypeScript
```

## 4. Yêu cầu môi trường

-   Node.js và npm
-   MongoDB Community Server
-   MongoDB Compass (không bắt buộc, dùng để xem dữ liệu)
-   Trình duyệt web như Google Chrome

## 5. Cấu hình MongoDB

Backend sử dụng chuỗi kết nối:

``` env
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb://localhost:27017/moto_db
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
JWT_EXPIRE=7d
CLIENT_URL=http://localhost:5173
```

Tạo hoặc kiểm tra file `backend/.env`. Đảm bảo MongoDB Server đang chạy.
Dự án sử dụng database `moto_db`; dữ liệu và collection sẽ xuất hiện khi
ứng dụng ghi dữ liệu thành công.

**Lưu ý:** `CLIENT_URL` phải trùng với địa chỉ Frontend đang chạy. Nếu
Vite hiển thị địa chỉ khác `http://localhost:5173`, hãy cập nhật giá trị
này. Thay `JWT_SECRET` bằng một chuỗi bí mật riêng trước khi triển khai
công khai. Không đưa file `.env` hoặc thông tin bí mật lên GitHub.

## 6. Cài đặt và chạy dự án

Trên Windows PowerShell, có thể dùng `npm.cmd` nếu lệnh `npm` bị chặn
bởi Execution Policy.

### Bước 1: Chạy Backend

Mở terminal tại thư mục `backend`:

``` powershell
npm.cmd install
npm.cmd start
```

Backend sử dụng cổng `5000`, địa chỉ `http://localhost:5000`.

Nếu dự án không có script `start`, chạy `npm.cmd run` để xem các script
có sẵn và chọn script phù hợp, chẳng hạn `npm.cmd run dev`.

### Bước 2: Chạy Frontend

Mở **terminal thứ hai** tại thư mục `client`:

``` powershell
npm.cmd install
npm.cmd run dev
```

Mở địa chỉ Local mà Vite hiển thị trong terminal, thường là
`http://localhost:5173`. Giữ cả hai terminal chạy trong khi sử dụng
website.

> Nếu báo không tìm thấy `package.json`, hãy kiểm tra bạn đã đứng đúng
> thư mục `backend` hoặc `client` chưa.

## 7. Kiểm tra kết nối MongoDB

1.  Mở MongoDB Compass.
2.  Kết nối bằng URI `mongodb://localhost:27017`.
3.  Chạy Backend và kiểm tra terminal có thông báo kết nối MongoDB thành
    công hay không.
4.  Đăng ký một tài khoản thử nghiệm trên website.
5.  Làm mới danh sách database trong Compass, kiểm tra `moto_db` và
    collection `users`.
6.  Nếu không có dữ liệu, kiểm tra `MONGODB_URI`, log Backend và request
    trong tab Network của trình duyệt.

## 8. Kiểm thử cơ bản

-   Đăng ký bằng thông tin hợp lệ và thử đăng ký lại bằng email đã tồn
    tại.
-   Đăng nhập với mật khẩu đúng và sai.
-   Tìm kiếm và xem chi tiết xe.
-   Thử tạo đơn đặt xe với dữ liệu hợp lệ.
-   Đăng nhập tài khoản chủ xe để thử đăng xe và cập nhật thông tin.
-   Đăng nhập tài khoản quản trị viên để kiểm tra quản lý người dùng, xe
    và đơn đặt xe.
-   Kiểm tra phân quyền: tài khoản thường không được phép thực hiện chức
    năng chỉ dành cho quản trị viên.
-   Đối chiếu dữ liệu sau thao tác trong MongoDB Compass.

Nếu trang hiển thị trắng hoặc API trả về `401`/`403`, hãy kiểm tra
Console và Network trong DevTools, token đăng nhập, quyền tài khoản và
log Backend.

## 9. Các nhóm API

  Nhóm          Đường dẫn
  ------------- ----------------------
  Xác thực      `/api/auth`
  Người dùng    `/api/users`
  Phương tiện   `/api/vehicles`
  Đặt xe        `/api/bookings`
  Đánh giá      `/api/reviews`
  Chat          `/api/chat`
  Quản trị      `/api/admin`
  Yêu thích     `/api/favorites`
  Tải tệp       `/api/upload`
  Thông báo     `/api/notifications`

Đây là các tiền tố API được khai báo trong Backend; endpoint chi tiết và
phương thức HTTP được xác định trong từng file routes.

## 10. Tác giả

-   **Sinh viên:** Trần Tuấn Hiệp
-   **Mã sinh viên:** 523100148
-   **Đề tài:** Xây dựng website hỗ trợ tìm kiếm và cho thuê xe --
    Hiepcar

------------------------------------------------------------------------

Đồ án phục vụ mục đích học tập và thực hành xây dựng ứng dụng web.
