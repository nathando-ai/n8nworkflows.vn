---
title: "🚀 Tự động phân loại email Gmail và soạn thảo thư nháp thông minh bằng GPT-4 với n8n"
description: "Hướng dẫn xây dựng hệ thống tự động hóa n8n giúp phân loại email đến, gắn nhãn ưu tiên và tự động tạo nội dung trả lời nháp bằng OpenAI GPT-4."
slug: "phan-loai-email-gmail-va-tao-nhap-gpt-4-n8n"
tags: [n8n, automation, no-code, gmail, openai, gpt-4, ai-automation]
keywords: [n8n workflow, tự động hóa gmail, phân loại email bằng ai, openAi gpt-4 n8n, tao draft email tu dong]
---

# 🚀 Tự động phân loại email Gmail và soạn thảo thư nháp thông minh bằng GPT-4

Các sếp có bao giờ cảm thấy ngợp thở mỗi sáng khi mở hộp thư đến (Inbox) với hàng chục, thậm chí hàng trăm email lẫn lộn từ việc khẩn cấp, câu hỏi chung cho đến các vấn đề tài chính, hóa đơn? Việc đọc thủ công, phân loại rồi ngồi soạn từng email phản hồi ngốn rất nhiều thời gian quý báu mà lẽ ra các sếp nên dành cho việc chốt deal hay phát triển kinh doanh.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh: **Gmail Email Classifier with GPT-4 Auto-Generated Draft Replies**. Hệ thống sẽ tự động quét email đến, nhờ AI phân loại chủ đề, tự động gắn nhãn (Label) màu sắc tương ứng và chuẩn bị sẵn một bản thảo trả lời (Draft) cực kỳ chuyên nghiệp ngay trong tài khoản Gmail của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phân loại tự động:** AI tự động đọc hiểu nội dung email và chia vào 3 nhóm cụ thể: Khẩn cấp (High Priority), Thắc mắc chung (Inquiry), và Tài chính/Hóa đơn (Finance/Billing).
- **Gắn nhãn khoa học:** Tự động áp dụng nhãn Gmail tương ứng để hộp thư lúc nào cũng gọn gàng, trực quan.
- **Tiết kiệm 80% thời gian:** Tự động tạo sẵn bản thảo (Draft) trả lời bằng GPT-4 dựa trên ngữ cảnh thực tế của email khách hàng, các sếp chỉ cần bấm "Gửi" hoặc tinh chỉnh lại chút ít.
- **Hoạt động 24/7:** Không bỏ sót bất kỳ email quan trọng nào ngay cả khi các sếp đang ngủ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google/Gmail** (đã cấp quyền kết nối với n8n và đã tạo sẵn các nhãn/labels trong Gmail tương ứng).
- **OpenAI API Key** (có hạn mức sử dụng để gọi model GPT-4 / GPT-4o-mini).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n, sau đó tại giao diện n8n Editor, chọn **Add workflow** -> Dán hoặc Import file JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp nhớ cấu hình kỹ các điểm mấu chốt sau:

- **Node `Gmail Trigger`**: Kết nối tài khoản Gmail của các sếp. Node này sẽ đóng vai trò "còi báo động", kích hoạt workflow ngay khi có email mới gửi đến.
- **Model AI trung tâm (`LLM Support Model`)**: Cấu hình credentials OpenAI và chọn model phù hợp (ví dụ: `gpt-4.1-mini` hoặc `gpt-4o-mini`).
- **Node `Gmail Category Classifier`**: Đây là bộ não phân loại sử dụng công nghệ LangChain Text Classifier, giúp điều hướng email dựa trên nội dung tiếng Việt hoặc tiếng Anh.
- **Các node Gắn nhãn & Lưu nháp (`Label: High Priority`, `Save Draft: High Priority`, v.v.)**: 
  - Đảm bảo trỏ đúng tài khoản Gmail.
  - **Lưu ý quan trọng**: Thay thế các giá trị `YOUR_LABEL_ID_XXX` bằng ID nhãn thực tế trong tài khoản Gmail của các sếp (Các sếp có thể lấy ID nhãn bằng cách gọi API List Labels của Gmail hoặc tạo sẵn nhãn trong cài đặt Gmail).

#### 3. Kích hoạt ⚡️
- Bấm nút **Test workflow** và gửi một email mẫu đến hộp thư của các sếp để kiểm tra xem hệ thống có tự động gắn nhãn và tạo draft hay không.
- Nếu mọi thứ chạy xanh mướt, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

---

### ✍️ Mẹo & gợi ý nâng cao
Muốn hệ thống "bá đạo" hơn nữa? Các sếp hoàn toàn có thể mở rộng workflow này với các ý tưởng sau:
1. **Tích hợp Slack/Telegram**: Bắn một thông báo kèm nội dung tóm tắt và link email vào nhóm chat nội bộ khi có email `High Priority` xuất hiện.
2. **Lưu log vào Google Sheets**: Ghi lại lịch sử phân loại email, thời gian nhận và trạng thái xử lý để làm báo cáo tuần/tháng.
3. **Cá nhân hóa Prompt AI**: Tinh chỉnh prompt trong các node `Generate Draft` để AI trả lời theo văn phong riêng của công ty (trang trọng, gần gũi, hoặc chèn sẵn chữ ký, thông tin liên hệ).

### 📌 Kết luận
Việc tự động hóa quy trình xử lý email đầu vào không chỉ giúp tiết kiệm hàng giờ đồng hồ mỗi tuần mà còn nâng cấp dịch vụ chăm sóc khách hàng lên một tầm cao mới nhờ tốc độ phản hồi chớp nhoáng. Hãy áp dụng ngay workflow này vào hệ thống của các sếp và cảm nhận sự khác biệt!