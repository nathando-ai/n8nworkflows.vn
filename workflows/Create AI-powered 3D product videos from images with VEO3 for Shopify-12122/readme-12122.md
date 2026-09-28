---
title: "🚀 Tạo video sản phẩm 3D AI từ ảnh với VEO3 cho Shopify"
description: "Tự động tạo video 3D sản phẩm từ ảnh, giảm thời gian và công sức, nâng cao trải nghiệm khách hàng trên Shopify."
slug: "tang-video-3d-ai-tu-anh-voi-veo3-shopify"
tags: [n8n, automation, no-code, Shopify, AI, video]
keywords: [n8n workflow, tự động hóa, video 3D AI, Shopify, VEO3, AI automation]
---

# 🚀 Tạo video sản phẩm 3D AI từ ảnh với VEO3 cho Shopify

Bạn đang quản lý cửa hàng Shopify và muốn làm nổi bật sản phẩm bằng video 3D? Việc tạo video thủ công tốn thời gian, chi phí và đòi hỏi kỹ năng thiết kế. Workflow này giúp bạn **tự động** lấy ảnh sản phẩm, loại bỏ nền, phân tích nội dung, tạo video 3D bằng VEO3, và cập nhật liên kết video vào Google Sheets – toàn bộ quá trình diễn ra **không cần code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ tạo video thủ công xuống chỉ vài phút.
- **Độ chính xác cao**: Hình ảnh nền được loại bỏ tự động, video 3D được tạo theo mô tả AI.
- **Tự động cập nhật**: Liên kết video được ghi vào Google Sheets ngay sau khi hoàn thành.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào người dùng.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Drive**: Tạo thư mục chia sẻ cho workflow, cấp quyền đọc/ghi.
- **Google Sheets**: Tạo bảng tính với các cột: `Product ID`, `Image URL`, `Video URL`, `Remove BG URL`, v.v.
- **OpenAI**: API key để phân tích ảnh và tạo prompt cho VEO3.
- **VEO3 API**: Key và endpoint để tạo video 3D.
- **Gmail**: Tài khoản gửi email thông báo.
- **Discord**: Tên webhook để gửi tin nhắn.
- **Rapiwa**: Tài khoản và API key (nếu sử dụng).
- **Form (Google Forms hoặc Typeform)**: Gửi dữ liệu khi người dùng nhập thông tin sản phẩm.
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: <https://n8n.io/workflows/12122>.
2. Mở n8n Editor, chọn **Import** → **Import from file** → chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào ô **Import from JSON**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **On Form Submission** | Trigger khi form được gửi | URL webhook của form |
| **Give Access to folder** | Cấp quyền truy cập thư mục Google Drive | ID thư mục |
| **Get Image File** | Lấy file ảnh từ Google Drive | ID file |
| **Upload Remove BG image** | Tải ảnh đã loại nền lên Drive | ID thư mục, tên file |
| **Create Folder** | Tạo thư mục mới cho video | Tên thư mục (được sinh từ Product ID) |
| **Remove Image Background** | Gọi API loại nền | URL ảnh, API key |
| **Insert New Product** | Thêm dòng mới vào Google Sheets | Sheet name, dữ liệu |
| **Update Video Link** | Cập nhật liên kết video | Sheet name, row ID, URL |
| **Get row(s) in sheet** | Lấy dữ liệu dòng hiện tại | Sheet name, row ID |
| **AI Agent** | Xử lý logic AI | Prompt, dữ liệu đầu vào |
| **Rapiwa** | Gửi dữ liệu tới Rapiwa (nếu cần) | API key, payload |
| **Send a message** | Gửi email thông báo | To, Subject, Body |
| **Post on message** | Gửi tin nhắn Discord | Webhook URL, message |
| **OpenAI** | Phân tích ảnh | API key, prompt |
| **Think** | Lập kế hoạch AI | Tool, prompt |
| **Parser Output** | Phân tích output của AI | Schema |
| **Download Video** | Tải video từ VEO3 | Video ID, API key |
| **Check Video Status** | Kiểm tra trạng thái video | Video ID |
| **Analyze image** | Phân tích nội dung ảnh | API key, image URL |
| **if** | Điều kiện logic | Thông số điều kiện |
| **Generation Video using VEO3** | Tạo video 3D | Prompt, API key |
| **Update Remove BG URL** | Cập nhật URL ảnh đã loại nền | Sheet name, row ID, URL |
| **Wait 20s** | Đợi 20 giây trước khi tiếp tục | N/A |

> **Lưu ý**: Mỗi node cần **đăng ký credentials** trong phần **Credentials** của n8n. Đảm bảo rằng các API key và token được bảo mật và có quyền truy cập đầy đủ.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (bấm **Execute Workflow**).
2. Kiểm tra logs, đảm bảo không có lỗi.
3. Khi mọi thứ ổn, bật **Active** để workflow tự động chạy khi form được gửi.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram**: Thay vì Discord, bạn có thể gửi thông báo tới Slack hoặc Telegram bằng webhook.
- **Lưu log**: Thêm node `Code` để ghi log vào Google Sheets hoặc Cloud Logging.
- **Báo cáo định kỳ**: Sử dụng node `Cron` để gửi báo cáo video đã tạo hàng ngày.
- **Tùy chỉnh prompt**: Thêm biến `Product Description` vào prompt để AI tạo video phù hợp hơn.
- **Quản lý lỗi**: Sử dụng node `If` để kiểm tra trạng thái API và gửi email cảnh báo khi có lỗi.

## 📌 Kết luận
Workflow “Create AI-powered 3D product videos from images with VEO3 for Shopify” là công cụ mạnh mẽ giúp các sếp tự động hóa quy trình tạo video 3D cho sản phẩm Shopify. Bằng cách kết hợp Google Drive, Google Sheets, OpenAI, VEO3 và các dịch vụ thông báo, bạn có thể giảm thiểu công sức, tăng tính nhất quán và nâng cao trải nghiệm khách hàng. Hãy **cài đặt ngay** và trải nghiệm sự tự động hóa hoàn toàn!

---