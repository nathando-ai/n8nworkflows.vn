---
title: "🚀 Tự động hóa xuất hóa đơn Rivhit từ ảnh chụp WhatsApp bằng AI Agent & Google Vision"
description: "Hướng dẫn cài đặt workflow n8n tự động trích xuất thông tin từ ảnh hóa đơn/chứng từ gửi qua WhatsApp, xử lý qua AI và xuất biên lai Rivhit chuyên nghiệp."
slug: "tu-dong-hoa-xuat-hoa-don-rivhit-tu-whatsapp-ai-google-vision"
tags: [n8n, automation, whatsapp, ai-agent, rivhit, google-vision]
keywords: [n8n workflow, whatsapp automation, rivhit receipt, google vision ocr, ai agent n8n, tự động hóa hóa đơn]
---

# 🚀 Tự động hóa xuất hóa đơn Rivhit từ ảnh chụp WhatsApp bằng AI Agent & Google Vision

Các sếp làm trong lĩnh vực kinh doanh, vận chuyển hay dịch vụ thực tế thường đau đầu với việc nhân viên giao hàng (courier) chụp ảnh hóa đơn, chứng từ thanh toán rồi gửi lên nhóm chat WhatsApp. Việc tổng hợp, nhập liệu thủ công lên phần mềm kế toán Rivhit vừa tốn thời gian, dễ sai sót lại vừa chậm trễ dòng tiền.

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Hệ thống sẽ đóng vai trò như một trợ lý AI thông minh trực 24/7 trên WhatsApp: Nhận ảnh chụp hóa đơn/thanh toán $\rightarrow$ Đọc chữ bằng Google Vision OCR $\rightarrow$ AI Agent đối chiếu, hỏi lại xác nhận $\rightarrow$ Tự động xuất biên lai (receipt) trên Rivhit và gửi ngược file PDF lại cho nhân viên qua WhatsApp. Tất cả diễn ra tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nhập liệu:** Nhân viên chỉ cần chụp ảnh gửi vào nhóm WhatsApp, mọi việc còn lại AI lo.
- **Xử lý đa dạng hình thức thanh toán:** Hỗ trợ tiền mặt, séc (check), thẻ tín dụng, chuyển khoản ngân hàng và thanh toán hỗn hợp (chia nhiều hình thức).
- **Độ chính xác cao:** Kết hợp sức mạnh OCR của Google Vision và khả năng suy luận logic của GPT-4o giúp đọc trọn vẹn thông tin trên hóa đơn mờ hoặc chụp vội.
- **Hoạt động không ngừng nghỉ:** Trợ lý AI túc trực 24/7, tự động đóng hóa đơn (close invoice) và gửi file biên lai PDF về thẳng điện thoại nhân viên.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Hệ thống n8n** (Self-hosted hoặc n8n Cloud).
- **WAHA (WhatsApp HTTP API)**: Để nhận và gửi tin nhắn/file tự động qua WhatsApp.
- **Google Cloud Account**: API Key cho Google Cloud Vision (phục vụ OCR đọc ảnh).
- **Tài khoản OpenAI**: API Key để chạy mô hình `gpt-4o`.
- **Tài khoản phần mềm kế toán Rivhit**: Lấy API Token từ phần cài đặt tài khoản.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n Editor chọn **Add workflow** -> Dấu ba chấm (...) ở góc trên bên phải -> **Import from File / Clipboard** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với hệ thống của các sếp, hãy chú ý cấu hình các node quan trọng sau:

- **Node `Webhook`**: Nhận tin nhắn đến từ WAHA qua đường dẫn `whatsapp-receipt-agent`. Hãy trỏ webhook của WAHA về URL này.
- **Node `Only if it's from the bot's group` (Filter)**: Lọc tin nhắn chỉ nhận từ nhóm WhatsApp chỉ định của công ty. Các sếp nhớ thay thế Group ID bằng định dạng chuẩn: `120363XXXXXXXXXX@g.us` (có thể lấy ID này từ payload mẫu khi test).
- **Node `Extracting text from images` (HTTP Request)**: Cần tích hợp Google Cloud Vision API Key vào phần query parameters để trích xuất văn bản từ ảnh.
- **Node `api key` (Set)**: Điền **Rivhit API token** của các sếp vào đây (lấy từ cài đặt tài khoản Rivhit -> mục API).
- **Node `OpenAI Chat Model`**: Chọn credentials kết nối với tài khoản OpenAI và đảm bảo model đang được chọn là `gpt-4o`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một bức ảnh hóa đơn mẫu qua WhatsApp để test luồng chạy.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống chính thức làm việc tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Nối thêm một node Telegram hoặc Slack vào nhánh xử lý biên lai để ban quản lý nhận được thông báo tức thì mỗi khi có giao dịch thành công.
- **Lưu trữ dữ liệu:** Lưu toàn bộ log giao dịch vào Google Sheets hoặc Airtable để dễ dàng thống kê doanh thu cuối ngày.
- **Xử lý ngoại lệ (Error Handling):** Thêm Error Trigger để nếu AI không đọc được ảnh hoặc API Rivhit lỗi, hệ thống sẽ tự động nhắn tin lại nhắc nhân viên chụp lại rõ hơn.

### 📌 Kết luận
Workflow tự động hóa xuất hóa đơn Rivhit qua WhatsApp kết hợp Google Vision và GPT-4o là giải pháp chuyển đổi số cực kỳ thiết thực cho các đội ngũ sale thực địa hoặc giao hàng. Triển khai ngay hôm nay để tối ưu hóa vận hành và loại bỏ hoàn toàn các thao tác nhập liệu thủ công cho doanh nghiệp của các sếp!