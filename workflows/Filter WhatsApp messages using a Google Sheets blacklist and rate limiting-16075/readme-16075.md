---
title: "🚀 Lọc tin nhắn WhatsApp thông minh bằng Google Sheets Blacklist và Rate Limiting trong n8n"
description: "Hướng dẫn xây dựng hệ thống bảo vệ trợ lý AI WhatsApp tự động chặn spam, tin nhắn rác từ danh sách đen Google Sheets và giới hạn tần suất gửi tin (Rate Limit)."
slug: "loc-tin-nhan-whatsapp-google-sheets-blacklist-rate-limiting"
tags: [n8n, automation, whatsapp, google-sheets, security, ai-agents]
keywords: [n8n workflow, lọc tin nhắn whatsapp, google sheets blacklist, rate limiting n8n, chống spam whatsapp ai]
---

# 🚀 Lọc tin nhắn WhatsApp thông minh bằng Google Sheets Blacklist và Rate Limiting

Khi triển khai các trợ lý AI hoặc hệ thống CSKH tự động trên WhatsApp, nỗi đau lớn nhất của các doanh nghiệp là đối mặt với tình trạng **spam tin nhắn rác**, các đối tượng xấu cố tình tấn công API, hoặc người dùng gửi quá nhiều tin nhắn liên tục làm quá tải hệ thống AI (tốn kém chi phí token và làm chậm hệ thống).

Workflow này ra đời như một giải pháp tự động hóa 100% không cần code, giúp chặn đứng tin nhắn từ các số điện thoại nằm trong danh sách đen (Blacklist) lưu trữ tại Google Sheets và áp dụng cơ chế giới hạn tần suất (Rate Limiting) trước khi tin nhắn kịp chạm tới các node xử lý AI.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo vệ hệ thống AI:** Ngăn chặn tuyệt đối các cuộc tấn công spam hoặc dữ liệu rác làm lãng phí token LLM.
- **Tự động hóa quản lý Blacklist:** Dễ dàng thêm/xóa số điện thoại bị chặn trực tiếp qua Google Sheets mà không cần sửa code workflow.
- **Kiểm soát lưu lượng thông minh:** Cơ chế Rate Limiting tự động giới hạn số lượng tin nhắn tối đa trong khoảng thời gian nhất định (ví dụ: tối đa 30 tin nhắn/phút).
- **Vận hành liên tục 24/7:** Hoạt động bền bỉ, ghi nhận và tách luồng rõ ràng cho các trường hợp hợp lệ và bị chặn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động.
- Tài khoản **Google Sheets** đã chuẩn bị sẵn một bảng dữ liệu (Sheet) làm Blacklist (với các cột cơ bản như `phone`, `reason`).
- Credentials kết nối **Google Sheets OAuth2 API** trong n8n.
- Triggers nguồn nhận tin nhắn WhatsApp (có thể thay thế node test thủ công bằng webhook WhatsApp Cloud API chính thức).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Sao chép mã JSON của workflow từ nguồn hoặc tải tệp JSON, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp bằng cách chọn **New workflow** -> ấn `Ctrl + V` (hoặc `Cmd + V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru với môi trường thực tế, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Google Sheets — Fetch Blacklist**: Chọn đúng tài khoản credentials Google Sheets OAuth2 API của các sếp, sau đó trỏ chính xác đến file Google Sheets chứa danh sách đen và tên Sheet (Tab) tương ứng (`phone`, `reason`).
- **Set — Max messages per minute**: Node này định nghĩa ngưỡng giới hạn tần suất (mặc định là 30 tin nhắn/phút). Các sếp có thể điều chỉnh tham số `limitThreshold` cho phù hợp với tải hệ thống thực tế.
- **Code — Rate Limiter Engine**: Node JavaScript tùy chỉnh để theo dõi nhịp độ tin nhắn. Nếu muốn đổi cửa sổ thời gian (window size), các sếp có thể tinh chỉnh giá trị `60000` (miligiây) bên trong code.
- **Manual Trigger — Test Execution / Set — Mock WhatsApp Input**: Khi đưa vào sản xuất (Production), các sếp nhớ thay thế các node giả lập đầu vào thủ công này bằng webhook nhận tin nhắn thực tế từ WhatsApp API (Meta Cloud API, Baileys, hoặc Evolution API).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** với dữ liệu mẫu (Mock Data) để kiểm tra luồng chạy qua các nhánh `If — is Blocked?` và `If — Rate Limit Exceeded?`.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên cùng bên phải để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Auto-Response:** Thay thế các node `NoOp` (No Operation) ở nhánh bị chặn bằng các node gửi tin nhắn WhatsApp tự động phản hồi lại người dùng (Ví dụ: *"Số điện thoại của bạn đã bị hạn chế"* hoặc *"Bạn gửi quá nhanh, vui lòng thử lại sau 1 phút"*).
- **Lưu Audit Log:** Kết nối các nhánh bị chặn vào một bảng Google Sheets phụ hoặc cơ sở dữ liệu (như PostgreSQL, Supabase) để theo dõi các hành vi cố tình spam hoặc quét hệ thống (scraping).
- **Cảnh báo đội ngũ quản trị:** Thêm node Slack hoặc Telegram để gửi thông báo tức thì về kênh nội bộ khi phát hiện một số điện thoại kích hoạt cơ chế bảo mật liên tục.

### 📌 Kết luận
Workflow lọc tin nhắn WhatsApp kết hợp Google Sheets Blacklist và Rate Limiting là lớp khiên bảo vệ cực kỳ quan trọng cho bất kỳ hệ thống AI Automation nào trong thời đại số. Hãy import ngay vào n8n của các sếp để tối ưu hóa tài nguyên và giữ cho trợ lý AI luôn hoạt động an toàn, hiệu quả!