---
title: "🚀 Tự động gửi báo cáo chi phí và Token AI hàng tuần qua Gmail với Alephant & n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động tổng hợp chi phí và mức tiêu thụ token AI từ Alephant AI Gateway, sau đó gửi báo cáo qua Gmail mỗi thứ Hai hàng tuần."
slug: "tu-dong-bao-cao-chi-phi-ai-weekly-voi-alephant-va-gmail"
tags: [n8n, automation, ai-gateway, alephant, gmail, cost-control]
keywords: [n8n workflow, alephant ai, quan ly chi phi ai, token usage report, tu dong hoa gmail]
---

# 🚀 Tự động gửi báo cáo chi phí và Token AI hàng tuần qua Gmail với Alephant & n8n

Các sếp có đang triển khai các ứng dụng AI agents, LLM trong doanh nghiệp và đôi khi "giật mình" khi nhận hóa đơn thanh toán API cuối tháng không? Việc kiểm soát chi phí gọi AI model (OpenAI, Anthropic, v.v.) thủ công là cực kỳ khó khăn, đặc biệt khi các agent chạy ngầm liên tục. 

Giải pháp cho các sếp đây: Workflow n8n tự động hóa 100% này sẽ kết nối với **Alephant AI Gateway** để thống kê chi phí, lượng token tiêu thụ và gửi bảng báo cáo chi tiết qua **Gmail** vào mỗi sáng thứ Hai hàng tuần. Không cần code, thiết lập nhanh gọn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Kiểm soát chi phí chặt chẽ:** Nắm bắt chính xác chi phí AI theo tuần mà không cần truy cập dashboard thủ công.
- **Minh bạch hóa hoạt động:** Theo dõi sát sao lượng token tiêu thụ của từng agent, tránh tình trạng đội vốn bất ngờ.
- **Tự động hóa hoàn toàn:** Chạy ngầm định kỳ hàng tuần, gửi thẳng báo cáo đến hòm thư của quản lý hoặc đội ngũ kỹ thuật.
- **Phát hiện sớm bất thường:** Kịp thời điều chỉnh khi có agent tiêu thụ tài nguyên quá mức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Alephant Account:** Tài khoản Alephant (có gói Free-tier) để quản lý AI Gateway.
- **Gmail Account:** Tài khoản Gmail đã kết nối OAuth2 với n8n để gửi email.
- **Alephant Community Node:** Cài đặt node `@alephantai/n8n-nodes-alephant-analytics` vào n8n của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow hoặc import file trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Weekly Monday Trigger (`scheduleTrigger`):** Mặc định lịch chạy là 9 giờ sáng thứ Hai hàng tuần. Các sếp có thể điều chỉnh lại thời gian (chạy theo ngày hoặc giờ) nếu muốn kiểm tra thường xuyên hơn.
- **Fetch Alephant Usage Summary (`@alephantai/n8n-nodes-alephant-analytics.alephantUsage`):** 
  - Cần tạo và kết nối **Alephant Virtual Key API** credentials.
  - Lấy API Key từ trang quản trị của Alephant và dán vào n8n.
- **Set Email Recipient (`set`):** 
  - Mở node này và cấu hình địa chỉ email nhận báo cáo của các sếp hoặc đội ngũ quản lý.
- **Format Usage Report (`code`):** Node này dùng đoạn mã JS để làm sạch và định dạng dữ liệu từ Alephant thành một bản báo cáo đẹp mắt, sẵn sàng đưa vào email.
- **Send Usage Summary Email (`gmail`):** 
  - Chọn **Gmail OAuth2** credentials để xác thực tài khoản gửi email.
  - Đảm bảo quyền gửi email đã được cấp phép cho n8n.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để chạy thử xem email có được gửi đi chính xác hay không.
- Sau khi kiểm tra mọi thứ hoàn tất, gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Slack/Telegram:** Ngoài Gmail, các sếp có thể nhân bản nhánh cuối để gửi thông báo chi phí nhanh vào nhóm chat nội bộ của team dev.
- **Cảnh báo ngân sách (Budget Alert):** Kết hợp thêm điều kiện (If node), nếu chi phí vượt ngưỡng cho phép trong tuần, hệ thống sẽ bắn tin nhắn khẩn cấp ngay lập tức.
- **Lưu trữ lịch sử:** Lưu dữ liệu trả về từ Alephant vào Google Sheets hoặc Airtable để vẽ biểu đồ tăng trưởng chi phí AI theo tháng/quý.

### 📌 Kết luận
Việc kiểm soát chi phí vận hành AI giờ đây đã trở nên đơn giản hơn bao giờ hết với sự kết hợp giữa Alephant AI Gateway và n8n. Hãy "lên đồ" ngay workflow này để tối ưu hóa ngân sách công nghệ cho doanh nghiệp các sếp nhé!