# Notifications Module (`back-end/app/notifications`)

## 1. Giới thiệu
Thư mục `notifications/` đảm nhận hệ thống thông báo nội bộ ứng dụng (In-app notifications N1–N9), tính năng theo dõi Organizer và API hỗ trợ quy trình xét duyệt của Quản trị viên (Tính năng cốt lõi **F06**, **F07**).

## 2. Thành viên phụ trách
* **Ngô Trung Nghĩa** (`19127484`) — BA & Back-end Developer

## 3. Trách nhiệm & Chức năng chính
* **Hệ thống thông báo In-app (`N1` đến `N9`):**
  * Ghi nhận thông báo gắn liền với transaction của nghiệp vụ tương ứng, cam kết không sinh thông báo rác khi transaction rollback.
  * Đảm bảo tính duy nhất qua khóa định danh `outcome_key`.
* **Hộp thư cá nhân (`Inbox`):**
  * API lấy danh sách thông báo phân trang, hiển thị trạng thái đã đọc/chưa đọc.
  * Đánh dấu đã đọc từng thông báo hoặc toàn bộ hộp thư (`UC-14`).
* **Kênh phát thông báo:**
  * Thông báo từ Organizer gửi đến danh sách người tham gia đã đăng ký (`N8`, `UC-15`).
  * Thông báo toàn hệ thống do Admin phát sóng đến tất cả Active Users (`N9`, `UC-16`).
* **Theo dõi ban tổ chức (`Organizer Follow` - `UC-23`):**
  * Tính năng dành riêng cho Sinh viên có MSSV theo dõi/hủy theo dõi Organizer ưa thích.
  * Tự động gửi thông báo `N7` khi Organizer có sự kiện mới được duyệt xuất bản lần đầu.
* **Phối hợp F07 (Admin Review):**
  * API hàng đợi duyệt sự kiện (`reviewQueue`), chi tiết sự kiện chờ duyệt (`reviewDetails`) và quyết định Duyệt/Từ chối (`decideReview`) kèm ghi chú bắt buộc (`UC-17`, `UC-18`).

## 4. Cấu trúc gợi ý
```text
notifications/
├── __init__.py
├── router.py         # APIRouter cho /api/notifications & /api/admin/reviews
├── schemas.py        # Pydantic schemas (NotificationItem, BroadcastRequest, ReviewAction)
├── service.py        # Quản lý hộp thư, logic gửi broadcast và follow
└── helper.py         # Hàm tiện ích create_notification dùng chung transaction
```
