---
title: "🚀 Tự động lấy và xuất bản toàn bộ bài viết trong Storyblok bằng n8n"
description: "Hướng dẫn tự động hóa quy trình quản lý nội dung với n8n, giúp lấy toàn bộ stories và publish hàng loạt trên Storyblok chỉ với 1 cú click."
slug: "tu-dong-lay-va-xuat-ban-bai-viet-storyblok-n8n"
tags: [n8n, automation, no-code, storyblok, content-management, product]
keywords: [n8n workflow, storyblok automation, tự động xuất bản bài viết, quản lý nội dung storyblok, n8n storyblok integration]
---

# 🚀 Tự động lấy và xuất bản toàn bộ bài viết trong Storyblok bằng n8n

Việc quản lý và xuất bản nội dung hàng loạt trên Headless CMS như Storyblok thường ngốn rất nhiều thời gian nếu các sếp phải bấm thủ công từng bài viết. Thay vì lặp đi lặp lại những thao tác nhàm chán này, workflow n8n dưới đây sẽ giúp các sếp tự động hóa 100 quy trình: quét toàn bộ các stories có trong hệ thống và tiến hành publish chúng ngay lập tức chỉ với một cú click chuột!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Thay vì duyệt và bấm publish thủ công từng bài viết, hệ thống tự động xử lý toàn bộ danh sách chỉ trong vài giây.
- **Loại bỏ sai sót:** Đảm bảo không bỏ sót bất kỳ bài viết nháp (draft) nào cần đưa lên môi trường production.
- **Vận hành linh hoạt:** Dễ dàng kích hoạt thủ công khi cần đồng bộ hoặc cập nhật hàng loạt nội dung chiến dịch.
- **Tự động hóa hoàn toàn:** Không cần viết code phức tạp, tận dụng tối đa sức mạnh của n8n và Storyblok Management API.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Storyblok:** Truy cập vào không gian làm việc (Workspace/Space) của sếp.
- **Storyblok Management API Credentials:** Lấy API key hoặc Personal Access Token từ Storyblok để cấu hình kết nối trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n Editor, sau đó copy toàn bộ mã JSON của workflow (hoặc sử dụng file JSON được cung cấp từ cộng đồng n8n) và dán trực tiếp vào giao diện làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 nodes cốt lõi, các sếp cần chú ý cấu hình chính xác các điểm sau:

- **Node `On clicking 'execute'` (Manual Trigger):** 
  - Đây là điểm khởi đầu dạng thủ công. Khi các sếp bấm nút "Execute workflow", toàn bộ tiến trình sẽ chạy.
- **Node `Storyblok` (Get All):** 
  - **Operation:** Chọn `getAll` để lấy danh sách toàn bộ các stories hiện có trong không gian Storyblok của sếp.
  - **Credentials:** Kết nối tài khoản Storyblok bằng *Storyblok Management API*.
- **Node `Storyblok1` (Publish):** 
  - **Operation:** Chọn `publish` để tiến hành xuất bản các stories vừa được lấy về từ node trước đó.
  - **Credentials:** Sử dụng chung một cấu hình credentials với node bên cạnh.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách bấm nút "Execute Node" hoặc "Execute Workflow" để kiểm tra xem danh sách stories đã được lấy và publish thành công chưa.
- Sau khi test thành công, các sếp có thể chuyển sang chế độ kích hoạt tự động hoặc giữ nguyên dạng trigger thủ công tùy theo nhu cầu sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở nên mạnh mẽ hơn, các sếp có thể mở rộng thêm các tính năng sau:
- **Thay đổi Trigger:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành `Webhook` hoặc `Schedule Trigger` để tự động hóa việc xuất bản theo lịch định kỳ (ví dụ: tự động publish bài viết mới vào 8h sáng mỗi ngày).
- **Gửi thông báo qua Slack/Telegram:** Thêm node thông báo kết quả sau khi hoàn tất quá trình publish để team nắm bắt số lượng bài viết đã lên sóng thành công.
- **Lưu log vào Google Sheets:** Ghi lại ID và tên các bài viết đã được publish để tiện theo dõi và kiểm toán nội dung.

### 📌 Kết luận
Workflow "Get all the stories and publish them in Storyblok" là một công cụ cực kỳ hữu ích giúp các Content Manager và Developer tiết kiệm hàng giờ thao tác thủ công. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa quy trình quản lý nội dung nhé!