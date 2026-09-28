---
title: "🚀 Tự động hóa Email Cold Outreach với AI: Tiết kiệm 80% thời gian gửi email"
description: "Workflow n8n tự động hóa 100% quá trình tìm kiếm, nghiên cứu và viết email cold outreach cá nhân hóa từ LinkedIn leads với Wiza, Perplexity và GPT-5"
slug: "tu-dong-hoa-email-cold-outreach-voi-ai"
tags: [n8n, automation, no-code, sales, ai, cold-email]
keywords: [n8n workflow, tự động hóa sales, email cold outreach, ai writing, linkedin leads]
---

# 🚀 Tự động hóa Email Cold Outreach với AI: Tiết kiệm 80% thời gian gửi email

[Các sếp] có biết không? Mỗi ngày bạn phải dành hàng giờ để tìm kiếm, nghiên cứu và viết email cold outreach? Với workflow này, chúng ta có thể tự động hóa hoàn toàn quá trình này với công nghệ AI tiên tiến, giúp bạn tiết kiệm tới 80% thời gian và tăng tỷ lệ mở email lên gấp 3 lần!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa hoàn toàn quá trình từ tìm kiếm đến viết email
- **Cá nhân hóa cao**: Mỗi email được viết riêng với thông tin nghiên cứu thực tế
- **Chính xác cao**: Dữ liệu được xác thực qua Wiza và Perplexity AI
- **Tăng hiệu quả**: Email được gửi dưới dạng draft sẵn sàng review
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Wiza API
- Tài khoản OpenAI API (GPT-5)
- Tài khoản Perplexity API
- Tài khoản Gmail OAuth2
- File CSV mẫu cho "Leads" và "Case Studies" (có sẵn trong tài liệu)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12342](https://n8n.io/workflows/12342)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào menu "Workflows" > "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Email Finder"**:
   - Thêm credentials Wiza API
   - Đảm bảo đã kích hoạt email verification trong tài khoản Wiza

2. **Node "OpenAI Chat Model" và "OpenAI Chat Model2"**:
   - Thêm credentials OpenAI API
   - Chọn model phù hợp (gpt-5 hoặc gpt-5-mini-2025-08-07)

3. **Node "Perplexity Research"**:
   - Thêm credentials Perplexity API
   - Kiểm tra giới hạn API credits hàng tháng

4. **Node "Create a draft"**:
   - Thêm credentials Gmail OAuth2
   - Đảm bảo đã cấp quyền "Gmail API" trong Google Cloud Console

5. **Node "Your Offer"**:
   - Chỉnh sửa thông tin về sản phẩm/dịch vụ của bạn
   - Cập nhật các case studies trong node "Return Case Studies"

6. **Data Tables**:
   - Tạo 2 data tables: "Leads" và "Case Studies"
   - Import dữ liệu mẫu từ file CSV có sẵn trong tài liệu

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu:
   - Submit một LinkedIn URL vào form
   - Kiểm tra quá trình xử lý từ Wiza đến Gmail draft
2. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để nhận thông báo khi có lead mới hoặc email được tạo
2. **Lưu log hoạt động**: Thêm node để lưu log các email đã gửi và phản hồi từ người nhận
3. **Tự động gửi email**: Thêm node để tự động gửi email sau khi đã được review
4. **Phân tích hiệu quả**: Thêm node để theo dõi tỷ lệ mở email và phản hồi

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn nâng cao chất lượng email cold outreach. Bằng cách kết hợp công nghệ AI tiên tiến với quy trình tự động hóa hoàn chỉnh, bạn có thể xây dựng mối quan hệ với khách hàng tiềm năng một cách hiệu quả hơn bao giờ hết. Hãy thử ngay và trải nghiệm sự khác biệt!