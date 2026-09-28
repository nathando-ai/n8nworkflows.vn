---
title: "🚀 Gửi thông báo lỗi tự động qua Gmail cho workflow n8n"
description: "Giải pháp tự động gửi email khi bất kỳ workflow nào gặp lỗi, giúp đội ngũ DevOps nhanh chóng phát hiện và khắc phục sự cố."
slug: "giao-thong-loi-tro-gmail-n8n"
tags: [n8n, automation, no-code, devops, gmail]
keywords: [n8n workflow, tự động hóa, thông báo lỗi, Gmail, DevOps]
---

# 🚀 Gửi thông báo lỗi tự động qua Gmail cho workflow n8n

Bạn đang chạy nhiều workflow n8n trong môi trường DevOps và luôn lo lắng khi một workflow bất ngờ dừng lại vì lỗi?  
Đừng lo! Workflow “Automatic Workflow Error Notifications via Gmail” sẽ tự động gửi email ngay khi bất kỳ workflow nào gặp lỗi, giúp các sếp nhanh chóng nhận biết và khắc phục sự cố mà không cần phải kiểm tra thủ công từng workflow.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi từng workflow thủ công.  
- **Chính xác**: Email chỉ gửi khi có lỗi thực sự, tránh spam.  
- **Cá nhân hóa**: Gửi tới email cá nhân hoặc danh sách nhóm.  
- **Hoạt động liên tục**: Được kích hoạt ngay khi lỗi xảy ra, ngay cả khi workflow đang chạy 24/7.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản Gmail** (hoặc tài khoản Google Workspace) đã bật **API Gmail** và **OAuth 2.0**.  
- **Credentials** của Gmail trong n8n (đã được tạo trong phần Credentials → Gmail).  
- **Email nhận thông báo** (địa chỉ email cá nhân hoặc danh sách nhóm).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/6920) hoặc sao chép nội dung JSON.  
2. Mở n8n Editor → **File → Import Workflow** → dán JSON hoặc tải file.  
3. Lưu workflow với tên “Automatic Workflow Error Notifications via Gmail”.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Hướng dẫn cấu hình |
|------|----------|---------------------|
| **Error Trigger** | `Error Trigger` | Không cần cấu hình thêm. Node này sẽ tự động nhận dữ liệu lỗi khi bất kỳ workflow nào kích hoạt. |
| **Gmail** | `Send a message` | - Mở node Gmail → **Connect Credentials** → chọn Gmail credentials đã tạo. <br> - **To**: Nhập email nhận thông báo (địa chỉ cá nhân hoặc danh sách nhóm). <br> - **Subject**: `Error in {{$json["workflow"]["name"]}} (ID: {{$json["workflow"]["id"]}})` <br> - **Body**: Sử dụng các biến payload dưới đây để hiển thị chi tiết lỗi. |

#### Payload mẫu (được chèn vào Body):
```
Workflow: {{$json["workflow"]["name"]}} (ID: {{$json["workflow"]["id"]}})
Execution ID: {{$json["execution"]["id"] || "N/A"}}
Execution URL: {{$json["execution"]["url"] || "N/A"}}
Last Node Executed: {{$json["execution"]["lastNodeExecuted"] || "N/A"}}
Error Message: {{$json["execution"]["error"]["message"]}}
```
> **Lưu ý**: Khi lỗi xảy ra ngay tại thời điểm trigger, một số trường như `execution.id` có thể không có giá trị. Email vẫn được gửi với fallback “N/A”.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy một workflow mẫu có lỗi (ví dụ: node “Set” với giá trị `{{"error"}`) để kiểm tra email được gửi.  
2. **Bật Active**: Đánh dấu workflow “Automatic Workflow Error Notifications via Gmail” là **Active**.  
3. **Đặt làm Error Workflow**:  
   - Mở từng workflow mà bạn muốn nhận thông báo lỗi.  
   - Vào **Options → Settings → Error workflow** → chọn workflow vừa tạo.  

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram**: Thêm node Slack hoặc Telegram để nhận thông báo ngay trên kênh nội bộ.  
- **Lưu log**: Thêm node “Write Binary Data” để lưu payload lỗi vào Google Drive hoặc S3.  
- **Báo cáo định kỳ**: Kết hợp với node “Cron” để gửi báo cáo lỗi hàng ngày/tuần.  
- **Tùy chỉnh email**: Sử dụng HTML trong body để tạo email đẹp hơn, bao gồm bảng dữ liệu chi tiết.  

## 📌 Kết luận
Workflow “Automatic Workflow Error Notifications via Gmail” là giải pháp tối giản nhưng hiệu quả cho mọi đội ngũ DevOps. Bằng cách chỉ cần cấu hình một vài dòng, các sếp đã có thể nhận được thông báo lỗi ngay tức thì, giảm thiểu thời gian downtime và tăng độ tin cậy cho hệ thống.  

**Hãy thử ngay** và chia sẻ trải nghiệm của bạn!