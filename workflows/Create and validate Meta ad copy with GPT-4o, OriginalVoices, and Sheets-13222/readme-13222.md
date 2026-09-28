---
title: "🚀 Tự động tạo & xác thực quảng cáo Meta bằng GPT‑4o, OriginalVoices & Google Sheets"
description: "Giải pháp tự động tạo 50 biến thể quảng cáo Meta, lọc và xác thực bằng dữ liệu thực tế, lưu kết quả vào Google Sheets – tiết kiệm thời gian và nâng cao hiệu quả marketing."
slug: "tua-dong-tao-va-xac-thuc-quang-cao-meta-gpt4o-originalvoices-google-sheets"
tags: [n8n, automation, no-code, ai, marketing, google-sheets]
keywords: [n8n workflow, tự động hóa, quảng cáo Meta, GPT-4o, OriginalVoices, Google Sheets, AI marketing]
---

# 🚀 Tự động tạo & xác thực quảng cáo Meta bằng GPT‑4o, OriginalVoices & Google Sheets

Bạn đang phải mất hàng giờ để viết, thử nghiệm và xác thực từng bản sao quảng cáo Meta? Bạn muốn nhanh chóng có được những biến thể tối ưu, được đánh giá bởi dữ liệu thực tế của khách hàng mục tiêu?  
Workflow này sẽ giúp bạn **tạo 50 biến thể quảng cáo** được tối ưu bởi AI, **đánh giá** chúng qua dữ liệu thực tế của OriginalVoices Digital Twins, và **đưa top 10** vào Google Sheet – hoàn toàn **không cần code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ viết bản sao → chỉ vài phút tạo 50 biến thể.  
- **Chính xác hơn**: AI lấy dữ liệu thực tế từ Digital Twins để tối ưu ngôn từ.  
- **Cá nhân hóa**: Được phân loại theo đối tượng mục tiêu ngay trong prompt.  
- **Hoạt động liên tục**: Tự động lưu kết quả vào Google Sheet, sẵn sàng cho báo cáo hoặc tiếp thị tiếp theo.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **OpenAI API key** (được sử dụng trong hai node `OpenAI Chat Model` và `OpenAI Chat Model1`).  
- **OriginalVoices API key** (được truyền qua Header `X-Api-Key` trong node `OriginalVoices Digital Twins`).  
- **Google Sheets OAuth credentials** (được dùng trong node `Write to Google Sheet`).  
- **Google Sheet ID** của file chứa tab `Results` (để append dữ liệu).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: <https://n8n.io/workflows/13222> hoặc copy toàn bộ JSON.  
2. Mở n8n Editor → `File` → `Import Workflow` → dán JSON hoặc tải file.  
3. Lưu lại.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên thực tế | Cấu hình cần chỉnh | Ghi chú |
|------|-------------|---------------------|---------|
| `Ad Brief Form` | FormTrigger | Không cần credentials | Thu thập thông tin sản phẩm & đối tượng |
| `Generate 50 Variations` | Agent | - Prompt: “Generate 50 ad copies…”<br>- Credentials: **OpenAI** | Đảm bảo node `OpenAI Chat Model` được gắn vào |
| `OpenAI Chat Model` | lmChatOpenAi | - API Key (OpenAI) | Chọn model `gpt-4o` (đã được preset) |
| `Parse Variations` | Code | - Không cần credentials | Chuyển JSON trả về thành mảng |
| `Filter & Validate with Digital Twins` | Agent | - Prompt: “Validate each copy with Digital Twins…”<br>- Credentials: **OriginalVoices** | Gắn node `OriginalVoices Digital Twins` |
| `OpenAI Chat Model1` | lmChatOpenAi | - API Key (OpenAI) | Dùng cho bước xác thực bổ sung |
| `OriginalVoices Digital Twins` | mcpClientTool | - Header: `X-Api-Key: YOUR_API_KEY` | Đặt API key của OriginalVoices |
| `Parse Results` | Code | - Không cần credentials | Phân tích phản hồi từ Digital Twins |
| `Format for Sheets` | Code | - Không cần credentials | Tạo đối tượng phù hợp với Google Sheets |
| `Write to Google Sheet` | googleSheets | - Credentials: **Google OAuth**<br>- Operation: `append`<br>- Sheet ID & Tab: `Results` | Đảm bảo quyền ghi vào sheet |

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (điền form). Kiểm tra log, đảm bảo không có lỗi.  
2. **Activate**: Bật toggle `Active` ở góc trên bên phải. Workflow sẽ chạy tự động khi form được submit.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack**: Thêm node `Slack` sau `Write to Google Sheet` để gửi tin nhắn khi top 10 đã được lưu.  
- **Telegram bot**: Dùng node `Telegram` để nhận báo cáo nhanh.  
- **Lưu log**: Thêm node `Google Sheets` hoặc `File` để ghi lại toàn bộ quá trình (prompt, response, thời gian).  
- **Định kỳ gửi báo cáo**: Sử dụng node `Cron` để chạy workflow hàng ngày, tự động gửi email báo cáo tới đội ngũ marketing.  
- **Thay đổi LLM**: Thay `gpt-4o` bằng `gpt-4o-mini` để giảm chi phí, hoặc thử `Claude` nếu có.  
- **Tùy chỉnh prompt**: Thêm câu hỏi về tone, độ dài, hoặc yêu cầu cụ thể (ví dụ “đảm bảo ngôn ngữ thân thiện với người Việt”).  

### 📌 Kết luận
Workflow này giúp các sếp **tối ưu hoá quy trình sáng tạo quảng cáo Meta** từ ý tưởng đến dữ liệu thực tế chỉ trong vài phút. Không cần viết code, chỉ cần cấu hình credentials và bật workflow. Hãy thử ngay, chia sẻ kết quả và cải tiến theo nhu cầu của doanh nghiệp mình!