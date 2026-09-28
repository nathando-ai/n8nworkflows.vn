---
title: "🤖 Tự Động Hóa Phân Tích & Phân Loại Feedback Theo Sentiment (Typeform + AI GCP + Notion + Trello)"
description: "Workflow tự động hóa nhận feedback từ Typeform, phân tích tình cảm (sentiment) bằng AI GCP, phân loại vào Notion và Trello, đồng thời thông báo kết quả trên Slack - tiết kiệm 100% thời gian phân tích thủ công."
slug: "tu-dong-hoa-phan-tich-feedback-theo-sentiment"
tags: [n8n, automation, ai-summarization, sentiment-analysis, trello-notion-integration]
keywords: [n8n workflow sentiment analysis, tự động hóa feedback, phân tích tình cảm AI, Typeform Trello Notion, tự động hóa doanh nghiệp]
---

# 🚀 **Tự Động Hóa Phân Tích Feedback Theo Sentiment: Từ Typeform → AI → Notion → Trello**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải:
- **Nhận hàng chục phản hồi** từ khách hàng qua Typeform, Google Form hay email.
- **Phân tích từng câu** để xác định tình cảm (positive/negative/neutral) bằng mắt thường.
- **Chuyển dữ liệu** vào Notion/Trello để theo dõi, nhưng lại quên hoặc làm sai.
- **Mất thời gian** để báo cáo kết quả cho team, trong khi AI có thể làm tốt hơn.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Nhận phản hồi** từ Typeform.
✅ **Phân tích sentiment** bằng AI GCP (chính xác hơn 90% so với con người).
✅ **Phân loại phản hồi** vào Notion (theo label) và Trello (theo board).
✅ **Gửi thông báo Slack** khi có phản hồi tích cực (positive feedback).
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** phân tích feedback thủ công.
- **Chính xác 100%** với phân loại sentiment bằng AI.
- **Dữ liệu sạch** được tự động lưu vào Notion/Trello, không sai sót.
- **Team được thông báo kịp thời** khi có phản hồi tích cực qua Slack.
- **Báo cáo tự động** theo dõi xu hướng sentiment trong tháng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Typeform** (để nhận phản hồi).
2. **API Key GCP Natural Language** (để phân tích sentiment).
   - 👉 [Cài đặt API GCP](https://cloud.google.com/natural-language/docs/base/quickstart-client-libraries) (mã giảm giá 200$ cho mới: **N8N200**).
3. **Tài khoản Notion** (để lưu phản hồi theo database).
4. **Tài khoản Trello** (để tạo card theo dõi follow-up).
5. **Webhook Slack** (để nhận thông báo phản hồi tích cực).
6. **Credentials cho các API** (xem hướng dẫn dưới đây).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có 2 cách:
- **Tải file JSON** từ [n8n.io/workflows/7243](https://n8n.io/workflows/7243) và import vào n8n Editor.
- **Copy JSON** từ link trên và paste vào **Import Workflow** trong n8n.

:::note[Lưu ý]
- **Không cần chỉnh sửa cấu trúc** của workflow, chỉ cần điền credentials.
- **Nên cài n8n trên VPS** để workflow hoạt động 24/7 (không bị ngắt kết nối).
:::

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình:

| **Node**                          | **Lưu Ý Cần Chỉnh**                                                                 | **Tham Số Cần Điền**                          |
|-----------------------------------|------------------------------------------------------------------------------------|-----------------------------------------------|
| **Typeform: New Submission**      | Chọn **credentials** là `typeformApi`.                                            | -                                             |
| **Analyze Feedback Sentiment**    | Chọn **credentials** là `googleCloudNaturalLanguageOAuth2Api`.                     | -                                             |
| **Check Sentiment Score**         | Cấu hình **If Condition** để phân loại sentiment (ví dụ: `sentiment.score > 0.5` → Positive). | `{{ $json["sentiment"]["score"] }} > 0.5` |
| **Add Feedback to Notion**        | Chọn **database** và **properties** trong Notion (ví dụ: `Feedback`, `Sentiment`). | `databaseId`, `pageProperties`               |
| **Notify Slack with Positive FB** | Chọn **Slack channel** và cấu hình **message template**.                          | `channel`, `text` (ví dụ: `🎉 Feedback tích cực từ {{ $json["name"] }}!`) |
| **Create Trello Card for Follow-up** | Chọn **board** và **list** trong Trello (ví dụ: `Follow-up Negative`).          | `boardId`, `listId`, `name` (tự động lấy từ feedback) |

:::tip[Mẹo]
- **Test với 1 phản hồi mẫu** trước khi bật workflow.
- **Sử dụng Notion API** để tạo database mới nếu chưa có (ví dụ: `Feedback Database`).
- **Trello Card** sẽ tự động tạo với tiêu đề là **phản hồi** và mô tả là **sentiment score**.
:::

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với 1 phản hồi mẫu (ví dụ: "Tôi rất hài lòng với dịch vụ!").
2. **Bật Active** workflow sau khi kiểm tra kết quả.
3. **Monitor Slack** để xem phản hồi tích cực được thông báo không.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM NGOÀI]
1. **Gửi báo cáo định kỳ** (ví dụ: hàng tuần) về sentiment score qua Email.
   - Sử dụng **n8n-nodes-base.email** + **n8n-nodes-base.date** để tính ngày cuối tuần.
2. **Kết hợp với Google Sheets** để lưu lịch sử phản hồi.
   - Thêm node **Google Sheets** sau **Add Feedback to Notion**.
3. **Tự động tạo Trello Card cho phản hồi tiêu cực** (negative sentiment) với label `Urgent`.
4. **Sử dụng AI GPT-4** (thay cho GCP) để phân tích sentiment chi tiết hơn.
   - Thêm node **n8n-nodes-base.llm** (OpenAI) sau **Analyze Feedback Sentiment**.
5. **Lưu log hoạt động** vào Notion để theo dõi lỗi.
   - Thêm node **n8n-nodes-base.notion** với property `Log`.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc phân tích feedback thủ công, đồng thời **tăng độ chính xác** với AI. **Chỉ cần 10 phút setup**, các sếp sẽ có một hệ thống tự động hóa hoàn chỉnh từ **nhận phản hồi → phân tích → lưu trữ → thông báo**.

**Hành động ngay!**
1. **Đăng ký VPS** để self-host n8n (để workflow chạy 24/7).
   👉 [VPS TinoHost (Mã giảm 39%)](https://tino.vn/vps-n8n?affid=388) (**VPSN8N**)
   👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
2. **Import workflow** và bắt đầu tự động hóa!
3. **Chia sẻ kết quả** với team để cùng cải thiện dịch vụ.

**Cảm ơn các sếp đã đọc đến đây!** 🚀