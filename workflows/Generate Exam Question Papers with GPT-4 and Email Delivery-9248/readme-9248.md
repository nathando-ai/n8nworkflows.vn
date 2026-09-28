---
title: "🎓 Tự Động Hóa Tạo Đề Thi Trắc Nghiệm Với GPT-4 + Gửi Email Tự Động (N8N)"
description: "Workflow tự động hóa hoàn toàn không code giúp giáo viên tạo đề thi từ 0 đến 100 câu hỏi đa dạng (2 điểm, 13 điểm, 14 điểm) bằng GPT-4, sau đó gửi trực tiếp qua email. Giúp tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tay-dong-hoa-tao-de-thi-gpt-4-email"
tags: [n8n, automation, no-code, giáo dục, GPT-4, email automation, LangChain]
keywords: [tự động hóa đề thi, tạo đề thi bằng AI, n8n workflow giáo dục, gửi đề thi email tự động, GPT-4 tự động hóa]
---

# 🎓 **Tự Động Hóa Tạo Đề Thi Trắc Nghiệm Với GPT-4 + Gửi Email Tự Động (N8N)**

## **🔥 Nỗi Đau Của Giáo Viên Khi Tạo Đề Thi**
Giáo viên thường phải mất **từ 2-5 tiếng** để tạo một bộ đề thi hoàn chỉnh, bao gồm:
- **Tạo câu hỏi 2 điểm** (thường là lý thuyết ngắn)
- **Tạo câu hỏi 13 điểm** (phân tích, tính toán)
- **Tạo câu hỏi 14 điểm** (lập luận, thiết kế)
- **Sắp xếp lại cấu trúc** sao cho hợp lý
- **Gửi đề cho học sinh** qua email hoặc Google Classroom

**Kết quả?** Đề thi không đồng nhất, mất nhiều thời gian, và dễ bị lỗi chính tả hoặc logic.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quá trình** bằng GPT-4, tạo ra **các câu hỏi đa dạng, chính xác và chuyên nghiệp**, sau đó **gửi trực tiếp qua email** chỉ với một cú nhấp chuột.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Đề thi đa dạng và chuyên nghiệp**, tránh sai sót logic.
- **Cấu trúc đề tự động sắp xếp** theo yêu cầu (2 điểm, 13 điểm, 14 điểm).
- **Gửi đề qua email tự động**, không cần copy-paste.
- **Hoạt động 24/7**, không phụ thuộc vào thời gian làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (để sử dụng GPT-4):
   - API Key từ [OpenAI](https://platform.openai.com/) (đăng ký miễn phí).
   - **Mã giảm giá 20% cho API Key** (đăng ký qua [link này](https://platform.openai.com/api-keys?affiliate=gracewell) với mã **GRACEWELL20**).
2. **Tài khoản Gmail** (để gửi đề thi):
   - **OAuth 2.0 Credentials** (cấu hình trong n8n).
3. **Mô tả chi tiết môn học** (để AI tạo đề):
   - **Mã môn học** (ví dụ: "Toán 12", "Vật Lý 11").
   - **Chương trình giảng dạy (syllabus)** (nội dung cụ thể cần đề thi).
   - **Email nhận đề** (của giáo viên hoặc học sinh).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/9248](https://n8n.io/workflows/9248) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/9248) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng **GPT-4** và **LangChain** để tạo đề thi, nên cần cấu hình chính xác các node sau:

##### **🔹 Node "OpenAI Chat Model" (3 model khác nhau)**
- **Model mặc định:** `gpt-4-turbo-2024-04-09` (khuyến nghị sử dụng).
- **Lưu ý:**
  - Đảm bảo **API Key OpenAI** được điền vào **Credentials** (`openAiApi`).
  - Nếu không đủ credit, **cập nhật API Key mới** trong **Credentials Management**.

##### **🔹 Node "Part A QP Agent", "Part B QP Agent", "Part C QP Agent" (3 AI Agent khác nhau)**
- **Chức năng:**
  - **Part A:** Tạo **4 câu hỏi 2 điểm** (lý thuyết ngắn).
  - **Part B:** Tạo **4 câu hỏi 13 điểm** (phân tích, tính toán).
  - **Part C:** Tạo **2 câu hỏi 14 điểm** (lập luận, thiết kế).
- **Lưu ý:**
  - **Không cần chỉnh sửa Prompt** (đã được tối ưu sẵn).
  - Nếu muốn **thay đổi số lượng câu hỏi**, cần chỉnh sửa trong **Structured Output Parser**.

##### **🔹 Node "QP Formatter with HTML" (HTML Template)**
- **Hướng dẫn:**
  - Mở node này và **điền mã HTML template** để hiển thị đề thi.
  - **Ví dụ template cơ bản:**
    ```html
    <h1>{{ $json.subject }}</h1>
    <p>Môn: {{ $json.subject }}</p>
    <p>Thời gian: 90 phút</p>
    <div>
      <h2>Phần A: 4 câu hỏi 2 điểm</h2>
      {{ $json.partA }}
    </div>
    <div>
      <h2>Phần B: 4 câu hỏi 13 điểm</h2>
      {{ $json.partB }}
    </div>
    <div>
      <h2>Phần C: 2 câu hỏi 14 điểm</h2>
      {{ $json.partC }}
    </div>
    ```
  - **`{{ $json.partA }}`**, **`{{ $json.partB }}`**, **`{{ $json.partC }}`** sẽ tự động được thay thế bởi câu hỏi từ AI.

##### **🔹 Node "Gmail" (Gửi Email)**
- **Lưu ý:**
  - Chọn **Credentials** là `gmailOAuth2` (đã cấu hình trước).
  - **Không cần chỉnh sửa** nếu đã cấu hình OAuth 2.0 trong n8n.

##### **🔹 Node "Merge" & "Merge1" (Kết hợp dữ liệu)**
- **Không cần chỉnh sửa**, workflow sẽ tự động gộp dữ liệu từ AI vào template HTML.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - Nhập vào **Form Trigger**:
     - **Môn học:** "Toán 12"
     - **Chương trình giảng dạy:** "Đại số, Hình học, Giải tích"
     - **Email nhận:** `giaovien@example.com`
   - **Chạy Test Run** để kiểm tra đề thi được tạo ra như thế nào.
2. **Bật Active Workflow:**
   - Sau khi kiểm tra thành công, **bật Active** để workflow hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM TIẾP]
- **Thêm Slack/Telegram Notifications:**
  - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi đề thi được tạo xong.
- **Lưu Log vào Google Sheets:**
  - Thêm node **Google Sheets** để ghi lại lịch sử đề thi (môn học, ngày tạo, email nhận).
- **Tự động gửi đề cho nhiều giáo viên:**
  - Sử dụng node **Merge** kết hợp với **Gmail Bulk Send** để gửi đề cho nhiều email cùng lúc.
- **Cập nhật syllabus tự động:**
  - Nếu có **Google Drive/Notion** chứa syllabus, sử dụng node **Google Drive** hoặc **Notion** để lấy dữ liệu tự động.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng giáo viên khỏi công việc tạo đề thi mệt mỏi**, giúp họ tập trung vào **giảng dạy và tương tác với học sinh**. Với **GPT-4** và **n8n**, đề thi không chỉ **nhanh chóng** mà còn **chuyên nghiệp và đa dạng**.

**🚀 Hãy thử ngay và tiết kiệm thời gian cho mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý:** Nếu gặp vấn đề với API Key OpenAI, hãy liên hệ [OpenAI Support](https://help.openai.com/) để khôi phục.