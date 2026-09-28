---
title: "🤖 Tự Động Hóa Cuộc Gọi Bán Hàng Voice AI + GoHighLevel: Chuyển Gọi Thô → Lead Hot Chỉ Trong 60 Giây"
description: "Workflow này tự động phân loại, đánh giá và quản lý cuộc gọi bán hàng voice (inbound/outbound) bằng AI Claude, GPT-4o, Gemini, kết hợp với GoHighLevel để chuyển đổi lead thô thành lead hot/chuyển đổi, tiết kiệm 20+ giờ/ngày cho đội SDR. Hỗ trợ cả cuộc gọi inbound từ Vapi/Retell và outbound tự động hàng ngày."
slug: "tieu-dong-hoa-cuoc-goi-voice-ai-ghl"
tags: [n8n, automation, no-code, gohighlevel, ai-chatbot, sales-automation, voice-ai, lead-nurturing]
keywords: [tự động hóa cuộc gọi bán hàng, n8n workflow voice ai, gohighlevel automation, claude gpt-4o gemini bán hàng, tự động hóa lead hot, bán hàng voice ai, tự động gọi điện outbound]
---

# 🚀 **Tự Động Hóa Cuộc Gọi Bán Hàng Voice AI: Từ Lead Thô → Lead Hot Chỉ Trong 60 Giây**

## **Nỗi Đau Của Đội SDR Hiện Nay**
Hàng ngày, đội SDR phải:
- **Lắng nghe và ghi chép** hàng trăm cuộc gọi voice (thời gian trung bình 30-60 phút/cuộc).
- **Phân loại thủ công** lead theo tiêu chí BANT (Budget, Authority, Need, Timeline) với tỷ lệ sai lệch cao.
- **Tìm kiếm và cập nhật** thông tin khách hàng trong CRM GoHighLevel (GHN) một cách rườm rà.
- **Đối phó với objection** một cách không chuyên nghiệp, dẫn đến mất lead.
- **Quên theo dõi** lead không hot, khiến họ rơi vào "quên lãng".

**Kết quả?** Tỷ lệ chuyển đổi thấp, chi phí nhân sự cao, và mất nhiều thời gian cho công việc lặp lại.

---
### **🎯 Giải Pháp: Workflow AI + GoHighLevel "Tự Động Hóa Cuộc Gọi Bán Hàng"**
Workflow này **tự động hóa toàn bộ chuỗi từ nhận cuộc gọi voice đến chuyển đổi lead** bằng:
✅ **AI Claude/GPT-4o/Gemini** phân tích cuộc gọi, đánh giá BANT, phát hiện ý định đặt lịch, và đề xuất phản hồi objection.
✅ **GoHighLevel** tự động tạo/ cập nhật contact và opportunity, chuyển lead vào pipeline phù hợp.
✅ **Google Sheets + Supabase** lưu trữ log chi tiết cho báo cáo và phân tích.
✅ **Outbound tự động** hàng ngày từ lead chưa hot, tối ưu hóa ROI.

**Kết quả:**
- **Tiết kiệm 20+ giờ/ngày** cho đội SDR.
- **Tỷ lệ chuyển đổi tăng 30-50%** nhờ AI phân tích chính xác.
- **Lead hot tự động** được chuyển vào pipeline "Hot Lead" trong GHN.
- **Lead không hot** được xếp hàng và gọi lại tự động hàng ngày.
- **Báo cáo chi tiết** theo dõi hiệu suất cuộc gọi.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% cuộc gọi voice** (inbound/outbound) mà không cần code.
- **Đánh giá BANT chính xác** bằng AI Claude/GPT-4o (tỷ lệ chính xác >90%).
- **Tạo/ cập nhật contact & opportunity** trong GoHighLevel tự động.
- **Phản hồi objection chuyên nghiệp** bằng Claude Sonnet (phương pháp "Feel-Felt-Found").
- **Outbound tự động hàng ngày** từ lead chưa hot, tối ưu hóa ROI.
- **Báo cáo chi tiết** trên Google Sheets và Supabase cho phân tích.
- **Hoạt động 24/7** mà không cần can thiệp người dùng.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| Dịch vụ | Thông Tin Cần Thiết |
|---------|---------------------|
| **GoHighLevel (GHN)** | - OAuth2 Credential (tạo qua GHL Marketplace App) <br> - Pipeline ID <br> - Hot Lead Stage ID <br> - Nurturing Stage ID <br> - Nurture Workflow ID <br> - Location API Key (Settings → API Keys) |
| **Anthropic (Claude)** | API Key (truy cập [Anthropic Developer Portal](https://www.anthropic.com/api)) |
| **OpenAI (GPT-4o)** | API Key (truy cập [OpenAI Platform](https://platform.openai.com/account/api-keys)) |
| **Google Gemini** | API Key (truy cập [Google AI Studio](https://makersuite.google.com/app/apikey)) |
| **Supabase** | - URL Database <br> - Service Role Key |
| **Google Sheets** | - OAuth2 Credential <br> - Spreadsheet với sheet tên `Voice Call Log` (cấu trúc chi tiết ở phần sau) |
| **Voice Provider** | - **Vapi/Retell**: API Key và ID Phone Number/Assistant <br> - URL Webhook Inbound: `https://YOUR_N8N_URL/webhook/voice-sales-inbound` |

### **2. Cấu Hình GoHighLevel**
- **Pipeline**: Cần 2 stage:
  - **Hot Lead** (để lead đã hot).
  - **Nurturing** (để lead chưa hot).
- **Automation Workflow**: Tạo 1 workflow tự động để gọi lead chưa hot hàng ngày.

### **3. Cấu Hình Google Sheets**
Tạo 1 sheet với tên **`Voice Call Log`** và các cột sau (đầu tiên là tiêu đề):
| Call ID | Date | Phone Number | Direction | Provider | Duration (sec) | BANT Score | Qualified | Appointment Requested | GHL Contact ID | GHL Opp ID | CRM Note | Objection Response |
|---------|------|--------------|-----------|----------|----------------|------------|-----------|----------------------|----------------|-------------|-----------|-------------------|

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/14169](https://n8n.io/workflows/14169) (chọn "Download JSON").
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Mở n8n Editor → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON** → Dán nội dung JSON từ workflow gốc.
3. Nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** và có **nhiều node cần cấu hình chi tiết**. Dưới đây là hướng dẫn cụ thể cho từng phần quan trọng:

#### **🔹 STEP 1: Thiết Lập Credentials (BẮT BUỘC)**
Tất cả credentials phải được thêm **trước khi kích hoạt workflow**:
- **GoHighLevel OAuth2**:
  - Tạo app OAuth2 trên [GHN Marketplace](https://marketplace.gohighlevel.com/).
  - Thêm credential vào n8n với tên `YOUR_HL_CRED_ID` (ví dụ: `ghl_credential`).
- **Anthropic (Claude)**:
  - Thêm API Key vào n8n với tên `anthropic_api_key`.
- **OpenAI (GPT-4o)**:
  - Thêm API Key vào n8n với tên `openai_api_key`.
- **Google Gemini**:
  - Thêm API Key vào n8n với tên `gemini_api_key`.
- **Supabase**:
  - Thêm URL và Service Role Key với tên `supabase_credential`.
- **Google Sheets OAuth2**:
  - Thêm credential với tên `google_sheets_credential`.

#### **🔹 STEP 2: Cấu Hình Supabase**
1. **Tạo bảng `voice_call_logs`**:
   - Chạy SQL sau trên Supabase:
     ```sql
     CREATE TABLE voice_call_logs (
       id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
       call_id TEXT NOT NULL,
       phone_number TEXT,
       direction TEXT DEFAULT 'inbound',
       provider TEXT,
       duration_sec INTEGER,
       transcript TEXT,
       recording_url TEXT,
       bant_score INTEGER,
       qualified BOOLEAN DEFAULT FALSE,
       budget_confirmed BOOLEAN,
       authority_confirmed BOOLEAN,
       need_identified BOOLEAN,
       timeline_defined BOOLEAN,
       bant_summary TEXT,
       key_objections JSONB,
       appointment_requested BOOLEAN,
       preferred_time TEXT,
       ghl_contact_id TEXT,
       ghl_opp_id TEXT,
       crm_note TEXT,
       objection_response TEXT,
       outbound_call_id TEXT,
       created_at TIMESTAMPTZ DEFAULT NOW()
     );
     ```
   - **Thay thế `YOUR_SUPABASE_CRED_ID`** trong tất cả node Supabase bằng tên credential của bạn (ví dụ: `supabase_credential`).

2. **Cập nhật node `Log to Supabase` và `Log to Supabase NQ`**:
   - Mở node → Tab **Credentials** → Chọn credential Supabase vừa tạo.

#### **🔹 STEP 3: Cấu Hình GoHighLevel**
1. **Thay thế các placeholder ID**:
   | Placeholder | Giá Trị |
   |-------------|---------|
   | `YOUR_HL_CRED_ID` | Tên credential GHN trong n8n (ví dụ: `ghl_credential`) |
   | `YOUR_PIPELINE_ID` | ID Pipeline từ URL: `https://app.gohighlevel.com/pipelines/{PIPELINE_ID}` |
   | `YOUR_HOT_STAGE_ID` | ID Stage "Hot Lead" từ URL: `https://app.gohighlevel.com/opportunities/pipelines/{PIPELINE_ID}/stages/{STAGE_ID}` |
   | `YOUR_NURTURING_STAGE_ID` | ID Stage "Nurturing" tương tự |
   | `YOUR_NURTURE_WORKFLOW_ID` | ID Workflow tự động từ URL: `https://app.gohighlevel.com/automations/{WORKFLOW_ID}` |

2. **Cập nhật node `Search GHL Contact` và `Create Contact`**:
   - Mở node → Tab **Credentials** → Chọn credential GHN.
   - Thêm tham số `YOUR_PIPELINE_ID` vào **Request Headers** (nếu cần).

3. **Cập nhật node `Trigger Nurture Workflow`**:
   - Thêm **Environment Variable** `GHL_API_KEY` trong n8n Settings → Environment Variables với giá trị là Location API Key của GHN.

#### **🔹 STEP 4: Cấu Hình Voice Provider (Vapi/Retell)**
1. **Thiết lập Environment Variable**:
   - Trong n8n Settings → Environment Variables, thêm:
     | Key | Giá Trị |
     |-----|---------|
     | `VAPI_API_KEY` | API Key của Vapi/Retell |
     | `YOUR_VAPI_PHONE_NUMBER_ID` | ID Phone Number từ Vapi Dashboard |
     | `YOUR_VAPI_ASSISTANT_ID` | ID Assistant từ Vapi Dashboard |

2. **Cấu Hình Webhook Inbound**:
   - URL Webhook: `https://YOUR_N8N_URL/webhook/voice-sales-inbound`.
   - **Cấu hình Vapi/Retell**:
     - Đăng ký webhook `call_ended` để POST về URL trên.
     - Đảm bảo webhook này **chỉ gửi payload JSON** (không cần thêm header).

#### **🔹 STEP 5: Cấu Hình Google Sheets**
1. **Tạo sheet `Voice Call Log`**:
   - Tạo sheet mới với tên **`Voice Call Log`**.
   - Thêm các cột theo tiêu đề như trong phần **Yêu cầu cần thiết**.

2. **Cập nhật node `Log to Google Sheets` và `Log to Google Sheets NQ`**:
   - Mở node → Tab **Credentials** → Chọn credential Google Sheets.
   - Thêm tham số `YOUR_SPREADSHEET_ID` vào **Request Headers** (lấy từ URL sheet: `https://docs.google.com/spreadsheets/d/{SPREADSHEET_ID}/edit`).

#### **🔹 STEP 6: Cấu Hình Schedule Trigger (Outbound)**
- Node `Daily Outbound Schedule1` đã được cấu hình để chạy **lúc 9h sáng từ thứ 2 đến thứ 6**.
- **Không cần chỉnh** nếu muốn giữ lịch này.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Gọi một cuộc gọi test vào số Vapi/Retell.
   - Kiểm tra:
     - AI có phân tích BANT không?
     - Contact được tạo/cập nhật trong GHN không?
     - CRM Note được thêm vào không?
     - Log được ghi vào Supabase và Google Sheets không?

2. **Bật Active workflow**:
   - Sau khi test thành công, nhấn **Active** trên workflow.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tối ưu hóa AI Prompt**
- **Cải thiện độ chính xác BANT**:
  - Thêm ví dụ cụ thể vào prompt của Claude/GPT-4o để AI hiểu rõ hơn về tiêu chí BANT của doanh nghiệp.
  - Ví dụ:
    ```json
    "context": "Budget: Khách hàng phải có ngân sách >50 triệu. Authority: Người quyết định phải là trưởng phòng hoặc CEO. Need: Khách hàng phải có nhu cầu cụ thể về [sản phẩm/dịch vụ]. Timeline: Khách hàng phải xác định thời gian triển khai trong vòng 30 ngày."
    ```

- **Phản hồi objection chuyên nghiệp hơn**:
  - Thêm template phản hồi objection theo phương pháp **Challenger Sale** vào prompt của Claude Sonnet.

### **2. Kết hợp với Slack/Telegram**
- Thêm node **Slack/Telegram** để thông báo kết quả cuộc gọi:
  - Sau node `Qualified?`, thêm node **Slack** để gửi tin nhắn:
    ```json
    "message": "🚨 Lead mới được phân loại: {{$node["Qualified?"].json["qualified"] ? "Hot Lead" : "Nurture"}} - Phone: {{$node["Normalize Call Payload"].json["phone_number"]}}"
    ```

### **3. Lưu Log Chi Tiết**
- **Thêm node `Set`** sau node `Log to Supabase` để lưu thêm thông tin