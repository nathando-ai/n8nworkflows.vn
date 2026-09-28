---
title: "🚀 Tự động tra cứu thông tin cá nhân qua Email với Clearbit trong n8n"
description: "Hướng dẫn tích hợp Clearbit và n8n để tự động hóa việc tra cứu thông tin khách hàng, nhân sự hoặc đối tác chỉ bằng một địa chỉ email, giúp tiết kiệm thời gian nghiên cứu thủ công."
slug: "tra-cuu-thong-tin-ca-nhan-qua-email-clearbit-n8n"
tags: [n8n, automation, no-code, clearbit, sales, enrichment]
keywords: [n8n workflow, clearbit integration, tra cứu email, data enrichment, tự động hóa sales]
keywords: [n8n workflow, clearbit integration, tra cứu email, data enrichment, tự động hóa sales]
---

# 🚀 Tự động tra cứu thông tin cá nhân qua Email với Clearbit trong n8n

Các sếp trong ngành Sales, Marketing hay Support có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ tra cứu thông tin thủ công của khách hàng (chức vụ, công ty, mạng xã hội, quy mô doanh nghiệp...) từ một địa chỉ email lẻ loi? Việc này không chỉ làm giảm năng suất mà còn bỏ lỡ cơ hội tiếp cận khách hàng tiềm năng một cách nhanh chóng.

Đừng lo, bài toán này sẽ được giải quyết gọn gàng với workflow n8n cực kỳ đơn giản nhưng cực kỳ mạnh mẽ này. Workflow giúp tự động hóa 100% quá trình lấy thông tin chi tiết của một cá nhân từ Clearbit chỉ với vài cú click chuột!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Thay vì phải search Google hay LinkedIn từng người, hệ thống sẽ trả về toàn bộ thông tin chỉ trong tích tắc.
- **Làm giàu dữ liệu (Data Enrichment):** Tự động thu thập các thông tin quý giá như tên đầy đủ, vị trí công việc, công ty hiện tại, tài khoản mạng xã hội (Twitter, LinkedIn, GitHub...).
- **Nâng cao tỷ lệ chốt đơn:** Giúp đội ngũ Sales có ngay thông tin chi tiết về khách hàng trước khi gọi điện hoặc gửi email pitch.
- **Hoạt động linh hoạt:** Dễ dàng kết hợp với các workflow khác như Google Sheets, HubSpot, Slack hoặc CRM nội bộ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Clearbit Account:** Tài khoản Clearbit để lấy API Key (Clearbit API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow từ n8n hoặc copy đoạn mã JSON tương ứng.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (ba chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 2 nodes chính rất dễ cấu hình:

- **Node `On clicking 'execute'` (manualTrigger):** 
  - Đây là node kích hoạt thủ công để các sếp test workflow. Khi đưa vào sử dụng thực tế, các sếp có thể thay thế node này bằng **Webhook**, **Google Sheets Trigger**, **Typeform** hoặc **Schedule Trigger** tùy theo nhu cầu.
- **Node `Clearbit`:**
  - **Resource:** Giữ nguyên là `person` (để tra cứu thông tin cá nhân).
  - **Email:** Nhập địa chỉ email của người cần tra cứu (hoặc map dynamic từ node kích hoạt phía trước).
  - **Credentials:** Tạo mới một `clearbitApi` credential bằng cách nhập API Key lấy từ tài khoản Clearbit của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử với một email mẫu (ví dụ: `alex@example.com` hoặc email cá nhân/đồng nghiệp).
- Kiểm tra kết quả trả về ở bảng Output xem thông tin đã hiển thị đầy đủ chưa.
- Sau khi test thành công, nếu dùng dạng thủ công thì không cần bật Active, nhưng nếu đổi sang Webhook/Schedule thì hãy bật **Active** cho workflow chạy tự động nhé!

### ✍️ Mẹo & gợi ý nâng cao
Để workflow này trở thành một "vũ khí" thực thụ, các sếp có thể mở rộng thêm:
1. **Tích hợp Google Sheets / Airtable:** Tự động ghi lại thông tin tra cứu được vào bảng quản lý khách hàng tiềm năng (Lead Management).
2. **Bắn thông báo qua Slack/Telegram:** Ngay khi có khách hàng mới đăng ký bằng email doanh nghiệp, bot sẽ tự động gửi thông báo chi tiết về vị trí và công ty của họ lên group chat sales.
3. **Kết hợp AI (OpenAI/Claude):** Dùng AI để phân tích thông tin trả về từ Clearbit và tự động soạn một email giới thiệu (cold email) cá nhân hóa siêu đỉnh.

### 📌 Kết luận
Workflow tra cứu thông tin qua Clearbit là bước đầu tiên cực kỳ quan trọng để tự động hóa quy trình thu thập dữ liệu khách hàng. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa năng suất đội ngũ Sales và Marketing ngay hôm nay!