# Admin Management Pages (`front-end/src/admin`)

## 1. Giới thiệu
Thư mục `admin/` chịu trách nhiệm toàn bộ các màn hình giao diện dành cho Quản trị viên hệ thống (Admin), bao gồm duyệt sự kiện, quản lý người dùng và phát thông báo diện rộng (**F07**).

## 2. Thành viên phụ trách
* **Hoàng Anh Quân** (`24127111`) — Designer & Front-end Developer

## 3. Các màn hình chính
* **Hàng đợi duyệt sự kiện & bản chỉnh sửa (`SCR-11` - Review Queue):**
  * Danh sách các sự kiện mới tạo hoặc phiên bản chỉnh sửa (`Published revisions`) đang chờ phê duyệt (`Pending Approval`).
  * Bộ lọc phân loại: Sự kiện mới / Bản chỉnh sửa, sắp xếp theo thời gian gửi yêu cầu.
* **Chi tiết xét duyệt sự kiện (`SCR-12` - Review Details):**
  * Xem toàn bộ nội dung sự kiện được đề xuất.
  * Đối với bản chỉnh sửa: Hiển thị giao diện so sánh (Diff) giữa bản đang công bố và bản đề xuất thay đổi.
  * Biểu mẫu nhập lý do/ghi chú bắt buộc kèm hai nút hành động: **Phê duyệt (Approve)** hoặc **Từ chối (Reject)**.
* **Quản lý tài khoản & Quyền Organizer (`SCR-13`):**
  * Bảng danh sách người dùng, tìm kiếm theo tên, email, MSSV.
  * Phê duyệt hoặc từ chối các yêu cầu cấp quyền Ban tổ chức (Organizer).
  * Cập nhật, gán hoặc thu hồi MSSV.
* **Gửi thông báo toàn hệ thống (`SCR-14` - Broadcast Notification):**
  * Biểu mẫu soạn tiêu đề và nội dung thông báo phát thanh (`N9`).
  * Xem trước (Preview) nội dung thông báo trước khi gửi đi toàn bộ Active Users.

## 4. Cấu trúc gợi ý
```text
admin/
├── ReviewQueuePage.tsx       # SCR-11
├── ReviewDetailPage.tsx      # SCR-12
├── UserManagementPage.tsx    # SCR-13
├── BroadcastPage.tsx         # SCR-14
└── adminService.ts           # Axios/Fetch API client cho các tính năng Admin
```
