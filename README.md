# Sổ Giao nhận – Từ chối – Tư vấn mẫu – Bệnh viện Bạch Mai

## Phiên bản 99.69 / 79.69 (API 17)

Frontend: 99.69; backend Apps Script: 79.69. Chỉnh sửa từ bản 98.68 / 78.68, không đổi schema dữ liệu hoặc tên các Sheet.

- LOCAL mới/reset: mật khẩu ban đầu là mã nhân viên; bắt buộc đổi sau khi đăng nhập, chặn chức năng khác tại backend. SHARED_HHTM giữ nguyên.
- Kiểm soát dữ liệu công khai (giới hạn số mẫu bằng cấu hình, giảm nguy cơ dữ liệu văn bản bị coi là công thức trên Sheets/Excel).
- Excel ba sổ: chuẩn hóa ngày giờ bằng giá trị Date, đồng nhất múi giờ Asia/Ho_Chi_Minh; SID/ngày sinh giữ dạng text.
- TAT tư vấn phân loại đúng đến giây ở ngưỡng 15 phút. Tổng hợp ngày Tư vấn cần chạy lại để cập nhật sang schema thống kê 8.
- Báo cáo Từ chối: tên đơn vị 11px, bảng 2 và 3 12px, ngày chữ nghiêng, ký tên khoảng trống 90px. SID 12 số và nhãn ngày sinh không xuống dòng trong hai form.
- Service worker cache version: gm-static-v99.69. Không tự tải lại ứng dụng khi đang nhập.

## Ghi chú vận hành

Hàm `gm_checkDailySummary60()` chỉ kiểm tra trigger/tổng hợp ngày trên dự án Apps Script thực tế, không tự cài trigger. Hàm `gm_upgradeConsultTat15_()` thực hiện tái tổng hợp **mỗi lần tối đa 7 ngày** cần cập nhật; chạy lặp đến khi không còn ngày cũ. Không xóa dữ liệu nguồn.

Archive: hiện giữ cơ chế từ chối thống kê thiếu dữ liệu khi có Archive mà chưa có bộ đọc đủ tin cậy. Chưa bổ sung xóa dữ liệu hoặc migration Archive trong bản này. Chỉ di chuyển/xóa dữ liệu nguồn sau khi triển khai cơ chế đọc lịch sử đã kiểm thử.
