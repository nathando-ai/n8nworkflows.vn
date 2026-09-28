---
title: "🚀 Tự Động Hoá Scrape TikTok Trends + Tạo Video AI Chuyên Nghiệp với Apify, Fal AI & Google Suite"
description: "Workflow tự động hóa scrape dữ liệu TikTok về xu hướng mới nhất, phân tích bằng AI và tạo video vertical 8s chuyên nghiệp với Fal AI, hoàn toàn không cần code. Giúp các sếp tiết kiệm thời gian lên đến 8h/tuần và tăng cường nội dung marketing tự động."
slug: "tieu-dong-hoa-scrape-tiktok-tao-video-ai"
tags: [n8n, automation, content-creation, multimodal-ai, tiktok-scraper, fal-ai, google-suite, apify]
keywords: [n8n workflow scrape tiktok, tự động hóa tạo video ai, apify tiktok scraper, fal ai video generation, google sheets automation, content marketing tự động]
---

# 🚀 **Tự Động Hoá Scrape TikTok Trends + Tạo Video AI Chuyên Nghiệp với Apify, Fal AI & Google Suite**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Scrape** xu hướng TikTok liên tục (không cần viết code).
- **Tạo video vertical 8s** với nội dung AI phân tích từ xu hướng.
- **Tự động lưu trữ** dữ liệu và video vào Google Drive/Sheets.
- **Tiết kiệm thời gian** lên đến 8h/tuần so với cách làm thủ công.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Scrape và tạo video chỉ trong vài phút thay vì nhiều giờ.
- **Nội dung cá nhân hóa:** Video được tạo dựa trên xu hướng thực tế từ TikTok.
- **Hoạt động 24/7:** Workflow chạy tự động mỗi khi có xu hướng mới.
- **Dữ liệu sạch:** Lưu trữ metadata TikTok và prompt AI vào Google Sheets.
- **Video chuyên nghiệp:** Sử dụng mô hình Fal AI Veo3 để tạo video vertical chất lượng cao.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
**Các tài khoản & API cần thiết:**
1. **Apify Account** (đăng ký tại [apify.com](https://apify.com/)) với:
   - Token API (để scrape TikTok).
   - Đã mua credits cho actor `clockworks/tiktok-scraper`.
2. **Fal AI Account** (đăng ký tại [fal.ai](https://fal.ai/)) với:
   - API Key (để sử dụng mô hình `fal-ai/veo3`).
   - Đã nạp credits (mỗi video ~$0.10).
3. **OpenRouter Account** (đăng ký tại [openrouter.ai](https://openrouter.ai/)) với:
   - API Key (để phân tích và tạo prompt AI).
4. **Google Workspace** (Drive & Sheets) với:
   - Tài khoản đã kết nối OAuth2 cho Google Drive và Sheets.
   - 2 Sheet riêng biệt:
     - **Sheet 1:** Lưu dữ liệu raw từ TikTok (cột: `text`, `stats`, `author`).
     - **Sheet 2:** Lưu prompt AI đã tạo (cột: `prompt`, `video_concept`).
   - 1 Folder Google Drive để lưu video cuối cùng.

**Hệ thống:**
- n8n phiên bản **1.x trở lên** (khuyến nghị cài trên VPS để chạy 24/7).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11003](https://n8n.io/workflows/11003).
- **Cách 1:** Nhấn `Import` trong n8n Editor và chọn file JSON.
- **Cách 2:** Copy toàn bộ JSON và dán vào `Import Workflow` (đường dẫn: `https://<your-n8n-instance>/workflows/import`).

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Credentials**
| **Node**               | **Tham số cần thiết**                          | **Lưu ý**                                                                 |
|------------------------|------------------------------------------------|---------------------------------------------------------------------------|
| **Apify (HTTP Request)** | Thêm `token` vào URL query params: `?token=YOUR_APIFY_TOKEN` | Khuyến nghị chuyển sang **Header Auth** cho an toàn.                     |
| **Google Sheets**       | `documentId` và tên Sheet (`シート1`, `生成済み`) | Đảm bảo Sheet đã được tạo và cột dữ liệu khớp với workflow.               |
| **OpenRouter (AI Agent)** | API Key trong `lmChatOpenRouter` node          | Chọn mô hình phù hợp (ví dụ: `mistralai/Mistral-7B-Instruct-v0.1`).     |
| **Fal AI (HTTP Request)** | API Key trong Header Auth (`Authorization: Bearer YOUR_FAL_API_KEY`) | Đảm bảo mô hình `fal-ai/veo3` được chọn trong prompt.                   |
| **Google Drive**        | `folderId` trong node `Upload file`             | Thay đổi thành ID folder của bạn (tìm trong URL: `https://drive.google.com/drive/folders/FOLDER_ID`). |

#### **B. Cấu hình Google Sheets**
1. **Tạo 2 Sheet trong Google Sheets:**
   - **Sheet 1:** Tên `シート1` (hoặc `Raw Data`), cột cần có: `text`, `stats`, `author`.
   - **Sheet 2:** Tên `生成済み` (hoặc `Generated`), cột cần có: `prompt`, `video_concept`.
2. **Cập nhật `documentId`:**
   - Mở Sheet trong trình duyệt → URL sẽ có dạng:
     `https://docs.google.com/spreadsheets/d/[DOCUMENT_ID]/edit`.
   - Sao chép `DOCUMENT_ID` và điền vào các node `Google Sheets`.

#### **C. Cấu hình Google Drive**
1. **Tạo 1 folder mới** để lưu video (ví dụ: `AI-Generated-Videos`).
2. **Lấy `folderId`:**
   - Mở folder trong trình duyệt → URL sẽ có dạng:
     `https://drive.google.com/drive/folders/[FOLDER_ID]`.
   - Sao chép `FOLDER_ID` và điền vào node `Upload file`.

---
### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - Nhấn `Execute Workflow` để chạy thử.
   - Kiểm tra:
     - Dữ liệu TikTok có được scrape vào `Sheet 1` không?
     - Prompt AI có được tạo và lưu vào `Sheet 2` không?
     - Video có được tạo và upload lên Google Drive không?
2. **Bật Active:**
   - Sau khi test thành công, chuyển trạng thái workflow sang `Active`.
   - **Lưu ý:** Workflow sẽ chạy tự động khi kích hoạt `Manual Trigger`.

---
## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động chạy hàng ngày:**
   - Sử dụng **n8n-nodes-base.cron** để kích hoạt workflow mỗi ngày vào giờ peak (ví dụ: 8h sáng).
   - Cấu hình trong node `Manual Trigger`:
     ```json
     {
       "cron": "0 8 * * *"
     }
     ```

2. **Gửi báo cáo định kỳ:**
   - Kết hợp với **Slack/Telegram Bot** để thông báo khi có video mới được tạo.
   - Thêm node `n8n-nodes-base.slack` sau node `Upload file` để gửi tin nhắn:
     ```
     "text": "🎥 Video mới được tạo: {{ $node["Upload file"].json["fileName"] }}",
     "attachments": [
       {
         "title": "Xem video",
         "text": "https://drive.google.com/file/d/{{ $node["Upload file"].json["fileId"] }}/view",
         "mrkdwn_in": ["text"]
       }
     ]
     ```

3. **Lưu log hoạt động:**
   - Thêm node `n8n-nodes-base.stickyNote` để ghi lại thời gian scrape và trạng thái:
     ```
     "text": "Scrape TikTok thành công - Thời gian: {{ $node["Wait"].json["timestamp"] }}"
     ```

4. **Tối ưu prompt AI:**
   - Cập nhật mô hình OpenRouter để cải thiện chất lượng prompt (ví dụ: sử dụng `gpt-4` nếu có credits).
   - Thêm tham số `temperature: 0.7` trong node `OpenRouter Chat Model` để tăng tính sáng tạo.

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quy trình từ **scrape xu hướng TikTok** đến **tạo video AI chuyên nghiệp** chỉ trong vài phút. Bằng cách kết hợp **Apify, Fal AI, OpenRouter và Google Suite**, bạn không chỉ tiết kiệm thời gian mà còn nâng cao chất lượng nội dung marketing.

**👉 Hãy áp dụng ngay và bắt đầu tạo video AI từ xu hướng TikTok trong giây lát!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::