---
title: "🎥 Tự động phân tích video bằng AI Gemini - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động tải, phân tích video bằng AI Gemini và lưu kết quả. Giải phóng thời gian cho các sếp với workflow tự động hóa 100% không cần code."
slug: "tu-dong-phan-tich-video-bang-ai-gemini"
tags: [n8n, automation, no-code, ai, video-analysis]
keywords: [n8n workflow, tự động hóa video, ai phân tích video, gemini api, xử lý video]
---

# 🎥 Tự động phân tích video bằng AI Gemini - Workflow n8n hoàn chỉnh

[Các sếp đang gặp khó khăn khi phải phân tích thủ công hàng loạt video cho các dự án marketing, nội dung số hay quản lý nội dung. Với workflow này, các sếp có thể tự động tải, phân tích video bằng AI Gemini và lưu kết quả một cách nhanh chóng và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý hàng loạt video mà không cần can thiệp thủ công.
- **Phân tích chính xác**: Sử dụng công nghệ AI Gemini để nhận diện nội dung video một cách chi tiết.
- **Tự động hóa hoàn toàn**: Không cần lập trình, chỉ cần cấu hình và kích hoạt workflow.
- **Dữ liệu có thể tái sử dụng**: Kết quả phân tích được lưu trữ và có thể sử dụng cho nhiều mục đích khác nhau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **API Key của Google Gemini**: Các sếp cần có API Key từ Google để sử dụng dịch vụ AI của Gemini.
- **URL video**: Link đến video cần phân tích.
- **n8n Editor**: Phiên bản n8n đã được cài đặt và cấu hình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này bằng cách:
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập link: [https://n8n.io/workflows/3775](https://n8n.io/workflows/3775).
3. Hoặc tải file JSON về và import từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Set Input"**: Các sếp cần cấu hình URL của video cần phân tích.
- **Node "Download video"**: Đảm bảo URL video hợp lệ và có thể truy cập được.
- **Node "Upload video Gemini"**: Cấu hình API Key của Gemini trong phần Credentials.
- **Node "Analyze video Gemini"**: Có thể tùy chỉnh prompt để tập trung vào các khía cạnh cụ thể của video.

#### 3. Kích hoạt ⚡️
- **Test workflow**: Nhấn vào nút "Test workflow" để kiểm tra quá trình tải và phân tích video.
- **Active workflow**: Sau khi kiểm tra thành công, kích hoạt workflow để tự động xử lý video.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể cấu hình workflow để gửi kết quả phân tích đến các kênh thông báo.
- **Lưu log**: Lưu trữ kết quả phân tích vào Google Sheets hoặc cơ sở dữ liệu để theo dõi và phân tích sau này.
- **Gửi báo cáo định kỳ**: Tự động gửi báo cáo phân tích video theo lịch trình hàng ngày hoặc hàng tuần.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình phân tích video một cách nhanh chóng và chính xác. Với sự hỗ trợ của AI Gemini, các sếp có thể nhận được những thông tin chi tiết về nội dung video, từ đó tối ưu hóa các chiến dịch marketing và quản lý nội dung hiệu quả hơn. Hãy áp dụng ngay để giải phóng thời gian và nâng cao hiệu suất làm việc!