---
title: "🚀 Tự động tạo mô hình 3D và Texture từ ảnh 2D bằng AI với Hunyuan3D trên n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow tự động hóa biến ảnh 2D thành mô hình 3D và texture chuyên nghiệp sử dụng mô hình Hunyuan3D AI qua Replicate."
slug: "tao-mo-hinh-3d-tu-anh-voi-hunyuan3d-n8n"
tags: [n8n, automation, 3d-ai, hunyuan3d, replicate, ai-agents]
keywords: [n8n workflow, tạo mô hình 3d từ ảnh, hunyuan3d ai, replicate api, tự động hóa 3d, AI content creation]
---

# 🚀 Tự động tạo mô hình 3D và Texture từ ảnh 2D bằng AI với Hunyuan3D trên n8n

Việc chuyển đổi các bản vẽ, hình ảnh sản phẩm 2D thành mô hình 3D hoàn chỉnh kèm texture (chất liệu) thường đòi hỏi rất nhiều thời gian, kỹ năng đồ họa phức tạp và các phần mềm chuyên dụng đắt tiền. Điều này tạo ra nút thắt lớn cho các doanh nghiệp Thương mại điện tử, Game Studio hoặc nhà sáng tạo nội dung khi muốn số hóa hàng loạt sản phẩm.

Giải pháp là gì? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: nhận ảnh đầu vào, gọi mô hình AI **Hunyuan3D 2.1** thông qua Replicate API để tạo mô hình 3D, kiểm tra trạng thái xử lý và trả về kết quả hoàn chỉnh mà không cần một dòng code phức tạp nào từ các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến ảnh chụp sản phẩm hoặc bản vẽ 2D thành file mô hình 3D (.obj, .gltf,...) kèm texture chỉ với vài cú click.
- **Tiết kiệm chi phí khổng lồ:** Giảm thiểu thời gian dựng hình thủ công (3D modeling) cho đội ngũ thiết kế.
- **Quy trình bất đồng bộ thông minh:** Tích hợp cơ chế chờ (Wait) và kiểm tra trạng thái (Status Check) tự động để xử lý các tác vụ AI nặng mà không sợ bị timeout.
- **Dễ dàng mở rộng:** Có thể kết hợp thêm Google Drive để lưu trữ file 3D hoặc gửi thông báo qua Telegram/Slack khi hoàn thành.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc n8n Cloud).
- **Replicate Account:** Tài khoản trên Replicate kèm theo **API Token** (vì workflow sử dụng mô hình `ndreca/hunyuan3d-2.1-test`).
- **Hình ảnh đầu vào (Input Image):** Link URL công khai của hình ảnh 2D muốn chuyển đổi sang 3D.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm (`...`) ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes cốt lõi được thiết kế để gọi API, xử lý vòng lặp chờ và nhận kết quả từ Replicate:

1. **On clicking 'execute' (`manualTrigger`):** Node kích hoạt thủ công để test workflow. Các sếp có thể thay thế bằng *Webhook*, *Google Drive Trigger* hoặc *Telegram Trigger* khi muốn chạy tự động.
2. **Set API Key (`set`):** 
   - Nơi lưu trữ thông tin cấu hình như Replicate API Key và link hình ảnh đầu vào.
   - *Cách làm:* Nhập Replicate API Token của các sếp vào biến tương ứng trong node này.
3. **Create Prediction (`httpRequest`):**
   - Gửi yêu cầu khởi tạo tiến trình tạo mô hình 3D tới Replicate API sử dụng mô hình `ndreca/hunyuan3d-2.1-test`.
   - Đảm bảo header có chứa `Authorization: Bearer <Replicate_API_Key>` lấy từ node *Set API Key*.
4. **Extract Prediction ID (`code`):**
   - Sử dụng JavaScript cơ bản để bóc tách `Prediction ID` từ phản hồi của Replicate, phục vụ cho việc kiểm tra trạng thái ở các bước sau.
5. **Wait (`wait`):**
   - Tạm dừng workflow trong vài giây (ví dụ: 10-15 giây) để AI có thời gian xử lý việc tạo mô hình 3D trước khi gọi API kiểm tra lại.
6. **Check Prediction Status (`httpRequest`):**
   - Gọi lại Replicate API thông qua `Prediction ID` để kiểm tra xem tiến trình tạo 3D đã hoàn tất hay chưa.
7. **Check If Complete (`if`):**
   - Kiểm tra trạng thái trả về (`status === 'succeeded'`). Nếu hoàn tất, chuyển sang bước xử lý kết quả; nếu chưa, quay lại vòng chờ.
8. **Process Result (`code`):**
   - Trích xuất link tải file mô hình 3D và texture hoàn chỉnh từ phản hồi thành công của AI để sử dụng cho các bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Nhấp vào nút **Execute Workflow** để chạy thử với một ảnh mẫu.
- Kiểm tra kết quả trả về ở node cuối cùng (`Process Result`).
- Nếu mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** ở góc trên bên phải để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Thêm node *Google Drive* hoặc *AWS S3* ngay sau node `Process Result` để tự động tải và lưu trữ các file mô hình 3D vềkho lưu trữ của doanh nghiệp.
- **Thông báo qua Chat:** Tích hợp thêm node *Telegram* hoặc *Slack* để gửi tin nhắn kèm hình ảnh kết quả/link tải ngay khi AI dựng xong mô hình 3D.
- **Xử lý hàng loạt:** Kết hợp với node *Google Sheets* để đọc danh sách hàng chục link ảnh sản phẩm và tự động hóa toàn bộ quá trình dựng hình 3D ban đêm (Batch Processing).

### 📌 Kết luận
Workflow tích hợp Hunyuan3D AI này là công cụ tuyệt vời giúp các sếp tối ưu hóa quy trình sản xuất nội dung 3D một cách tự động, tiết kiệm hàng đống thời gian và chi phí nhân sự. Hãy import ngay vào n8n và bắt đầu "lên đồ" cho hệ thống của mình nhé!