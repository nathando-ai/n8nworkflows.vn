---
title: "🚀 **Tự Động Hóa Bảng Xếp Hạng Sales Tối Đa Hiệu Quả Với HighLevel CRM + GPT-4o + Notion + Slack**"
description: "Workflow tự động hóa hoàn toàn không cần code để tạo bảng xếp hạng sales động, phân tích hiệu suất từng nhân viên, gửi thông báo động viên qua Slack và cập nhật dashboard Notion. Giúp doanh nghiệp tiết kiệm 10+ giờ/tháng, tăng tính minh bạch và động viên đội ngũ bán hàng."
slug: "tieu-dong-hoa-bang-xep-hang-sales-highlevel-gpt-4o-notion-slack"
tags: [n8n, automation, no-code, CRM, AI, sales, HighLevel, GPT-4o, Notion, Slack, leaderboard]
keywords: [tự động hóa bảng xếp hạng sales, n8n workflow CRM, tự động hóa hiệu suất bán hàng, GPT-4o động viên nhân viên, dashboard Notion tự động, Slack tự động hóa sales]
---

# 🚀 **Tự Động Hóa Bảng Xếp Hạng Sales Tối Đa Hiệu Quả Với HighLevel + GPT-4o + Notion + Slack**

## **🔥 Nỗi Đau Của Đội Ngũ Sales Hiện Nay**
Các sếp đang phải:
- **Làm thủ công** bảng xếp hạng hàng tuần, mất 5-10 giờ để tổng hợp dữ liệu từ HighLevel CRM.
- **Không có tính minh bạch** vì dữ liệu thường bị "đóng gói" hoặc không được cập nhật kịp thời.
- **Thiếu động viên** vì thông báo hiệu suất thường bị "quên" hoặc không cá nhân hóa.
- **Không có dashboard trực quan** để theo dõi tiến độ từng nhân viên một cách dễ dàng.

**Workflow này giải quyết tất cả!** Với **1 lần cấu hình**, bạn sẽ có:
✅ **Bảng xếp hạng tự động** cập nhật hàng ngày từ HighLevel CRM.
✅ **Dashboard Notion cá nhân hóa** cho từng nhân viên với thống kê chi tiết.
✅ **Thông báo động viên qua Slack** bằng GPT-4o, giúp tăng tinh thần làm việc.
✅ **Lưu log lỗi** trên Google Sheets để kiểm soát chất lượng dữ liệu.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/tháng** cho việc tổng hợp và báo cáo hiệu suất.
- **Tăng tính minh bạch** với bảng xếp hạng tự động và dashboard Notion.
- **Động viên đội ngũ** bằng thông báo cá nhân hóa từ GPT-4o.
- **Cải thiện hiệu suất** với tính năng leaderboard và nhận xét tích cực.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản HighLevel CRM** (để lấy dữ liệu deal).
✔ **API Key HighLevel** (cấu hình trong `highLevelOAuth2Api`).
✔ **Tài khoản Google Sheets** (để lưu log lỗi).
✔ **API Key Google Sheets** (cấu hình trong `googleSheetsOAuth2Api`).
✔ **Tài khoản Notion** (để tạo dashboard cá nhân hóa).
✔ **API Key Notion** (cấu hình trong `notionApi`).
✔ **Tài khoản Slack** (để gửi thông báo động viên).
✔ **API Key Slack** (cấu hình trong `slackApi`).
✔ **API Key Azure OpenAI** (để sử dụng GPT-4o).
✔ **Node LangChain** (để kết nối với AI Agent).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10148](https://n8n.io/workflows/10148) hoặc copy toàn bộ JSON từ canvas.
- **Mở n8n Editor** → Nhấn **"Import"** → Dán JSON và chọn **"Import"**.
- **Kiểm tra cấu trúc** để đảm bảo tất cả nodes được import chính xác.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **11 nodes** quan trọng, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Fetch All Deals from HighLevel CRM**
- **Kiểm tra credentials**: Đảm bảo `highLevelOAuth2Api` đã được cấu hình với **API Key** và **URL HighLevel**.
- **Test API**: Chạy node này để xác nhận dữ liệu deal được lấy đầy đủ.

##### **🔹 Node 3: Validate Deal Fetch Success (IF Node)**
- **Cấu hình điều kiện**: Kiểm tra `deal_id` không rỗng (`$json.deal_id !== null`).
- **Nếu lỗi**: Dữ liệu sẽ được log vào Google Sheets (node 4).

##### **🔹 Node 4: Log Fetch or Validation Errors (Google Sheets)**
- **Chọn Sheet**: Đảm bảo đã tạo một sheet mới để lưu log lỗi.
- **Cấu hình header**: Cột `error_id` và `error` phải khớp với dữ liệu từ HighLevel.

##### **🔹 Node 5 & 6: Clean & Structure Deal Data + Summarize Sales by Representative**
- **Code Node**: Các sếp **không cần chỉnh sửa** trừ khi dữ liệu HighLevel thay đổi.
- **Kiểm tra output**: Sau khi chạy, đảm bảo dữ liệu được nhóm theo `rep_id` và tính toán chính xác.

##### **🔹 Node 7: Generate Notion Performance Dashboard**
- **Tạo Page Template**: Notion sẽ tự động tạo page với tiêu đề `{rep_id} - Sales Rep Performance Tracker`.
- **Kiểm tra quyền API**: Đảm bảo `notionApi` có quyền viết vào workspace Notion.

##### **🔹 Node 8 & 9: Transform Data for AI Input + GPT-4o Model Configuration**
- **Cấu hình GPT-4o**:
  - **Model**: Chọn `gpt-4o` trong `azureOpenAiApi`.
  - **System Role**: Đảm bảo prompt động viên là **nhân viên, ngắn gọn và tích cực**.
  - **Test Prompt**: Gửi một request mẫu để kiểm tra output của AI.

##### **🔹 Node 10: AI-Generated Motivational Slack Messages**
- **LangChain Agent**: Đảm bảo node này được kết nối với `lmChatAzureOpenAi`.
- **Kiểm tra output**: Slack message phải có **emoji** và **cá nhân hóa** (ví dụ: `@user, bạn đã đóng gói thành công 5 deal mới! 🎯`).

##### **🔹 Node 11: Notify Sales Team in Slack**
- **Chọn Channel**: Gửi đến **#sales-leaderboard** hoặc DM cá nhân.
- **Test Send**: Gửi một message mẫu để đảm bảo Slack API hoạt động.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy workflow với **dữ liệu mẫu** để kiểm tra toàn bộ flow.
- **Bật Active**: Sau khi kiểm tra xong, **bật workflow** để hoạt động tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH LÀM NÀY ĐỂ TIẾP CẬN HƠN**]
- **Thêm Log vào Google Sheets**: Lưu lịch sử hoạt động của workflow để theo dõi hiệu suất.
- **Gửi báo cáo định kỳ**: Sử dụng **n8n Trigger** (n8n-nodes-base.schedule) để chạy workflow hàng ngày/lần tuần.
- **Kết hợp với Email**: Gửi báo cáo Notion qua email bằng **n8n-nodes-base.email**.
- **Thêm Dashboard Power BI**: Xuất dữ liệu từ Notion sang Power BI để phân tích sâu hơn.
- **Tự động cập nhật Slack Bot**: Sử dụng **n8n-nodes-base.slackApp** để tạo bot cá nhân hóa.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi công việc thủ công, đồng thời **tăng động viên và minh bạch** trong đội ngũ sales. **Chỉ cần 1 lần cấu hình**, bạn sẽ có một hệ thống tự động hóa **mạnh mẽ, thông minh và hiệu quả**!

**👉 Hãy import ngay và bắt đầu tự động hóa bảng xếp hạng sales của mình!**

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý cuối cùng**: Nếu gặp vấn đề, các sếp có thể tham khảo [cộng đồng n8n Việt Nam](https://community.n8n.io/) hoặc liên hệ tác giả [Rahul Joshi](https://n8n.io/workflows/10148) để hỗ trợ!