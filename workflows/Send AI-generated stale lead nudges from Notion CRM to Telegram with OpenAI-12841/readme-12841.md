---
title: "🚀 Tự Động Gửi Nhắc Nhở AI Cho Lead Cũ Từ Notion CRM Sang Telegram (Không Cần Code)"
description: "Workflow tự động hóa hàng ngày để phát hiện lead không hoạt động trong Notion CRM, sử dụng OpenAI tạo tin nhắn cá nhân hóa và gửi nhắc nhở trực tiếp cho nhân viên bán hàng qua Telegram. Giúp tăng cường quản lý lead, tiết kiệm thời gian và cải thiện tỷ lệ chuyển đổi."
slug: "tieu-dong-gui-nhac-nho-ai-lead-cu-notion-sang-telegram"
tags: [n8n, automation, no-code, CRM, OpenAI, Telegram, sales, lead-nurturing]
keywords: [tự động hóa n8n, CRM Notion Telegram, AI chatbot bán hàng, lead nurturing tự động, workflow OpenAI, tự động nhắc nhở lead cũ]
---

# 🚀 **Tự Động Gửi Nhắc Nhở AI Cho Lead Cũ Từ Notion CRM Sang Telegram**

## **🔥 Nỗi Đau Của Các Sếp: Lead Cũ Bị Quên Qua, Tỷ Lệ Chuyển Đổi Giảm**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- **Quét thủ công** danh sách lead trong Notion CRM để tìm những lead không hoạt động trong **7-30 ngày**.
- **Gửi email/nhắn tin** nhắc nhở từng nhân viên bán hàng, nhưng **không phải lead nào cũng được nhắc nhở đúng cách** (tone không phù hợp, nội dung lặp lại).
- **Phải nhớ** gửi nhắc nhở hàng ngày, dễ bị quên hoặc không kịp thời.

**Kết quả?** Lead cũ bị bỏ rơi, tỷ lệ chuyển đổi giảm, doanh thu bị ảnh hưởng.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 5-10 giờ/tuần** không phải làm việc thủ công.
✅ **Nhắc nhở lead cũ một cách tự động, cá nhân hóa** (AI tự viết tin nhắn phù hợp với tình trạng lead).
✅ **Gửi nhắc nhở trực tiếp cho nhân viên bán hàng** (không phải spam toàn bộ team).
✅ **Tăng tỷ lệ chuyển đổi** nhờ nhắc nhở kịp thời và nội dung chuyên nghiệp.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
## **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài khoản Notion CRM** (đã sử dụng template [AI Sales Coach](https://probable-banana-3c9.notion.site/AI-Sales-Coach-System-n8n-Companion-v-1-2ee6bbcb3d0b811694b6d5ab51652670?pvs=143)).
📌 **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
📌 **Chat ID Telegram** của nhân viên bán hàng (cần lấy từ [@userinfobot](https://t.me/userinfobot)).
📌 **Tài khoản Telegram Bot** (đăng ký tại [@BotFather](https://t.me/BotFather)).
📌 **Tài khoản n8n Self-hosted** (để workflow chạy 24/7).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/12841](https://n8n.io/workflows/12841) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **📝 Node "CONFIGURATION" (Cấu Hình)**
- **Telegram Chat ID:** Điền **Chat ID** của từng nhân viên bán hàng (dạng số, ví dụ: `-1001234567890`).
- **Persona:** Chọn **tone** cho tin nhắn (ví dụ: *"Chuyên nghiệp"*, *"Thân thiện"*, *"Khuyến khích"*).

#### **📂 Node "Get Agents" & "Get Active Leads" (Lấy Dữ Liệu Notion)**
- **Database Name:** Điền tên **database** trong Notion chứa:
  - **Agents** (danh sách nhân viên bán hàng + Chat ID Telegram).
  - **Active Deals** (danh sách lead hiện tại).
- **API Key:** Điền **Notion Integration Key** (tạo tại [Notion API](https://www.notion.so/my-integrations)).

#### **🗓️ Node "Filter & Map Agents" (Lọc & Gán Nhân Viên)**
- **Days Inactive Threshold:** Đặt số ngày lead được coi là **"cũ"** (ví dụ: `7` ngày).
- **Mapping Rule:** Kiểm tra logic **gán lead cho nhân viên** dựa trên email (cần chỉnh sửa nếu Notion không lưu email).

#### **🤖 Node "AI Coach" (OpenAI)**
- **Model:** Chọn **GPT-3.5-turbo** (mặc định).
- **Prompt Template:** AI sẽ tự động viết tin nhắn dựa trên:
  - **Giá trị lead** (High Value / Cold).
  - **Trạng thái lead** (ví dụ: *"Lead này đã 15 ngày không hoạt động, giá trị 50M"*).
- **API Key:** Điền **OpenAI API Key** (tạo tại [OpenAI](https://platform.openai.com/)).

#### **📢 Node "Send Nudge" (Gửi Telegram)**
- **Bot Token:** Điền **Token** của Telegram Bot (tạo tại [@BotFather](https://t.me/BotFather)).
- **Chat ID:** Sử dụng **Chat ID** từ node **CONFIGURATION**.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run:** Chạy thử với **1 lead mẫu** để kiểm tra:
   - AI có viết tin nhắn phù hợp không?
   - Telegram có gửi được không?
2. **Bật Active:** Sau khi kiểm tra, **bật workflow** để chạy hàng ngày.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
🔹 **Kết hợp với Slack:** Thay vì Telegram, có thể gửi nhắc nhở qua **Slack** (sử dụng node `n8n-nodes-base.slack`).
🔹 **Lưu Log:** Sử dụng node **Sticky Note** để ghi lại **lịch sử nhắc nhở** (dễ theo dõi hiệu quả).
🔹 **Báo Cáo Định Kỳ:** Tạo **báo cáo hàng tuần** về lead cũ và gửi qua **Email** (node `n8n-nodes-base.email`).
🔹 **Tự Động Cập Nhật Notion:** Sau khi nhắc nhở, có thể **cập nhật trạng thái lead** trong Notion (node `n8n-nodes-base.notion` với `update` operation).

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhắc nhở lead cũ thủ công, đồng thời **tăng cường hiệu quả bán hàng** nhờ:
✔ **AI viết tin nhắn cá nhân hóa** (không lặp lại, phù hợp với từng lead).
✔ **Gửi nhắc nhở trực tiếp cho nhân viên** (không spam toàn bộ team).
✔ **Hoạt động tự động hàng ngày** (không cần can thiệp).

**🚀 Hãy áp dụng ngay và xem doanh thu của bạn tăng lên như thế nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Cần hỗ trợ?** Hãy để lại comment bên dưới hoặc liên hệ LogicCraft Automation qua [LinkedIn](https://www.linkedin.com/company/logiccraft-automation/).