---
title: "🤖 **Tự Động Hóa Agent IT Support AI với Azure Search, Entra ID & Jira – Giải Pháp Hỗ Trợ Kỹ Thuật 24/7 Miễn Code**"
description: "Workflow này tự động hóa việc tạo ticket hỗ trợ IT thông minh bằng AI, kết hợp Azure Search để tìm kiếm thông tin kỹ thuật nhanh chóng, Entra ID để quản lý người dùng và Jira để theo dõi vấn đề. Giúp các sếp tiết kiệm thời gian lên tới 80% trong việc giải quyết ticket hỗ trợ kỹ thuật."
slug: "tay-dong-hoa-agent-it-support-ai-azure-search-jira"
tags: [n8n, automation, ai, azure-search, jira, support-it, no-code, azure-entra-id, langchain]
keywords: [n8n workflow hỗ trợ IT, tự động hóa ticket Jira bằng AI, Azure Search cho hỗ trợ kỹ thuật, giải pháp hỗ trợ 24/7, LangChain với n8n, tự động hóa Azure Entra ID]
---

# 🚀 **Tạo Agent Hỗ Trợ IT AI Tự Động Hóa với Azure Search, Entra ID & Jira**

## **🔍 Nỗi Đau Của Các Sếp Hiện Nay**
Hỗ trợ kỹ thuật là một trong những công việc **mệt mỏi và tốn thời gian** nhất trong doanh nghiệp. Các sếp thường phải:
- **Tra cứu thông tin kỹ thuật** qua email, wiki hoặc tài liệu nội bộ mất nhiều thời gian.
- **Tạo ticket Jira thủ công**, dễ bị lỗi hoặc thiếu thông tin quan trọng.
- **Phản hồi người dùng chậm**, dẫn đến trải nghiệm tệ và mất khách hàng.
- **Quản lý người dùng và mật khẩu** qua Entra ID (cũ là Azure AD) phức tạp, dễ xảy ra lỗi.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động tạo ticket Jira** từ tin nhắn người dùng với thông tin chi tiết.
✅ **Tìm kiếm thông tin kỹ thuật bằng AI** (Azure Search + LangChain) trong thời gian thực.
✅ **Quản lý người dùng và mật khẩu** thông qua Entra ID (Azure AD) một cách an toàn.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian** trong việc xử lý ticket hỗ trợ kỹ thuật.
- **Giải quyết vấn đề nhanh chóng** với AI tìm kiếm thông tin chính xác từ Azure Search.
- **Tự động tạo ticket Jira** với thông tin đầy đủ, giảm lỗi và mất mát.
- **Quản lý người dùng và mật khẩu** một cách an toàn thông qua Entra ID.
- **Hoạt động liên tục** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Azure** (để tạo Azure AI Search và Entra ID).
2. **API Key của Azure AI Search** (để tạo và quản lý vector store).
3. **Tài khoản Jira Cloud** (để tạo ticket tự động).
4. **API Key của Jira** (để kết nối với n8n).
5. **Tài khoản Google Cloud** (để sử dụng Gemini AI).
6. **Tài khoản OpenAI** (nếu sử dụng embeddings từ OpenAI).
7. **Dữ liệu kỹ thuật** (tài liệu, wiki, FAQ) để upload vào Azure Search.
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/4560](https://n8n.io/workflows/4560) (hoặc copy JSON từ đây).
2. **Mở n8n Editor** và nhấn **"Import"** → **"From JSON"**.
3. **Dán JSON** và nhấn **"Import"**.

#### **Cách 2: Copy/Paste JSON**
1. **Mở n8n Editor** → **"Create New Workflow"**.
2. **Nhấn "Import"** → **"From JSON"** → **Dán JSON** → **"Import"**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 1. Cấu Hình Azure AI Search**
Workflow cần **tạo và cấu hình Azure AI Search Index** trước khi hoạt động.
- **Bước 1:** Tạo **Azure AI Search Service** trong Azure Portal.
- **Bước 2:** Tạo **Vector Index** để lưu embeddings.
- **Bước 3:** Lấy **Admin Key** của Azure AI Search và điền vào:
  - Node **"Get Azure AI Search Admin Key"**
  - Node **"Get Azure AI Search Admin Key1"**
  - Node **"Get Azure AI Search Admin Key2"**

#### **🔹 2. Cấu Hình Jira**
- **Tạo credential Jira** trong n8n:
  - **Tên credential:** `jiraSoftwareCloudApi`
  - **URL:** `https://[your-domain].atlassian.net`
  - **Email & API Token:** Lấy từ tài khoản Jira của bạn.
- **Kiểm tra node "Create Jira Ticket"** để đảm bảo thông tin ticket được tạo chính xác.

#### **🔹 3. Cấu Hình Azure Entra ID (Azure AD)**
- **Tạo credential OAuth2** trong n8n:
  - **Tên credential:** `microsoftOAuth2Api`
  - **Client ID & Secret:** Lấy từ **Azure Portal → App Registrations**.
- **Kiểm tra node "Query Microsoft Entra ID Users"** và **"Reset User Password"** để đảm bảo quyền truy cập.

#### **🔹 4. Cấu Hình Google Gemini AI**
- **Tạo credential Google Palm API** trong n8n:
  - **Tên credential:** `googlePalmApi`
  - **API Key:** Lấy từ [Google Cloud Console](https://console.cloud.google.com/).
- **Kiểm tra node "Google Gemini Chat Model"** để đảm bảo AI trả lời chính xác.

#### **🔹 5. Cấu Hình Embeddings (OpenAI)**
- **Tạo credential OpenAI** trong n8n:
  - **Tên credential:** `openAiApi`
  - **API Key:** Lấy từ [OpenAI Dashboard](https://platform.openai.com/account/api-keys).
- **Kiểm tra node "Get Embeddings"** và **"Get Embeddings1"** để đảm bảo embeddings được tạo đúng.

#### **🔹 6. Upload Dữ liệu Kỹ Thuật vào Azure Search**
- **Sử dụng node "On Knowledge Upload"** để upload tài liệu (PDF, DOCX, TXT) vào Azure Search.
- **Node "Prep Content"** sẽ xử lý và tạo embeddings trước khi upload.

#### **🔹 7. Cấu Hình Webhook cho Semantic Search**
- **Node "Semantic Search"** sử dụng **Webhook Key** để nhận tin nhắn từ người dùng.
- **Cần cấu hình URL Webhook** trong Azure Search để liên kết với n8n.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Gửi một tin nhắn mẫu (ví dụ: *"Tôi quên mật khẩu Azure AD"*) đến Webhook.
   - Kiểm tra workflow có tạo ticket Jira và trả lời AI không.
2. **Bật Active workflow**:
   - Nhấn **"Active"** trên tab workflow.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 1. Kết Nối với Slack/Telegram**
- **Sử dụng node "Slack" hoặc "Telegram Bot"** để thông báo ticket mới cho team.
- **Cấu hình Webhook Slack/Telegram** trong node **"Set Common Fields"** để gửi thông báo tự động.

### **🔹 2. Lưu Log & Báo Cáo**
- **Sử dụng node "Set" + "Code"** để lưu lịch sử ticket vào **Google Sheets** hoặc **Azure Blob Storage**.
- **Tạo báo cáo định kỳ** (hàng ngày/tuần) về số lượng ticket, thời gian giải quyết, và vấn đề phổ biến.

### **🔹 3. Cải Thiện Trải Nghiệm Người Dùng**
- **Thêm node "Email"** để gửi thông báo kết quả giải quyết ticket cho người dùng.
- **Sử dụng "Sticky Note"** để ghi chú nội bộ cho team hỗ trợ.

### **🔹 4. Tích Hợp với Microsoft Teams**
- **Sử dụng node "Microsoft Teams"** để thông báo ticket mới trong kênh #support.

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc hỗ trợ kỹ thuật mệt mỏi, đồng thời **tăng cường hiệu suất** với AI và tự động hóa. **Bắt đầu sử dụng ngay** và xem cách nó **cải thiện trải nghiệm người dùng** và **giảm tải cho team IT** của bạn!

:::success[**Hành Động Tiếp Theo**]
1. **Cài đặt n8n Self-hosted** trên VPS để workflow hoạt động 24/7.
2. **Tạo Azure AI Search Index** và upload dữ liệu kỹ thuật.
3. **Kết nối Jira, Entra ID và Google Gemini**.
4. **Test workflow** và bật hoạt động!
:::

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---
**Chúc các sếp thành công với workflow tự động hóa hỗ trợ IT AI này!** 🚀