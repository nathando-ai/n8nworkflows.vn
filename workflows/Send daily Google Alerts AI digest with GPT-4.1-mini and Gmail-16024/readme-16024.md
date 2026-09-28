---
title: "🚀 Tự Động Hóa Báo Cáo AI Tóm Tắt Google Alerts Hàng Ngày Với GPT-4.1-mini & Gmail"
description: "Giải pháp tự động hóa hoàn toàn không cần code để phân tích, đánh giá và gửi báo cáo tóm tắt tin tức liên quan từ Google Alerts hàng ngày qua email HTML đẹp mắt. Tiết kiệm thời gian cho các quản lý thương hiệu, nhóm PR và phân tích cạnh tranh."
slug: "tieu-dong-hoa-google-alerts-ai-digest-gpt-4-1-mini-gmail"
tags: [n8n, automation, no-code, market-research, ai-summarization, google-alerts, gmail-automation]
keywords: [tự động hóa google alerts, n8n workflow, ai tóm tắt tin tức hàng ngày, gpt-4.1-mini tự động hóa, báo cáo cạnh tranh tự động, gửi email tự động]
---

# 🚀 **Tự Động Hóa Báo Cáo AI Tóm Tắt Google Alerts Hàng Ngày Với GPT-4.1-mini & Gmail**

### **Giải pháp cho ai?**
Các **quản lý thương hiệu, nhóm PR, chuyên gia cạnh tranh** đang phải mất **giờ đồng hồ** mỗi ngày để:
- Theo dõi hàng trăm Google Alerts thủ công.
- Phân tích tin tức liên quan, đánh giá độ quan trọng và tình cảm (sentiment).
- Tóm tắt và gửi báo cáo định kỳ cho đội ngũ.

**Workflow này tự động hóa toàn bộ quy trình trong 1 giờ cài đặt**, giúp bạn:
✅ **Nhận báo cáo tóm tắt AI** hàng ngày với **độ chính xác cao** từ GPT-4.1-mini.
✅ **Lọc tin tức quan trọng** (đánh giá từ 1-10) và **đánh giá tình cảm** (Tích cực/Trung lập/Xấu).
✅ **Gửi email HTML đẹp mắt** với **thống kê, badge màu sắc** và **gợi ý hành động** cho từng tin.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** so với cách làm thủ công.
- **Độ chính xác cao** với phân tích AI từ GPT-4.1-mini.
- **Báo cáo cá nhân hóa** với **thống kê, badge màu sắc** và **gợi ý hành động**.
- **Hoạt động tự động** 24/7, không cần can thiệp.
- **Gửi email HTML đẹp mắt** thay vì văn bản thô.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Alerts** (để lấy URL RSS của các alert).
2. **API Key OpenAI** (để kết nối với GPT-4.1-mini).
3. **Tài khoản Gmail** (để gửi email báo cáo hàng ngày).
4. **Danh sách các Google Alerts** (cần định nghĩa trong workflow).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/16024](https://n8n.io/workflows/16024) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/16024) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **12 node**, các sếp cần chú ý cấu hình các node sau:

##### **🔹 Node 2: Code — Set Alert Feed URLs**
- **Cần thay đổi:**
  - Thay thế **URL RSS mẫu** bằng URL RSS của **Google Alerts** riêng của bạn.
  - **Cách lấy URL RSS:**
    1. Mở [Google Alerts](https://www.google.com/alerts).
    2. Chọn alert cần lấy.
    3. Nhấp vào **RSS icon** (📡) → Copy URL.
  - **Cấu trúc cần thêm:**
    ```json
    [
      {
        "name": "Alert Brand Name",
        "url": "https://www.google.com/alerts/feed/...",
        "category": "Brand"
      },
      {
        "name": "Alert Competitor X",
        "url": "https://www.google.com/alerts/feed/...",
        "category": "Competitor"
      }
    ]
    ```

##### **🔹 Node 6: AI Agent — Analyze Alert (GPT-4.1-mini)**
- **Cần kết nối OpenAI API:**
  1. Tạo **API Key** tại [OpenAI](https://platform.openai.com/account/api-keys).
  2. Trong node **OpenAI — GPT-4.1-mini Model**, chọn **credentials** đã tạo.
  3. **Tham số mặc định:**
     - Model: `gpt-4.1-mini`
     - Temperature: `0.2` (đảm bảo kết quả nhất quán)
     - Max Tokens: `250` (đủ để phân tích tin tức)

##### **🔹 Node 11: Gmail — Send Digest Email**
- **Cần kết nối Gmail OAuth2:**
  1. Tạo **credentials Gmail** trong n8n (nếu chưa có).
  2. Thay thế `REPLACE_WITH_YOUR_EMAIL@example.com` bằng **email nhận báo cáo**.
  3. **Lưu ý:**
     - Email này **không được đặt là Gmail chính** (nên tạo 1 email phụ).
     - Nếu gặp lỗi OAuth, tham khảo [hướng dẫn kết nối Gmail](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.gmail.html).

##### **🔹 Node 10: Code — Build HTML Email Digest**
- **Cần thay thế `YOUR_BRAND_NAME`** trong footer bằng tên công ty của bạn.

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Execute Workflow** và kiểm tra email nhận được.
2. **Bật Active Workflow** để chạy hàng ngày.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notifications:**
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi báo cáo cùng lúc với email.
   - **Cách thêm:**
     ```json
     {
       "name": "Slack — Send Alert",
       "type": "slack",
       "operation": "sendMessage",
       "credentials": "slack_credential",
       "text": "{{ $json.emailBody }}"
     }
     ```

2. **Lưu Log vào Google Sheets:**
   - Sử dụng node **Google Sheets** để ghi lại **tất cả alert** (bao gồm cả những alert bị loại).
   - **Cách thêm:**
     ```json
     {
       "name": "Google Sheets — Log All Alerts",
       "type": "googleSheets",
       "operation": "createRow",
       "credentials": "google_sheets_credential",
       "sheetName": "Alert_Log",
       "data": {
         "Title": "{{ $node["Parse RSS Entries"].json["title"] }}",
         "URL": "{{ $node["Parse RSS Entries"].json["link"] }}",
         "Score": "{{ $node["Parse AI Response"].json["score"] }}",
         "Sentiment": "{{ $node["Parse AI Response"].json["sentiment"] }}"
       }
     }
     ```

3. **Gửi Báo Cáo Định Kỳ (Tuần/Tháng):**
   - Thay đổi **Schedule Trigger** từ `Every 24 Hours` sang `Every Monday at 9 AM` (hoặc ngày khác).
   - **Cách thay đổi:**
     - Trong node **Schedule — Every 24 Hours**, chỉnh:
       ```json
       {
         "cron": "0 9 * * 1" // Gửi hàng tuần thứ 2 lúc 9 AM
       }
       ```

4. **Tối ưu Prompt cho GPT-4.1-mini:**
   - Nếu kết quả AI không chính xác, chỉnh sửa **Prompt** trong node **AI Agent**:
     ```json
     {
       "prompt": "Analyze this news article and provide:
       - Relevance Score (1-10)
       - One-sentence insight
       - Sentiment (Positive/Neutral/Negative)
       - Recommended action
       Format response as JSON: {{ $json }}"
     }
     ```

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc theo dõi Google Alerts thủ công, đồng thời **cung cấp báo cáo AI tóm tắt** với **độ chính xác cao** và **định dạng chuyên nghiệp**. **Chỉ cần 1 giờ cài đặt**, bạn sẽ nhận được **báo cáo hàng ngày tự động** qua email, giúp **quản lý thương hiệu, PR và cạnh tranh** trở nên hiệu quả hơn.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho công việc quan trọng hơn!**

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/16024)**
**💡 Cần hỗ trợ? Hỏi ngay tại [Community n8n](https://community.n8n.io/)**