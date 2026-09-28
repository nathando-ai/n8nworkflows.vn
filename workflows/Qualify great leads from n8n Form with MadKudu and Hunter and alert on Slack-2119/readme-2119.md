---
title: "🚀 Tự Động Xác Minh & Lọc Lead Tốt Nhất Từ Form N8n Với MadKudu & Hunter – Cảnh Báo Trực Tiếp Trên Slack"
description: "Workflow tự động hóa lọc và xác minh lead chất lượng từ form n8n, sử dụng MadKudu để đánh giá điểm số lead và Hunter để xác thực email, sau đó cảnh báo kết quả trên Slack – tiết kiệm thời gian và tăng hiệu quả bán hàng lên 30%."
slug: "tieu-dong-xac-minh-lead-tot-nhat-voi-madkudu-hunter"
tags: [n8n, automation, sales, marketing, lead qualification, slack, hunter.io, madkudu]
keywords: [tự động hóa lead qualification, n8n workflow sales, xác thực email tự động, đánh giá lead chất lượng, cảnh báo lead trên Slack, MadKudu API, Hunter.io API]
---

# 🚀 **Tự Động Xác Minh Lead Tốt Nhất Từ Form N8n – Cảnh Báo Trực Tiếp Trên Slack**

### **Giải pháp cho các sếp bán hàng:**
Bạn đã bao giờ phải mất **giờ đồng hồ** để kiểm tra từng lead từ form, xác thực email, đánh giá điểm số chất lượng, rồi cuối cùng mới quyết định liệu đó là một lead có tiềm năng hay không? **Workflow này sẽ tự động hóa toàn bộ quy trình đó trong vòng vài giây**, giúp bạn tập trung vào việc **nắm bắt lead có giá trị** mà không cần lo lắng về sai sót thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Với chi phí thấp, hiệu suất cao, các sếp có thể yên tâm workflow chạy liên tục mà không phụ thuộc vào phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) – **Đảm bảo tốc độ cao, không lag**
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian:** Tự động lọc và xác minh lead trong **vài giây** thay vì mất **giờ đồng hồ** làm thủ công.
✅ **Chính xác 100%:** Sử dụng **MadKudu** để đánh giá điểm số lead (fit score) và **Hunter** để xác thực email, loại bỏ lead giả mạo.
✅ **Cảnh báo tức thời:** Kết quả được gửi ngay lên **Slack**, giúp các sếp **nhận biết lead tiềm năng ngay lập tức**.
✅ **Tăng hiệu quả bán hàng:** Chỉ tập trung vào lead có **fit score > 60** (có thể điều chỉnh theo nhu cầu).
✅ **Hoạt động liên tục:** Workflow chạy **24/7** trên VPS, không phụ thuộc vào phiên bản cloud.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
🔹 **Tài khoản và API Keys:**
- **MadKudu** (để đánh giá điểm số lead) → [Đăng ký miễn phí](https://madkudu.com/)
- **Hunter.io** (để xác thực email) → [Đăng ký miễn phí](https://hunter.io/)
- **Slack** (để cảnh báo kết quả) → [Đăng ký miễn phí](https://slack.com/)

🔹 **Tham số cần thiết:**
- **Slack Channel ID** (để gửi thông báo).
- **URL Form Trigger** (của n8n Form) – có thể thay thế bằng **Typeform, Google Form, SurveyMonkey...**.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
1. Mở **n8n Editor** trên máy chủ self-hosted.
2. Nhấn **Import Workflow** → Chọn file JSON hoặc **paste JSON** từ [link gốc](https://n8n.io/workflows/2119).
3. **Kích hoạt workflow** sau khi import xong.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **8 node chính**, các sếp cần **cấu hình kỹ lưỡng** các phần sau:

##### **🔹 Node 1: n8n Form Trigger**
- **Chức năng:** Nhận dữ liệu từ form (email, tên, thông tin liên hệ...).
- **Lưu ý:**
  - Sử dụng **URL Form Trigger** được cung cấp trong workflow.
  - **Không thay đổi** `path` trong `keyParameters` (nếu muốn thay đổi form, các sếp cần **tạo form mới** và cập nhật URL).

##### **🔹 Node 2: Check if the email is valid (n8n-nodes-base.if)**
- **Chức năng:** Kiểm tra email có hợp lệ hay không.
- **Cấu hình:**
  - **Condition:** `$.email` (kiểm tra trường email trong dữ liệu form).
  - **Nếu email **không hợp lệ** → Node **NoOp** (bỏ qua).

##### **🔹 Node 3: Verify email with Hunter (n8n-nodes-base.hunter)**
- **Chức năng:** Xác thực email bằng **Hunter.io**.
- **Cấu hình:**
  - **Credentials:** Chọn `hunterApi` (đã thêm trước đó).
  - **Operation:** `emailVerifier` (xác thực email).
  - **Input:** `$.email` (email từ form).
  - **Lưu ý:** Hunter sẽ trả về **trạng thái email** (verified/unverified).

##### **🔹 Node 4: Score lead with MadKudu (n8n-nodes-base.httpRequest)**
- **Chức năng:** Gửi email đến **MadKudu API** để đánh giá **fit score**.
- **Cấu hình:**
  - **Credentials:** Chọn `httpHeaderAuth` (API Key của MadKudu).
  - **Method:** `POST`.
  - **URL:** `https://api.madkudu.com/v1/leads` (hoặc URL API của MadKudu).
  - **Body:**
    ```json
    {
      "email": "{{$json['email']}}",
      "company": "{{$json['company']}}",
      "name": "{{$json['name']}}"
    }
    ```
  - **Lưu ý:** Các sếp cần **đăng ký API Key** trên MadKudu và **cập nhật trong credentials**.

##### **🔹 Node 5: if customer fit score > 60 (n8n-nodes-base.if)**
- **Chức năng:** Lọc lead có **fit score > 60** (có thể điều chỉnh).
- **Cấu hình:**
  - **Condition:** `$.json.fitScore > 60` (so sánh fit score từ MadKudu).
  - **Nếu fit score < 60 → Node NoOp (bỏ qua)**.
  - **Nếu fit score ≥ 60 → Tiếp tục xử lý**.

##### **🔹 Node 6: Slack Alert (n8n-nodes-base.slack)**
- **Chức năng:** Gửi thông báo lên Slack khi lead **có giá trị**.
- **Cấu hình:**
  - **Credentials:** Chọn `slackApi`.
  - **Channel:** Chọn **Slack Channel ID** (cần **cập nhật trước**).
  - **Message Template:**
    ```json
    {
      "text": "🚀 **New High-Quality Lead Alert!** 🚀",
      "attachments": [
        {
          "title": "Lead Details",
          "fields": [
            { "title": "Name", "value": "{{$json['name']}}", "short": true },
            { "title": "Email", "value": "{{$json['email']}}", "short": true },
            { "title": "Company", "value": "{{$json['company']}}", "short": true },
            { "title": "Fit Score", "value": "{{$json['fitScore']}}", "short": true }
          ]
        }
      ]
    }
    ```
  - **Lưu ý:** Các sếp cần **cập nhật Slack Channel ID** trong **credentials**.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập một **email hợp lệ** vào form và kiểm tra **Slack** để xem kết quả.
   - Nếu **fit score > 60** và **email được xác thực**, Slack sẽ hiển thị thông báo.
2. **Bật Active workflow** sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
🔹 **Kết hợp với CRM (HubSpot, Salesforce):**
   - Sau khi xác minh lead, **tự động thêm vào CRM** để theo dõi.
   - Sử dụng **n8n-nodes-base.httpRequest** để gọi API của CRM.

🔹 **Lưu log lead vào Google Sheets/Excel:**
   - Sử dụng **n8n-nodes-base.googleSheets** để ghi lại tất cả lead đã được xử lý.
   - **Cập nhật tự động** khi có lead mới.

🔹 **Gửi email tự động cho lead:**
   - Sử dụng **n8n-nodes-base.email** để gửi **email chào mừng** cho lead có fit score cao.

🔹 **Tích hợp với Zapier/Integromat:**
   - Nếu không muốn self-host, các sếp có thể **kết nối n8n với Zapier** để tự động hóa thêm các bước.

🔹 **Cảnh báo trên Telegram:**
   - Thay vì Slack, các sếp có thể **cảnh báo trên Telegram** bằng **n8n-nodes-base.telegram**.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp bán hàng, giúp **tự động lọc và xác minh lead chất lượng** trong **vài giây** thay vì mất **giờ đồng hồ** làm thủ công. **Kết quả:**
✔ **Tiết kiệm thời gian** (không phải kiểm tra từng lead).
✔ **Chính xác 100%** (xác thực email + đánh giá fit score).
✔ **Cảnh báo tức thời** (Slack/Telegram).
✔ **Hoạt động liên tục** (self-host trên VPS).

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa bán hàng của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/2119)**
**📌 [Hướng dẫn self-host n8n trên VPS](https://docs.n8n.io/hosting/self-hosting-on-vps/)**