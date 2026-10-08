Sổ giao nhận / từ chối mẫu - Version 58.41
- Frontend: index 58.41.html / index.html
- Backend: Code 58.41.gs
- PWA: service-worker 58.41.js / service-worker.js + manifest/icons

Nâng từ 57.40:
1. Cập nhật Code 58.41.gs vào Apps Script.
2. Chạy gm_upgradeSchemaTo5841() MỘT LẦN trước khi sử dụng bản mới với dữ liệu hiện hữu.
3. Hàm nâng schema bổ sung PointType cho DIEM_NHAN_MAU, SampleMode cho GIAO_NHAN và chuyển Master Vị trí phát hiện/Lý do từ chối sang Master chung hai cơ sở. SampleJson lịch sử được giữ nguyên.
4. Sau đó cập nhật frontend/PWA.

Lưu ý: không đổi Script ID/Deployment ID khi triển khai; file này chỉ là gói mã nguồn, chưa triển khai.
