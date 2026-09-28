---
title: "🚀 Tự động tổng hợp tin tức Crypto và gửi Telegram bằng RSS + GPT‑4"
description: "Workflow n8n thu thập tin tức crypto từ 5 nguồn RSS, lọc, tóm tắt, dịch sang tiếng Nga bằng GPT‑4 và tự động gửi bản tin tới Telegram mỗi 3 giờ."
slug: "tu-dong-tong-hop-tin-tuc-crypto-telegram-rss-gpt4"
tags: [n8n, automation, no-code, crypto, telegram, openai]
keywords: [n8n workflow, tự động hóa, crypto news, GPT-4, Telegram bot]
---

# 🚀 Tự động tổng hợp tin tức Crypto và gửi Telegram bằng RSS + GPT‑4

Bạn đã từng mất hàng giờ mỗi ngày để lướt qua các trang tin crypto, sao chép, dịch và chia sẻ lại cho đội ngũ?  
Việc làm thủ công này không chỉ tốn thời gian mà còn dễ bỏ lỡ những tin quan trọng.  

**Workflow này** sẽ tự động:

1. **Kéo tin mới** từ 5 nguồn RSS uy tín (Coindesk, Cointelegraph, Decrypt, Cryptobriefing, Nulltx).  
2. **Lọc, sắp xếp** và loại bỏ trùng lặp.  
3. **Phân tích, tóm tắt & dịch** sang tiếng Nga bằng OpenAI GPT‑4 (mini / 4.1‑mini).  
4. **Định dạng HTML** phù hợp cho Telegram.  
5. **Đăng bản tin** vào kênh hoặc nhóm Telegram **mỗi 3 giờ**.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không còn phải mở 5 trang web, sao chép, dịch thủ công.  
- **Độ chính xác cao**: GPT‑4 phân tích nội dung, lọc tin “đáng chú ý”.  
- **Bản tin đa ngôn ngữ**: Dịch sang tiếng Nga (hoặc tùy chỉnh) chỉ trong vài giây.  
- **Hoạt động liên tục**: Tự động chạy mỗi 3 giờ, luôn cập nhật tin mới nhất.  
- **Dễ mở rộng**: Thêm nguồn RSS, kênh Telegram, hoặc các bước AI khác.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản OpenAI** với **API Key** (có quyền truy cập GPT‑4).  
- **Bot Telegram**: tạo bot qua @BotFather, lấy **Bot Token**.  
- **Chat ID** của kênh hoặc nhóm Telegram (có thể là `@your_channel` hoặc numeric ID).  
- **n8n** (cài đặt trên VPS hoặc Docker).  
- (Tùy chọn) **Node.js** phiên bản >= 18 nếu tự host.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ trang gốc hoặc liên kết chia sẻ).  
2. Vào **n8n Editor → Import → From File** và chọn file JSON.  
3. Hoặc **Copy/Paste** toàn bộ JSON vào **Import → From Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng và cách cấu hình:

| Node | Loại | Hướng dẫn cấu hình |
|------|------|-------------------|
| **Coindesk**, **Cointelegraph**, **Decrypt**, **Cryptobriefing**, **Nulltx** | `rssFeedRead` | - `Feed URL` tương ứng (được điền sẵn). <br> - Đặt `Read Items` = `All` hoặc `Latest`. |
| **Scheduler** | `scheduleTrigger` | - `Cron` hoặc `Every X hours`. <br> - Mặc định: **Every 3 hours**. |
| **Merge** | `merge` | - Chọn **Mode**: `Append` (để gộp danh sách tin từ các RSS). |
| **News Filter & Sorter** | `code` | - Script JavaScript lọc trùng lặp, sắp xếp theo ngày. <br> - Kiểm tra biến `items` đầu vào, trả về mảng `filteredItems`. |
| **News Formatter** | `code` | - Định dạng mỗi tin thành **HTML** (tiêu đề, link, mô tả ngắn). <br> - Đảm bảo output là chuỗi `htmlContent`. |
| **SMM Editor** | `agent` (LangChain) | - Prompt: “Viết tiêu đề hấp dẫn cho bản tin crypto, ngắn gọn, không quá 80 ký tự”. <br> - Chọn **Model**: `gpt-4o-mini`. |
| **Crypto Analyst** | `agent` (LangChain) | - Prompt: “Phân tích nhanh nội dung tin, đưa ra 2‑3 điểm nổi bật, viết bằng tiếng Nga”. <br> - Model: `gpt-4o-mini`. |
| **News Preparer** | `code` | - Kết hợp output từ **SMM Editor** & **Crypto Analyst** thành một bản tin duy nhất. |
| **GPT** | `lmChatOpenAi` | - **Credentials**: `openAiApi`. <br> - **Model**: `gpt-4o-mini`. <br> - Prompt mặc định: “Summarize and translate the following crypto news into Russian”. |
| **GPT 2** | `lmChatOpenAi` | - **Credentials**: `openAiApi`. <br> - **Model**: `gpt-4.1-mini`. <br> - Dùng để **refine** bản tóm tắt nếu cần. |
| **Post to Group** | `telegram` | - **Credentials**: Bot Token của bạn. <br> - `Chat ID`: nhập `@your_channel` hoặc ID số. <br> - `Message Type`: **HTML**. <br> - `Message`: đưa biến `htmlContent` (kết quả từ **News Preparer**). |

> **⚠️ Lưu ý:** Đảm bảo **OpenAI API quota** đủ cho số lần gọi (mỗi lần chạy sẽ gọi GPT 2‑3 lần).  

#### 3. Kích hoạt ⚡️
1. **Test run**: Chọn **Execute Workflow** → Kiểm tra log ở mỗi node, đặc biệt node **Post to Group**.  
2. Nếu mọi thứ ổn, **bật** nút **Active** (góc trên bên phải).  
3. Kiểm tra Telegram: bạn sẽ nhận được bản tin dạng HTML mỗi 3 giờ.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm nguồn RSS**: Duplicate một node `rssFeedRead`, thay URL mới, và kết nối vào node **Merge**.  
- **Gửi báo cáo hàng ngày**: Thêm một node **ScheduleTrigger** (hàng ngày) + **HTML Table** để tổng hợp số tin đã gửi, gửi qua email hoặc Slack.  
- **Lưu log vào Google Sheets**: Thêm node **Google Sheets** sau **News Preparer** để ghi lại tiêu đề, link, thời gian.  
- **Đa ngôn ngữ**: Thay prompt trong **GPT** node để dịch sang tiếng Việt, Anh, hoặc bất kỳ ngôn ngữ nào cần.  

### 📌 Kết luận
Với workflow này, các sếp sẽ **không còn phải mất công tìm, dịch, tóm tắt tin crypto** nữa. Chỉ cần một lần thiết lập, n8n sẽ tự động cung cấp bản tin chất lượng, luôn cập nhật, và đưa thẳng vào Telegram. Hãy triển khai ngay hôm nay để tối ưu hoá thời gian và nâng cao hiệu quả truyền thông nội bộ! 🚀