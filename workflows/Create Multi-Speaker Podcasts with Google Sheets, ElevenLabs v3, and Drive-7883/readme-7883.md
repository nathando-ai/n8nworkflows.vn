---
title: "🚀 Tạo Podcast Đa Diễn Đàn Tự Động với Google Sheets, ElevenLabs v3 và Drive"
description: "Hướng dẫn chi tiết cách tự động tạo podcast đa diễn viên từ dữ liệu Google Sheets, chuyển đổi sang audio với ElevenLabs v3 và lưu trữ lên Google Drive – hoàn toàn không cần code."
slug: "tao-podcast-da-diien-dan-tu-dong"
tags: [n8n, automation, no-code, google-sheets, elevenlabs, podcast]
keywords: [n8n workflow, tự động hóa, podcast, google sheets, elevenlabs, text to speech, multi-speaker]
---

# 🚀 Tạo Podcast Đa Diễn Đàn Tự Động với Google Sheets, ElevenLabs v3 và Drive

Bạn đang muốn tạo podcast chuyên nghiệp mà không cần viết code?  
Workflow này sẽ giúp bạn **đọc nội dung từ Google Sheets**, **chuyển thành audio đa diễn viên** bằng ElevenLabs v3, và **lưu trữ tệp audio lên Google Drive** chỉ với một cú click “Execute workflow”.  
Tất cả đều được tự động hoá 100% – tiết kiệm thời gian, giảm sai sót và nâng cao chất lượng nội dung.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động lấy dữ liệu, tạo audio, lưu trữ – không cần thao tác thủ công.  
- **Chính xác & nhất quán**: Nội dung luôn được lấy từ nguồn duy nhất (Google Sheets).  
- **Cá nhân hóa**: Mỗi diễn viên có giọng nói riêng, có thể thêm hiệu ứng âm thanh.  
- **Hoạt động liên tục**: Workflow có thể chạy bất cứ lúc nào, kể cả ngoài giờ làm việc.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ / Tài khoản | Mô tả | Lưu ý |
|---------------------|-------|-------|
| **Google Sheets** | Tạo bảng dữ liệu với các cột: *Speaker ID*, *Voice ID*, *Dialogue*. | Đảm bảo bảng được chia sẻ công khai hoặc chia sẻ với tài khoản n8n. |
| **Google Drive** | Lưu trữ tệp audio cuối cùng. | Cần cấp quyền truy cập đầy đủ (đọc/ghi). |
| **ElevenLabs** | API Key và Voice ID cho từng diễn viên. | Đăng ký tài khoản miễn phí, lấy API Key từ trang dashboard. |
| **n8n** | Self-hosted hoặc n8n.cloud. | Cài đặt phiên bản mới nhất để hỗ trợ các node cần thiết. |
| **API Key ElevenLabs** | Đặt trong node *Generate podcast* (header `xi-api-key`). | Đặt đúng key, tránh lỗi 401. |
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/7883).  
2. Trong n8n Editor, chọn **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** để tải workflow vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Credentials cần thiết | Tham số cần cấu hình |
|------|----------|-----------------------|----------------------|
| 1 | `When clicking ‘Execute workflow’` | Không cần | - |
| 2 | `Upload file` | `googleDriveOAuth2Api` | *Folder ID* (đường dẫn lưu trữ) |
| 3 | `Generate podcast` | `httpHeaderAuth` | Header: `xi-api-key: YOUR_API_KEY` |
| 4 | `Get dialogue` | `googleSheetsOAuth2Api` | *Spreadsheet ID*, *Sheet Name* |
| 5 | `Prepare dialogue` | Không cần | Định dạng prompt (đọc thêm phần *Tips* dưới). |

- **Google Sheets**: Đảm bảo bảng có ít nhất 3 cột: `Speaker ID`, `Voice ID`, `Dialogue`.  
- **ElevenLabs**: Trong cột `Voice ID`, ghi ID giọng nói tương ứng với diễn viên.  
- **Prompt**: Node *Prepare dialogue* sẽ chuyển dữ liệu thành chuỗi JSON phù hợp với API ElevenLabs. Bạn có thể chỉnh sửa logic trong node *Code* nếu muốn thêm tags hoặc hiệu ứng.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (bấm “Execute workflow”). Kiểm tra log, xem tệp audio được tạo và lưu trữ.  
2. **Bật Active**: Khi mọi thứ ổn, bật toggle “Active” để workflow tự động chạy khi có trigger.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: Gửi thông báo khi podcast đã hoàn thành.  
- **Lưu log**: Dùng node *Google Sheets* hoặc *File* để ghi lại lịch sử tạo podcast.  
- **Báo cáo định kỳ**: Sử dụng *Cron* node để tự động tạo podcast hàng ngày/tuần.  
- **Hiệu ứng âm thanh**: Sử dụng các tags như `[laughs]`, `[clapping]` trong prompt để làm phong phú hơn nội dung.  
- **Đa ngôn ngữ**: Thêm cột `Language` và điều chỉnh API key tương ứng.

### 📌 Kết luận
Workflow “Create Multi‑Speaker Podcasts with Google Sheets, ElevenLabs v3, and Drive” là công cụ mạnh mẽ giúp các sếp chuyển đổi nhanh chóng từ dữ liệu văn bản sang podcast chuyên nghiệp, tiết kiệm thời gian và công sức.  
Hãy thử ngay, tùy chỉnh theo nhu cầu và chia sẻ kết quả với cộng đồng n8n!