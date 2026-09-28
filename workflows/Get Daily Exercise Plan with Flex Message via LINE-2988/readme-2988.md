---
title: "🚀 Tự động tạo kế hoạch tập luyện hàng ngày và gửi thông báo Flex Message qua LINE với n8n và AI"
description: "Xây dựng trợ lý ảo YogiAI tự động gợi ý bài tập yoga hàng ngày từ Google Sheets, sử dụng AI để viết nội dung và gửi tin nhắn LINE Flex Message cực kỳ sinh động."
slug: "tu-dong-tao-ke-hoach-tap-luyen-line-flex-message-n8n"
tags: [n8n, automation, ai, line, google-sheets, azure-openai]
keywords: [n8n workflow, tự động hóa line, yoga ai bot, line flex message, azure openai n8n, google sheets automation]
---

# 🚀 Tự động tạo kế hoạch tập luyện hàng ngày và gửi thông báo Flex Message qua LINE với n8n và AI

Việc duy trì thói quen tập luyện hay gửi thông báo chăm sóc sức khỏe thủ công cho khách hàng hoặc nhóm mỗi ngày ngốn rất nhiều thời gian. Chưa kể việc phải thiết kế các mẫu tin nhắn bắt mắt (Flex Message) trên LINE lại càng phức tạp. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100%: Lấy dữ liệu tư thế tập ngẫu nhiên từ Google Sheets, nhờ Azure OpenAI viết nội dung thân thiện, tạo mã JSON Flex Message chuẩn chỉnh và đẩy thẳng thông báo đến tài khoản LINE của các sếp theo lịch trình cố định!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Lịch trình chạy đều đặn mỗi ngày (qua `Trigger 2130 YogaPosesToday`) mà không cần can thiệp thủ công.
- **Trải nghiệm trực quan:** Gửi tin nhắn LINE dạng **Flex Message** có kèm hình ảnh, mô tả sinh động, chuyên nghiệp.
- **Sử dụng AI thông minh:** Kết hợp Azure OpenAI (GPT-4o) cùng các cấu trúc Output Parser để đảm bảo dữ liệu JSON luôn hợp lệ và nội dung bài tập thân thiện, hấp dẫn.
- **Lưu log thông minh:** Tự động ghi lại lịch sử gửi vào Google Sheets để tối ưu hóa việc phân phối bài tập ngẫu nhiên theo trọng số (weighted random).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Tài khoản Azure OpenAI:** Có API Key và mô hình `4o` đã được triển khai.
- **Google Sheets:** Tài khoản Google Drive/Sheets chứa database các tư thế tập (tham khảo mẫu chuẩn từ tác giả [tại đây](https://docs.google.com/spreadsheets/d/1eqLJsUL_QkOMy_qPzNCrUCZdx36asC8P1i3PowTQqLY/edit?usp=sharing)).
- **LINE Official Account / Messaging API:** Đã cấu hình LINE Bot, lấy được Channel Access Token và User ID (`to`) để nhận tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc copy toàn bộ JSON và dán vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thành phần sau để workflow chạy mượt mà:
- **Trigger Node (`Trigger 2130 YogaPosesToday`):** Điều chỉnh lại múi giờ và thời gian chạy lịch trình (Schedule) theo ý muốn.
- **Google Sheets Nodes (`PosesDatabase1`, `YogaLog`, `YogaLog2`, `Get PoseName`):** Kết nối tài khoản Google Sheets OAuth2 và trỏ đến file Google Sheets quản lý tư thế tập của các sếp. Nhớ cập nhật lại tên Sheet và cấu trúc cột cho khớp với database mẫu.
- **Azure OpenAI Nodes (`Azure OpenAI Chat Model`, `Azure OpenAI Chat Model1`, v.v.):** Cung cấp thông tin đăng nhập `azureOpenAiApi` và chọn đúng model `4o`. Các node AI này chịu trách nhiệm chọn lọc tư thế, viết văn bản hướng dẫn và sinh mã JSON Flex Message.
- **HTTP Request Node (`Line Push with Flex Bubble`):** 
  - Cấu hình thông tin xác thực `httpHeaderAuth` với Channel Access Token từ LINE Developer Console.
  - Thay thế trường `to` bằng LINE User ID thực tế của các sếp để nhận tin nhắn test.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm (Test run) và kiểm tra xem tin nhắn đã được đẩy về LINE hay chưa.
- Kiểm tra các bảng Google Sheets xem dữ liệu log đã được ghi nhận chính xác chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc **Active** góc trên cùng bên phải để bật workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Các sếp có thể nhân bản nhánh cuối để vừa gửi qua LINE, vừa bắn thông báo sang **Telegram**, **Slack** hoặc **Zalo ZNS** cho nhóm tập luyện cùng theo dõi.
- **Lưu trữ lịch sử chi tiết:** Tận dụng các node Google Sheets để thống kê xem người dùng đã tập những động tác nào nhiều nhất trong tuần/tháng.
- **Tùy biến Prompt AI:** Tinh chỉnh các prompt trong các node `Chain LLM` để phong cách hướng dẫn tập luyện trở nên hài hước, nghiêm túc hoặc cá nhân hóa hơn theo từng đối tượng.

### 📌 Kết luận
Với workflow n8n kết hợp AI và LINE Flex Message này, việc vận hành một trợ lý chăm sóc sức khỏe hay kênh thông tin tự động trở nên đơn giản hơn bao giờ hết. Chúc các sếp "lên đồ" thành công và tự động hóa thành công quy trình của mình!