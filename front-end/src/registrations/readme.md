# Registrations Pages & Modals (`front-end/src/registrations`)

## 1. Giới thiệu
Thư mục `registrations/` phụ trách hiển thị kết quả đăng ký tham gia, theo dõi vé và lịch sử tham gia của sinh viên, cũng như bảng quản lý người đăng ký dành cho Ban tổ chức.

## 2. Thành viên phụ trách
* **Hoàng Anh Quân** (`24127111`) — Designer & Front-end Developer

## 3. Các màn hình chính
* **Màn hình / Modal Xác nhận đăng ký (`SCR-05`):**
  * Phản hồi kết quả sau khi bấm Đăng ký:
    * **Thành công (Confirmed):** Hiển thị mã vé/xác nhận dành cho sinh viên có MSSV.
    * **Chờ duyệt (Pending Confirmation):** Hiển thị thông báo giải thích vị trí trong danh sách chờ cho người dùng thông thường trước mốc $S - 72h$.
* **Màn hình Lịch sử đăng ký (`SCR-06` - My Registrations):**
  * Giao diện dành cho sinh viên quản lý các sự kiện đã đăng ký.
  * Hiển thị trạng thái vé, thời gian đăng ký và nút Hủy tham gia (chỉ hiển thị nếu còn trong hạn cutoff $C$).
* **Màn hình Quản lý người tham gia (`SCR-10` - Registrant List):**
  * Giao diện cho Organizer quản lý danh sách đăng ký theo từng sự kiện.
  * Tìm kiếm, phân loại người tham gia theo trạng thái (Confirmed / Pending / Cancelled).
  * Nút xuất danh sách người tham gia (CSV/Excel).

## 4. Cấu trúc gợi ý
```text
registrations/
├── RegistrationModal.tsx    # SCR-05
├── MyRegistrationsPage.tsx  # SCR-06
├── RegistrantListPage.tsx   # SCR-10
└── registrationService.ts   # Axios/Fetch API client cho registrations
```
