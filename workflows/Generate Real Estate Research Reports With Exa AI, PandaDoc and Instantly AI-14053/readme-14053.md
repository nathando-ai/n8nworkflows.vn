---
title: "🚀 Tự động hóa báo cáo nghiên cứu bất động sản với Exa AI, PandaDoc và Instantly AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa 100% quy trình nghiên cứu thị trường BĐS, tạo báo cáo qua PandaDoc và phân phối hàng loạt qua Instantly AI."
slug: "tu-dong-hoa-bao-cao-bat-dong-san-exa-ai-pandadoc-instantly-ai"
tags: [n8n, automation, real-estate, exa-ai, pandadoc, instantly-ai]
keywords: [n8n workflow, tự động hóa bất động sản, Exa AI, PandaDoc, Instantly AI, research report automation]
---

# 🚀 Tự động hóa báo cáo nghiên cứu bất động sản với Exa AI, PandaDoc và Instantly AI

Các sếp làm trong ngành bất động sản hay sales & marketing chắc chắn hiểu rõ nỗi đau: mỗi khi cần làm báo cáo thị trường, cập nhật danh sách cho nhà đầu tư hay khách hàng là tốn hàng giờ đồng hồ để tra cứu dữ liệu web, copy-paste vào template thuyết trình, rồi lại lọ mọ gửi email thủ công từng người một. Vừa tốn thời gian, vừa dễ sai sót.

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó. Nó tự động hóa toàn bộ quy trình từ việc quét dữ liệu thị trường, đóng gói vào mẫu báo cáo chuyên nghiệp, kiểm duyệt qua Slack cho đến chiến dịch gửi email hàng loạt tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn nghiên cứu thị trường:** Khai thác dữ liệu web, xu hướng giá và danh sách bất động sản qua Exa AI mà không cần thao tác tay.
- **Báo cáo chuẩn chỉnh, đồng bộ thương hiệu:** Dữ liệu tự động điền vào template thiết kế sẵn trên PandaDoc, tạo ra các báo cáo/slide cực kỳ chuyên nghiệp.
- **Kiểm soát chặt chẽ trước khi phát hành:** Tích hợp Slack để duyệt báo cáo trước khi gửi đi, đảm bảo không có sai sót lọt ra ngoài.
- **Scale-up chiến dịch gửi khách hàng:** Kết hợp Google Sheets và Instantly AI để phân phối báo cáo cá nhân hóa cho hàng loạt nhà đầu tư/khách hàng một cách an toàn, tránh bị khóa tài khoản nhờ cơ chế quản lý Rate Limit thông minh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Exa AI Account:** Lấy API key để phục vụ việc cào dữ liệu nghiên cứu web.
- **PandaDoc Account & API:** Tạo sẵn một template báo cáo bất động sản với các trường (fields) tương ứng.
- **Google Cloud Console:** Cấu hình Google OAuth2 để n8n đọc/ghi dữ liệu từ Google Sheets (danh sách khách hàng/nhà đầu tư).
- **Slack App / Bot:** Token hoặc Webhook để nhận thông báo chờ duyệt và tổng kết chiến dịch.
- **Instantly AI Account & API:** Cấu hình sẵn các template email chiến dịch gửi đi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ nguồn cung cấp, sau đó tại giao diện n8n Editor, chọn **Add workflow** -> **Import from File** và chọn file JSON vừa tải lên.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 19 nodes được chia thành 3 giai đoạn chính. Các sếp cần chú ý cấu hình kỹ các node sau:

- **Schedule Trigger:** Node khởi chạy lịch trình (hàng ngày, hàng tuần...). Các sếp có thể thay thế bằng Webhook hoặc Form Trigger nếu muốn kích hoạt thủ công.
- **Create a research task & Get a research task (Exa AI):** Kết nối tài khoản Exa AI và cấu hình truy vấn tìm kiếm dữ liệu thị trường, bối cảnh listing và tín hiệu giá cho khu vực mục tiêu.
- **PandaDoc (Generate Presentation) & PandaDoc (checkPresentationStatus):** Kết nối API của PandaDoc. Chỉ định chính xác ID của Template báo cáo bất động sản đã tạo sẵn để hệ thống tự map dữ liệu vào đúng vị trí.
- **Pending Approval (Slack):** Kết nối tài khoản Slack và chọn channel nhận thông báo báo cáo hoàn thành để sếp duyệt trước khi gửi.
- **Fetch Contact & Update Sheet Status (Google Sheets):** Chọn credentials Google OAuth2, trỏ tới file Google Sheets chứa danh sách contact (khách hàng/nhà đầu tư) và map đúng tên sheet.
- **Instantly Add Lead & Wait for Instantly Rate Limit:** Kết nối Instantly API, chọn chiến dịch và template email gửi báo cáo. Node *Wait* giúp giãn cách thời gian giữa các batch để tuân thủ rate limit của Instantly, tránh bị đánh dấu spam.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng dữ liệu mẫu để kiểm tra toàn bộ luồng chạy từ Exa AI -> PandaDoc -> Slack -> Google Sheets -> Instantly AI.
- Sau khi test thành công, bật công tắc **Active** để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Slack, các sếp có thể tích hợp thêm Telegram Bot hoặc Microsoft Teams để nhận thông báo chờ duyệt báo cáo linh hoạt hơn.
- **Lưu trữ Log chi tiết:** Bổ sung một node Google Sheets hoặc Airtable ở cuối workflow để ghi lại lịch sử gửi báo cáo thành công/thất bại phục vụ việc audit sau này.
- **Cá nhân hóa nội dung nâng cao:** Kết hợp thêm các node AI (như OpenAI/Claude) ở bước *Prep Batch Upload Data* để viết thêm lời chào riêng biệt dựa trên sở thích đầu tư của từng khách hàng trước khi đẩy qua Instantly AI.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các đội ngũ Sales và Marketing bất động sản muốn tự động hóa hoàn toàn khâu nghiên cứu và chăm sóc khách hàng quy mô lớn. Hãy cài đặt ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần!