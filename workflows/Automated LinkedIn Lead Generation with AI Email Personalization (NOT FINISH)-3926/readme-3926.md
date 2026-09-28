---
title: "🚀 Tự Động Hóa Sinh Lên Lead LinkedIn Với Email Cá Nhân Hóa AI – Giảm 90% Thời Gian Sales"
description: "Workflow tự động hóa tìm kiếm, lọc và gửi email cá nhân hóa cho các lead LinkedIn chất lượng cao, tăng tỷ lệ chuyển đổi lên 30%+ chỉ với AI và API. Giúp các sếp tiết kiệm 20+ giờ/tháng cho công việc sales."
slug: "tieu-dong-hoa-lead-linkedin-ai-email"
tags: [n8n, automation, sales, ai-marketing, linkedin-lead-generation]
keywords: [n8n workflow lead linkedin, tự động hóa sales, email cá nhân hóa ai, tìm kiếm lead chất lượng, giảm thời gian sales]
---

# 🚀 **Tự Động Hóa Sinh Lên Lead LinkedIn Với Email Cá Nhân Hóa AI**

### **Giải pháp cho các sếp muốn:**
- **Tìm kiếm tự động** các lead LinkedIn phù hợp với mục tiêu doanh nghiệp (không cần tra cứu thủ công).
- **Lọc ra 3 lead top** có khả năng chuyển đổi cao nhất dựa trên AI.
- **Gửi email cá nhân hóa** với tỷ lệ mở cao (30%+) bằng cách tích hợp thông tin LinkedIn của lead.
- **Tiết kiệm 20+ giờ/tháng** cho đội ngũ sales, tập trung vào giao dịch chứ không phải tìm kiếm lead.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian:** Tự động hóa toàn bộ quy trình từ tìm kiếm lead đến gửi email cá nhân hóa.
✅ **Tỷ lệ chuyển đổi cao:** AI lọc ra 3 lead top/doanh nghiệp, tăng cơ hội thành công lên **30%**.
✅ **Email cá nhân hóa thực sự:** Không chỉ là "Xin chào [Tên]", mà tích hợp thông tin LinkedIn của lead (bài viết gần đây, ngành nghề, sở thích).
✅ **Hoạt động 24/7:** Workflow chạy tự động, không phụ thuộc vào giờ làm việc của nhân viên.
✅ **Giảm chi phí API:** Dự kiến chỉ **~$2 cho 40 công ty** (thay vì 100 công ty ban đầu do lọc sàng lọc).
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản API:**
   - **GhostGenius API** (tìm kiếm nhân viên LinkedIn) – [Đăng ký miễn phí](https://ghostgenius.com/).
   - **MillionVerifier API** (kiểm tra email hợp lệ) – [Đăng ký](https://millionverifier.com/).
   - **OpenAI API** (sử dụng GPT-4 cho cá nhân hóa) – [Đăng ký](https://platform.openai.com/).
   - **Google Sheets OAuth2** (lưu trữ lead và kết quả) – [Cài đặt OAuth](https://developers.google.com/sheets/api/quickstart/python).

2. **Google Sheet CRM:**
   - Một bảng Google Sheets với các cột: `Company Name`, `Website`, `Score`, `Status`, `Target Roles`.
   - **Workflow phụ** để enrich CRM đã được cung cấp [tại đây](https://n8n.io/workflows/3926) (cần import trước).

3. **Tham số cấu hình:**
   - **Target Roles:** Danh sách các vị trí mục tiêu (VD: "CEO", "CTO", "Head of Sales").
   - **Email Template:** Các biến như `{{firstName}}`, `{{company}}`, `{{personalization}}` sẽ được thay thế tự động.
   - **API Keys:** Điền vào n8n dưới dạng **Credentials** (OpenAI API Key, GhostGenius Token, MillionVerifier API Key).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/3926](https://n8n.io/workflows/3926) (chọn "Download JSON").
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Self-hosted** (nếu tự cài n8n) hoặc **n8n.cloud** (nếu dùng dịch vụ cloud).

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor → Nhấn **Import** → Chọn **Paste JSON**.
2. Copy toàn bộ mã JSON từ [n8n.io/workflows/3926](https://n8n.io/workflows/3926) (chọn "Copy JSON") và dán vào.
3. Chọn **Self-hosted** và nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** và có **29 node**, nên các sếp cần chú ý các bước sau:

#### **A. Cấu hình Credentials (API Keys)**
- **OpenAI API:**
  - Tạo **Credentials** mới trong n8n: `n8n-nodes-base.openAi` → Chọn `openAiApi`.
  - Điền `API Key` từ OpenAI vào `apiKey` (tìm trong tài khoản OpenAI → Settings → API Keys).
  - Chọn model: `gpt-4` (để cá nhân hóa tốt nhất).

- **GhostGenius API:**
  - Tạo `httpHeaderAuth` mới trong n8n.
  - Điền `Authorization: Bearer <YOUR_GHOSTGENIUS_TOKEN>` (tìm trong tài khoản GhostGenius → API Keys).

- **MillionVerifier API:**
  - Tạo `httpHeaderAuth` mới.
  - Điền `Authorization: Bearer <YOUR_MILLIONVERIFIER_API_KEY>`.

- **Google Sheets OAuth2:**
  - Tạo `googleSheetsOAuth2Api` mới.
  - Theo hướng dẫn [Google Sheets API](https://developers.google.com/sheets/api/quickstart/python) để tạo OAuth2 Client ID.
  - Chọn **Google Sheet** chứa dữ liệu CRM (cần có cột: `Company Name`, `Website`, `Score`, `Status`).

#### **B. Cấu hình Google Sheet CRM**
- Workflow **lọc ra các công ty có Score ≥ 7** và **Status = "Qualified"**.
- Các cột cần thiết:
  | Cột          | Mô tả                          |
  |---------------|--------------------------------|
  | `Company Name`| Tên công ty (VD: "TechCorp")   |
  | `Website`     | URL website (VD: "techcorp.com")|
  | `Score`       | Điểm đánh giá (cần ≥ 7)        |
  | `Status`      | "Qualified" (đã lọc sàng lọc)  |
  | `Target Roles`| Danh sách vị trí mục tiêu (VD: "CEO, CTO") |

#### **C. Cấu hình Target Roles**
- Trong node **"Set Variables"** (node `Set`), các sếp cần điền:
  ```json
  {
    "targetRoles": ["CEO", "CTO", "Head of Sales", "Product Manager"]
  }
  ```
  (Thay thế bằng danh sách vị trí phù hợp với ngành nghề của doanh nghiệp).

#### **D. Cấu hình Email Template**
- Workflow sẽ tự động tạo email cá nhân hóa bằng AI.
- Các biến mặc định:
  - `{{firstName}}`
  - `{{company}}`
  - `{{personalization}}` (tích hợp từ bài viết LinkedIn gần đây của lead).
- **Không cần chỉnh sửa template** (AI sẽ tự động tạo nội dung phù hợp).

#### **E. Cấu hình Batch Processing**
- Node **"Loop Over Items"** (`splitInBatches`) cần thiết để xử lý **1 công ty/lần**.
- **Không cần chỉnh sửa** mặc định (n8n sẽ tự động chia batch).

---
### **3. Kích hoạt ⚡️**
1. **Test Run với 1 công ty mẫu:**
   - Nhấn **Run Workflow** và nhập **1 công ty** vào `Company Name` (VD: "TechCorp").
   - Kiểm tra các node quan trọng:
     - **"Find Employees"** → Đã tìm được ≥3 nhân viên?
     - **"Verify Emails"** → Có email hợp lệ không?
     - **"Generate Emails"** → Email có cá nhân hóa không?

2. **Bật Active Workflow:**
   - Sau khi test thành công, chuyển **Status** từ `Inactive` → `Active`.
   - **Lưu ý:** Workflow sẽ chạy **tự động** khi có dữ liệu mới trong Google Sheet.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **"Slack Webhook"** (`n8n-nodes-base.slack`) để thông báo khi có lead mới.
   - **Cách làm:**
     ```json
     {
       "operation": "post",
       "url": "https://hooks.slack.com/services/...",
       "body": {
         "text": "🚀 Lead mới từ {{company}}: {{firstName}} ({{email}}) - Score: {{score}}"
       }
     }
     ```

2. **Lưu log hoạt động:**
   - Thêm node **"Google Sheets"** (`n8n-nodes-base.googleSheets`) để ghi lại lịch sử hoạt động (VD: "2024-05-20: Xử lý TechCorp").
   - **Cột cần thêm:** `Action`, `Timestamp`, `Status`.

3. **Gửi báo cáo định kỳ:**
   - Sử dụng **n8n Scheduler** để chạy workflow hàng tuần và gửi báo cáo qua **Email** (`n8n-nodes-base.email`).
   - **Dữ liệu báo cáo:**
     - Số lead tìm được.
     - Tỷ lệ email hợp lệ.
     - Tỷ lệ mở email (nếu tích hợp với Mailchimp/HubSpot).

4. **Tối ưu chi phí API:**
   - **GhostGenius:** Sử dụng **private endpoint** (rẻ hơn) nếu có nhu cầu lớn.
   - **MillionVerifier:** Chỉ kiểm tra email cho **3 lead top** (không cần kiểm tra tất cả).
   - **OpenAI:** Sử dụng **gpt-3.5-turbo** (rẻ hơn gpt-4) cho các bước không cần cao cấp.

5. **Tích hợp với CRM:**
   - Nếu dùng **HubSpot** hoặc **Salesforce**, thay thế node Google Sheets bằng **HubSpot API** (`n8n-nodes-base.hubspot`).
   - **Cách làm:**
     - Tạo `HubSpot OAuth2` credentials.
     - Thay node `googleSheets` bằng `hubspot.createContact`.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng đội ngũ sales** khỏi công việc mòn mỏi là tìm kiếm lead thủ công, thay vào đó **tự động hóa toàn bộ quy trình từ tìm kiếm đến gửi email cá nhân hóa**. Kết quả:
✔ **Tiết kiệm 20+ giờ/tháng**.
✔ **Tăng tỷ lệ chuyển đổi lên 30%** nhờ AI lọc lead và cá nhân hóa email.
✔ **Hoạt động 24/7** mà không cần nhân viên.

:::tip[LÀM GÌ TIẾP THEO?]
1. **Import workflow** và cấu hình API theo hướng dẫn trên.
2. **Test với 1-2 công ty** trước khi bật chế độ tự động.
3. **Tích hợp Slack/Email** để nhận thông báo lead mới.
4. **Tối ưu chi phí** bằng cách lọc sàng lọc lead trước khi xử lý.

**Bắt đầu tự động hóa sales ngay hôm nay!** 🚀
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::