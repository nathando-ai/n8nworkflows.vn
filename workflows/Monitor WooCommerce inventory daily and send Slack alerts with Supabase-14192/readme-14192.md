---
title: "🚀 Tự động giám sát tồn kho WooCommerce hàng ngày, cảnh báo qua Slack và lưu trữ Supabase"
description: "Hướng dẫn thiết lập workflow n8n tự động kiểm tra kho WooCommerce mỗi ngày, tính toán tốc độ bán hàng, cảnh báo hàng sắp hết qua Slack và lưu lịch sử vào Supabase."
slug: "tu-dong-giam-sat-ton-kho-woocommerce-slack-supabase"
tags: [n8n, automation, woocommerce, slack, supabase, e-commerce]
keywords: [n8n workflow, tự động hóa kho hàng, woocommerce inventory, cảnh báo tồn kho slack, supabase n8n]
---

# 🚀 Tự động giám sát tồn kho WooCommerce hàng ngày, cảnh báo qua Slack và lưu trữ Supabase

Các chủ cửa hàng e-commerce thường xuyên đối mặt với cơn ác mộng: sản phẩm bán chạy thì hết hàng mà không biết (mất doanh thu), trong khi hàng tồn kho ế ẩm lại chiếm dụng vốn. Việc kiểm tra thủ công hàng nghìn sản phẩm mỗi ngày là bất khả thi.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: quét dữ liệu sản phẩm và đơn hàng từ WooCommerce, phân tích hiệu suất bán hàng trong 30 ngày, phân loại trạng thái tồn kho, tính toán số lượng cần nhập, tự động gửi cảnh báo khẩn cấp qua Slack và lưu trữ toàn bộ lịch sử vào cơ sở dữ liệu Supabase.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Chạy lịch trình định kỳ mỗi ngày mà không cần can thiệp thủ công.
- **Tránh đứt gãy nguồn hàng**: Tự động tính toán lượng hàng an toàn (safety stock) và thời điểm đặt hàng lại (reorder quantity).
- **Phân loại thông minh**: Sản phẩm được chia thành Top Performer, Steady, At Risk hoặc Consider Discontinue dựa trên dữ liệu thực tế.
- **Cảnh báo tức thì**: Đội ngũ nhận thông báo chi tiết qua Slack ngay khi có sản phẩm chạm ngưỡng nguy hiểm, kèm bản tổng hợp hàng ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **WooCommerce Store**: Tài khoản quản trị với quyền truy cập API (Consumer Key & Consumer Secret).
- **Supabase Account**: Dự án cơ sở dữ liệu để lưu trữ lịch sử kiểm tra tồn kho.
- **Slack Workspace**: Bot hoặc Webhook tích hợp để gửi tin nhắn cảnh báo và tổng kết.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc sử dụng tính năng copy/paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 14 nodes, trong đó các sếp cần chú ý cấu hình kỹ các kết nối và tham số sau:

- **Run Daily Invetory check (`scheduleTrigger`)**: Cấu hình khung giờ chạy tự động mỗi ngày (ví dụ: 8:00 sáng hàng ngày).
- **Fecth Products & Fetch order (`wooCommerce`)**: Kết nối tài khoản WooCommerce thông qua `wooCommerceApi`. Đảm bảo cung cấp đúng URL cửa hàng và API Keys có quyền đọc (Read).
- **Save Inventory record to database (`supabase`)**: Kết nối `supabaseApi` và trỏ tới bảng dữ liệu phù hợp để lưu trữ bản ghi tồn kho hàng ngày.
- **Send critical inventory alert & Send Inventory summry (`slack`)**: Cấu hình `slackApi` để chọn channel nhận thông báo cảnh báo khẩn cấp và bản tổng kết kho hàng.
- **Các node Code xử lý logic (`Inventory Classification`, `Calculate product sales`, `Calculate reorder quantity`, v.v.)**: Các đoạn mã JavaScript có sẵn sẽ tự động phân tích tốc độ bán hàng 30 ngày qua, tính toán lượng hàng tồn và mức độ khẩn cấp (Normal, High, Critical) mà không cần chỉnh sửa gì thêm trừ khi có nhu cầu tùy chỉnh công thức riêng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test execution**) để kiểm tra luồng dữ liệu từ WooCommerce qua Supabase và bắn tin nhắn thử nghiệm lên Slack.
- Sau khi dữ liệu trả về chính xác, bật công tắc **Active** để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Kết hợp thêm node Telegram hoặc Email để gửi báo cáo song song cho đội ngũ quản lý kho.
- **Tạo Google Sheets backup**: Thêm node Google Sheets bên cạnh Supabase nếu ban lãnh đạo thích xem báo cáo dạng bảng tính quen thuộc.
- **Tự động tạo Purchase Order**: Mở rộng workflow bằng cách kết hợp với hệ thống ERP hoặc gửi email tự động cho nhà cung cấp khi sản phẩm đạt mức `Critical`.

### 📌 Kết luận
Workflow giám sát tồn kho WooCommerce kết hợp Slack và Supabase là "vũ khí" tối ưu giúp tự động hóa khâu quản trị kho hàng, loại bỏ rủi ro thất thoát do hết hàng và giúp đội ngũ luôn nắm bắt chính xác tình hình kinh doanh mỗi ngày. Áp dụng ngay để tối ưu vận hành cho cửa hàng của các sếp!