# Auth Module (`back-end/app/auth`)

## 1. Giới thiệu
Thư mục `auth/` triển khai phân hệ xác thực, phân quyền người dùng và quản lý vai trò trong dự án CampusHub (Tính năng cốt lõi **F01** và một phần **F07**).

## 2. Thành viên phụ trách
* **Nguyễn Trường Sơn** (`24127233`) — Core Back-end Developer

## 3. Trách nhiệm & Chức năng chính
* **Đăng ký tài khoản (`UC-01`):**
  * Đăng ký tài khoản người dùng với email, họ tên, mật khẩu.
  * Hỗ trợ gán MSSV nếu MSSV tồn tại trong bảng danh sách sinh viên hợp lệ (`eligible_students`).
* **Đăng nhập hệ thống (`UC-02`):**
  * Kiểm tra thông tin xác thực, cấp phát JWT Access Token (thời hạn $\le 60$ phút).
* **Đăng xuất & Thu hồi Token (`UC-20`):**
  * Xử lý vô hiệu hóa phiên làm việc, thu hồi token trên server.
* **Phân quyền Role-Based Access Control (RBAC):**
  * Các vai trò: Sinh viên có MSSV, Người dùng thông thường, Ban tổ chức (Organizer), Quản trị viên (Admin).
  * Dependency kiểm tra quyền: `get_current_user`, `require_student`, `require_organizer`, `require_admin`.
* **Quản lý quyền Organizer (`UC-03`, `UC-19`):**
  * Gửi yêu cầu cấp quyền Organizer, Admin duyệt/thu hồi quyền Organizer.

## 4. Cấu trúc gợi ý
```text
auth/
├── __init__.py
├── router.py         # FastAPI APIRouter cho /api/auth
├── schemas.py        # Pydantic schemas (Login, Register, Token, UserResponse)
├── service.py        # Nghiệp vụ xử lý xác thực & phân quyền
└── dependencies.py   # Các dependency injection xác thực token & role
```
