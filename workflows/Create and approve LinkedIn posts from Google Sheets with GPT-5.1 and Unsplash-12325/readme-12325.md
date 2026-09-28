---
title: "🚀 Tự Động Hóa Tạo & Phê Duyệt Bài Đăng LinkedIn Từ Google Sheets Với GPT-5.1 & Hình Ảnh Unsplash"
description: "Workflow tự động hóa hoàn toàn tạo nội dung LinkedIn chuyên nghiệp, chọn hình ảnh phù hợp từ Unsplash, gửi cho phê duyệt qua email và đăng trực tiếp lên LinkedIn - tiết kiệm thời gian lên đến 80% cho các sếp marketing."
slug: "tieu-dong-hoa-tao-phieu-duyet-bai-dang-linkedin"
tags: [n8n, automation, content-creation, ai-gpt, linkedin-automation, google-sheets, unsplash]
keywords: [tự động hóa linkedin, tạo bài đăng linkedin bằng ai, workflow n8n content marketing, tự động hóa nội dung social media, gpt-5.1 cho linkedin]
---

# 🚀 **Tự Động Hóa Tạo & Phê Duyệt Bài Đăng LinkedIn Từ Google Sheets Với AI GPT-5.1**

Bạn đã bao giờ cảm thấy mệt mỏi vì phải viết bài đăng LinkedIn từ đầu, chọn hình ảnh phù hợp, gửi cho đồng nghiệp phê duyệt và cuối cùng mới đăng tải? **Workflow này giải quyết tất cả những vấn đề đó chỉ với một nhấp chuột!** Dùng AI GPT-5.1 tạo nội dung chuyên nghiệp, tự động tìm kiếm và chọn hình ảnh từ Unsplash, gửi cho phê duyệt qua email và đăng trực tiếp lên LinkedIn - **tiết kiệm thời gian lên đến 80% cho các sếp marketing và content creator**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ viết bài đến đăng tải, chỉ cần phê duyệt.
- **Nội dung chuyên nghiệp**: AI GPT-5.1 tạo bài đăng phù hợp với giọng điệu và đối tượng mục tiêu.
- **Hình ảnh chất lượng cao**: Tự động tìm kiếm và chọn hình ảnh phù hợp từ Unsplash.
- **Phê duyệt an toàn**: Tất cả bài đăng đều phải được xác nhận qua email trước khi đăng tải.
- **Hoạt động liên tục**: Scheduling tự động hàng ngày tại thời điểm bạn chỉ định.
- **Giảm thiểu lỗi**: Kiểm tra tự động về độ dài bài đăng, số lượng hashtag và chất lượng hình ảnh.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Google Sheets** với cấu trúc cột như sau:
   - **Topic/Subject** (Chủ đề bài đăng)
   - **Content Type** (Loại nội dung: Blog, Video, Event, etc.)
   - **Tone** (Giọng điệu: Formal, Friendly, Professional, etc.)
   - **Target Audience** (Đối tượng mục tiêu)
   - **Additional Notes** (Ghi chú bổ sung)
   - **Image link** (Link hình ảnh tùy chọn)
   - **Include Image?** (Có/Không bao gồm hình ảnh)
   - **Status** (Trạng thái: Ready, In Progress, Rejected, Posted)

2. **API Keys và Credentials**:
   - **OpenAI API Key** (để sử dụng GPT-5.1 và GPT-4.1-mini)
   - **Unsplash Access Key** (để tìm kiếm hình ảnh)
   - **Google Sheets OAuth2** (để đọc và cập nhật trạng thái)
   - **Gmail OAuth2** (để gửi email phê duyệt)
   - **LinkedIn OAuth2** (để đăng bài)

3. **Tài khoản LinkedIn và Email**:
   - Tài khoản LinkedIn để đăng bài.
   - Email chính để nhận thông báo phê duyệt.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### 1. **Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [n8n.io/workflows/12325](https://n8n.io/workflows/12325).
- **Bước 2**: Mở n8n Editor và nhấn **Import Workflow** → Chọn file JSON vừa tải.
- **Bước 3**: Chọn **Import** để hoàn tất.

### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Google Sheets**
- **Node "Get Post Idea"**:
  - Chọn **Google Sheets OAuth2Api** đã cấu hình.
  - Chọn **Sheet** và **Tab** phù hợp.
  - Đặt **Query** để lấy dữ liệu từ cột `Status = "Ready"`:
    ```json
    {
      "query": "SELECT * WHERE Status = 'Ready' LIMIT 1"
    }
    ```

- **Node "Update Post Status"**:
  - Chọn **Google Sheets OAuth2Api** tương tự.
  - Đặt **Operation** là `update` và **Range** là `SheetName!A:Z` (hoặc cột cụ thể).

#### **B. Cấu hình OpenAI**
- **Node "OpenAI Chat Model" (GPT-5.1)**:
  - Chọn **Credentials** là `openAiApi`.
  - Đặt **Model** là `gpt-5.1` (hoặc `gpt-4.1-mini` nếu chưa có API GPT-5.1).
  - Cấu hình **Prompt** trong node **AI Content Generation** (node `agent`):
    ```json
    {
      "role": "user",
      "content": "Tạo một bài đăng LinkedIn chuyên nghiệp về chủ đề {{Topic}}, với giọng điệu {{Tone}}, đối tượng mục tiêu là {{Target Audience}}. Bài đăng phải có độ dài khoảng 300-500 từ, bao gồm ít nhất 3 hashtag liên quan và kết thúc bằng một câu gọi hành động (CTA)."
    }
    ```

#### **C. Cấu hình Unsplash**
- **Node "Get Image in Unsplash"**:
  - Chọn **Credentials** là `unsplashAccessKey`.
  - Đặt **URL** trong node **Download Image**:
    ```json
    {
      "url": "https://api.unsplash.com/photos/random?query={{keywords}}&client_id={{unsplashAccessKey}}"
    }
    ```
  - Node **Convert Share Link to Download Link** (node `code`):
    ```javascript
    // Chuyển link share Unsplash thành link download trực tiếp
    const shareUrl = $input.all().imageUrl;
    const downloadUrl = shareUrl.replace('unsplash.com', 'images.unsplash.com');
    return { imageUrl: downloadUrl };
    ```

#### **D. Cấu hình Email Phê Duyệt**
- **Node "Send Post Preview"**:
  - Chọn **Credentials** là `gmailOAuth2`.
  - Đặt **To** là email của người phê duyệt.
  - **Subject**: `Phê duyệt bài đăng LinkedIn: {{Topic}}`
  - **HTML Content**: Sử dụng node **Format Content to HTML** để định dạng bài đăng thành email.

- **Node "Send email for confirmation"**:
  - Chọn **Credentials** là `gmailOAuth2`.
  - Đặt **Operation** là `sendAndWait`.
  - **Subject**: `Xác nhận đăng bài: {{Topic}}`
  - **HTML Content**: Gửi link preview và yêu cầu xác nhận.

#### **E. Cấu hình LinkedIn**
- **Node "Create a post"**:
  - Chọn **Credentials** là `linkedInOAuth2`.
  - **Content**: Sử dụng kết quả từ node **Post Formatter**.
  - **Image URL**: Sử dụng kết quả từ node **Download Image** (nếu có).

#### **F. Cấu hình Scheduling**
- **Node "Schedule Trigger"**:
  - Đặt **Schedule** là `0 0 * * *` (hàng ngày lúc 00:00).
  - Hoặc tùy chỉnh theo nhu cầu (ví dụ: `0 9 * * 1-5` để chạy hàng ngày lúc 9h từ thứ 2 đến thứ 6).

#### **G. Cấu hình Kiểm tra & Phê Duyệt**
- **Node "Validate Post Quality"**:
  - Kiểm tra độ dài bài đăng (ít nhất 300 từ) và số lượng hashtag (ít nhất 3).
  - Nếu không đáp ứng, workflow sẽ **loop lại** và yêu cầu AI tái tạo.

- **Node "Check Email Approval"**:
  - Kiểm tra email phản hồi từ người phê duyệt.
  - Nếu **không có phản hồi**, workflow sẽ **dừng lại** và cập nhật trạng thái `In Progress`.
  - Nếu **phê duyệt**, workflow tiếp tục đăng bài.
  - Nếu **từ chối**, cập nhật trạng thái `Rejected`.

---

### 3. **Kích hoạt ⚡️**
- **Bước 1**: Nhấn **Test Run** để chạy workflow với dữ liệu mẫu.
- **Bước 2**: Kiểm tra email phê duyệt và xác nhận.
- **Bước 3**: Nếu phê duyệt, kiểm tra bài đăng trên LinkedIn.
- **Bước 4**: Nhấn **Active** để chạy workflow tự động hàng ngày.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh giọng điệu và đối tượng mục tiêu**:
   - Thêm cột **Tone** và **Target Audience** trong Google Sheets để AI tạo nội dung phù hợp.
   - Ví dụ: `Tone: Friendly` và `Target Audience: Startup Founders` sẽ tạo bài đăng thân thiện và tập trung vào người sáng lập startup.

2. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** để ghi lại trạng thái của mỗi bài đăng (ví dụ: `Bài đăng "Tối ưu hóa SEO" đã được đăng tải thành công`).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Gmail** hoặc **Slack** để gửi báo cáo tổng hợp các bài đăng đã đăng tải trong tuần.

4. **Kết hợp với Slack**:
   - Thêm node **Slack** để thông báo khi bài đăng được phê duyệt hoặc đăng tải thành công.

5. **Tối ưu API OpenAI**:
   - Sử dụng **Rate Limiter** (node `limit`) để tránh bị giới hạn API khi chạy nhiều bài đăng cùng lúc.

6. **Tự động cập nhật hình ảnh**:
   - Nếu hình ảnh từ Unsplash không phù hợp, AI sẽ tự động tìm kiếm và chọn lại.

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp marketing và content creator để tập trung vào chiến lược nội dung thay vì làm thủ công. **Tự động hóa toàn bộ quy trình từ viết bài đến đăng tải**, với AI tạo nội dung chuyên nghiệp và hình ảnh phù hợp, **phê duyệt an toàn qua email**, và **đăng tải tự động lên LinkedIn**.

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa nội dung LinkedIn của bạn!** 🚀
Nếu có bất kỳ câu hỏi hoặc gặp khó khăn trong quá trình cấu hình, hãy để lại bình luận bên dưới. Chúng tôi sẽ hỗ trợ bạn một cách chi tiết nhất!