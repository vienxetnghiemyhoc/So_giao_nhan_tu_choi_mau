# Sổ giao nhận / từ chối mẫu – v61.43

Bản sửa lỗi chuyển phiên giữa hai cơ sở trên nền v60.42.

## Phiên bản
- Frontend: **61** (`index.html` / `index 61.43.html`)
- Backend: **43** (`Code 61.43.gs`)
- API schema: **16** (không đổi schema dữ liệu)

## Nội dung sửa
1. Chuẩn hóa logout/chuyển cơ sở:
   - Giữ nguyên cơ chế đồng bộ queue trước logout.
   - Sau `authLogout`, xóa toàn bộ runtime context của user/cơ sở cũ: catalog đang dùng, config/transport version tạm, điểm tiếp nhận, PointType/SampleMode, requestId, module state và prefetch promise.
   - Cache catalog vẫn lưu riêng theo `MaCoSo`; login cơ sở mới chỉ đọc đúng cache của cơ sở đó.
2. `loadCache()` luôn reset runtime trước khi nạp cache của cơ sở mới; cache thiếu/sai schema không còn để state cơ sở trước rơi sang cơ sở sau.
3. `staffPreload` và `staffBootstrap` không tải cấu hình vận chuyển trong request login/bootstrap.
   - Transport lazy-load riêng qua `staffTransportCatalogs` sau khi app đã vào màn hình chính.
   - Response transport của phiên cũ bị bỏ qua nếu user/cơ sở đã thay đổi.
4. Khi `TRANSPORT_CONFIG_VERSION` thay đổi, cache transport cũ bị đánh dấu invalid và tự tải lại.
5. Tối ưu backend:
   - `getActiveReceivePointAssignments_()` chỉ đọc các sheet cần thiết, không kéo toàn bộ catalog nhóm xét nghiệm để xác định điểm được phân công.
   - `getTestGroupsForSite_()` batch-read Master/Applicability một lần thay vì đọc lặp theo từng chuyên ngành.

## Migration
- Không thay đổi schema so với v58.41.
- Nếu đã chạy `gm_upgradeSchemaTo5841()` thì **không chạy lại**.
- Nếu chưa từng nâng từ v57.40 thì chạy `gm_upgradeSchemaTo5841()` đúng 1 lần.

Chưa upload GitHub / chưa deploy trong gói này.
