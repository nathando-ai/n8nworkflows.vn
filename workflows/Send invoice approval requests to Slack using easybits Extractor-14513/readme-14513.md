---
title: "🚀 Tự động hóa quy trình duyệt hóa đơn gửi lên Slack với easybits Extractor trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động nhận hóa đơn qua Web Form, trích xuất dữ liệu bằng AI với easybits Extractor và gửi yêu cầu phê duyệt thông minh kèm nút tương tác lên Slack."
slug: "tu-dong-hoa-duyet-hoa-don-slack-easybits-n8n"
tags: [n8n, automation, easybits, slack, invoice-processing, ai-extraction]
keywords: [n8n workflow, duyệt hóa đơn tự động, easybits Extractor, Slack approval, tự động hóa n8n]
---

# 🚀 Tự động hóa quy trình duyệt hóa đơn gửi lên Slack với easybits Extractor

Việc xử lý và phê duyệt hóa đơn thủ công thường tốn rất nhiều thời gian: kế toán phải đọc từng file PDF, nhập liệu thủ công vào bảng tính, sau đó nhắn tin hoặc gọi điện cho quản lý để xin chữ ký hoặc nút bấm phê duyệt. Quy trình này dễ dẫn đến sai sót, chậm trễ thanh toán và phiền toái trong việc lưu trữ.

Giải pháp? Workflow n8n này sẽ tự động hóa 100% quy trình trên! Từ việc cung cấp giao diện upload hóa đơn, sử dụng AI trích xuất thông tin, phân loại hạn mức phê duyệt cho đến việc bắn tin nhắn tương tác trực tiếp lên Slack. Các sếp chỉ cần ngồi chơi và bấm nút **Approve** hoặc **Reject** ngay trên Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần nhập liệu hay soát hóa đơn thủ công.
- **Phân loại thông minh:** Tự động phân cấp phê duyệt (Standard, Medium, High) dựa theo giá trị tiền trên hóa đơn.
- **Tương tác mượt mà:** Gửi thông báo chi tiết kèm nút bấm tương tác trực tiếp trên Slack, không cần rời khỏi ứng dụng chat.
- **Vận hành 24/7:** Hoạt động tự động liên tục, minh bạch và lưu vết rõ ràng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (hỗ trợ community nodes).
- **Tài khoản easybits Extractor:** Đăng ký tại [extractor.easybits.tech](https://extractor.easybits.tech) để lấy API Key và Pipeline ID.
- **Slack Workspace:** Quyền tạo Slack App để cấu hình Bot Token và tính năng Interactivity.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào không gian làm việc trong n8n Editor của mình. Workflow bao gồm 4 nodes chính:
- **Invoice Upload Form** (`formTrigger`): Giao diện web form nhận file hóa đơn (PDF, PNG, JPEG).
- **easybits Extractor: Extract Invoice Data** (`@easybits/n8n-nodes-extractor.easybitsExtractor`): Trích xuất dữ liệu thông minh từ hóa đơn.
- **Map Invoice Fields** (`set`): Xử lý dữ liệu, định dạng trường thông tin và tính toán hạn mức phê duyệt (Approval Tier).
- **Send to Slack for Approval** (`httpRequest`): Gửi yêu cầu duyệt kèm nút bấm tương tác lên kênh Slack định sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Invoice Upload Form`**: Không cần cấu hình phức tạp, node này sẽ tự động sinh ra một URL public để các sếp gửi cho nhà cung cấp hoặc nội bộ tải hóa đơn lên.
- **Node `easybits Extractor: Extract Invoice Data`**: 
  - Truy cập `extractor.easybits.tech`, tạo pipeline mới với các trường: `vendor_name`, `invoice_number`, `invoice_date`, `total_amount`, `customer_name`.
  - Tạo Credentials trong n8n bằng cách nhập **Pipeline ID** và **API Key** từ easybits.
- **Node `Map Invoice Fields`**: Kiểm tra lại logic phân loại hạn mức tiền tệ (Approval Tiers):
  - 🟢 **Standard:** Dưới €1,000
  - 🟡 **Medium:** Từ €1,000 đến €5,000
  - 🔴 **High:** Trên €5,000
- **Node `Send to Slack for Approval`**:
  - Tạo Slack App tại `api.slack.com/apps`, thêm Bot Token Scopes (`chat:write`, `chat:write.public`).
  - Lấy **Bot User OAuth Token** (bắt đầu bằng `xoxb-`) để cấu hình credentials trong n8n.
  - Thay thế Channel ID chính xác vào đường dẫn hoặc body của HTTP Request để bắn thông báo đúng kênh cần nhận duyệt.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách upload một hóa đơn mẫu qua trang Form.
- Kiểm tra kết quả trả về trên Slack xem các nút bấm tương tác đã hiển thị chuẩn chỉnh chưa.
- Gạt công tắc sang **Active** để đưa vào sử dụng chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Kết nối thêm node Google Sheets hoặc Airtable ngay sau bước trích xuất để lưu toàn bộ dữ liệu hóa đơn vào bảng quản lý tài chính.
- **Thông báo trạng thái:** Thêm nhánh xử lý khi người quản lý bấm nút "Approve" hoặc "Reject" trên Slack để gửi email cảm ơn nhà cung cấp hoặc thông báo cho bộ phận kế toán tiến hành thanh toán.
- **Tích hợp AI Agent:** Có thể kết hợp thêm LLM (OpenAI/Anthropic) để phân tích nội dung hóa đơn sâu hơn (ví dụ: cảnh báo chi phí bất thường).

### 📌 Kết luận
Với workflow n8n kết hợp easybits Extractor và Slack này, quy trình phê duyệt hóa đơn rườm rà trước đây sẽ được thu gọn chỉ trong vài cú click chuột. Hãy áp dụng ngay vào doanh nghiệp của các sếp để tối ưu hóa năng suất và số hóa toàn diện quy trình kế toán nhé!