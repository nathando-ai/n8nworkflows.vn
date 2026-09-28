---
title: "🚀 Tự động hóa tạo mô hình 3D (.glb) từ ảnh 2D với Hunyuan3D v2 và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động biến ảnh 2D thành mô hình 3D định dạng .glb bằng AI Hunyuan3D v2 thông qua Fal.ai và lưu kết quả vào Google Sheets."
slug: "tao-mo-hinh-3d-tu-anh-hunyuan3d-google-sheets-n8n"
tags: [n8n, automation, no-code, ai, 3d-generation, google-sheets, hunyuan3d]
keywords: [n8n workflow, tạo 3d từ ảnh, hunyuan3d v2, fal ai, google sheets automation, chuyển ảnh thành 3d glb]
---

# 🚀 Tự động hóa tạo mô hình 3D (.glb) từ ảnh 2D với Hunyuan3D v2 và Google Sheets

Các sếp có đang đau đầu khi phải dựng hình 3D thủ công cho hàng loạt ảnh sản phẩm, bản thảo thời trang hay ý tưởng thiết kế? Việc này ngốn rất nhiều thời gian, chi phí nhân sự và khó có thể mở rộng hàng loạt. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực đỉnh giúp tự động hóa 100% quy trình: **Lấy ảnh từ Google Sheets ➡️ Gửi sang AI (Hunyuan3D v2) xử lý ➡️ Kiểm tra trạng thái ➡️ Nhận kết quả file 3D (.glb) và lưu ngược lại Google Sheets** mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến kho ảnh 2D thành mô hình 3D định dạng `.glb` một cách tự động theo lịch trình định sẵn hoặc chạy thủ công.
- **Tiết kiệm thời gian & chi phí:** Loại bỏ hoàn toàn khâu xuất/nhập dữ liệu thủ công và thao tác trên web tạo 3D từng cái một.
- **Tích hợp thông minh:** Kết hợp mượt mà giữa Google Sheets và các mô hình AI tạo sinh (Generative AI) hàng đầu qua Fal.ai.
- **Vòng lặp thông minh (Polling Loop):** Tự động kiểm tra trạng thái render 3D mỗi 30 giây cho đến khi hoàn thành mà không làm treo hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google Sheets** (đã chuẩn bị sẵn file chứa danh sách ảnh).
- **Tài khoản Fal.ai** kèm API Key để gọi mô hình Hunyuan3D v2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import trực tiếp file JSON thông qua menu giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Schedule Trigger / When clicking ‘Test workflow’:** Nơi khởi chạy quy trình (chạy thủ công hoặc định kỳ mỗi 15 phút).
- **Get new image (Google Sheets):** 
  - Chọn tài khoản kết nối Google Sheets (OAuth2).
  - Trỏ đến file Sheet ID của các sếp và chọn đúng Sheet Name.
  - Đảm bảo Google Sheet có các cột cơ bản: `IMAGE_URL` (link ảnh đầu vào) và `RESULT_GLB` (link nhận kết quả).
- **Submit to Hunyuan3D (HTTP Request):** 
  - Cấu hình Header chứa API Key của Fal.ai.
  - Trỏ đến endpoint API của mô hình Hunyuan3D v2 với payload truyền vào là đường dẫn ảnh (`IMAGE_URL`).
- **Wait 30 sec & Check Status & Is Completed?:** 
  - Vòng lặp chờ đợi trạng thái render từ AI. Node `Is Completed?` sẽ kiểm tra xem trạng thái trả về đã là `COMPLETED` hay chưa. Nếu chưa, quay lại đợi tiếp; nếu rồi, tiến hành bước tiếp theo.
- **Get Final Result (HTTP Request):** 
  - Lấy đường dẫn file mô hình `.glb` hoàn chỉnh từ kết quả trả về của AI.
- **Update Result (Google Sheets):** 
  - Chọn thao tác `update`.
  - Ghi đè đường dẫn file `.glb` vừa nhận được vào cột `RESULT_GLB` tương ứng trên dòng của Google Sheets.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử với 1 dòng dữ liệu mẫu xem file `.glb` có được trả về Google Sheets thành công không.
- Sau khi test xanh mượt, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối luồng để bot bắn thông báo về máy mỗi khi một mô hình 3D được render xong.
- **Xử lý lỗi (Error Handling):** Cấu hình thêm nhánh `Error Trigger` để nếu AI gặp lỗi khi xử lý ảnh nặng, hệ thống sẽ tự động ghi chú "Failed" vào Google Sheets thay vì bị dừng đột ngột.
- **Lưu trữ file tự động:** Thay vì lưu trực tiếp link tạm từ AI, các sếp có thể tích hợp thêm bước tải file `.glb` về lưu trữ trực tiếp trên Google Drive hoặc AWS S3 của doanh nghiệp.

### 📌 Kết luận
Tự động hóa việc tạo mô hình 3D từ ảnh 2D chưa bao giờ dễ dàng đến thế với sự kết hợp giữa n8n, Google Sheets và Hunyuan3D v2. Hãy áp dụng ngay vào quy trình sản xuất nội dung hoặc thương mại điện tử của các sếp để tối ưu hóa năng suất ngay hôm nay!