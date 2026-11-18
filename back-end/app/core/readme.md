# Core Module (`back-end/app/core`)

## 1. Giới thiệu
Thư mục `core/` chịu trách nhiệm cấu hình nền tảng máy chủ, các tiện ích dùng chung, bảo mật và kết nối cơ sở dữ liệu cho toàn bộ ứng dụng Back-end (FastAPI).

## 2. Thành viên phụ trách
* **Nguyễn Trường Sơn** (`24127233`) — Core Back-end Developer

## 3. Trách nhiệm & Chức năng chính
* **Cấu hình hệ thống (`config.py` / `settings.py`):**
  * Quản lý biến môi trường qua Pydantic Settings (`.env`).
  * Cấu hình CORS, secret key, log level, environment (development / staging / production).
* **Kết nối Cơ sở dữ liệu (`database.py`):**
  * Thiết lập kết nối PostgreSQL qua SQLAlchemy engine.
  * Cấu hình connection pooling và quản lý dependency `get_db` cung cấp `Session` cho các route.
* **Bảo mật & Xác thực (`security.py`):**
  * Mã hóa mật khẩu an toàn sử dụng `bcrypt` (hoặc `passlib[bcrypt]`).
  * Khởi tạo, mã hóa và giải mã JSON Web Token (JWT) cho các phiên đăng nhập.
  * Giới hạn thời gian sống của token: **tối đa 60 phút**.
* **Đồng bộ thời gian máy chủ:**
  * Đồng bộ chuẩn múi giờ `Asia/Ho_Chi_Minh` cho toàn bộ các mốc thời gian lưu trữ và kiểm tra logic nghiệp vụ.

## 4. Cấu trúc gợi ý
```text
core/
├── __init__.py
├── config.py         # Pydantic Settings đọc biến môi trường
├── database.py       # SQLAlchemy engine & session factory
├── security.py       # Mã hóa mật khẩu & JWT helpers
└── timezone.py       # Helper chuẩn hóa múi giờ Asia/Ho_Chi_Minh
```
