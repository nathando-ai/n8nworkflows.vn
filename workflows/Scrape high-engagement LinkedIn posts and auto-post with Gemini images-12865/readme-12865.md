---
title: "🚀 Tự Động Hóa Scrape & Tạo Nội Dung LinkedIn Viral Với Gemini AI - Giảm 90% Thời Gian Content Creation"
description: "Workflow tự động hóa scrape nội dung LinkedIn có engagement cao, phân tích xu hướng bằng Gemini AI, tạo bài viết + hình ảnh chuyên nghiệp và tự động đăng lên trang tổ chức - Giúp các sếp tiết kiệm 90% thời gian content creation mà vẫn đạt hiệu quả cao nhất."
slug: "tieu-dong-hoa-scrape-linkedin-voi-gemini-ai"
tags: [n8n, automation, content-creation, ai-multimodal, linkedin-automation, google-gemini, no-code]
keywords: [n8n workflow linkedin, tự động hóa content linkedin, scrape linkedin bằng n8n, gemini ai tạo hình ảnh, tự động đăng bài linkedin, content marketing tự động]
---

# 🚀 **Tự Động Hóa Scrape & Tạo Nội Dung LinkedIn Viral Với Gemini AI**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tiết kiệm 90% thời gian** tìm kiếm và tạo nội dung LinkedIn chất lượng cao
- **Tự động phát hiện** bài viết viral từ các profile top trong ngành
- **Tạo bài viết + hình ảnh chuyên nghiệp** bằng Gemini AI
- **Đăng tự động** lên trang tổ chức mà không cần can thiệp thủ công

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với cách làm thủ công (không cần scrape, phân tích, viết bài, tạo hình)
- **Nội dung 100% tối ưu** theo xu hướng hiện tại (AI phân tích hàng ngàn bài viết để tạo content viral)
- **Hình ảnh chuyên nghiệp** tự động sinh ra từ Gemini AI (không cần designer)
- **Hoạt động 24/7** mà không cần can thiệp (scheduled trigger + tự động đăng)
- **Dữ liệu phân tích** được lưu trữ trong Google Sheets để theo dõi hiệu suất
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản LinkedIn tổ chức** (để đăng bài tự động)
2. **API Key Apify** (để scrape LinkedIn)
3. **Google Sheets** với 2 sheet:
   - `profile_urls` (để lưu danh sách profile cần scrape)
   - `scraped_posts` (để lưu dữ liệu bài viết viral)
4. **Google Gemini API Key** (để phân tích và tạo hình ảnh)
5. **Google Sheets OAuth 2.0 Credentials** (để trigger tự động khi có dữ liệu mới)
6. **Tài khoản n8n Self-hosted** (để chạy workflow 24/7)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/12865](https://n8n.io/workflows/12865) và import vào n8n Editor
- **Cách 2:** Copy toàn bộ JSON và paste vào **Import Workflow** trong n8n Editor

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Google Sheets**
1. **Tạo 2 sheet trong Google Sheets**:
   - `profile_urls` (cột `url` chứa danh sách profile LinkedIn cần scrape)
   - `scraped_posts` (cột `url`, `title`, `content`, `engagement`, `date`)
2. **Cập nhật credentials**:
   - Node `Fetch LinkedIn Profile URLs` → Chọn sheet `profile_urls`
   - Node `Save Viral Posts to Sheets` → Chọn sheet `scraped_posts`
   - Node `New Post Data Trigger` → Chọn `googleSheetsTriggerOAuth2Api` (cấu hình OAuth 2.0 trong n8n)

#### **B. Cấu hình Apify API (Scrape LinkedIn)**
1. **Đăng ký API Key Apify**:
   - Tạo tài khoản tại [Apify.com](https://apify.com/)
   - Lấy API Key từ **Settings > API Tokens**
2. **Cập nhật trong node `Scrape LinkedIn Posts API`**:
   - Thay thế `{{ $json.output.api_key }}` bằng API Key thực tế
   - Thay thế `{{ $json.output.profile_url }}` bằng `$node["Fetch LinkedIn Profile URLs"].json[].url`

#### **C. Cấu hình Google Gemini AI**
1. **Lấy API Key Gemini**:
   - Đăng ký tại [Google AI Studio](https://aistudio.google.com/)
   - Lấy API Key từ **API Credentials**
2. **Cập nhật credentials**:
   - Node `Google Gemini Chat Model` → Chọn `googlePalmApi`
   - Node `Generate an image` → Chọn `googlePalmApi` (đảm bảo cùng API Key)

#### **D. Cấu hình LinkedIn Publishing**
1. **Cấu hình LinkedIn Credentials**:
   - Tạo **LinkedIn App** tại [LinkedIn Developer Portal](https://www.linkedin.com/developers/)
   - Lấy `Client ID` và `Client Secret`
   - Cập nhật trong node `Publish to LinkedIn` (thay thế `{{ $json.output.client_id }}` và `{{ $json.output.client_secret }}`)

#### **E. Thiết lập Scheduled Trigger**
- Node `LinkedIn Content Automation Scheduler` → Chọn **Every 12 hours** (hoặc thời gian phù hợp)

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với 1-2 profile mẫu để kiểm tra:
   - Scrape thành công không?
   - AI phân tích và tạo hình ảnh có logic không?
   - Bài viết đăng lên LinkedIn thành công không?
2. **Bật Active** khi tất cả node hoạt động ổn định.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[TIẾP CẬN HƠN]
1. **Tăng hiệu quả bằng cách:**
   - Thêm **filter engagement cao hơn** (ví dụ: 50+ likes thay vì 20)
   - **Tự động chia sẻ bài viết** lên các group LinkedIn quan trọng (sử dụng node `linkedIn` với API Group)
2. **Lưu log hoạt động:**
   - Thêm node `googleSheets` để lưu log lỗi và thành công
   - Sử dụng node `stickyNote` để ghi chú các vấn đề phát sinh
3. **Tối ưu hình ảnh:**
   - Sử dụng **Gemini Pro Vision** để tạo hình ảnh động (nếu có API)
   - Thêm **watermark** cho hình ảnh bằng node `code`
4. **Báo cáo định kỳ:**
   - Tạo **dashboard Google Data Studio** từ dữ liệu trong Google Sheets
   - Gửi **báo cáo tuần/Tháng** qua email (sử dụng node `email`)
:::

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✅ **Tự động hóa 100% quy trình content LinkedIn**
✅ **Tạo nội dung viral** dựa trên xu hướng thực tế
✅ **Tiết kiệm thời gian** mà không cần designer hoặc chuyên gia SEO

**Hành động ngay!**
1. **Cài n8n Self-hosted** trên VPS để workflow hoạt động 24/7
2. **Import workflow** và cấu hình theo hướng dẫn
3. **Bật scheduled trigger** và để AI làm việc cho bạn!

👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
**Chú ý:** Workflow này yêu cầu **API Key Apify** (có thể bị giới hạn rate limit). Nếu gặp vấn đề, hãy liên hệ với Apify để nâng cấp plan.