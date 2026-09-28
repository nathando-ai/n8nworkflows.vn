---
title: "🎨 Tự Động Hoá Sáng Tạo Hình Ảnh Siêu Thực Tế Cho Mạng Xã Hội Với RunComfy & Airtable (N8N)"
description: "Workflow này tự động tạo hình ảnh siêu thực tế cho mạng xã hội từ mô tả trong Airtable, sử dụng AI RunComfy + LoRa Models, sau đó cập nhật kết quả vào Airtable và thông báo qua Telegram. Giúp các sếp tiết kiệm thời gian lên đến 80% so với thủ công."
slug: "tieu-dong-hoa-sang-tao-hinh-anh-sieu-thuc-te-runcomfy-airtable"
tags: [n8n, automation, ai-content-generation, airtable, runcomfy, telegram-notification, no-code]
keywords: [n8n workflow tự động hóa, tạo hình ảnh siêu thực tế, RunComfy AI, Airtable API, tự động hóa nội dung mạng xã hội, tự động hóa sáng tạo hình ảnh]
---

# 🚀 **Tự Động Hoá Sáng Tạo Hình Ảnh Siêu Thực Tế Cho Mạng Xã Hội Với RunComfy & Airtable**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Các sếp đang phải **tốn thời gian và công sức** để tạo hình ảnh siêu thực tế cho mạng xã hội (Facebook, Instagram, TikTok) từ những mô tả phức tạp? Hay phải **quan sát và quản lý** quá trình chạy AI liên tục để tránh lãng phí chi phí? Workflow này sẽ **tự động hóa toàn bộ quy trình** từ mô tả → tạo hình → cập nhật kết quả → thông báo kết quả, giúp các sếp **tiết kiệm thời gian, giảm chi phí và nâng cao chất lượng nội dung**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với thủ công: Không cần phải tạo hình ảnh một một.
- **Chất lượng cao nhất**: Sử dụng AI RunComfy + LoRa Models để tạo hình ảnh siêu thực tế.
- **Tự động cập nhật dữ liệu**: Kết quả được tự động lưu vào Airtable và thông báo qua Telegram.
- **Hoạt động liên tục**: Workflow có thể chạy theo lịch trình (schedule) hoặc thủ công.
- **Giảm chi phí**: Hệ thống tự động dừng server khi hoàn thành, tránh lãng phí.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản RunComfy Premium** (để sử dụng API và LoRa Models).
2. **Tài khoản Airtable** (để lưu dữ liệu mô tả và kết quả).
3. **Tài khoản Telegram** (để nhận thông báo kết quả).
4. **API Keys**:
   - **RunComfy API Key** (tạo từ tài khoản RunComfy).
   - **Airtable API Key** (tạo từ Airtable).
   - **Telegram Bot Token** (tạo từ [@BotFather](https://t.me/BotFather)).
5. **LoRa Models** (đã tải lên RunComfy và liên kết với workflow).
6. **Workflow Flux Realism** (tải từ RunComfy và thêm node `rgthree`).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và mở **n8n Editor**.
2. Nhấp vào **Import Workflow** và chọn file JSON (hoặc copy/paste JSON).
3. Chọn **Import** để tải workflow vào.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
#### **A. Cấu Hình Server Node (Trung Tâm Của Workflow)**
Trong node **"RunComfy Start Server"**, các sếp cần điền vào **body parameter**:
```
{
  "WORKFLOW_SERVER_ID": "ID của server RunComfy (một chuỗi duy nhất)",
  "TIME_TO_RUN": 300, // Thời gian chạy (giây), ví dụ: 300 = 5 phút
  "SIZE": "large" // Kích thước server: "medium", "large", hoặc "bigger"
}
```
- **Lưu ý**: Sau khi workflow hoàn thành, **hãy dừng server thủ công** để tiết kiệm chi phí (n8n không tự động dừng).

#### **B. Liên Kết Airtable**
Trong node **"Search All Records from Airtable"**, các sếp cần cấu hình:
1. **Credentials**: Chọn `airtableTokenApi` (đã cấu hình trước).
2. **Query**: Sử dụng mô tả từ cột `pose_1` trong Airtable (ví dụ: `"A girl with red hair"`).
3. **LoRa Model**: Điền tên **exact** của LoRa Model đã tải lên RunComfy (ví dụ: `"my_custom_character"`).

#### **C. Cấu Hình RunComfy Workflow**
Trong node **"RunComfyFluxRealism"**, các sếp cần:
1. **Credentials**: Chọn `httpHeaderAuth` (đã cấu hình trước).
2. **Body Parameter**: Sử dụng cấu trúc JSON từ RunComfy (ví dụ:
   ```json
   {
     "workflow_id": "ID của workflow Flux Realism",
     "input": {
       "prompt": "${{ $json["pose_1"] }}",
       "lora": "${{ $json["LoRa_Name"] }}"
     }
   }
   ```
   - `${{ $json["pose_1"] }}` lấy mô tả từ Airtable.
   - `${{ $json["LoRa_Name"] }}` lấy tên LoRa Model.

#### **D. Thông Báo Kết Quả Qua Telegram**
Trong node **"Final message"**, các sếp cần:
1. **Credentials**: Chọn `telegramApi`.
2. **Message**: Cấu hình tin nhắn tự động (ví dụ:
   ```
   "📸 Hình ảnh đã tạo thành công!\n
   Mô tả: ${{ $json["pose_1"] }}\n
   Link hình: ${{ $json["image_url"] }}"
   ```
   - `${{ $json["image_url"] }}` là đường dẫn đến hình ảnh đã tạo.

#### **E. Cấu Hình Schedule Trigger (Nếu Muốn Chạy Theo Lịch)**
Trong node **"Schedule Trigger"**, các sếp có thể:
- Chọn **thời gian chạy** (ví dụ: 9h sáng hàng ngày).
- Chọn **ngày trong tuần** (ví dụ: Thứ 2 đến Thứ 6).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**: Chạy workflow với **dữ liệu mẫu** từ Airtable để kiểm tra.
2. **Bật Active**: Sau khi kiểm tra thành công, nhấp **Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Xóa Server Sau Khi Hoàn Thành**:
   - Thêm node **"Delete RunComfy Server"** sau khi hình ảnh được tạo để tránh lãng phí.
2. **Lưu Log Kết Quả**:
   - Sử dụng node **StickyNote** để ghi lại thông tin debug (ví dụ: lỗi API, thời gian chạy).
3. **Gửi Báo Cáo Định Kỳ**:
   - Kết hợp với **Google Sheets** hoặc **Email** để gửi báo cáo tổng hợp hình ảnh đã tạo.
4. **Tạo Video/Carousel Từ Hình Ảnh**:
   - Nếu cần, các sếp có thể mở rộng workflow để tự động tạo video hoặc carousel từ hình ảnh.

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa sáng tạo hình ảnh siêu thực tế** mà không cần code. Với chỉ vài bước cấu hình, các sếp sẽ **tiết kiệm thời gian, nâng cao chất lượng nội dung và giảm chi phí** đáng kể.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Airtable, RunComfy và Telegram**.
3. **Bật Active** và bắt đầu tự động hóa!

Nếu gặp vấn đề, các sếp có thể liên hệ với tác giả qua **hello@saits.ai** để hỗ trợ cá nhân hóa workflow theo nhu cầu cụ thể.

---
**Chúc các sếp thành công!** 🚀