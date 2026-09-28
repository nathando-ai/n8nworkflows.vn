---
title: "🤖 **Tự Động Học Bài & Đánh Giá Dự Thảo Nội Dung với OpenRouter & LangChain (n8n)**"
description: "Workflow tự động hóa đánh giá và cải tiến nội dung bằng trí tuệ nhân tạo, giúp các sếp tiết kiệm thời gian review, nâng cao chất lượng bài viết và tối ưu quy trình content creation. Kết quả: Dự thảo được đánh giá chính xác, nhận feedback chi tiết và được cải tiến tự động."
slug: "tieu-dong-hoa-danh-gia-du-thao-noidung-voi-openrouter-langchain"
tags: [n8n, automation, content-creation, ai-summarization, langchain, openrouter, no-code]
keywords: [n8n workflow đánh giá nội dung, tự động hóa review bài viết, AI đánh giá chất lượng bài viết, LangChain OpenRouter n8n, tự động hóa content creation]
---

# 🚀 **Tự Động Học Bài & Đánh Giá Dự Thảo Nội Dung với OpenRouter & LangChain**

## **Nỗi Đau Của Các Sếp Trong Quy Trình Content Creation**
Các sếp thường phải mất **giờ đồng hồ** để review và chỉnh sửa hàng chục bài viết mỗi ngày. Các vấn đề thường gặp bao gồm:
- **Chất lượng không đồng nhất**: Một số bài viết được viết tốt, nhưng nhiều bài lại thiếu logic, sai thông tin hoặc không phù hợp với giọng điệu mục tiêu.
- **Thời gian review lâu**: Các sếp phải đọc từng đoạn, đánh giá từng khía cạnh (độ chính xác, tính logic, tính hấp dẫn), và viết feedback chi tiết.
- **Khó theo dõi tiến độ**: Không có hệ thống đánh giá khách quan để so sánh giữa các phiên bản bài viết.
- **Rủi ro sai sót**: Thiếu một công cụ tự động hóa để phát hiện lỗi logic, sai thông tin hoặc nội dung trùng lặp.

**Workflow này giải quyết tất cả những vấn đề trên bằng trí tuệ nhân tạo (AI) và tự động hóa 100% không cần code!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian review**: AI tự động đánh giá dự thảo trong **vài giây**, thay vì mất nhiều giờ của các sếp.
- **Đánh giá khách quan và chi tiết**: AI phân tích **độ chính xác, logic, tính hấp dẫn, và tính hoàn chỉnh** của bài viết, không bị chủ quan như con người.
- **Feedback cụ thể và cải tiến tự động**: Nhận **báo cáo đánh giá chi tiết** (score, điểm mạnh, điểm yếu, và gợi ý sửa đổi) để cải tiến nội dung.
- **Tối ưu quy trình content**: Kết hợp với **Content Pipeline** để tự động điều chỉnh bài viết theo feedback AI, giảm số lần chỉnh sửa thủ công.
- **Chất lượng nội dung đồng nhất**: AI đảm bảo tất cả bài viết tuân theo **một tiêu chuẩn đánh giá nhất quán**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản OpenRouter API**:
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - Thêm **credentials** trong n8n với tên `openRouterApi` (để sử dụng trong node `lmChatOpenRouter`).
   - *Lưu ý*: OpenRouter hỗ trợ nhiều mô hình LLM như `mistral`, `llama2`, `gpt-4`. Các sếp có thể chọn mô hình phù hợp với ngân sách.

2. **Workflow cha (Content Pipeline)**:
   - Workflow này là **subworkflow** (workflow con) được gọi từ một **workflow cha** (ví dụ: workflow quản lý content creation).
   - Workflow cha phải truyền dữ liệu đầu vào gồm:
     - `brief`: Tóm tắt yêu cầu của bài viết.
     - `currentDraft`: Nội dung dự thảo hiện tại.
     - `revisionCount`: Số lần đã chỉnh sửa (để theo dõi tiến độ).

3. **N8n Self-hosted (khuyến nghị)**:
   - Để workflow hoạt động **24/7** và không bị giới hạn bởi phiên bản miễn phí, các sếp nên **self-host n8n** trên VPS.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/15951](https://n8n.io/workflows/15951).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và paste vào **Import Workflow** trong menu.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials cho OpenRouter**
- Trong node **`OpenRouter - Reviewer`** (type: `lmChatOpenRouter`), các sếp phải:
  1. Chọn **credentials** là `openRouterApi` (đã thêm trước đó).
  2. Chọn **model** (ví dụ: `mistral-tiny`, `llama2-70b`, `gpt-4`).
  3. Cấu hình **prompt** để AI đánh giá bài viết:
     ```json
     "prompt": "You are a professional content reviewer. Evaluate the following draft based on the brief provided. Score the draft on a scale of 1-10 for:
     - Accuracy (Does it match the brief and facts?)
     - Logic (Is the flow coherent and well-structured?)
     - Tone (Is it engaging and appropriate for the target audience?)
     - Completeness (Does it cover all key points?)
     Return a weighted overall score (1-10) and detailed revision notes."
     ```
  4. Thêm **parameters** như:
     - `temperature`: 0.7 (để AI không quá ngẫu nhiên).
     - `max_tokens`: 1000 (đủ để AI trả lời chi tiết).

#### **B. Cấu Hình Node `Reviewer Agent`**
- Node này sử dụng **LangChain Agent** để tự động hóa quy trình đánh giá.
- Các sếp **không cần chỉnh sửa** nếu muốn sử dụng mặc định, nhưng có thể tùy chỉnh:
  - **Scoring dimensions**: Thêm/bỏ các tiêu chí đánh giá (ví dụ: thêm "Originality" hoặc "SEO Optimization").
  - **Weighted score formula**: Điều chỉnh công thức tính điểm tổng (ví dụ: `Accuracy * 0.4 + Logic * 0.3 + Tone * 0.2 + Completeness * 0.1`).

#### **C. Node `Parse Review Output` (Code)**
- Node này **trích xuất** kết quả từ AI và định dạng lại để workflow cha có thể sử dụng.
- Mẫu code mặc định:
  ```javascript
  // Trích xuất score và feedback từ output của AI
  const output = {
    ...$input.all(),
    review: {
      accuracy: parseFloat($input.all().output.text.match(/Accuracy: (\d+\.\d+)/)[1]),
      logic: parseFloat($input.all().output.text.match(/Logic: (\d+\.\d+)/)[1]),
      tone: parseFloat($input.all().output.text.match(/Tone: (\d+\.\d+)/)[1]),
      completeness: parseFloat($input.all().output.text.match(/Completeness: (\d+\.\d+)/)[1]),
      overallScore: parseFloat($input.all().output.text.match(/Overall Score: (\d+\.\d+)/)[1]),
      revisionNotes: $input.all().output.text.match(/Revision Notes:(.*)/)[1].trim()
    }
  };
  return output;
  ```
- **Lưu ý**:
  - Nếu AI trả về định dạng khác, các sếp phải **cập nhật regex** trong code.
  - Kết quả cuối cùng sẽ là một object chứa:
    ```json
    {
      "brief": "...",
      "currentDraft": "...",
      "review": {
        "accuracy": 8.5,
        "logic": 9.0,
        "tone": 7.8,
        "completeness": 8.2,
        "overallScore": 8.5,
        "revisionNotes": "Suggest adding more examples in the conclusion..."
      }
    }
    ```

#### **D. Kết Nối với Workflow Cha**
- Workflow này là **subworkflow**, nên phải được **gọi từ workflow cha** (Content Pipeline).
- Trong workflow cha, các sếp thêm node **`Execute Subworkflow`** và chọn workflow này.
- **Input** phải truyền:
  ```json
  {
    "brief": "Viết bài về SEO cho doanh nghiệp năm 2024",
    "currentDraft": "Nội dung dự thảo hiện tại...",
    "revisionCount": 1
  }
  ```
- **Output** sẽ trả về:
  ```json
  {
    "brief": "...",
    "currentDraft": "...",
    "review": { ... } // Đã được AI đánh giá
  }
  ```

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một **dự thảo bài viết** vào workflow cha.
   - Kiểm tra kết quả trong node **`Parse Review Output`** để đảm bảo AI trả về score và feedback chính xác.
2. **Bật Active**:
   - Sau khi test thành công, các sếp có thể **bật workflow** để hoạt động tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối với Slack/Telegram để Báo Cáo Kết Quả**
- Thêm node **`Slack`** hoặc **`Telegram`** sau node **`Parse Review Output`** để tự động gửi báo cáo đánh giá:
  ```json
  {
    "text": `📝 **Review Report** 📝
    - Overall Score: ${$input.all().review.overallScore}/10
    - Revision Notes: ${$input.all().review.revisionNotes}
    - Draft: ${$input.all().currentDraft.substring(0, 200)}...`
  }
  ```

### **2. Lưu Log Đánh Giá vào Google Sheets/Notion**
- Sử dụng node **`Google Sheets`** hoặc **`Notion`** để lưu lịch sử đánh giá:
  ```json
  {
    "sheetName": "Content Reviews",
    "row": {
      "Date": new Date().toISOString(),
      "Title": $input.all().brief,
      "Draft": $input.all().currentDraft,
      "Overall Score": $input.all().review.overallScore,
      "Feedback": $input.all().review.revisionNotes
    }
  }
  ```

### **3. Tự Động Chỉnh Sửa Bài Viết Theo Feedback**
- Kết hợp với **LangChain Agent** để tự động sửa bài viết:
  1. Sau khi nhận feedback từ AI, workflow cha gọi **workflow con sửa đổi**.
  2. Sử dụng node **`lmChatOpenRouter`** với prompt:
     ```json
     "prompt": "Rewrite the following draft based on the revision notes:
     Draft: ${$input.all().currentDraft}
     Notes: ${$input.all().review.revisionNotes}
     Keep the same tone and style."
     ```

### **4. Tự Động Gửi Báo Cáo Định Kỳ cho Team**
- Sử dụng **n8n Scheduler** để chạy workflow hàng ngày và gửi báo cáo tổng hợp:
  ```json
  {
    "schedule": {
      "cron": "0 0 * * *", // Mỗi ngày lúc 00:00
      "timeZone": "Asia/HoChiMinh"
    }
  }
  ```

---

## 📌 **Kết Luận**
Workflow này là **công cụ mạnh mẽ** giúp các sếp:
✅ **Tự động hóa review nội dung** bằng trí tuệ nhân tạo.
✅ **Nâng cao chất lượng bài viết** với đánh giá khách quan.
✅ **Tiết kiệm thời gian** và tập trung vào công việc chiến lược.
✅ **Tối ưu quy trình content creation** với feedback chi tiết.

**Hành động ngay!**
1. **Self-host n8n** trên VPS để workflow hoạt động 24/7.
2. **Import workflow** và cấu hình OpenRouter API.
3. **Test với dự thảo bài viết** và xem kết quả AI đánh giá như thế nào!
4. **Kết hợp với workflow cha** để tự động hóa toàn bộ quy trình content.

**🚀 Cùng tự động hóa content creation của mình ngay hôm nay!** 🚀