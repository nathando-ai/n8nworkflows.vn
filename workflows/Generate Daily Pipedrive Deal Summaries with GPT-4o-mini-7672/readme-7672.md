---
title: "🚀 Tự động hóa tóm tắt Deal Pipedrive hàng ngày bằng AI (GPT-4o-mini & n8n)"
description: "Hướng dẫn cấu hình workflow n8n giúp lấy dữ liệu deals và notes từ Pipedrive, xử lý bằng Code và tóm tắt tự động qua OpenAI GPT-4o-mini."
slug: "tu-dong-hoa-tom-tat-deal-pipedrive-hang-ngay-gpt-4o-mini"
tags: [n8n, automation, no-code, pipedrive, openai, ai-summarization]
keywords: [n8n workflow, pipedrive automation, tóm tắt deal crm, openai gpt-4o-mini, n8n crm integration]
---

# 🚀 Tự động hóa tóm tắt Deal Pipedrive hàng ngày bằng AI (GPT-4o-mini & n8n)

Việc cập nhật tình hình kinh doanh, kiểm tra các deal và ghi chú (notes) trên CRM mỗi ngày thường ngốn rất nhiều thời gian của các nhà quản lý và đội ngũ sales. Các sếp có cảm thấy mệt mỏi khi phải thủ công rà soát từng cơ hội bán hàng? 

Workflow này ra đời như một giải pháp tự động hóa 100% không cần code (No-code), kết hợp sức mạnh của **Pipedrive CRM** và **OpenAI (GPT-4o-mini)** để tự động gom nhóm, làm sạch dữ liệu deal, ghi chú và tạo ra bản tóm tắt tình hình phễu bán hàng (sales funnel) cực kỳ sắc bén mỗi ngày.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Thay vì mất hàng giờ lướt CRM, AI sẽ tổng hợp toàn bộ bức tranh kinh doanh chỉ trong vài giây.
- **Nắm bắt insight nhanh chóng:** Tự động lọc các ghi chú quan trọng, chuyển đổi stage ID thành tên giai đoạn dễ hiểu.
- **Cá nhân hóa theo nhu cầu:** Dễ dàng mở rộng để gửi bản tóm tắt qua Slack, Email hoặc Telegram.
- **Hoạt động liên tục:** Có thể kích hoạt thủ công hoặc cài đặt lịch chạy tự động (Cron/Schedule Trigger) mỗi sáng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Pipedrive CRM** cùng với API Token quyền truy cập.
- **Tài khoản OpenAI** đã có sẵn số dư (Credits) và API Key để sử dụng mô hình `gpt-4o-mini`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (hoặc sử dụng file JSON được cung cấp) và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 10 nodes chính. Các sếp cần chú ý cấu hình các mục sau:

- **Node `Get many deals` & `Get many notes` (Pipedrive):**
  - Chọn hoặc tạo mới **Pipedrive API Credentials**.
  - *Cách lấy Credential:* Vào Pipedrive cá nhân $\rightarrow$ *Personal preferences $\rightarrow$ API* để lấy **API token**. Company domain chính là phần subdomain trên URL của các sếp (ví dụ: `https://{your-company}.pipedrive.com`).
  - Có thể cấu hình thêm bộ lọc (filter) về owner, label hoặc thời gian tạo nếu muốn thu hẹp phạm vi deal.

- **Node `OpenAI Chat Model3` (OpenAI):**
  - Chọn hoặc tạo mới **OpenAI API Credentials**.
  - Đảm bảo đã nạp tiền vào tài khoản OpenAI Platform và trỏ model về đúng tham số `gpt-4o-mini` để tối ưu chi phí và tốc độ.

- **Các nodes trung gian (`Code`, `Combine Notes`, `Set Field Names`, `Aggregate for Agent`, `Turn Objects to Text`, `Summarize Pipedrive`):**
  - Các nodes này đóng vai trò xử lý dữ liệu trung gian, map các ID giai đoạn sang tên tiếng Việt/dễ hiểu, nhóm các ghi chú lại và chuyển hóa thành định dạng text phù hợp để đưa vào LangChain Agent. Giữ nguyên cấu hình mặc định của tác giả Robert Breen.

#### 3. Kích hoạt ⚡️
- Nhấn nút **`When clicking ‘Execute workflow’`** để test run dữ liệu mẫu xem hệ thống hoạt động trơn tru chưa.
- Sau khi kiểm tra kết quả trả về từ AI thành công, hãy gạt công tắc sang **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình quản trị, các sếp có thể mở rộng workflow này bằng cách:
- Thay thế node `manualTrigger` bằng **Schedule Trigger** để hệ thống tự động chạy lúc 8:00 sáng mỗi ngày.
- Thêm node **Slack** hoặc **Telegram** ở cuối chuỗi để tự động gửi bản tóm tắt thẳng vào nhóm chat của ban quản lý.
- Tích hợp thêm bước gửi email tự động cho đội ngũ sales nắm bắt các deal cần lưu ý trong ngày.

### 📌 Kết luận
Workflow tự động hóa tóm tắt Pipedrive Deal bằng GPT-4o-mini là một "vũ khí" tối ưu hóa thời gian cực kỳ mạnh mẽ cho các nhà quản lý sales. Hãy triển khai ngay hôm nay để giải phóng sức lao động và để AI làm thay những công việc lặp đi lặp lại!