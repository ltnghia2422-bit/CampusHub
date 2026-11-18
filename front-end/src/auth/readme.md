# Auth Pages & Context (`front-end/src/auth`)

## 1. Giới thiệu
Thư mục `auth/` phụ trách toàn bộ giao diện và luồng xử lý xác thực người dùng, lưu trữ token và phân quyền hiển thị trên giao diện Front-end.

## 2. Thành viên phụ trách
* **Hoàng Anh Quân** (`24127111`) — Designer & Front-end Developer

## 3. Các màn hình & Chức năng chính
* **Màn hình Đăng nhập (`SCR-01`):**
  * Biểu mẫu nhập email và mật khẩu với validation phía client.
  * Gọi API đăng nhập, lưu JWT vào LocalStorage / Secure Cookie.
  * Chuyển hướng người dùng về trang trước đó hoặc trang chủ sau khi đăng nhập thành công.
* **Màn hình Đăng ký tài khoản (`SCR-02`):**
  * Biểu mẫu đăng ký: Họ tên, email, mật khẩu, xác nhận mật khẩu.
  * Trường nhập MSSV (tùy chọn) với gợi ý quyền lợi dành cho sinh viên.
  * Thông báo kết quả đăng ký và xác nhận MSSV.
* **Quản lý phiên đăng nhập (`AuthContext` / Store):**
  * Lưu trữ thông tin định danh người dùng hiện tại và vai trò (Student, Regular User, Organizer, Admin).
  * Cung cấp các wrapper `ProtectedRoute` để chặn truy cập trái phép vào các trang quản trị hoặc trang Organizer.

## 4. Cấu trúc gợi ý
```text
auth/
├── LoginPage.tsx          # SCR-01
├── RegisterPage.tsx       # SCR-02
├── AuthContext.tsx        # Quản lý state đăng nhập & user profile
├── useAuth.ts             # Custom hook tiện ích
└── types.ts               # Định nghĩa interface AuthState, Credentials
```
