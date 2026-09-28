---
title: "🚀 Tự Động Hóa Outreach B2B Từ LinkedIn Đến Email: AI + AnyMailFinder + Perplexity (Không Cần Code)"
description: "Workflow tự động hóa outreach B2B chuyên nghiệp, kết hợp AI GPT-4, AnyMailFinder và Perplexity để tìm kiếm email, tạo nội dung cá nhân hóa và gửi email tự động. Giúp các sếp tiết kiệm 10+ giờ/ngày trong lead nurturing."
slug: "tieu-dong-hoa-outreach-b2b-linkedin-den-email"
tags: [n8n, automation, lead-nurturing, ai-business, outreach-automation, sales-automation, ai-chatbot]
keywords: [tự động hóa outreach B2B, n8n workflow, tìm kiếm email AnyMailFinder, AI tạo nội dung email, tự động hóa bán hàng, lead nurturing tự động]
---

# 🚀 **Tự Động Hóa Outreach B2B Từ LinkedIn Đến Email: AI + AnyMailFinder + Perplexity**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp Trong Outreach B2B**
Bạn đã bao giờ phải:
- **Tìm kiếm email** của lead từ LinkedIn trong hàng giờ?
- **Tạo nội dung email** cá nhân hóa cho từng lead, nhưng lại mất thời gian viết lại?
- **Gửi email thủ công** và lo lắng về hiệu quả thấp?
- **Không biết cách kết hợp AI** để tối ưu hóa quy trình outreach?

Workflow này **giải quyết tất cả** bằng cách tự động hóa **tất cả các bước** từ tìm kiếm lead trên LinkedIn đến gửi email cá nhân hóa, **không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/ngày** trong việc tìm kiếm email và viết email.
✅ **Tăng tỷ lệ mở email** nhờ nội dung cá nhân hóa bởi AI.
✅ **Tự động hóa outreach liên tục** (không cần can thiệp thủ công).
✅ **Kết hợp AI GPT-4 + Perplexity** để tối ưu hóa nội dung.
✅ **Lưu trữ lead và lịch sử** trên Google Sheets để theo dõi.
✅ **Gửi email tự động** qua AnyMailFinder (không cần SMTP).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản LinkedIn cá nhân** (để tìm kiếm lead).
✔ **Tài khoản AnyMailFinder** (để tìm email từ LinkedIn).
✔ **API Key OpenAI** (để sử dụng GPT-4).
✔ **API Key Perplexity** (để tối ưu hóa nội dung).
✔ **Google Sheets** (để lưu trữ lead và lịch sử).
✔ **Tài khoản email** (để gửi email tự động).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7929](https://n8n.io/workflows/7929).
- **Mở n8n Editor** → **Import** → Chọn file JSON.
- **Hoặc copy/paste** JSON vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **19 node**, nhưng các bước **quan trọng nhất** cần điều chỉnh:

##### **A. Cấu Hình AnyMailFinder (Tìm Email)**
- **Node: "HTTP Request"** (tìm kiếm email từ LinkedIn)
  - **URL:** `https://api.anymailfinder.com/v1/find`
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer YOUR_ANYMAILFINDER_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON):**
    ```json
    {
      "email": "linkedin_profile_url_here",
      "limit": 10
    }
    ```

##### **B. Cấu Hình AI (Tạo Nội Dung Email)**
- **Node: "OpenAI Chat Model4" & "OpenAI Chat Model5"**
  - **Model:** `gpt-4` (hoặc `gpt-3.5-turbo` nếu tiết kiệm chi phí).
  - **Prompt:** Sử dụng **template cá nhân hóa** (ví dụ: *"Tôi là [Tên], CEO của [Công Ty]. Tôi thấy [Lead] có kinh nghiệm trong [Ngành Nghề]. Hãy giúp tôi viết một email ngắn gọn, thân thiện và hiệu quả để liên lạc với họ về [Mục Đích]."*).
  - **API Key:** Điền **OpenAI API Key** vào **Credentials** của node.

- **Node: "Perplexity" (Tối ưu hóa nội dung)**
  - **API Key:** Điền **Perplexity API Key**.
  - **Prompt:** *"Optimize this email for better engagement: [Email Content]."*

##### **C. Cấu Hình Google Sheets (Lưu Trữ Lead)**
- **Node: "Get row(s) in sheet1"**
  - **Sheet Name:** Đặt tên là **"Leads"** (cần tạo trước trên Google Sheets).
  - **Columns:** `LinkedIn URL | Email | Status | Last Contact`.

- **Node: "Update no find email" & "Update Final"**
  - **Sheet Name:** Cùng là **"Leads"**.
  - **Columns:** `Status` (cập nhật thành **"Found"** hoặc **"Not Found"**).

##### **D. Cấu Hình Gửi Email (AnyMailFinder)**
- **Node: "HTTP Request" (gửi email)**
  - **URL:** `https://api.anymailfinder.com/v1/send`
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer YOUR_ANYMAILFINDER_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON):**
    ```json
    {
      "email": "{{$node["Set credentials"].json["email"]}}",
      "subject": "{{$node["Set Email Template"].json["subject"]}}",
      "body": "{{$node["Structured Output Parser2"].json["email_content"]}}"
    }
    ```

##### **E. Cấu Hình LinkedIn (Post Tương Tác)**
- **Node: "Personal LinkedIn Account POST"**
  - **URL:** `https://api.linkedin.com/v2/ugcPosts`
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer YOUR_LINKEDIN_ACCESS_TOKEN",
      "X-Restli-Protocol-Version": "2.0.0",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON):**
    ```json
    {
      "author": "urn:li:person:YOUR_LINKEDIN_ID",
      "lifecycleState": "PUBLISHED",
      "specificContent": {
        "com.linkedin.ugc.ShareContent": {
          "shareCommentary": {
            "text": "{{$node["Set Email Template"].json["post_content"]}}"
          },
          "shareMediaCategory": "NONE"
        }
      },
      "visibility": {
        "com.linkedin.ugc.MemberNetworkVisibility": "PUBLIC"
      }
    }
    ```

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1-2 lead mẫu** để kiểm tra:
   - Email có được tìm thấy không?
   - Nội dung email có hợp lý không?
   - Email có được gửi thành công không?
2. **Bật Active** workflow sau khi kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**
   - Thêm **node Slack Webhook** để thông báo khi email được gửi thành công.
   - **Node:** `n8n-nodes-base.slack`

2. **Lưu Log & Báo Cáo**
   - Sử dụng **Google Sheets** để lưu lịch sử outreach.
   - Thêm **node "Code"** để tính toán tỷ lệ mở email.

3. **Tối ưu hóa AI**
   - Sử dụng **LangChain** (node `@n8n/n8n-nodes-langchain`) để cải thiện prompt.
   - Thử **Perplexity AI** để viết email dài hơn và chuyên nghiệp hơn.

4. **Automate Follow-ups**
   - Thêm **node "Wait"** (delay 3-7 ngày) trước khi gửi email thứ 2.
   - Sử dụng **node "If"** để kiểm tra trạng thái lead trước khi gửi tiếp.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì làm việc thủ công. Với **AI + AnyMailFinder + Perplexity**, outreach B2B trở nên **nhanh chóng, cá nhân hóa và hiệu quả hơn bao giờ hết!**

👉 **Bắt đầu ngay hôm nay!**
1. **Import workflow** từ [n8n.io/workflows/7929](https://n8n.io/workflows/7929).
2. **Cấu hình API keys** và **Google Sheets**.
3. **Test run** và **bật Active**.
4. **Xem kết quả** trong Google Sheets!

**Nếu cần hỗ trợ**, liên hệ với tác giả LukaszB tại **kontakt@lumizone.pl** hoặc comment bên dưới! 🚀