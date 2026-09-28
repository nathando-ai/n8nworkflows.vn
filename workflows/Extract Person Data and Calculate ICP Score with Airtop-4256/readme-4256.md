---
title: "🚀 Tự động trích xuất thông tin LinkedIn và chấm điểm ICP với Airtop trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình enrich dữ liệu cá nhân từ LinkedIn và tính điểm ICP (Ideal Customer Profile) bằng Airtop API mà không cần code."
slug: "tu-dong-trich-xuat-linkedin-va-cham-diem-icp-voi-airtop"
tags: [n8n, automation, airtop, lead-generation, icp-scoring, linkedin]
keywords: [n8n workflow, trích xuất dữ liệu linkedin, chấm điểm icp, airtop api, tự động hóa sales]
---

# 🚀 Tự động trích xuất thông tin LinkedIn và chấm điểm ICP với Airtop

Các sếp trong ngành Sales và Marketing chắc chắn đã quá quen thuộc với nỗi đau: Mỗi khi có một Lead (khách hàng tiềm năng) mới đăng ký, đội ngũ phải tốn hàng giờ đồng hồ lên LinkedIn thủ công để tìm kiếm profile, kiểm tra xem họ làm công ty nào, chức vụ gì, và đánh giá xem họ có "khớp" với chân dung khách hàng lý tưởng (ICP) hay không. Quy trình này vừa chậm chạp, vừa dễ sai sót, lại tốn rất nhiều nhân lực.

Giải pháp là gì? Workflow n8n này sẽ tự động hóa **100%** quy trình đó! Kết hợp sức mạnh của n8n và **Airtop Browser Automation API**, hệ thống sẽ tự động lọc email doanh nghiệp, tìm kiếm LinkedIn, trích xuất toàn bộ thông tin chuyên sâu và tính điểm ICP ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải tra cứu thủ công từng profile LinkedIn của khách hàng.
- **Chấm điểm Lead tự động:** Phân loại ngay lập tức lead nào nóng, lead nào lạnh dựa trên điểm ICP chuẩn xác.
- **Lọc Lead rác hiệu quả:** Tự động loại bỏ các email cá nhân (Gmail, Yahoo...) nhờ bộ lọc thông minh.
- **Hoạt động 24/7 không nghỉ:** Nhận dữ liệu từ Form đăng ký hoặc trigger từ hệ thống khác và xử lý trong tích tắc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đã sẵn sàng hoạt động.
- Tài khoản [Airtop](https://portal.airtop.ai/) và **Airtop API Key**.
- Một **Airtop Profile** đã được đăng nhập sẵn tài khoản LinkedIn (xem thêm tại [Airtop Browser Profiles](https://portal.airtop.ai/browser-profiles)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (từ nguồn n8n template #4256) và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 9 nodes phối hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các node sau:
- **On form submission / When Executed by Another Workflow**: Điểm khởi đầu nhận dữ liệu đầu vào bao gồm Tên người dùng (*Person Name*) và Email công việc (*Work Email*).
- **Unify Parameters**: Chuẩn hóa các tham số đầu vào để truyền tiếp vào các bước xử lý phía sau.
- **Is corporate email? (Filter)**: Node này sẽ kiểm tra xem email có phải là email doanh nghiệp hay không (loại bỏ các tên miền email cá nhân phổ biến).
- **Find Person Linkedin URL, Extract Person Data & ICP Scoring (Execute Workflow)**: Các node này sử dụng Airtop API để tự động hóa trình duyệt web:
  - *Find Person Linkedin URL*: Tự động tìm kiếm và xác thực đúng đường dẫn LinkedIn của lead.
  - *Extract Person Data*: Truy cập profile và trích xuất toàn bộ thông tin chuyên môn.
  - *ICP Scoring*: Tính toán điểm số ICP dựa trên dữ liệu đã trích xuất.
- **Is valid Linkedin URL? (Filter)**: Đảm bảo chỉ tiếp tục xử lý khi tìm thấy URL LinkedIn hợp lệ.
- **Merge**: Tổng hợp dữ liệu profile đã làm giàu và kết quả chấm điểm ICP thành một kết quả duy nhất trả về cho hệ thống.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** với dữ liệu mẫu để kiểm tra xem Airtop có trích xuất dữ liệu thành công hay không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống bán hàng thông minh hơn, các sếp có thể mở rộng workflow này với các ý tưởng sau:
- **Đẩy dữ liệu vào CRM:** Kết hợp thêm node HubSpot, Salesforce hoặc Google Sheets để lưu trữ tự động danh sách lead đã chấm điểm.
- **Cảnh báo qua Slack/Telegram:** Thiết lập gửi thông báo ngay lập tức về nhóm Sales khi có một Lead đạt điểm ICP cao (ví dụ: > 80 điểm).
- **Xử lý hàng loạt (Batch Processing):** Kết hợp với Google Sheets để quét danh sách hàng trăm lead cùng lúc thay vì điền form từng người một.

### 📌 Kết luận
Tự động hóa quy trình nghiên cứu khách hàng và chấm điểm ICP với Airtop và n8n là chìa khóa giúp đội ngũ Sales tăng tốc độ tiếp cận khách hàng tiềm năng lên gấp nhiều lần. Hãy "lên đồ" ngay hôm nay để tối ưu hóa phễu bán hàng của doanh nghiệp các sếp nhé!