---
title: "🤖 Tự Động Hồi Phục Khách Hàng Cũ Với AI Claude 3.7 Sonnet, Gmail & Google Sheets - Không Cần Code"
description: "Workflow tự động hóa gửi email hồi phục khách hàng cũ 100% cá nhân hóa bằng AI Claude 3.7 Sonnet, tránh spam và tiết kiệm 10+ giờ/lần cho các sếp. Kết hợp Gmail + Google Sheets để quản lý hiệu quả."
slug: "tieu-dong-hoi-phuc-khach-hang-cu-ai-claude-3-7"
tags: [n8n, automation, lead-nurturing, ai-multimodal, gmail, google-sheets, claude-3-7, no-code]
keywords: [n8n workflow hồi phục khách hàng, tự động hóa email AI, Claude 3.7 Sonnet n8n, gửi email cá nhân hóa tự động, quản lý khách hàng cũ bằng Google Sheets]
---

# 🚀 **Hồi Phục Khách Hàng Cũ Với AI: Gửi Email Cá Nhân Hóa Tự Động Hằng Ngày**

Bạn đã từng phải mất **5-10 giờ/lần** để tìm kiếm, phân tích và viết email hồi phục cho khách hàng cũ? Hay phải lo lắng rằng email của bạn **trùng lặp, không cá nhân hóa** và bị coi là spam? **Workflow này giải quyết tất cả vấn đề đó** bằng cách tự động hóa toàn bộ quy trình với **AI Claude 3.7 Sonnet**, kết hợp **Gmail** và **Google Sheets** để:
✅ **Tự động gửi email hồi phục 100% cá nhân hóa** dựa trên lịch sử giao tiếp trước đó.
✅ **Tránh gửi email cho khách hàng đã phản hồi** trong vòng 30 ngày, tránh spam.
✅ **Tiết kiệm 10+ giờ/tháng** cho các sếp, tự động hóa toàn bộ quy trình từ A-Z.
✅ **Cập nhật trạng thái khách hàng** trên Google Sheets để theo dõi hiệu quả.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. N8n trên máy chủ cloud sẽ **không bị treo** và hoạt động liên tục.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao, phù hợp cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải viết email hồi phục thủ công, tự động hóa **100% quy trình**.
- **Tăng tỷ lệ phản hồi**: Email được **AI Claude 3.7 Sonnet** viết dựa trên **lịch sử giao tiếp**, cao độ cá nhân hóa.
- **Tránh spam**: **Bỏ qua khách hàng đã phản hồi** trong vòng 30 ngày, giữ mối quan hệ chuyên nghiệp.
- **Quản lý dễ dàng**: **Cập nhật trạng thái khách hàng** trên Google Sheets, theo dõi hiệu quả dễ dàng.
- **Hoạt động liên tục**: **Không cần can thiệp**, workflow chạy tự động hằng ngày.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để kết nối **Gmail** và **Google Sheets**).
✔ **API Key Anthropic** (để sử dụng **Claude 3.7 Sonnet**).
✔ **Google Sheet** với **3 tab** (cấu trúc chi tiết dưới đây).
✔ **Email chính thức** (để gửi email hồi phục từ Gmail).

#### **Cấu trúc Google Sheet cần thiết**
Workflow yêu cầu **3 tab** trong Google Sheet:
1. **"Database"** (dữ liệu khách hàng cũ):
   | Tên Khách Hàng | Email | Trạng Thái | STOP (Nếu muốn dừng) |
   |----------------|-------|-------------|----------------------|
   | Khách Hàng A   | abc@email.com | Chờ | FALSE |

2. **"Follow-up Messages"** (template email hồi phục):
   | Tình Huống | Nội Dung Template |
   |------------|-------------------|
   | Khách hàng không phản hồi | "Xin chào [Tên], chúng tôi thấy quý khách đã không phản hồi trong thời gian gần đây..." |

3. **"Situation"** (prompt cho AI):
   | Tình Huống | Prompt AI |
   |------------|-----------|
   | Khách hàng cũ | "Viết email hồi phục cho khách hàng cũ [Tên], dựa trên lịch sử giao tiếp trước đó..." |

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/14217](https://n8n.io/workflows/14217) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **paste** vào **n8n Editor** (tab "Import").

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **20 node**, các sếp cần **cấu hình chính xác** các phần sau:

##### **🔹 1. Cấu hình Trigger & Google Sheets**
- **Node "⏰ Daily Schedule Trigger"**:
  - Đặt thời gian chạy **mỗi ngày** (ví dụ: 8h sáng).
- **Node "📋 Old Client Database"**:
  - **Chọn OAuth Credentials** của Google Sheets.
  - **Điền Sheet ID** (tìm trong URL của Google Sheet: `https://docs.google.com/spreadsheets/d/[SHEET_ID]/edit`).
  - **Chọn tab "Database"** và **cột dữ liệu** (ví dụ: `A1:D1000`).

##### **🔹 2. Cấu hình Gmail**
- **Node "📧 Fetch Client's Latest Email"**:
  - **Chọn OAuth Credentials** của Gmail.
  - **Điền email chính thức** (để AI gửi email hồi phục).
- **Node "📬 Fetch 10 Email Conversations"**:
  - **Chọn cùng OAuth Credentials** của Gmail.
  - **Lọc email** từ địa chỉ khách hàng (ví dụ: `FROM:abc@email.com`).

##### **🔹 3. Cấu hình Claude 3.7 Sonnet**
- **Node "🤖 Claude 3.7 Sonnet LLM"**:
  - **Điền API Key Anthropic** (tạo tại [Anthropic](https://www.anthropic.com/)).
  - **Chọn model**: `claude-3-7-sonnet-20250219`.
- **Node "📦 Prepare AI Input Bundle"**:
  - **Kiểm tra dữ liệu input** (template + lịch sử email) trước khi AI xử lý.

##### **🔹 4. Cấu hình Email & Google Sheets Update**
- **Node "📤 Send Re-engagement Email"**:
  - **Chọn OAuth Credentials** của Gmail.
  - **Điền email chính thức** (để AI gửi email).
- **Node "📊 Update Email Count in Sheet"**:
  - **Chọn cùng OAuth Credentials** của Google Sheets.
  - **Cập nhật cột "Email Count"** trong tab "Database".

##### **🔹 5. Rate Limit & Wait**
- **Node "⏱️ Rate Limit Wait (1 Min)"**:
  - **Đặt thời gian chờ 1 phút** giữa các email (tránh bị Gmail block).

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chọn **1 khách hàng mẫu** và **run test** để kiểm tra email AI viết có hợp lý không.
  - **Kiểm tra email** đã được gửi hay chưa.
- **Bật Active**:
  - Sau khi **cấu hình hoàn chỉnh**, **bật workflow** để chạy hằng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH NÂNG CAO HIỆU QUẢ]
- **Thêm Slack/Telegram Notification**:
  - Sử dụng **node Slack/Telegram** để **báo cáo khi email được gửi thành công**.
- **Lưu Log Email**:
  - **Node "stickyNote"** để lưu **lịch sử email đã gửi** (dễ dàng theo dõi).
- **Gửi Báo Cáo Định Kỳ**:
  - **Node Schedule Trigger** + **Google Sheets** để **tạo báo cáo tháng** về tỷ lệ phản hồi.
- **Tối ưu Template**:
  - **Cập nhật "Follow-up Messages"** thường xuyên để **phù hợp với xu hướng thị trường**.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **viết email hồi phục thủ công**, đồng thời **tăng tỷ lệ phản hồi** nhờ **AI Claude 3.7 Sonnet** viết email **cá nhân hóa 100%**. **Chỉ cần setup 1 lần**, workflow sẽ **chạy tự động hằng ngày**, giúp các sếp **tích cực hơn trong việc hồi phục khách hàng cũ**.

**🚀 Hãy áp dụng ngay và thấy sự khác biệt trong 24 giờ đầu tiên!**
Nếu có vấn đề, **hãy comment bên dưới** hoặc liên hệ với **isaWOW** (tác giả workflow) để hỗ trợ.

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/14217)** | **📌 [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/self-hosting-on-vps/)**