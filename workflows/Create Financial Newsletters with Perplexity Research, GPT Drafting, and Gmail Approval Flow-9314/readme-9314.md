---
title: "📊 Tự Động Hoàn Chế Báo Cáo Tài Chính với AI Perplexity, GPT & Gmail (Không Cần Code)"
description: "Workflow tự động hóa tạo báo cáo tài chính chuyên nghiệp với AI nghiên cứu tin tức, viết bản thảo bằng GPT-4, và hệ thống phê duyệt qua Gmail - tiết kiệm 10+ giờ/tháng cho các sếp tài chính."
slug: "tieu-dong-hoan-che-bao-cao-tai-chinh-ai-gmail"
tags: [n8n, automation, content-creation, ai-multimodal, gmail-integration]
keywords: [n8n workflow tài chính, tự động hóa báo cáo AI, GPT-4 viết báo cáo, phê duyệt email tự động, Perplexity API]
---

# 🚀 **Tự Động Hoàn Chế Báo Cáo Tài Chính với AI Perplexity, GPT & Gmail**

### **Giải Phóng Tay Các Sếp Tài Chính: Từ Viết Báo Cáo 10+ Giờ Sang 5 Phút/Ngày**
Hiện nay, việc biên soạn báo cáo tài chính hàng tuần vẫn là một công việc **mệt mỏi, tốn thời gian** và dễ mắc lỗi của nhiều sếp tài chính. Các sếp phải:
- **Tìm kiếm tin tức thị trường** từ nhiều nguồn khác nhau (Bloomberg, Reuters, các báo chuyên ngành).
- **Viết bản thảo** với cấu trúc chuyên nghiệp, tránh sai sót pháp lý và ngôn ngữ hấp dẫn.
- **Phê duyệt nội dung** qua email, dễ bị quên hoặc mất thời gian chờ đợi phản hồi.
- **Đảm bảo nhất quán** về phong cách và branding cho từng khách hàng.

**Workflow này tự động hóa toàn bộ quy trình** bằng cách kết hợp:
✅ **AI Perplexity** để nghiên cứu tin tức thị trường tự động.
✅ **GPT-4 (OpenAI)** để viết bản thảo chuyên nghiệp và xây dựng HTML.
✅ **Gmail** để phê duyệt và gửi báo cáo cuối cùng.
✅ **Webhook** để quản lý quy trình phê duyệt linh hoạt.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10+ giờ/tháng**: Không còn phải viết báo cáo từ đầu.
- **Chất lượng chuyên nghiệp**: AI đảm bảo cấu trúc, ngữ pháp và phong cách nhất quán.
- **Phê duyệt tự động**: Hệ thống gửi báo cáo đến email của sếp để phê duyệt mà không mất thời gian chờ đợi.
- **Hoạt động 24/7**: Báo cáo được tự động gửi vào thời gian đã đặt (ví dụ: thứ 5 sáng 8h).
- **Dễ dàng tùy chỉnh**: Thay đổi phong cách, branding hoặc nội dung theo yêu cầu của khách hàng.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐẶT**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail/Google Workspace**:
   - Đăng ký **OAuth2 Credentials** cho Gmail (để gửi preview và bản cuối cùng).
   - Đăng ký **API Key** cho [Perplexity AI](https://www.perplexity.ai/) (miễn phí cho 3000 credit/tháng).
   - Đăng ký **API Key** cho [OpenAI](https://platform.openai.com/) (để sử dụng GPT-4).

2. **Thông tin branding**:
   - Tên công ty, liên hệ, website (để thêm vào footer báo cáo).
   - Mẫu chữ ký (signature_html) với tên và logo của công ty.

3. **Thông tin n8n**:
   - **Domain n8n Cloud** hoặc **self-hosted domain** (để thay thế `[YOURDOMAIN]` trong workflow).
   - **Mã API Webhook** (nếu tự host, cần cấu hình domain và SSL).

4. **Thông tin đăng ký**:
   - Danh sách email **test/distribution list** (để gửi preview trước khi phê duyệt).
   - Thời gian tự động gửi báo cáo (ví dụ: **thứ 5 hàng tuần, 8h sáng**).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/9314](https://n8n.io/workflows/9314) và import vào **n8n Editor**.
- **Copy/Paste JSON** từ file vào **Import Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- **Không** sử dụng workflow gốc mà phải **tùy chỉnh** theo hướng dẫn dưới đây.
- **Không** quên thay thế `[YOURDOMAIN]` bằng domain thực của n8n.
:::

---

### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**

#### **A. Cấu Hình API & Credentials**
| **Node**               | **Tham Số Cần Thay Đổi**                          | **Hướng Dẫn**                                                                 |
|------------------------|--------------------------------------------------|-------------------------------------------------------------------------------|
| **Research LLM**        | `perplexityApi` (API Key)                        | Thay thế bằng API Key từ [Perplexity](https://www.perplexity.ai/api).         |
| **QC LLM / HTML Builder** | `openAiApi` (API Key)                          | Thay thế bằng API Key từ [OpenAI](https://platform.openai.com/).              |
| **Editor LLM**          | `openAiApi` (API Key)                            | Cùng API Key với node trên.                                                   |
| **Send Preview**        | `sendTo` (email test/distribution list)          | Thay thế bằng email của mình hoặc nhóm test.                                  |
| **Create Final Draft**  | `gmailOAuth2` (credentials)                       | Cấu hình OAuth2 cho Gmail/Google Workspace.                                    |

#### **B. Tùy Chỉnh Nội Dung & Branding**
1. **Thay thế `[YOURDOMAIN]`**:
   - Trong node **Schedule Trigger** và **Approval Webhook (GET)**, thay thế:
     ```json
     "https://[YOURDOMAIN]/newsletter-approval"
     ```
     bằng domain n8n của mình (ví dụ: `https://tinon8n.com/newsletter-approval`).

2. **Cập Nhật thông tin công ty**:
   - Trong node **Enrich for Editorial**, thay đổi:
     ```json
     "firm_name": "Company Name",
     "contact_url": "contact@example.com",
     "view_url": "https://website/${runKey}"
     ```
     bằng tên công ty và website thực tế.

3. **Thay đổi prompt AI**:
   - Trong node **Editor LLM** và **HTML Builder LLM**, các sếp có thể **tùy chỉnh hệ thống prompt** để phù hợp với:
     - **Phong cách ngôn ngữ** (chuyên nghiệp, thân thiện, kỹ thuật).
     - **Branding** (màu sắc, font, cấu trúc bảng).
     - **Quy tắc QC** (ví dụ: kiểm tra ngôn ngữ hứa hẹn, phân bổ rủi ro).

4. **Đặt lịch gửi báo cáo**:
   - Trong node **Schedule Trigger**, thay đổi:
     ```json
     "interval": "weekly",
     "triggerAtHour": 8
     ```
     để phù hợp với thời gian muốn gửi (ví dụ: `triggerAtHour: 16` để gửi vào 4h chiều).

#### **C. Cấu Hình Webhook Phê Duyệt**
- **Approval Submit (POST)**: Sử dụng URL webhook này để gửi yêu cầu phê duyệt từ bên ngoài (nếu cần).
- **Approval Webhook (GET)**: Cấu hình để nhận phản hồi phê duyệt từ email Gmail.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Chạy **manual execution** với dữ liệu mẫu để kiểm tra:
     - AI có nghiên cứu tin tức không?
     - Bản thảo có hợp lý không?
     - Email preview có gửi được không?

2. **Bật Active**:
   - Sau khi kiểm tra xong, **bật Active** và chờ workflow chạy tự động theo lịch.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối Slack/Telegram để Báo Lỗi**
- Thêm node **Slack/Telegram** sau **Send Preview** để nhận thông báo khi có lỗi:
  ```json
  {
    "name": "Notify Slack on Error",
    "type": "slack",
    "credentials": ["slackApi"]
  }
  ```

### **2. Lưu Log Tất Cả Các Lần Chạy**
- Thêm node **Google Sheets** hoặc **Airtable** để ghi lại:
  - Ngày giờ chạy.
  - Tình trạng (thành công/thất bại).
  - Link preview.

### **3. Gửi Báo Cáo Định Kỳ cho Khách Hàng**
- Thay vì gửi preview cho mình, **gửi trực tiếp cho khách hàng** bằng cách:
  - Thay đổi `sendTo` trong **Send Preview** thành email khách hàng.
  - Thêm bước **phê duyệt qua Slack** (nếu khách hàng yêu cầu).

### **4. Tùy Chỉnh Cấu Trúc HTML**
- Trong node **HTML Builder LLM**, các sếp có thể **định hình cấu trúc HTML** rõ ràng hơn bằng cách:
  ```json
  "prompt": "Tạo một bản báo cáo HTML với cấu trúc sau:
  - Header: Tiêu đề + logo công ty.
  - Section 1: Tin tức thị trường (dưới dạng bảng).
  - Section 2: Phân tích (dạng văn bản).
  - Footer: Chữ ký + liên hệ."
  ```

### **5. Sử Dụng AI để Chỉnh Sửa Bản Cuối Cùng**
- Thêm node **OpenAI** sau **Merge Revision Notes** để AI **chỉnh sửa lại bản cuối cùng** trước khi gửi:
  ```json
  {
    "name": "Final Polish by AI",
    "type": "openAi",
    "credentials": ["openAiApi"],
    "operation": "edit"
  }
  ```

---
## 📌 **Kết Luận: Đừng Chờ Đợi, Tự Động Hóa Ngay!**
Workflow này **giải phóng thời gian** cho các sếp tài chính để tập trung vào **strategy và phân tích** thay vì việc viết báo cáo thủ công. Với **AI Perplexity và GPT-4**, báo cáo không chỉ nhanh mà còn **chuyên nghiệp, chính xác và cá nhân hóa**.

**Hành động ngay:**
1. **Tùy chỉnh workflow** theo hướng dẫn trên.
2. **Test với dữ liệu mẫu** trước khi bật chế độ tự động.
3. **Đăng ký VPS n8n** để lưu trữ workflow 24/7 (không phụ thuộc vào n8n Cloud).

:::success[**Bắt Đầu Tự Động Hóa Hôm Nay!**]
- [Đăng ký VPS TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)
- [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Câu hỏi?** Để lại comment bên dưới hoặc liên hệ với team n8n để hỗ trợ! 🚀