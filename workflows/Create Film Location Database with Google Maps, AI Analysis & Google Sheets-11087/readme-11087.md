---
title: "🚀 Tự động tìm kiếm địa điểm phim: Google Maps + AI + Google Sheets"
description: "Giải pháp tự động 100% không cần code để tìm kiếm, phân tích và lưu trữ địa điểm phim, đồng thời gửi thông báo qua Slack."
slug: "tuyendung-tim-kiem-dia-diem-phim-voi-google-maps-ai-google-sheets"
tags: [n8n, automation, no-code, google-maps, ai, google-sheets, slack]
keywords: [n8n workflow, tự động hóa, tìm kiếm địa điểm phim, AI phân tích, Google Sheets, Slack notification]
---

# 🚀 Tự động tìm kiếm địa điểm phim: Google Maps + AI + Google Sheets

Bạn đang làm việc trong lĩnh vực sản xuất phim, truyền hình hoặc nội dung sáng tạo và cần một công cụ nhanh chóng, chính xác để tìm kiếm, đánh giá và lưu trữ các địa điểm quay phim?  
Workflow **Create Film Location Database with Google Maps, AI Analysis & Google Sheets** của **Yoshino Haruki** đã được thiết kế để giải quyết mọi nỗi đau này:

- **Tìm kiếm** địa điểm qua Google Places API chỉ với một từ khóa.
- **Phân tích** AI (OpenRouter) viết “Director’s Commentary” cho từng địa điểm.
- **Lưu trữ** dữ liệu vào Google Sheets một cách tự động.
- **Thông báo** ngay trên Slack khi hoàn thành.

Bạn không cần viết bất kỳ dòng code nào, chỉ cần cấu hình vài credential và workflow sẽ chạy 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ việc tìm kiếm thủ công tới lưu trữ dữ liệu chỉ mất vài phút.  
- **Chính xác & nhất quán**: Dữ liệu được lấy trực tiếp từ API Google, phân tích bởi AI, tránh sai sót do con người.  
- **Cá nhân hóa**: AI viết “Director’s Commentary” theo phong cách riêng, giúp nội dung phong phú hơn.  
- **Hoạt động liên tục**: Khi workflow được kích hoạt, mọi thao tác diễn ra tự động, không cần can thiệp.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ / Credential | Mô tả | Cách lấy |
|-----------------------|-------|----------|
| **Google Places API Key** | Dùng để truy vấn Google Maps Places | Google Cloud Console → APIs & Services → Library → Places API → Enable → Credentials |
| **Google Sheets API** | Dùng để ghi dữ liệu vào bảng tính | Google Cloud Console → APIs & Services → Library → Sheets API → Enable → Credentials (OAuth 2.0 Client ID) |
| **Slack Bot Token** | Dùng để gửi thông báo | Slack API → Apps → Create an app → OAuth & Permissions → Bot Token |
| **OpenRouter API Key** | Dùng cho mô hình AI (Chat) | Đăng ký tại https://openrouter.ai/ → API Keys |
| **Workflow Configuration Node** | Cập nhật các key, ID, URL | Node “Workflow Configuration” trong workflow |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/11087) hoặc sao chép nội dung JSON.  
2. Mở n8n Editor → **Import** → **Import from file** hoặc **Import from clipboard**.  
3. Đảm bảo chọn **Overwrite existing workflow** nếu muốn thay thế.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Thông tin cần cấu hình | Ghi chú |
|------|----------|------------------------|---------|
| **Chat Trigger** | `Chat Trigger` | Không cần credential, chỉ cần cấu hình “Trigger” (ví dụ: Slack message, Discord, Telegram). | Đây là điểm khởi đầu khi sếp gửi lệnh. |
| **Simple Memory** | `Simple Memory` | `memoryBufferWindow` – không cần credential. | Dùng lưu trữ tạm thời cho các biến. |
| **Workflow Configuration** | `Workflow Configuration` | `set` – nhập **Google Places API Key**, **Google Sheets ID**, **Slack Channel ID**, **OpenRouter API Key**. | Đây là node quan trọng nhất, hãy chắc chắn các key đúng. |
| **Google Maps Places Search** | `Google Maps Places Search` | `httpRequest` – URL: `https://maps.googleapis.com/maps/api/place/textsearch/json?query={{$json["keyword"]}}&key={{$json["googlePlacesApiKey"]}}` | Thay `keyword` bằng từ khóa nhập vào. |
| **Loop Over Items** | `Loop Over Items` | `splitInBatches` – `Batch Size`: 5 (hoặc tùy ý). | Giúp tránh vượt quota API. |
| **AI Location Analyzer** | `AI Location Analyzer` | `agent` – cấu hình `OpenRouter Chat Model` (OpenRouter API Key), `Prompt` (định dạng “Director’s Commentary”). | Đảm bảo prompt rõ ràng, tránh lỗi. |
| **OpenRouter Chat Model** | `OpenRouter Chat Model` | `lmChatOpenRouter` – API Key, mô hình (ví dụ: `gpt-4o-mini`). | Kiểm tra quota và chi phí. |
| **Append to Google Sheets** | `Append to Google Sheets` | `googleSheets` – `operation: append`, Sheet ID, Range (ví dụ: `Sheet1!A:E`). | Đảm bảo bảng tính có header đúng thứ tự. |
| **Send Slack Notification** | `Send Slack Notification` | `slack` – Channel ID, message text. | Gửi thông báo khi hoàn thành. |
| **Limit** | `Limit` | `limit` – `maxItems`: 10 (hoặc tùy ý). | Giới hạn số lượng địa điểm để tránh chi phí cao. |
| **Split Out** | `Split Out` | `splitOut` – `output`: `data`. | Dùng để lấy dữ liệu cuối cùng cho Slack. |
| **Sticky Note** | `Sticky Note` | Không cần cấu hình. | Dùng ghi chú nội bộ. |

> **Lưu ý**: Mỗi node có thể có nhiều tham số tùy chỉnh. Đọc kỹ tài liệu của node trong n8n để hiểu rõ hơn.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với một keyword mẫu (ví dụ: “Cyberpunk streets in Tokyo”).  
2. Kiểm tra dữ liệu trong Google Sheets và Slack.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.  

## ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram**: Thay `Chat Trigger` bằng `Telegram Trigger` để nhận lệnh qua bot Telegram.  
- **Lưu log**: Thêm node `Write Binary File` để ghi log vào Google Drive hoặc S3.  
- **Báo cáo định kỳ**: Sử dụng `Cron` node để gửi báo cáo hàng ngày/tuần qua Slack hoặc Email.  
- **Phân loại địa điểm**: Thêm một node `Function` để phân loại địa điểm theo thể loại (đoạn phim, quảng cáo, v.v.) trước khi ghi vào Sheets.  

## 📌 Kết luận
Workflow này là công cụ “điện thoại” cho các sếp trong ngành phim, giúp tiết kiệm thời gian, giảm sai sót và tăng tính sáng tạo.  
Hãy thử ngay, tùy chỉnh theo nhu cầu và chia sẻ kết quả với cộng đồng n8n!  

> **Cách tiếp cận**: Bắt đầu với một keyword đơn giản, xem kết quả, rồi mở rộng scope.  
> **Hỗ trợ**: Nếu gặp khó khăn, hãy mở issue trên GitHub của workflow hoặc tham gia cộng đồng n8n.  

Chúc các sếp thành công và có nhiều “địa điểm tuyệt vời” cho dự án sắp tới!