---
title: "🚀 Tự Động Phân Tích Cảm Xúc & Chủ Đề Từ Jotform Với Google Gemini"
description: "Workflow n8n tự động trích xuất chủ đề, từ khóa và phân tích cảm xúc từ dữ liệu Jotform, sau đó lưu kết quả vào Google Sheets bằng AI Google Gemini."
slug: "phan-tich-cam-xuc-chu-de-jotform-gemini"
tags: [n8n, automation, no-code, google-gemini, jotform, google-sheets]
keywords: [n8n workflow, tự động hóa, phân tích cảm xúc, google gemini, jotform integration]
---

# 🚀 Tự Động Phân Tích Cảm Xúc & Chủ Đề Từ Jotform Với Google Gemini

Trong kinh doanh hiện đại, việc thu thập phản hồi từ khách hàng qua các biểu mẫu (forms) là cực kỳ quan trọng. Tuy nhiên, thách thức lớn nhất không nằm ở việc thu thập dữ liệu, mà là **xử lý và phân tích** chúng. Khi có hàng trăm hoặc hàng nghìn phản hồi mỗi ngày, việc đọc từng dòng để xác định khách hàng đang hài lòng hay phẫn nộ, cũng như tìm ra các chủ đề chính (topics) và từ khóa (keywords) nổi bật là một công việc tốn thời gian và dễ mắc sai sót.

Workflow n8n này giải quyết triệt để nỗi đau đó. Bằng cách kết hợp sức mạnh của **Google Gemini AI**, workflow sẽ tự động quét nội dung phản hồi từ **Jotform**, phân tích cảm xúc (Sentiment Analysis), trích xuất các chủ đề và từ khóa quan trọng, rồi tổng hợp tất cả vào **Google Sheets**. Toàn bộ quy trình diễn ra hoàn toàn tự động, không cần viết một dòng code nào, giúp các sếp tiết kiệm hàng giờ làm việc thủ công mỗi tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Loại bỏ hoàn toàn công đoạn đọc và phân tích thủ công phản hồi khách hàng.
- **Độ chính xác cao:** Sử dụng AI Google Gemini để đánh giá cảm xúc và trích xuất từ khóa chính xác hơn con người trong khối lượng lớn.
- **Dữ liệu có cấu trúc:** Kết quả được lưu vào Google Sheets với các cột rõ ràng (Cảm xúc, Chủ đề, Từ khóa), dễ dàng tạo báo cáo và dashboard.
- **Tự động hóa 100%:** Workflow chạy liên tục, xử lý ngay lập tức khi có phản hồi mới từ Jotform.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản miễn phí hoặc bản trả phí (khuyến nghị self-hosted).
2. **Tài khoản Jotform:** Có API Key hoặc OAuth2 credentials.
3. **Tài khoản Google:**
   - **Google Sheets:** Để lưu trữ dữ liệu.
   - **Google AI Studio (Gemini):** Để lấy API Key cho mô hình Gemini.
4. **Google Sheet:** Tạo sẵn một sheet với các cột tương ứng (ví dụ: `Response Text`, `Sentiment`, `Topics`, `Keywords`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này vào n8n của mình bằng cách:
- Tải xuống file JSON của workflow từ link gốc.
- Vào n8n Editor, chọn **Import from File** hoặc **Import from URL**.
- Hoặc copy toàn bộ JSON code và dán vào editor n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node sau để workflow chạy đúng:

1. **JotForm Trigger** (`jotFormTrigger`):
   - Chọn **Credentials** Jotform của bạn.
   - Chọn **Form ID** cụ thể mà các sếp muốn theo dõi.
   - Chọn **Trigger On**: `New Submission` (khi có phản hồi mới).

2. **Format the Form Data** (`code`):
   - Node này xử lý dữ liệu thô từ Jotform. Các sếp có thể chỉnh sửa code bên trong nếu cấu trúc dữ liệu form của mình khác (ví dụ: tên trường dữ liệu khác).
   - Mục đích: Chuẩn hóa dữ liệu để AI dễ đọc.

3. **Google Gemini Chat Model** (`lmChatGoogleGemini`):
   - Chọn **Credentials** Google Palm API (Gemini).
   - Chọn **Model**: Khuyến nghị dùng `gemini-1.5-flash` hoặc `gemini-1.5-pro` tùy theo độ phức tạp và chi phí.

4. **Sentiment Analyzer** (`chainLlm`):
   - Đây là node AI phân tích cảm xúc.
   - Kiểm tra **Prompt**: Đảm bảo prompt yêu cầu AI trả về cảm xúc (Positive, Negative, Neutral) một cách rõ ràng.
   - Kết nối với **Structured Output Parser** để đảm bảo output là JSON chuẩn.

5. **Topics & Keywords** (`chainLlm`):
   - Node AI trích xuất chủ đề và từ khóa.
   - Kiểm tra **Prompt**: Yêu cầu AI liệt kê các chủ đề chính và từ khóa quan trọng từ nội dung phản hồi.
   - Kết nối với **Structured Output Parser for Topics & Keywords**.

6. **Merge** (`merge`):
   - Node này gộp kết quả từ hai nhánh AI (Cảm xúc và Chủ đề/Từ khóa) lại với nhau.
   - Đảm bảo mode merge là `Append` hoặc `Combine` phù hợp.

7. **Aggregate** (`aggregate`):
   - Tổng hợp dữ liệu cuối cùng trước khi lưu.

8. **Append or update row in sheet** (`googleSheets`):
   - Chọn **Credentials** Google Sheets OAuth2.
   - Chọn **Document** (Sheet ID) và **Sheet Name**.
   - **Mapping**: Ánh xạ các trường dữ liệu từ output của Aggregate vào các cột tương ứng trong Google Sheet.
     - Ví dụ: `Sentiment` -> Cột "Cảm xúc"
     - `Topics` -> Cột "Chủ đề"
     - `Keywords` -> Cột "Từ khóa"
     - `Response Text` -> Cột "Nội dung phản hồi"

#### 3. Kích hoạt ⚡️
- **Test Run**: Gửi một phản hồi mẫu vào form Jotform của bạn.
- Chạy workflow bằng cách nhấn nút **Execute Workflow** hoặc chờ trigger tự động.
- Kiểm tra kết quả trong Google Sheet xem dữ liệu đã được điền đúng chưa.
- Nếu mọi thứ ổn, bật **Active** workflow để chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node **Slack** hoặc **Telegram** để gửi cảnh báo ngay lập tức khi phát hiện phản hồi có cảm xúc **Negative** (tiêu cực), giúp đội ngũ CSKH phản ứng nhanh.
- **Phân loại ưu tiên:** Thêm logic trong node Code để gán mức độ ưu tiên (High/Medium/Low) dựa trên cảm xúc và từ khóa, sau đó lọc ra các trường hợp khẩn cấp.
- **Tạo báo cáo định kỳ:** Sử dụng node **Cron** để chạy workflow tổng hợp dữ liệu từ Google Sheet hàng tuần và gửi email báo cáo cho quản lý.
- **Đa ngôn ngữ:** Nếu form nhận phản hồi bằng nhiều ngôn ngữ, hãy điều chỉnh prompt trong node AI để yêu cầu AI phân tích và trả về kết quả bằng tiếng Việt hoặc ngôn ngữ mong muốn.

### 📌 Kết luận
Việc tự động hóa phân tích phản hồi khách hàng không chỉ giúp tiết kiệm thời gian mà còn mang lại cái nhìn sâu sắc hơn về trải nghiệm người dùng. Với workflow n8n kết hợp Google Gemini này, các sếp có thể biến dữ liệu thô từ Jotform thành thông tin chiến lược một cách nhanh chóng và chính xác. Hãy thử ngay hôm nay và trải nghiệm sự khác biệt mà tự động hóa AI mang lại!