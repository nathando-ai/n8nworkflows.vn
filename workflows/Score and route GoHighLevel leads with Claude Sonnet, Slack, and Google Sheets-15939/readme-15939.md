---
title: "🚀 Tự Động Hóa Xếp Loại & Phân Loại Lead GoHighLevel Với Claude AI, Slack & Google Sheets - Không Cần Code!"
description: "Workflow tự động hóa 100% miễn phí xếp loại lead từ GoHighLevel bằng AI Claude Sonnet, phân loại thành Hot/Warm/Cold, gửi thông báo Slack và ghi log vào Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/ngày xử lý lead thủ công!"
slug: "tieu-dong-hoa-xep-loai-lead-ghl-ai-claude-slack-google-sheets"
tags: [n8n, automation, lead-generation, ai-claude, gohighlevel, slack, google-sheets]
keywords: [tự động hóa lead GoHighLevel, xếp loại lead bằng AI, Claude Sonnet n8n, phân loại lead Hot/Warm/Cold, tự động hóa Slack, ghi log lead Google Sheets]
---

# 🚀 **Tự Động Hóa Xếp Loại Lead GoHighLevel Với AI Claude Sonnet, Slack & Google Sheets**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp:**
Hàng ngày, các sếp phải mất **10+ giờ** để:
✅ **Xếp loại lead thủ công** theo tiêu chí ICP (Ideal Customer Profile) phức tạp.
✅ **Phân loại lead** thành Hot/Warm/Cold dựa trên nhiều yếu tố (ngành nghề, kích thước công ty, ngân sách, từ khóa).
✅ **Gửi thông báo Slack** cho team khi có lead ưu tiên cao.
✅ **Cập nhật thông tin lead** vào GoHighLevel và Google Sheets để theo dõi.

**Workflow này tự động hóa toàn bộ quy trình đó chỉ trong 10 phút setup!** Không cần viết code, chỉ cần cài n8n và kết nối API.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của n8n.cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** xử lý lead thủ công.
- **Xếp loại lead chính xác** với AI Claude Sonnet (độ chính xác cao hơn con người).
- **Phân loại tự động** lead thành **Hot (7-10)**, **Warm (4-6)**, **Cold (1-3)**.
- **Gửi thông báo Slack** ngay khi có lead ưu tiên cao.
- **Cập nhật GoHighLevel** tự động (tag + chuyển pipeline).
- **Ghi log toàn bộ lead** vào Google Sheets với thời gian, lý do, và hành động tiếp theo.
- **Hoạt động liên tục 24/7** mà không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản GoHighLevel** (đã có API Key và Location ID).
✔ **Tài khoản Claude AI** (API Key từ [console.anthropic.com](https://console.anthropic.com/)).
✔ **Tài khoản Slack** (nếu muốn nhận thông báo).
✔ **Google Sheets** (đã tạo bảng `GHL Lead Log` với các cột: `Timestamp`, `Name`, `Email`, `Phone`, `Source`, `Score`, `Tier`, `Reasoning`, `Next Action`).
✔ **VPS hoặc n8n.cloud** (để chạy workflow liên tục).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15939) hoặc copy JSON từ canvas.
- Mở **n8n Editor** → Nhấn `Import` → Dán JSON → Chọn `Import`.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Webhook GoHighLevel**
- Mở node **`Receive GHL Contact`** → Copy **URL Webhook** (vd: `https://your-n8n-url/webhook/ghl-new-contact`).
- Tại **GoHighLevel**:
  1. Đi đến **Settings → Integrations → Webhooks**.
  2. Tạo **mới 1 Webhook** với:
     - **Trigger**: `Contact Created`.
     - **URL**: Dán URL từ n8n.
     - **Payload**: `JSON`.
  3. **Bật Webhook** và **Activate workflow** để URL hoạt động.

##### **B. Cấu Hình ICP & API Key GoHighLevel**
- Mở node **`Configure ICP and Settings`** (Code Node).
- Điền các thông tin sau:
  ```json
  {
    "ghlApiKey": "API_KEY_CỦA_BẠN_TẠI_GHL",
    "locationId": "LOCATION_ID_CỦA_BẠN_TẠI_GHL",
    "icp": {
      "niche": "Ngành nghề mục tiêu (vd: SaaS, E-commerce)",
      "companySize": ["10-50", "50-200"],
      "goodKeywords": ["ngân sách cao", "mua ngay", "tăng trưởng nhanh"],
      "badKeywords": ["ngân sách thấp", "chỉ xem xét", "không phù hợp"]
    }
  }
  ```
- **Lưu ý**: Thay thế `API_KEY` và `LOCATION_ID` bằng thông tin từ **Settings → API Keys** và **Settings → Locations** tại GoHighLevel.

##### **C. Cấu Hình Claude AI (Claude Sonnet)**
- Mở node **`Claude Sonnet`** → Click vào **`lmChatAnthropic`**.
- Thêm **mới 1 credential** với:
  - **API Key**: Copy từ [console.anthropic.com](https://console.anthropic.com/).
  - **Model**: Chọn `claude-sonnet-4-5` (hoặc `claude-haiku` nếu muốn tiết kiệm chi phí).
- **Prompt mặc định** đã tối ưu, nhưng các sếp có thể chỉnh sửa để phù hợp với ngành nghề:
  ```plaintext
  Analyze the contact details and assign a score (1-10), tier (Hot/Warm/Cold), reasoning, and next action.
  ```

##### **D. Cấu Hình Slack (Nếu Sử Dụng)**
- Mở node **`Notify Team - Hot Lead`** → Click vào **`slack`**.
- Thêm **mới 1 credential** với:
  - **Token**: Copy từ **Apps → Slack → Add to Slack → Token**.
  - **Channel**: Chọn `#lead-alerts` (hoặc channel khác).
- **Lưu ý**: Nếu không muốn Slack, **right-click → Disable** node này.

##### **E. Cấu Hình Google Sheets**
- Mở node **`Log Lead to Sheets`** → Click vào **`googleSheets`**.
- Thêm **mới 1 credential** với:
  - **Email**: Tài khoản Google liên kết với Sheets.
  - **Spreadsheet**: Chọn `GHL Lead Log`.
  - **Sheet Name**: `Sheet1` (hoặc tên sheet đã tạo).
- **Lưu ý**: Đảm bảo **Google Sheets** đã có **các cột bắt buộc** như mô tả ở trên.

##### **F. Cấu Hình Phân Loại Lead (Switch Node)**
- Mở node **`Route by Tier`** → Chỉnh **threshold** theo tiêu chí của doanh nghiệp:
  - **Hot Lead**: Score **7-10**.
  - **Warm Lead**: Score **4-6**.
  - **Cold Lead**: Score **1-3**.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  1. Tạo **một lead mẫu** tại GoHighLevel.
  2. Kiểm tra **Slack** (nếu có) và **Google Sheets** để xác nhận workflow hoạt động.
- **Bật Active**:
  - Nhấn `Activate` trên canvas n8n.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tăng tính cá nhân hóa**:
   - Chỉnh sửa **prompt Claude** để thêm yêu cầu cụ thể như:
     ```plaintext
     "Nếu lead có từ khóa 'urgent' hoặc 'ngay hôm nay', tăng score +1."
     ```
2. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n + Google Apps Script** để tự động gửi **báo cáo hàng tuần** về lead mới.
3. **Kết hợp với CRM khác**:
   - Thay thế **Google Sheets** bằng **HubSpot** hoặc **Pipedrive** thông qua API.
4. **Optimize chi phí Claude**:
   - Sử dụng **Claude Haiku** thay vì Sonnet nếu lead volume cao.
5. **Log chi tiết hơn**:
   - Thêm **cột `Lead Source`** vào Google Sheets để phân tích nguồn lead hiệu quả nhất.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** và **sales** thay vì làm việc thủ công. Với **AI Claude Sonnet**, lead được xếp loại **chính xác và nhanh chóng**, trong khi **Slack và Google Sheets** giúp theo dõi và quản lý dễ dàng.

**Hành động ngay!**
1. **Setup workflow** theo hướng dẫn trên.
2. **Tạo lead mẫu** để test.
3. **Bật Active** và **quên đi việc xếp loại lead thủ công!**

👉 **Xem video demo** tại [n8n.io/workflows/15939](https://n8n.io/workflows/15939) để hiểu rõ hơn!

---
**Chia sẻ workflow này với team để cùng tự động hóa quy trình!** 🚀