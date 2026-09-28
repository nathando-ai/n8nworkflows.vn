---
title: "🚀 Xử lý hồ sơ ứng viên tự động: Phân loại CV bằng Claude, PDF.co, Google Docs & Gmail"
description: "Tự động nhận, phân loại và trả lời ứng viên qua email, đồng thời lên lịch phỏng vấn mà không cần viết code."
slug: "xuat-ly-hoso-ung-vien-tu-dong"
tags: [n8n, automation, no-code, HR, AI, summarization]
keywords: [n8n workflow, tự động hóa, phân loại CV, AI summarization, Claude, PDF.co, Google Docs, Gmail]
---

# 🚀 Xử lý hồ sơ ứng viên tự động: Phân loại CV bằng Claude, PDF.co, Google Docs & Gmail

Bạn đang phải xử lý hàng trăm CV thủ công, trích xuất thông tin, so sánh với tiêu chí tuyển dụng và gửi email phản hồi?  
Workflow này sẽ giúp bạn **đánh giá, phân loại và phản hồi ứng viên** chỉ trong vài phút, hoàn toàn không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ xử lý thủ công xuống vài phút tự động.  
- **Độ chính xác cao**: AI Claude trích xuất và so sánh dữ liệu chính xác, giảm sai sót.  
- **Cá nhân hóa email**: Tự động gửi email chúc mừng hoặc từ chối, kèm lịch phỏng vấn phù hợp.  
- **Hoạt động liên tục**: Workflow 24/7, không cần giám sát.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ / API | Credential cần thiết | Ghi chú |
|---------------|----------------------|---------|
| Google Docs   | `googleDocsOAuth2Api` | Dùng để lấy **điều kiện tuyển dụng** (định dạng bảng). |
| Gmail         | `gmailOAuth2`         | Gửi email phản hồi. |
| PDF.co        | `pdfcoApi`            | Tải lên, chuyển đổi và trích xuất PDF. |
| Google Calendar | `googleCalendarOAuth2Api` | Kiểm tra lịch trống cho phỏng vấn. |
| Anthropic (Claude) | `anthropicApi` | Mô hình `claude-sonnet-4-5-20250929`. |
| LangChain (n8n) | - | Sử dụng `agent`, `textClassifier`, `chainSummarization`, `lmChatAnthropic`. |
:::

> **Lưu ý**: Đảm bảo các credential đã được cấp quyền đầy đủ (đọc/ghi) trên các dịch vụ.

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/12779) hoặc copy toàn bộ JSON.  
2. Mở **n8n Editor**, chọn **Import** → **JSON** → dán nội dung.  
3. Nhấn **Import**. Workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Mô tả | Tham số cần cấu hình |
|------|----------|-------|----------------------|
| **On form submission** | `formTrigger` | Bắt đầu workflow khi người dùng gửi form. | Định nghĩa các trường: `Name`, `Email`, `CV File (Upload)` |
| **Switch** | `Switch` | Chia nhánh dựa trên định dạng file (PDF / Google Docs). | Đặt điều kiện: `{{ $json["