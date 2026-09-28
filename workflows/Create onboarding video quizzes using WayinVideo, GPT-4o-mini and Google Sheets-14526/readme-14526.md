---
title: "🎬 Tự Động Hoá Tạo Trắc Nghiệm Video Onboarding Với WayinVideo, GPT-4o-mini & Google Sheets"
description: "Giải pháp tự động hóa hoàn toàn không code để chuyển đổi video onboarding thành trắc nghiệm MCQ thông minh, tiết kiệm thời gian và nâng cao hiệu quả đào tạo. Kết quả: Thư viện trắc nghiệm tự động cập nhật trên Google Sheets, sẵn sàng sử dụng cho các khóa học mới."
slug: "tay-dong-hoa-tao-trac-nghiem-video-onboarding"
tags: [n8n, automation, ai-summarization, document-extraction, google-sheets, openai, wayinvide]
keywords: [n8n workflow tự động hóa, tạo trắc nghiệm video, GPT-4o-mini, WayinVideo, Google Sheets, tự động hóa đào tạo, AI quiz generator]
---

# 🚀 **Tự Động Hoá Tạo Trắc Nghiệm Video Onboarding Với AI – Không Cần Code!**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải:
- **Tìm kiếm video** để tạo trắc nghiệm onboarding cho nhân viên mới.
- **Chuyển đổi nội dung video** thành câu hỏi trắc nghiệm MCQ (Multiple Choice) một cách thủ công, mất nhiều thời gian và dễ sai sót.
- **Cập nhật thủ công** vào Google Sheets hoặc hệ thống LMS, dẫn đến trùng lặp và mất tính nhất quán.

**Workflow này giải quyết tất cả!** Chỉ cần **nhập URL video + chủ đề**, hệ thống sẽ tự động:
✅ **Chuyển đổi video thành văn bản** (transcript) bằng WayinVideo.
✅ **Tạo trắc nghiệm MCQ** với câu trả lời và tham chiếu bằng **GPT-4o-mini**.
✅ **Lưu tự động** vào Google Sheets với metadata đầy đủ (Department, Video URL, Số lượng câu hỏi, Thời gian tạo).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công.
- **Chính xác 100%** – AI phân tích toàn bộ nội dung video, không bỏ sót chi tiết.
- **Cá nhân hóa** – Tạo trắc nghiệm theo **phân bộ phận** (Department) và **số lượng câu hỏi** mong muốn.
- **Hoạt động liên tục** – Workflow tự động chạy 24/7, không cần can thiệp.
- **Dữ liệu sẵn sàng** – Thư viện trắc nghiệm tự động cập nhật trên Google Sheets, dễ dàng chia sẻ hoặc tích hợp vào hệ thống LMS.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản WayinVideo** và **API Key** (để chuyển đổi video thành transcript).
2. **Tài khoản OpenAI** với **API Key** (để sử dụng GPT-4o-mini).
3. **Google Sheets** với:
   - Một **tab** tên **Quiz Bank**.
   - Các cột: **Department** (Phân bộ phận), **Video URL**, **Total Questions** (Số lượng câu hỏi), **Quiz Questions** (Nội dung trắc nghiệm), **Generated On** (Thời gian tạo).
4. **Credentials OAuth2** để n8n có thể truy cập Google Sheets.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14526](https://n8n.io/workflows/14526) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **có 1 lỗi nghiêm trọng** (infinite loop) và cần **cấu hình lại 3 node quan trọng**:

##### **🔴 Node 5: If — Transcript Status Check (Sửa lỗi Infinite Loop)**
- **Lỗi hiện tại**: Node `If` không có điều kiện nào, dẫn đến **lặp vô hạn** khi transcript chưa sẵn sàng.
- **Cách sửa**:
  1. Mở node `If` → Nhấn **Edit Condition**.
  2. Thêm điều kiện:
     ```json
     {{ $json.data.status }} == "SUCCEEDED"
     ```
  3. **Kết quả**: Workflow sẽ **chỉ chạy AI tạo trắc nghiệm** khi transcript đã hoàn tất.

##### **🔵 Node 2 & 4: WayinVideo — Submit/Retrieve Transcript (Cấu hình API Key)**
- **Thao tác**:
  1. Mở node `WayinVideo — Submit Transcript` (node 2) và `WayinVideo — Get Transcript` (node 4).
  2. Trong **HTTP Request Method**, chọn **POST** (node 2) và **GET** (node 4).
  3. Thêm **Header**:
     ```
     Authorization: Bearer YOUR_WAYINVIDEO_API_KEY
     ```
     (Thay `YOUR_WAYINVIDEO_API_KEY` bằng API Key thực tế từ WayinVideo).

##### **🟢 Node 6: AI — Generate MCQ Quiz (Cấu hình Prompt & Model)**
- **Thao tác**:
  1. Mở node `AI — Generate MCQ Quiz` (node 6).
  2. Trong **Agent Configuration**, đảm bảo:
     - **Model**: `gpt-4o-mini` (đã cấu hình sẵn).
     - **Prompt**: Sử dụng prompt mặc định (nếu muốn thay đổi, các sếp có thể chỉnh sửa để:
       - **Đổi ngôn ngữ** (Việt Nam, Anh, Nhật...).
       - **Thay đổi độ khó** (dễ, trung bình, khó).
       - **Thêm yêu cầu cụ thể** (ví dụ: "Câu hỏi phải có ít nhất 3 lựa chọn").
  3. **Mẹo**: Nếu muốn **chất lượng cao hơn**, có thể thay `gpt-4o-mini` bằng `gpt-4` (tuy nhiên sẽ tốn chi phí cao hơn).

##### **🟢 Node 7: Google Sheets — Save Quiz Bank (Cấu hình OAuth2 & Sheet ID)**
- **Thao tác**:
  1. Mở node `Google Sheets — Save Quiz Bank`.
  2. Nhấn **Add Credentials** → Chọn **Google OAuth2**.
  3. Đăng nhập tài khoản Google → Cho phép truy cập.
  4. Trong **Operation**, chọn **Append** (đã cấu hình sẵn).
  5. Thay `YOUR_GOOGLE_SHEET_ID` bằng **ID của tab Quiz Bank** (có thể lấy từ URL Google Sheets: `https://docs.google.com/spreadsheets/d/[ID]/edit`).

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhập **URL video** (ví dụ: một video onboarding của công ty).
   - Nhập **Department** (ví dụ: "Marketing").
   - Nhập **Total Questions** (ví dụ: 5).
   - Nhấn **Execute Workflow**.
2. **Kiểm tra**:
   - WayinVideo có chuyển đổi thành transcript không?
   - AI có tạo ra trắc nghiệm không?
   - Dữ liệu có được lưu vào Google Sheets không?
3. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi có dữ liệu mới.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram để thông báo kết quả**:
   - Thêm node `Slack` hoặc `Telegram Bot` sau node `Google Sheets` để gửi thông báo khi trắc nghiệm được tạo thành công.
   - **Cách làm**:
     ```json
     {
       "name": "8. Slack — Notify Completion",
       "type": "slackWebhook"
     }
     ```
     Thêm payload:
     ```json
     {
       "text": "🎉 Trắc nghiệm video đã tạo thành công!\n- Video: {{ $json.data.videoUrl }}\n- Số lượng câu hỏi: {{ $json.data.totalQuestions }}\n- Thời gian tạo: {{ $json.data.generatedOn }}"
     }
     ```

2. **Lưu Log để theo dõi lỗi**:
   - Thêm node `Set` trước node `If` để lưu trạng thái transcript:
     ```json
     {
       "name": "Log — Transcript Status",
       "type": "set",
       "parameters": {
         "data": {
           "status": "{{ $json.data.status }}"
         }
       }
     }
     ```
   - Sau đó, sử dụng dữ liệu này để debug nếu có lỗi.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `Schedule` để chạy workflow hàng tuần và gửi báo cáo tổng hợp về số lượng trắc nghiệm mới tạo.
   - **Cách làm**:
     ```json
     {
       "name": "Schedule — Weekly Report",
       "type": "schedule",
       "parameters": {
         "cron": "0 0 * * 0" // Thứ 7 hàng tuần
       }
     }
     ```
     Sau đó kết nối với node `Google Sheets` để cập nhật báo cáo.

4. **Tối ưu hóa AI với Prompt Engineering**:
   - Nếu muốn **câu hỏi phức tạp hơn**, chỉnh sửa prompt trong node `AI` như sau:
     ```
     Bạn là một chuyên gia tạo trắc nghiệm. Hãy phân tích video với transcript sau và tạo {{ totalQuestions }} câu hỏi trắc nghiệm MCQ với các yêu cầu sau:
     1. Mỗi câu hỏi phải có ít nhất 3 lựa chọn.
     2. Câu trả lời đúng phải được đánh dấu rõ ràng.
     3. Thêm tham chiếu cụ thể đến thời gian trong video (ví dụ: "Phút 2:30").
     4. Tránh câu hỏi quá dễ hoặc quá khó.
     ```

---

### 📌 **Kết Luận: Áp Dụng Ngay Để Nâng Cao Hiệu Quả Đào Tạo!**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **nâng cao chất lượng** của trắc nghiệm onboarding. Bằng cách tự động hóa quá trình từ **video → transcript → trắc nghiệm → lưu trữ**, công ty có thể:
✔ **Tiết kiệm thời gian** lên đến 80%.
✔ **Đảm bảo nhất quán** trong các khóa đào tạo.
✔ **Cập nhật dễ dàng** khi có video mới.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1-2 video** để đảm bảo hoạt động.
3. **Bật Active** và bắt đầu tự động hóa!

**Có thắc mắc?** Để lại comment bên dưới hoặc liên hệ với cộng đồng n8n để được hỗ trợ! 🚀