---
title: "🚀 Tự Động Hóa Trả Lời Trên Emelia → Thông Báo Ngay Lên Mattermost (Không Cần Code)"
description: "Khi khách hàng trả lời tin nhắn trên Emelia, hệ thống tự động gửi thông báo ngay lên Mattermost để team Sales/Marketing phản hồi nhanh chóng. Giảm thời gian phản hồi từ 5 phút xuống 0 giây!"
slug: "tu-dong-hoa-emelia-mattermost"
tags: [n8n, automation, sales-marketing, emelia, mattermost, no-code]
keywords: [n8n workflow emelia mattermost, tự động hóa sales marketing, phản hồi khách hàng nhanh, n8n tự động hóa tin nhắn]
---

# 🚀 **Tự Động Hóa Trả Lời Emelia → Thông Báo Mattermost: Phản Hồi Khách Hàng Trong Vài Giây**

### **Nỗi Đau Của Các Sếp Sales/Marketing**
Các sếp đã từng phải:
- **Làm thủ công**: Theo dõi từng tin nhắn trên Emelia, sau đó copy-paste vào Mattermost để team phản hồi.
- **Mất thời gian**: Trễ phản hồi dẫn đến mất khách hàng hoặc cơ hội bán hàng.
- **Rủi ro sai sót**: Thông tin bị nhầm lẫn khi chuyển đổi giữa các nền tảng.

**Workflow này giải quyết tất cả!** Khi khách hàng trả lời tin nhắn trên Emelia, hệ thống tự động chuyển thông báo sang Mattermost, giúp team phản hồi **ngay lập tức** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không bị gián đoạn, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thời**: Thông báo tự động lên Mattermost khi khách hàng trả lời → **giảm thời gian phản hồi từ 5 phút xuống 0 giây**.
- **Tiết kiệm thời gian**: Không cần copy-paste thủ công → team có thể tập trung vào chiến lược bán hàng.
- **Chính xác 100%**: Thông tin được chuyển tự động, tránh sai sót khi chuyển đổi giữa các nền tảng.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào giờ làm việc của nhân viên.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần:
1. **Tài khoản Emelia**:
   - API Key của Emelia (được tạo trong **Cài đặt → API Keys**).
   - **Credentials** trong n8n: `emeliaApi` (điền vào **n8n Editor → Credentials → Add Credential → Emelia**).

2. **Tài khoản Mattermost**:
   - **Token API** của Mattermost (thường được tạo trong **Admin → API Tokens**).
   - **Credentials** trong n8n: `mattermostApi` (điền vào **n8n Editor → Credentials → Add Credential → Mattermost**).
   - **Channel ID** của nhóm Mattermost muốn nhận thông báo (có thể tìm trong URL khi mở channel).

3. **n8n Editor**:
   - Các sếp cần **n8n self-hosted** (không dùng phiên bản miễn phí trên cloud).
   - **Phiên bản n8n**: 1.0+ (đảm bảo hỗ trợ node `emeliaTrigger` và `mattermost`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/1039) và import vào n8n Editor:
  ```bash
  1. Mở n8n Editor → Nhấn "Import" → Chọn file JSON.
  2. Chọn "Import" để hoàn tất.
  ```
- **Cách 2**: Copy toàn bộ JSON từ [link trên](https://n8n.io/workflows/1039) và dán vào **n8n Editor → Import Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này chỉ có **2 node**, nhưng các sếp **phải cấu hình chính xác** để hoạt động:

##### **Node 1: Emelia Trigger**
- **Loại node**: `emeliaTrigger` (được tự động thêm khi import).
- **Cấu hình bắt buộc**:
  - **Credentials**: Chọn `emeliaApi` (đã tạo trước).
  - **Trigger Type**: Chọn **"Reply"** (để bắt tất cả phản hồi từ khách hàng).
  - **Filter**: Nếu muốn chỉ bắt phản hồi từ một tin nhắn cụ thể, điền **Message ID** vào trường `filter`.

##### **Node 2: Mattermost**
- **Loại node**: `mattermost` (gửi thông báo).
- **Cấu hình bắt buộc**:
  - **Credentials**: Chọn `mattermostApi` (đã tạo trước).
  - **Channel ID**: Nhập **ID của channel Mattermost** (có thể tìm bằng cách mở channel → URL chứa `channel/` + số ID).
  - **Message**: Sử dụng **template** để định dạng thông báo:
    ```json
    "text": "🚨 **Phản hồi mới từ khách hàng** 🚨\n\n**Tin nhắn gốc**: {{ $node["emeliaTrigger"].json["message"] }}\n**Trả lời**: {{ $node["emeliaTrigger"].json["reply"] }}\n**Người gửi**: {{ $node["emeliaTrigger"].json["sender"] }}"
    ```
  - **Username**: Điền tên hiển thị (ví dụ: "Bot Emelia").
  - **Icon Emoji**: Chọn emoji (ví dụ: "🚀").

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  1. Nhấn **"Run Workflow"** trong n8n Editor.
  2. Gửi một tin nhắn trên Emelia và trả lời nó.
  3. Kiểm tra Mattermost để xác nhận thông báo đã xuất hiện.
- **Bật Active**:
  - Sau khi test thành công, nhấn **"Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NGOÀI THƯỜNG]
1. **Thêm thông báo vào Slack/Telegram**:
   - Sử dụng node `slack` hoặc `telegramBot` để gửi thông báo song song lên Mattermost.
   - **Cách làm**:
     ```bash
     1. Thêm node Slack/Telegram sau node Mattermost.
     2. Cấu hình credentials và message tương tự.
     ```

2. **Lưu log phản hồi**:
   - Thêm node `googleSheets` hoặc `notion` để ghi lại tất cả phản hồi khách hàng vào bảng tính/Notion.
   - **Cách làm**:
     ```bash
     1. Thêm node `googleSheets` sau node Mattermost.
     2. Chọn sheet và cấu hình header (cột) cho dữ liệu.
     ```

3. **Gửi email thông báo**:
   - Sử dụng node `email` (Gmail/SMTP) để gửi email cảnh báo cho team khi có phản hồi mới.
   - **Cách làm**:
     ```bash
     1. Thêm node `email` sau node Mattermost.
     2. Cấu hình SMTP hoặc Gmail OAuth.
     3. Sử dụng template email:
        ```json
        "subject": "🚨 Có phản hồi mới từ khách hàng trên Emelia"
        "text": "Xin chào,\n\nCó phản hồi mới từ khách hàng:\n{{ $node["emeliaTrigger"].json["reply"] }}\n\nTrả lời ngay tại: [Link Emelia]({{ $node["emeliaTrigger"].json["link"] }})"
        ```
     ```

4. **Phân loại phản hồi tự động**:
   - Sử dụng node `function` để phân loại phản hồi (ví dụ: "Cần hỗ trợ", "Hỏi giá", "Khiếu nại").
   - **Cách làm**:
     ```bash
     1. Thêm node `function` giữa `emeliaTrigger` và `mattermost`.
     2. Sử dụng code JavaScript để phân loại:
        ```javascript
        return {
          data: {
            reply: $input.all().reply,
            category: $input.all().reply.toLowerCase().includes("giá") ? "Hỏi giá" : "Khác"
          }
        };
        ```
     3. Sử dụng `$node["function"].json["category"]` trong template Mattermost.
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho team Sales/Marketing bằng cách tự động hóa quá trình phản hồi khách hàng. Khi khách hàng trả lời trên Emelia, hệ thống sẽ **ngay lập tức** gửi thông báo lên Mattermost, giúp team phản hồi **ngay tức khắc** mà không cần can thiệp thủ công.

**Hành động ngay hôm nay**:
1. **Self-host n8n** trên VPS để workflow chạy 24/7.
2. **Import workflow** và cấu hình credentials.
3. **Test run** và bật **Active** để bắt đầu tự động hóa!

👉 [Tải workflow JSON](https://n8n.io/workflows/1039) và bắt đầu **tự động hóa Sales Marketing** của mình ngay bây giờ! 🚀