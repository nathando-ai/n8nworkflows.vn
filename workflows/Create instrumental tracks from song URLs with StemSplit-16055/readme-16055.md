---
title: "🚀 Tạo track instrumental từ URL bài hát bằng StemSplit"
description: "Tự động tách vocal, tải lên Google Drive và gửi link tải về cho người dùng qua email – hoàn toàn không cần code."
slug: "tao-track-instrumental-tu-url-bai-hat-bang-stemsplit"
tags: [n8n, automation, no-code, stemsplit, google-drive, gmail]
keywords: [n8n workflow, tự động hóa, stemsplit, karaoke instrumental, tách vocal, google drive, gmail]
---

# 🚀 Tạo track instrumental từ URL bài hát bằng StemSplit

Bạn là chủ karaoke, DJ, giáo viên âm nhạc hay một nhóm cộng đồng muốn cho khách hàng gửi yêu cầu “instrumental” mà không cần phải xử lý thủ công?  
Workflow này sẽ nhận dữ liệu từ một form, kiểm tra URL, tách vocal bằng StemSplit, tải lên Google Drive và gửi link tải về cho người gửi – tất cả tự động, 100% không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần xử lý thủ công từng yêu cầu.  
- **Độ chính xác cao**: StemSplit tách vocal một cách tự động, giảm lỗi con người.  
- **Tự động hoá liên tục**: Workflow chạy 24/7, không phụ thuộc vào giờ làm việc.  
- **Dễ dàng quản lý**: File được lưu trữ ngay trong Google Drive, link gửi qua Gmail.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ | Mô tả | Lưu ý |
|---------|-------|-------|
| **StemSplit API** | API key từ trang [stemsplit.io](https://stemsplit.io/app/settings/api) | Cần đặt vào hai node StemSplit (`getBalance` và `separateStemsWait`). |
| **Google Drive OAuth2** | Đăng nhập Google Drive, cấp quyền đọc/ghi | Đặt trong node `Upload to Google Drive`. |
| **Gmail OAuth2** | Đăng nhập Gmail, cấp quyền gửi email | Đặt trong ba node Gmail (`send download link`, `invalid URL notice`, `insufficient credits`). |
| **n8n-nodes-stemsplit** | Node plugin StemSplit | Cài đặt nếu chưa có: `npm i n8n-nodes-stemsplit` hoặc qua UI. |
| **Form Trigger** | URL form n8n | Lấy URL từ node `On karaoke form submission`. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
- Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/16055) hoặc copy toàn bộ JSON.  
- Trong n8n Editor, chọn **Import** → **Import from JSON** → dán JSON → **Import**.  
- Workflow sẽ xuất hiện với 11 node chính.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Tham số cần cấu hình | Ghi chú |
|------|----------|----------------------|---------|
| 1 | `On karaoke form submission` | **Production URL** (được copy sau import) | Đây là link mà khách hàng sẽ điền dữ liệu. |
| 2 | `Normalize form data` | `Set` → `email`, `songTitle`, `songUrl` | Đảm bảo dữ liệu được chuẩn hóa. |
| 3 | `Is song URL valid?` | `if` → điều kiện kiểm tra `songUrl` có chứa `http` và mở được không | Nếu sai → chuyển sang node `Gmail: invalid URL notice`. |
| 4 | `StemSplit: check credits` | `operation: getBalance` | Trả về số credit còn lại. |
| 5 | `Enough StemSplit credits?` | `if` → `balance >= 60` (đơn vị: giây) | Nếu chưa đủ → chuyển sang node `Gmail: insufficient credits`. |
| 6 | `StemSplit: create instrumental` | `operation: separateStemsWait` → `songUrl` | Đợi cho tới khi StemSplit trả về file MP3. |
| 7 | `Download instrumental MP3` | `httpRequest` → `URL` lấy từ node 6 | Tải file MP3. |
| 8 | `Upload to Google Drive` | `operation: upload`, `resource: file`, `folderId` (tuỳ chọn) | Đặt tên file = `songTitle` + `.mp3`. |
| 9 | `Gmail: send download link` | `to`: `{{ $json.email }}`, `subject`: “Instrumental của {{ $json.songTitle }}”, `body`: link Google Drive | Gửi link tải về. |
| 10 | `Gmail: invalid URL notice` | `to`: `{{ $json.email }}`, `subject`: “URL không hợp lệ”, `body`: thông báo lỗi | Gửi khi URL sai. |
| 11 | `Gmail: insufficient credits` | `to`: `{{ $json.email }}`, `subject`: “Credits không đủ”, `body`: thông báo thiếu credit | Gửi khi credit thấp. |

> **Tip**: Kiểm tra lại các credentials trong từng node trước khi bật workflow.

### 3. Kích hoạt ⚡️
1. **Test run**: Chọn một URL MP3 công khai (ví dụ: `https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3`) và gửi qua form.  
2. Kiểm tra Google Drive xem file đã xuất hiện chưa.  
3. Kiểm tra email nhận link.  
4. Khi mọi thứ hoạt động, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram notification**: Thêm node Slack/Telegram để nhận thông báo khi một yêu cầu mới được xử lý.  
- **Log file**: Sử dụng node `Write Binary File` để lưu log tách vocal vào Google Drive.  
- **Thời gian chờ tối ưu**: Nếu muốn giảm thời gian chờ, có thể cấu hình `separateStemsWait` với `maxWaitTime`.  
- **Quản lý credit**: Thêm node `Set` để hiển thị số credit còn lại trong email gửi về.  

## 📌 Kết luận
Workflow “Tạo track instrumental từ URL bài hát bằng StemSplit” giúp bạn tiết kiệm thời gian, giảm sai sót và mang lại trải nghiệm tự động hoá tuyệt vời cho khách hàng.  
Hãy thử ngay, bật workflow, chia sẻ link form và xem khách hàng nhận được instrumental ngay lập tức!