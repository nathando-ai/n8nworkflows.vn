---
title: "🚀 Tìm Kiếm Cơ Hội B2B Từ Website Bằng BrightData & OpenRouter AI"
description: "Giải pháp tự động 100% tạo báo cáo cơ hội bán hàng từ website công ty, giảm thời gian thủ công và tăng hiệu quả tiếp cận khách hàng."
slug: "tuyen-dung-b2b-voi-brightdata-openrouter"
tags: [n8n, automation, no-code, AI, web-scraping, lead-generation]
keywords: [n8n workflow, tự động hóa, lead generation, AI, BrightData, OpenRouter]
---

# 🚀 Tìm Kiếm Cơ Hội B2B Từ Website Bằng BrightData & OpenRouter AI

Bạn đang mất hàng giờ để phân tích website của khách hàng tiềm năng, tìm hiểu về đội ngũ, sản phẩm và pain points? Workflow này sẽ giúp bạn **tự động hóa hoàn toàn** quy trình này, chỉ cần nhập URL và nhận ngay báo cáo cơ hội bán hàng chi tiết, không lặp lại, sẵn sàng gửi tới đội sales.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ → vài phút.
- **Độ chính xác cao**: AI phân tích nội dung, giảm sai sót do con người.
- **Không lặp lại**: Đầu ra được dedupe, tránh trùng lặp cơ hội.
- **Hoạt động liên tục**: 24/7, không phụ thuộc vào lịch làm việc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **BrightData API key** – đăng ký miễn phí tại [BrightData](https://get.brightdata.com/scrap).
- **OpenRouter API key** – đăng ký tại [OpenRouter](https://openrouter.ai/).
- **n8n** – phiên bản mới nhất, chạy trên VPS hoặc Docker.
- (Tùy chọn) **Google Docs API** nếu muốn xuất báo cáo tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: <https://n8n.io/workflows/8076>.
2. Mở n8n Editor → **Import** → **Upload JSON** → chọn file vừa tải.
3. Hoặc copy toàn bộ JSON → **Import** → **Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| **parameters** | set | Đặt các tham số đầu vào (ví dụ: `url`, `maxPages`). | Dùng để truyền dữ liệu từ chatTrigger. |
| **extract url** | code | Đoạn JS lấy URL từ `parameters`. | Đảm bảo `return { url: $json.url };`. |
| **scrap urls** | BrightData | Credentials: `brightdataApi`. <br>Parameters: `url`, `maxPages`. | Scrape trang “About Us”, “Team”, v.v. |
| **OpenRouter Chat Model1** | lmChatOpenRouter | Credentials: `openRouterApi`. <br>Model: `openai/o4-mini`. | Phân tích nội dung sơ bộ. |
| **Structured Output Parser1** | outputParserStructured | Định dạng output JSON. | Đảm bảo key `opportunities`. |
| **scrap urls1** | BrightData | Credentials: `brightdataApi`. | Scrape thêm trang nếu cần. |
| **HTML cleaner** | html | Operation: `extractHtmlContent`. | Loại bỏ script, style, v.v. |
| **OpenRouter Chat Model2** | lmChatOpenRouter | Model: `openai/gpt-5`. | Phân tích chi tiết. |
| **Structured Output Parser2** | outputParserStructured | Định dạng output. | |
| **OpenRouter Chat Model3** | lmChatOpenRouter | Model: `openai/gpt-5`. | Tóm tắt cuối cùng. |
| **merge pages** | code | Nối nội dung các trang đã scrape. | |
| **clean list** | code | Loại bỏ duplicate URLs. | |
| **When chat message received** | chatTrigger | Trigger khi nhận tin nhắn chứa URL. | |
| **Find best pages** | agent | Agent tìm trang quan trọng nhất. | |
| **Identify business opportunities** | agent | Agent phân tích pain points. | |
| **de-dupe** | agent | Agent loại bỏ duplicate opportunities. | |

**Credentials**  
- Vào **Credentials** → **Add New** → chọn `brightdataApi` → nhập API key BrightData.  
- Tương tự cho `openRouterApi`.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhắn tin vào bot (ví dụ: `/lead https://example.com`) và kiểm tra output trong console.  
2. Khi mọi thứ ổn, bật **Active** cho workflow.  
3. Đảm bảo **Webhook** hoặc **chatTrigger** được cấu hình đúng kênh (Telegram, Slack, v.v.).

### ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram**: Thêm node Slack hoặc Telegram để gửi báo cáo tự động.  
- **Lưu log**: Dùng node `writeBinaryFile` để lưu raw HTML, AI responses.  
- **Báo cáo định kỳ**: Kết hợp với node `cron` để chạy tự động mỗi ngày, gửi tới Google Docs.  
- **Tùy chỉnh AI**: Thay đổi model (ví dụ `openai/gpt-4o-mini`) để cân bằng chi phí và chất lượng.  

### 📌 Kết luận
Workflow “Tìm Kiếm Cơ Hội B2B Từ Website” giúp các sếp **tiết kiệm thời gian, giảm sai sót và tăng hiệu quả bán hàng**. Hãy thử ngay, điều chỉnh theo nhu cầu và mở rộng thêm các kênh giao tiếp để tối ưu hoá quy trình. Chúc các sếp thành công!