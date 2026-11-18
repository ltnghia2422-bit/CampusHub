# Events Pages & Components (`front-end/src/events`)

## 1. Giới thiệu
Thư mục `events/` xây dựng các màn hình khám phá sự kiện công khai, trang chi tiết sự kiện và bảng quản lý sự kiện dành cho Ban tổ chức (Organizer).

## 2. Thành viên phụ trách
* **Hoàng Anh Quân** (`24127111`) — Designer & Front-end Developer

## 3. Các màn hình chính
* **Màn hình Khám phá sự kiện (`SCR-03`):**
  * Khung tìm kiếm từ khóa kết hợp thanh bộ lọc đa năng (theo ngày, ban tổ chức, tình trạng chỗ trống, thẻ tag).
  * Danh sách sự kiện dạng lưới hiển thị qua `EventCard`.
  * Thanh phân trang (10 sự kiện/trang).
* **Màn hình Chi tiết sự kiện (`SCR-04`):**
  * Hiển thị đầy đủ thông tin: Banner, tiêu đề, thời gian bắt đầu/kết thúc, địa điểm, đơn vị tổ chức, mô tả chi tiết, danh sách tag.
  * Thống kê chỗ: Sức chứa tối đa, số lượng đã đăng ký còn lại.
  * Nút tương tác: Nút Đăng ký tham gia (hoặc Hủy đăng ký nếu đã tham gia), nút Theo dõi Organizer.
* **Bảng điều khiển Organizer (`SCR-08` - My Events):**
  * Danh sách sự kiện do bản thân tạo ra, lọc theo trạng thái (`Draft`, `Pending Approval`, `Published`, `Cancelled`).
  * Hành động: Tạo mới, Chỉnh sửa, Xem danh sách đăng ký, Hủy sự kiện.
* **Màn hình Tạo / Chỉnh sửa sự kiện (`SCR-09`):**
  * Biểu mẫu tạo mới hoặc đề xuất chỉnh sửa sự kiện đã công bố (`Published revisions`).
  * Chọn tag từ danh mục hoặc gửi đề xuất tag mới.

## 4. Cấu trúc gợi ý
```text
events/
├── EventListPage.tsx       # SCR-03
├── EventDetailPage.tsx     # SCR-04
├── OrganizerDashboard.tsx  # SCR-08
├── EventEditorPage.tsx     # SCR-09
├── components/             # Sub-components đặc thù cho sự kiện
└── eventService.ts         # Axios/Fetch API client cho events
```
