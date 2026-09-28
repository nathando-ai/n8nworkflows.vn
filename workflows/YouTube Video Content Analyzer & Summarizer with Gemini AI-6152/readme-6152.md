---
title: "🚀 Phân Tích & Tóm Tắt Video YouTube Tự Động với Gemini AI"
description: "Giải pháp tự động phân tích nội dung video YouTube và tạo bản tóm tắt chi tiết chỉ với một liên kết, giúp bạn tiết kiệm thời gian và tăng hiệu quả nội dung."
slug: "phan-tich-tom-tat-video-youtube-gemini-ai"
tags: [n8n, automation, no-code, youtube, ai, gemini]
keywords: [n8n workflow, tự động hóa, Gemini AI, phân tích video, tóm tắt nội dung, YouTube automation]
---

# 🚀 Phân Tích & Tóm Tắt Video YouTube Tự Động với Gemini AI

Bạn đang phải xem hàng trăm video YouTube để lấy ý tưởng, tóm tắt nội dung, hoặc chỉ đơn giản là muốn biết nhanh những điểm chính của một video? Việc lướt qua từng video, ghi chú lại những thông tin quan trọng là một công việc tốn thời gian và dễ gây sai sót. Workflow này sẽ giúp bạn **đưa toàn bộ quá trình phân tích và tóm tắt video YouTube vào một chuỗi tự động hoàn toàn, không cần viết code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút xem video → vài giây tóm tắt.
- **Độ chính xác cao**: Sử dụng Gemini AI, nhận được bản tóm tắt chi tiết, ngữ cảnh đầy đủ.
- **Tự động hóa 100%**: Không cần thao tác thủ công, chỉ cần nhập link và mô tả (nếu cần).
- **Tích hợp linh hoạt**: Dễ dàng mở rộng sang Slack, Telegram, email, hay lưu kết quả vào Google Sheets.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **API Key của Google Gemini**: Đăng ký tại [Google Cloud Console](https://console.cloud.google.com/) → tạo API key cho Gemini.
- **n8n**: Đã cài đặt và chạy (Self-hosted hoặc Cloud).
- **Không cần tài khoản YouTube API**: Workflow chỉ lấy link, Gemini sẽ xử lý nội dung video.
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/6152) hoặc sao chép toàn bộ JSON.
2. Trong n8n Editor, chọn **Import** → **Import from file** hoặc **Import from clipboard**.
3. Đặt tên workflow: `YouTube Video Content Analyzer & Summarizer with Gemini AI`.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cài đặt cần chỉnh |
|------|-------|-------------------|
| **Get Input** | Form để nhập link YouTube và mô tả (bắt buộc/tuỳ chọn). | Không cần chỉnh, chỉ cần kiểm tra trường `YouTube URL` đã được đánh dấu *required*. |
| **Check if description is empty** | Code node kiểm tra mô tả, nếu trống thì tạo prompt mặc định. | Đảm bảo biến `description` được truyền từ node trước. |
| **Get analysis from Google Gemini** | HTTP Request tới endpoint Gemini. | <ul><li>**URL**: `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key={{$json["geminiApiKey"]}}</li><li>**Method**: POST</li><li>**Body**: JSON chứa `contents` với prompt đã được tạo.</li><li>**Credentials**: Chọn *Google Gemini* (đã tạo API key).*</li></ul> |
| **Analysis result** | Form hiển thị kết quả tóm tắt. | Không cần chỉnh. |
| **Redirect for another analysis** | Form cho phép chạy lại workflow với link mới. | Không cần chỉnh. |

> **Tip**: Nếu bạn muốn thay đổi prompt mặc định, chỉnh node **Check if description is empty** bằng cách thay đổi biến `defaultPrompt` trong code.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** trong n8n, nhập link YouTube và mô tả (hoặc để trống).
2. Kiểm tra kết quả trong node **Analysis result**. Nếu mọi thứ ổn, chuyển workflow sang trạng thái *Active*.
3. Khi workflow được kích hoạt, mỗi lần người dùng nhập link mới, Gemini sẽ tự động trả về bản tóm tắt.

## ✍️ Mẹo & gợi ý nâng cao
- **Gửi kết quả tới Slack**: Thêm node **Slack** sau node **Analysis result** để tự động gửi tin nhắn kèm tóm tắt.
- **Lưu kết quả vào Google Sheets**: Thêm node **Google Sheets** để ghi lại link, tóm tắt, thời gian thực thi.
- **Tự động gửi email**: Sử dụng node **Email** để gửi bản tóm tắt tới danh sách email.
- **Lưu log**: Thêm node **Write Binary File** hoặc **Database** để lưu lịch sử phân tích.

## 📌 Kết luận
Workflow “YouTube Video Content Analyzer & Summarizer with Gemini AI” là công cụ mạnh mẽ giúp các sếp **tiết kiệm thời gian, nâng cao độ chính xác và tự động hóa quy trình** phân tích nội dung video. Hãy thử ngay, tích hợp vào quy trình nội dung của bạn, và trải nghiệm sự tiện lợi mà AI mang lại!