---
title: "🚀 Tự động hóa tổng kết video YouTube cho mạng xã hội bằng AI"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình tổng kết nội dung video YouTube thành bài viết sẵn sàng đăng lên mạng xã hội bằng n8n và Google Gemini"
slug: "tu-dong-hoa-tong-ket-video-youtube-cho-mang-xa-hoi"
tags: [n8n, automation, no-code, AI, Google Gemini]
keywords: [n8n workflow, tự động hóa, tổng kết video, mạng xã hội, Google Gemini]
---

# 🚀 Tự động hóa tổng kết video YouTube cho mạng xã hội bằng AI

[Các sếp] có biết không? Mỗi ngày bạn phải xem hàng chục video YouTube để tìm nội dung chất lượng cho mạng xã hội. Nhưng với workflow này, bạn chỉ cần nhập link video và AI sẽ tự động tổng kết nội dung thành bài viết sẵn sàng đăng lên Facebook, Instagram hay TikTok.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian** so với làm thủ công
- Tạo ra **nội dung chất lượng cao** với các điểm chính được tóm tắt rõ ràng
- **Tự động hóa hoàn toàn** quá trình từ lấy transcript đến viết bài
- **Cá nhân hóa** nội dung cho từng nền tảng mạng xã hội
- **Hoạt động liên tục** 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API key cho Google Gemini
- Tài khoản Google Drive để lưu trữ transcript
- Link video YouTube cần tổng kết
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5292](https://n8n.io/workflows/5292)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Thiết lập form với trường nhập "YouTube Video URL"
   - Tùy chỉnh giao diện form theo nhu cầu

2. **Node "Google Gemini Chat Model"**:
   - Tạo credential mới với tên "googlePalmApi"
   - Nhập API key từ Google Cloud Console
   - Đảm bảo tài khoản có quyền truy cập Google Gemini API

3. **Node "Google Docs"**:
   - Tạo credential mới với tên "googleApi"
   - Nhập thông tin xác thực Google
   - Điền "Document ID" của file Google Docs sẽ lưu transcript
   - Đảm bảo tài khoản có quyền chỉnh sửa file này

4. **Node "Youtube Transcriptor"**:
   - Không cần cấu hình gì thêm, node này sẽ tự động lấy transcript từ video

5. **Node "Mapper"**:
   - Kiểm tra các trường dữ liệu được truyền giữa các node
   - Đảm bảo các trường cần thiết được ánh xạ đúng

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trong Google Docs và các node tiếp theo
3. Sau khi test thành công, bật "Active" workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack/Telegram**: Thêm node gửi thông báo khi workflow hoàn thành
2. **Lưu log hoạt động**: Thêm node lưu log vào Google Sheets để theo dõi lịch sử
3. **Tự động đăng lên mạng xã hội**: Kết nối với các node Facebook, Instagram hay TikTok để tự động đăng bài
4. **Tùy chỉnh prompt**: Chỉnh sửa prompt trong node "AI Agent" để phù hợp với phong cách viết của bạn

### 📌 Kết luận
Workflow này không chỉ tiết kiệm thời gian mà còn giúp các sếp tạo ra nội dung chất lượng cao, phù hợp với từng nền tảng mạng xã hội. Hãy thử ngay và thấy sự khác biệt trong cách làm việc của bạn!