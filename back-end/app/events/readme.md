# Events Module (`back-end/app/events`)

## 1. Giới thiệu
Thư mục `events/` phụ trách nghiệp vụ vòng đời sự kiện, khám phá công khai, quản lý bản nháp, xuất bản và danh mục tag trong CampusHub (Tính năng cốt lõi **F02**, **F03**).

## 2. Thành viên phụ trách
* **Lưu Trọng Nghĩa** (`24127463`) — Team Lead & Back-end Developer

## 3. Trách nhiệm & Chức năng chính
* **Khám phá sự kiện công khai (`UC-04`, `UC-05`):**
  * API lấy danh sách sự kiện đã xuất bản (`Published`).
  * Phân trang cố định: **10 sự kiện/trang**.
  * Tìm kiếm và lọc nâng cao kết hợp logic `AND`: theo từ khóa tiêu đề/mô tả, ngày diễn ra, đơn vị tổ chức (Organizer), tình trạng còn chỗ trống, danh mục tag đã duyệt.
* **Vòng đời sự kiện của Organizer (`UC-07`):**
  * Tạo sự kiện nháp (`Draft`), cập nhật nội dung nháp, gửi yêu cầu xét duyệt (`Pending Approval`).
  * Xóa bản nháp khi không còn nhu cầu.
  * Xem danh sách sự kiện do cá nhân tổ chức (`My Events`), bao gồm chế độ chỉ đọc khi bị thu hồi quyền Organizer.
  * Hủy sự kiện đã công bố: Áp dụng điều kiện thời gian bắt buộc $t \le S - 24h$ (trước giờ bắt đầu ít nhất 24 giờ).
* **Bản chỉnh sửa sự kiện đã công bố (`Published revisions` - `UC-08`):**
  * Đề xuất chỉnh sửa sự kiện đã đăng và gửi vào hàng đợi duyệt của Admin mà không làm gián đoạn sự kiện đang hiển thị.
* **Quản lý danh mục Tag (`UC-09`):**
  * Khởi tạo và quản lý 10 tag mặc định của hệ thống.
  * Quy trình tiếp nhận đề xuất tag mới từ Organizer và duyệt tag từ Admin.

## 4. Cấu trúc gợi ý
```text
events/
├── __init__.py
├── router.py         # APIRouter cho /api/events & /api/organizer/events
├── schemas.py        # Pydantic schemas (EventCreate, EventUpdate, EventDetail, TagSchema)
├── service.py        # Nghiệp vụ tìm kiếm, phân trang, CRUD sự kiện, kiểm tra mốc thời gian
└── tags.py           # Xử lý logic danh mục tag
```
