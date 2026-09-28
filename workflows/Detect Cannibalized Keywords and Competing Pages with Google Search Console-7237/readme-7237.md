---
title: "🚀 Tự động phát hiện Cannibalized Keywords và các trang cạnh tranh SEO với Google Search Console"
description: "Hướng dẫn sử dụng n8n workflow để tự động quét Google Search Console, phát hiện tình trạng từ khóa ăn thịt lẫn nhau (Keyword Cannibalization) giúp tối ưu thứ hạng SEO."
slug: "phat-hien-cannibalized-keywords-google-search-console-n8n"
tags: [n8n, automation, no-code, seo, google-search-console, market-research]
keywords: [n8n workflow, tự động hóa SEO, keyword cannibalization, Google Search Console API, tối ưu SEO]
---

# 🚀 Tự động phát hiện Cannibalized Keywords và các trang cạnh tranh SEO với Google Search Console

Chào các sếp! Trong quá trình làm SEO, chắc hẳn các sếp đã từng đau đầu với hiện tượng **Keyword Cannibalization (Từ khóa ăn thịt lẫn nhau)**. Đây là tình trạng khi có từ 2 trang trở lên trên cùng một website cạnh tranh cho một từ khóa, khiến Google phân vân không biết nên xếp hạng trang nào, dẫn đến việc tụt hạng hoặc lãng phí ngân sách crawl.

Việc kiểm tra thủ công trên Google Search Console (GSC) cực kỳ mất thời gian và dễ bỏ sót. Bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n tự động hoàn toàn để quét, tổng hợp và phát hiện chính xác các từ khóa đang bị "ăn thịt" và các trang đang cạnh tranh nhau mà không tốn một xu tiền công cụ đắt đỏ!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần export file CSV thủ công từ GSC rồi dùng Excel phức tạp.
- **Phát hiện chính xác:** Lọc ra ngay các từ khóa có nhiều hơn 1 trang nhận click thực tế (True Cannibalization).
- **Tiết kiệm thời gian:** Giúp đội ngũ Content và SEO nhanh chóng tối ưu lại (merge bài hoặc redirect) để tăng trưởng traffic.
- **Linh hoạt:** Có thể chạy thủ công (Manual Start) hoặc cài đặt chạy định kỳ hàng tuần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Google Search Console (GSC):** Tài khoản có quyền truy cập vào property (website) cần quét.
- **Credentials:** Tài khoản Google OAuth2 được cấp quyền đọc dữ liệu từ GSC.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này (hoặc tải file từ [n8n.io Workflow 7237](https://n8n.io/workflows/7237)) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes chính, các sếp chú ý cấu hình kỹ các điểm sau:

- **Manual Start (Node bắt đầu):** 
  - Mặc định dùng để chạy thủ công. Các sếp có thể thay thế bằng node *Schedule Trigger* nếu muốn n8n tự quét hàng tuần.
- **Query Search Analytics (Node Google Search Console):**
  - **Operation:** Đặt là `getPageInsights` (lấy dữ liệu phân tích trang và từ khóa).
  - **Credentials:** Kết nối tài khoản Google Search Console OAuth2 của các sếp.
  - **Property / Site URL:** Thay thế giá trị mặc định `sc-domain:example.com` bằng tên miền thực tế của các sếp (ví dụ: `sc-domain:your-domain.com` hoặc URL dạng `https://your-domain.com/`).
  - **Time Range:** Lấy dữ liệu trong 12 tháng qua để có cái nhìn toàn diện nhất.
- **Summarize by Query (Node Summarize):**
  - Node này gom nhóm dữ liệu theo **query** (từ khóa) và tạo ra các mảng (arrays) chứa danh sách các trang (`appended_page`) và lượng clicks (`appended_clicks`) tương ứng cho từng từ khóa đó.
- **Filter Cannibal Queries (Node Filter):**
  - Node lọc thông minh thực hiện nhiệm vụ: Giữ lại các từ khóa thỏa mãn điều kiện có **> 1 trang** xuất hiện VÀ **trang thứ hai vẫn có lượng clicks > 0** (đảm bảo đây là hiện tượng cạnh tranh thực sự, không phải chỉ hiển thị lác đác vài impression).

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để test run với dữ liệu mẫu từ GSC của các sếp.
- Kiểm tra kết quả trả về (`query`, `appended_page[]`, `appended_clicks[]`, `count_query`).
- Nếu mọi thứ mượt mà, gạt công tắc sang chế độ **Active** để hệ thống tự động làm việc.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở nên "bá đạo" hơn, các sếp có thể mở rộng:
- **Tích hợp Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối để bắn thẳng danh sách các từ khóa bị cannibalization về máy mỗi tuần/tháng.
- **Lưu trữ báo cáo:** Đẩy toàn bộ kết quả lọc được vào Google Sheets để đội ngũ content dễ dàng theo dõi và xử lý từng bài viết.
- **Nâng cao thuật toán:** Theo gợi ý từ tác giả, các sếp có thể dùng hàm `sum` để cộng dồn clicks và lọc chặt chẽ hơn đối với các site có traffic lớn.

### 📌 Kết luận
Keyword Cannibalization là "sâu mọt" âm thầm hút máu traffic SEO của website mà các sếp có thể không nhận ra. Với workflow n8n siêu gọn nhẹ này, việc phát hiện và xử lý các trang cạnh tranh lẫn nhau trở nên đơn giản hơn bao giờ hết. Chúc các sếp áp dụng thành công và đưa từ khóa lên top bền vững!