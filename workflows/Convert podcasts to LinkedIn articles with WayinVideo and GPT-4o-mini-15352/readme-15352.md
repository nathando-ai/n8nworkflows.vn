---
title: "🚀 Chuyển Podcast Sang Bài Đăng LinkedIn Tự Động Với WayinVideo + GPT-4o-mini - Không Cần Viết Tài Liệu!"
description: "Workflow tự động hóa hoàn toàn chuyển đổi nội dung podcast thành bài đăng LinkedIn chuyên nghiệp, bao gồm tiêu đề hấp dẫn, nội dung chi tiết, 5 điểm học tập và hashtags phù hợp - chỉ cần nhập URL podcast. Tiết kiệm thời gian lên đến 80% so với viết thủ công!"
slug: "chuyen-podcast-sang-bai-dang-linkedin-tu-dong"
tags: [n8n, automation, content-marketing, ai-gpt, wayinvideo, linkedin, no-code]
keywords: [tự động hóa podcast, chuyển đổi nội dung, bài đăng linkedin tự động, gpt-4o-mini, wayinvideo api, tự động viết bài]
---

# 🚀 **Chuyển Podcast Sang Bài Đăng LinkedIn Tự Động - Không Cần Viết Tài Liệu!**

### **Giải pháp cho những ai:**
- **Chủ podcast** muốn tái sử dụng nội dung podcast trên LinkedIn mà không mất thời gian viết bài.
- **Marketer nội dung** cần tạo bài đăng chuyên nghiệp từ các buổi phỏng vấn hoặc podcast.
- **Nhà xây dựng thương hiệu cá nhân** muốn tăng tầm nhìn và tương tác trên LinkedIn mà không cần viết từ đầu.

Workflow này **tự động hóa toàn bộ quy trình** từ việc transcribe podcast (với WayinVideo) đến viết bài LinkedIn hoàn chỉnh (với GPT-4o-mini) và lưu draft vào Google Sheets để bạn chỉ việc review và đăng tải.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với viết bài từ đầu.
- **Nội dung chuyên nghiệp** với cấu trúc tiêu đề hấp dẫn, nội dung 400-600 từ, 5 điểm học tập và hashtags phù hợp.
- **Tái sử dụng nội dung hiệu quả** từ podcast, buổi phỏng vấn hoặc video.
- **Hoạt động 24/7** - không cần can thiệp thủ công.
- **Dữ liệu tập trung** - tất cả bài đăng được lưu vào Google Sheets với trạng thái "Draft" để review.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản WayinVideo** (để transcribe podcast):
   - API Key từ [cài đặt tài khoản WayinVideo](https://wayin.ai/account).
2. **Tài khoản OpenAI** (để sử dụng GPT-4o-mini):
   - API Key từ [OpenAI Platform](https://platform.openai.com/).
3. **Tài khoản Google** (để lưu draft bài đăng):
   - Credential OAuth2 của Google Sheets.
   - Một **Google Sheet** mới với tab tên **"LinkedIn Drafts"** và các cột sau:
     | Podcast Title | Video URL | Episode Duration (min) | LinkedIn Headline | LinkedIn Article | Key Takeaways | Hashtags | Word Count | Generated On | Status |
     |---------------|-----------|------------------------|------------------|------------------|---------------|-----------|------------|-------------|----------|
4. **URL podcast hoặc video** (được upload lên WayinVideo trước).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15352](https://n8n.io/workflows/15352) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **"Import"** → Dán JSON hoặc tải file JSON đã download.
- Chọn **"Import"** để hoàn tất.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **11 node** quan trọng, các sếp cần cấu hình như sau:

#### **🔹 Node 2 & 4: WayinVideo — Submit & Get Transcript**
- **Thay thế `YOUR_WAYINVIDEO_API_KEY`** trong hai node này bằng API Key của bạn (từ WayinVideo).
- **Cấu hình URL API**:
  - **Submit Transcription**: `https://api.wayin.ai/v1/tasks`
  - **Get Transcript Results**: `https://api.wayin.ai/v1/tasks/{taskId}` (sử dụng `{taskId}` từ response của node 2).

#### **🔹 Node 9: OpenAI — GPT-4o-mini Model**
- **Kết nối credential OpenAI**:
  - Tạo một **credential mới** trong n8n với loại `OpenAI` và điền API Key từ OpenAI.
  - Chọn credential này trong node 9.
- **Prompt mặc định** đã được tối ưu hóa cho LinkedIn, nhưng các sếp có thể **cập nhật** trong node 8 (AI Agent) nếu muốn thay đổi phong cách viết.

#### **🔹 Node 11: Google Sheets — Save LinkedIn Draft**
- **Kết nối credential Google Sheets**:
  - Tạo credential OAuth2 trong n8n và điền thông tin từ Google Cloud Console.
- **Thay thế `YOUR_GOOGLE_SHEET_ID`** bằng ID của Google Sheet bạn đã tạo (tham khảo cách lấy ID [tại đây](https://support.google.com/docs/answer/1204120)).
- **Đảm bảo tab "LinkedIn Drafts"** có đúng cấu trúc cột như mô tả ở trên.

#### **🔹 Node 7 & 10: Code — Format Transcript & Parse AI Output**
- **Node 7 (Format Transcript)**:
  - Code mặc định đã được tối ưu hóa, nhưng các sếp có thể **cập nhật** nếu muốn thay đổi định dạng đầu vào cho GPT.
- **Node 10 (Parse AI Output)**:
  - Sử dụng **regex** để trích xuất tiêu đề, nội dung, điểm học tập và hashtags từ output của GPT.
  - Nếu GPT trả về định dạng khác, cần **cập nhật regex** để trích xuất chính xác.

#### **🔹 Node 5: IF — Transcription Complete?**
- Node này **kiểm tra trạng thái transcribe** từ WayinVideo.
  - Nếu trạng thái **không phải "SUCCEEDED"**, workflow sẽ **chờ 30 giây** và retry.
  - Nếu trạng thái **"SUCCEEDED"**, workflow tiến đến bước viết bài.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với một URL podcast mẫu:
   - Điền URL podcast vào **Form Trigger** (Node 1).
   - Chọn **"Run Workflow"** để kiểm tra toàn bộ quy trình.
   - Kiểm tra **Google Sheets** xem draft bài đăng có được tạo ra không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **trạng thái "Active"**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để thông báo khi bài đăng được tạo thành công.
   - Ví dụ: `When workflow completes → Send notification to Slack channel`.

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Database** để lưu lịch sử các bài đăng đã tự động hóa.

3. **Tự động đăng bài lên LinkedIn**:
   - Sử dụng **LinkedIn API** (nếu có) hoặc **n8n-nodes-linkedin** (nếu có node hỗ trợ) để đăng bài tự động sau khi review.

4. **Tối ưu prompt cho GPT**:
   - Cập nhật **Node 8 (AI Agent)** để thay đổi phong cách viết (ví dụ: chuyên nghiệp hơn, thân thiện hơn, hoặc phù hợp với ngành nghề cụ thể).

5. **Xử lý lỗi tự động**:
   - Thêm node **Error Handling** để gửi email/Slack khi có lỗi (ví dụ: API WayinVideo thất bại, GPT trả về output không hợp lệ).
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc viết bài LinkedIn từ đầu, đồng thời **tăng chất lượng nội dung** nhờ AI và transcribe chuyên nghiệp. **Chỉ cần nhập URL podcast**, hệ thống sẽ tự động:
✅ Transcribe podcast với WayinVideo.
✅ Viết bài LinkedIn hoàn chỉnh với GPT-4o-mini.
✅ Lưu draft vào Google Sheets để review.

**Hành động ngay!**
- **Import workflow** và bắt đầu tự động hóa nội dung của mình.
- **Tối ưu hóa prompt** để phù hợp với phong cách viết của bạn.
- **Kết hợp với các công cụ khác** (Slack, Telegram, LinkedIn API) để hoàn thiện hệ thống.

**🎁 Đăng ký VPS để chạy workflow 24/7:**
:::info[HƯỚNG DẪN CÀI ĐẶT N8N TRÊN VPS]
Để workflow hoạt động liên tục, các sếp nên **self-host n8n** trên VPS. Dưới đây là một số lựa chọn ưu tiên:
- **TinoHost (VPS 4GB Xeon chỉ 50k/tháng)**:
  👉 [Đăng ký VPS](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%).
- **BNIX (VPS 4GB chỉ 60k/tháng)**:
  👉 [Đăng ký VPS](https://my.bnix.one/aff.php?aff=172).
:::

**Bắt đầu tự động hóa nội dung LinkedIn của mình ngay hôm nay!** 🚀