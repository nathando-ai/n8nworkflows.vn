---
title: "🚀 Tự Động Hóa Xét Duyệt CV Cho Nhiều Vị Trí Với AI, Google Sheets, Gmail & Calendly - N8n"
description: "Workflow tự động hóa AI đánh giá CV theo nhiều vị trí việc làm, gửi email mời phỏng vấn hoặc từ chối tự động, và theo dõi lịch phỏng vấn trên Calendly - hoàn toàn không cần code. Giúp HR tiết kiệm 80% thời gian xử lý ứng viên."
slug: "tieu-duyet-cv-voi-ai-google-sheets-gmail-calendly"
tags: [n8n, automation, hr-automation, ai-summarization, google-sheets, gmail, calendly, no-code]
keywords: [tự động hóa xét duyệt cv, n8n workflow hr, ai đánh giá cv, tự động hóa phỏng vấn, google sheets + gmail + calendly]
---

# 🚀 **Tự Động Hóa Xét Duyệt CV Cho Nhiều Vị Trí Với AI, Google Sheets, Gmail & Calendly**

## **🔥 Nỗi Đau Của HR: Xét Duyệt CV Thủ Công Làm Mất Thời Gian & Tiềm Năng**
Hàng ngày, các sếp HR phải:
- **Lọc hàng trăm CV** thủ công để tìm ứng viên phù hợp.
- **Đánh giá không đồng nhất** giữa các thành viên đội ngũ.
- **Gửi email mời/ từ chối** một cách tẻ nhạt, không cá nhân hóa.
- **Quên theo dõi lịch phỏng vấn** trên Calendly, dẫn đến trùng lịch hoặc bỏ lỡ ứng viên.
- **Mất thời gian** để cập nhật trạng thái ứng viên trên Google Sheets.

**Workflow này giải quyết tất cả!** Sử dụng **AI OpenRouter** để đánh giá CV theo **nhiều vị trí việc làm khác nhau**, tự động **gửi email mời/ từ chối** và **theo dõi lịch phỏng vấn** trên Calendly – **không cần viết một dòng code nào!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** xét duyệt CV thủ công.
✅ **Đánh giá khách quan** với AI theo tiêu chí cụ thể của từng vị trí.
✅ **Gửi email mời/ từ chối tự động**, cá nhân hóa với tên ứng viên.
✅ **Theo dõi lịch phỏng vấn** trên Calendly và cập nhật trạng thái tự động.
✅ **Tránh trùng lặp** với hệ thống kiểm tra email duy nhất.
✅ **Cập nhật kết quả AI** (điểm số, kỹ năng phù hợp, nhận xét) trực tiếp trên Google Sheets.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với:
   - **Google Form** để ứng viên nộp CV (đã cấu hình lưu CV lên Google Drive).
   - **Bảng Google Sheets** lưu trữ ứng viên (cần thêm các cột: `score`, `seniority`, `recommendation`, `HR_Decision`, `Email_Status`, `Interview_Time`).
2. **Tài khoản Google Drive** (để workflow tải CV từ liên kết Google Drive).
3. **Tài khoản Gmail** (để gửi email mời/ từ chối).
4. **Tài khoản Calendly** (để tạo liên kết phỏng vấn tự động).
5. **API Key OpenRouter** (đăng ký miễn phí tại [openrouter.ai](https://openrouter.ai/)).
6. **n8n Data Table** tên **"CV Screening"** với cột `Email` (string) để tránh xử lý trùng lặp.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15293](https://n8n.io/workflows/15293) hoặc copy toàn bộ JSON từ đây.
- **Mở n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** bằng cách bật nút **"Active"** ở góc trên bên phải.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **3 phần chính**, mỗi phần đều cần cấu hình kỹ lưỡng:

##### **📌 Phần 1: Xét Duyệt CV Tự Động (33 Node)**
- **New Application Received (Google Sheets Trigger)**
  - Chọn **Google Sheets OAuth2 API** và chỉ định **bảng lưu trữ ứng viên** (bảng chứa kết quả Google Form).
  - **Lưu ý**: Workflow **polling** (kiểm tra) bảng Sheets **mỗi phút** để bắt đầu xử lý ứng viên mới.

- **Extract CV File ID (Code Node)**
  - **Không cần chỉnh sửa**, node này tự động **trích xuất ID file CV** từ liên kết Google Drive (đối với 3 định dạng khác nhau).

- **Duplicate Guard (Data Table Node)**
  - **Không cần chỉnh sửa**, node này **kiểm tra email ứng viên** đã được xử lý chưa trong **Data Table "CV Screening"**.
  - Nếu email đã tồn tại → **dừng workflow** (tránh trùng lặp).

- **Route by Job Role (Switch Node)**
  - **Cần chỉnh sửa**: Thêm **điều kiện mới** cho mỗi vị trí việc làm mới (ví dụ: "Lập trình viên React", "Chuyên gia SEO").
  - Mỗi vị trí cần **Job Profile Set Node** riêng (xem phần **Customization** dưới đây).

- **Job Profile Set Nodes (4 Node)**
  - **BẮT BUỘC chỉnh sửa** để phù hợp với yêu cầu của từng vị trí:
    - **required_skills**: Kỹ năng bắt buộc (ví dụ: "React", "Node.js").
    - **nice_to_have_skills**: Kỹ năng ưu tiên (ví dụ: "TypeScript", "Docker").
    - **min_years**: Số năm kinh nghiệm tối thiểu.
    - **seniority**: "Junior", "Mid", "Senior".
    - **tech_weight**, **experience_weight**, **nice_to_have_weight**: Cân nặng cho mỗi tiêu chí (tổng = 100).

- **OpenRouter Chat Model (LM Chat OpenRouter)**
  - **Chọn model**:
    - **openrouter/free** (để test).
    - **openai/gpt-4o** (để sản xuất).
  - **Điền API Key** trong **OpenRouter Credentials** (đã cấu hình trước).

- **Structured Output Parser**
  - **Không cần chỉnh sửa**, node này **tách kết quả AI** thành JSON có cấu trúc:
    ```json
    {
      "score": 85,
      "seniority": "Mid",
      "recommendation": "Invite",
      "matched_skills": ["React", "Node.js"],
      "missing_skills": ["Docker"],
      "nice_to_have_matched": ["TypeScript"],
      "red_flags": null,
      "summary": "Ứng viên có kinh nghiệm React và Node.js, phù hợp vị trí Mid."
    }
    ```

- **Update in Sheet (Google Sheets)**
  - **Không cần chỉnh sửa**, node này **cập nhật kết quả AI** (điểm số, nhận xét) vào cùng hàng với ứng viên trên Google Sheets.

##### **📌 Phần 2: Gửi Email Mời/ Từ Chối (10 Node)**
- **HR Decision Watcher (IF Node)**
  - **Cần chú ý**:
    - Workflow **polling** bảng Sheets **mỗi phút** để kiểm tra cột `HR_Decision`.
    - **HR phải nhập chính xác**:
      - **"Send Invite"** → Gửi email mời phỏng vấn.
      - **"Send Rejection"** → Gửi email từ chối.
    - **Tránh trùng lặp email**: Nếu `Email_Status` đã là **"Sent"**, workflow **dừng lại**.

- **Invitation Message & Rejection Message (Set Nodes)**
  - **Chỉnh sửa nội dung email**:
    - Thêm **tên công ty**, **liên kết Calendly**, **mã QR** (nếu có).
    - **BẮC BUỘC thay thế `YOUR_CALENDLY_LINK`** trong node **Invitation Message** bằng liên kết Calendly thực tế của bạn.

- **Send Interview Invite / Send Rejection Email (Gmail Nodes)**
  - **Chọn Gmail OAuth2 Credential** đã cấu hình trước.
  - **Không cần chỉnh sửa**, node này **gửi email tự động** và cập nhật `Email_Status = "Sent"`.

##### **📌 Phần 3: Theo Dõi Lịch Phỏng Vấn (10 Node)**
- **Interview Event Received (Calendly Trigger)**
  - **Chọn Calendly OAuth2 API** và **chọn sự kiện** (`invitee.created` và `invitee.canceled`).

- **Route by Event Type (Switch Node)**
  - **Không cần chỉnh sửa**, node này **chia làm 2 nhánh**:
    - **Booking**: Khi ứng viên đặt lịch.
    - **Cancellation**: Khi ứng viên hủy lịch.

- **Format Interview Time (DateTime Node)**
  - **Chỉnh sửa format thời gian** để phù hợp với **múi giờ của bạn** (ví dụ: `HH:mm (Vietnam Standard Time)`).

- **Skip if Rescheduled (IF Node)**
  - **Không cần chỉnh sửa**, node này **kiểm tra** nếu lịch được **chuyển lịch** (`rescheduled = true`), thì **dừng workflow** để tránh trùng lặp.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một ứng viên mẫu:
   - Thêm một hàng mới vào Google Sheets (đã điền đầy đủ thông tin).
   - Kiểm tra **log** trong n8n để xem workflow chạy như thế nào.
2. **Bật Active** workflow sau khi đã kiểm tra.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM TIẾP THEO]
- **Thêm vị trí việc làm mới**:
  1. Thêm **tùy chọn mới** vào Google Form (dropdown).
  2. Thêm **điều kiện mới** vào **Route by Job Role (Switch Node)**.
  3. **Sao chép** một **Job Profile Set Node** và chỉnh sửa kỹ năng cho vị trí mới.

- **Cập nhật scoring weights**:
  - Mở **Job Profile Set Node** → Điều chỉnh `tech_weight`, `experience_weight`, `nice_to_have_weight` (tổng = 100).

- **Lưu log hoạt động**:
  - Thêm **Google Drive Node** sau **Send Email** để lưu **copy email** vào một folder cụ thể.

- **Gửi báo cáo định kỳ**:
  - Sử dụng **n8n-nodes-base.email** để gửi **báo cáo tổng hợp** về ứng viên hàng tuần cho HR.

- **Tích hợp Slack/Telegram**:
  - Thêm **Slack Webhook Node** để thông báo khi có **email mời/ từ chối** mới.

- **Sử dụng AI mạnh hơn**:
  - Thay đổi model trong **OpenRouter Chat Model** từ `openrouter/free` sang `gpt-4o` hoặc `deepseek` để có kết quả chính xác hơn.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng HR khỏi công việc lặp lại**, giúp:
✔ **Xét duyệt CV nhanh chóng** với AI.
✔ **Gửi email tự động** với nội dung cá nhân hóa.
✔ **Theo dõi lịch phỏng vấn** một cách chính xác.
✔ **Tiết kiệm thời gian** để tập trung vào việc **quyết định tuyển dụng** chứ không phải xử lý thủ công.

**🚀 Hãy áp dụng ngay workflow này cho doanh nghiệp của các sếp!**
Nếu cần hỗ trợ, các sếp có thể liên hệ với **Salman Mehboob** (tác giả) thông qua [n8n Community](https://community.n8n.io/).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý cuối cùng**:
- **Không cần code** để chạy workflow này.
- **Tùy chỉnh dễ dàng** cho phù hợp với yêu cầu của từng vị trí việc làm.
- **Hoàn toàn miễn phí** (trừ chi phí API OpenRouter và các dịch vụ Google/Gmail/Calendly).