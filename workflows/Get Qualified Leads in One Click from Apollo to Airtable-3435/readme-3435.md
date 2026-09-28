---
title: "🚀 Tự Động Lọc & Lưu Lead Chất Lượng Từ Apollo Vào Airtable Chỉ Với 1 Click"
description: "Hướng dẫn cài đặt workflow n8n giúp scrape dữ liệu khách hàng tiềm năng từ Apollo.io, tự động lọc email và lưu trữ trực tiếp vào Airtable cực kỳ nhanh chóng."
slug: "tu-dong-loc-va-luu-lead-tu-apollo-vao-airtable-bang-n8n"
tags: [n8n, automation, sales, lead-generation, apollo, airtable, no-code]
keywords: [n8n workflow, tự động hóa sales, lấy lead từ apollo, lưu lead vào airtable, scrape leads apollo]
---

# 🚀 Tự Động Lọc & Lưu Lead Chất Lượng Từ Apollo Vào Airtable Chỉ Với 1 Click

Các sếp trong ngành sales và marketing chắc chắn hiểu cảm giác mệt mỏi thế nào khi phải ngồi tìm kiếm thủ công từng khách hàng tiềm năng trên Apollo.io, copy/paste thông tin rồi lọc xem ai có email, ai không để đưa vào CRM. Quá trình này ngốn hàng giờ đồng hồ mỗi ngày mà lại dễ sai sót.

Đừng lo, giải pháp ở đây rồi! Với workflow n8n siêu việt này từ **Not Another Marketer**, các sếp có thể tự động hóa toàn bộ quy trình: thu thập hàng ngàn lead đã được làm giàu (enriched leads), lọc bỏ những contact không có email, và lưu gọn gàng vào Airtable chỉ bằng một cú click chuột. 100% tự động, không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh copy/paste thủ công từng dòng dữ liệu từ Apollo sang bảng tính.
- **Dữ liệu sạch sẽ, chất lượng:** Tự động lọc bỏ các lead "rác" không có email, đảm bảo đội ngũ sales chỉ tiếp cận những contact có thể liên lạc được.
- **Đồng bộ thời gian thực:** Thông tin khách hàng tiềm năng được đẩy thẳng vào Airtable, sẵn sàng cho các chiến dịch Outreach tiếp theo.
- **Hoạt động linh hoạt:** Dễ dàng tùy biến tiêu chí tìm kiếm lead theo nhu cầu thực tế của doanh nghiệp.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
2. **Tài khoản Apollo.io** kèm theo API Key hoặc cấu hình kết nối tương ứng để tiến hành scrape dữ liệu.
3. **Tài khoản Airtable** cùng một Base/Table đã được tạo sẵn để lưu trữ thông tin lead.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy toàn bộ mã JSON từ template gốc.
- Mở n8n Editor của các sếp, chọn **Add workflow** -> **Import from File / Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính được thiết kế tối ưu, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **When clicking ‘Test workflow’ (`manualTrigger`):** Node kích hoạt thủ công để kiểm tra. Các sếp có thể thay thế bằng *Webhook* hoặc *Schedule Trigger* nếu muốn chạy tự động định kỳ.
- **Edit Fields (`set`):** Nơi các sếp cấu hình các tham số đầu vào cho chiến dịch tìm kiếm lead (như chức danh, ngành nghề, địa điểm, quy mô công ty...) phù hợp với chân dung khách hàng (ICP) của mình.
- **Scrape Leads (`httpRequest`):** Node cốt lõi thực hiện gọi API tới Apollo để lấy dữ liệu. Các sếp cần điền Apollo API Key hoặc cấu hình header xác thực chính xác tại đây.
- **Filter leads without email (`if`):** Node logic dùng để sàng lọc. Hệ thống sẽ kiểm tra xem trường email có tồn tại hay không. Chỉ những lead có email mới được đi tiếp.
- **Save Leads in database (`airtable`):** Node kết nối tới cơ sở dữ liệu. Các sếp cần chọn **Credentials** (Airtable API Key / Personal Access Token), sau đó map chính xác các trường dữ liệu từ Apollo (Tên, Email, Công ty, Chức vụ...) vào các cột tương ứng trong bảng Airtable của mình.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử với một vài dữ liệu mẫu và kiểm tra kết quả trong Airtable.
- Sau khi thấy dữ liệu đổ về mượt mà, hãy gạt công tắc sang **Active** để bật chế độ tự động chạy chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình sales hơn nữa, các sếp có thể mở rộng workflow này với các ý tưởng:
- **Tích hợp Slack / Telegram:** Gửi thông báo ngay vào nhóm chat của team sales mỗi khi có một batch lead mới được cào và lưu thành công vào Airtable.
- **Kết nối AI (OpenAI / Claude):** Thêm một node AI để tự động viết email giới thiệu (cold email) cá nhân hóa dựa trên thông tin chức vụ và công ty của lead vừa lấy được.
- **Gửi Email tự động:** Kết nối tiếp với Gmail hoặc các công cụ gửi email hàng loạt để outreach ngay lập tức.

### 📌 Kết luận
Việc tìm kiếm và làm giàu dữ liệu khách hàng chưa bao giờ dễ dàng đến thế với sức mạnh của tự động hóa n8n. Hãy áp dụng ngay workflow này để giải phóng thời gian cho đội ngũ sales và tăng tốc doanh số ngay hôm nay các sếp nhé!