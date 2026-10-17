# Sổ Giao nhận – Từ chối – Tư vấn mẫu – Bệnh viện Bạch Mai

## Phiên bản 102.69 / 79.69 (API 17)

Frontend: 102.69; backend Apps Script: 79.69. Chỉ cập nhật frontend trên nền 101.69; backend, API 17, schema và Sheet giữ nguyên.

- LOCAL mới/reset: mật khẩu ban đầu là mã nhân viên; bắt buộc đổi sau khi đăng nhập, chặn chức năng khác tại backend. SHARED_HHTM giữ nguyên.
- Kiểm soát dữ liệu công khai (giới hạn số mẫu bằng cấu hình, giảm nguy cơ dữ liệu văn bản bị coi là công thức trên Sheets/Excel).
- Excel ba sổ: chuẩn hóa ngày giờ bằng giá trị Date, đồng nhất múi giờ Asia/Ho_Chi_Minh; SID/ngày sinh giữ dạng text.
- TAT tư vấn phân loại đúng đến giây ở ngưỡng 15 phút. Tổng hợp ngày Tư vấn cần chạy lại để cập nhật sang schema thống kê 8.
- Báo cáo Từ chối: tên đơn vị 13px, dịch lên 5px, bảng 2 và 3 12px, ngày chữ nghiêng, ký tên khoảng trống 90px. SID 12 số và nhãn ngày sinh không xuống dòng trong hai form (ngày sinh 46% / SID 54%).
- Service worker cache version: gm-static-v102.69. Không tự tải lại ứng dụng khi đang nhập.

## Ghi chú vận hành

Hàm `gm_checkDailySummary60()` chỉ kiểm tra trigger/tổng hợp ngày trên dự án Apps Script thực tế, không tự cài trigger. Hàm `gm_upgradeConsultTat15_()` thực hiện tái tổng hợp **mỗi lần tối đa 7 ngày** cần cập nhật; chạy lặp đến khi không còn ngày cũ. Không xóa dữ liệu nguồn.

Archive: hiện giữ cơ chế từ chối thống kê thiếu dữ liệu khi có Archive mà chưa có bộ đọc đủ tin cậy. Chưa bổ sung xóa dữ liệu hoặc migration Archive trong bản này. Chỉ di chuyển/xóa dữ liệu nguồn sau khi triển khai cơ chế đọc lịch sử đã kiểm thử.

## Sửa frontend 102.69

- Bảng 1 Báo cáo Từ chối: hiển thị tên Nhóm XN từ danh mục thay vì mã; mỗi Nhóm XN một dòng, các lý do đúng dòng, gộp các ô thông tin chung của khoa; giữ nguyên dòng tổng và tỷ lệ.
- Các trường nhập liệu dưới XEM BÁO CÁO mặc định ẩn, chỉ hiện sau khi tải báo cáo thành công; đổi bộ lọc thì ẩn lại.
- Giữ nguyên cơ chế cập nhật bản xem trước ngay khi nhập; nút LƯU chỉ ghi Google Sheets như trước.
- Các định dạng 100.69–101.69 giữ nguyên; không cần thay đổi backend.
