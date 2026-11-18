# Models Module (`back-end/app/models`)

## 1. Giới thiệu
Thư mục `models/` định nghĩa cấu trúc dữ liệu ORM của hệ thống CampusHub bằng SQLAlchemy, làm cầu nối ánh xạ giữa mã nguồn Python và cơ sở dữ liệu PostgreSQL.

## 2. Thành viên phụ trách
* **Nguyễn Trường Sơn** (`24127233`) — Core Back-end Developer

## 3. Trách nhiệm & Chức năng chính
* **Định nghĩa 16 bảng dữ liệu cốt lõi:**
  * Bảng người dùng và sinh viên: `users`, `eligible_students`.
  * Bảng sự kiện và danh mục: `events`, `event_tags`, `tags`, `event_revisions`, `event_reviews`.
  * Bảng tham gia & đăng ký: `participations` (với các trạng thái: Pending, Confirmed, Cancelled).
  * Bảng thông báo & theo dõi: `notifications`, `organizer_follows`.
* **Ràng buộc dữ liệu toàn vẹn:**
  * Thiết lập đầy đủ Primary Key, Foreign Key và quan hệ `relationship()` giữa các model.
  * Áp dụng các ràng buộc kiểm tra (`CHECK constraints`) và partial indexes.
* **Quản lý giao dịch & Khóa dòng dữ liệu:**
  * Hỗ trợ cơ chế khóa dòng (`SELECT ... FOR UPDATE`) phục vụ chức năng đăng ký chống race condition và overbooking.

## 4. Cấu trúc gợi ý
```text
models/
├── __init__.py       # Export toàn bộ các Model
├── base.py           # Base model (id, created_at, updated_at)
├── user.py           # Model User, EligibleStudent
├── event.py          # Model Event, EventRevision, EventReview, Tag
├── registration.py   # Model Participation
└── notification.py   # Model Notification, OrganizerFollow
```
