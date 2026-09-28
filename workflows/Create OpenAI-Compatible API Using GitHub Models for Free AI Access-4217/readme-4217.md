---
title: "🚀 Tạo API Tương Thích OpenAI Miễn Phí Bằng GitHub Models - Tự Động Hóa AI Cho Doanh Nghiệp"
description: "Workflow này giúp các sếp xây dựng API tương thích với OpenAI miễn phí bằng GitHub Models, tiết kiệm chi phí AI cao cấp mà không cần code. Hoạt động 24/7, hỗ trợ các mô hình AI tiên tiến nhất từ GitHub cho tất cả các workflow n8n của doanh nghiệp."
slug: "tao-api-tuong-thich-openai-github-models"
tags: [n8n, automation, ai, github-models, openai-compatible, no-code]
keywords: [n8n workflow miễn phí, tự động hóa AI với GitHub, API tương thích OpenAI, mô hình AI tiên tiến, tự động hóa doanh nghiệp]
---

# 🚀 Tạo API Tương Thích OpenAI Miễn Phí Bằng GitHub Models - Giải Pháp AI Cho Doanh Nghiệp

## 🔍 Nỗi Đau Của Các Sếp
Các sếp đang gặp khó khăn khi phải chi trả hàng nghìn đô cho API OpenAI để chạy các mô hình AI tiên tiến trong các workflow tự động hóa. Thậm chí, với những dự án nhỏ, chi phí này trở thành gánh nặng không cần thiết. **Workflow này giải quyết vấn đề đó bằng cách xây dựng một API tương thích với OpenAI hoàn toàn miễn phí, sử dụng mô hình AI của GitHub - một giải pháp mạnh mẽ và không tốn kém.**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí AI**: Sử dụng mô hình AI tiên tiến của GitHub miễn phí thay vì OpenAI.
- **Hoạt động liên tục**: API hoạt động 24/7, không cần quản lý thủ công.
- **Tích hợp dễ dàng**: Sử dụng các node LLM trong n8n như với OpenAI, không cần refactor code.
- **Cải thiện chất lượng AI**: Trải nghiệm với các mô hình AI mới nhất từ GitHub, không giới hạn rate limit.
:::

---

### 🔧 Yêu Cầu Cần Thiết
:::info[CHUẨN BỊ]
- **Tài khoản GitHub**: Để truy cập API mô hình AI của GitHub.
- **API Key GitHub**: Tạo tại [GitHub Developer Settings](https://github.com/settings/tokens).
- **n8n Self-hosted**: Workflow này yêu cầu n8n được cài đặt trên máy chủ riêng (không dùng phiên bản cloud).
- **N8N Webhook URL**: URL của webhook để kết nối với API GitHub.
- **OpenAI Credential**: Tạo một credential mới trong n8n để kết nối với API GitHub (mô phỏng OpenAI).
:::

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1. Import Workflow 📥
1. **Tải workflow** từ [n8n.io/workflows/4217](https://n8n.io/workflows/4217).
2. **Import vào n8n Editor**:
   - Nhấp vào **Import** trên giao diện n8n.
   - Chọn file JSON đã tải xuống hoặc **copy/paste** JSON từ file vào ô nhập.
   - Nhấp **Import** để hoàn tất.

#### 2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌
##### **a. Thiết Lập Credential GitHub**
- **Tạo credential GitHub**:
  - Vào **Credentials** trong n8n.
  - Nhấp **Add Credential** → Chọn **GitHub API**.
  - Điền **API Key** từ GitHub vào ô `API Key`.
  - Nhấp **Save**.

##### **b. Thiết Lập Credential OpenAI (Mô Phỏng)**
- **Tạo credential OpenAI mới**:
  - Vào **Credentials** trong n8n.
  - Nhấp **Add Credential** → Chọn **OpenAI**.
  - Đặt tên credential là **"n8n-webhook"** (hoặc tên tùy ý).
  - **API Key**: Điền bất kỳ chuỗi nào (ví dụ: `"12345"`).
  - **Base URL**: Điền `https://<your_n8n_url>/webhook/github-models` (thay `<your_n8n_url>` bằng URL của n8n).
  - Nhấp **Save**.

##### **c. Cấu Hình Webhook**
- **Kiểm tra Webhook URL**:
  - Đảm bảo URL webhook trong credential OpenAI chính xác với URL của n8n.
  - Ví dụ: `https://tên-máy-chủ-machine.com/webhook/github-models`.

##### **d. Kích Hoạt Workflow**
- **Test Run**:
  - Nhấp **Run Workflow** để kiểm tra các node hoạt động.
  - Kiểm tra **Models Response** và **Chat Response** để đảm bảo API trả về dữ liệu đúng định dạng.
- **Bật Active**:
  - Sau khi test thành công, nhấp **Active** để workflow hoạt động liên tục.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
1. **Kết Nối Với Các Node AI Khác**:
   - Sau khi cấu hình xong, các node LLM trong n8n (ví dụ: `@n8n/n8n-nodes-langchain.chainLlm`) sẽ tự động sử dụng API GitHub này thay vì OpenAI.

2. **Lưu Log & Theo Dõi**:
   - Sử dụng node **Sticky Note** để ghi chú các thông tin quan trọng (ví dụ: log lỗi, mô hình đang sử dụng).
   - Kết nối với **Slack/Telegram** để nhận thông báo khi workflow hoạt động hoặc gặp lỗi.

3. **Tối Ưu Hóa Mô Hình**:
   - Thử nghiệm với các mô hình khác nhau từ GitHub (ví dụ: `openai/gpt-4o-mini`, `codestral-latest`) để tìm mô hình phù hợp nhất cho dự án.

4. **Tự Động Hóa Báo Cáo**:
   - Sử dụng node **HTTP Request** để gửi báo cáo sử dụng mô hình AI định kỳ (ví dụ: hàng tuần) qua email hoặc Slack.

---

### 📌 Kết Luận
Workflow này không chỉ giúp các sếp **tiết kiệm chi phí AI** mà còn mở ra khả năng sử dụng các mô hình AI tiên tiến nhất từ GitHub trong các dự án tự động hóa. **Không cần code, không cần quản lý API phức tạp** - chỉ cần import, cấu hình và bật hoạt động. **Hãy thử ngay và trải nghiệm sự mạnh mẽ của AI miễn phí!**

---
**🔗 Tài Liệu Tham Khảo**:
- [GitHub Models Documentation](https://docs.github.com/en/github-models)
- [n8n Credentials Guide](https://docs.n8n.io/integrations/builtin/credentials/)
- [n8n Webhook Node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook/)

**💬 Có Thắc Mắc?**:
- Hãy tham gia **Discord n8n** ([đây](https://discord.com/invite/XPKeKXeB7d)) hoặc **Forum n8n** ([đây](https://community.n8n.io/)) để được hỗ trợ!