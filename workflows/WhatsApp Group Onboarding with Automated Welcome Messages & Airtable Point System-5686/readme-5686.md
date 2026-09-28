---
title: "🚀 WhatsApp Group Onboarding với Tin Nhắn Chào Mừng Tự Động & Hệ Thống Điểm Airtable"
description: "Tự động chào mừng thành viên mới trong nhóm WhatsApp, ghi nhận họ vào Airtable với điểm khởi đầu 100, hoàn toàn không cần code."
slug: "whatsapp-group-onboarding-automated-welcome-airtabled-point-system"
tags: [n8n, automation, no-code, whatsapp, airtable, social-media]
keywords: [n8n workflow, tự động hóa, WhatsApp, Airtable, điểm thưởng]
---

# 🚀 WhatsApp Group Onboarding với Tin Nhắn Chào Mừng Tự Động & Hệ Thống Điểm Airtable

Bạn đang quản lý một nhóm WhatsApp và phải chào mừng từng thành viên mới bằng tay? Bạn muốn ghi nhận họ vào hệ thống điểm thưởng ngay lập tức mà không cần viết code? Workflow này sẽ giúp bạn tự động hoá toàn bộ quy trình: từ nhận thông báo khi có thành viên mới, gửi tin nhắn chào mừng, kiểm tra điều kiện, đến ghi nhận vào Airtable với 100 điểm khởi đầu.  

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải chào mừng thủ công, tự động gửi tin nhắn ngay khi thành viên mới tham gia.  
- **Chính xác & nhất quán**: Mỗi thành viên nhận được cùng một tin nhắn chào mừng, tránh sai sót.  
- **Tích hợp điểm thưởng ngay lập tức**: Ghi nhận 100 điểm ngay khi đăng ký, giúp khuyến khích tham gia.  
- **Quản lý dữ liệu dễ dàng**: Tất cả thông tin được lưu trữ trong Airtable, có thể xuất báo cáo, phân tích.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Tài khoản / Dịch vụ | Mô tả | Cách lấy |
|----------------------|-------|----------|
| **Whapi API Key** | Dùng để gửi tin nhắn WhatsApp qua HTTP Request. | Đăng ký tại [Whapi](https://whapi.io/) và lấy API Key. |
| **Airtable API Key** | Dùng để tạo bản ghi trong bảng Airtable. | Vào trang Airtable, Settings → API → Generate API Key. |
| **Airtable Base ID & Table Name** | Định danh bảng lưu điểm. | Từ URL Airtable (Base ID) và tên bảng trong UI. |
| **Group ID (WhatsApp)** | ID nhóm cần kiểm tra trong filter. | Từ URL nhóm WhatsApp hoặc qua API. |
| **Webhook Path** | Đường dẫn nhận POST từ Whapi. | Được tạo khi xuất workflow, ví dụ `0d328573-da59-489e-8f2f-784aa4c19b82`. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/5686).  
2. Mở n8n Editor → `Workflows` → `Import`.  
3. Chọn file JSON và nhấn **Import**. Workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần chỉnh | Ghi chú |
|------|--------------------|---------|
| **Webhook – New group participant** | `path` = `0d328573-da59-489e-8f2f-784aa4c19b82` (hoặc đường dẫn bạn muốn) | Đảm bảo URL webhook được Whapi gọi. |
| **Filter – Filter** | `Conditions` → `group_id` = ID nhóm của bạn, `action` = `"add"` | Kiểm tra đúng nhóm và hành động thêm. |
| **HTTP Request – Welcome WhatsApp message** | `URL` = `https://api.whapi.io/v1/messages`, `Method` = `POST`, `Body` = JSON chứa `to`, `message`, `api_key` = Whapi API Key | Định dạng body: `{"to":"{{ $json[\"from\"] }}","message":"Chào mừng bạn đã tham gia nhóm! ...","api_key":"YOUR_WHAPI_KEY"}` |
| **Airtable – Airtable Create** | `Base ID`, `Table Name`, `Operation` = `create`, `Fields` = `WhatsApp ID`, `Points`, `Last Interaction` | Điền Base ID và Table Name, sau đó map các trường từ dữ liệu webhook. |
| **Credentials** | Đặt `Whapi API Key` và `Airtable API Key` trong phần Credentials của n8n. | Đảm bảo credentials đã được lưu trong n8n. |

### 3. Kích hoạt ⚡️
1. **Test run**: Chọn một webhook URL, gửi POST mẫu từ Whapi (hoặc dùng Postman) để kiểm tra.  
2. Kiểm tra log: Đảm bảo tin nhắn được gửi, bản ghi Airtable được tạo.  
3. Khi mọi thứ ổn, bật **Active** cho workflow. Workflow sẽ chạy tự động mỗi khi có thành viên mới.

## ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack**: Thêm node `Slack` để gửi tin nhắn khi thành viên mới được chào mừng.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại lịch sử chào mừng.  
- **Tự động gửi báo cáo điểm**: Sử dụng node `Schedule` để gửi email hàng tuần tới quản trị viên với bảng điểm.  
- **Tích hợp Telegram**: Gửi tin nhắn chào mừng qua Telegram bot nếu muốn đa kênh.  

## 📌 Kết luận
Workflow “WhatsApp Group Onboarding với Tin Nhắn Chào Mừng Tự Động & Hệ Thống Điểm Airtable” giúp bạn tiết kiệm thời gian, giảm lỗi và nâng cao trải nghiệm người dùng ngay từ lần đầu tham gia. Hãy thử ngay, tùy chỉnh cho phù hợp với nhóm của mình và cảm nhận sự khác biệt!  

> **Tác giả**: David w/ SimpleGrow – chuyên gia tự động hóa n8n, giúp doanh nghiệp tối ưu quy trình, giảm chi phí và tăng hiệu quả.  
> **Link gốc**: https://n8n.io/workflows/5686