---
title: "🚀 Tự Động Hóa Xác Minh & Phân Loại Lead B2B Siêu Tốc Với GPT-4o-mini, Hunter.io & Slack (Không Cần Code)"
description: "Workflow tự động hóa nhận, phân tích, đánh giá và phân loại lead B2B từ mọi nguồn (webform, CRM, email) thành hot/warm/cold với AI GPT-4o-mini, enrich dữ liệu công ty bằng Hunter.io, và tự động gửi thông báo Slack/email. Giúp sales team tiết kiệm 10+ giờ/ngày và tăng tỷ lệ chuyển đổi lead thành khách hàng."
slug: "tieu-dong-hoa-xac-minh-phan-loai-lead-b2b-gpt-4o-mini"
tags: [n8n, automation, lead-generation, ai-summarization, hunter-io, gpt-4o-mini, slack, gmail, google-sheets]
keywords: [tự động hóa lead B2B, workflow n8n lead qualification, AI phân loại lead, Hunter.io enrich data, GPT-4o-mini tự động hóa sales, tự động gửi email lead hot, tự động hóa CRM]
---

# 🚀 **Tự Động Hóa Xác Minh & Phân Loại Lead B2B Siêu Tốc Với AI GPT-4o-mini**

Hàng ngày, các sếp sales phải mất **giờ đồng hồ** để:
- **Lọc rác** trong hàng trăm lead từ webform, CRM, hoặc email.
- **Nhập liệu thủ công** vào Google Sheets, HubSpot, hoặc Pipedrive.
- **Đánh giá lead** bằng tiêu chí BANT (Budget, Authority, Need, Timeline) một cách chủ quan.
- **Gửi email/Slack** cho lead hot mà không biết liệu họ có thực sự là khách hàng tiềm năng hay không.

**Kết quả?** Lead chất lượng bị bỏ qua, lead không phù hợp tiêu tốn thời gian, và tỷ lệ chuyển đổi **giảm 30-50%** so với tiềm năng thực sự.

---
## 🎯 **Kết quả các sếp nhận được khi áp dụng workflow này**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** cho team sales: Lead được tự động nhận, phân loại và hành động ngay lập tức.
- **Tăng tỷ lệ chuyển đổi lead** lên **40-60%** nhờ AI đánh giá chính xác theo tiêu chí BANT.
- **Cá nhân hóa tương tác** với lead hot bằng email tự động + link đặt lịch hẹn (Cal.com).
- **Hỗ trợ quyết định** với dữ liệu công ty enrich từ Hunter.io (tên công ty, ngành nghề, quy mô, vị trí).
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Lưu trữ lead** tự động vào Google Sheets (hoặc CRM khác) với tất cả thông tin enrich.
:::

---
## 🔧 **Yêu cầu cần thiết để chạy workflow**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - [OpenRouter](https://openrouter.ai) (để sử dụng GPT-4o-mini hoặc các mô hình AI khác).
   - [Hunter.io](https://hunter.io) (tùy chọn, để enrich dữ liệu công ty).
   - [Google Sheets](https://sheets.google.com) (để lưu log lead).
   - [Gmail](https://mail.google.com) (để gửi email tự động).
   - [Slack](https://slack.com) (để gửi thông báo lead hot).

2. **Thông tin cấu hình**:
   - **Spreadsheet ID** của Google Sheets (để lưu lead).
   - **URL đặt lịch hẹn** (ví dụ: `https://cal.com/ten-cua-ban`).
   - **Channel Slack** `#sales-alerts` (để nhận thông báo lead hot).

3. **Hệ thống n8n**:
   - **Self-hosted** (khuyến nghị) để workflow hoạt động 24/7.
   - **N8n Cloud** (tùy chọn, nhưng có giới hạn tài nguyên).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/15557](https://n8n.io/workflows/15557).
- **Copy JSON** và dán vào **Import Workflow** trong n8n Editor.

:::note[LƯU Ý]
- **Không thay đổi cấu trúc** của workflow, chỉ cần **điền thông tin cấu hình** như hướng dẫn dưới đây.
- **Không xóa node** nào, chỉ cần **cấu hình lại credentials** và tham số.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔑 Cấu hình OpenRouter (GPT-4o-mini)**
Workflow sử dụng **OpenRouter** để:
- **Trích xuất trường lead** từ payload nguyên thủy (Stage 2b).
- **Đánh giá lead** theo tiêu chí BANT (Stage 4).

**Cách cấu hình**:
1. **Tạo tài khoản OpenRouter** tại [openrouter.ai](https://openrouter.ai).
2. **Tạo API Key** trong dashboard.
3. **Tạo credential Header Auth** trong n8n:
   - **Credential Type**: `Header Auth`
   - **Name**: `Header Auth OpenRouter`
   - **Configuration**:
     | Field       | Value                          |
     |-------------|-------------------------------|
     | Name        | `Authorization`                |
     | Value       | `Bearer YOUR_OPENROUTER_API_KEY` |

4. **Gắn credential** này vào:
   - Node **`AI extract fields`** (Stage 2b).
   - Node **`AI score via OpenRouter`** (Stage 4).

:::tip[Mẹo]
- **Model mặc định**: `openai/gpt-4o-mini` (rẻ và nhanh).
- **Thay đổi model** nếu muốn:
  - `anthropic/claude-haiku-3-5` (tính toán tốt hơn).
  - `meta-llama/llama-3.1-8b-instruct` (miễn phí).
:::

---

#### **🔎 Cấu hình Hunter.io (Enrich Dữ liệu Công Ty)**
Workflow tự động **enrich dữ liệu công ty** từ email domain của lead (ví dụ: `lead@example.com` → `Công ty Example, Ngành nghề Tech, 50-100 nhân viên, Việt Nam`).

**Cách cấu hình**:
1. **Tạo tài khoản Hunter.io** tại [hunter.io](https://hunter.io).
2. **Tạo API Key** trong dashboard.
3. **Tạo credential Header Auth** trong n8n:
   - **Credential Type**: `Header Auth`
   - **Name**: `Header Auth Hunter`
   - **Configuration**:
     | Field       | Value                          |
     |-------------|-------------------------------|
     | Name        | `api_key`                      |
     | Value       | `YOUR_HUNTER_API_KEY`          |

4. **Gắn credential** này vào node **`Hunter.io domain search`**.

:::warning[Lưu ý về giá cả]
- **Free plan**: 25 request/tháng (đủ cho nhỏ lẻ).
- **Paid plan**: Từ **$34/tháng** (khuyến nghị nếu có nhiều lead).
:::

---

#### **📧 Cấu hình Gmail (Gửi Email Tự Động)**
Workflow sẽ **gửi email tự động** cho:
- **Lead hot**: Email cá nhân hóa + link đặt lịch hẹn.
- **Lead warm**: Email nurture mềm (không bán hàng).

**Cách cấu hình**:
1. **Kết nối Gmail OAuth2** trong n8n:
   - Đi đến **Credentials** → **Add** → **Gmail OAuth2**.
   - Theo hướng dẫn để **cho phép n8n truy cập Gmail**.
2. **Thay đổi URL đặt lịch hẹn**:
   - Trong node **`Book a call URL`**, thay thế:
     ```json
     "YOUR_BOOK_A_CALL_URL"
     ```
     bằng URL thực tế của bạn (ví dụ: `https://cal.com/ten-cua-ban`).
   - **Thay thế `YOUR_NAME_HERE`** trong email template bằng tên của bạn.

---

#### **🤖 Cấu hình Slack (Thông báo Lead Hot)**
Khi lead được đánh giá là **hot**, workflow sẽ gửi thông báo đến **channel Slack**.

**Cách cấu hình**:
1. **Kết nối Slack OAuth2** trong n8n:
   - Đi đến **Credentials** → **Add** → **Slack OAuth2**.
   - Chọn **Scopes**: `chat:write`, `channels:join`.
   - Theo hướng dẫn để **cho phép n8n truy cập Slack**.
2. **Đảm bảo channel `#sales-alerts` tồn tại** trong Slack.

---

#### **📊 Cấu hình Google Sheets (Lưu Log Lead)**
Workflow sẽ **lưu tất cả lead** vào Google Sheets với cấu trúc:
- **Hot Lead**: `Status = Hot`, `Action = Slack + Email`.
- **Warm Lead**: `Status = Warm`, `Action = Email Nurture`.
- **Cold Lead**: `Status = Cold`, `Action = Tagging`.

**Cách cấu hình**:
1. **Tạo Google Sheet mới** và chia sẻ cho n8n.
2. **Thay thế `YOUR_SPREADSHEET_ID`** trong node **`Google Sheets — log lead`**:
   - Mở Google Sheets → URL sẽ có dạng:
     ```
     https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit
     ```
   - **Copy `SPREADSHEET_ID`** và điền vào node.
3. **Đảm bảo sheet có các cột**:
   - `Email`, `Company`, `Name`, `Status`, `Score`, `Action`, `Notes`.

---

### **3. Kích hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi **payload JSON** đến **webhook** (`/lead-qualifier`).
   - Kiểm tra các node:
     - **AI extract fields** → **AI score** → **Route by lead tier**.
   - Xem kết quả trên **Google Sheets** và **Slack**.
2. **Bật Active** workflow khi đã kiểm tra thành công.

---
## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Kết hợp với CRM khác**
Ngoài Google Sheets, các sếp có thể **thay thế** bằng:
- **HubSpot**: Sử dụng node **HubSpot API**.
- **Pipedrive**: Sử dụng node **Pipedrive API**.
- **Airtable**: Sử dụng node **Airtable API**.

**Cách thay đổi**:
- Xóa node **Google Sheets** cũ.
- Thêm node **HTTP Request** hoặc **CRM tương ứng**.
- Cấu hình **URL API** và **credentials OAuth2**.

---

### **2. Lưu log hoạt động**
Để **theo dõi hoạt động** của workflow, các sếp có thể:
- **Thêm node `Set`** sau **Google Sheets** để lưu **timestamp** và **status**.
- **Gửi báo cáo định kỳ** (hàng tuần) qua **Slack/Email** bằng node **Schedule**.

**Ví dụ**:
```json
{
  "name": "Log Activity",
  "type": "set",
  "properties": [
    {
      "name": "timestamp",
      "value": "{{ $datetime.now('YYYY-MM-DD HH:mm:ss') }}"
    },
    "status": "{{ $node["Route by lead tier"].json["output"]["data"]["status"] }}"
  ]
}
```

---

### **3. Tự động gửi báo cáo hàng tuần**
Sử dụng **node `Schedule`** để gửi **tổng hợp lead** qua **Email/Slack** mỗi tuần.

**Cách cấu hình**:
1. Thêm node **Schedule** vào workflow.
2. Cấu hình:
   - **Frequency**: `Weekly` (Thứ 2 hàng tuần).
   - **Time**: `09:00 AM`.
3. Kết nối với **Gmail** hoặc **Slack** để gửi báo cáo.

---

### **4. Cải thiện AI Prompt**
Nếu AI **đánh giá lead không chính xác**, các sếp có thể:
- **Tối ưu prompt** trong node **`Build AI prompt`**.
- **Thêm ví dụ** trong prompt để AI hiểu rõ tiêu chí BANT.
- **Test với lead mẫu** trước khi áp dụng toàn bộ.

**Ví dụ prompt cải tiến**:
```json
"Analyze the lead based on BANT criteria:
- Budget: Does the lead mention budget or ROI?
- Authority: Is the lead a decision-maker (e.g., CEO, CTO)?
- Need: Does the lead describe a pain point?
- Timeline: Does the lead mention a deadline or urgency?
Score from 0-100 and classify as Hot (70+), Warm (40-69), Cold (<40)."
```

---

## 📌 **Kết luận**
Workflow này **giải phóng team sales** khỏi công việc lặp lại, **tăng tỷ lệ chuyển đổi lead**, và **cải thiện hiệu quả hoạt động** nhờ AI và tự động hóa.

**Các sếp hãy:**
1. **Import workflow** và **cấu hình credentials**.
2. **Test với lead mẫu** trước khi áp dụng toàn bộ.
3. **Bật Active** và **theo dõi kết quả** trên Slack/Google Sheets.

**Kết quả?** **Lead hot được xử lý ngay lập tức**, **lead warm được nurture tự động**, và **lead cold được phân loại** để follow-up sau này.

---
:::success[🚀 **Bắt đầu ngay!**]
- **Đăng ký VPS TinoHost** để self-host n8n 24/7:
  👉 [🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%](https://tino.vn/vps-n8n?affid=388)
- **Xem video hướng dẫn** import workflow:
  [📺 Link YouTube](https://youtu.be/your-video-link)
:::

**Chia sẻ feedback** nếu có vấn đề! 🚀