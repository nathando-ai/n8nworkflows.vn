---
title: "🚀 Xóa Hàng Loạt Bài Viết & Ảnh Featured trên WordPress"
description: "Workflow n8n tự động xóa các bài viết và ảnh featured trên WordPress, giúp dọn dẹp nội dung nhanh chóng, không cần viết code."
slug: "xoa-bai-viet-anh-featured-wordpress"
tags: [n8n, automation, no-code, wordpress, marketing, bulk-delete]
keywords: [n8n workflow, tự động xóa wordpress, bulk delete posts, featured image removal, no-code automation]
---

# 🚀 Xóa Hàng Loạt Bài Viết & Ảnh Featured trên WordPress

Bạn đang phải **đánh tay xóa hàng chục, hàng trăm bài viết** trên WordPress, mỗi lần lại phải **điều hướng, xóa ảnh featured, xóa bài** thủ công?  
Công việc này không chỉ tốn thời gian mà còn dễ gây lỗi, ảnh hưởng tới SEO và trải nghiệm người dùng.

**Workflow này** sẽ tự động:

1. Lấy danh sách các bài viết (theo trạng thái bạn muốn, ví dụ `pending`).
2. Kiểm tra mỗi bài có **ảnh featured** hay không.  
3. Nếu có → **Xóa ảnh** rồi **xóa bài**.  
4. Nếu không → **Chỉ xóa bài**.  

Tất cả chỉ bằng **một cú click**, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xóa hàng trăm bài chỉ trong vài giây.  
- **Độ chính xác 100%**: Không còn rủi ro xóa nhầm hoặc bỏ sót ảnh.  
- **Tự động hoá 24/7**: Có thể lên lịch chạy hàng ngày/tuần.  
- **Dễ mở rộng**: Kết nối Slack, Airtable, Google Sheets để lưu log.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **WordPress site** (đã bật REST API).  
- **Application Password** hoặc **JWT token** để xác thực các request HTTP.  
- **n8n instance** (Self‑hosted hoặc Cloud).  
- **Domain của WordPress** (được đặt trong node *Change your Domain here*).  
- (Tùy chọn) Công cụ lưu log: Airtable, Google Sheets, NocoDB, v.v.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Chọn **Upload JSON** và tải file workflow (hoặc copy/paste JSON từ trang gốc).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình quan trọng |
|------|---------|----------------------|
| **Change your Domain here** (Manual Trigger) | Đặt domain WordPress | Nhập URL site của bạn, ví dụ `https://myblog.com` vào trường `wpUrl`. |
| **get post** (HTTP Request) | Lấy danh sách bài viết | - **Authentication**: Chọn `Basic Auth` → nhập Application Password.<br>- **URL**: `{{$json["wpUrl"]}}/wp-json/wp/v2/posts?status=pending&per_page=100&order=desc`<br>- **Method**: `GET`. |
| **Filter** (Filter) | Lọc các bài trả về | Đặt **Expression**: `{{$json["status"]}}` = `pending` (hoặc tùy chỉnh). |
| **Has Img** (If) | Kiểm tra có ảnh featured? | **Condition**: `{{$json["featured_media"]}}` **is not empty**. |
| **get img** (HTTP Request) | Lấy thông tin ảnh để xóa | - **URL**: `{{$json["wpUrl"]}}/wp-json/wp/v2/media/{{$json["featured_media"]}}`<br>- **Method**: `GET`. |
| **delete img** (HTTP Request) | Xóa ảnh featured | - **URL**: `{{$json["wpUrl"]}}/wp-json/wp/v2/media/{{$json["featured_media"]}}`<br>- **Method**: `DELETE`. |
| **delete post** (HTTP Request) | Xóa bài không có ảnh | - **URL**: `{{$json["wpUrl"]}}/wp-json/wp/v2/posts/{{$json["id"]}}`<br>- **Method**: `DELETE`. |
| **delete post with img** (HTTP Request) | Xóa bài có ảnh (sau khi ảnh đã bị xóa) | - **URL**: `{{$json["wpUrl"]}}/wp-json/wp/v2/posts/{{$json["id"]}}`<br>- **Method**: `DELETE`. |
| **if** (n8n-nodes-base.if) | (Optional) Kiểm tra trạng thái duyệt | Nếu muốn tích hợp phê duyệt, thêm webhook ở đây. |

> **Lưu ý:** Tất cả các node HTTP Request phải **đặt cùng một Credential** (Application Password) để tránh lỗi 401.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → Kiểm tra log ở mỗi node, chắc chắn các request trả về `200`.  
2. Nếu mọi thứ ổn → Bật **Active** (nút chuyển đổi góc trên bên phải).  
3. Đặt **Schedule** (nếu muốn chạy định kỳ) → `Cron` → ví dụ `0 2 * * *` (hàng ngày 02:00).

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu log**: Thêm node **Airtable** hoặc **Google Sheets** sau node `delete post` để ghi lại `post ID`, `title`, `deletedAt`.  
- **Thông báo Slack/Telegram**: Khi workflow hoàn thành, gửi tin nhắn tóm tắt số bài đã xóa.  
- **Phê duyệt tự động**: Thay `Manual Trigger` bằng **Webhook** từ Slack (button “Approve”) → Khi người dùng nhấn, webhook kích hoạt phần xóa.  
- **Batch size**: Nếu số bài > 100, dùng **Pagination** (parameter `page`) để lặp qua các trang.  

### 📌 Kết luận
Với workflow **Batch Delete Posts and Featured Images in WordPress**, các sếp có thể **giải phóng hàng giờ công** chỉ bằng một cú click, đồng thời giảm rủi ro lỗi khi xóa nội dung thủ công. Hãy **import ngay**, cấu hình domain và credentials, rồi để n8n làm việc cho bạn! 🚀