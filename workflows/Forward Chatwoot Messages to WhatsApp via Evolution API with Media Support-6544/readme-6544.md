---
title: "🚀 Tự động chuyển tiếp tin nhắn Chatwoot sang WhatsApp qua Evolution API"
description: "Hướng dẫn cấu hình workflow n8n giúp tự động đồng bộ tin nhắn và đa phương tiện từ hệ thống CSKH Chatwoot sang WhatsApp mượt mà bằng Evolution API."
slug: "chuyen-tiep-chatwoot-sang-whatsapp-evolution-api"
tags: [n8n, chatwoot, whatsapp, evolution-api, automation, cskh]
keywords: [n8n workflow, chatwoot whatsapp integration, evolution api n8n, tu dong hoa cskh]
---

# 🚀 Tự động chuyển tiếp tin nhắn Chatwoot sang WhatsApp qua Evolution API

Trong các mô hình chăm sóc khách hàng (CSKH) hiện đại, việc đồng bộ đa kênh là yếu tố sống còn để không bỏ lỡ bất kỳ khách hàng nào. Tuy nhiên, việc đội ngũ hỗ trợ phải liên tục kiểm tra nhiều nền tảng cùng lúc gây tốn rất nhiều thời gian và dễ xảy ra sai sót. 

Giải pháp hoàn hảo cho các sếp đây: Workflow n8n tự động hóa 100% giúp **chuyển tiếp tin nhắn và tệp đính kèm từ Chatwoot trực tiếp sang WhatsApp** thông qua **Evolution API** một cách mượt mà, hỗ trợ cả văn bản, hình ảnh, video, âm thanh và tài liệu!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đồng bộ thời gian thực:** Tin nhắn từ agent hoặc bot trên Chatwoot sẽ ngay lập tức được đẩy sang WhatsApp của khách hàng.
- **Hỗ trợ đa phương tiện (Media Support):** Không chỉ văn bản, workflow còn xử lý và gửi chính xác các định dạng hình ảnh, video, audio, và tài liệu (PDF, Docs...).
- **Lọc thông minh:** Tự động loại bỏ các tin nhắn riêng tư (private notes) của nội bộ nhân viên, tránh làm phiền khách hàng.
- **Khảo sát độ hài lòng:** Tích hợp sẵn tính năng gửi link khảo sát CSAT từ Chatwoot qua WhatsApp.
:::

### 👽 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Hệ thống Chatwoot:** Đã cấu hình Webhook để bắn dữ liệu sang n8n.
- **Evolution API:** Server Evolution API đang hoạt động để kết nối với WhatsApp.
- **Credentials trong n8n:** API Key và thông tin kết nối của Evolution API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào n8n editor, chọn **Import from Clipboard** và dán vào là xong phần khung xương.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 17 nodes được thiết kế tối ưu bởi chuyên gia Thiago Vazzoler Loureiro. Các sếp cần chú ý cấu hình các điểm sau:

- **Node `When Executed by Another Workflow`**: Đóng vai trò là điểm nhận dữ liệu đầu vào (Trigger) từ webhook của Chatwoot chuyển đến. Hãy đảm bảo định dạng JSON đầu vào khớp với cấu trúc Chatwoot payload.
- **Node `Check if message is private`**: Node điều kiện (IF) này kiểm tra xem tin nhắn có phải là ghi chú nội bộ (private note) hay không. Nếu là private, workflow sẽ dừng lại (`No Operation, do nothing`) để tránh lộ thông tin nội bộ cho khách hàng.
- **Node `Gateway` & `Switch` (Message Type)**: Phân loại luồng tin nhắn (tin nhắn đến từ khách, tin nhắn đi từ agent, hay khảo sát sự hài lòng - Satisfaction Survey).
- **Node `Has attachment?` & `Check attachment file type`**: Kiểm tra xem tin nhắn có kèm file hay không và xác định định dạng tệp (image, video, audio, document).
- **Node `Loop array of attachments` (`splitInBatches`)**: Xử lý trường hợp khách hàng hoặc agent gửi nhiều file cùng lúc, đảm bảo gửi lần lượt không bị nghẽn API.
- **Các node gửi tin nhắn (`Send message text`, `Send image message`, `Send video message`, `Send audio message`, `Send document message`, `Send text - Satisfaction Survey`)**: 
  - Cần chọn đúng **Evolution API Credentials**.
  - Cấu hình instance name, số điện thoại người nhận (`number`), và nội dung/đường dẫn file truyền từ các node Code (`Array of attachments`, `Object message`) phía trước.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với một bản ghi mẫu từ Chatwoot để kiểm tra luồng dữ liệu qua các nhánh media.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu log vào Google Sheets / Airtable:** Các sếp có thể gắn thêm một node Google Sheets ở đầu hoặc cuối workflow để lưu lại lịch sử tin nhắn chăm sóc khách hàng phục vụ việc tra cứu sau này.
- **Cảnh báo lỗi qua Telegram/Slack:** Thêm một node Error Trigger để nếu Evolution API lỗi (do mất kết nối WhatsApp), hệ thống sẽ ngay lập tức bắn thông báo vào nhóm Telegram nội bộ để IT xử lý kịp thời.

### 📌 Kết luận
Workflow chuyển tiếp tin nhắn Chatwoot sang WhatsApp qua Evolution API là mảnh ghép hoàn hảo giúp tối ưu hóa quy trình chăm sóc khách hàng đa kênh mà không tốn chi phí thuê, gọi bên thứ ba đắt đỏ. Hãy cài đặt ngay để nâng tầm trải nghiệm khách hàng của doanh nghiệp các sếp nhé!