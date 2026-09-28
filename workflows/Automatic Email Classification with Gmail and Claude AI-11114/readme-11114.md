---
title: "🚀 Phân loại Email Tự động với Gmail & Claude AI"
description: "Tự động gắn nhãn cho email dựa trên nội dung, giảm thời gian quản lý hộp thư và tăng năng suất làm việc."
slug: "phan-loai-email-tuy-dung-gmail-claude-ai"
tags: [n8n, automation, no-code, gmail, claude-ai, langchain]
keywords: [n8n workflow, tự động hóa email, phân loại email, Gmail, Claude AI, LangChain]
---

# 🚀 Phân loại Email Tự động với Gmail & Claude AI

Bạn đang phải mất hàng giờ mỗi ngày để lọc, gắn nhãn và tìm kiếm email quan trọng trong hộp thư Gmail?  
Workflow này sẽ **đánh dấu tự động** các email thành “Ads”, “Work”, “Personal”, “Financial” hoặc “Other” chỉ bằng một dòng lệnh – không cần viết code, chỉ cần cấu hình một vài credential.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải lọc thủ công hàng trăm email mỗi ngày.  
- **Chính xác**: AI phân loại dựa trên ngữ cảnh, từ khóa và tone của email.  
- **Tự động 24/7**: Khi email mới đến, workflow ngay lập tức gắn nhãn.  
- **Tùy biến linh hoạt**: Thêm, đổi tên nhãn theo nhu cầu mà không cần chỉnh sửa code.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản Gmail** (đã bật API Gmail và OAuth2).  
- **API Key Anthropic** (để sử dụng Claude Sonnet 4.5).  
- **Đăng ký n8n** (Self‑hosted hoặc n8n.cloud).  
:::

## 🚀 Cách import & Lưu ý khi “lên đồ”

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc: <https://n8n.io/workflows/11114>.  
2. Mở n8n Editor → **Import** → **Import from file** → chọn file JSON.  
3. Hoặc copy toàn bộ nội dung JSON và dán vào ô **Import from JSON**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Credential | Tham số cần cấu hình |
|------|----------|------------|----------------------|
| Gmail Trigger | `Gmail Trigger` | `gmailOAuth2` | Đăng nhập tài khoản Gmail, chọn “Inbox” |
| Email Content Classifier | `Email Content Classifier` | *Không cần credential* | `inputText` = `{{ $json["body"] }}` (hoặc `{{ $json["snippet"] }}`) |
| Anthropic Chat Model | `Anthropic Chat Model` | `anthropicApiKey` | Chọn mô hình “claude-sonnet-4-5-20250929” |
| Gmail Label Nodes | `Add "Ads" label to message`, `Add "Work" label to message`, … | `gmailOAuth2` | `Message ID` = `{{ $json["id"] }}`; `Label IDs` = ID của nhãn tương ứng (tạo nhãn trong Gmail trước) |

> **Lưu ý**: Mỗi node Gmail (add label) cần **đăng nhập cùng tài khoản Gmail** với Gmail Trigger. Nếu dùng nhiều tài khoản, hãy tạo credential riêng cho từng node.

### 3. Kích hoạt ⚡️

1. **Test run**: Gửi một email mẫu (đúng nội dung “Work” hoặc “Personal”) tới hộp thư.  
2. Kiểm tra trong n8n: node “Email Content Classifier” trả về label “Work”.  
3. Kiểm tra Gmail: email đã được gắn nhãn “Work”.  
4. Khi mọi thứ ổn, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram notification**: Thêm node Slack/Telegram sau Gmail Label để thông báo khi email được gắn nhãn.  
- **Lưu log**: Dùng node “Write Binary Data” để ghi lại nội dung email và label vào Google Sheet hoặc database.  
- **Báo cáo định kỳ**: Kết hợp node “Cron” + “Google Sheets” để gửi báo cáo hàng ngày về số lượng email theo từng nhãn.  
- **Tùy chỉnh classifier**: Thêm ví dụ “Invoice”, “Meeting” vào node “Email Content Classifier” và tạo nhãn Gmail tương ứng.

## 📌 Kết luận

Workflow “Automatic Email Classification with Gmail and Claude AI” giúp các sếp **đưa tổ chức** vào hộp thư Gmail một cách **đơn giản, nhanh chóng** và **độ chính xác cao**.  
Hãy thử ngay, gửi vài email mẫu và cảm nhận sự khác biệt trong công việc hàng ngày!

---