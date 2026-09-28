---
title: "🎨 Tự Động Hóa Tạo Câu Chuyện Emotion với Gemini AI: Sáng Tạo Hình Ảnh + JSON Prompt Veo3 (N8N)"
description: "Workflow tự động hóa 100% không code giúp các sếp tạo câu chuyện cảm xúc sâu sắc với hình ảnh AI và JSON Prompt Veo3 chỉ bằng Gemini AI. Giúp tiết kiệm thời gian lên đến 80% so với cách làm thủ công, đồng thời nâng cao chất lượng nội dung với tính cá nhân hóa cao."
slug: "tay-dong-hoa-tao-cau-chuyen-emotion-voi-gemini-ai"
tags: [n8n, automation, content-creation, multimodal-ai, google-gemini, google-drive, google-sheets]
keywords: [n8n workflow tự động hóa, tạo câu chuyện AI, Gemini AI, JSON Prompt Veo3, tự động hóa nội dung, tự động hóa hình ảnh AI]
---

# 🚀 **Tự Động Hóa Tạo Câu Chuyện Emotion với Gemini AI: Hình Ảnh + JSON Prompt Veo3**

Hiện nay, việc tạo nội dung cảm xúc sâu sắc như câu chuyện, hình ảnh và JSON Prompt Veo3 thường là một quá trình tốn thời gian và đòi hỏi sự sáng tạo cao. Các sếp phải dành hàng giờ để viết kịch bản, tìm kiếm hình ảnh phù hợp, và cấu trúc JSON Prompt để phù hợp với Veo3. **Workflow này giải quyết tất cả những vấn đề đó bằng cách tự động hóa toàn bộ quy trình chỉ với một cú nhấp chuột!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ viết câu chuyện đến tạo hình ảnh và JSON Prompt, giảm thời gian lên đến **80%** so với cách làm thủ công.
- **Nội dung cá nhân hóa cao**: Sử dụng Gemini AI để tạo câu chuyện và hình ảnh phù hợp với chủ đề, nhân vật và cảm xúc mong muốn.
- **Tích hợp Veo3**: Tạo JSON Prompt chuẩn cho Veo3, giúp tối ưu hóa quá trình tạo video từ hình ảnh.
- **Quản lý tập trung**: Tất cả câu chuyện, hình ảnh và JSON Prompt được lưu trữ trên Google Drive và Google Sheets, dễ dàng theo dõi và quản lý.
- **Hoạt động liên tục**: Workflow có thể chạy 24/7 trên VPS, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **Tài khoản Google Workspace** (Google Drive và Google Sheets).
- **API Key Google Gemini** (đăng ký tại [Google AI Studio](https://aistudio.google.com/)).
- **n8n Self-hosted** (để chạy workflow 24/7).
- **Các credential sau**:
  - `googleDriveOAuth2Api` (để tạo folder và upload file).
  - `googleSheetsOAuth2Api` (để cập nhật và theo dõi dữ liệu).
  - `googlePalmApi` (để kết nối với Gemini AI).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/) và chọn **Import Workflow**.
2. Chọn file JSON hoặc paste JSON từ [link gốc](https://n8n.io/workflows/8158).
3. Nhấp **Import** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **29 node** và cần cấu hình một số node quan trọng sau:

##### **A. Cấu hình Credentials**
- **Google Drive OAuth2**:
  - Đăng nhập vào tài khoản Google Workspace.
  - Tạo credential mới trong **n8n Credentials Manager** với loại `googleDriveOAuth2Api`.
- **Google Sheets OAuth2**:
  - Tạo credential mới với loại `googleSheetsOAuth2Api`.
- **Google Gemini API**:
  - Tạo credential mới với loại `googlePalmApi` và điền **API Key** từ Google AI Studio.

##### **B. Cấu hình Node Quan Trọng**
1. **`Create folder` (Google Drive)**:
   - Điền **Folder Name** (ví dụ: `AI_Story_Generation`).
   - Chọn **Parent Folder ID** (để tạo folder con trong folder cha).

2. **`Create sheet` (Google Sheets)**:
   - Điền **Sheet Name** (ví dụ: `AI_Story_Tracker`).
   - Chọn **Spreadsheet ID** (tạo mới hoặc chọn spreadsheet đã có).

3. **`Generate an image` (Google Gemini)**:
   - Điền **Prompt** trong node `Folder Name` (chainLlm) để định nghĩa câu chuyện và yêu cầu hình ảnh.
   - Ví dụ:
     ```
     "Create a surreal landscape with a mysterious castle, golden sunset, and a lone figure walking towards it. Aspect ratio: 16:9, Style: Cinematic, Quality: Ultra HD"
     ```

4. **`Story Creator` (chainLlm)**:
   - Điền **Prompt** để định nghĩa câu chuyện (ví dụ: "Tạo một câu chuyện về một người phiêu lưu trong rừng ma thuật").
   - Sử dụng **Structured Output Parser** để đảm bảo kết quả có định dạng JSON.

5. **`Prompt converter1` (chainLlm)**:
   - Chuyển câu chuyện và hình ảnh thành **JSON Prompt Veo3** (ví dụ: định nghĩa camera movement, lighting, fps, resolution).

6. **`Update row in sheet` và `Append row in sheet`**:
   - Đảm bảo **Sheet Name** và **Column Headers** phù hợp với dữ liệu bạn muốn lưu (ví dụ: `Story`, `Image_URL`, `Veo3_Prompt`).

##### **C. Test Run & Kích Hoạt**
1. Nhấp **Execute workflow** để chạy thử với dữ liệu mẫu.
2. Kiểm tra:
   - Câu chuyện có được tạo không?
   - Hình ảnh có được upload lên Google Drive không?
   - JSON Prompt Veo3 có được lưu trên Google Sheets không?
3. Nếu tất cả hoạt động bình thường, bật **Active workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết hợp với Slack/Telegram**: Gửi kết quả câu chuyện và hình ảnh lên Slack/Telegram để cập nhật nhóm.
- **Lưu log hoạt động**: Sử dụng node `stickyNote` để ghi lại lỗi hoặc tiến trình.
- **Tự động gửi báo cáo định kỳ**: Sử dụng node `googleSheets` để gửi báo cáo tổng hợp về câu chuyện và hình ảnh đã tạo.
- **Tối ưu hóa Prompt**: Thử nghiệm các Prompt khác nhau để cải thiện chất lượng câu chuyện và hình ảnh.
- **Dùng cho nhiều chủ đề**: Tạo nhiều folder và sheet riêng cho từng chủ đề (ví dụ: `Fantasy`, `Sci-Fi`, `Romance`).
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình tạo nội dung cảm xúc với Gemini AI. Bằng cách kết hợp **tạo câu chuyện, hình ảnh AI và JSON Prompt Veo3**, các sếp không chỉ tiết kiệm thời gian mà còn nâng cao chất lượng nội dung một cách đáng kể.

**Hãy áp dụng ngay workflow này và bắt đầu tạo câu chuyện AI của riêng mình!** 🚀

---
**Nếu gặp vấn đề hoặc cần hỗ trợ tùy chỉnh**, liên hệ với tác giả:
📧 **Email**: mfarooqiqbal143@gmail.com
📱 **Phone**: +923036991118
💼 **LinkedIn**: [Muhammad Farooq Iqbal](https://linkedin.com/in/muhammadfarooqiqbal)
🌐 **Portfolio**: [mfarooqone.github.io/n8n](https://mfarooqone.github.io/n8n/)