---
title: "🚀 Tự Động Viết Kịch Bản Meta Ads Chuyển Đổi Cao Với GPT & Gemini"
description: "Workflow n8n giúp các sếp biến dữ liệu hiệu suất quảng cáo thành kịch bản video chuyển đổi cao chỉ với 1 tin nhắn Telegram, hoàn toàn không cần code."
slug: "tu-dong-viet-kich-ban-meta-ads-gpt-gemini"
tags: [n8n, automation, no-code, meta-ads, ai-marketing, notion]
keywords: [n8n workflow, tự động hóa quảng cáo, viết kịch bản ads, GPT-4, Gemini, Telegram bot]
---

# 🚀 Tự Động Viết Kịch Bản Meta Ads Chuyển Đổi Cao Với GPT & Gemini

Viết kịch bản quảng cáo (Ad Copy) cho Meta (Facebook/Instagram) luôn là một bài toán đau đầu. Các sếp thường phải dành hàng giờ để phân tích dữ liệu hiệu suất (CTR, CVR, ROAS), nghiên cứu tâm lý khách hàng, và thử nghiệm hàng chục phiên bản kịch bản khác nhau. Việc làm thủ công này không chỉ tốn thời gian mà còn dễ dẫn đến sự thiếu nhất quán trong thông điệp, khiến ngân sách quảng cáo bị lãng phí vào những nội dung kém hiệu quả.

Workflow này là giải pháp "chìa khóa trao tay" giúp các sếp tự động hóa toàn bộ quy trình sáng tạo nội dung quảng cáo. Chỉ cần gửi một tin nhắn hoặc file audio qua Telegram, hệ thống sẽ tự động phân tích dữ liệu, sử dụng sức mạnh của AI (OpenAI GPT và Google Gemini) để tạo ra kịch bản video chuyển đổi cao, sau đó lưu trữ có hệ thống vào Notion và thông báo kết quả ngay trên Telegram.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần xử lý các yêu cầu AI liên tục, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian sáng tạo:** Biến ý tưởng thô hoặc dữ liệu hiệu suất thành kịch bản hoàn chỉnh chỉ trong vài phút.
- **Tối ưu hóa chi phí quảng cáo:** Kịch bản được AI phân tích dựa trên các nguyên tắc chuyển đổi cao, giúp tăng CTR và giảm CPC.
- **Quản lý nội dung tập trung:** Tất cả kịch bản được lưu tự động vào Notion, dễ dàng tra cứu, chỉnh sửa và phân công cho team sản xuất video.
- **Tương tác thời gian thực:** Nhận kết quả ngay trên Telegram, phù hợp với nhịp độ làm việc nhanh của các team Marketing.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và credentials sau:
1. **Tài khoản n8n:** Đã cài đặt và chạy (Self-hosted hoặc Cloud).
2. **Telegram Bot:** Tạo bot qua @BotFather để lấy `Bot Token`.
3. **OpenAI API Key:** Dùng cho các node `Transcribe Audio`, `OpenAI`, và `Generate Script Outline`.
4. **Notion API Token:** Tạo Integration trong Notion và cấp quyền truy cập vào Database chứa kịch bản.
5. **Dữ liệu đầu vào:** Các sếp cần có sẵn dữ liệu hiệu suất quảng cáo (có thể gửi dưới dạng text hoặc audio mô tả) để AI phân tích.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/7145` HOẶC copy toàn bộ JSON của workflow và dán vào editor.
3. Sau khi import, các sếp sẽ thấy các node chính: `Telegram Trigger`, `Transcribe Audio`, `Code`, `OpenAI`, `Generate Script Outline`, `Save to Notion`, và `Telegram`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình credentials cũng như tham số:

*   **Node: `Telegram Trigger`**
    *   Chọn **Credentials**: Chọn hoặc tạo mới credentials Telegram (dán `Bot Token` đã lấy từ BotFather).
    *   **Lưu ý:** Workflow sẽ kích hoạt khi nhận được tin nhắn từ user đã được phép (hoặc tất cả user tùy cấu hình).

*   **Node: `Transcribe Audio` (OpenAI)**
    *   Chọn **Credentials**: OpenAI API Key.
    *   **Model**: Chọn model hỗ trợ audio-to-text (ví dụ: `whisper-1`).
    *   **Input**: Node này sẽ nhận file audio từ Telegram. Nếu các sếp chỉ gửi text, node này có thể bị bỏ qua hoặc cần logic xử lý thêm (tuy nhiên, workflow gốc thiết kế để hỗ trợ cả audio).

*   **Node: `Code`**
    *   Node này thường dùng để xử lý dữ liệu thô, định dạng lại input trước khi đưa vào LLM. Các sếp nên kiểm tra lại logic code nếu dữ liệu đầu vào của mình khác với mẫu gốc (ví dụ: thay đổi cấu trúc JSON của dữ liệu hiệu suất).

*   **Node: `OpenAI` & `Generate Script Outline`**
    *   Chọn **Credentials**: OpenAI API Key.
    *   **Model**: Khuyến nghị dùng `gpt-4o` hoặc `gpt-4-turbo` để có chất lượng kịch bản tốt nhất.
    *   **System Prompt / User Prompt**: Đây là "linh hồn" của workflow. Các sếp cần chỉnh sửa prompt để phù hợp với ngách sản phẩm của mình.
        *   *Ví dụ:* Thay đổi yêu cầu từ "viết kịch bản cho sản phẩm X" thành "viết kịch bản video 30 giây cho dịch vụ tư vấn tài chính, giọng văn chuyên nghiệp, tập trung vào nỗi đau về lãi suất...".
    *   **Lưu ý về Gemini:** Workflow gốc có thể tích hợp Gemini qua node HTTP Request hoặc Code. Nếu các sếp muốn dùng Gemini, hãy kiểm tra node `HTTP Request` (nếu có) hoặc node `Code` để đảm bảo API key Gemini được cấu hình đúng.

*   **Node: `Save to Notion` & `Save to Notion1`**
    *   Chọn **Credentials**: Notion API Token.
    *   **Database ID**: Dán ID của Database trong Notion mà các sếp muốn lưu kịch bản.
    *   **Properties**: Kiểm tra mapping các trường dữ liệu (ví dụ: `Title`, `Script Content`, `Performance Data`, `Date`) để đảm bảo thông tin được điền đúng cột trong Notion.

*   **Node: `Telegram` (Output)**
    *   Chọn **Credentials**: Cùng Telegram Bot Token ở trên.
    *   **Chat ID**: Có thể để trống nếu muốn gửi vào chat riêng tư của người gửi, hoặc cấu hình gửi vào Group ID nếu muốn chia sẻ chung cho team.
    *   **Message**: Kiểm tra template tin nhắn để đảm bảo hiển thị đầy đủ kịch bản và link Notion (nếu có).

#### 3. Kích hoạt ⚡️
1. **Test Run**: Nhấn nút **Execute Workflow**. Sau đó, mở Telegram và gửi một tin nhắn mẫu (ví dụ: "Viết kịch bản cho sản phẩm áo thun, dữ liệu hiệu suất: CTR 2%, CVR 1%").
2. Kiểm tra xem có lỗi credentials không. Nếu thành công, các sếp sẽ nhận được tin nhắn phản hồi từ Bot.
3. Kiểm tra Notion xem kịch bản đã được lưu chưa.
4. Bật **Active** (công tắc xanh) để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm A/B Testing:** Tạo 2 node OpenAI song song với 2 prompt khác nhau (ví dụ: một bên tập trung vào cảm xúc, một bên tập trung vào lý trí) để AI tạo ra 2 phiên bản kịch bản, sau đó gửi cả hai lên Telegram để team chọn.
- **Tự động hóa lên lịch đăng bài:** Kết nối thêm node `Meta Ads Manager` hoặc `Buffer` để tự động lên lịch đăng video sau khi kịch bản được duyệt.
- **Phân tích cảm xúc (Sentiment Analysis):** Thêm một bước AI để đánh giá mức độ "aggressive" hay "soft" của kịch bản, giúp các sếp kiểm soát tone & voice thương hiệu chặt chẽ hơn.
- **Lưu trữ phiên bản:** Trong Notion, thêm một property `Version` và `Status` (Draft, Approved, Published) để quản lý vòng đời của kịch bản một cách chuyên nghiệp.

### 📌 Kết luận
Việc sử dụng AI để viết kịch bản quảng cáo không còn là điều xa xỉ, mà là lợi thế cạnh tranh cần thiết trong kỷ nguyên digital. Với workflow n8n này, các sếp có thể biến quy trình sáng tạo nội dung quảng cáo từ thủ công, chậm chạp thành một dòng chảy tự động, nhanh chóng và chính xác. Hãy import workflow, chỉnh sửa prompt cho phù hợp với sản phẩm của mình, và bắt đầu tiết kiệm hàng giờ mỗi tuần ngay từ hôm nay!