---
title: "🎬 Tự Động Chuyển Đổi Video YouTube Thành Nhiều Loại Nội Dung (Blog, Script, Tweet...) Với AI OpenRouter & Airtable - N8N"
description: "Workflow tự động hóa 100% không code giúp các sếp chuyển đổi video YouTube thành nhiều định dạng nội dung (blog, script, tweet, newsletter...) chỉ với 1 lần nhập liệu, tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dong-video-youtube-thanh-nhieu-loai-noi-dung"
tags: [n8n, automation, content-creation, ai-openrouter, airtable, no-code, marketing-automation]
keywords: [n8n workflow youtube, tự động hóa nội dung marketing, chuyển đổi video thành blog, ai openrouter n8n, airtable automation, tự động hóa content creation]
---

# 🚀 **Tự Động Chuyển Đổi Video YouTube Thành Nhiều Loại Nội Dung (Blog, Script, Tweet...) Với AI OpenRouter & Airtable**

## **🔥 Nỗi Đau Của Các Sếp Trong Content Creation**
Các sếp thường phải mất **giờ đồng hồ** để:
- **Lấy transcript** từ video YouTube.
- **Viết blog**, **script YouTube**, **tweet**, **newsletter**, **bài LinkedIn** từ nội dung video.
- **Quản lý và lưu trữ** các bản nội dung này một cách rối rắm trên nhiều công cụ khác nhau.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi nội dung có thể được tái sử dụng nhiều lần để tối ưu hóa SEO và tiếp cận nhiều kênh khác nhau.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình** chỉ với **1 lần nhập liệu** từ video YouTube, sử dụng **AI OpenRouter** để tạo ra nhiều định dạng nội dung khác nhau và **Airtable** để quản lý tất cả.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
✅ **Tạo ra nhiều định dạng nội dung** (blog, script, tweet, newsletter, LinkedIn) từ **1 video YouTube**.
✅ **Cá nhân hóa nội dung** cho từng kênh truyền thông khác nhau.
✅ **Quản lý nội dung hiệu quả** trên **Airtable**, dễ dàng cập nhật và theo dõi.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
✅ **Tối ưu hóa SEO** bằng cách tái sử dụng nội dung từ video.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Airtable** (để lưu trữ danh sách video và nội dung tạo ra).
   - **Link mẫu bảng Airtable**: [https://airtable.com/appOfTK0sDWqNiJyl](https://airtable.com/appOfTK0sDWqNiJyl) (sếp có thể sao chép và tùy chỉnh).
2. **API Key OpenRouter** (để sử dụng AI tạo nội dung).
   - **Đăng ký tại**: [https://openrouter.ai/](https://openrouter.ai/) (miễn phí hoặc trả phí tùy theo nhu cầu).
3. **API Key Scrape Creator** (để lấy transcript từ video YouTube).
   - **Tài liệu API**: [https://docs.scrapecreators.com/v1/youtube/video/transcript](https://docs.scrapecreators.com/v1/youtube/video/transcript).
4. **N8n Self-hosted** (để workflow chạy 24/7).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/6899) (hoặc sao chép từ link trên).
- Mở **n8n Editor** → **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô tương ứng.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **27 node**, nhưng các sếp cần chú ý đến các **node quan trọng** sau:

#### **🔹 Node "Get YouTube URLs" (Airtable)**
- **Mục đích**: Lấy danh sách video YouTube từ bảng Airtable.
- **Cấu hình**:
  - **Credentials**: Chọn `airtableTokenApi` (đã cấu hình trước khi import).
  - **Operation**: Đảm bảo chọn `search`.
  - **Filter**: Cần thiết để chỉ lấy video cần xử lý (ví dụ: `status = "pending"`).

#### **🔹 Node "Get Transcript" (HTTP Request)**
- **Mục đích**: Lấy transcript từ video YouTube bằng API Scrape Creator.
- **Cấu hình**:
  - **Credentials**: Chọn `httpHeaderAuth` (đã cấu hình API Key Scrape Creator).
  - **URL**: `https://api.scrapecreators.com/v1/youtube/video/transcript`.
  - **Query Parameters**:
    ```json
    {
      "url": "{{$node["Get YouTube URLs"].json["fields"]["YouTube URL"]}}"
    }
    ```
  - **Headers**:
    ```json
    {
      "Authorization": "{{$credentials.httpHeaderAuth.apiKey}}"
    }
    ```

#### **🔹 Node "OpenRouter Chat Model" (LM Chat OpenRouter)**
- **Mục đích**: Sử dụng AI OpenRouter để tạo nội dung (blog, script, tweet...).
- **Cấu hình**:
  - **Credentials**: Chọn `openRouterApi` (đã cấu hình API Key OpenRouter).
  - **Model**: Đặt `openai/gpt-4.1-nano` (hoặc model khác phù hợp).
  - **Prompt**: Các sếp có thể **tùy chỉnh prompt** trong các node `chainLlm` sau (ví dụ: `blogpost`, `youtube script`, `tweet`).

#### **🔹 Node "Update Airtable" (Airtable)**
- **Mục đích**: Cập nhật nội dung tạo ra vào bảng Airtable.
- **Cấu hình**:
  - **Credentials**: Chọn `airtableTokenApi`.
  - **Operation**: Chọn `upsert` (cập nhật hoặc thêm mới).
  - **Record ID**: Sử dụng trường `ID` từ bảng Airtable.
  - **Fields**: Điền các trường tương ứng (ví dụ: `Blog Post`, `YouTube Script`, `Tweet`).

#### **🔹 Node "Delete Selected Records" (Airtable)**
- **Mục đích**: Xóa video đã xử lý khỏi danh sách (nếu cần).
- **Cấu hình**:
  - **Credentials**: Chọn `airtableTokenApi`.
  - **Operation**: Chọn `deleteRecord`.
  - **Filter**: Chỉ xóa video đã hoàn thành (ví dụ: `status = "completed"`).

#### **🔹 Node "Switch" & "Filter"**
- **Mục đích**: Chỉ xử lý nội dung có kết quả (tránh lỗi).
- **Cấu hình**:
  - Các node `filter` (ví dụ: `filter tutorial output`) cần **kiểm tra `result`** có tồn tại không.
  - Ví dụ:
    ```json
    {
      "jsonpath": "$.result"
    }
    ```

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1 video mẫu**:
   - Chọn **node "Manual Trigger"** → Nhấn **Execute Workflow**.
   - Kiểm tra **log** và **bảng Airtable** để xác nhận nội dung đã được tạo ra.
2. **Bật Active Workflow**:
   - Sau khi test thành công, **bật workflow** để nó hoạt động tự động khi có video mới.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn `"Video [TITLE] đã được chuyển đổi thành [BLOG/TWEET/...]"`.
2. **Lưu Log Tự Động**:
   - Sử dụng node **Set** hoặc **Code** để lưu log vào **Airtable** hoặc **Google Sheets**.
3. **Gửi Báo Cáo Định Kỳ**:
   - Dùng **n8n Cron Trigger** để gửi báo cáo tổng hợp nội dung đã tạo ra hàng tuần.
4. **Tùy Chỉnh Prompt AI**:
   - Các sếp có thể **cập nhật prompt** trong node `chainLlm` để phù hợp với **ngôn ngữ mục tiêu** (Việt Nam, Anh, Nhật...).
5. **Sử Dụng Model AI Khác**:
   - Thay đổi model trong `OpenRouter Chat Model` (ví dụ: `mistralai/mixtral-8x7b`).
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp đi lặp lại trong **content creation**, đồng thời **tối ưu hóa hiệu quả** bằng cách tái sử dụng nội dung từ video YouTube trên nhiều kênh khác nhau.

**🚀 Hãy áp dụng ngay và xem kết quả!**
- **Bắt đầu với VPS n8n** để workflow chạy 24/7.
- **Tùy chỉnh prompt** để phù hợp với nhu cầu của doanh nghiệp.
- **Kết nối với Slack/Telegram** để theo dõi tiến trình.

**Chia sẻ kết quả của các sếp sau khi sử dụng workflow này!** 👇

---
:::note[LƯU Ý CUỐI CUNG]
- Nếu gặp lỗi, hãy kiểm tra **credentials** và **log** trong n8n Editor.
- Các sếp có thể **sao chép và tùy chỉnh** bảng Airtable theo nhu cầu.
- Để hỗ trợ kỹ thuật, liên hệ với **Alexandra Spalato** (tác giả workflow) qua [website](https://alexandraspalato.com/).
:::