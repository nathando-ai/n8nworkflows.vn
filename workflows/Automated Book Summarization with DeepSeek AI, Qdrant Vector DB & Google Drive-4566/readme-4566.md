---
title: "📚 Tự Động Tóm Tắt Sách Tự Động Với DeepSeek AI, Trữ Lượng Vector Qdrant & Google Drive - Không Cần Code!"
description: "Workflow tự động hóa tóm tắt sách, báo cáo, tài liệu dài bằng AI DeepSeek, lưu trữ thông tin bằng Qdrant Vector DB và tự động đồng bộ lên Google Drive. Giúp các sếp tiết kiệm thời gian đọc hiểu tài liệu lên đến 90%!"
slug: "tieu-dong-tom-tat-sach-deepseek-qdrant-google-drive"
tags: [n8n, automation, ai, deepseek, qdrant, google-drive, no-code, langchain]
keywords: [tự động hóa tóm tắt sách, deepseek ai n8n, qdrant vector db, lưu trữ tài liệu tự động, google drive automation, workflow ai không code]
---

# 🚀 **Tự Động Tóm Tắt Sách & Tài Liệu Dài Bằng AI DeepSeek + Qdrant + Google Drive**

## **🔍 Nỗi Đau Của Các Sếp Khi Đọc Tài Liệu**
Các sếp thường phải mất **giờ đồng hồ** để đọc và tóm tắt sách, báo cáo, hoặc tài liệu dài như:
- **Sách chuyên ngành** (kinh tế, quản lý, công nghệ)
- **Báo cáo nghiên cứu** (market research, phân tích thị trường)
- **Tài liệu pháp lý** (hợp đồng, quy định mới)
- **Bài báo khoa học** (cần tóm tắt để trình bày cho đồng nghiệp)

Kết quả? **Thời gian quý giá bị "chôn vùi" trong việc đọc**, còn **tóm tắt chính xác** lại phụ thuộc vào khả năng hiểu biết cá nhân của mỗi người.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động tóm tắt** sách/tài liệu bằng **AI DeepSeek** (mô hình ngôn ngữ tiên tiến)
✅ **Lưu trữ thông tin** trong **Qdrant Vector DB** (trữ lượng vector cho tìm kiếm nhanh)
✅ **Đồng bộ tự động** kết quả lên **Google Drive** (dễ dàng chia sẻ và truy cập)
✅ **Hoạt động 24/7** (không cần can thiệp thủ công)

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian đọc lên đến 90%** (AI tự tóm tắt trong vài giây thay vì giờ đồng hồ)
- **Tóm tắt chính xác & cá nhân hóa** (DeepSeek hiểu ngữ cảnh và logic của tài liệu)
- **Tìm kiếm thông tin nhanh chóng** (Qdrant Vector DB cho phép tra cứu nội dung bằng từ khóa)
- **Lưu trữ an toàn & chia sẻ dễ dàng** (tất cả kết quả tự động đồng bộ lên Google Drive)
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Lên Đồ**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Google Drive** (để lưu trữ kết quả)
2. **API Key DeepSeek** (mô hình AI tóm tắt)
   - 👉 [Đăng ký API Key DeepSeek](https://deepseek.com/) (miễn phí cho thử nghiệm)
3. **Qdrant Vector DB** (trữ lượng vector cho tìm kiếm)
   - 👉 [Tạo collection Qdrant](https://qdrant.tech/) (có thể dùng phiên bản cloud miễn phí)
4. **Credentials cho n8n** (nếu self-hosted)
   - **Google Drive API Key** (tạo ở [Google Cloud Console](https://console.cloud.google.com/))
   - **DeepSeek API Key** (đăng ký trên trang chủ DeepSeek)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/4566](https://n8n.io/workflows/4566) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và dán vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **21 node**, nhưng các node **quan trọng nhất** cần cấu hình kỹ là:

##### **A. Cấu Hình DeepSeek AI (Tóm Tắt Tài Liệu)**
- **Node:** `DeepSeek Chat Model` (type: `lmChatDeepSeek`)
  - **Cấu hình:**
    - **API Key:** Điền API Key DeepSeek (đã đăng ký trước)
    - **Model:** Chọn `deepseek-chat` (hoặc phiên bản mới nhất)
    - **Prompt:** Sử dụng template mặc định (có thể tùy chỉnh để yêu cầu AI tóm tắt chi tiết hoặc ngắn gọn)
    - **Temperature:** Đặt **0.3-0.5** (để kết quả logic hơn)

##### **B. Cấu Hình Qdrant Vector DB (Lưu Trữ & Tìm Kiếm)**
- **Node:** `Qdrant Vector Store` (type: `vectorStoreQdrant`)
  - **Cấu hình:**
    - **URL:** Địa chỉ Qdrant (nếu self-hosted) hoặc URL cloud (nếu dùng phiên bản miễn phí)
    - **Collection Name:** Tên collection (ví dụ: `book_summaries`)
    - **API Key:** Nếu cần (check tài liệu Qdrant)
  - **Node:** `Embeddings Cohere` (type: `embeddingsCohere`)
    - **Cấu hình:**
      - **API Key:** Điền API Key Cohere (nếu dùng Cohere, nếu không, có thể thay bằng `text-embedding-ada-002` của OpenAI)
      - **Model:** `embed-multilingual-v3.0` (hoặc phiên bản mới nhất)

##### **C. Cấu Hình Google Drive (Lưu Kết Quả)**
- **Node:** `Google Drive` (type: `googleDrive`)
  - **Cấu hình:**
    - **Credentials:** Chọn tài khoản Google Drive đã cấu hình trong n8n
    - **Folder ID:** Chọn thư mục muốn lưu kết quả (có thể tạo mới)
    - **File Name:** Đặt tên tự động (ví dụ: `Tóm tắt_<Tên sách>.txt`)
  - **Node:** `Google Drive Trigger` (type: `googleDriveTrigger`)
    - **Cấu hình:**
      - **Event Type:** Chọn `file.create` (để kích hoạt khi file mới được tạo)

##### **D. Cấu Hình AI Agent (Logic Tóm Tắt)**
- **Node:** `AI Agent` (type: `agent`)
  - **Cấu hình:**
    - **Tools:** Chọn các node liên quan (`DeepSeek Chat Model`, `Qdrant Vector Store`, `Information Extractor`)
    - **Prompt:** Sử dụng template mặc định (có thể tùy chỉnh để yêu cầu AI:
      - Tóm tắt **mở rộng** (500 từ)
      - Tóm tắt **ngắn gọn** (100 từ)
      - Trích xuất **điểm chính** (bullet points))

##### **E. Cấu Hình Text Splitter (Chia Tài Liệu Thành Mảnh)**
- **Node:** `Recursive Character Text Splitter` (type: `textSplitterRecursiveCharacterTextSplitter`)
  - **Cấu hình:**
    - **Chunk Size:** 1000-1500 ký tự (để AI tóm tắt từng phần nhỏ)
    - **Chunk Overlap:** 200 ký tự (để tránh mất mát nội dung)

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với Dữ Liệu Mẫu**
   - Upload một tài liệu mẫu (PDF, DOCX, TXT) vào **Google Drive**.
   - Chạy workflow và kiểm tra kết quả:
     - AI có tóm tắt chính xác không?
     - Kết quả có được lưu vào Qdrant và Google Drive không?
2. **Bật Active Workflow**
   - Sau khi kiểm tra thành công, **bật chế độ Active** để workflow hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Cách Tối Ưu Hiệu Quả**]
1. **Tùy Chỉnh Prompt cho DeepSeek**
   - Nếu muốn tóm tắt **chuyên sâu**, thêm vào prompt:
     ```
     "Tóm tắt chi tiết với 3 điểm chính, bao gồm ví dụ thực tế và kết luận."
     ```
   - Nếu muốn **ngắn gọn**, sử dụng:
     ```
     "Tóm tắt trong 100 từ, chỉ giữ lại thông tin quan trọng nhất."
     ```

2. **Tích Hợp Slack/Telegram để Báo Lỗi**
   - Thêm node **Slack/Telegram Webhook** sau `DeepSeek Chat Model` để nhận thông báo khi AI gặp lỗi.

3. **Lưu Log Tóm Tắt vào Google Sheets**
   - Thêm node **Google Sheets** để ghi lại lịch sử tóm tắt (tên sách, ngày tóm tắt, độ dài).

4. **Tự Động Tóm Tắt Tài Liệu Mới Tạo trên Google Drive**
   - Sử dụng **Google Drive Trigger** để kích hoạt workflow khi có file mới được upload.

5. **Sử Dụng Qdrant để Tìm Kiếm Tài Liệu**
   - Sau khi lưu vào Qdrant, các sếp có thể **tra cứu nội dung** bằng từ khóa (ví dụ: "tìm tất cả sách về AI").

---

### 📌 **Kết Luận: Tự Động Hóa Tóm Tắt Tài Liệu Bằng AI - Không Cần Code!**
Workflow này giúp **giảm thiểu thời gian đọc tài liệu** từ **giờ đồng hồ xuống còn vài phút**, đồng thời **tự động hóa lưu trữ và chia sẻ kết quả** một cách an toàn.

**Các sếp hãy:**
✅ **Import workflow ngay** và thử với tài liệu đầu tiên!
✅ **Tùy chỉnh prompt** để phù hợp với nhu cầu đọc hiểu của mình.
✅ **Tích hợp thêm Slack/Telegram** để theo dõi quá trình tự động hóa.

**🚀 Hãy bắt đầu tự động hóa ngay hôm nay!** Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với tác giả [Adam Crafts](https://n8n.io/workflows/4566) để hỗ trợ.

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**#TựĐộngHóa #AI #DeepSeek #Qdrant #GoogleDrive #n8n**