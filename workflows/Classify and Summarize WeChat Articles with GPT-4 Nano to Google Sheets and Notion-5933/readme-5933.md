---
title: "🚀 Tự Động Hóa Phân Loại & Tóm Tắt Bài Đăng WeChat Sáng Tạo với GPT-4 Nano – Lưu Trữ Trên Google Sheets & Notion"
description: "Workflow tự động hóa 100% không code để phân loại, tóm tắt và lưu trữ bài đăng WeChat từ RSS feed vào Google Sheets và Notion, tiết kiệm thời gian nghiên cứu thị trường cho các sếp marketing và phân tích dữ liệu. Sử dụng GPT-4 Nano để phân loại chủ đề và tạo tóm tắt chuyên nghiệp."
slug: "tu-dong-hoa-phan-loai-tom-tat-wechat-gpt4-nano"
tags: [n8n, automation, ai-summarization, google-sheets, notion, market-research, wechat-rss]
keywords: [tự động hóa n8n, phân loại bài đăng WeChat, tóm tắt AI với GPT-4 Nano, lưu trữ Google Sheets Notion, nghiên cứu thị trường tự động]
---

# 🚀 **Tự Động Hóa Phân Loại & Tóm Tắt Bài Đăng WeChat Sáng Tạo với GPT-4 Nano**

### **Giải pháp cho các sếp marketing & nghiên cứu thị trường**
Bạn đã bao giờ phải mất **giờ đồng hồ** để đọc, phân loại và tóm tắt hàng chục bài đăng WeChat mỗi ngày? Hay phải lo lắng **bỏ sót thông tin quan trọng** vì quá tải công việc? Workflow này sẽ **tự động hóa toàn bộ quy trình** cho bạn:
- **Đọc** bài đăng từ RSS feed của WeChat.
- **Phân loại** theo chủ đề (AI, công nghệ, thị trường, cá nhân...) bằng AI.
- **Tóm tắt** nội dung chính bằng GPT-4 Nano.
- **Lưu trữ** kết quả vào **Google Sheets** (dạng bảng dữ liệu) và **Notion** (dạng trang cơ sở dữ liệu).
- **Tiết kiệm** tối thiểu **80% thời gian** so với cách làm thủ công.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Xử lý hàng trăm bài đăng chỉ trong vài phút.
✅ **Độ chính xác cao**: AI phân loại và tóm tắt với logic tự động, giảm sai sót con người.
✅ **Cá nhân hóa**: Lọc và lưu trữ bài đăng theo chủ đề quan trọng cho doanh nghiệp.
✅ **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp thủ công.
✅ **Dữ liệu sẵn sàng**: Kết quả được lưu trên **Google Sheets** (dễ dàng phân tích) và **Notion** (dễ dàng chia sẻ).
:::

---
## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài khoản & API Key**
- **Google Sheets**:
  - Tài khoản Google với quyền chỉnh sửa **1 bảng Google Sheets** (để lưu trữ danh sách link và kết quả).
  - **API Key OAuth2** của Google Sheets (cài đặt trong n8n).
- **OpenAI**:
  - **API Key** của OpenAI (để sử dụng GPT-4 Nano).
- **Notion**:
  - **API Key** của Notion (để tạo trang cơ sở dữ liệu).
- **RSS Feed**:
  - **URL của RSS feed WeChat** (của tài khoản hoặc trang bạn muốn theo dõi).

### **2. Hệ thống chạy workflow**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Bước 1: Tải workflow từ n8n.io**
- Truy cập [link workflow gốc](https://n8n.io/workflows/5933).
- Nhấn **Export** để tải file `.json`.

#### **Bước 2: Import vào n8n Editor**
- Mở **n8n Editor** (trên máy hoặc VPS).
- Nhấn **Import** và chọn file `.json` vừa tải.
- Chọn **Create new workflow** và nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **21 node**, nhưng các sếp chỉ cần chú ý đến **các node quan trọng sau**:

#### **A. Cấu hình Google Sheets**
- **Node "Read Initial Links"** và **"Read RSS Links"**:
  - Điền **ID của Google Sheet** (tìm trong URL của sheet: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  - Chọn **tab** chứa dữ liệu (ví dụ: `Sheet1`).
  - **Lưu ý**: Sheet phải có **cột "link"** (để lưu trữ URL bài đăng).

- **Node "Save Initial Data"**:
  - Chọn **tab** để lưu kết quả phân loại (ví dụ: `Relevant_Articles`).

#### **B. Cấu hình RSS Feed**
- **Node "RSS Read"**:
  - Điền **URL RSS feed** của WeChat (ví dụ: `https://mp.weixin.qq.com/cgi-bin/show?action=get_rss&lang=zh_CN&f=wx&token=...`).
  - **Lưu ý**: URL này thường nằm trong phần **RSS** của trang WeChat (nếu tài khoản có RSS feed).

#### **C. Cấu hình OpenAI (GPT-4 Nano)**
- **Node "OpenAI Chat Model1"** và **"OpenAI Chat Model"**:
  - Điền **API Key OpenAI** vào **credentials** `openAiApi`.
  - **Model**: Đã mặc định là `gpt-4.1-nano` (tiết kiệm chi phí so với GPT-4).

#### **D. Cấu hình Notion**
- **Node "Create a database page"**:
  - Điền **API Key Notion** vào `notionApi`.
  - **Database ID**: Tìm trong URL của cơ sở dữ liệu Notion (ví dụ: `https://www.notion.so/workspace/[DATABASE_ID]`).
  - **Properties**: Cần cấu hình trước trên Notion:
    - `Title` (tên bài đăng).
    - `Summary` (tóm tắt AI).
    - `Classification` (phân loại chủ đề).
    - `Link` (URL bài đăng).

#### **E. Cấu hình AI Prompt (Phân loại & Tóm tắt)**
- **Node "Relevance Classification"**:
  - **Prompt mặc định** đã được tối ưu cho phân loại bài đăng WeChat.
  - **Lưu ý**: Nếu muốn **tùy chỉnh chủ đề phân loại**, chỉnh sửa trong **stickyNote** liên quan (nếu có).

- **Node "Basic LLM Chain"**:
  - **Prompt tóm tắt** cũng đã được thiết kế cho bài đăng WeChat.
  - **Lưu ý**: Nếu muốn **tóm tắt dài hơn/ngắn hơn**, chỉnh sửa trong **code node** liên quan.

---
### **3. Kích hoạt ⚡️**
#### **Bước 1: Test Run với dữ liệu mẫu**
- Nhấn **Execute Workflow** (node `manualTrigger`).
- Kiểm tra **Google Sheets** và **Notion** để xác nhận kết quả.

#### **Bước 2: Bật Active**
- Sau khi test thành công, chuyển **status** của workflow từ **Inactive** sang **Active**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tùy chỉnh chủ đề phân loại**
- Mở **stickyNote** liên quan đến `Relevance Classification` và chỉnh sửa **danh sách chủ đề** (ví dụ: thêm "Chính trị", "Tài chính" nếu cần).

### **2. Lưu log hoạt động**
- Thêm **node `stickyNote`** sau `OpenAI Chat Model` để ghi lại **chi tiết API call** (giúp debug nếu có lỗi).

### **3. Gửi báo cáo định kỳ**
- Sử dụng **node `googleSheets`** để **tạo báo cáo tuần/monthly** từ dữ liệu đã lưu.
- **Mẹo**: Sử dụng **node `set`** để tính toán số lượng bài đăng mới mỗi tuần.

### **4. Kết hợp với Slack/Telegram**
- Thêm **node `slack`** hoặc `telegram` sau `Basic LLM Chain` để **gửi tóm tắt ngay khi có bài đăng mới**.

### **5. Lọc bài đăng theo từ khóa**
- Sử dụng **node `code`** trong `Filter Unique Links` để **lọc bài đăng chứa từ khóa cụ thể** (ví dụ: "AI", "ChatGPT").

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp marketing, nghiên cứu thị trường hoặc phân tích dữ liệu muốn:
✔ **Tự động hóa** việc theo dõi bài đăng WeChat.
✔ **Phân loại & tóm tắt** nội dung bằng AI.
✔ **Lưu trữ** kết quả trên **Google Sheets** (dễ dàng phân tích) và **Notion** (dễ dàng chia sẻ).

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và **cấu hình credentials**.
3. **Bật Active** và bắt đầu **tự động hóa nghiên cứu thị trường** của mình!

---
### **🔗 Tài liệu tham khảo**
- [Workflow gốc trên n8n.io](https://n8n.io/workflows/5933)
- [Hướng dẫn cài đặt n8n Self-hosted](https://docs.n8n.io/hosting/installation/)
- [Cách lấy API Key Notion](https://www.notion.so/my-integrations)