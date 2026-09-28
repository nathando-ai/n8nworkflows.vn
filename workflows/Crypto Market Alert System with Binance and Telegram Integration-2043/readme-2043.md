---
title: "🚀 Xây dựng Hệ thống Cảnh báo Biến động Giá Crypto tự động với Binance và Telegram trên n8n"
description: "Tự động theo dõi biến động giá thị trường tiền điện tử từ sàn Binance 24/7 và gửi cảnh báo tức thì qua Telegram khi có đồng coin biến động trên 10%."
slug: "he-thong-canh-bao-bien-dong-gia-crypto-binance-telegram"
tags: [n8n, automation, crypto, binance, telegram, no-code, trading-bot]
keywords: [n8n workflow, cảnh báo giá crypto, bot telegram binance, tự động hóa n8n, api binance, trade crypto tự động]
---

# 🚀 Xây dựng Hệ thống Cảnh báo Biến động Giá Crypto tự động với Binance và Telegram

Thị trường tiền điện tử (crypto) biến động từng phút, việc ngồi canh biểu đồ 24/7 là điều bất khả thi đối với các nhà đầu tư bận rộn. Nếu bỏ lỡ các nhịp tăng trưởng mạnh hoặc các cú sập giá bất ngờ, các sếp có thể bỏ lỡ cơ hội vàng hoặc chịu khoản lỗ lớn.

Giải pháp là gì? Hãy để công nghệ lo! Bài viết này sẽ hướng dẫn các sếp cách triển khai một workflow n8n tự động hoàn toàn, kết nối trực tiếp với sàn Binance để quét giá liên tục và bắn tin nhắn cảnh báo ngay lập tức qua Telegram khi có đồng coin nào biến động vượt mức 10%. Không cần biết lập trình, chỉ mất 5 phút cài đặt!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 24/7:** Hệ thống tự động kiểm tra thị trường theo lịch trình cài đặt sẵn (mặc định 5 phút/lần).
- **Cảnh báo tức thì:** Phát hiện ngay các đồng coin có biến động giá trên 10% trong 24h qua và gửi thẳng vào Telegram cá nhân hoặc nhóm chat.
- **Tiết kiệm chi phí:** Sử dụng API công khai miễn phí của Binance, không tốn một xu phí API.
- **Tối ưu hiển thị:** Tự động gom nhóm (Aggregate) và chia nhỏ tin nhắn (Split by 1K chars) để không bị lỗi tràn giới hạn ký tự của Telegram.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Telegram Bot:** Một Bot Telegram đã được tạo sẵn qua `@BotFather` để lấy **Bot Token** và **Chat ID** nơi nhận thông báo.
- **Binance API:** (Tùy chọn) Sẵn sàng sử dụng API công khai miễn phí của Binance, không bắt buộc phải có tài khoản Binance API Key.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ hoặc copy đoạn JSON template, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau để hệ thống hoạt động trơn tru:

- **Schedule Trigger:** Mặc định workflow được thiết lập chạy định kỳ 5 phút/lần. Các sếp có thể đổi thời gian này tùy theo nhu cầu theo dõi thị trường nhanh hay chậm.
- **Binance 24h Price Change (HTTP Request Node):** Node này gọi API công khai miễn phí của Binance để lấy thông tin biến động giá 24h. Các sếp có thể giữ nguyên cấu hình mặc định vì nó hoàn toàn miễn phí và không cần API Key.
- **Filter by 10% Change rate (Function Node):** Node này chứa đoạn code lọc ra các đồng coin có tỷ lệ thay đổi giá (tăng hoặc giảm) vượt mốc 10%. Các sếp có thể mở code ra và điều chỉnh lại con số phần trăm (`10`) nếu muốn lọc mức biến động cao hơn hoặc thấp hơn.
- **Aggregate & Split By 1K chars (Aggregate & Code Nodes):** Hai node này có nhiệm vụ gom các đồng coin thỏa điều kiện lại và cắt ngắn nội dung dưới 1000 ký tự để tránh việc tin nhắn Telegram bị lỗi hiển thị.
- **Send Telegram Message (Telegram Node):** 
  - Tạo Credentials loại **Telegram Bot API** và điền **Bot Token** lấy từ BotFather.
  - Điền chính xác **Chat ID** của cá nhân hoặc nhóm chat Telegram vào ô cấu hình của node để bot biết đường gửi tin nhắn về đâu.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử và kiểm tra xem Telegram có nhận được tin nhắn báo cáo từ bot hay không.
- Nếu mọi thứ mượt mà, hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Nâng cấp & Gợi ý mở rộng
Để hệ thống xịn xò hơn nữa, các sếp có thể phát triển thêm:
1. **Đa kênh thông báo:** Kết hợp thêm node Discord hoặc Slack để bắn tin nhắn cảnh báo đồng thời sang các kênh cộng đồng.
2. **Lưu lịch sử vào Google Sheets:** Thêm node Google Sheets để ghi lại lịch sử các đợt biến động giá lớn nhằm phân tích xu hướng sau này.
3. **Bộ lọc thông minh:** Tùy chỉnh code lọc chỉ lấy các cặp giao dịch với USDT hoặc các đồng coin nằm trong Top 100 vốn hóa thị trường để tránh bị nhiễu bởi các đồng coin rác (shitcoin).

### 📌 Kết luận
Chỉ với vài thao tác kéo thả đơn giản trên n8n, các sếp đã sở hữu ngay một "cạ cứng" săn cơ hội crypto 24/7 mà không tốn một đồng chi phí vận hành nào. Nhanh tay "lên đồ" và cài đặt ngay để không bỏ lỡ bất kỳ con sóng nào của thị trường nhé!