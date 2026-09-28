---
title: "💰 Tự Động Hóa Khớp Lại Giao Dịch Ngân Hàng & Tạo Báo Cáo Tự Động Với GPT-4 & Gmail (N8n)"
description: "Workflow này tự động khớp lại giao dịch ngân hàng, phân loại chi tiêu, phát hiện lỗi, và tạo báo cáo tài chính chi tiết bằng GPT-4, giúp tiết kiệm **90% thời gian** so với thủ công. Kết quả được gửi tự động qua email hàng ngày hoặc hàng tháng."
slug: "tieu-dong-hoa-khop-lai-giao-dich-ngan-hang-voi-gpt-4-gmail"
tags: [n8n, automation, ai, gpt-4, tài chính, báo cáo tự động, no-code]
keywords: [tự động hóa khớp lại giao dịch ngân hàng, n8n workflow tài chính, GPT-4 phân loại giao dịch, báo cáo tài chính tự động, giảm thời gian khớp lại giao dịch]
---

# 🚀 **Tự Động Hóa Khớp Lại Giao Dịch Ngân Hàng & Tạo Báo Cáo Tự Động Với GPT-4 & Gmail**

Hiện nay, việc khớp lại giao dịch ngân hàng thủ công không chỉ tốn thời gian mà còn dễ mắc lỗi, đặc biệt khi doanh nghiệp có lượng giao dịch lớn. Các sếp phải dành hàng giờ mỗi tháng để so sánh dữ liệu giữa ngân hàng và hệ thống kế toán, phân loại giao dịch, phát hiện sai sót, và tạo báo cáo cho ban lãnh đạo. **Workflow này giải quyết tất cả những vấn đề đó bằng AI + tự động hóa 100% không cần code!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo an toàn và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với khớp lại giao dịch thủ công.
- **Phân loại giao dịch tự động** bằng GPT-4, giảm sai sót trong phân loại chi tiêu.
- **Phát hiện lỗi và gian lận** bằng AI, cảnh báo ngay khi có giao dịch bất thường.
- **Tạo báo cáo tài chính chuyên nghiệp** với định dạng email tự động.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** với quyền truy cập **GPT-4o** (hoặc GPT-4).
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
3. **Tài khoản Gmail** (để gửi báo cáo tự động).
4. **Credentials OAuth 2.0 cho Gmail** (cấu hình trong n8n).
5. **API của ngân hàng** (hoặc mock API như Fable Bank trong ví dụ này).
6. **Hệ thống kế toán** (nếu cần khớp lại với dữ liệu nội bộ).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/12377](https://n8n.io/workflows/12377) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/12377) và dán vào **Create Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **31 node** và được cấu trúc theo **6 bước chính**:
1. **Lấy dữ liệu giao dịch từ ngân hàng** (API HTTP Request).
2. **Lấy dữ liệu kế toán nội bộ** (API HTTP Request).
3. **Gộp và phân tích dữ liệu** (Merge + AI Agents).
4. **Phân loại giao dịch, khớp lại, phát hiện lỗi** (bằng GPT-4).
5. **Tạo sổ cái và báo cáo** (Journal Entry + Financial Reports).
6. **Gửi báo cáo qua email** (Gmail).

##### **🔹 Node quan trọng cần cấu hình:**
| **Node** | **Lưu ý cấu hình** | **Tham số cần điền** |
|----------|---------------------|----------------------|
| **Daily Accounting Run** | Cấu hình **schedule trigger** để chạy hàng ngày/ngày cuối tháng. | `Cron expression` (ví dụ: `0 0 1 * *` để chạy ngày 1 hàng tháng). |
| **Fetch Bank Transactions** | Thay đổi URL API của ngân hàng (không còn là Fable Bank). | `URL`, `Headers`, `API Key`. |
| **Fetch Accounting System Data** | Nếu sử dụng hệ thống kế toán nội bộ. | `URL`, `Credentials`. |
| **OpenAI GPT-4** | Đảm bảo chọn **GPT-4o** (hoặc GPT-4). | `openAiApi` (credentials đã cấu hình). |
| **Gmail Tool** | Cấu hình **OAuth 2.0** cho Gmail. | `gmailOAuth2` (credentials). |
| **Send Summary Email** | Chỉ định **người nhận** và **định dạng email**. | `To`, `Subject`, `HTML Body`. |

##### **🔹 Cấu hình AI Agents (6 Agent chính):**
Workflow sử dụng **6 AI Agent** để xử lý logic phức tạp:
1. **Transaction Classifier Agent** → Phân loại giao dịch (chi tiêu, thu nhập, lỗi).
2. **Account Reconciliation Agent** → Khớp lại giao dịch với hệ thống kế toán.
3. **Journal Entry Generator Agent** → Tạo sổ cái tự động.
4. **Error Detection Agent** → Phát hiện giao dịch sai sót.
5. **Financial Statement Generator Agent** → Tạo báo cáo tài chính.
6. **Tax Report Generator Agent** → Tạo báo cáo thuế tự động.

**Lưu ý:**
- Các **Schema** (`Transaction Classification Schema`, `Reconciliation Schema`,...) được định nghĩa sẵn. Các sếp **không cần chỉnh sửa** trừ khi cần thay đổi logic phân loại.
- **Calculator Tool** được sử dụng để tính toán số liệu tự động (ví dụ: tổng chi tiêu theo loại).

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu từ ngân hàng.
2. **Bật Active** workflow.
3. **Kiểm tra email** để xác nhận báo cáo được gửi đúng.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram** để cảnh báo lỗi ngay khi phát hiện.
   ```json
   // Thêm node `webhook` hoặc `slack` sau `Error Detection Agent`.
   ```
2. **Lưu log vào Google Sheets/Notion** để theo dõi lịch sử.
   ```json
   // Thêm node `googleSheets` sau `Aggregate All Results`.
   ```
3. **Tự động gửi báo cáo định kỳ** (hàng tuần/tháng) bằng **Schedule Trigger**.
4. **Cập nhật API ngân hàng mới** nếu chuyển sang ngân hàng khác.
5. **Optimize cost OpenAI** bằng cách sử dụng **GPT-4o** (rẻ hơn GPT-4).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc khớp lại giao dịch thủ công, đồng thời **tăng độ chính xác** nhờ AI. **Chỉ cần cấu hình 1 lần**, workflow sẽ hoạt động tự động hàng ngày/mỗi tháng, gửi báo cáo chuyên nghiệp qua email.

**🚀 Hãy áp dụng ngay để tiết kiệm thời gian và giảm sai sót!**
Nếu cần hỗ trợ, liên hệ tác giả:
📧 **mcschin1@yahoo.com** (Dr. Cheng Siong CHIN - Chuyên gia tự động hóa AI).

---
**🔹 Bạn có thể tùy chỉnh workflow này để phù hợp với:**
✅ Ngân hàng Việt Nam (Vietcombank, Techcombank, VPBank...)
✅ Hệ thống kế toán nội bộ (SAP, QuickBooks, ERP...)
✅ Báo cáo thuế tự động (Bộ Tài chính)