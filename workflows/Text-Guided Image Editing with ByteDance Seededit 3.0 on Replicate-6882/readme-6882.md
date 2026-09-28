---
title: "🎨 Tự động hóa chỉnh sửa ảnh theo văn bản với ByteDance Seededit 3.0 trên Replicate"
description: "Hướng dẫn tự động hóa chỉnh sửa ảnh theo văn bản với ByteDance Seededit 3.0 trên Replicate bằng n8n. Tiết kiệm thời gian và nâng cao hiệu suất tạo nội dung."
slug: "tu-dong-hoa-chinh-sua-anh-theo-van-ban-byte-dance-seededit-3-0"
tags: [n8n, automation, no-code, content creation, multimodal AI]
keywords: [n8n workflow, tự động hóa, chỉnh sửa ảnh, ByteDance Seededit, Replicate]
---

# 🎨 Tự động hóa chỉnh sửa ảnh theo văn bản với ByteDance Seededit 3.0 trên Replicate

[Các sếp đang gặp khó khăn khi phải chỉnh sửa ảnh theo văn bản một cách thủ công? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình với n8n, tiết kiệm thời gian và nâng cao hiệu suất tạo nội dung.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quy trình chỉnh sửa ảnh theo văn bản
- Tiết kiệm thời gian đáng kể trong quá trình tạo nội dung
- Nâng cao hiệu suất và chất lượng hình ảnh đầu ra
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Tích hợp dễ dàng với các hệ thống khác thông qua n8n
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Replicate và API Key (để truy cập ByteDance Seededit 3.0 model)
- Ảnh đầu vào (định dạng hỗ trợ: JPG, PNG)
- Văn bản hướng dẫn chỉnh sửa (prompt)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/6882)
2. Nhấn nút "Download" để tải file JSON
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Set API Key** node:
   - Thêm credentials cho Replicate API
   - Nhập API Key của bạn vào trường "apiKey"

2. **Create Prediction** node:
   - Đảm bảo phương thức là POST
   - URL: `https://api.replicate.com/v1/predictions`
   - Headers:
     ```
     Content-Type: application/json
     Authorization: Bearer {{ $node["Set API Key"].json["apiKey"] }}
     ```
   - Body:
     ```json
     {
       "version": "25d2f75ecda0c0bed344f811738e6abf1f395414a9b42bc09b04206588f9e183",
       "input": {
         "prompt": "{{ $node["On clicking 'execute'"].json["prompt"] }}",
         "image": "{{ $node["On clicking 'execute'"].json["image"] }}"
       }
     }
     ```

3. **Wait** node:
   - Thiết lập thời gian chờ phù hợp (thường từ 30s đến 2 phút tùy thuộc vào kích thước ảnh)

4. **Check Prediction Status** node:
   - Đảm bảo phương thức là GET
   - URL: `https://api.replicate.com/v1/predictions/{{ $node["Extract Prediction ID"].json["predictionId"] }}`
   - Headers:
     ```
     Authorization: Bearer {{ $node["Set API Key"].json["apiKey"] }}
     ```

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute" để chạy workflow với dữ liệu mẫu
2. Kiểm tra kết quả ở node cuối cùng (Process Result)
3. Bật "Active" workflow để sử dụng trong thực tế

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack/Telegram**: Thêm node để nhận thông báo khi quá trình hoàn thành
2. **Lưu log**: Thêm node để lưu lịch sử các lần chỉnh sửa
3. **Xử lý hàng loạt**: Sử dụng vòng lặp để xử lý nhiều ảnh cùng lúc
4. **Tối ưu hóa prompt**: Thêm node để tự động tạo prompt phù hợp từ mô tả văn bản

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình chỉnh sửa ảnh theo văn bản với ByteDance Seededit 3.0 trên Replicate. Bằng cách tích hợp với n8n, các sếp có thể tiết kiệm thời gian đáng kể và nâng cao hiệu suất tạo nội dung. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của đội ngũ!