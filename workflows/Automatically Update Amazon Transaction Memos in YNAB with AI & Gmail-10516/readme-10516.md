---
title: "🤖 **Tự Động Hóa Cập Nhật Ghi Chú Giao Dịch Amazon Trên YNAB Với AI & Gmail – Giảm 100% Công Việc Lặp Lại**"
description: "Workflow tự động hóa cập nhật ghi chú (memo) cho giao dịch Amazon trên YNAB (You Need A Budget) bằng AI ChatGPT/Gemini, kết hợp với Gmail để tự động trích xuất thông tin chi tiết. Giúp các sếp tiết kiệm **5-10 giờ/Tháng** và tránh sai sót khi nhập liệu thủ công."
slug: "tieu-dong-hoa-cap-nhat-ghi-chu-amazon-tren-ynab-voi-ai-gmail"
tags: [n8n, automation, no-code, ynab, gmail, ai-chatgpt, self-hosted, workflow-tien-dien]
keywords: [n8n workflow ynab, tự động hóa ynab, chatgpt trích xuất email, cập nhật memo giao dịch amazon, tự động hóa tài chính cá nhân]
---

# 🚀 **Tự Động Hóa Cập Nhật Ghi Chú Giao Dịch Amazon Trên YNAB Với AI & Gmail**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp:**
Hàng tháng, bạn phải **quét qua hàng trăm giao dịch Amazon** trên YNAB để cập nhật ghi chú (memo) chi tiết như:
- Danh sách sản phẩm mua (tránh quên).
- Giá trị tổng cộng (để theo dõi chi tiêu).
- Ngày giao hàng (để phân loại chi phí).

**Kết quả?** **Thời gian mất 5-10 giờ/Tháng**, dễ xảy ra **sai sót** khi nhập liệu thủ công, và **không thể tự động hóa** với các công cụ truyền thống.

**Workflow này giải quyết tất cả:**
✅ **Tự động trích xuất** thông tin từ email Amazon (bao gồm cả nội dung HTML).
✅ **Sử dụng AI (ChatGPT/Gemini)** để tổng hợp và rút gọn ghi chú (dưới 500 ký tự).
✅ **Cập nhật trực tiếp** vào YNAB mà không cần can thiệp thủ công.
✅ **Chạy 24/7** trên VPS riêng (Self-hosted) để không phụ thuộc vào n8n.io.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị giới hạn API**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho AI + API).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/Tháng** cho việc cập nhật ghi chú giao dịch.
- **Chính xác 100%** (không còn quên hoặc nhập sai thông tin).
- **Tự động hóa hoàn toàn** (không cần can thiệp thủ công).
- **Cá nhân hóa ghi chú** (AI rút gọn danh sách sản phẩm dưới 500 ký tự).
- **Hoạt động liên tục** (chạy hàng giờ/lần, không phụ thuộc vào thời gian làm việc).
- **Hỗ trợ nhiều AI** (ChatGPT, Gemini, hoặc các mô hình khác).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản YNAB** (để lấy API Key và Budget ID).
2. **Tài khoản Gmail** (để trích xuất email từ Amazon).
3. **API Key OpenAI** (hoặc API Key Gemini) để sử dụng AI.
4. **VPS Self-hosted** (để chạy workflow 24/7, khuyến nghị sử dụng [TinoHost](https://tino.vn/vps-n8n?affid=388)).

---
:::info[CHUẨN BỊ]
- **YNAB API Key**:
  - Tạo tại [YNAB Developer Portal](https://developer.youneedabudget.com/).
  - Thêm vào n8n dưới **Credentials** với tên `ynabApi`.
- **Gmail OAuth2**:
  - Cấu hình tại [Google Cloud Console](https://console.cloud.google.com/).
  - Thêm vào n8n dưới **Credentials** với tên `gmailOAuth2`.
- **OpenAI API Key** (hoặc Gemini):
  - Mua tại [OpenAI](https://platform.openai.com/) hoặc [Google AI Studio](https://aistudio.google/).
  - Thêm vào n8n dưới **Credentials** với tên `openAiApi`.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/10516](https://n8n.io/workflows/10516) và import vào n8n Editor.
- **Copy/Paste JSON** từ file vào n8n Editor (đảm bảo không có lỗi syntax).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **23 node**, các sếp cần chú ý đến các node quan trọng sau:

##### **A. Cấu Hình YNAB API**
- **Node: "Get All Unapproved Transactions"**
  - **Credentials**: Chọn `ynabApi` (đã cấu hình trước).
  - **URL**: Đảm bảo sử dụng URL chính xác của YNAB (ví dụ: `https://api.youneedabudget.com/v1/budgets/{budgetId}/transactions`).
  - **Header Auth**: Sử dụng `httpHeaderAuth` với `Authorization: Bearer {ynabApiKey}`.

- **Node: "Update Transaction Memo Field"**
  - **Method**: POST.
  - **URL**: `https://api.youneedabudget.com/v1/budgets/{budgetId}/transactions/{transactionId}`.
  - **Body**: JSON với trường `memo` được cập nhật từ AI.

##### **B. Cấu Hình Gmail**
- **Node: "Search Emails for Transaction Amount"**
  - **Credentials**: Chọn `gmailOAuth2`.
  - **Query**: Sử dụng `from:amazon@amazon.com` (hoặc `from:orders@amazon.com`) để lọc email từ Amazon.
  - **Time Range**: Cấu hình để tìm email trong **5 ngày trước và sau** ngày giao dịch (để tránh bỏ lỡ).

##### **C. Cấu Hình AI (ChatGPT/Gemini)**
- **Node: "OpenAI Chat Model"**
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: Chọn `gpt-4.1-mini` (hoặc `gpt-3.5-turbo` nếu muốn tiết kiệm chi phí).
  - **System Prompt**: AI sẽ sử dụng **template mặc định** để trích xuất thông tin từ email. Các sếp có thể tùy chỉnh để phù hợp với nhu cầu (ví dụ: yêu cầu AI rút gọn danh sách sản phẩm hơn).

- **Node: "Memo AI Agent"**
  - **Input**: Gồm **email trích xuất** và **thông tin giao dịch** từ YNAB.
  - **Output**: Ghi chú (memo) được rút gọn dưới **500 ký tự**.

##### **D. Cấu Hình Schedule Trigger**
- **Node: "Schedule Trigger"**
  - **Cron Expression**: `0 * * * *` (chạy **mỗi giờ**).
  - **Time Zone**: Chọn **UTC** hoặc **múi giờ địa phương** của các sếp.

##### **E. Rate Limiting**
- **Node: "Wait 5 seconds"**
  - **Thời gian chờ**: **5 giây** (để tránh bị giới hạn API của OpenAI/Gemini).
  - **Lưu ý**: Nếu sử dụng mô hình **ChatGPT**, có thể tăng thời gian chờ lên **10-15 giây** để tránh bị cutoff.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Sử dụng **node "Manual Trigger"** để chạy workflow một lần và kiểm tra kết quả.
   - Kiểm tra **email** và **YNAB** để xác nhận ghi chú đã được cập nhật.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** và **bật Schedule Trigger** để chạy tự động hàng giờ.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **node Slack/Telegram** để thông báo khi workflow hoàn thành hoặc gặp lỗi.
   - Ví dụ: `If error occurs → Send notification to Slack`.

2. **Lưu Log Lỗi**:
   - Sử dụng **node "Set"** để lưu thông tin lỗi vào một **Google Sheet** hoặc **Notion Database** để theo dõi.

3. **Tùy Chỉnh AI**:
   - Nếu muốn **giảm chi phí**, thay thế ChatGPT bằng **Gemini Free Tier** (nhưng có thể giảm độ chính xác).
   - Thêm **node "HTML to Markdown"** trước khi gửi email vào AI để **giảm token** (nhưng có thể mất một phần độ chính xác).

4. **Xử Lý Giao Dịch Không Phải Amazon**:
   - Thêm **node "If"** để **bỏ qua** giao dịch không phải từ Amazon (ví dụ: giao dịch ngân hàng, chi phí khác).

5. **Báo Cáo Định Kỳ**:
   - Sử dụng **node "Schedule Trigger"** kết hợp với **node "Aggregate"** để tạo **báo cáo tổng hợp** chi tiêu Amazon hàng tháng.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại, **tăng độ chính xác** trong quản lý tài chính, và **tự động hóa hoàn toàn** quá trình cập nhật ghi chú giao dịch trên YNAB.

**Hành động ngay:**
1. **Cài đặt VPS** (nếu chưa có) và cài **n8n Self-hosted**.
2. **Import workflow** và cấu hình **YNAB API, Gmail, và OpenAI**.
3. **Bật Schedule Trigger** để chạy tự động hàng giờ.

**Kết quả?** **Tiết kiệm 5-10 giờ/Tháng** và **không còn lo lắng về sai sót** khi nhập liệu!

---
**💡 Mẹo cuối:**
Nếu các sếp muốn **tăng tốc độ**, có thể **tăng số lượng node "Split In Batches"** để xử lý nhiều giao dịch cùng một lúc (nhưng phải điều chỉnh **rate limiting** để không bị giới hạn API).

**Hãy thử ngay và chia sẻ kết quả với chúng tôi!** 🚀