---
title: "🤖 Tự Động Phân Tích & Lọc Leads từ Đánh Giá Khách Hàng bằng AI (GPT-4o-mini + Google Sheets)"
description: "Workflow tự động hóa phân tích sentiment, định hướng ý kiến khách hàng và đánh giá số điểm từ đánh giá trên Google Sheets, kết hợp với AI Azure GPT-4o-mini để tạo cơ sở dữ liệu leads chất lượng cao 24/7."
slug: "tieu-dong-phan-tich-leads-danh-gia-khach-hang"
tags: [n8n, automation, ai-summarization, azure-openai, google-sheets, self-hosted]
keywords: [n8n workflow phân tích leads, tự động hóa đánh giá khách hàng, AI GPT-4o-mini, phân tích sentiment tự động, Google Sheets tự động hóa]
---

# 🚀 **Tự Động Phân Tích & Lọc Leads từ Đánh Giá Khách Hàng bằng AI**

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm 10+ giờ/tuần** phân tích đánh giá khách hàng thủ công?
- **Hiểu rõ ý kiến khách hàng** (phê bình, đề xuất, yêu cầu) chỉ trong vài giây?
- **Lọc leads chất lượng** từ hàng trăm đánh giá hàng ngày?
- **Cập nhật tự động** cơ sở dữ liệu phản hồi khách hàng trên Google Sheets?

Workflow này **tự động hóa toàn bộ quy trình** từ nhận dữ liệu đánh giá → phân tích AI → lưu trữ kết quả → tạo cơ sở dữ liệu leads sẵn sàng cho marketing/sales.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ xử lý AI nhanh)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa 100%** phân tích đánh giá khách hàng (không cần code).
✅ **Phân loại chính xác** ý kiến khách hàng (phê bình, đề xuất, yêu cầu, khen ngợi).
✅ **Đánh giá sentiment** (tích cực, tiêu cực, trung lập) và **điểm số 1-10** cho từng đánh giá.
✅ **Tóm tắt ngắn gọn** ý kiến khách hàng để marketing/sales dễ tiếp cận.
✅ **Cập nhật tự động** cơ sở dữ liệu leads trên Google Sheets, sẵn sàng cho phân tích tiếp theo.
✅ **Hoạt động liên tục** 24/7, không phụ thuộc vào nhân viên.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với quyền chỉnh sửa:
   - **Sheet nguồn**: Chứa dữ liệu đánh giá khách hàng (cột: `Timestamp`, `Name`, `Email`, `Contact`, `Review Text`).
   - **Sheet đích**: Để lưu kết quả phân tích (các cột: `Intent`, `Sentiment`, `Score`, `Summary`).
2. **API Key Azure OpenAI**:
   - **Model**: `gpt-4o-mini` (hoặc tương đương).
   - **Endpoint**: Cấu hình trong `azureOpenAiApi` (n8n sẽ yêu cầu).
3. **Credentials OAuth2 cho Google Sheets**:
   - Thiết lập trong `googleSheetsTriggerOAuth2Api` và `googleSheetsOAuth2Api`.

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8278](https://n8n.io/workflows/8278) hoặc copy JSON từ canvas.
- **Mở n8n Editor** → Nhấn `Import` → Dán JSON → Chọn `Import`.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **Node 1: Google Sheets Trigger**
- **Chọn credentials**: `googleSheetsTriggerOAuth2Api`.
- **Cấu hình**:
  - **Sheet Name**: Tên sheet chứa dữ liệu đánh giá (ví dụ: `CustomerReviews`).
  - **Range**: `A1:E1000` (đảm bảo bao gồm tất cả cột cần theo dõi).
  - **Polling Interval**: `60000` (1 phút) để cập nhật thường xuyên.

#### **Node 2: AI Agent (Azure GPT-4o-mini)**
- **Chọn credentials**: `azureOpenAiApi`.
- **Cấu hình Prompt**:
  ```json
  {
    "system_prompt": "You are a professional customer review analyzer. Your task is to analyze the following review and extract the following fields in JSON format:\n\n1. Intent: The purpose of the review (praise, complaint, suggestion, feature request)\n2. Sentiment: Positive, negative, neutral, or mixed\n3. Score: A numerical score from 1-10 (1 = very negative, 10 = very positive)\n4. Summary: A concise summary of the review (max 100 words)\n\nReturn ONLY the JSON object with these fields. Do not include any additional text."
  }
  ```
- **Model**: Đảm bảo chọn `gpt-4o-mini` trong `keyParameters`.

#### **Node 3: Code - Parse AI JSON**
- **Mã JavaScript** (không cần chỉnh sửa, nhưng các sếp có thể mở để hiểu logic):
  ```javascript
  // Kết hợp dữ liệu nguyên thủy với kết quả AI
  return {
    json: {
      ...node.input.all[0].json,
      ...node.input.all[1].json.data.choices[0].message.content // JSON từ AI
    }
  };
  ```
- **Lưu ý**: Node này tự động **parse JSON** từ AI và **ghép với dữ liệu khách hàng** (tên, email, review text).

#### **Node 4: Google Sheets - Update Lead**
- **Chọn credentials**: `googleSheetsOAuth2Api`.
- **Cấu hình**:
  - **Sheet Name**: Tên sheet đích (ví dụ: `ProcessedReviews`).
  - **Range**: `A1:F1000` (đảm bảo đủ cột cho `Intent`, `Sentiment`, `Score`, `Summary`).
  - **Operation**: `appendOrUpdate` (cập nhật nếu có dữ liệu cũ).

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn `Run Workflow` với dữ liệu mẫu (ví dụ: một đánh giá khách hàng).
   - Kiểm tra kết quả trên Google Sheets.
2. **Bật Active**:
   - Chuyển `Active` sang `ON` để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `slack` hoặc `telegramBot` để **báo cáo tự động** khi có đánh giá mới hoặc leads ưu tiên (ví dụ: `Sentiment: Negative`).
2. **Lưu log hoạt động**:
   - Thêm node `set` hoặc `code` để **ghi lịch sử** phân tích vào một sheet riêng.
3. **Báo cáo định kỳ**:
   - Sử dụng node `googleSheets` để **tạo báo cáo tổng hợp** hàng tuần/month với thống kê sentiment và điểm số trung bình.
4. **Cải thiện Prompt AI**:
   - Nếu kết quả AI không chính xác, điều chỉnh `system_prompt` trong node `AI Agent` để phù hợp với ngành nghề của doanh nghiệp.

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc phân tích đánh giá khách hàng thủ công, đồng thời **cung cấp dữ liệu leads chất lượng** sẵn sàng cho chiến dịch marketing hoặc cải tiến sản phẩm.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Bật Active** để tự động hóa phân tích 24/7.
3. **Tích hợp với Slack/Email** để nhận báo cáo tức thời.

👉 **Bắt đầu tự động hóa ngay** với [n8n.io](https://n8n.io/) và **tăng hiệu suất doanh nghiệp** của mình!

---