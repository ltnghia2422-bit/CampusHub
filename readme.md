# CampusHub

**CampusHub** là nền tảng web tập trung hỗ trợ khám phá, đăng ký và quản lý các sự kiện miễn phí trong trường đại học. Dự án tập trung vào 7 nhóm tính năng cốt lõi (MVP: F01–F07) dành cho Sinh viên (có MSSV), Người dùng thông thường, Ban tổ chức (Organizer) và Quản trị viên (Admin).

## Công nghệ sử dụng
* **Front-end:** React 18, TypeScript, Vite, Tailwind CSS.
* **Back-end:** Python, FastAPI, Pydantic, SQLAlchemy.
* **Cơ sở dữ liệu:** PostgreSQL.

---

## Cấu trúc thư mục dự án

```text
.
├── back-end/
│   └── app/
│       ├── auth/
│       ├── core/
│       ├── events/
│       ├── models/
│       ├── notifications/
│       └── registrations/
├── docs/
│   ├── PA1-ProjectProposal-Plan_final.pdf
│   ├── PA2-SoftwareRequirementsSpecification.pdf
│   └── PA3-SoftwareDesign.docx.pdf
└── front-end/
    └── src/
        ├── admin/
        ├── auth/
        ├── events/
        ├── notifications/
        ├── registrations/
        └── ui/
```

---

## Chức năng chính của từng thư mục

### 1. `/docs` — Tài liệu dự án
Lưu trữ toàn bộ tài liệu đặc tả và thiết kế theo từng giai đoạn của đồ án:
* `PA1-ProjectProposal-Plan_final.pdf`: Đề xuất dự án, phạm vi tính năng, kế hoạch thực hiện (WBS, lịch trình, quản lý rủi ro).
* `PA2-SoftwareRequirementsSpecification.pdf`: Đặc tả yêu cầu phần mềm (FR, NFR, Business Rules, Use Cases và Mockups).
* `PA3-SoftwareDesign.docx.pdf`: Thiết kế hệ thống (kiến trúc C4, ADRs, biểu đồ lớp/tuần tự/trạng thái, thiết kế CSDL ERD và giao diện).

### 2. `/back-end/app` — Mã nguồn Back-end (FastAPI)
Tổ chức theo mô hình Modular Monolith, gom nhóm router và logic nghiệp vụ theo từng cụm chức năng:
* `core/`: Cấu hình hệ thống, kết nối cơ sở dữ liệu, mã hóa mật khẩu, xác thực JWT (hạn tối đa 60 phút) và đồng bộ thời gian máy chủ (`Asia/Ho_Chi_Minh`).
* `models/`: Định nghĩa các bảng cơ sở dữ liệu bằng SQLAlchemy (`users`, `eligible_students`, `events`, `event_reviews`, `participations`, `notifications`,...) và quản lý giao dịch (transaction / row-locking).
* `auth/`: Xử lý đăng ký, đăng nhập, đăng xuất (thu hồi JWT trên server), gán MSSV từ danh sách hợp lệ và quản lý quyền Organizer/Admin (F01, F07).
* `events/`: API khám phá/tìm kiếm/lọc sự kiện công khai, quản lý vòng đời sự kiện (Draft, Pending Approval, Published, Cancelled), đề xuất chỉnh sửa sự kiện đã đăng (Published revisions), quy trình Admin duyệt sự kiện và quản lý tag (F02, F03, F07).
* `registrations/`: Xử lý đăng ký và hủy đăng ký sự kiện có khóa dòng dữ liệu (`SELECT ... FOR UPDATE`) chống trùng lặp và vượt sức chứa; xử lý xác nhận tức thì cho MSSV, trạng thái chờ (Pending Confirmation) và tác vụ duyệt tự động theo thứ tự FIFO tại mốc `S - 72h`; xuất danh sách người tham gia (F04, F05).
* `notifications/`: Lưu trữ và truy vấn thông báo trong ứng dụng (N1–N9) gắn liền với giao dịch CSDL, đánh dấu đã đọc, gửi thông báo cho người tham gia, phát thông báo toàn hệ thống và chức năng theo dõi Organizer dành riêng cho Sinh viên (F06).

### 3. `/front-end/src` — Mã nguồn Front-end (React + TypeScript)
Chia theo từng nhóm tính năng và màn hình tương ứng từ `SCR-01` đến `SCR-14`:
* `ui/`: Các thành phần giao diện dùng chung cho toàn ứng dụng như thanh điều hướng (Header), menu tài khoản, chuông thông báo, thẻ sự kiện (EventCard), nhãn trạng thái (StatusBadge) và hộp thoại xác nhận.
* `auth/`: Màn hình Đăng nhập (`SCR-01`), Đăng ký tài khoản (`SCR-02`) và quản lý trạng thái phiên đăng nhập.
* `events/`: Màn hình Khám phá sự kiện (`SCR-03`), Chi tiết sự kiện (`SCR-04`), Bảng điều khiển của Organizer (`SCR-08`) và Tạo/Chỉnh sửa sự kiện (`SCR-09`).
* `registrations/`: Màn hình Xác nhận trạng thái đăng ký (`SCR-05`), Lịch sử đăng ký dành riêng cho Sinh viên có MSSV (`SCR-06`) và Danh sách người đăng ký của Organizer (`SCR-10`).
* `notifications/`: Màn hình Hộp thư thông báo (`SCR-07`) và tương tác theo dõi/hủy theo dõi Organizer.
* `admin/`: Hàng đợi duyệt sự kiện & bản chỉnh sửa (`SCR-11`), Chi tiết xét duyệt sự kiện (`SCR-12`), Quản lý tài khoản/MSSV/yêu cầu Organizer (`SCR-13`) và Gửi thông báo toàn hệ thống (`SCR-14`).