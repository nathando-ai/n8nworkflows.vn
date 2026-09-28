---
title: "🚀 Tự động dịch metadata YouTube đa ngôn ngữ với Gemini AI và Google Sheets"
description: "Giải pháp tự động dịch tiêu đề, mô tả và thẻ của video YouTube sang nhiều ngôn ngữ, cập nhật ngay trên kênh mà không cần code."
slug: "tuy-dong-dich-metadata-youtube-đa-ngôn-ngu-gemini-google-sheets"
tags: [n8n, automation, no-code, youtube, google-sheets, gemini-ai]
keywords: [n8n workflow, tự động hóa, dịch metadata YouTube, Gemini AI, Google Sheets]
---

# 🚀 Tự động dịch metadata YouTube đa ngôn ngữ với Gemini AI và Google Sheets

Bạn đang phải chỉnh sửa thủ công tiêu đề, mô tả và thẻ cho từng video YouTube trong nhiều ngôn ngữ?  
Bạn muốn tiết kiệm thời gian, giảm sai sót và luôn cập nhật metadata mới nhất ngay trên kênh?  
Workflow **Multilingual YouTube Metadata Translator** của Agent Circle sẽ giúp bạn thực hiện điều đó **100% tự động, không cần code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn chỉnh sửa thủ công từng video, mỗi lần cập nhật chỉ cần một lần trigger workflow.  
- **Chính xác & nhất quán**: Dịch được chuẩn xác nhờ Gemini AI, đồng thời giữ nguyên cấu trúc metadata gốc.  
- **Cá nhân hóa**: Hỗ trợ nhiều ngôn ngữ tùy chỉnh, dễ dàng mở rộng thêm ngôn ngữ mới chỉ bằng cách thêm vào Google Sheet.  
- **Hoạt động liên tục**: Trigger theo lịch hoặc khi có video mới, luôn cập nhật metadata ngay lập tức.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ / Tài khoản | Mô tả | Lưu ý |
|---------------------|-------|-------|
| **Google Sheets** | Sheet chứa danh sách ngôn ngữ, URL video, trạng thái, v.v. | Cần bật API Google Sheets và tạo Service Account, lưu key JSON. |
| **YouTube Data API** | Truy cập metadata video và cập nhật metadata. | Tạo API key trong Google Cloud Console, bật YouTube Data API v3. |
| **Gemini API** | Dịch nội dung metadata. | Đăng ký Gemini API key (Google Cloud Gemini). |
| **n8n** | Môi trường chạy workflow. | Cài đặt n8n (Self-hosted) hoặc sử dụng n8n.cloud. |
| **HTTP Request** | Gửi yêu cầu cập nhật metadata lên YouTube. | Cấu hình endpoint và headers đúng chuẩn của YouTube Data API. |
| **Optional** | Slack/Telegram để nhận thông báo. | Nếu muốn, thêm node Slack/Telegram vào workflow. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ link gốc:  
   <https://n8n.io/workflows/5902>  
2. Mở n8n Editor → **Import** → **Upload JSON** → chọn file vừa tải.  
3. Hoặc copy toàn bộ JSON và dán vào **Import** → **Paste JSON**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **Schedule Trigger** | Định kỳ chạy workflow (ví dụ: 1 lần/đêm). | `Cron` hoặc `Interval`. |
| **Get Language List** | Lấy danh sách ngôn ngữ từ Google Sheet. | `Spreadsheet ID`, `Sheet Name`, `Range`. |
| **Parse Data To JSON** | Chuyển dữ liệu sheet sang JSON. | `Code` (đã được