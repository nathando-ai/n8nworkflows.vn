---
title: "🚀 Tự động nén và lưu trữ PDF cũ từ Google Drive vào AWS S3 với báo cáo Slack"
description: "Giải pháp tự động 100% giúp doanh nghiệp di chuyển PDF cũ từ Google Drive sang AWS S3 cold storage, giảm chi phí lưu trữ và gửi báo cáo Slack hàng tuần."
slug: "tang-nhan-luu-tru-pdf-cu-gd-aws-s3-bao-cao-slack"
tags: [n8n, automation, no-code, google-drive, aws-s3, slack]
keywords: [n8n workflow, tự động hóa, compress pdf, google drive, aws s3, slack report]
---

# 🚀 Tự động nén và lưu trữ PDF cũ từ Google Drive vào AWS S3 với báo cáo Slack

Bạn đang phải loay hoay quản lý hàng nghìn file PDF trên Google Drive, chi phí lưu trữ tăng dần, và chưa có báo cáo nào để theo dõi tình trạng lưu trữ?  
Workflow này sẽ **đánh dấu** các file PDF đã cũ hơn 6 tháng, **nén** chúng để tiết kiệm dung lượng, **di chuyển** sang AWS S3 cold storage và **gửi báo cáo** qua Slack cho đội ngũ IT. Tất cả đều **không cần viết code** – chỉ cần cấu hình một vài credential và chạy.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí lưu trữ**: Di chuyển dữ liệu cũ sang cold storage giảm 70% chi phí.  
- **Tăng tính bảo mật**: Dữ liệu quan trọng được lưu trữ trong bucket S3, có thể thiết lập IAM chính sách nghiêm ngặt.  
- **Công việc tự động 24/7**: Không cần can thiệp thủ công, workflow chạy hàng tuần tự động.  
- **Báo cáo nhanh chóng**: Slack report cung cấp số lượng file, dung lượng đã giảm, thời gian thực hiện.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Drive**: Tài khoản OAuth2, folder ID của “Hot Storage”.  
- **HTML to PDF API**: API key cho dịch vụ n8n‑nodes‑htmlcsstopdf.  
- **AWS S3**: Bucket name, Access Key ID & Secret Access Key (hoặc IAM role).  
- **Slack**: OAuth2 token và ID kênh để gửi báo cáo.  
- **Luxon**: Đã được tích hợp sẵn trong node Code, không cần cài thêm.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/12655).  
2. Mở n8n Editor → **Import** → **Import from file** → chọn file JSON.  
3. Hoặc copy toàn bộ JSON và dán vào **Import from clipboard**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|--------------------|---------|
| `Trigger: Weekly Archive Scan` | `scheduleTrigger` | Thời gian chạy (ví dụ: `0 0 * * 1` – thứ 2 00:00) | Đặt theo nhu cầu doanh nghiệp |
| `List Active Project Files` | `googleDrive` | `folderId` (ID folder Hot Storage) | Sử dụng Google Drive OAuth2 |
| `Calculate File Age (Luxon Logic)` | `code` | Thay đổi `monthsThreshold` (mặc định 6) | Tính tuổi file |
| `IF: Meets Archive Criteria?` | `if` | `true` → tiếp tục, `false` → bỏ qua | Kiểm tra tuổi file |
| `Download Hot Storage Binary` | `googleDrive` | `fileId` (được truyền từ node trước) | Tải file PDF |
| `Compress PDF for Archival` | `htmlcsstopdf` | `apiKey` (đã cấu hình trong credentials) | Nén PDF |
| `Upload to Cold Storage (S3)` | `s3` | `bucketName`, `region`, `accessKeyId`, `secretAccessKey` | Đưa file vào bucket cold storage |
| `Log Savings to Slack` | `slack` | `channelId`, `message` (được cấu hình trong node) | Gửi báo cáo |

> **Tip**: Đối với node `code`, bạn có thể mở `Code` và chỉnh `monthsThreshold = 6;` hoặc thay đổi tùy ý.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (bấm “Execute Node”). Kiểm tra log, xem file đã được nén và upload đúng.  
2. **Bật Active**: Sau khi xác nhận, chuyển workflow sang trạng thái **Active** để tự động chạy theo lịch.

## ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo định kỳ**: Thêm node `scheduleTrigger` + `slack` để gửi báo cáo hàng ngày/tuần về dung lượng đã giảm.  
- **Lưu log vào Google Sheet**: Thêm node `googleSheets` để ghi lại danh sách file đã archive, ngày archive, dung lượng trước/đpués.  
- **Thêm Slack/Telegram**: Dùng node `slack` hoặc `telegram` để thông báo ngay khi có lỗi.  
- **Sử dụng Sticky Note**: Đặt node `stickyNote` giữa các bước để ghi chú nhanh cho người quản trị.  
- **Tự động tạo thư mục mới**: Nếu muốn lưu trữ theo năm/tháng, dùng node `googleDrive` để tạo folder mới trước khi upload.  

## 📌 Kết luận
Workflow “Compress and archive old Google Drive PDFs to AWS S3 cold storage with Slack reports” là giải pháp **đơn giản, hiệu quả** cho các doanh nghiệp muốn tối ưu chi phí lưu trữ và giữ cho dữ liệu luôn sạch sẽ.  
Hãy **đăng ký VPS**, **cấu hình credentials** và **đưa workflow lên n8n** ngay hôm nay để trải nghiệm tự động hóa 100% không cần code!