# Notifications Pages & Subscriptions (`front-end/src/notifications`)

## 1. Giới thiệu
Thư mục `notifications/` phụ trách giao diện trung tâm thông báo cá nhân (Inbox) và các thành phần tương tác theo dõi Ban tổ chức trong ứng dụng CampusHub.

## 2. Thành viên phụ trách
* **Hoàng Anh Quân** (`24127111`) — Designer & Front-end Developer

## 3. Các màn hình & Chức năng chính
* **Màn hình Hộp thư thông báo (`SCR-07`):**
  * Hiển thị danh sách các thông báo theo thứ tự thời gian từ mới nhất đến cũ nhất.
  * Phân loại trực quan các loại thông báo từ hệ thống (`N1` đến `N9`):
    * Thông báo kết quả đăng ký sự kiện, nhắc nhở trước sự kiện.
    * Thông báo duyệt/từ chối sự kiện của Organizer.
    * Thông báo sự kiện mới từ Organizer đang theo dõi (`N7`).
    * Tin nhắn từ Organizer gửi người tham gia (`N8`).
    * Thông báo khẩn/phát thanh toàn hệ thống từ Admin (`N9`).
  * Hành động: Bấm vào thông báo để dẫn đến trang chi tiết liên quan, nút đánh dấu đã đọc từng mục hoặc đánh dấu tất cả đã đọc.
* **Thành phần Theo dõi Organizer (`FollowButton`):**
  * Nút chuyển đổi trạng thái Follow / Unfollow dành cho sinh viên có MSSV.
  * Tích hợp gọi API cập nhật trạng thái và hiển thị toast thông báo tương ứng.

## 4. Cấu trúc gợi ý
```text
notifications/
├── NotificationInboxPage.tsx # SCR-07
├── FollowButton.tsx          # Component nút theo dõi Organizer
├── NotificationItem.tsx      # Component hiển thị từng thông báo
└── notificationService.ts    # Axios/Fetch API client cho notifications
```
