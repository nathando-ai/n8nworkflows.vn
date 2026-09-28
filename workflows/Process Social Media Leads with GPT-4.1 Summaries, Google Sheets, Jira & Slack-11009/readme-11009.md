---
title: "🚀 Tự Động Hóa & Tóm Tắt Lead Tiềm Năng Từ Mạng Xã Hội Với GPT-4.1, Google Sheets, Jira & Slack (N8N)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp thu thập, phân loại, tóm tắt và theo dõi lead từ mạng xã hội, website hoặc tin nhắn DM bằng trí tuệ nhân tạo (GPT-4.1), lưu trữ trên Google Sheets, tạo task tự động trên Jira và báo cáo định kỳ qua Slack. Giúp tiết kiệm thời gian lên đến 80% trong quản lý lead."
slug: "tu-dong-hoa-lead-social-media-gpt4-1-n8n"
tags: [n8n, automation, lead-generation, ai-summarization, google-sheets, jira, slack, openai, no-code]
keywords: [n8n workflow lead social media, tự động hóa lead từ mạng xã hội, GPT-4.1 tóm tắt lead, quản lý lead Jira Slack, tự động hóa không code, n8n self-hosted]
---

# 🚀 **Tự Động Hóa Lead Từ Mạng Xã Hội: Từ DM Đến Task Jira, Báo Cáo Slack Với GPT-4.1**

Hiện nay, việc thu thập và theo dõi lead từ mạng xã hội, website hoặc tin nhắn riêng tư (DM) là một trong những công việc tốn thời gian nhất của các sếp marketing và sales. Thường thì các sếp phải:
- **Lọc thủ công** hàng trăm tin nhắn mỗi ngày để tìm lead có giá trị.
- **Ghi chép lại** thông tin lead vào Google Sheets hoặc Excel, dễ bị lỗi và mất thời gian.
- **Tạo task theo dõi** trên Jira hoặc Trello một cách thủ công, dẫn đến trễ hạn hoặc quên follow-up.
- **Báo cáo định kỳ** cho team hoặc lãnh đạo bằng cách tổng hợp dữ liệu từ nhiều nguồn khác nhau.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động thu thập** lead từ DM, website hoặc bot mạng xã hội.
✅ **Phân loại và tóm tắt** lead bằng GPT-4.1 (OpenAI) để rút gọn thông tin quan trọng.
✅ **Lưu trữ tự động** vào Google Sheets với định dạng chuẩn.
✅ **Tạo task Jira** để team sales/follow-up xử lý kịp thời.
✅ **Báo cáo định kỳ** (hàng ngày/tuần) qua Slack với dữ liệu tổng hợp.
✅ **Lọc lead theo chủ đề** (quảng cáo, hợp tác, đề xuất sản phẩm...) để tập trung vào lead có giá trị.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian** trong việc thu thập và xử lý lead thủ công.
- **Chính xác 100%** với AI tóm tắt và phân loại lead theo chủ đề.
- **Theo dõi lead tự động** trên Jira, không còn quên hoặc trễ hạn.
- **Báo cáo tự động** hàng tuần qua Slack, giúp team cập nhật nhanh chóng.
- **Lưu trữ dữ liệu an toàn** trên Google Sheets với định dạng chuẩn.
- **Cá nhân hóa** thông báo Slack và task Jira theo từng lead.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản và API Key**:
   - **OpenAI API Key** (để sử dụng GPT-4.1 tóm tắt lead).
   - **Google Sheets OAuth 2.0 API Key** (để lưu lead).
   - **Jira Cloud API Key** (để tạo task tự động).
   - **Slack API Token** (để gửi thông báo và báo cáo).
   - **Webhook URL** (để nhận lead từ DM, website hoặc bot mạng xã hội).

2. **Dịch vụ và công cụ**:
   - **Google Sheet** (để lưu trữ lead, tên sheet phải phù hợp với cấu trúc trong workflow).
   - **Jira Project** (đã cấu hình các trường như *Summary*, *Description*, *Assignee*).
   - **Slack Channel** (để nhận thông báo và báo cáo).
   - **n8n Self-hosted** (để workflow chạy 24/7, không phụ thuộc vào phiên bản cloud).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io/workflows/11009](https://n8n.io/workflows/11009) và nhấn **"Import Workflow"**.
2. Hoặc tải file JSON và import vào n8n Editor.
3. Sau khi import, workflow sẽ hiển thị trên canvas với 12 node.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Dưới đây là danh sách các node quan trọng cần cấu hình:

#### **🔹 Node "Get DM" (Webhook)**
- **Cấu hình Webhook**:
  - **Path**: `marketing-lead` (không thay đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Không cần, nhưng các sếp phải đảm bảo Webhook nhận được dữ liệu từ DM hoặc website.
  - **Lưu ý**: Nếu sử dụng bot mạng xã hội (Facebook, Instagram, Telegram...), các sếp phải cấu hình Webhook để gửi dữ liệu đến URL này.

#### **🔹 Node "AI Lead Classifier" (OpenAI)**
- **Cấu hình OpenAI**:
  - **API Key**: Điền vào `openAiApi` (tạo trong n8n Credentials).
  - **Model**: Sử dụng `gpt-4-1106-preview` (hoặc phiên bản mới nhất).
  - **Prompt**: Workflow đã cấu hình sẵn prompt để phân loại lead. Các sếp có thể chỉnh sửa trong node **"AI Output Parser"** (node Code) nếu cần.
  - **Lưu ý**: Đảm bảo tài khoản OpenAI có đủ credit để chạy AI.

#### **🔹 Node "Store Lead" (Google Sheets)**
- **Cấu hình Google Sheets**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trong n8n).
  - **Sheet Name**: Đảm bảo tên sheet phù hợp với cấu trúc trong workflow (ví dụ: `Lead_Management`).
  - **Operation**: `append` (thêm mới lead vào sheet).
  - **Lưu ý**: Các sếp phải tạo sheet mới hoặc đảm bảo sheet đã có các cột: `Date`, `Lead Text`, `Summary`, `Lead Type`, `Source`, `Assignee`, `Status`.

#### **🔹 Node "Create Task" (Jira)**
- **Cấu hình Jira**:
  - **Credentials**: Chọn `jiraSoftwareCloudApi`.
  - **Project Key**: Điền vào trường `projectKey` (ví dụ: `MKT`).
  - **Issue Type**: Chọn `Task` (hoặc `Story` tùy thuộc vào cấu trúc Jira).
  - **Fields**:
    - `summary`: Sử dụng thông tin tóm tắt từ AI.
    - `description`: Sử dụng lead nguyên bản.
    - `assignee`: Chọn thành viên team (ví dụ: `sales-team`).
  - **Lưu ý**: Các sếp phải kiểm tra cấu trúc trường trong Jira để đảm bảo khớp với workflow.

#### **🔹 Node "Weekly lead Filter" & "Report Data Formatter" (Code)**
- **Cấu hình tự động**:
  - Node này sử dụng JavaScript để lọc lead theo tuần và tính toán dữ liệu báo cáo.
  - **Không cần chỉnh sửa** nếu các sếp muốn sử dụng cấu trúc mặc định.
  - **Lưu ý**: Đảm bảo Google Sheet có dữ liệu đủ để lọc (ít nhất 1 tuần).

#### **🔹 Node "Send a Summary" & "Weekly Report Slack" (Slack)**
- **Cấu hình Slack**:
  - **Credentials**: Chọn `slackApi`.
  - **Channel**: Chọn channel muốn nhận thông báo (ví dụ: `#marketing-leads`).
  - **Message Format**: Workflow đã cấu hình sẵn template. Các sếp có thể chỉnh sửa trong node Code nếu cần.
  - **Lưu ý**: Đảm bảo Slack API Token có quyền gửi tin nhắn vào channel.

#### **🔹 Node "Schedule Trigger"**
- **Cấu hình lịch trình**:
  - **Daily Trigger**: 00:00 (giờ sáng) để tổng hợp lead hàng ngày.
  - **Weekly Trigger**: Chủ nhật 00:00 để gửi báo cáo tuần.
  - **Lưu ý**: Các sếp có thể điều chỉnh thời gian theo nhu cầu.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Gửi một tin nhắn mẫu đến Webhook (node `Get DM`) để kiểm tra workflow.
   - Kiểm tra:
     - Lead có được tóm tắt bởi AI không?
     - Task có được tạo trên Jira không?
     - Lead có được lưu vào Google Sheets không?
     - Thông báo Slack có được gửi không?

2. **Bật Active**:
   - Sau khi test thành công, các sếp bật **Active** cho workflow.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy Chỉnh Keyword Filter**:
   - Node `Lead Keyword Filter` (Code) có thể được chỉnh sửa để lọc lead theo chủ đề cụ thể (ví dụ: "quảng cáo", "hợp tác", "đề xuất sản phẩm").
   - Các sếp có thể mở node Code và chỉnh sửa mảng `keywords` để phù hợp với chiến dịch marketing.

2. **Gửi Báo Cáo Định Kỳ Qua Email**:
   - Thêm node **Email** (ví dụ: `n8n-nodes-base.email`) sau node `Weekly Report Slack` để gửi báo cáo tuần cho team hoặc lãnh đạo.

3. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Drive** hoặc **AWS S3** để lưu bản sao dữ liệu lead để backup.

4. **Kết Hợp Với CRM**:
   - Nếu sử dụng CRM như HubSpot hoặc Salesforce, các sếp có thể thêm node tương ứng để tự động đồng bộ lead.

5. **Tự Động Phân Loại Lead Theo Nguồn**:
   - Chỉnh sửa node `Lead Keyword Filter` để phân loại lead theo nguồn (Facebook, Instagram, Website...) và gửi đến team phù hợp.

---
## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** để tự động hóa quy trình quản lý lead từ mạng xã hội, website hoặc DM, giúp các sếp:
✔ **Tiết kiệm thời gian** lên đến 80% trong việc thu thập và xử lý lead.
✔ **Tăng cường hiệu quả** với AI tóm tắt và phân loại lead.
✔ **Theo dõi lead một cách tự động** trên Jira và Slack.
✔ **Cập nhật team** với báo cáo định kỳ qua Slack.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7.
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Test và bật Active** để tự động hóa quản lý lead của mình.

👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/11009) và bắt đầu tự động hóa ngay!