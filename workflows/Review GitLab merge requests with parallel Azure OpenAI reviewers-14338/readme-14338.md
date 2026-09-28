---
title: "🤖 Tự Động Hóa Review Merge Request GitLab Với AI Azure OpenAI Song Song (N8n)"
description: "Workflow tự động hóa đánh giá song song các merge request trên GitLab bằng AI Azure OpenAI, tiết kiệm thời gian cho các sếp dev 100% không cần code. Kết quả: Review chính xác, nhanh chóng, và cá nhân hóa cho từng file thay đổi."
slug: "tieu-dong-hoa-review-gitlab-azure-openai-song-song"
tags: [n8n, automation, gitlab, ai-summarization, azure-openai, no-code, devops]
keywords: [n8n workflow gitlab, tự động hóa review code, ai đánh giá merge request, azure openai n8n, tự động hóa devops, review code song song]
---

# 🚀 **Tự Động Hóa Review Merge Request GitLab Với AI Azure OpenAI Song Song**

### **Giải pháp AI tự động hóa đánh giá code cho các sếp dev**
Hãy tưởng tượng một tình huống: Các sếp đang phải review hàng chục merge request mỗi ngày, phải đọc từng dòng code thay đổi, kiểm tra lỗi, rủi ro bảo mật và tính bảo trì. **Thời gian và công sức bị lãng phí!** Với workflow này, các sếp có thể **tự động hóa toàn bộ quy trình review** bằng AI Azure OpenAI, phân tích song song các file thay đổi, và **được báo cáo kết quả chi tiết** dưới dạng comment trực tiếp trên GitLab.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI tự động review hàng chục file thay đổi trong vài phút thay vì giờ.
- **Chính xác cao**: Phân tích song song 3 mặt: **lỗi (bug), bảo mật (security), và bảo trì (maintainability)**.
- **Cá nhân hóa**: Kết quả được format thành comment trực tiếp trên GitLab, dễ theo dõi.
- **Hoạt động liên tục**: Workflow chạy tự động khi có comment trigger, không cần can thiệp thủ công.
- **Tối ưu hóa quy trình**: Loại bỏ lỗi nhẹ, trùng lặp, và chỉ giữ lại những vấn đề thực sự cần xử lý.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản GitLab** với quyền API:
   - **Token Personal Access Token** (có quyền `api`).
   - **GitLab Base URL** (ví dụ: `https://gitlab.com`).
2. **Azure OpenAI API Key**:
   - **API Key** từ [Azure Portal](https://portal.azure.com/).
   - **Model**: `gpt-5.4-mini` (được cấu hình sẵn trong workflow).
3. **Workflow Configuration** (cần chỉnh sửa):
   - **Trigger comment**: Phiên bản mặc định là `+0` (các sếp có thể thay đổi).
   - **Messages**:
     - `Start message` (comment bắt đầu review).
     - `Summary message` (tóm tắt kết quả).
     - `No-issues message` (nếu không tìm thấy lỗi).
   - **Threshold confidence**: Giá trị từ 0-1 để lọc kết quả (ví dụ: 0.7 để loại bỏ lỗi nhẹ).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/14338](https://n8n.io/workflows/14338).
2. Mở **n8n Editor** và chọn **Import Workflow** → Chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và paste vào **Import Workflow** → **Paste JSON**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Credentials**
- **GitLab API**:
  - Tạo **Personal Access Token** trên GitLab (quyền `api`).
  - Đi đến **Credentials** trong n8n → Thêm **GitLab API** → Điền:
    - **Host**: `https://gitlab.com` (hoặc URL của GitLab self-hosted).
    - **Token**: Token Personal Access Token.
- **Azure OpenAI API**:
  - Đi đến **Credentials** → Thêm **Azure OpenAI API** → Điền:
    - **API Key**: API Key từ Azure.
    - **Organization ID** và **Resource Name** (tham khảo [Azure Docs](https://learn.microsoft.com/en-us/azure/ai-services/openai/quickstart)).

#### **B. Cấu hình Workflow Configuration**
- Mở node **"Workflow Configuration"** → Chỉnh sửa các tham số:
  - **GitLab Base URL**: `https://gitlab.com` (hoặc URL của GitLab self-hosted).
  - **Review Trigger Phrase**: `+0` (hoặc thay đổi thành comment trigger mới).
  - **Messages**:
    - `startMessage`, `summaryMessage`, `noIssuesMessage`.
  - **Minimum Confidence**: Giá trị từ 0-1 (ví dụ: `0.7`).

#### **C. Cấu hình AI Reviewers**
Workflow sử dụng **3 AI reviewer song song**:
1. **Bug Reviewer**: Phân tích lỗi trong code.
2. **Security Reviewer**: Kiểm tra rủi ro bảo mật.
3. **Maintainability Reviewer**: Đánh giá tính bảo trì.
- Các **prompt** và **model** đã được cấu hình sẵn (`gpt-5.4-mini`), các sếp có thể chỉnh sửa trong node tương ứng (ví dụ: `Bug Reviewer Model`).

#### **D. Kiểm tra và Test**
- **Test Run**: Chọn **Run Workflow** với một merge request mẫu.
- **Kiểm tra kết quả**:
  - AI sẽ trả về **comment tự động** trên GitLab.
  - Kiểm tra các **inline comment** và **summary reply**.

### **3. Kích hoạt ⚡️**
- Sau khi cấu hình xong, **bật Active** workflow.
- **Trigger review** bằng cách comment `+0` trên merge request.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** để báo cáo kết quả review ngay khi hoàn thành.
2. **Lưu log review**:
   - Sử dụng node **HTTP Request** để gửi kết quả review vào **Google Sheets** hoặc **Notion** để theo dõi lịch sử.
3. **Tùy chỉnh prompt**:
   - Các sếp có thể chỉnh sửa **prompt** của AI trong node `lmChatAzureOpenAi` để phù hợp với yêu cầu cụ thể của dự án.
4. **Bật/dừng review tự động**:
   - Sử dụng node **Set** để điều khiển workflow (ví dụ: chỉ review trên branch `main` hoặc `develop`).

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp dev khỏi công việc review thủ công, đồng thời **tăng cường chất lượng code** bằng AI. **Chỉ cần comment `+0` trên merge request**, AI sẽ tự động phân tích và trả về kết quả chi tiết dưới dạng comment trên GitLab.

**Hãy áp dụng ngay và làm việc hiệu quả hơn!** 🚀
Nếu có vấn đề, các sếp có thể tham khảo [hướng dẫn chính thức](https://n8n.io/workflows/14338) hoặc liên hệ cộng đồng n8n trên [Discord](https://n8n.io/community).