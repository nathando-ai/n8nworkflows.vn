---
title: "🚀 Tự động trích xuất dữ liệu tương tác bài viết LinkedIn với Airtop và n8n"
description: "Hướng dẫn cài đặt workflow n8n sử dụng Airtop AI để tự động lấy danh sách người tương tác, bình luận và số liệu thống kê từ bài viết LinkedIn một cách nhanh chóng."
slug: "trich-xuat-du-lieu-tuong-tac-linkedin-airtop"
tags: [n8n, automation, linkedin, airtop, marketing, lead-generation]
keywords: [n8n workflow, trích xuất dữ liệu linkedin, airtop ai, tự động hóa marketing, lấy danh sách comment linkedin]
---

# 🚀 Tự động trích xuất dữ liệu tương tác bài viết LinkedIn với Airtop

Các sếp làm Marketing, Sales hay Nghiên cứu thị trường có bao giờ thấy nản khi phải ngồi thủ công copy danh sách hàng trăm người đã like, comment, share trên một bài viết LinkedIn hot để làm Lead Generation chưa? Việc này vừa tốn thời gian, dễ bỏ sót lại cực kỳ nhàm chán.

Giải pháp đây rồi! Workflow n8n tích hợp **Airtop AI** này sẽ giúp các sếp tự động hóa 100% quy trình: chỉ cần ném đường link bài viết LinkedIn vào, AI sẽ tự động "đọc" trang, gom toàn bộ số liệu tương tác và xuất ra danh sách chi tiết thông tin người dùng (Họ tên, Chức vụ, Link Profile) gọn gàng dưới dạng JSON. Không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Thu thập data chất lượng:** Tự động lấy danh sách đầy đủ tên, chức vụ và link profile của những người đã tương tác (bình luận, thả cảm xúc) để làm nguồn Data chạy chiến dịch outbound.
- **Thống kê số liệu trực quan:** Nắm bắt ngay lập tức tổng số lượng reactions, comments, và reposts của bài viết.
- **Tiết kiệm 95% thời gian:** Thay vì mất hàng giờ copy/paste thủ công, AI xử lý mọi thứ chỉ trong vài giây.
- **Linh hoạt kích hoạt:** Có thể chạy thủ công qua Form n8n hoặc gọi tự động từ một workflow khác qua Sub-workflow.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Airtop**: Nền tảng tự động hóa trình duyệt bằng AI (`portal.airtop.ai`) với một Airtop Profile đã đăng nhập sẵn tài khoản LinkedIn.
- **API Key/Credentials** tương ứng từ Airtop để kết nối vào n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow và paste trực tiếp vào màn hình n8n Editor của mình, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 5 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **On form submission / When Executed by Another Workflow**: Điểm khởi đầu của luồng. Nếu chạy độc lập, hãy dùng Form Trigger để tạo giao diện nhập URL bài viết. Nếu gọi từ luồng khác, giữ nguyên Execute Workflow Trigger.
- **Map fields (Set node)**: Nơi nhận các tham số đầu vào quan trọng:
  - `linkedin_post_url`: Đường dẫn đầy đủ của bài viết LinkedIn cần phân tích.
  - `airtop_profile`: Tên Airtop Profile đã đăng nhập sẵn LinkedIn của các sếp.
- **Airtop (Extraction node)**: Node cốt lõi sử dụng AI để phân tích trang. 
  - *Operation*: `query` / *Resource*: `extraction`.
  - *Prompt*: AI đã được cấu hình sẵn để quét bài viết, tìm kiếm thông tin người comment/react (Tên, Chức vụ, Profile URL) và đếm tổng số lượng tương tác. Các sếp có thể tinh chỉnh lại prompt nếu muốn lấy thêm thông tin khác.
- **Parse engagement analysis response (Code node)**: Xử lý dữ liệu trả về từ Airtop thành cấu trúc JSON sạch sẽ, sẵn sàng cho các bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với một đường link bài viết LinkedIn cụ thể để kiểm tra kết quả đầu ra (Interactors list, reactions_count, comments_count, reposts_count).
- Bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình làm việc, các sếp có thể mở rộng workflow này bằng cách:
1. **Đẩy data vào Google Sheets / Airtable**: Thêm node Google Sheets để tự động lưu danh sách lead vừa quét được vào file quản lý khách hàng tiềm năng.
2. **Gửi thông báo qua Telegram / Slack**: Báo cáo ngay số liệu tương tác và danh sách lead nóng về group chat nội bộ ngay khi quét xong.
3. **Kết hợp Automation Outreach**: Sau khi có Profile URL, tự động đưa vào chu trình kết bạn hoặc gửi tin nhắn chăm sóc (nếu sử dụng công cụ phù hợp).

### 📌 Kết luận
Việc khai thác dữ liệu từ LinkedIn chưa bao giờ dễ dàng đến thế nhờ sự kết hợp giữa n8n và Airtop AI. Hãy áp dụng ngay workflow này để tối ưu hóa hiệu quả các chiến dịch Marketing và Sales của doanh nghiệp các sếp nhé!