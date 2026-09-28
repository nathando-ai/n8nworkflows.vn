---
title: "🚀 Gửi lời mời kết nối LinkedIn tới bình luận viên bài viết đối thủ qua ConnectSafely.ai"
description: "Tự động lấy danh sách bình luận viên của bài viết LinkedIn, lọc, và gửi lời mời kết nối 100% không cần code – tiết kiệm thời gian, tăng độ chính xác, và tối ưu quy trình lead generation."
slug: "gửi-lời-mời-kết-nối-linkedin-bình-đánh-đối-thủ"
tags: [n8n, automation, no-code, lead-generation, linkedin, connect-safely]
keywords: [n8n workflow, tự động hóa, LinkedIn, lead generation, ConnectSafely]
---

# 🚀 Gửi lời mời kết nối LinkedIn tới bình luận viên bài viết đối thủ qua ConnectSafely.ai

Bạn đang gặp khó khăn khi phải thủ công tìm kiếm, lọc và gửi lời mời kết nối tới những người đã bình luận trên bài viết của đối thủ?  
Workflow này sẽ **tự động** lấy danh sách bình luận viên (đến 500 người), lọc ra những người không thuộc đối thủ, kiểm tra giới hạn gửi hàng ngày, và gửi lời mời kết nối một cách thông minh, 24/7 – **không cần viết code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ làm thủ công xuống vài phút tự động.  
- **Chính xác cao**: Lọc tự động người không thuộc đối thủ, tránh gửi spam.  
- **Tối ưu quy trình**: Giới hạn gửi hàng ngày, tránh bị LinkedIn hạn chế tài khoản.  
- **Hoạt động liên tục**: Khi đạt giới hạn, workflow tự động chờ đến ngày mới và tiếp tục.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản ConnectSafely.ai** với quyền truy cập API.  
- **Credentials**: `httpBearerAuth` hoặc `httpHeaderAuth` (được dùng trong các node HTTP Request).  
- **Form Trigger**: Cần cấu hình form để nhập URL bài viết và template tin nhắn.  
- **Daily limit**: Mặc định 8 lời mời mỗi ngày (có thể điều chỉnh trong node *Set Config*).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/13094).  
2. Trong n8n, vào **Workflows → Import** và chọn file JSON.  
3. Hoặc copy toàn bộ JSON và dán vào **n8n Editor → Import → Paste JSON**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Mô tả | Cấu hình cần chỉnh |
|------|----------|-------|---------------------|
| **Form Trigger** | `Form Trigger` | Nhận URL bài viết & template tin nhắn. | Không cần chỉnh. |
| **Set Config** | `Set Config` | Đặt `dailyLimit`, `messageTemplate`. | Chỉnh `dailyLimit` (định số) và `messageTemplate` (định chuỗi). |
| **Get Comments** | `Get Comments` | Gọi API ConnectSafely để lấy bình luận. | Chọn **Credentials**: `httpBearerAuth` hoặc `httpHeaderAuth`. |
| **Extract Profiles** | `Extract Profiles` | Phân tích JSON trả về, lấy danh sách profile. | Không cần chỉnh. |
| **Loop** | `Loop` | Lặp qua từng profile. | Không cần chỉnh. |
| **Check Limit** | `Check Limit` | Kiểm tra số lần gửi hôm nay. | Không cần chỉnh. |
| **Limit Reached?** | `Limit Reached?` | Nếu đã đạt giới hạn, chuyển sang `Wait Until Tomorrow`. | Không cần chỉnh. |
| **Wait Until Tomorrow** | `Wait Until Tomorrow` | Chờ đến ngày mới. | Không cần chỉnh. |
| **Wait** | `Wait` | Chờ 3 giây giữa mỗi lần gửi. | Có thể điều chỉnh thời gian (đơn vị ms). |
| **Get Profile** | `Get Profile` | Lấy thông tin chi tiết profile. | Chọn **Credentials**: `httpBearerAuth` hoặc `httpHeaderAuth`. |
| **Prepare & Filter** | `Prepare & Filter` | Lọc ra những người không thuộc đối thủ. | Không cần chỉnh. |
| **Should Send?** | `Should Send?` | Kiểm tra điều kiện gửi. | Không cần chỉnh. |
| **Send Connection** | `Send Connection` | Gửi lời mời kết nối. | Chọn **Credentials**: `httpBearerAuth` hoặc `httpHeaderAuth`. |
| **Log & Increment** | `Log & Increment` | Ghi log và tăng counter. | Không cần chỉnh. |
| **Aggregate** | `Aggregate` | Tổng hợp kết quả. | Không cần chỉnh. |
| **Summary** | `Summary` | Tạo báo cáo cuối cùng. | Không cần chỉnh. |

> **Lưu ý**: Mỗi node **HTTP Request** đều cần **Credentials** `httpBearerAuth` hoặc `httpHeaderAuth`. Đăng ký tài khoản ConnectSafely.ai, lấy **API Key** và tạo credential trong n8n.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (URL bài viết hợp lệ). Kiểm tra log, đảm bảo không có lỗi.  
2. **Bật Active**: Khi mọi thứ ổn, bật **Active** để workflow tự động chạy khi form được submit.  

## ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` trong node *Log & Increment* để nhận thông báo khi gửi thành công hoặc lỗi.  
- **Lưu log vào Google Sheets**: Thêm node `Google Sheets` trong *Log & Increment* để ghi lại danh sách đã gửi.  
- **Báo cáo định kỳ**: Sử dụng node `Cron` để gửi báo cáo tổng hợp qua email hoặc Slack mỗi ngày.  
- **Tăng giới hạn**: Nếu cần gửi nhiều hơn, tăng `dailyLimit` trong node *Set Config* và kiểm tra giới hạn của LinkedIn.  
- **Chỉnh thời gian chờ**: Nếu gặp rate‑limit, tăng thời gian trong node *Wait 3s* (đơn vị ms).  

## 📌 Kết luận
Workflow này giúp các sếp **tự động hoá toàn bộ quy trình** từ lấy danh sách bình luận viên, lọc, gửi lời mời, đến báo cáo kết quả – **điều khiển 100% không cần code**.  
Hãy thử ngay, điều chỉnh `dailyLimit` và `messageTemplate` theo nhu cầu, và tận dụng sức mạnh của ConnectSafely.ai để mở rộng mạng lưới LinkedIn một cách hiệu quả nhất!