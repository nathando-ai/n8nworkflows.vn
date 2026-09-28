---
title: "🚀 Trích xuất Insights Marketing và Tự động viết bài từ TikTok với Dumpling AI & GPT-4"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc phân tích video TikTok, trích xuất insight khách hàng và viết content marketing bằng GPT-4."
slug: "trich-xuat-marketing-insights-tu-tiktok-voi-dumpling-ai-gpt4"
tags: [n8n, automation, no-code, tiktok, ai, openai, googlesheets]
keywords: [n8n workflow, tự động hóa tiktok, trích xuất insight, gpt-4, ai transform, google sheets]
---

# 🚀 Trích xuất Insights Marketing và Tự động viết bài từ TikTok với Dumpling AI & GPT-4

Các sếp làm marketing chắc hẳn đều đau đầu khi phải ngồi hàng giờ lướt TikTok, xem video đối thủ hoặc video xu hướng để phân tích xem khách hàng đang gặp vấn đề gì, mong muốn điều gì, rồi lại hì hục viết bài quảng cáo. Việc này vừa tốn thời gian, vừa dễ bỏ sót các "từ khóa vàng" chạm đúng cảm xúc khách hàng.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình: Nhận URL TikTok 👉 Lấy transcript (phụ đề) bằng Dumpling AI 👉 Dùng sức mạnh của GPT-4 (LangChain Agents) để phân tích nỗi đau (pain points), mong muốn, trích dẫn đắt giá 👉 Viết lại thành một bài đăng marketing hoàn chỉnh 👉 Lưu trữ gọn gàng vào Google Sheets. Các sếp chỉ việc ngồi đọc và copy mang đi đăng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nghiên cứu thị trường:** Không cần cày cuốc xem từng video TikTok dài dòng.
- **Bắt trúng insight khách hàng:** Tự động tổng hợp chính xác nỗi đau (pain points), kết quả mong muốn và trích dẫn trực tiếp từ video.
- **Sản xuất content hàng loạt:** GPT-4 tự động viết lại nội dung video thành bài đăng marketing chuyên nghiệp, sẵn sàng sử dụng cho Facebook, LinkedIn hoặc Threads.
- **Quản lý tập trung:** Mọi dữ liệu phân tích và bài viết đều được đồng bộ tự động vào Google Sheets để team cùng sử dụng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
2. **Dumpling AI API:** Tài khoản và API key để trích xuất transcript từ video TikTok.
3. **OpenAI API Key:** Để sử dụng các mô hình GPT-4o-mini thông qua LangChain.
4. **Google Sheets Account:** Tạo sẵn một Google Sheet để lưu trữ dữ liệu (có sẵn các cột phù hợp).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp, sau đó tại giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Form: Submit TikTok URL + Product Info (`formTrigger`):** Node này tạo một giao diện Web Form đơn giản để các sếp nhập Link video TikTok và thông tin sản phẩm. Hãy copy URL form này để sử dụng mỗi khi cần phân tích.
- **Dumpling AI: Get TikTok Transcript (`httpRequest`):** Cần cấu hình `Credentials` loại `httpHeaderAuth` với API Key của Dumpling AI để hệ thống gọi API lấy phụ đề video.
- **Format: Clean VTT Captions (`code`):** Node chạy mã JavaScript đơn giản để làm sạch định dạng phụ đề VTT, loại bỏ các thẻ thời gian rườm rà.
- **GPT-4: Extract Pain Points & Insights (`agent`) & GPT-4: Rewrite Transcript as Marketing Post (`agent`):** Đây là hai AI Agents cốt lõi. Các sếp cần liên kết chúng với các node LLM mô hình bên dưới.
- **GPT-4: Used in Research Agent & GPT-4: Used in Rewrite Agent (`lmChatOpenAi`):** Điền `Credentials` chứa OpenAI API Key. Cấu hình chọn model `gpt-4o-mini` (hoặc các biến thể GPT-4 phù hợp).
- **Google Sheets: Log Insights + Post Copy (`googleSheets`):** 
  - Chọn `Credentials` Google Sheets OAuth2.
  - Cấu hình thông số `operation` thành `appendOrUpdate`.
  - Trỏ đúng tới file Google Sheet và Sheet Name các sếp muốn lưu kết quả (Pain points, Desired outcomes, Direct quotes, Marketing post copy...).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một URL TikTok thử nghiệm qua form để kiểm tra dữ liệu trả về.
- Nếu mọi thứ xanh mướt (success), hãy gạt công tắc sang **Active** để chính thức đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để bot tự động bắn kết quả bài viết và insight về thẳng group chat của team ngay khi submit form xong.
- **Mở rộng nguồn dữ liệu:** Có thể thay thế Form Trigger bằng Webhook kết nối với các công cụ khác để tự động hóa hoàn toàn việc quét video TikTok hàng ngày.
- **Lưu lịch sử chạy:** Sử dụng thêm tính năng lưu log lỗi để dễ dàng kiểm soát nếu video TikTok bị lỗi bản quyền hoặc không lấy được transcript.

### 📌 Kết luận
Việc nghiên cứu đối thủ và viết content trên TikTok chưa bao giờ dễ dàng và tự động hóa đến thế. Hãy áp dụng ngay workflow này vào quy trình marketing của doanh nghiệp các sếp để tối ưu hóa hiệu suất ngay hôm nay!