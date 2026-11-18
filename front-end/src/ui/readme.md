# Shared UI Components (`front-end/src/ui`)

## 1. Giới thiệu
Thư mục `ui/` lưu trữ toàn bộ các thành phần giao diện (UI components) tái sử dụng trong hệ thống Front-end của CampusHub, được xây dựng dựa trên React 18, TypeScript và Tailwind CSS.

## 2. Thành viên phụ trách
* **Hoàng Anh Quân** (`24127111`) — Designer & Front-end Developer

## 3. Các thành phần chính
* **Điều hướng & Khung ứng dụng:**
  * `Header` / `Navbar`: Thanh điều hướng đầu trang, logo thương hiệu, ô tìm kiếm nhanh, nút đăng nhập/đăng ký hoặc menu người dùng.
  * `NotificationBell`: Chuông thông báo hiển thị số lượng chưa đọc theo thời gian thực và dropdown xem nhanh thông báo.
  * `Footer`: Chân trang hiển thị thông tin bản quyền và liên kết dự án.
* **Hiển thị dữ liệu:**
  * `EventCard`: Thẻ sự kiện tiêu chuẩn hiển thị ảnh banner, tên sự kiện, ngày giờ tổ chức, địa điểm, tag và trạng thái số chỗ còn trống.
  * `StatusBadge`: Huy hiệu trạng thái quy ước màu sắc chuẩn hóa (`Pending Confirmation`, `Registered`, `Event Full`, `Draft`, `Pending Approval`, `Published`, `Cancelled`).
  * `Pagination`: Điều hướng phân trang danh sách (10 phần tử/trang).
  * `EmptyState`: Trạng thái trống thân thiện khi danh sách không có dữ liệu hoặc không tìm thấy kết quả.
* **Tương tác & Phản hồi:**
  * `ConfirmModal`: Hộp thoại xác nhận đa năng (xác nhận hủy đăng ký, hủy sự kiện, duyệt/từ chối).
  * `LoadingSpinner` / `Skeleton`: Trạng thái chờ tải dữ liệu.

## 4. Quy ước
* Đảm bảo tính tương thích hiển thị chuẩn trên 2 độ phân giải: Desktop (`1366x768`) và Mobile (`360x800`).
* Tuân thủ các nguyên tắc khả năng tiếp cận (Accessibility / WCAG).
