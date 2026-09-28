---
title: "🚀 Tự động hóa phân loại và định tuyến email khách hàng thương mại điện tử với AI trong n8n"
description: "Hướng dẫn xây dựng hệ thống tự động phân loại yêu cầu từ form liên hệ e-commerce bằng AI Text Classifier, tự động điều hướng đến đúng phòng ban và lưu trữ dữ liệu vào Google Sheets."
slug: "tu-dong-hoa-phan-loai-dinh-tuyen-email-ai-ecommerce-n8n"
tags: [n8n, automation, no-code, ai, openai, ecommerce, google-sheets]
keywords: [n8n workflow, phân loại email bằng ai, text classifier, tự động hóa ecommerce, openai gpt-4o-mini]
---

# 🚀 Tự động hóa phân loại và định tuyến email khách hàng thương mại điện tử với AI

Các sếp đang kinh doanh thương mại điện tử (eCommerce) chắc chắn luôn đối mặt với cơn ác mộng mang tên: Hàng trăm email, yêu cầu hỗ trợ (support ticket) từ khách hàng đổ về mỗi ngày nhưng lại bị gom chung vào một hộp thư đến (inbox). Nhân viên mất hàng giờ đồng hồ chỉ để đọc, phân loại thủ công xem email nào cần chuyển cho bộ phận Đơn hàng (Order), Kỹ thuật/Sản phẩm (Product), Báo giá (Quote) hay Hỗ trợ chung (General). Việc này vừa chậm trễ, vừa dễ sai sót.

Giải pháp ở đây là gì? Hãy để AI làm thay các sếp! Workflow n8n này sẽ tự động hóa 100% quy trình: tiếp nhận thông tin từ form liên hệ, dùng AI thông minh phân loại ý định của khách hàng, sau đó tự động gửi email thông báo cho đúng phòng ban phụ trách và đồng thời lưu toàn bộ dữ liệu vào Google Sheets tương ứng để quản lý.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Khách hàng vừa bấm gửi form là hệ thống tự động phân tích và xử lý ngay lập tức mà không cần con người nhúng tay vào.
- **Độ chính xác cao:** Nhờ sức mạnh của mô hình OpenAI (GPT-4o-mini) kết hợp với node `Text Classifier`, nội dung của khách hàng được phân loại chính xác vào đúng 5 phòng ban: Sản phẩm, Báo giá, Đơn hàng, Tổng hợp và Khác.
- **Đa kênh lưu trữ:** Tự động ghi nhận thông tin vào các Google Sheets riêng biệt tùy theo danh mục để các bộ phận dễ dàng theo dõi và xử lý.
- **Vận hành không gián đoạn:** Hoạt động 24/7, loại bỏ hoàn toàn tình trạng bỏ sót email hoặc chuyển nhầm phòng ban.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để cấu hình thành công workflow này, các sếp cần chuẩn bị sẵn:
- **Tài khoản OpenAI:** Lấy API Key để kết nối với node LLM (`gpt-4o-mini`).
- **Tài khoản Google:** Để cấu hình kết nối Google Sheets (`Google Sheets OAuth2 API`).
- **Hệ thống gửi Email:** Tài khoản SMTP (hoặc các dịch vụ gửi email tương đương như Gmail, SendGrid, Outlook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện n8n (ID: `2851`), sau đó vào giao diện n8n Editor chọn **Import from File** hoặc sao chép và dán trực tiếp JSON vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hệ thống sẽ hiển thị 13 nodes bao gồm Form Trigger, Text Classifier, OpenAI, các node Email (SMTP) và Google Sheets. Các sếp cần cấu hình kỹ các điểm sau:

- **On form submission (`formTrigger`):** Đây là điểm khởi đầu lấy dữ liệu từ form khách hàng. Các sếp có thể thay thế node này bằng webhook nếu dùng form ngoài (như Contact Form 7 trên WordPress, Typeform, Webflow...).
- **OpenAI (`lmChatOpenAi`):** Cần gắn Credentials của OpenAI và giữ nguyên model `gpt-4o-mini` để tối ưu chi phí và tốc độ xử lý.
- **Text Classifier (`textClassifier`):** Node trung tâm để cấu hình các nhãn (categories) phân loại yêu cầu thành các phòng ban tương ứng: *Prod. Dep.*, *Quote Dep.*, *Order Dep.*, *Gen. Dep.*, và *Other Dep.*.
- **Các node Email (`Prod. Dep.`, `Quote Dep.`, `Gen. Dep.`, `Order Dep.`, `Other Dep.`):** Cần cấu hình thông tin kết nối SMTP (Host, Port, User, Pass) và email người nhận của từng phòng ban cụ thể.
- **Các node Google Sheets (`Prod DB`, `Quote DB`, `General DB`, `Order DB`, `Other DB`):** Kết nối tài khoản Google Sheets của các sếp, chọn đúng Spreadsheet ID và Sheet Name tương ứng cho từng bảng dữ liệu lưu trữ yêu cầu khách hàng (`operation`: `append`).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền form mẫu để kiểm tra dữ liệu có được phân loại đúng phòng ban và ghi vào đúng Google Sheets hay không.
- Nếu mọi thứ chạy mượt mà, hãy bật nút **Active** ở góc trên cùng bên phải để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot/Slack:** Thêm node Slack hoặc Telegram để bắn thông báo khẩn vào group nội bộ ngay khi có yêu cầu đặt hàng lớn hoặc khiếu nại từ khách hàng.
- **Cá nhân hóa phản hồi tự động:** Thêm một node Email gửi thẳng cho khách hàng với nội dung: *"Cảm ơn bạn đã liên hệ, yêu cầu của bạn đã được chuyển đến bộ phận [Tên phòng ban] và sẽ được phản hồi trong vòng 2 giờ"* để nâng cao trải nghiệm khách hàng.
- **Mở rộng danh mục:** Dễ dàng bổ sung thêm các nhánh phân loại mới trên Text Classifier nếu doanh nghiệp của các sếp có thêm các phòng ban chuyên trách khác (ví dụ: Bảo hành, Hoàn tiền...).

### 📌 Kết luận
Modular & Customizable AI-Powered Email Routing là một "vũ khí" tối tân giúp tự động hóa khâu chăm sóc khách hàng ban đầu cho các cửa hàng online. Áp dụng ngay hôm nay để tiết kiệm thời gian, tối ưu hóa đội ngũ nhân sự và làm hài lòng khách hàng tốt hơn các sếp nhé!