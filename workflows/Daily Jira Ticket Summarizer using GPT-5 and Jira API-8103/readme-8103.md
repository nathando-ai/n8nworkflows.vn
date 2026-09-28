---
title: "🤖 **Tự Động Hóa Tóm Tắt Tickets Jira Hàng Ngày Với GPT-5 – Giảm Thời Gian Theo Dõi 90%!**"
description: "Workflow tự động hóa lấy tất cả tickets Jira được tạo trong ngày, phân tích chi tiết bằng GPT-5, tổng hợp thành báo cáo chuyên nghiệp và gửi email tự động hàng ngày. Giúp các sếp tiết kiệm thời gian theo dõi công việc, cải thiện hiệu suất và giảm thiểu lỗi nhân sự."
slug: "tieu-dong-hoa-tom-tat-tickets-jira-hang-ngay-gpt-5"
tags: [n8n, automation, jira, gpt-5, ai-summarization, no-code, workflow-tieng-viet]
keywords: [tự động hóa jira, gpt-5 n8n, tổng hợp tickets jira, báo cáo hàng ngày tự động, ai automation, n8n workflow jira]
---

# **🚀 Tự Động Hóa Tóm Tắt Tickets Jira Hàng Ngày Với GPT-5 – Giúp Các Sếp Tiết Kiệm 10+ Giờ/Tuần**

---

## **💥 Nỗi Đau Của Các Sếp Khi Theo Dõi Tickets Jira Thủ Công**
Hàng ngày, các sếp phải:
- **Lọc và tổng hợp** hàng chục tickets mới được tạo trong Jira.
- **Đọc chi tiết** từng ticket, comments và lịch sử thay đổi để hiểu tình trạng tiến độ.
- **Tóm tắt bằng tay** thông tin quan trọng để báo cáo cho ban lãnh đạo.
- **Gửi email** tổng hợp cho team hoặc khách hàng, mất thời gian và dễ bị lỗi.

**Kết quả?** Thời gian theo dõi công việc bị "chôn vùi" trong công việc thủ công, hiệu suất giảm, và quyết định không còn dựa trên dữ liệu chính xác.

---
### **🎯 Kết Quả Các Sếp Nhận Được Khi Sử Dụng Workflow Này**
:::tip[**3 Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm 10+ giờ/tuần** – Workflow tự động lấy và phân tích tất cả tickets mới.
✅ **Báo cáo chuyên nghiệp** – GPT-5 tổng hợp thông tin chi tiết thành tóm tắt logic, đề xuất giải pháp và gợi ý hành động.
✅ **Gửi email tự động** – Báo cáo được format đẹp và gửi qua Gmail hàng ngày, không cần can thiệp.
✅ **Cải thiện quyết định** – Dữ liệu được phân tích AI, giảm thiểu sai sót nhân sự.
:::

---

## **🔧 Yêu Cầu Cần Thiết Trước Khi Sử Dụng**
:::info[**CHUẨN BỊ CÁC THÀNH PHẦN NÀY**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Jira Cloud** (API Key) – Để lấy dữ liệu tickets.
2. **Tài khoản Gmail** (OAuth2) – Để gửi báo cáo hàng ngày.
3. **API Key OpenAI** – Để sử dụng mô hình **GPT-5** phân tích tickets.
4. **Dự án Jira cụ thể** – Workflow sẽ lấy tất cả tickets mới được tạo trong ngày từ dự án này.
:::

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow Từ File JSON**
:::note[**Bước 1: Tải Workflow**]
- Tải file JSON từ [n8n.io/workflows/8103](https://n8n.io/workflows/8103) (hoặc copy JSON từ trang này).
- Trong **n8n Editor**, nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô **Import Workflow**.
:::

### **2. Các Bước Cấu Hình BẮT BUỘC**
Workflow gồm **18 node**, nhưng chỉ có **5 node quan trọng** cần chỉnh sửa:

#### **🔹 Node 1: "Set Project Key" (n8n-nodes-base.set)**
- **Mục đích**: Xác định dự án Jira cần lấy tickets.
- **Cách làm**:
  - Nhấp vào node này → Chọn **Edit** → Điền **Project Key** của dự án Jira (ví dụ: `SUP`).
  - Lưu ý: Project Key là phần sau `/projects/` trong URL Jira (ví dụ: `https://your-domain.atlassian.net/projects/SUP/`).

#### **🔹 Node 2: "OpenAI Chat Model" (lmChatOpenAi)**
- **Mục đích**: Chỉ định mô hình AI là **GPT-5**.
- **Cách làm**:
  - Nhấp vào node → Chọn **Edit** → Trong **Model**, chọn `gpt-5` (nếu không có, thêm vào danh sách mô hình).
  - Đảm bảo **API Key OpenAI** đã được cấu hình trong **Credentials** của n8n.

#### **🔹 Node 3: "Ticket Summarizer" (chainLlm)**
- **Mục đích**: Cấu hình prompt cho AI tóm tắt tickets.
- **Cách làm**:
  - Nhấp vào node → Chọn **Edit** → Trong **Chain**, chỉnh sửa **Prompt** để phù hợp với yêu cầu của công ty.
  - **Gợi ý prompt**:
    ```plaintext
    Tóm tắt ticket này với cấu trúc sau:
    1. Tóm tắt ngắn (1-2 câu).
    2. Nhận xét về tiến độ hiện tại.
    3. Gợi ý hành động tiếp theo.
    4. Nếu có, đề xuất giải pháp kỹ thuật.
    ```
  - Chọn **Output Parser** là `Structured Output Parser` để AI trả về định dạng JSON.

#### **🔹 Node 4: "Send Ticket Summaries" (gmail)**
- **Mục đích**: Cấu hình email gửi báo cáo.
- **Cách làm**:
  - Nhấp vào node → Chọn **Edit** → Điền:
    - **Recipient**: Email của người nhận (ví dụ: `team@company.com`).
    - **Subject**: `"Daily Ticket Summaries – [Date]"` (có thể tự động hóa bằng biến `{{ $node["Schedule Trigger"].json["date"] }}`).
    - **Body**: Sử dụng **Format Body** (node sau) để định dạng email đẹp.

#### **🔹 Node 5: "Schedule Trigger" (scheduleTrigger)**
- **Mục đích**: Chạy workflow hàng ngày.
- **Cách làm**:
  - Nhấp vào node → Chọn **Edit** → Chọn **Cron Expression**:
    - `0 8 * * *` → Chạy lúc 8h sáng hàng ngày.
    - Thay đổi theo nhu cầu (ví dụ: `0 17 * * 1-5` để chạy từ thứ 2 đến thứ 6 lúc 5h chiều).

---
### **3. Kích Hoạt Workflow**
:::success[**BƯỚC CUỐI CUNG**]
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** để kiểm tra các node hoạt động.
   - Kiểm tra email nhận được có đúng format không.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động hàng ngày.
:::

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH LÀM ĐẸP HƠN**]
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi báo cáo ngay khi có tickets mới.
2. **Lưu Log Vào Google Sheets**:
   - Thêm node **Google Sheets** sau "Aggregate" để lưu tất cả lịch sử tickets.
3. **Tùy Chỉnh AI Prompt**:
   - Nếu muốn AI đề xuất giải pháp chi tiết hơn, cập nhật prompt trong node **Ticket Summarizer**.
4. **Báo Cáo Định Kỳ Cho Khách Hàng**:
   - Sử dụng node **Zapier** hoặc **Make (Integromat)** để gửi báo cáo đến khách hàng qua email hoặc CRM.
5. **Duy Trì Dữ Liệu**:
   - Thêm node **Database** (ví dụ: PostgreSQL) để lưu trữ lịch sử tickets lâu dài.
:::

---

## **📌 Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian!**
Workflow này **giải phóng các sếp khỏi công việc thủ công tẻ nhạt**, giúp họ tập trung vào việc **quản lý team và chiến lược** thay vì mất thời gian theo dõi tickets.

**👉 Hành động ngay:**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Jira, Gmail và OpenAI** theo hướng dẫn.
3. **Bật Schedule Trigger** để nhận báo cáo hàng ngày.

**💡 Cần hỗ trợ kỹ thuật?**
- Liên hệ **Billy Christi** (n8n Expert) qua email: [billychartanto@gmail.com](mailto:billychartanto@gmail.com).
- Hoặc tham khảo thêm dự án của Billy tại: [billychristi.com/n8n](https://www.billychristi.com/n8n).

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) thay vì dùng phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Hãy tự động hóa ngay hôm nay – thời gian là tài sản quý giá nhất của các sếp!**