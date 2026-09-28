---
title: "🚀 Tự động đăng bài lên Instagram, Facebook & LinkedIn từ Google Sheets"
description: "Kết nối Google Sheets làm lịch nội dung, tự động đăng bài lên 3 mạng xã hội chỉ trong vài giây mà không viết code."
slug: "tu-dong-dang-bai-instagram-facebook-linkedin-tu-google-sheets"
tags: [n8n, automation, no-code, social-media, instagram, facebook, linkedin]
keywords: [n8n workflow, tự động đăng bài, Instagram, Facebook, LinkedIn, Google Sheets]
---

# 🚀 Tự động đăng bài lên Instagram, Facebook & LinkedIn từ Google Sheets

Bạn đã từng mất hàng giờ mỗi ngày để **copy‑paste** nội dung từ bảng tính lên từng nền tảng xã hội?  
Việc quản lý lịch đăng, kiểm tra trạng thái đã đăng, và đồng bộ nội dung giữa các kênh thường khiến các sếp phải **đánh đổi thời gian** và **rủi ro sai sót**.  

**Workflow này** sẽ giải quyết mọi phiền toái: chỉ cần thêm một dòng mới vào Google Sheets, nội dung sẽ tự động được đăng lên Instagram, Facebook và LinkedIn (theo cờ bật/tắt) và trạng thái sẽ được cập nhật lại ngay trong sheet. Hoàn toàn **không cần code**, chỉ cần cấu hình một lần và để n8n chạy 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Đăng hàng loạt chỉ bằng một thao tác “Thêm dòng” trong Google Sheets.  
- **Độ chính xác 100 %**: Không còn lỗi copy‑paste, nội dung luôn đồng nhất trên mọi nền tảng.  
- **Theo dõi trạng thái**: Cột *Status* trong sheet cho biết bài đã đăng thành công trên kênh nào.  
- **Hoạt động liên tục**: Workflow chạy nền 24/7, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
1. **Tài khoản Google** có quyền truy cập Google Sheets.  
2. **Instagram Business Account ID** và **Facebook Page ID** (để cấu hình trong node *Workflow Configuration*).  
3. **Credentials** cho:
   - Google Sheets (OAuth2)  
   - Facebook Graph API (App ID + App Secret + Page Access Token)  
   - LinkedIn (OAuth2)  
4. Google Sheet với các cột bắt buộc: `Content`, `Instagram`, `Facebook`, `LinkedIn`, `Status`.  
5. n8n phiên bản mới nhất (được cài trên VPS hoặc Docker).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ link gốc https://n8n.io/workflows/11996).  
2. Vào **n8n → Workflows → Import** → Chọn file JSON → **Import**.  
3. Hoặc **Copy/Paste** toàn bộ JSON vào cửa sổ **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách **11 node** cần cấu hình chi tiết:

| Node | Loại | Cấu hình quan trọng | Ghi chú |
|------|------|---------------------|---------|
| **New Row in Content Sheet** | `googleSheetsTrigger` | - Chọn **Google Sheets Trigger OAuth2 API**.<br>- Chỉ định **Spreadsheet ID** và **Sheet Name** (ví dụ: `Content Calendar`). | Trigger sẽ kích hoạt mỗi khi có dòng mới. |
| **Workflow Configuration** | `set` | - Thêm 2 trường: `instagramBusinessAccountId`, `facebookPageId`.<br>- Điền giá trị ID thực tế của tài khoản Instagram Business và Facebook Page. | Các ID này sẽ được truyền cho node đăng bài. |
| **Check Platform: Instagram** | `if` | - Điều kiện: `{{$json["Instagram"]}} === true` (hoặc `"TRUE"` tùy cách nhập). | Nếu cờ Instagram = TRUE → đi tới node “Post to Instagram”. |
| **Check Platform: Facebook** | `if` | - Điều kiện: `{{$json["Facebook"]}} === true`. | Nếu cờ Facebook = TRUE → đi tới node “Post to Facebook”. |
| **Check Platform: LinkedIn** | `if` | - Điều kiện: `{{$json["LinkedIn"]}} === true`. | Nếu cờ LinkedIn = TRUE → đi tới node “Post to LinkedIn”. |
| **Post to Instagram** | `facebookGraphApi` (dùng để post Instagram qua Facebook Graph) | - **Credentials**: Facebook Graph API (cùng token với Page).<br>- **Operation**: `POST`.<br>- **Endpoint**: `/{{ $json["instagramBusinessAccountId"] }}/media` (đăng media) và `/{{ $json["instagramBusinessAccountId"] }}/media_publish` (publish).<br>- **Body**: `caption` = `{{$json["Content"]}}`. | Đảm bảo tài khoản Instagram đã được liên kết với Page. |
| **Post to Facebook** | `facebookGraphApi` | - **Credentials**: Facebook Graph API.<br>- **Operation**: `POST`.<br>- **Endpoint**: `{{ $json["facebookPageId"] }}/feed`.<br>- **Body**: `message` = `{{$json["Content"]}}`. | Có thể thêm `link`, `picture` nếu muốn. |
| **Post to LinkedIn** | `linkedIn` | - **Credentials**: LinkedIn OAuth2 API.<br>- **Operation**: `Create Post`.<br>- **Author**: `urn:li:person:{yourLinkedInId}` hoặc `urn:li:organization:{orgId}`.<br>- **Text**: `{{$json["Content"]}}`. | Đảm bảo quyền `r_liteprofile`, `w_member_social`. |
| **Update Status: Instagram** | `googleSheets` (update) | - **Credentials**: Google Sheets OAuth2 API.<br>- **Spreadsheet ID** & **Sheet Name**.<br>- **Range**: dòng hiện tại (sử dụng `{{ $json["rowNumber"] }}`).<br>- **Values**: ghi `Posted to Instagram` vào cột `Status`. | Cập nhật sau khi nhận phản hồi thành công. |
| **Update Status: Facebook** | `googleSheets` (update) | Tương tự như trên, ghi `Posted to Facebook`. | |
| **Update Status: LinkedIn** | `googleSheets` (update) | Tương tự, ghi `Posted to LinkedIn`. | |

> **Lưu ý:** Các node “Update Status” cần **rowNumber** (hoặc `range`) để xác định dòng cần cập nhật. Bạn có thể lấy giá trị này từ trigger (`{{ $json["rowNumber"] }}`) hoặc thêm một **Set** node để lưu lại.

#### 3. Kích hoạt ⚡️
1. **Test run**: Thêm một dòng mẫu vào Google Sheet, đặt các cờ nền tảng thành `TRUE`.  
2. Kiểm tra log trong n8n để xác nhận mỗi node chạy thành công.  
3. Khi mọi thứ ổn, bật **Active** cho workflow (nút toggle ở góc trên‑phải).  

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo tổng hợp**: Thêm node **Email** hoặc **Slack** để gửi bản tóm tắt các bài đã đăng mỗi ngày.  
- **Lưu log chi tiết**: Dùng node **Google Drive** hoặc **Airtable** để lưu toàn bộ payload trả về từ API, giúp debug nhanh.  
- **Hỗ trợ hình ảnh/video**: Mở rộng node “Post to Instagram/Facebook” bằng cách truyền URL media trong cột `MediaURL` của sheet.  
- **Đặt lịch đăng**: Thay `googleSheetsTrigger` bằng **Cron** + **Google Sheets** để chỉ đăng vào khung giờ nhất định (ví dụ 09:00 mỗi ngày).  

### 📌 Kết luận
Với workflow này, các sếp có thể **đánh bại mọi rào cản thủ công**, biến Google Sheets thành trung tâm điều phối nội dung đa kênh, đồng thời **giám sát trạng thái** một cách trực quan. Hãy triển khai ngay, để thời gian quý báu của bạn được tập trung vào sáng tạo nội dung, không còn lo lắng về việc đăng tải! 🚀