# Phân công công việc — Dự án CampusHub (MVP: F01–F07)

Tài liệu này phân chia trách nhiệm lập trình cho 5 thành viên nhóm dựa trên cấu trúc thư mục hiện tại của repository, tuân theo nguyên tắc:
* **Developer & Tester** phụ trách **Back-end** (`back-end/app/`) và kiểm thử API.
* **Designer** phụ trách **Front-end** (`front-end/src/`) và chuẩn hóa giao diện (UI/UX).

---

## 1. Bảng phân công tổng quan

| Thành viên (MSSV) | Vai trò triển khai | Khu vực phụ trách chính | Thư mục đảm nhiệm | Phạm vi tính năng |
| :--- | :--- | :--- | :--- | :--- |
| **Nguyễn Trường Sơn** (`24127233`) | Core Back-end Developer | Back-end (Nền tảng & Xác thực) | `back-end/app/core/`<br>`back-end/app/models/`<br>`back-end/app/auth/` | Cấu hình DB/JWT, 16 bảng SQLAlchemy, **F01** (Auth, RBAC, MSSV, quyền Organizer/Admin) |
| **Lưu Trọng Nghĩa** (`24127463`) | Team Lead & Back-end Developer | Back-end (Sự kiện) & Quản lý dự án | `back-end/app/events/`<br>`docs/` | **F02, F03** (Khám phá, tìm kiếm/lọc, CRUD sự kiện, Published revisions, Tags), Review PR & Deploy |
| **Phạm Nhựt Anh** (`24127014`) | Back-end Developer *(từ Tester)* | Back-end (Đăng ký) & Test API | `back-end/app/registrations/` | **F04, F05** (Đăng ký/hủy chống overbooking, Priority Release `S - 72h`, Roster) & viết Pytest |
| **Ngô Trung Nghĩa** (`19127484`) | BA & Back-end Developer | Back-end (Thông báo & Duyệt) | `back-end/app/notifications/`<br>*(phối hợp `events/` & `auth/`)* | **F06, F07** (In-app notifications N1–N9, Follow Organizer, API hàng đợi duyệt Admin) |
| **Hoàng Anh Quân** (`24127111`) | Designer & Front-end Developer | Toàn bộ Front-end (UI/UX) | `front-end/src/ui/`<br>`front-end/src/auth/`<br>`front-end/src/events/`<br>`front-end/src/registrations/`<br>`front-end/src/notifications/`<br>`front-end/src/admin/` | Toàn bộ 14 màn hình (`SCR-01` – `SCR-14`), Responsive (`1366x768`, `360x800`) & Accessibility |

---

## 2. Chi tiết đầu việc từng thành viên

### 1. Nguyễn Trường Sơn (`24127233`) — Core Back-end Developer
* **`back-end/app/core/`**: Thiết lập kết nối PostgreSQL, cấu hình biến môi trường, mã hóa mật khẩu (bcrypt/passlib), cấp phát & xác thực JWT (hạn ≤ 60 phút), xử lý đồng bộ giờ server (`Asia/Ho_Chi_Minh`).
* **`back-end/app/models/`**: Định nghĩa 16 bảng dữ liệu bằng SQLAlchemy (`users`, `eligible_students`, `events`, `event_reviews`, `participations`, `notifications`,...) kèm đầy đủ khóa ngoại, `CHECK` constraints và partial indexes; thiết lập cơ chế transaction dùng chung.
* **`back-end/app/auth/`**: Xây dựng API đăng ký (`UC-01`), đăng nhập (`UC-02`), đăng xuất & thu hồi token (`UC-20`), gán/thu hồi MSSV từ danh sách hợp lệ và duyệt yêu cầu quyền Organizer (`UC-03`, `UC-19`).

### 2. Lưu Trọng Nghĩa (`24127463`) — Team Lead & Back-end Developer
* **`back-end/app/events/`**:
  * API công khai khám phá sự kiện (`Published`, phân trang cố định 10 sự kiện/trang, tìm kiếm & lọc kết hợp `AND` theo từ khóa, ngày, Organizer, trạng thái chỗ trống, tag đã duyệt).
  * API quản lý sự kiện của Organizer: Tạo Draft, chỉnh sửa, gửi duyệt, xóa Draft, xem danh sách sự kiện của tôi (`My Events`, bao gồm chế độ chỉ đọc khi bị thu hồi quyền Organizer).
  * Xử lý đề xuất chỉnh sửa sự kiện đã đăng (`Published revisions`) và hủy sự kiện (`t <= S - 24h`).
  * Quản lý danh mục 10 tag mặc định và luồng đề xuất/duyệt tag mới.
* **Quản lý chung**: Review Pull Request, quản lý tiến độ trên Jira, cập nhật tài liệu `docs/` và triển khai lên cloud (Vercel, Render, Neon).

### 3. Phạm Nhựt Anh (`24127014`) — Back-end Developer *(chuyển từ Tester)*
* **`back-end/app/registrations/`**:
  * API đăng ký tham gia (`UC-10`) sử dụng khóa dòng PostgreSQL (`SELECT ... FOR UPDATE`) đảm bảo không trùng lặp và không vượt sức chứa: xác nhận ngay cho MSSV, đưa vào `Pending Confirmation` (không giữ chỗ) cho non-MSSV.
  * API hủy đăng ký / rút yêu cầu (`UC-11`) có kiểm tra `cycle_no` và mốc cutoff `C`.
  * Tác vụ `PriorityReleaseTask` chạy khi khởi động server và qua internal webhook định kỳ 5 phút để duyệt FIFO các yêu cầu `Pending Confirmation` tại mốc `S - 72h`.
  * API xem lịch sử đăng ký của Sinh viên (`My Registrations`) và danh sách người tham gia (`Registrant List`) cho Organizer.
* **Kiểm thử Back-end**: Viết unit test và integration test (Pytest), đặc biệt là kiểm thử đồng thời (concurrency test) cho trường hợp nhiều người cùng đăng ký slot cuối cùng.

### 4. Ngô Trung Nghĩa (`19127484`) — BA & Back-end Developer
* **`back-end/app/notifications/`**:
  * Xây dựng hàm ghi thông báo trong ứng dụng (`N1`–`N9`) dùng chung transaction với các nghiệp vụ khác, đảm bảo tính duy nhất theo `outcome_key` và không tạo thông báo ảo khi rollback.
  * API hộp thư cá nhân (`Inbox`), đánh dấu đã đọc từng mục / tất cả (`UC-14`), gửi tin nhắn Organizer tới người đã đăng ký (`N8`, `UC-15`), phát thông báo Admin tới toàn bộ Active Users (`N9`, `UC-16`).
  * API theo dõi / hủy theo dõi Organizer dành riêng cho Sinh viên có MSSV (`UC-23`) và gửi `N7` khi sự kiện được duyệt đăng lần đầu.
* **Phối hợp F07 (Admin Approval)**: Xây dựng API hàng đợi duyệt (`reviewQueue`), chi tiết duyệt (`reviewDetails`) và ra quyết định Duyệt/Từ chối (`decideReview`) với ghi chú bắt buộc và kiểm tra version nguyên tử.

### 5. Hoàng Anh Quân (`24127111`) — Designer & Front-end Developer
* **`front-end/src/ui/`**: Xây dựng bộ component dùng chung (Header, Navigation, Notification Bell, EventCard, StatusBadge phân biệt rõ `Pending Confirmation` / `Registered` / `Event Full`, Pagination, EmptyState, ConfirmModal).
* **`front-end/src/auth/`**: Hoàn thiện màn hình Đăng nhập (`SCR-01`), Đăng ký (`SCR-02`) và lưu trạng thái đăng nhập/phân quyền giao diện.
* **`front-end/src/events/`**: Hoàn thiện Khám phá sự kiện (`SCR-03`), Chi tiết sự kiện (`SCR-04`), Organizer Dashboard (`SCR-08`), Tạo/Sửa sự kiện (`SCR-09`).
* **`front-end/src/registrations/`**: Hoàn thiện Xác nhận đăng ký (`SCR-05`), Lịch sử đăng ký (`SCR-06`), Danh sách người tham gia (`SCR-10`).
* **`front-end/src/notifications/`**: Hoàn thiện Hộp thư thông báo (`SCR-07`) và nút Follow/Unfollow Organizer.
* **`front-end/src/admin/`**: Hoàn thiện Hàng đợi duyệt (`SCR-11`), Chi tiết duyệt sự kiện (`SCR-12`), Quản lý tài khoản/MSSV (`SCR-13`), Gửi thông báo hệ thống (`SCR-14`).

---

## 3. Quy ước phối hợp (Giảm tải cho Front-end)

* **Thứ tự ưu tiên**: `Nguyễn Trường Sơn` hoàn thiện `core/` + `models/` + `auth/` trước để các thành viên Back-end khác có nền tảng code song song; đồng thời `Hoàng Anh Quân` dựng khung `ui/` và các màn hình tĩnh bằng mock data.
* **Hỗ trợ tích hợp API**: Vì toàn bộ Front-end do 1 thành viên đảm nhiệm, ở giai đoạn ghép API thật, mỗi thành viên Back-end sẽ phối hợp trực tiếp với `Hoàng Anh Quân` để nối API thuộc phân hệ mình phụ trách và cùng kiểm tra lỗi hiển thị.