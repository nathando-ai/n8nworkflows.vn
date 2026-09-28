---
title: "🎓 **Tự Động Học Viện Đánh Giá Đăng Ký Khóa Học Với AI, Gmail & Google Sheets - Không Cần Code!**"
description: "Workflow tự động hóa đánh giá hồ sơ đăng ký khóa học của sinh viên thông qua AI, gửi email tự động và cập nhật dữ liệu vào Google Sheets. Giúp các sếp tiết kiệm thời gian đánh giá thủ công và cải thiện trải nghiệm cho sinh viên."
slug: "tieu-dong-hoa-danh-gia-dang-ky-khoa-hoc-voi-ai-gmail-google-sheets"
tags: [n8n, automation, no-code, ai-summarization, google-sheets, gmail, pinecone, openai, google-gemini]
keywords: [tự động hóa đăng ký khóa học, đánh giá hồ sơ sinh viên bằng AI, n8n workflow, google sheets tự động, gmail tự động hóa, pinecone vector store, openai gpt-4o-mini]
---

# 🚀 **Tự Động Học Viện Đánh Giá Hồ Sơ Đăng Ký Khóa Học Với AI, Gmail & Google Sheets**

## **📌 Nỗi Đau Của Các Sếp: Đánh Giá Hồ Sơ Thủ Công Làm Mất Thời Gian & Tiềm Năng**
Hàng ngày, các sếp phải dành nhiều giờ để:
- **Xem xét hàng trăm hồ sơ đăng ký** từ sinh viên.
- **Đánh giá chất lượng hồ sơ** dựa trên các tiêu chí khác nhau (CV, bài viết tự giới thiệu, file đính kèm).
- **Gửi phản hồi cá nhân hóa** qua email cho từng sinh viên.
- **Cập nhật dữ liệu** vào Google Sheets để theo dõi tiến trình.

**Kết quả?** Thời gian bị "chôn vùi" trong công việc thủ công, sinh viên phải chờ lâu mới biết kết quả, và khả năng đánh giá khách quan bị giảm.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình!** Sử dụng **AI (OpenAI + Google Gemini)**, **Gmail tự động** và **Google Sheets**, workflow sẽ:
✅ **Đọc & phân tích hồ sơ** (CV, file đính kèm) bằng AI.
✅ **Đánh giá tự động** dựa trên tiêu chí đã định nghĩa.
✅ **Gửi email phản hồi cá nhân hóa** cho sinh viên.
✅ **Cập nhật dữ liệu vào Google Sheets** để quản lý dễ dàng.

---

## **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/ngày** trong việc đánh giá hồ sơ thủ công.
- **Đánh giá khách quan & nhanh chóng** nhờ AI phân tích văn bản.
- **Phản hồi cá nhân hóa** cho sinh viên, tăng trải nghiệm.
- **Dữ liệu tự động cập nhật** vào Google Sheets, dễ theo dõi & báo cáo.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

## **🔧 Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**               | **Thông Tin Cần Thiết**                                                                 | **Lưu Ý** |
|---------------------------|----------------------------------------------------------------------------------------|------------|
| **Google Drive**          | OAuth 2.0 API Key (để tải file đính kèm từ sinh viên)                                 | Cài đặt [Google Drive API](https://developers.google.com/drive/api/v3/quickstart/python) |
| **Google Sheets**         | OAuth 2.0 API Key (để cập nhật dữ liệu)                                                | Chọn **Google Sheets OAuth 2.0 API** trong n8n |
| **Gmail**                 | OAuth 2.0 API Key (để gửi email phản hồi)                                              | Cài đặt [Gmail API](https://developers.google.com/gmail/api/quickstart/python) |
| **OpenAI (GPT-4o-mini)** | API Key (để sử dụng mô hình AI)                                                       | Mua tại [OpenAI Platform](https://platform.openai.com/) |
| **Google Gemini**         | API Key (để tạo embedding cho file)                                                   | Cài đặt [Google Vertex AI](https://cloud.google.com/vertex-ai) |
| **Pinecone**              | API Key (để lưu trữ vector store)                                                     | Đăng ký tại [Pinecone](https://www.pinecone.io/) |

### **2. File & Google Sheets**
- **Google Form** (để sinh viên đăng ký khóa học).
- **Google Sheet** (để lưu trữ kết quả đánh giá, cấu trúc như sau):
  ```
  | Email (Sinh Viên) | Tên | Điểm AI | Phản Hồi | Trạng Thái |
  |-------------------|-----|---------|----------|-------------|
  ```

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/8567](https://n8n.io/workflows/8567) (chọn **Export JSON**).
2. **Mở n8n Editor** (trên n8n Cloud hoặc Self-hosted).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
2. Copy toàn bộ mã JSON từ [n8n.io/workflows/8567](https://n8n.io/workflows/8567) → Dán vào và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node "On form submission" (Trigger)**
- **Cấu hình Google Form**:
  - Đảm bảo **Google Form** được kết nối với **Google Sheets** (để lưu dữ liệu đầu vào).
  - **Webhook URL** của n8n phải được thêm vào **Thiết lập → Cài đặt thêm → Webhook** của Google Form.

#### **🔹 Node "AI Agent" & "OpenAI Chat Model"**
- **Mô hình AI**: Sử dụng **gpt-4o-mini** (mặc định).
- **Prompt cần tùy chỉnh**:
  - Thêm **tiêu chí đánh giá** cụ thể (ví dụ: "Điểm 10 cho CV có kinh nghiệm liên quan, điểm 5 cho bài viết tự giới thiệu rõ ràng").
  - Ví dụ prompt mẫu:
    ```plaintext
    Bạn là một chuyên gia đánh giá hồ sơ khóa học. Đọc CV và file đính kèm của sinh viên, sau đó đánh giá dựa trên các tiêu chí sau:
    1. Kinh nghiệm liên quan (30%)
    2. Bài viết tự giới thiệu (40%)
    3. File đính kèm (30%)
    Trả về kết quả dưới dạng JSON:
    {
      "score": int,
      "feedback": str,
      "recommendation": str
    }
    ```

#### **🔹 Node "Embeddings Google Gemini" & "Pinecone Vector Store"**
- **Đảm bảo Pinecone có index** đã tạo trước khi chạy workflow.
- **Cấu hình Pinecone**:
  - **Environment**: Chọn môi trường đã tạo (ví dụ: `asia-southeast1-gcp`).
  - **Index Name**: Tên index lưu trữ embedding (ví dụ: `course-embeddings`).

#### **🔹 Node "Send a message in Gmail"**
- **Chọn tài khoản Gmail** (n8n sẽ gửi email phản hồi cho sinh viên).
- **Cấu trúc email**:
  ```plaintext
  Chào [Tên Sinh Viên],

  Cảm ơn bạn đã đăng ký khóa học! Sau khi đánh giá, chúng tôi có kết quả như sau:
  - Điểm: [Score]
  - Phản hồi: [Feedback]

  Trạng thái: [Đã chấp nhận/Từ chối/Hãy liên hệ]

  Xin chân thành cảm ơn!
  ```
- **Thêm file đính kèm** (nếu có): Sử dụng node **Google Drive → Download file** để lấy file phản hồi từ AI.

#### **🔹 Node "Append row in sheet"**
- **Chọn Google Sheet** cần cập nhật.
- **Cấu trúc dữ liệu**:
  ```plaintext
  {
    "Email": "{{$node["Combine User Data"].json["email"]}}",
    "Tên": "{{$node["Combine User Data"].json["name"]}}",
    "Điểm AI": "{{$json["score"]}}",
    "Phản hồi": "{{$json["feedback"]}}",
    "Trạng Thái": "{{$json["recommendation"]}}"
  }
  ```

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Điền thông tin vào **Google Form** (ví dụ: email, tên, file CV).
   - Chạy **Test Run** trong n8n để kiểm tra workflow.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tăng Cường Tính Cá Nhân Hóa Phản Hồi**
- **Sử dụng AI để tạo phản hồi chi tiết**:
  - Thêm node **OpenAI Chat Model** với prompt:
    ```plaintext
    Bạn là một mentor khóa học. Viết một email phản hồi chi tiết cho sinh viên dựa trên điểm số và feedback từ AI, bao gồm:
    - Điểm mạnh
    - Điểm cần cải thiện
    - Lời khuyến nghị cụ thể
    ```
- **Kết hợp với Slack/Telegram**:
  - Thêm node **Slack/Telegram Bot** để thông báo kết quả cho quản lý.

### **2. Lưu Log & Theo Dõi Kết Quả**
- **Sử dụng Sticky Note** (node `stickyNote`) để lưu log:
  ```plaintext
  {
    "timestamp": "{{$node["Current Date/Time"].json}}",
    "email": "{{$node["Combine User Data"].json["email"]}}",
    "status": "success"
  }
  ```
- **Tạo báo cáo định kỳ**:
  - Sử dụng **Google Sheets → Query** để tổng hợp dữ liệu và tạo báo cáo.

### **3. Cải Thiện Trải Nghiệm Sinh Viên**
- **Gửi email tự động xác nhận nhận hồ sơ**:
  - Thêm node **Gmail** trước khi xử lý để gửi email:
    ```plaintext
    Chào [Tên],

    Cảm ơn bạn đã gửi hồ sơ đăng ký khóa học! Chúng tôi sẽ đánh giá và phản hồi trong vòng 24 giờ.
    ```
- **Thêm tính năng chatbot**:
  - Sử dụng **Google Gemini** để trả lời câu hỏi thường gặp của sinh viên qua email.

---

## **📌 Kết Luận: Tự Động Hóa Đánh Giá Hồ Sơ Để Tiết Kiệm Thời Gian & Tăng Trải Nghiệm**

Workflow này **giải phóng các sếp khỏi công việc thủ công mệt mỏi**, đồng thời **cải thiện chất lượng đánh giá** nhờ AI. Với **Gmail tự động**, **Google Sheets cập nhật liên tục** và **phản hồi cá nhân hóa**, sinh viên sẽ có trải nghiệm tốt hơn, trong khi các sếp có thể **tập trung vào công việc chiến lược**.

**👉 Hãy import workflow ngay hôm nay và bắt đầu tự động hóa quy trình đánh giá!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Bạn có câu hỏi về cách tùy chỉnh workflow? Hãy để lại comment bên dưới!** 🚀