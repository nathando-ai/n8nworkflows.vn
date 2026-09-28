---
title: "🚀 Tự Động Hóa Email Outreach Cá Nhân Hóa Từ Email Khách Hàng (N8n + AI Gemini)"
description: "Workflow tự động hóa hoàn toàn không cần code để phân tích lịch sử email khách hàng, xây dựng persona AI, và tạo ra email outreach cá nhân hóa chuẩn CRM, tiết kiệm 80% thời gian so với cách làm thủ công."
slug: "tieu-dong-hoa-email-outreach-ca-nhan-hoa-ai-gemini"
tags: [n8n, automation, crm, ai-summarization, sales-outreach]
keywords: [n8n workflow email outreach, tự động hóa email cá nhân hóa, AI Gemini cho CRM, tự động hóa HubSpot Gmail, template email sales AI]
---

# 🚀 **Tự Động Hóa Email Outreach Cá Nhân Hóa Từ Email Khách Hàng (N8n + AI Gemini)**

### **Giải pháp cho các sếp bán hàng:**
Bạn có bao giờ phải mất **3-5 tiếng** để viết email outreach cho 50 khách hàng tiềm năng, chỉ để cuối cùng phải chỉnh sửa lại vì không phù hợp với từng cá nhân? Hay phải tra cứu lịch sử email của khách hàng để hiểu rõ nhu cầu, nhưng lại không có thời gian để phân tích chi tiết?

**Workflow này sẽ:**
- **Tự động** lấy toàn bộ lịch sử email của khách hàng từ Gmail.
- **Xây dựng persona AI** dựa trên hành vi, mục tiêu và điểm đau từ email.
- **Tạo email outreach cá nhân hóa** phù hợp với từng khách hàng, với **tone, nội dung và CTA** được tối ưu.
- **Lưu email draft** trong Gmail để bạn chỉ cần review và gửi – **không cần viết từ đầu!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** so với cách viết email thủ công.
✅ **Tăng tỷ lệ mở email** lên **30-50%** nhờ nội dung cá nhân hóa.
✅ **Tối ưu tone & CTA** phù hợp với từng khách hàng (formal/casual).
✅ **Hoạt động tự động** 24/7, không phụ thuộc vào giờ làm việc.
✅ **Dữ liệu AI chính xác** từ lịch sử email thực tế, không phải đoán mò.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để lấy lịch sử email và lưu draft).
2. **Tài khoản HubSpot** (để lấy danh sách khách hàng tiềm năng).
3. **API Key Google Gemini** (miễn phí, đăng ký tại [Google AI Studio](https://aistudio.google/)).
4. **Danh sách khách hàng mục tiêu** (cần lọc sẵn trong HubSpot để workflow hiệu quả).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần code**: Workflow hoàn toàn **no-code**, chỉ cần copy/paste JSON.
- **Test trước khi chạy thực tế**: Sử dụng **Manual Trigger** để kiểm tra với một khách hàng mẫu.
- **Cập nhật API Key**: Nếu API Key Google Gemini hết hạn, workflow sẽ ngừng hoạt động.
:::

---

## 🚀 **Cách Import & Lưu ý khi "Lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/8968](https://n8n.io/workflows/8968) (chọn **Export as JSON**).
2. Mở **n8n Editor** (trang chủ của n8n) → **Import Workflow** → Chọn file JSON vừa tải.
3. **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/8968) (chọn **Export as JSON**) và paste vào **Import Workflow**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → **Create New Workflow** → Chọn **Import from JSON**.
2. Dán toàn bộ mã JSON từ [n8n.io/workflows/8968](https://n8n.io/workflows/8968) (chọn **Export as JSON**).
3. Click **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Node "Variables" (Biến môi trường)**
- **Tên biến**: `OUTREACH_TOPIC` (ví dụ: *"Tăng cường an ninh cho doanh nghiệp"*).
- **Giá trị**: Nội dung chủ đề email outreach bạn muốn AI sử dụng để viết email.

#### **B. Cấu hình Node "Google Gemini Chat Model"**
1. **Credentials**:
   - Chọn **googlePalmApi** (nếu đã cấu hình trước).
   - Nếu chưa có, đi đến **Credentials** → **Add Credentials** → Chọn **Google Palm API**.
   - Nhập **API Key** từ [Google AI Studio](https://aistudio.google/).
2. **Prompt Template**:
   - AI sẽ sử dụng **Information Extractor** để phân tích email. Các sếp **không cần chỉnh sửa** prompt mặc định (n8n đã tối ưu sẵn).

#### **C. Cấu hình Node "Get Contacts" (HubSpot)**
1. **Credentials**:
   - Chọn **hubspotOAuth2Api** (nếu đã cấu hình OAuth2 từ HubSpot).
   - Nếu chưa có, đi đến **Credentials** → **Add Credentials** → Chọn **HubSpot OAuth2 API**.
   - Nhập **Client ID**, **Client Secret**, và **Redirect URI** từ [HubSpot Developer](https://developers.hubspot.com/).
2. **Key Parameters**:
   - **Operation**: `search` (đã mặc định).
   - **Filter**: Lọc khách hàng mục tiêu (ví dụ: `lifecycleStage=lead` hoặc `hs_object_count=1`).

#### **D. Cấu hình Node "Get All Customer's Correspondence" (Gmail)**
1. **Credentials**:
   - Chọn **Gmail** (nếu đã cấu hình OAuth2 từ Gmail).
   - Nếu chưa có, đi đến **Credentials** → **Add Credentials** → Chọn **Gmail OAuth2**.
   - Nhập **Client ID** và **Client Secret** từ [Google Cloud Console](https://console.cloud.google.com/).
2. **Key Parameters**:
   - **Operation**: `getAll` (đã mặc định).
   - **Filter**: Lọc email liên quan đến khách hàng (ví dụ: `from:khachhang@example.com`).

#### **E. Cấu hình Node "Create Draft Email For Review" (Gmail)**
1. **Credentials**:
   - Chọn **Gmail** (cùng tài khoản đã cấu hình ở trên).
2. **Key Parameters**:
   - **Resource**: `draft` (đã mặc định).
   - **To**: Địa chỉ email của khách hàng (được lấy từ HubSpot).
   - **Subject**: AI sẽ tự động tạo dựa trên `OUTREACH_TOPIC`.

---
### **3. Kích hoạt ⚡️**
1. **Test Run với 1 khách hàng mẫu**:
   - Click vào **Manual Trigger** → Chọn **Execute Workflow**.
   - Chọn **1 khách hàng** từ danh sách HubSpot → Click **Execute**.
   - Kiểm tra **draft email** trong Gmail (nếu thành công, sẽ có email draft mới).
2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.
   - Workflow sẽ tự động chạy **hàng ngày** (hoặc theo lịch bạn thiết lập).

---
## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tối ưu danh sách khách hàng trong HubSpot**
- **Lọc nhỏ**: Chỉ lấy **50-100 khách hàng** đầu tiên để test, sau đó mở rộng.
- **Sắp xếp theo giá trị**: Ưu tiên khách hàng có **lịch sử tương tác cao** (ví dụ: đã mở email trước đó).

### **2. Cải thiện chất lượng email AI**
- **Cập nhật `OUTREACH_TOPIC`**: Nếu chủ đề outreach thay đổi, cập nhật biến này.
- **Sửa đổi prompt AI** (nếu cần):
  - Trong node **Information Extractor**, bạn có thể chỉnh sửa **prompt** để AI tập trung vào **điểm đau cụ thể** (ví dụ: *"Tìm kiếm thông tin về ngân sách của khách hàng"*).

### **3. Kết hợp với Slack/Telegram để báo cáo**
- Thêm **node Slack/Telegram Webhook** sau node **Create Draft Email** để nhận thông báo khi email draft được tạo.
- Ví dụ:
  ```json
  {
    "node": "slack",
    "type": "webhook",
    "credentials": ["slackWebhook"],
    "operation": "sendMessage",
    "text": "📧 Email draft đã tạo cho {{$json["email"]["to"]}}: {{$json["email"]["subject"]}}"
  }
  ```

### **4. Lưu log hoạt động**
- Thêm **node StickyNote** để ghi lại **lịch sử chạy workflow**, ví dụ:
  ```json
  {
    "node": "stickyNote",
    "type": "stickyNote",
    "text": "Workflow chạy thành công cho khách hàng: {{$json["contact"]["email"]}}"
  }
  ```

### **5. Chạy định kỳ với Cron**
- Sử dụng **node Cron** để chạy workflow **hàng ngày** vào giờ rảnh (ví dụ: 8h sáng).
- Cấu hình:
  ```json
  {
    "node": "cron",
    "type": "cron",
    "schedule": "0 8 * * *" // Chạy lúc 8h sáng hàng ngày
  }
  ```

---
## 📌 **Kết luận**
Workflow **Personalized Outreach from Customer Emails** là **giải pháp hoàn hảo** để các sếp bán hàng:
✔ **Tiết kiệm thời gian** viết email thủ công.
✔ **Tăng tỷ lệ chuyển đổi** nhờ nội dung cá nhân hóa.
✔ **Hoạt động tự động** 24/7, không phụ thuộc vào giờ làm việc.

**Bắt đầu ngay hôm nay!**
1. **Import workflow** từ [n8n.io/workflows/8968](https://n8n.io/workflows/8968).
2. **Cấu hình Gmail, HubSpot và API Key**.
3. **Test với 1 khách hàng mẫu** → **Bật Active** và để workflow làm việc!

**🚀 Cần hỗ trợ kỹ thuật?** Đăng ký VPS n8n tại [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ support để được cài đặt workflow miễn phí!