---
title: "🚀 Kiểm tra bảo mật n8n hàng tuần: Gửi email báo cáo với Supabase & Gmail"
description: "Workflow tự động thực hiện kiểm tra bảo mật n8n mỗi tuần, so sánh với kết quả trước, và gửi email cảnh báo khi có rủi ro mới hoặc thay đổi."
slug: "run-audit-weekly-n8n-security-gmail-supabase"
tags: [n8n, automation, no-code, security, audit, supabase, gmail]
keywords: [n8n workflow, tự động hóa, audit bảo mật, Supabase, Gmail, n8n security audit]
---

# 🚀 Kiểm tra bảo mật n8n hàng tuần: Gửi email báo cáo với Supabase & Gmail

Bạn đang phải lo lắng vì những lỗ hổng bảo mật tiềm ẩn trong hệ thống n8n của mình?  
Workflow này sẽ giúp bạn tự động thực hiện kiểm tra bảo mật mỗi tuần, so sánh với kết quả trước đó, và gửi email cảnh báo ngay khi phát hiện rủi ro mới hoặc thay đổi. Không cần viết code, chỉ cần cấu hình một vài credential và bật workflow – công việc bảo mật sẽ được thực hiện 24/7, chính xác và nhanh chóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động chạy mỗi tuần, không cần thao tác thủ công.  
- **Chính xác 100%**: So sánh dữ liệu JSON, tránh sai sót do con người.  
- **Cá nhân hóa báo cáo**: Email được định dạng rõ ràng, dễ đọc cho mọi thành viên.  
- **Hoạt động liên tục**: Dữ liệu luôn được lưu trữ trong Supabase, sẵn sàng cho lần so sánh tiếp theo.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **n8n API** – Tạo key trong Settings → API → Create key, rồi thêm vào credential `n8nApi`.  
- **Supabase** – Cần Project URL + Service Role API key, thêm vào credential `supabaseApi`.  
- **Gmail OAuth2** – Kết nối Gmail qua OAuth2, thêm vào credential `gmailOAuth2`.  
- **Supabase table** – Tạo bảng lưu kết quả audit (xem chi tiết dưới “Create Supabase table”).  
- **Email nhận báo cáo** – Thay `recipient@example.com` trong node Gmail thành địa chỉ thực tế.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
- Tải file JSON từ link gốc hoặc copy toàn bộ JSON vào n8n Editor → **Import** → **Import from clipboard**.  
- Đảm bảo workflow được lưu với tên “Run a weekly n8n security audit and email changes with Supabase and Gmail”.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên trong workflow | Credential cần chọn | Tham số cần điền |
|------|--------------------|---------------------|------------------|
| **Every Monday 09:00** | scheduleTrigger | - | `Cron: 0 9 * * 1` (hoặc tùy chỉnh giờ) |
| **Generate a security audit** | n8n | `n8nApi` | `operation: generate`, `resource: audit` |
| **Fetch Previous Audit** | supabase | `supabaseApi` | `operation: getAll` (lấy bản ghi mới nhất) |
| **Compare Audits** | code | - | - |
| **Store Audit Result** | supabase | `supabaseApi` | `operation: insert` (đưa dữ liệu vào bảng `n8n_audit_results`) |
| **Any New Findings?** | if | - | `hasChanges` (boolean từ node Compare Audits) |
| **Send Alert Email** | gmail | `gmailOAuth2` | `to: recipient@example.com`, `subject`, `body` (định dạng JSON summary) |

> **Lưu ý**: Node `code` và `if` không cần credential, nhưng cần kiểm tra logic trong node `code` (đảm bảo trả về `hasChanges` đúng).

### 3. Kích hoạt ⚡️
- **Test run**: Chạy workflow với dữ liệu mẫu (bấm “Execute Workflow”) để kiểm tra xem các node có trả về dữ liệu đúng không.  
- **Bật Active**: Sau khi xác nhận, chuyển trạng thái sang **Active**. Workflow sẽ tự động chạy vào thứ Hai 09:00 mỗi tuần.

## ✍️ Mẹo & gợi ý nâng cao
1. **Thêm Slack/Telegram**: Thêm node Slack hoặc Telegram để nhận cảnh báo ngay tức thì, không chỉ qua email.  
2. **Lưu log chi tiết**: Sử dụng node `writeBinaryFile` để lưu kết quả audit vào bucket S3 hoặc Google Drive, giúp lưu trữ lịch sử chi tiết.  
3. **Báo cáo định kỳ**: Kết hợp node `cron` khác để gửi báo cáo tổng quan hàng tháng tới toàn bộ đội ngũ.  
4. **Tự động cập nhật credential**: Sử dụng node `n8n` để tự động refresh token Gmail khi hết hạn, tránh workflow bị dừng.

## 📌 Kết luận
Workflow “Run a weekly n8n security audit and email changes with Supabase and Gmail” là giải pháp tối ưu cho các sếp muốn bảo mật n8n mà không tốn công sức.  
- **Nhanh chóng**: Kiểm tra tự động mỗi tuần.  
- **Độ tin cậy cao**: So sánh dữ liệu JSON chính xác.  
- **Dễ dàng mở rộng**: Thêm Slack, log, báo cáo định kỳ chỉ vài click.  

Hãy áp dụng ngay hôm nay để bảo vệ hệ thống n8n của bạn khỏi những lỗ hổng tiềm ẩn!