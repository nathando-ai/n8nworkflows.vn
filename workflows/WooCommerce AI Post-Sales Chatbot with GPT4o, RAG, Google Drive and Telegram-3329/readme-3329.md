---
title: "🚀 Tự động hóa Chatbot Hậu bán hàng WooCommerce với GPT4o, RAG và Telegram"
description: "Hướng dẫn chi tiết cách triển khai chatbot AI hậu bán hàng tích hợp WooCommerce, Google Drive và Telegram để tự động hóa hỗ trợ khách hàng, kiểm tra đơn hàng và trả lời câu hỏi thường gặp."
slug: "tu-dong-hoa-chatbot-hau-ban-hang-woocommerce-gpt4o-rag-telegram"
tags: [n8n, automation, no-code, woocommerce, ai, telegram, google-drive]
keywords: [n8n workflow, tự động hóa, chatbot hậu bán hàng, woocommerce, ai, telegram, google drive]
---

# 🚀 Tự động hóa Chatbot Hậu bán hàng WooCommerce với GPT4o, RAG và Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình hỗ trợ hậu bán hàng
- Kiểm tra đơn hàng và thông tin vận chuyển trong thời gian thực
- Trả lời các câu hỏi thường gặp về chính sách trả hàng, thời gian giao hàng và điều khoản dịch vụ
- Tích hợp Telegram để chuyển tiếp các yêu cầu phức tạp đến nhân viên hỗ trợ
- Tăng cường bảo mật thông tin khách hàng thông qua xác thực email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WooCommerce với API key và secret key
- Tài khoản Google Drive với quyền truy cập vào thư mục chứa tài liệu hỗ trợ
- Tài khoản Qdrant với URL và API key
- Tài khoản OpenAI với API key
- Tài khoản Telegram với bot token và chat ID
- Plugin "YITH WooCommerce Order & Shipment Tracking" đã cài đặt trên WooCommerce
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [WooCommerce AI Post-Sales Chatbot with GPT4o, RAG, Google Drive and Telegram](https://n8n.io/workflows/3329) trên trang chủ n8n.
2. Nhấp vào nút "Download" để tải xuống file JSON của workflow.
3. Trong giao diện n8n Editor, nhấp vào nút "Import from File" và chọn file JSON đã tải xuống.
4. Hoặc, bạn có thể sao chép nội dung JSON từ trang web và dán vào nút "Import from Clipboard" trong n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **When chat message received**: Node này sẽ kích hoạt khi nhận được tin nhắn từ khách hàng. Bạn không cần cấu hình gì thêm.

- **Simple Memory**: Node này lưu trữ lịch sử cuộc trò chuyện để cung cấp ngữ cảnh cho các câu trả lời. Bạn không cần cấu hình gì thêm.

- **get_order, get_orders, get_user**: Các node này kết nối với WooCommerce để lấy thông tin đơn hàng và khách hàng. Bạn cần cấu hình credentials "wooCommerceApi" với API key và secret key của WooCommerce.

- **Calculator**: Node này thực hiện các phép tính toán. Bạn không cần cấu hình gì thêm.

- **When clicking ‘Test workflow’**: Node này kích hoạt khi bạn nhấp vào nút "Test workflow" trong n8n Editor. Bạn không cần cấu hình gì thêm.

- **Create collection, Refresh collection**: Các node này tạo và làm mới bộ sưu tập trong Qdrant. Bạn cần thay đổi các tham số "QDRANTURL" và "COLLECTION" trong các node này.

- **Get folder, Download Files**: Các node này truy cập vào Google Drive để tải xuống các tài liệu hỗ trợ. Bạn cần cấu hình credentials "googleDriveOAuth2Api" với thông tin xác thực Google Drive.

- **Default Data Loader, Token Splitter**: Các node này xử lý và chia nhỏ các tài liệu tải xuống từ Google Drive. Bạn không cần cấu hình gì thêm.

- **Qdrant Vector Store1, Embeddings OpenAI1, Qdrant Vector Store, Embeddings OpenAI**: Các node này tạo và quản lý vector database trong Qdrant. Bạn cần cấu hình credentials "qdrantApi" và "openAiApi" với thông tin xác thực Qdrant và OpenAI.

- **OpenAI Chat Model**: Node này sử dụng mô hình ngôn ngữ của OpenAI để tạo các câu trả lời tự động. Bạn cần cấu hình credentials "openAiApi" với thông tin xác thực OpenAI.

- **ToS**: Node này truy cập vào vector database để lấy thông tin về điều khoản dịch vụ. Bạn không cần cấu hình gì thêm.

- **get_tracking**: Node này lấy thông tin mã theo dõi đơn hàng từ WooCommerce. Bạn không cần cấu hình gì thêm.

- **When Executed by Another Workflow**: Node này kích hoạt khi workflow được thực thi bởi một workflow khác. Bạn không cần cấu hình gì thêm.

- **Post-Sales Agent**: Node này quản lý quá trình hỗ trợ hậu bán hàng. Bạn không cần cấu hình gì thêm.

- **human_assistence**: Node này gửi thông báo đến Telegram khi cần hỗ trợ từ nhân viên. Bạn cần cấu hình credentials "telegramApi" với thông tin xác thực Telegram và thay đổi tham số "CHAT_ID" trong node này.

- **Get tracking, Set tracking code**: Các node này lấy và thiết lập mã theo dõi đơn hàng. Bạn cần cấu hình credentials "httpBasicAuth" với thông tin xác thực WooCommerce và thay đổi URL trong node "Http Request" với URL của cửa hàng WooCommerce.

- **GPT 4o-mini**: Node này sử dụng mô hình ngôn ngữ GPT 4o-mini của OpenAI để tạo các câu trả lời tự động. Bạn cần cấu hình credentials "openAiApi" với thông tin xác thực OpenAI.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong các node quan trọng, bạn có thể thực hiện một test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Khi đã kiểm tra và đảm bảo workflow hoạt động đúng, bạn có thể kích hoạt workflow bằng cách nhấp vào nút "Active workflow" trong n8n Editor.

### ✍️ Mẹo & gợi ý nâng cao
- Tích hợp thêm các kênh truyền thông khác như Slack, Facebook Messenger hoặc WhatsApp để mở rộng phạm vi hỗ trợ khách hàng.
- Lưu trữ lịch sử cuộc trò chuyện để phân tích và cải thiện chất lượng hỗ trợ.
- Gửi báo cáo định kỳ về các yêu cầu hỗ trợ và hiệu suất của chatbot đến quản lý.
- Tích hợp với các hệ thống CRM khác để quản lý thông tin khách hàng và lịch sử giao dịch.

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để tự động hóa hỗ trợ hậu bán hàng trên WooCommerce, giúp các doanh nghiệp tiết kiệm thời gian và tăng cường trải nghiệm khách hàng. Bằng cách tích hợp các công nghệ AI và tự động hóa, workflow này đảm bảo rằng các yêu cầu của khách hàng được xử lý nhanh chóng và chính xác, đồng thời cung cấp một kênh hỗ trợ liên tục và hiệu quả.