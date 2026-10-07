Sổ giao nhận / từ chối mẫu - Version 57.40
- Frontend: index 57.40.html / index.html
- Backend: Code 57.40.gs
- PWA: service-worker 57.40.js / service-worker.js + manifest/icons
- Thay đổi vòng này: Cài đặt mở tab ngay, không dùng màn hình chờ toàn màn hình; toàn bộ dữ liệu Cài đặt theo quyền tải bằng một settingsPreload duy nhất, mỗi Sheet cấu hình đọc một lần trong request, cache theo user trong phiên; timeout/retry hữu hạn và lỗi hiển thị trong vùng Cài đặt.
