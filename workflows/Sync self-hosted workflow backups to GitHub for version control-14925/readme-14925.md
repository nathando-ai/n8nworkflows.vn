---
title: "🔄 Tự động sao lưu workflow n8n lên GitHub để quản lý phiên bản"
description: "Hướng dẫn tự động hóa sao lưu tất cả workflow n8n lên GitHub định kỳ, giúp quản lý phiên bản và khôi phục dữ liệu dễ dàng"
slug: "tu-dong-sao-luu-workflow-n8n-len-github"
tags: [n8n, automation, devops, version-control, github]
keywords: [n8n workflow, tự động hóa, quản lý phiên bản, github, devops]
---

# 🔄 Tự động sao lưu workflow n8n lên GitHub để quản lý phiên bản

[Các sếp đang gặp khó khăn khi quản lý các workflow n8n của mình? Bạn có muốn có một bản sao lưu an toàn cho tất cả các workflow n8n của mình? Workflow này sẽ giúp các sếp tự động sao lưu tất cả các workflow n8n lên một repository GitHub định kỳ. Với giải pháp này, các sếp có thể dễ dàng quản lý phiên bản và khôi phục dữ liệu khi cần thiết.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Quản lý phiên bản hiệu quả**: Tất cả các workflow n8n được sao lưu lên GitHub với tên file rõ ràng và thời gian commit.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, workflow sẽ tự động chạy theo lịch trình đã đặt.
- **Dễ dàng khôi phục**: Khi cần thiết, các sếp có thể dễ dàng khôi phục workflow từ repository GitHub.
- **Tiết kiệm thời gian**: Giảm thiểu công việc thủ công và tối ưu hóa thời gian làm việc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản GitHub**: Tạo một Personal Access Token với quyền `repo` và thêm vào n8n dưới dạng GitHub credential.
- **API Key n8n**: Tạo một API key trong phần *Settings → API* của n8n và thêm vào dưới dạng n8n credential.
- **Repository GitHub**: Tạo một repository trống trên GitHub (ví dụ: `your-username/n8n-backup`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của các sếp, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [n8n workflow](https://n8n.io/workflows/14925).
2. Nhấp vào nút **Import** để tải xuống file JSON của workflow.
3. Trong n8n Editor, nhấp vào **Import from File** và chọn file JSON đã tải xuống.

Hoặc các sếp có thể copy/paste JSON từ trang workflow vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các node quan trọng sau:

- **Schedule Trigger**: Đặt lịch trình sao lưu theo nhu cầu (mặc định là mỗi giờ).
- **List Files in GitHub Repo**: Cập nhật **owner** (tên GitHub của các sếp) và **repository** (tên repository đã tạo).
- **Fetch All n8n Workflows**: Đảm bảo các sếp đã thêm n8n API credential.
- **GitHub nodes**: Tìm kiếm tất cả các node GitHub trong workflow và thay thế **owner** và **repository** với thông tin của các sếp.

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong, các sếp cần thực hiện các bước sau:

1. **Test run**: Chạy workflow với dữ liệu mẫu để đảm bảo mọi thứ hoạt động đúng.
2. **Bật Active workflow**: Kích hoạt workflow để nó chạy tự động theo lịch trình đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể thêm các node để gửi thông báo qua Slack hoặc Telegram khi workflow chạy thành công hoặc gặp lỗi.
- **Lưu log**: Thêm các node để lưu log của workflow vào một file hoặc database để theo dõi lịch sử sao lưu.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo định kỳ về trạng thái của các workflow n8n và trạng thái sao lưu lên GitHub.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động sao lưu tất cả các workflow n8n lên GitHub định kỳ, giúp quản lý phiên bản và khôi phục dữ liệu dễ dàng. Hãy áp dụng ngay để tiết kiệm thời gian và tối ưu hóa công việc!