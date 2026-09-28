---
title: "🚀 Tự Động Hóa Tạo Nội Dung AI Cho LinkedIn & Facebook: Từ Khái Niệm Đến Đăng Bài - Không Cần Code!"
description: "Workflow này tự động tạo nội dung AI chuyên nghiệp, 4 biến thể hình ảnh độc đáo, và lên lịch đăng bài trên LinkedIn & Facebook với sự phê duyệt người dùng. Giúp các sếp tiết kiệm 10+ giờ/ngày và tăng engagement 300%!"
slug: "tieu-dong-hoa-tao-noi-dung-ai-cho-linkedin-facebook"
tags: [n8n, automation, no-code, ai-content-generation, social-media-marketing, google-drive, slack-integration]
keywords: [n8n workflow tự động hóa nội dung AI, tạo bài viết LinkedIn Facebook bằng AI, tự động hóa marketing social media, AI tạo hình ảnh và văn bản, phê duyệt nội dung tự động]
---

# 🚀 **Tự Động Hóa Tạo Nội Dung AI Chuyên Nghiệp Cho LinkedIn & Facebook**

### **Giải Phóng Thời Gian Của Các Sếp Với Nội Dung AI Tự Động, Hình Ảnh Đa Dạng & Phê Duyệt Người Dùng**

Hiện nay, việc tạo nội dung cho LinkedIn và Facebook là một công việc **mệt mỏi, tốn thời gian** và thường phụ thuộc vào sự sáng tạo cá nhân. Các sếp phải:
- **Tìm kiếm ý tưởng** cho mỗi bài viết
- **Tạo hình ảnh** phù hợp (hoặc mua từ bên ngoài)
- **Chỉnh sửa lại** nếu nội dung không phù hợp
- **Lên lịch đăng bài** theo chiến lược
- **Phê duyệt** trước khi đăng

**Workflow này giải quyết tất cả vấn đề trên bằng AI!** Nó tự động:
✅ **Tạo nội dung AI** phù hợp với brand của bạn (văn bản + hình ảnh)
✅ **Sinh ra 4 biến thể hình ảnh** khác nhau (ảnh thực, infographic, 3D, minh họa)
✅ **Lên lịch đăng bài** trên LinkedIn & Facebook
✅ **Yêu cầu phê duyệt** từ người dùng trước khi đăng
✅ **Tự động chỉnh sửa hình ảnh** theo feedback
✅ **Lưu tất cả dữ liệu** vào Google Sheets cho theo dõi

---
## 🎯 **Kết Quả Các Sếp Nhận Được**

:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10+ giờ/ngày** cho việc tạo nội dung thủ công
- **Nội dung chuyên nghiệp** phù hợp với brand, không cần viết code
- **4 biến thể hình ảnh** tăng cơ hội engagement
- **Phê duyệt AI + người dùng** đảm bảo chất lượng cao
- **Lên lịch tự động** trên LinkedIn & Facebook
- **Dữ liệu theo dõi** trong Google Sheets (tất cả bài viết, feedback, lịch đăng)
:::

---
## 🔧 **Yêu Cầu Cần Thiết**

:::info[**Chuẩn Bị Trước Khi Lên Đồ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| Dịch Vụ / API | Mô Tả | Làm Thế Nào Để Lấy |
|--------------|--------|---------------------|
| **OpenRouter API** | Dùng để gọi mô hình AI (gpt-5-mini) | [Đăng ký tại OpenRouter](https://openrouter.ai/) |
| **Perplexity API** | Dùng cho nghiên cứu trend & tư vấn AI | [Đăng ký tại Perplexity](https://www.perplexity.ai/api) |
| **Google Sheets API** | Lưu trữ dữ liệu bài viết & feedback | [Bật OAuth 2.0 cho Google Sheets](https://developers.google.com/sheets/api/quickstart/python) |
| **Google Drive API** | Upload hình ảnh & file | [Bật OAuth 2.0 cho Google Drive](https://developers.google.com/drive/api/v3/quickstart/python) |
| **Slack API** | Gửi thông báo & yêu cầu phê duyệt | [Tạo App Slack](https://api.slack.com/apps) |
| **Late API (Facebook/Instagram & LinkedIn)** | Lên lịch đăng bài | [Đăng ký tại Late](https://late.app/) (sử dụng API Key) |
| **NanoBanana API** | Chỉnh sửa hình ảnh theo feedback | [Đăng ký tại NanoBanana](https://nanobanana.com/) |
| **HTTP Header Auth** | Đối với các request API riêng | (Nếu cần, tạo từ các dịch vụ như Postman) |

### **2. Tham Số Brand Cần Điền**
Workflow yêu cầu các sếp **điền các biến brand** sau vào **Sticky Note** (node `Edit Fields`):
```yaml
BRAND_NAME: "Tên Brand của bạn (ví dụ: 'VinaPhone')"
INDUSTRY: "Ngành nghề (ví dụ: 'Điện thoại di động')"
TARGET_DEMOGRAPHICS: "Đối tượng mục tiêu (ví dụ: 'Nam giới 25-35 tuổi')"
TARGET_LOCATION: "Địa bàn mục tiêu (ví dụ: 'Việt Nam')"
PRIMARY_VALUE_PROPOSITION: "Lợi ích chính của sản phẩm (ví dụ: 'Điện thoại 5G giá rẻ')"
CUSTOMER_CHALLENGE: "Vấn đề khách hàng gặp phải (ví dụ: 'Mất pin nhanh')"
DESIRED_OUTCOME: "Kết quả mong muốn (ví dụ: 'Tăng doanh số 20%')"
BRAND_VOICE: "Tôn chỉ brand (ví dụ: 'Chuyên nghiệp, thân thiện')"
```

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương Pháp 1: Import từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/8398](https://n8n.io/workflows/8398) (chọn **Export as JSON**).
2. **Mở n8n Editor** trên máy chủ của bạn.
3. Nhấn **Import** → Chọn file JSON vừa tải.
4. **Xác nhận import** và workflow sẽ hiện lên canvas.

#### **Phương Pháp 2: Copy/Paste JSON**
1. **Tải file JSON** từ link trên.
2. **Mở n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
3. **Dán toàn bộ nội dung JSON** vào ô và nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials (API Keys)**
Các node quan trọng cần **cấu hình credentials** như sau:

| **Node** | **Credentials Cần Thiết** | **Hướng Dẫn Cấu Hình** |
|----------|--------------------------|------------------------|
| **OpenRouter Chat Model2/3** | `openRouterApi` | Điền `API Key` từ OpenRouter vào **Credentials Manager** của n8n. |
| **Perplexity Tool** | `perplexityApi` | Điền `API Key` từ Perplexity. |
| **Google Sheets** | `googleSheetsOAuth2Api` | Tạo OAuth 2.0 cho Google Sheets và chọn **Google Sheets API**. |
| **Google Drive** | `googleDriveOAuth2Api` | Tạo OAuth 2.0 cho Google Drive và chọn **Google Drive API**. |
| **Slack** | `slackOAuth2Api` | Tạo OAuth Token từ Slack App và chọn **Bot Token**. |
| **Late API (Facebook/Instagram & LinkedIn)** | `httpHeaderAuth` | Điền `API Key` từ Late và cấu hình header `Authorization: Bearer <API_KEY>`. |
| **NanoBanana** | `httpHeaderAuth` | Điền `API Key` từ NanoBanana và cấu hình header tương tự. |

#### **B. Cấu Hình Node Quan Trọng**
1. **Node `Edit Fields` (Set)**
   - Điền **tất cả biến brand** vào `json` như trong phần **Yêu cầu cần thiết** trên.
   - Ví dụ:
     ```json
     {
       "BRAND_NAME": "VinaPhone",
       "INDUSTRY": "Điện thoại di động",
       "TARGET_DEMOGRAPHICS": "Nam giới 25-35 tuổi",
       ...
     }
     ```

2. **Node `AI Agent2` (LangChain Agent)**
   - **Không cần cấu hình thêm**, workflow đã tự động cấu hình prompt cho AI.

3. **Node `OpenRouter Chat Model2/3`**
   - **Model mặc định**: `openai/gpt-5-mini` (không cần thay đổi).

4. **Node `Slack` (Send message and wait for response)**
   - **Channel**: Chọn channel Slack muốn gửi thông báo (ví dụ: `#content-approval`).
   - **Message Template**: Workflow đã tự động cấu hình, **không cần chỉnh sửa**.

5. **Node `Google Sheets` (Append or update row)**
   - **Sheet Name**: Điền tên sheet (ví dụ: `Social Media Content`).
   - **Range**: `A1` (để lưu dữ liệu từ đầu hàng A).

6. **Node `Late API` (Schedule Post)**
   - **Account ID**: Thay thế `accountId` trong header bằng **Account ID của bạn** từ Late.
   - **Example**:
     ```json
     {
       "accountId": "YOUR_LATE_ACCOUNT_ID",
       "postId": "{{$node["Image Generation"].json.postId}}"
     }
     ```

7. **Node `NanoBanana` (Edit Image)**
   - **API Endpoint**: Điền URL API của NanoBanana (ví dụ: `https://api.nanobanana.com/v1/edit`).
   - **Header Auth**: Điền `Authorization: Bearer <API_KEY>`.

8. **Node `Switch` (Merge Image Paths)**
   - **Condition**: Workflow đã cấu hình tự động, **không cần chỉnh sửa**.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với Dữ liệu Mẫu**
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - **Điền dữ liệu mẫu** vào node `On form submission` (nếu có).
   - Kiểm tra:
     - AI có tạo nội dung không?
     - Hình ảnh có sinh ra không?
     - Slack có gửi yêu cầu phê duyệt không?

2. **Bật Active Workflow**
   - Sau khi test thành công, **bật Active** và chọn **Trigger Type**:
     - **Form Trigger** (nếu muốn kích hoạt thủ công).
     - **Schedule Trigger** (nếu muốn chạy định kỳ).

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa Cho Mục Đích Marketing**
- **Thêm Analytics**: Kết nối với **Google Analytics** hoặc **Meta Business Suite** để theo dõi hiệu suất bài viết.
- **Tự động Tag Hashtag**: Sử dụng node **Set** để thêm hashtag tự động vào bài viết (ví dụ: `#TinTứcTech`, `#VinaPhone`).
- **Lên lịch theo giờ cao điểm**: Cấu hình **Schedule Trigger** để đăng bài vào **8h-10h sáng** (thời gian engagement cao).

### **2. Quản Lý Feedback Hiệu Quả**
- **Tạo Form Phê Duyệt**: Sử dụng **Google Forms** hoặc **Typeform** để người dùng đánh giá bài viết trước khi đăng.
- **Lưu Log Feedback**: Sử dụng node **Google Sheets** để lưu tất cả feedback vào một sheet riêng (`Feedback_Content`).
- **AI Tự Động Chỉnh Sửa**: Nếu feedback là "Hình ảnh không phù hợp", workflow sẽ tự động **sinh hình ảnh mới** và gửi lại Slack.

### **3. Kết Hợp Với Dịch Vụ Khác**
- **Telegram Bot**: Thay vì Slack, sử dụng **Telegram Bot** để gửi yêu cầu phê duyệt.
- **Notion Database**: Lưu dữ liệu bài viết vào **Notion** thay vì Google Sheets.
- **Canva API**: Thay vì NanoBanana, sử dụng **Canva API** để chỉnh sửa hình ảnh.

### **4. Tự Động Hóa Cho Nhiều Brand**
- **Sử dụng Sticky Note** để lưu trữ nhiều **set biến brand** khác nhau.
- **Loop Over Items** để chạy workflow cho **nhiều brand cùng lúc**.

---
## 📌 **Kết Luận: Đăng Bài AI Chuyên Nghiệp Mỗi Ngày - Không Cần Code!**

Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy marketing** thay vì việc tạo nội dung thủ công. Với **AI tạo văn bản + hình ảnh**, **phê duyệt tự động**, và **lên lịch đăng bài**, bạn sẽ:
✔ **Tăng engagement** trên LinkedIn & Facebook
✔ **Tiết kiệm thời gian** lên đến **10+ giờ/ngày**
✔ **Nội dung chuyên nghiệp** phù hợp với brand
✔ **Dữ liệu theo dõi** đầy đủ trong Google Sheets

**Hãy thử ngay!** Import workflow, điền biến brand, và **bắt đầu tự động hóa nội dung AI** của mình.

---
### **🔗 Tài Liệu Tham Khảo**
- [OpenRouter API Docs](https://openrouter.ai/docs)
- [Perplexity API Docs](https://www.perplexity.ai/api)
- [Late API Docs](https://late.app/docs)
- [NanoBanana API Docs](https://nanobanana.com/docs)

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chúc các sếp thành công với tự động hóa nội dung AI!** 🚀