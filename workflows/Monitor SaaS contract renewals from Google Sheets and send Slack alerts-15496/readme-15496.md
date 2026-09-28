---
title: "🚀 Tự động giám sát gia hạn hợp đồng SaaS từ Google Sheets và gửi cảnh báo Slack thông minh"
description: "Xây dựng hệ thống tự động kiểm tra hạn hợp đồng SaaS hàng ngày qua Google Sheets, xử lý logic thông minh và gửi cảnh báo qua Slack giúp doanh nghiệp không bỏ lỡ bất kỳ kỳ hạn quan trọng nào."
slug: "tu-dong-giam-sat-gia-han-hop-dong-saas-google-sheets-slack"
tags: [n8n, automation, google-sheets, slack, saas-management, business-operations]
keywords: [n8n workflow, tự động hóa gia hạn hợp đồng, quản lý SaaS, Google Sheets Slack integration, RenewalFlow Intelligence]
---

# 🚀 Tự động giám sát gia hạn hợp đồng SaaS từ Google Sheets và gửi cảnh báo Slack

Các sếp có bao giờ gặp tình trạng "tá hỏa" khi phát hiện một phần mềm SaaS quan trọng của công ty đã tự động gia hạn (auto-renew) với chi phí đắt đỏ chỉ vì... quên ngày hết hạn? Việc quản lý thủ công danh sách hàng chục, hàng trăm hợp đồng SaaS trên Excel hay Google Sheets rất dễ dẫn đến sai sót, bỏ lỡ các mốc đàm phán quan trọng để tối ưu chi phí.

Workflow **RenewalFlow Intelligence** này được thiết kế bởi chuyên gia Mychel Garzon sẽ giải quyết triệt để bài toán trên. Hệ thống sẽ tự động quét danh sách hợp đồng mỗi ngày, tính toán các mốc thời gian quan trọng và gửi cảnh báo trực tiếp vào Slack, đồng thời tự động cập nhật trạng thái ngược lại Google Sheets để tránh spam tin nhắn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần nhân sự mất thời gian kiểm tra file Excel/Google Sheets hàng ngày.
- **Cảnh báo thông minh theo mốc thời gian:** Gửi thông báo chi tiết vào các mốc 45 ngày (Nhắc nhở), 30 ngày (Báo giá), 14 ngày (Ra quyết định) và 7 ngày (Hạn cuối).
- **Cơ chế Catch-up thông minh:** Nếu workflow bị gián đoạn (cuối tuần hoặc sập nguồn), hệ thống vẫn tự động quét bù trong cửa sổ 5 ngày của mỗi mốc.
- **Giám sát lỗi tập trung:** Tự động gửi thông báo qua Slack ngay lập tức nếu có sự cố về API hoặc hết hạn credentials.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Account:** Tài khoản Google Sheets để lưu trữ cơ sở dữ liệu hợp đồng.
- **Slack Workspace:** Tài khoản Slack có quyền tạo hoặc cấu hình Bot, kết nối kênh chuyên biệt (ví dụ: `#contract-renewals`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp cần cấu hình chính xác các thành phần sau:

- **Cấu trúc Google Sheets (Cột A đến F):**
  - **A:** `Contract Name` (Tên hợp đồng - Text)
  - **B:** `Vendor Name` (Tên nhà cung cấp - Text)
  - **C:** `Renewal Date` (Ngày gia hạn - Định dạng `YYYY-MM-DD`)
  - **D:** `Current Annual Cost` (Chi phí hàng năm - Số, không có ký hiệu tiền tệ)
  - **E:** `Vendor Pricing URL` (Đường dẫn bảng giá - `https://...`)
  - **F:** `Status` (Trạng thái: `Active`, `Renewed`, hoặc `Cancelled`)

- **Node `Google Sheets: Load Contracts` & `Google Sheets: Update Status`:**
  - Lấy `Spreadsheet ID` từ URL file Google Sheets của các sếp và dán vào node.
  - Thiết lập kết nối OAuth2 hoặc Service Account cho Google Sheets.
  - Chia sẻ file Google Sheets với tài khoản dịch vụ (nếu dùng Service Account).

- **Các Node Slack (`Slack: Daily Summary`, `Slack: Send Alert`, `Slack: Error Alert`):**
  - Tạo kênh `#contract-renewals` trên Slack.
  - Cấp các quyền cần thiết cho Bot: `chat:write`, `chat:write.public`.
  - Thêm Bot vào kênh `#contract-renewals`.
  - Cấu hình thông tin Slack credentials cho tất cả các node Slack trong workflow.

- **Node `Schedule: Daily 9AM`:**
  - Mặc định lịch chạy là 9 giờ sáng mỗi ngày. Các sếp có thể điều chỉnh lại múi giờ (timezone) cho phù hợp với doanh nghiệp.

#### 3. Kích hoạt ⚡️
- Thực hiện chạy thử (Test run) thủ công để kiểm tra dữ liệu từ Google Sheets đổ về node `Brain: Validate & Route`.
- Kiểm tra kết quả hiển thị trên Slack.
- Bật công tắc **Active** để workflow tự động chạy ngầm hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm AI (OpenAI/Anthropic):** Có thể kết hợp thêm node LLM trước bước gửi Slack để AI tự động soạn nội dung email đàm phán giảm giá dựa trên chi phí hiện tại.
- **Mở rộng kênh nhận tin:** Thêm node Telegram hoặc Microsoft Teams để gửi cảnh báo song song với Slack cho các sếp quản lý cấp cao.
- **Lưu log chi tiết:** Kết hợp ghi log lịch sử các lần cảnh báo vào một Sheet riêng biệt (`Audit Log`) để dễ dàng theo dõi lịch sử xử lý hợp đồng.

### 📌 Kết luận
Hệ thống quản lý gia hạn SaaS tự động này sẽ giúp doanh nghiệp tiết kiệm hàng ngàn đô la nhờ chủ động đàm phán lại hợp đồng hoặc cắt giảm các phần mềm không cần thiết đúng thời điểm. Hãy thiết lập ngay hôm nay để tối ưu hóa chi phí vận hành cho tổ chức của các sếp!