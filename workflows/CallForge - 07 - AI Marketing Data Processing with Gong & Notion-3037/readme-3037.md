---
title: "🚀 CallForge - 07: Xử lý Dữ liệu Marketing AI từ Gong & Notion"
description: "Workflow tự động 100% không cần code, chuyển dữ liệu cuộc gọi bán hàng từ Gong qua Notion, tạo insights marketing, chủ đề lặp lại và actionable insights."
slug: "callforge-07-ai-marketing-data-processing-gong-notion"
tags: [n8n, automation, no-code, Gong, Notion, AI]
keywords: [n8n workflow, tự động hóa, AI marketing, Gong, Notion, marketing insights, recurring topics, actionable insights]
---

# 🚀 CallForge - 07: Xử lý Dữ liệu Marketing AI từ Gong & Notion

Bạn đang phải mất hàng giờ để phân tích dữ liệu cuộc gọi bán hàng, trích xuất insights marketing và ghi lại các chủ đề lặp lại?  
Workflow này sẽ **đưa dữ liệu AI từ Gong vào Notion một cách tự động, 100% không cần code**, giúp bạn tiết kiệm thời gian, giảm sai sót và luôn có dữ liệu cập nhật liên tục.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ phân tích xuống vài phút.  
- **Chính xác hơn**: Dữ liệu được ghi lại chính xác, tránh lỗi thủ công.  
- **Cá nhân hóa**: Mỗi phòng ban có thể tạo database riêng trong Notion.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Notion API Key**: Tạo trong Settings & Members → Integrations → New integration → Copy token.  
- **Database IDs**:  
  - *Marketing Insights Database*  
  - *Recurring Topics Database*  
  - *Actionable Insights Database*  
- **Gong**: Workflow nguồn dữ liệu AI phải gửi payload tới **Execute Workflow Trigger** của workflow này.  
- **n8n Self-hosted** (hoặc n8n Cloud với plan phù hợp).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/3037) hoặc copy toàn bộ JSON.  
2. Mở **n8n Editor**, chọn **Import** → **JSON** → dán JSON vào ô.  
3. Nhấn **Import**. Workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Mô tả | Cài đặt cần chỉnh |
|------|----------|-------|-------------------|
| 1 | Execute Workflow Trigger | Nhận dữ liệu AI từ workflow Gong. | Không cần chỉnh. |
| 2 | Create Marketing Insight Data | Tạo trang trong database Marketing Insights. | **Database ID** (Marketing Insights), **Notion API Key**. |
| 3 | Check if Recurring Topics Found | Kiểm tra có chủ đề lặp lại không. | Không cần chỉnh. |
| 4 | Wait for rate limiting - Recurring | Đợi để tránh rate limit Notion. | **Duration** (ms) tùy nhu cầu. |
| 5 | Split Out Recurring Topics | Phân tách mảng chủ đề lặp lại. | Không cần chỉnh. |
| 6 | Create Recurring Topics Data | Tạo trang trong database Recurring Topics. | **Database ID** (Recurring Topics), **Notion API Key**. |
| 7 | Bundle Recurring Topics Data to 1 object | Gộp dữ liệu thành một object. | Không cần chỉnh. |
| 8 | Merge Recurring Topics Thread | Kết hợp thread cho các chủ đề. | Không cần chỉnh. |
| 9 | Check if Marketing Insight Data Found | Kiểm tra dữ liệu insights có tồn tại không. | Không cần chỉnh. |
| 10 | Wait for rate limiting - Marketing Insights | Đợi rate limit. | **Duration** (ms). |
| 11 | Split out Insights | Phân tách mảng insights. | Không cần chỉnh. |
| 12 | Bundle Marketing Insights Data to 1 object | Gộp insights thành một object. | Không cần chỉnh. |
| 13 | Merge Marketing Insights Thread | Kết hợp thread cho insights. | Không cần chỉnh. |
| 14 | Check if Actionable Insights Data Found | Kiểm tra dữ liệu actionable insights có tồn tại không. | Không cần chỉnh. |
| 15 | Wait for rate limiting - Actionable Insights | Đợi rate limit. | **Duration** (ms). |
| 16 | Split Out Actionable Insights | Phân tách mảng actionable insights. | Không cần chỉnh. |
| 17 | Create Actionable Insights Data | Tạo trang trong database Actionable Insights. | **Database ID** (Actionable Insights), **Notion API Key**. |
| 18 | Bundle Actionable Insights Data to 1 object | Gộp actionable insights thành một object. | Không cần chỉnh. |
| 19 | Merge Actionable Insights Thread | Kết hợp thread cho actionable insights. | Không cần chỉnh. |

> **Lưu ý**: Mỗi node Notion cần **Notion API Key** và **Database ID** tương ứng. Nếu bạn chưa có Database ID, mở Notion, click vào **⋮** > **Copy link** và lấy phần cuối cùng (đoạn sau `https://www.notion.so/.../`).

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (đảm bảo payload có cấu trúc giống như Gong gửi).  
2. Kiểm tra trong Notion xem các trang đã được tạo đúng chưa.  
3. Khi mọi thứ ổn, bật **Active** để workflow tự động chạy khi nhận dữ liệu.

## ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo định kỳ**: Thêm node **Cron** + **Email** để gửi summary hàng ngày tới đội marketing.  
- **Slack/Telegram notification**: Thêm node **Slack** hoặc **Telegram** để nhận alert khi có actionable insight mới.  
- **Lưu log**: Thêm node **Google Sheets** hoặc **MongoDB** để ghi lại lịch sử dữ liệu.  
- **Tích hợp Pipedrive/Salesforce**: Khi phần tích hợp hoàn thiện, thay thế Notion node bằng **Pipedrive** hoặc **Salesforce** node để đồng bộ dữ liệu.  

## 📌 Kết luận
Workflow **CallForge - 07** giúp các sếp **đưa dữ liệu AI từ Gong vào Notion một cách nhanh chóng, chính xác và liên tục**.  
Hãy **đăng ký VPS**, **tạo Notion API Key**, **đặt Database IDs** và **đưa workflow lên** ngay hôm nay để tiết kiệm thời gian và nâng cao hiệu quả công việc marketing của bạn!