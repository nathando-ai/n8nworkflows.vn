---
title: "📰 [Tự động hóa] Workflow n8n: Tạo Báo Cáo Tin Tức AI Hàng Ngày với Perplexity và Gmail"
description: "Hướng dẫn tự động hóa việc tổng hợp tin tức AI hàng ngày từ Perplexity và gửi email báo cáo qua Gmail bằng n8n. Tiết kiệm thời gian và duy trì thông tin cập nhật liên tục."
slug: "tu-dong-hoa-bao-cao-tin-tuc-ai-hang-ngay-voi-perplexity-va-gmail"
tags: [n8n, automation, no-code, AI, email]
keywords: [n8n workflow, tự động hóa, tin tức AI, Perplexity, Gmail]
---

# 📰 [Tự động hóa] Workflow n8n: Tạo Báo Cáo Tin Tức AI Hàng Ngày với Perplexity và Gmail

[Các sếp đang làm việc trong lĩnh vực AI hoặc công nghệ có thể gặp khó khăn khi phải theo dõi hàng trăm nguồn tin tức hàng ngày để cập nhật những phát triển mới nhất. Việc thủ công này tốn thời gian và dễ bỏ sót thông tin quan trọng. Workflow này sẽ giúp các sếp tự động hóa quy trình này 100% không cần code, chỉ với vài bước cấu hình đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải tìm kiếm và đọc tin tức AI hàng ngày.
- **Thông tin cập nhật liên tục**: Nhận báo cáo hàng ngày về những phát triển mới nhất trong lĩnh vực AI.
- **Dễ dàng theo dõi**: Các tin tức được phân loại rõ ràng và gửi qua email với định dạng đẹp mắt.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cấu hình xong.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Perplexity với API key.
- Tài khoản Gmail với quyền truy cập OAuth2.
- Địa chỉ email nhận báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [Workflow gốc](https://n8n.io/workflows/4412).
2. Click vào nút "Import" và sao chép JSON workflow.
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Daily Trigger"**:
   - Thay đổi thời gian chạy nếu cần (mặc định là 9 AM hàng ngày).

2. **Node "Perplexity AI News Search"**:
   - Thêm credentials cho Perplexity API.
   - Cập nhật prompt trong node để phù hợp với nhu cầu của các sếp (ví dụ: thay đổi các danh mục tin tức).

3. **Node "Gmail"**:
   - Thêm credentials cho Gmail OAuth2.
   - Cập nhật địa chỉ email nhận báo cáo trong node này.

4. **Node "Format Email Content1"**:
   - Tùy chỉnh nội dung email theo ý muốn (ví dụ: thay đổi định dạng, thêm/xóa các phần tin tức).

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" để test workflow với dữ liệu mẫu.
2. Sau khi kiểm tra thành công, click vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi báo cáo qua Slack hoặc Telegram.
- **Lưu log**: Thêm node để lưu log các tin tức đã gửi để theo dõi lịch sử.
- **Gửi báo cáo định kỳ**: Thay đổi lịch trình trong node "Daily Trigger" để gửi báo cáo hàng tuần hoặc hàng tháng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc tổng hợp và gửi báo cáo tin tức AI hàng ngày một cách dễ dàng và hiệu quả. Với việc cấu hình đơn giản và không cần code, các sếp có thể tiết kiệm thời gian và duy trì thông tin cập nhật liên tục. Hãy áp dụng ngay để bắt đầu nhận báo cáo tin tức AI hàng ngày!