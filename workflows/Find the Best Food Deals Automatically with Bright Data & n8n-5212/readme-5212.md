---
title: "🚀 Tự động săn deal đồ ăn, mã giảm giá Pizza cực hời với Bright Data & n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu (scrape) Uber Eats bằng Bright Data, lọc tên nhà hàng và ưu đãi, sau đó gửi email báo cáo deal ngon mỗi ngày."
slug: "tu-dong-san-deal-do-an-bright-data-n8n"
tags: [n8n, automation, web-scraping, bright-data, gmail, no-code]
keywords: [n8n workflow, tu dong san deal, bright data web unlocker, scrape uber eats, html extract n8n, gui email tu dong]
---

# 🚀 Tự động săn deal đồ ăn, mã giảm giá Pizza cực hời với Bright Data & n8n

Việc thủ công lướt qua các ứng dụng giao đồ ăn như Uber Eats, DoorDash mỗi ngày để tìm các mã giảm giá (deals) hay món ăn miễn phí vừa tốn thời gian lại dễ bỏ lỡ cơ hội. Các trang web này thường có hệ thống chống bot (anti-bot) rất gắt gao, khiến việc viết script cào dữ liệu thông thường trở nên khó khăn.

Giải pháp ư? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: sử dụng **Bright Data Web Unlocker** để vượt rào cản kỹ thuật, cào dữ liệu trang tìm kiếm, bóc tách tên nhà hàng và ưu đãi, sau đó tổng hợp và gửi thẳng vào hộp thư Gmail cá nhân. Không cần viết code phức tạp, mọi thứ đã được đóng gói sẵn sàng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian & chi phí:** Không còn phải thủ công tìm kiếm voucher, mã giảm giá ăn uống mỗi ngày.
- **Vượt rào cản chống bot:** Tận dụng sức mạnh của Bright Data Web Unlocker để cào dữ liệu mượt mà từ các trang web lớn mà không sợ bị block IP.
- **Cập nhật chủ động:** Tự động hóa hoàn toàn lịch trình quét dữ liệu (chạy theo giờ hoặc theo yêu cầu).
- **Cá nhân hóa thông báo:** Nhận ngay danh sách các quán pizza kèm ưu đãi hot nhất trực tiếp qua Gmail mỗi sáng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Bright Data Account:** Tài khoản Bright Data để lấy API Key / Endpoint Web Unlocker (Các sếp có thể đăng ký qua [link ủng hộ tác giả](https://get.brightdata.com/1tndi4600b25)).
- **Gmail Account:** Tài khoản Google kết nối qua OAuth2 trong n8n để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn workflow từ n8n.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 4 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

1. **Trigger Workflow (`manualTrigger`):**
   - Mặc định đây là node chạy thủ công (Manual). Các sếp có thể thay thế bằng node **Schedule Trigger** nếu muốn hệ thống tự động chạy định kỳ mỗi sáng hoặc vài tiếng một lần.

2. **Fetch Uber Eats Search Page - Bright Data (`httpRequest`):**
   - Node này thực hiện request HTTP gửi tới API của Bright Data để lấy toàn bộ mã nguồn HTML của trang tìm kiếm Uber Eats (ví dụ: `https://www.ubereats.com/search?query=pizza`).
   - Các sếp cần cấu hình URL, Headers và điền API Key hoặc Token xác thực của Bright Data vào node này.

3. **Extract Names & Deals (`html`):**
   - Đây là trái tim của việc bóc tách dữ liệu. Sử dụng tính năng trích xuất HTML với các CSS Selector chuẩn xác:
     - **Name Selector:** `div.be.f3.bg.f2.ck.bp.bn.k2` (Dùng để lấy tên nhà hàng).
     - **Deal Selector:** `div.hr.bn.k2` (Dùng để lấy các chương trình giảm giá/ưu đãi).
   - Hãy nhớ cấu hình option lấy **tất cả các kết quả khớp (Get Many/All matches)** để quét toàn bộ danh sách nhà hàng trên trang.

4. **Send Pizza Deals via Gmail (`gmail`):**
   - Kết nối với tài khoản Gmail của các sếp bằng **Gmail OAuth2**.
   - Soạn tiêu đề và định dạng nội dung HTML gửi đi, có thể sử dụng vòng lặp template để hiển thị gọn gàng danh sách deal:
     ```html
     <h3>🍕 Today’s Top Pizza Deals</h3>
     <ul>
       {{#each items}}
         <li><b>{{this.title}}</b> — {{this.deal}}</li>
       {{/each}}
     </ul>
     ```

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm xem dữ liệu có trả về đúng ý không.
- Kiểm tra hộp thư Gmail xem đã nhận được báo cáo deal pizza chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm!

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa nền tảng:** Các sếp hoàn toàn có thể thay đổi URL mục tiêu thành DoorDash, Grubhub hoặc bất kỳ trang thương mại điện tử nào bằng cách thay đổi CSS Selector tương ứng.
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi qua Gmail, các sếp có thể tích hợp thêm node **Telegram** hoặc **Slack** để nhận thông báo ngay trên điện thoại nhóm bạn bè hoặc đồng nghiệp.
- **Lưu trữ lịch sử:** Kết nối thêm node **Google Sheets** hoặc **Notion** để lưu lại lịch sử các deal hời theo từng ngày, phục vụ việc phân tích xu hướng giảm giá.

### 📌 Kết luận
Workflow "Find the Best Food Deals Automatically with Bright Data & n8n" là một ví dụ tuyệt vời cho việc ứng dụng công nghệ No-Code và Web Scraping vào đời sống thực tế giúp tiết kiệm thời gian và tiền bạc. Hãy import ngay vào n8n của các sếp và bắt đầu săn những chiếc pizza giảm giá hời nhất hôm nay nhé!