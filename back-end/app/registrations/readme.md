# Registrations Module (`back-end/app/registrations`)

## 1. Giới thiệu
Thư mục `registrations/` xử lý quy trình đăng ký tham gia sự kiện, bảo đảm kiểm soát đồng thời chống vượt sức chứa (overbooking), hủy đăng ký và tác vụ ưu tiên tự động (Tính năng cốt lõi **F04**, **F05**).

## 2. Thành viên phụ trách
* **Phạm Nhựt Anh** (`24127014`) — Back-end Developer

## 3. Trách nhiệm & Chức năng chính
* **Đăng ký tham gia sự kiện (`UC-10`):**
  * Sử dụng kỹ thuật khóa dòng PostgreSQL (`SELECT ... FOR UPDATE`) để xử lý tranh chấp đồng thời khi nhiều người đăng ký vào các slot cuối cùng.
  * **Sinh viên có MSSV:** Xác nhận giữ chỗ ngay lập tức (`Confirmed`) nếu sự kiện còn chỗ.
  * **Người dùng thông thường (non-MSSV):** Đưa vào danh sách chờ xác nhận (`Pending Confirmation`), không chiếm giữ slot chính thức.
* **Hủy đăng ký / Rút yêu cầu (`UC-11`):**
  * Kiểm tra chu kỳ đăng ký (`cycle_no`) và thời điểm cutoff $C$ quy định theo từng sự kiện.
* **Tác vụ tự động duyệt ưu tiên (`PriorityReleaseTask`):**
  * Thực thi khi khởi động server và kích hoạt qua cron job / internal webhook định kỳ mỗi **5 phút**.
  * Tự động giải phóng các slot còn trống và duyệt theo thứ tự FIFO cho danh sách `Pending Confirmation` tại mốc thời gian $S - 72h$ (72 giờ trước khi sự kiện diễn ra).
* **Báo cáo & Danh sách:**
  * API Lịch sử đăng ký của sinh viên (`My Registrations` - `UC-12`).
  * API Danh sách người tham gia (`Registrant List` - `UC-13`) cho Organizer kèm tính năng xuất dữ liệu.

## 4. Cấu trúc gợi ý
```text
registrations/
├── __init__.py
├── router.py         # APIRouter cho /api/registrations
├── schemas.py        # Pydantic schemas (RegistrationRequest, RegistrationResponse, RosterItem)
├── service.py        # Logic khóa dòng dữ liệu, kiểm tra sức chứa, hủy vé
└── tasks.py          # PriorityReleaseTask (FIFO matching tại mốc S - 72h)
```
