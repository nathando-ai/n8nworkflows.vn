---
title: "🚀 Sao lưu tự động workflow n8n lên GitHub mỗi 6 giờ"
description: "Tự động sao lưu toàn bộ workflow n8n lên GitHub định kỳ, tránh mất dữ liệu và dễ dàng quản lý phiên bản."
slug: "sao-luu-workflow-n8n-github"
tags: [n8n, automation, no-code, devops, backup, github]
keywords: [n8n workflow, tự động sao lưu, GitHub, backup workflow, devops]
---

# 🚀 Sao lưu tự động workflow n8n lên GitHub mỗi 6 giờ

Bạn có bao giờ lo lắng vì một cú lỗi, một cập nhật sai cấu hình khiến **tất cả các workflow** trong n8n bị mất?  
Việc sao lưu thủ công từng workflow, đặt tên file, commit lên GitHub… tốn thời gian, dễ sai sót và không đảm bảo tính liên tục.  

**Workflow này** sẽ giải quyết hoàn toàn vấn đề: mỗi 6 giờ (hoặc tùy chỉnh) nó sẽ tự động **xuất toàn bộ workflow**, chuyển thành file JSON và **đẩy lên GitHub** – không cần viết một dòng code nào. Các sếp sẽ luôn có bản sao lưu an toàn, có lịch sử phiên bản và có thể khôi phục ngay khi cần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không lo mất dữ liệu**: Mỗi backup được lưu lại với timestamp, dễ dàng rollback.  
- **Tiết kiệm thời gian**: Tự động chạy, không cần thao tác thủ công.  
- **Quản lý phiên bản**: GitHub cung cấp lịch sử commit, review và so sánh thay đổi.  
- **Hoạt động liên tục 24/7**: Khi n8n gặp sự cố, backup đã sẵn sàng để phục hồi.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản GitHub** với quyền **repo** (đọc/ghi) trên repository muốn lưu backup.  
- **GitHub API Credential** trong n8n (`githubApi`).  
- **API Key của n8n** (nếu n8n được bảo mật) để gọi endpoint `/workflows`.  
- **URL của instance n8n** (ví dụ: `https://your-n8n.com`).  
- **Thư mục (path) trong repo** nơi lưu file backup, ví dụ: `backups/workflows/`.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ link gốc: https://n8n.io/workflows/6392) hoặc sao chép toàn bộ JSON.  
2. Vào **n8n > Workflows > Import** → Dán JSON → **Import**.  
3. Đặt tên lại nếu muốn, rồi **Save**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng và cách cấu hình:

| Node | Mô tả | Cấu hình cần thay đổi |
|------|------|----------------------|
| **Schedule Trigger** | Kích hoạt workflow theo lịch. | - `Cron` → mặc định mỗi 6 giờ (`0 */6 * * *`). <br> - Thay đổi nếu muốn tần suất khác. |
| **Get All Workflows** (HTTP Request) | Gọi API `/workflows` để lấy danh sách workflow dưới dạng JSON. | - **Method**: `GET` <br> - **URL**: `{{ $json["n8nUrl"] }}/rest/workflows` <br> - **Authentication**: chọn **Header Auth** → `Authorization: Bearer <YOUR_N8N_API_KEY>` |
| **Move Binary Data** | Chuyển JSON sang dạng binary để GitHub chấp nhận. | Không cần thay đổi, chỉ đảm bảo **Input** là output của node “Get All Workflows”. |
| **If file not exits?** (If) | Kiểm tra file backup đã tồn tại trên GitHub chưa. | - **Expression**: `{{ $json["exists"] === false }}` (sử dụng output của node “Edit a file”). |
| **Get Previous FIle back** (Merge) | Khi file chưa tồn tại, merge dữ liệu để tạo file mới. | Đặt **Mode** là **Pass Through** để truyền dữ liệu từ “Move Binary Data” sang node tiếp theo. |
| **Edit a file** (GitHub) | Cập nhật file backup nếu đã tồn tại. | - **Operation**: `Edit` <br> - **Resource**: `File` <br> - **Owner**: `<your-github-username>` <br> - **Repository**: `<your-repo>` <br> - **File Path**: `backups/workflows/{{ $now.format("YYYYMMDD_HHmm") }}.json` <br> - **Content**: `{{ $binary["data"] }}` <br> - **Commit Message**: `Backup workflow @ {{ $now }}` |
| **Create a file** (GitHub) | Tạo file mới nếu chưa tồn tại. | Cấu hình tương tự “Edit a file” nhưng **Operation** = `Create`. |
| **Sticky Note** (n8n‑nodes‑base.stickyNote) | Chỉ là ghi chú, không ảnh hưởng tới luồng. | Không cần thay đổi. |

> **Lưu ý:** Cả hai node GitHub (`Edit a file` & `Create a file`) phải **đính kèm credential** `githubApi`. Vào tab **Credentials** → **Add New Credential** → chọn **GitHub API** → nhập **Personal Access Token** có quyền `repo`.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → Kiểm tra log, đảm bảo không có lỗi 4xx/5xx.  
2. Kiểm tra repository GitHub: một file JSON mới (hoặc cập nhật) đã xuất hiện.  
3. Bật **Active** → Workflow sẽ tự động chạy theo lịch đã định.

## ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau node GitHub để gửi tin nhắn báo thành công/ thất bại.  
- **Lưu log vào Google Sheet**: Dùng node **Google Sheets** để ghi lại thời gian backup, trạng thái và link file.  
- **Branch riêng cho backup**: Đặt `branch` là `backup` để tách biệt với code chính, dễ quản lý.  
- **Retention policy**: Thêm một script (hoặc GitHub Action) xóa các backup cũ hơn 30 ngày, giữ repo gọn gàng.

## 📌 Kết luận
Với workflow này, các sếp sẽ **không còn lo lắng** về việc mất workflow quan trọng, đồng thời tận dụng sức mạnh của GitHub để **quản lý phiên bản** và **phục hồi nhanh chóng**. Hãy **import**, **cấu hình credential**, **bật active** và để n8n tự động bảo vệ tài sản tự động hoá của bạn! 🚀🔒