---
title: "🚀 Tự Động Hóa Email Outreach Cá Nhân Hóa Sử Dụng LinkedIn, Crunchbase & Gemini AI - Giảm 80% Thời Gian Làm Thủ Công"
description: "Workflow này tự động tra cứu thông tin chi tiết từ LinkedIn và Crunchbase, sau đó sử dụng Gemini AI để tạo nội dung email outreach cá nhân hóa hoàn toàn tự động. Giúp các sếp tiết kiệm thời gian, tăng tỷ lệ phản hồi và nâng cao hiệu quả bán hàng."
slug: "tieu-dong-hoa-email-outreach-ca-nhan-hoa-voi-linkedin-crunchbase-gemini"
tags: [n8n, automation, lead-nurturing, ai-chatbot, linkedin-scraping, crunchbase-api, gemini-ai, email-marketing]
keywords: [n8n workflow outreach, tự động hóa email cá nhân hóa, LinkedIn API, Crunchbase API, Gemini AI, cold email automation, lead generation]
---

# 🚀 **Tự Động Hóa Email Outreach Cá Nhân Hóa Sử Dụng LinkedIn, Crunchbase & Gemini AI**

## **📌 Nỗi Đau Của Các Sếp Trong Email Outreach**
Các sếp thường phải mất **giờ đồng hồ** để:
- Tra cứu thông tin chi tiết của khách hàng tiềm năng trên LinkedIn và Crunchbase (địa chỉ email, vị trí công việc, thông tin công ty).
- Viết nội dung email **cá nhân hóa** phù hợp với từng cá nhân, tránh bị đánh vào spam.
- Theo dõi và cập nhật trạng thái của từng lead một cách thủ công.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Tra cứu thông tin** từ LinkedIn và Crunchbase.
✅ **Tạo email outreach cá nhân hóa** bằng Gemini AI.
✅ **Cập nhật trạng thái** trong bảng dữ liệu tự động.
✅ **Tiết kiệm thời gian** lên đến **80%** so với làm thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quá trình tra cứu và viết email, cho phép các sếp tập trung vào chiến lược bán hàng.
- **Email cá nhân hóa cao**: Gemini AI phân tích dữ liệu và tạo nội dung email phù hợp với từng lead.
- **Dữ liệu chính xác**: Thông tin từ LinkedIn và Crunchbase được cập nhật liên tục.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp thủ công.
- **Tăng tỷ lệ phản hồi**: Email cá nhân hóa giúp tăng cơ hội được trả lời từ khách hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản RapidAPI** (để tra cứu dữ liệu từ LinkedIn và Crunchbase):
   - [Đăng ký tại RapidAPI](https://rapidapi.com/ikemo-ikemo-default/api/cold-outreach-enrichment-scraper) (miễn phí hoặc trả phí tùy thuộc vào nhu cầu).
   - **API Key** của RapidAPI (được cung cấp sau khi đăng ký).

2. **Bảng dữ liệu (Google Sheets/Excel)** với các cột sau:
   | Cột Tên               | Mô Tả                                  |
   |-----------------------|----------------------------------------|
   | First_name             | Tên đầu tiên của lead                  |
   | Last_name              | Tên cuối của lead                      |
   | email                  | Email của lead                         |
   | Title                  | Chức vụ của lead                      |
   | Location               | Vị trí công tác                        |
   | Company_Name           | Tên công ty                             |
   | Company_site           | Website công ty                        |
   | Linkedin_URL           | Link LinkedIn cá nhân                  |
   | Crunchbase_URL         | Link Crunchbase công ty                |
   | email_subject          | Chủ đề email (có thể để trống)         |
   | email_body             | Nội dung email (có thể để trống)        |

3. **Google Cloud API Key** (để sử dụng Gemini AI):
   - [Cài đặt Google Cloud API](https://ai.google.dev/tutorials/quickstart) và lấy **API Key** cho Gemini.

4. **Tài khoản n8n Self-hosted** (để chạy workflow 24/7):
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [đây](https://n8n.io/workflows/9814) (hoặc sử dụng file JSON đã cung cấp).
2. Mở **n8n Editor** và nhấn **"Import"** → Chọn file JSON.
3. Hoặc copy toàn bộ JSON và nhấn **"Paste JSON"** trong Editor.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **27 node**, nhưng các sếp cần chú ý đặc biệt đến các node sau:

#### **🔹 Node "Google Gemini Chat Model" (lmChatGoogleGemini)**
- **Yêu cầu**:
  - Đăng ký **Google Cloud API** và lấy **API Key**.
  - Trong node này, chọn **credentials** là `googlePalmApi` (đã được cấu hình trước).
  - Điền **API Key** vào **Google Cloud API Key** trong **n8n Credentials Manager**.

#### **🔹 Node "RapidAPI-Key" (set)**
- **Yêu cầu**:
  - Sau khi đăng ký RapidAPI, copy **API Key** và dán vào node này.
  - Node này sẽ truyền **API Key** cho các request HTTP sau.

#### **🔹 Node "Linkedin_URL", "Linkedin_URL_COMPANY", "Crunchbase_URL" (httpRequest)**
- **Yêu cầu**:
  - Các node này sử dụng **API từ RapidAPI** để tra cứu dữ liệu.
  - **URL Base** của API RapidAPI là:
    ```
    https://cold-outreach-enrichment-scraper.p.rapidapi.com/
    ```
  - Các sếp cần đảm bảo **API Key** đã được truyền đúng vào header của request.

#### **🔹 Node "Get row(s)" và "Update row(s)" (dataTable)**
- **Yêu cầu**:
  - Chọn **Google Sheets** hoặc **Excel Online** làm nguồn dữ liệu.
  - Điền **Sheet Name** và **Credentials** (n8n sẽ tự động lấy từ **Google Sheets Credentials**).
  - Các node này sẽ **lấy dữ liệu lead** và **cập nhật trạng thái** sau khi xử lý xong.

#### **🔹 Node "Agent One" và "Judge Agent" (agent)**
- **Yêu cầu**:
  - Các agent này sử dụng **Gemini AI** để phân tích và tạo nội dung email.
  - Đảm bảo **Google Gemini Chat Model** đã được cấu hình đúng (node ở trên).

#### **🔹 Node "Approval Route" (if)**
- **Yêu cầu**:
  - Node này kiểm tra xem email đã được tạo chưa.
  - Nếu chưa, workflow sẽ tiếp tục tạo email mới.
  - Nếu đã, workflow sẽ **bỏ qua** và chuyển sang node tiếp theo.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với một lead mẫu:
   - Chọn một hàng trong bảng dữ liệu và nhấn **"Execute Workflow"**.
   - Kiểm tra xem workflow có chạy đúng không (đặc biệt là phần tra cứu LinkedIn/Crunchbase và tạo email).
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi Email Tự Động**:
   - Kết hợp với **n8n Email Node** hoặc **SendGrid API** để gửi email tự động sau khi tạo xong.

2. **Lưu Log Hoạt Động**:
   - Sử dụng **Google Sheets Log** hoặc **Slack Notification** để theo dõi trạng thái của từng lead.

3. **Báo Cáo Định Kỳ**:
   - Tạo một workflow phụ để **tổng hợp báo cáo** về tỷ lệ phản hồi, thời gian phản hồi, và hiệu quả của email outreach.

4. **Kết Hợp Slack/Telegram**:
   - Khi workflow hoàn thành, gửi thông báo lên **Slack** hoặc **Telegram** để các sếp biết.

5. **Tối Ưu Hóa Gemini AI**:
   - Thử nghiệm với các **prompt khác nhau** để cải thiện chất lượng email (ví dụ: thêm thông tin công ty, vị trí, hoặc sở thích cá nhân).
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa **email outreach cá nhân hóa** một cách hiệu quả. Bằng cách kết hợp **LinkedIn, Crunchbase, và Gemini AI**, nó giúp:
✔ **Tiết kiệm thời gian** lên đến 80%.
✔ **Tăng tỷ lệ phản hồi** nhờ email cá nhân hóa.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hãy thử ngay và nâng cao hiệu quả bán hàng của mình!** 🚀

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/9814)**
**📌 [Hướng dẫn cài đặt n8n Self-hosted](https://docs.n8n.io/)**