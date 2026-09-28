---
title: "🎬 Tự động hóa tóm tắt nội dung YouTube bằng Google Gemini & Google Docs"
description: "Hướng dẫn chi tiết cách tự động hóa việc tóm tắt nội dung video YouTube bằng công cụ AI Google Gemini và lưu kết quả vào Google Docs"
slug: "tu-dong-hoa-tom-tat-noi-dung-youtube-google-gemini-google-docs"
tags: [n8n, automation, no-code, AI, Google Docs]
keywords: [n8n workflow, tự động hóa nội dung, tóm tắt video, Google Gemini, Google Docs]
---

# 🎬 Tự động hóa tóm tắt nội dung YouTube bằng Google Gemini & Google Docs

[Các sếp] có biết không? Với lượng video YouTube ngày càng tăng, việc tóm tắt nội dung thủ công trở nên cực kỳ tốn thời gian và công sức. Bạn phải ngồi xem video, ghi chú, sau đó viết lại nội dung một cách ngắn gọn. Đó là quá trình cực kỳ mệt mỏi, đặc biệt khi bạn phải làm việc này hàng ngày.

Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quá trình này, từ việc lấy nội dung video đến việc tóm tắt và lưu kết quả vào Google Docs. Tất cả chỉ với vài bước đơn giản, không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình từ lấy nội dung đến tóm tắt.
- **Chính xác cao**: Sử dụng công nghệ AI Google Gemini để đảm bảo nội dung tóm tắt chất lượng.
- **Cá nhân hóa**: Có thể chọn ngôn ngữ cho bản tóm tắt phù hợp với nhu cầu.
- **Hoạt động liên tục**: Workflow có thể chạy tự động 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Google Docs và Google Gemini được kích hoạt.
- API Key cho Google Gemini và Google Docs.
- Tài khoản RapidAPI để sử dụng YouTube Transcript API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/5866](https://n8n.io/workflows/5866)
3. Hoặc bạn có thể tải file JSON về và import trực tiếp từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **On form submission**: Node này sẽ tạo một form để nhập URL video YouTube và ngôn ngữ mong muốn cho bản tóm tắt.
  - Không cần cấu hình gì thêm, chỉ cần đảm bảo form hoạt động bình thường.

- **Google Gemini Chat Model**: Node này sử dụng công nghệ AI Google Gemini để tóm tắt nội dung.
  - **Credentials**: Cần cấu hình Google Palm API.
  - **Tham số**: Đảm bảo API key được nhập chính xác và có quyền truy cập vào Google Gemini.

- **Google Docs**: Node này sẽ lưu bản tóm tắt vào Google Docs.
  - **Credentials**: Cần cấu hình Google API.
  - **Tham số**: Nhập đúng URL của Google Doc mà bạn muốn lưu bản tóm tắt.

- **YouTube Transcript AI**: Node này sẽ lấy nội dung transcript từ video YouTube.
  - **Credentials**: Cần cấu hình RapidAPI.
  - **Tham số**: Đảm bảo API key và endpoint của YouTube Transcript API được nhập chính xác.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong các node quan trọng, hãy chạy thử workflow với dữ liệu mẫu.
2. Kiểm tra kết quả trên Google Docs để đảm bảo bản tóm tắt được lưu đúng như mong đợi.
3. Nếu mọi thứ hoạt động tốt, bạn có thể kích hoạt workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Bạn có thể thêm node để gửi thông báo khi bản tóm tắt hoàn thành.
- **Lưu log**: Thêm node để lưu log các lần chạy workflow để theo dõi hiệu suất.
- **Gửi báo cáo định kỳ**: Tự động gửi báo cáo tóm tắt qua email hoặc Slack hàng ngày.

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm thời gian và công sức trong việc tóm tắt nội dung video YouTube. Với công nghệ AI Google Gemini và Google Docs, bạn có thể tự động hóa toàn bộ quá trình này một cách dễ dàng. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của mình!