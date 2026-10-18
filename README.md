# Sổ Giao nhận – Từ chối – Tư vấn mẫu – Bệnh viện Bạch Mai

## Phiên bản 109.72 / 82.73 (API 17)

Frontend: 109.72; backend Apps Script: 82.73. Chỉ sửa nội dung đã chốt; API 17, schema và Sheet giữ nguyên.

- LOCAL mới/reset: mật khẩu ban đầu là mã nhân viên; bắt buộc đổi sau khi đăng nhập, chặn chức năng khác tại backend. SHARED_HHTM giữ nguyên.
- Kiểm soát dữ liệu công khai (giới hạn số mẫu bằng cấu hình, giảm nguy cơ dữ liệu văn bản bị coi là công thức trên Sheets/Excel).
- Excel ba sổ: chuẩn hóa ngày giờ bằng giá trị Date, đồng nhất múi giờ Asia/Ho_Chi_Minh; SID/ngày sinh giữ dạng text.
- TAT tư vấn phân loại đúng đến giây ở ngưỡng 15 phút. Tổng hợp ngày Tư vấn cần chạy lại để cập nhật sang schema thống kê 8.
- Báo cáo Từ chối: tên đơn vị 13px, không dịch lên khi in, bảng 2 và 3 12px, ngày chữ nghiêng, ký tên khoảng trống 90px. SID 12 số và nhãn ngày sinh không xuống dòng trong hai form (ngày sinh 46% / SID 54%).
- Service worker cache version: gm-static-v109.72. Không tự tải lại ứng dụng khi đang nhập.

## Ghi chú vận hành

Hàm `gm_checkDailySummary60()` chỉ kiểm tra trigger/tổng hợp ngày trên dự án Apps Script thực tế, không tự cài trigger. Hàm `gm_upgradeConsultTat15_()` thực hiện tái tổng hợp **mỗi lần tối đa 7 ngày** cần cập nhật; chạy lặp đến khi không còn ngày cũ. Không xóa dữ liệu nguồn.

Archive: hiện giữ cơ chế từ chối thống kê thiếu dữ liệu khi có Archive mà chưa có bộ đọc đủ tin cậy. Chưa bổ sung xóa dữ liệu hoặc migration Archive trong bản này. Chỉ di chuyển/xóa dữ liệu nguồn sau khi triển khai cơ chế đọc lịch sử đã kiểm thử.

## Sửa frontend 102.69

- Bảng 1 Báo cáo Từ chối: hiển thị tên Nhóm XN từ danh mục thay vì mã; mỗi Nhóm XN một dòng, các lý do đúng dòng, gộp các ô thông tin chung của khoa; giữ nguyên dòng tổng và tỷ lệ.
- Các trường nhập liệu dưới XEM BÁO CÁO mặc định ẩn, chỉ hiện sau khi tải báo cáo thành công; đổi bộ lọc thì ẩn lại.
- Giữ nguyên cơ chế cập nhật bản xem trước ngay khi nhập; nút LƯU chỉ ghi Google Sheets như trước.
- Các định dạng 100.69–101.69 giữ nguyên; không cần thay đổi backend.

## FIX 104.71 / 81.71

- LOCAL: mật khẩu mới tối thiểu 4 ký tự (có thể 4 chữ số), mật khẩu mặc định vẫn là mã nhân viên; SHARED_HHTM giữ chuẩn tối thiểu 8 ký tự. Xóa ghi chú ở màn hình bắt buộc đổi, căn giữa nút, ẩn nút và hiển thị spinner khi lưu; bảo vệ chống gửi trùng.
- Khi đổi người đăng nhập trên cùng máy: xóa tất cả form, các trường người thực hiện/ẩn ID, kết quả thống kê, báo cáo, tổng mẫu và cấu hình đang hiển thị; đặt lại state theo phiên; kết quả API cũ không được áp dụng sang phiên mới. Giữ nguyên hàng đợi chưa đồng bộ theo khóa tài khoản; cảnh báo khi còn bản nhập chưa lưu.
- Báo cáo Từ chối: giữ chữ 13px, tăng line-height 1.4, đệm trên và không dịch lên trong bản in để tránh cắt dấu tiếng Việt.
- Không thay đổi nghiệp vụ, Sheet, route API hay các danh mục quản trị.

Kiểm tra cục bộ: cú pháp frontend/backend, mô phỏng đổi tài khoản A→B và chặn phản hồi phiên cũ; chưa thay thế nghiệm thu với tài khoản thực trên dữ liệu đang vận hành.

## Bổ sung 104.71 / 81.71

- Giao nhận mẫu: bộ lọc Viện/TT/Khoa thực hiện phụ thuộc Điểm tập trung (chuyên ngành) hoặc Điểm tại khoa (nhóm xét nghiệm). Chọn đợt có mẫu phù hợp nhưng giữ nguyên toàn bộ mẫu và tổng của đợt. Lọc đồng nhất XEM DS, phân trang, Excel, cache và danh sách cục bộ. Không thêm Sheet hay cột.
- Nhãn nút Thống kê: THỐNG KÊ. Hai ô ngày sinh/SID chia 50%–50% tại Từ chối và Tư vấn.

## FIX 105.71 – Trạng thái Cài đặt sau đăng xuất

- Dùng cùng cấu trúc `State.settings` cho khởi tạo và reset phiên đăng nhập; không còn thiếu `adminLists` khi XEM DANH SÁCH sau đăng xuất/đăng nhập lại.
- Ngăn kết quả tải danh sách, preload Cài đặt, tìm nhân viên reset mật khẩu và cấu hình ngưỡng thuộc phiên cũ cập nhật state phiên mới.
- Không sửa API, schema, Sheet và logic ghi dữ liệu backend.

## QR gửi mẫu cố định – 106.72/82.73

- QR mới được tạo với `mode=send`, `site`, `point`, `pointName` (tên nhận dạng chỉ để hiển thị nhanh). CSHN/CSNB hardcode tên cơ sở ở frontend; mã và tên Điểm tiếp nhận lấy thẳng từ QR để hiển thị tức thì.
- Nhãn cơ sở và điểm nhận cố định, không cho đổi. Nút GỬI MẪU chỉ được mở sau khi `publicBootstrap` hoặc `publicCatalogVersion` xác minh cơ sở, điểm nhận, trạng thái hoạt động và danh mục.
- Frontend cache theo `MaCoSo + MaDiemNhan`; backend cache lookup và danh mục riêng điểm nhận cũng phân biệt cơ sở.
- Với QR tập trung, số mẫu theo chuyên ngành; QR tại khoa, theo nhóm XN. Không hỗ trợ QR cũ thiếu `site` vì chưa phát hành QR.
- API schema 17, không thêm Sheet, không thay đổi hợp đồng API hoặc nghiệp vụ ghi.

## FIX giao diện 107.72 (chỉ frontend)

- Nền đăng nhập phủ hết khung ứng dụng, bao gồm vùng footer; bỏ nền riêng của footer.
- Dùng duy nhất một footer trong suốt; vẫn hiển thị trên màn hình chờ nhờ thứ tự lớp phù hợp.
- Điện thoại/máy tính bảng: tự ẩn footer khi phát hiện bàn phím ảo để không che biểu mẫu; hiện lại khi đóng bàn phím.
- Không thay đổi nghiệp vụ, API hoặc dữ liệu; Apps Script giữ 82.73.

## FIX frontend 108.72 – bàn phím iPhone

- Sửa lỗi footer vẫn nhô lên khi Safari iPhone không phát tín hiệu co `visualViewport` đủ lớn.
- Trên màn hình nhỏ, ẩn footer ngay khi focus vào ô nhập văn bản, không còn phụ thuộc ngưỡng giảm chiều cao 130 px; tự hiển thị lại khi thoát ô nhập.
- Giữ nguyên nền đăng nhập, màn hình chờ, QR gửi mẫu và logic nghiệp vụ; backend vẫn 82.73.


## FIX mobile 109.72 – cuộn tự nhiên (iPhone/Android)

- Màn hình đăng nhập và biểu mẫu gửi mẫu QR trên điện thoại cuộn theo trang (document), không khóa bởi chiều cao visualViewport hoặc vùng .app-shell flex cố định.
- Footer duy nhất nằm cuối nội dung; không có vùng chân trang nổi che ô nhập khi mở bàn phím. Không dùng JS đo kích thước bàn phím để ẩn footer.
- Màn hình chờ vẫn đưa cùng footer lên phía trước lớp chờ; desktop và các bảng quản trị giữ nguyên.
- Backend 82.73, API Schema 17 và các Sheet không thay đổi.
