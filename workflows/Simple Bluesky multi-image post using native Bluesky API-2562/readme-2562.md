---
title: "🚀 Tự động đăng bài Bluesky với nhiều hình ảnh bằng API gốc"
description: "Hướng dẫn tự động hóa đăng bài Bluesky với nhiều hình ảnh chỉ với 11 nodes đơn giản, tiết kiệm thời gian và nâng cao hiệu quả marketing"
slug: "tu-dong-dang-bai-bluesky-voi-nhieu-hinh-anh"
tags: [n8n, automation, no-code, bluesky, marketing]
keywords: [n8n workflow, tự động hóa, bluesky, đăng bài tự động, marketing]
---

# 🚀 Tự động đăng bài Bluesky với nhiều hình ảnh bằng API gốc

[Các sếp marketing] thường phải tốn nhiều thời gian để đăng bài trên Bluesky với nhiều hình ảnh. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình chỉ với 11 nodes đơn giản, tiết kiệm thời gian và nâng cao hiệu quả marketing.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đăng bài: Tự động hóa toàn bộ quy trình đăng bài Bluesky với nhiều hình ảnh
- Tăng hiệu quả marketing: Đăng bài nhanh chóng và chính xác với nhiều hình ảnh
- Tăng tương tác: Bài viết với hình ảnh thường thu hút nhiều lượt tương tác hơn
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công sau khi cấu hình
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Bluesky đã kích hoạt
- App Password từ [Bluesky Settings](https://bsky.app/settings/app-passwords)
- Danh sách URL hình ảnh cần đăng (tối đa 4 hình, mỗi hình không quá 1MB)
- Nội dung bài viết (tối đa 300 ký tự)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/2562](https://n8n.io/workflows/2562)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Define Credentials** (Node "Define Credentials"):
   - Thiết lập giá trị cho `_identifier`: Tên người dùng Bluesky của bạn (ví dụ: `username.bsky.social`)
   - Thiết lập giá trị cho `_appPassword`: App Password đã tạo từ [Bluesky Settings](https://bsky.app/settings/app-passwords)

2. **Set Caption** (Node "Set Caption"):
   - Thiết lập giá trị cho `caption`: Nội dung bài viết (tối đa 300 ký tự)
   - Thiết lập giá trị cho `imageUrls`: Danh sách URL hình ảnh (tối đa 4 hình, mỗi hình không quá 1MB)

3. **Post to Bluesky** (Node "Post to Bluesky"):
   - Đảm bảo các tham số `accessJwt` và `did` được tự động truyền từ node "Create Bluesky Session"

4. **Post Image to Bluesky** (Node "Post Image to Bluesky"):
   - Đảm bảo các tham số `accessJwt` và `did` được tự động truyền từ node "Create Bluesky Session"

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test workflow" để kiểm tra workflow với dữ liệu mẫu
2. Sau khi kiểm tra thành công, click vào nút "Active workflow" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các dịch vụ khác như Slack hoặc Telegram để nhận thông báo khi đăng bài thành công
- Lưu log các bài đăng vào Google Sheets để theo dõi hiệu quả
- Tự động hóa đăng bài định kỳ bằng cách kết hợp với node "Schedule Trigger"
- Tạo nhiều workflow khác nhau cho các loại bài viết khác nhau (bài viết thông thường, bài viết quảng cáo, bài viết khuyến mãi...)

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình đăng bài Bluesky với nhiều hình ảnh, tiết kiệm thời gian và nâng cao hiệu quả marketing. Hãy áp dụng ngay để tối ưu hóa quy trình marketing của bạn!