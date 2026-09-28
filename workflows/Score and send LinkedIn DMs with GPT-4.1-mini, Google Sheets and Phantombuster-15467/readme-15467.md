---
title: "🚀 Tự Động Hóa Outreach LinkedIn Siêu Tốc: Scoring Lead + DM Cá Nhân Hóa Bằng AI + Phantombuster"
description: "Workflow tự động hóa outreach LinkedIn chuyên nghiệp với AI GPT-4.1-mini, Google Sheets và Phantombuster giúp các sếp tiết kiệm 10+ giờ/ngày trong lead nurturing, tăng tỷ lệ phản hồi lên 30%+ và tự động hóa toàn bộ pipeline từ scoring đến closing lead."
slug: "tieu-dong-hoa-outreach-linkedin-ai-phantombuster"
tags: [n8n, automation, lead-nurturing, ai-chatbot, linkedin-outreach, google-sheets, openai, phantombuster]
keywords: [tự động hóa outreach linkedin, scoring lead bằng ai, dm linkedin tự động, phantombuster n8n, google sheets automation, ai chatbot sales]
---

# 🚀 **Outreach LinkedIn Siêu Tốc: Scoring Lead + DM Cá Nhân Hóa Bằng AI + Phantombuster**

### **Giải pháp tự động hóa outreach LinkedIn 100% không code cho các sếp B2B**
Hãy tưởng tượng một ngày không phải mất 5-10 giờ để tìm kiếm lead, viết DM cá nhân hóa, theo dõi phản hồi và cập nhật CRM thủ công. **Workflow này tự động hóa toàn bộ quy trình từ scoring lead đến closing lead**, giúp các sếp tiết kiệm thời gian, tăng tỷ lệ phản hồi và tự động hóa pipeline sales.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** trong lead nurturing với tự động hóa toàn bộ quy trình.
- **Tăng tỷ lệ phản hồi lên 30%+** nhờ DM cá nhân hóa bằng AI GPT-4.1-mini.
- **Quản lý lead hiệu quả** với scoring tự động (Hot/Warm/Cold) và lịch trình tự động.
- **Tự động hóa closing lead** khi không có phản hồi sau 3-5 ngày.
- **Lưu trữ toàn bộ lịch sử** trong Google Sheets, dễ dàng theo dõi và báo cáo.
- **Tuân thủ LinkedIn** với giới hạn DM an toàn (20 DM/ngày) nhờ Phantombuster.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với bảng dữ liệu có cấu trúc chuẩn (xem chi tiết dưới đây).
2. **API Key OpenAI** (để sử dụng GPT-4.1-mini).
3. **API Key Phantombuster** + **ID Agent LinkedIn** (để gửi DM tự động).
4. **Tài khoản LinkedIn** (đăng ký trên Phantombuster để sử dụng agent).
5. **VPS n8n** (để workflow chạy 24/7).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/15467](https://n8n.io/workflows/15467) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15467) và paste vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **16 node** với logic phức tạp. Dưới đây là hướng dẫn chi tiết để cấu hình:

#### **A. Cấu hình Google Sheets**
- **Bảng dữ liệu cần có các cột sau** (không được thiếu):
  | Cột | Loại Dữ liệu | Ghi chú |
  |------|--------------|---------|
  | # | Số | ID duy nhất cho mỗi lead |
  | First Name | Text | Tên của lead |
  | Title | Text | Chức vụ của lead |
  | Company Name | Text | Tên công ty |
  | LinkedIn URL | Text | Link LinkedIn đầy đủ |
  | Country | Text | Quốc gia |
  | Status | Text | Trạng thái: *Contacted / Follow-up Sent / Replied / Closed* |
  | Step | Số | Bước hiện tại: *0 (mới) / 1 (đã gửi DM) / 2 (đã gửi follow-up) / 3 (đóng)* |
  | LastContacted | ISO timestamp | Thời gian cuối cùng liên lạc |
  | NextActionDate | ISO timestamp | Ngày tiếp theo cần hành động |
  | AI_LeadScore | Text | *Hot / Warm / Cold* |
  | AI_Priority | Text | *High / Medium / Low* |
  | AI_MessageAngle | Text | *pain_point / value_add / curiosity / social_proof* |
  | AI_FirstDM | Text | Nội dung DM đầu tiên (sẽ được AI tự động hóa) |
  | AI_FollowupDM | Text | Nội dung DM follow-up (sẽ được AI tự động hóa) |
  | Response | Text | Phản hồi hoặc lý do đóng lead |

- **Cách kết nối Google Sheets trong n8n:**
  1. Tạo **credentials OAuth2** trong n8n với quyền đọc/giới hạn viết vào bảng.
  2. Trong node **"Get Prospects from Sheet"**, chọn **Google Sheets** và chọn sheet tương ứng.

#### **B. Cấu hình OpenAI (GPT-4.1-mini)**
- **Bước 1:** Tạo **credentials OpenAI** trong n8n với API Key của bạn.
- **Bước 2:** Trong các node **"Score Lead with AI"**, **"Generate First DM"**, và **"Generate Follow-up DM"**:
  - Chọn **OpenAI** như provider.
  - Đặt **model** là `gpt-4-1106-preview` (hoặc phiên bản mới nhất của GPT-4.1-mini).
  - **Prompt mẫu** (cần chỉnh sửa theo nhu cầu):
    ```json
    "You are a LinkedIn outreach expert. Score this lead based on their role, company, and LinkedIn profile. Return a structured JSON with:
    - LeadScore: 'Hot', 'Warm', or 'Cold'
    - Priority: 'High', 'Medium', or 'Low'
    - MessageAngle: 'pain_point', 'value_add', 'curiosity', or 'social_proof'
    - FirstDM: A short, personalized cold DM (max 150 words)
    - FollowupDM: A soft follow-up DM (max 100 words)
    Data: {First Name: '[First Name]', Title: '[Title]', Company: '[Company]', LinkedIn URL: '[LinkedIn URL]'}"
    ```

#### **C. Cấu hình Phantombuster**
- **Bước 1:** Tạo **credentials HTTP Request** trong n8n với:
  - **URL API Phantombuster**: `https://api.phantombuster.com/api/v1/phantom/[PHANTOM_ID]/run`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer [YOUR_PHANTOM_BUSTER_API_KEY]",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "data": {
        "linkedin_message_sender": {
          "message": "{{$node["Parse First DM"].json["AI_FirstDM"]}}",
          "recipient": "{{$node["Get Prospects from Sheet"].json[0].LinkedIn_URL}}",
          "agent_id": "[YOUR_LINKEDIN_AGENT_ID]"
        }
      }
    }
    ```
- **Bước 2:** Trong node **"Send First DM via Phantombuster"**, chọn **HTTP Request** và điền thông tin như trên.

#### **D. Cấu hình Schedule Trigger**
- **Bước 1:** Trong node **"Schedule Trigger"**, chọn **Hourly** (hoặc tùy chỉnh theo nhu cầu).
- **Bước 2:** Đảm bảo **Google Sheets** và **Phantombuster** đều hoạt động ổn định.

#### **E. Cấu hình Logic Routing (Switch Node)**
- Node **"Route by Step"** sử dụng logic:
  - **Step = 0** → Chuyển sang **First DM flow**.
  - **Step = 1** → Chuyển sang **Follow-up DM flow**.
  - **Step ≥ 2** → **Auto-close lead**.

---

### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Thêm 1-2 lead vào Google Sheets với **Step = 0** và **Status = ""** (trống).
   - Chạy workflow và kiểm tra:
     - AI có scoring lead không?
     - DM có được gửi qua Phantombuster không?
     - Google Sheets có cập nhật trạng thái không?
2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển trạng thái workflow thành **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu Prompt AI**:
   - Thay đổi **Prompt** trong node **"Score Lead with AI"** để phù hợp với ngành nghề của bạn.
   - Ví dụ: Nếu là SaaS, có thể thêm yêu cầu về **CTA (Call-to-Action)** trong DM.

2. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để thông báo khi DM được gửi hoặc lead được closing.

3. **Lưu log hoạt động**:
   - Sử dụng node **Google Sheets** để ghi lại tất cả hoạt động (thời gian gửi, phản hồi, lỗi...).

4. **Giới hạn DM an toàn**:
   - Đặt **daily limit** trong Phantombuster là **20 DM/ngày** để tránh bị LinkedIn chặn.

5. **Tự động hóa báo cáo**:
   - Sử dụng node **Google Sheets** để tạo báo cáo hàng tuần về:
     - Số lead được tiếp cận.
     - Tỷ lệ phản hồi.
     - Lead được closing.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp B2B muốn tự động hóa outreach LinkedIn một cách chuyên nghiệp, tiết kiệm thời gian và tăng tỷ lệ chuyển đổi. **Không cần code, chỉ cần cấu hình và chạy 24/7!**

:::tip[Hành động ngay]
1. **Cài đặt n8n trên VPS** (để workflow chạy liên tục).
2. **Chuẩn bị Google Sheets, OpenAI API và Phantombuster**.
3. **Import workflow và cấu hình theo hướng dẫn**.
4. **Thêm lead đầu tiên và bắt đầu tự động hóa!**

**Chúc các sếp thành công với outreach LinkedIn siêu tốc!** 🚀