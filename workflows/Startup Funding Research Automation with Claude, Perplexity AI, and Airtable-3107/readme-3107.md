---
title: "🚀 Tự động hóa Nghiên cứu Đầu tư Startup với Claude, Perplexity AI và Airtable"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình nghiên cứu đầu tư startup bằng n8n, kết hợp AI và Airtable để tiết kiệm thời gian và tối ưu hóa quy trình phân tích."
slug: "tu-dong-hoa-nghien-cuu-dau-tu-startup-voi-claude-perplexity-ai-va-airtable"
tags: [n8n, automation, no-code, ai, startup, funding, airtable]
keywords: [n8n workflow, tự động hóa, nghiên cứu đầu tư, startup, funding, airtable, perplexity ai, claude ai]
---

# 🚀 Tự động hóa Nghiên cứu Đầu tư Startup với Claude, Perplexity AI và Airtable

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các nhà đầu tư khi phải theo dõi hàng trăm startup hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code để theo dõi, phân tích và lưu trữ thông tin đầu tư.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình từ theo dõi tin tức đến phân tích dữ liệu.
- Chính xác cao: Sử dụng các mô hình AI tiên tiến để trích xuất thông tin quan trọng.
- Cá nhân hóa: Tùy chỉnh các tiêu chí lọc và phân tích theo nhu cầu cụ thể.
- Hoạt động liên tục: Theo dõi 24/7 mà không cần can thiệp thủ công.
- Trung tâm dữ liệu thống nhất: Lưu trữ tất cả thông tin trong Airtable để quản lý tập trung.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản [Airtable](https://airtable.com/) với base đã tạo (hoặc sử dụng template [Startup Funding Research](https://airtable.com/appYwSYZShjr8TN5r/shryOEdmJmZE5ROce)).
- API Key từ [Anthropic](https://www.anthropic.com/) (cho Claude AI).
- API Key từ [OpenRouter](https://openrouter.ai/) (cho Perplexity AI).
- (Tùy chọn) API Key từ [Jina AI](https://jina.ai/) cho chức năng tìm kiếm nâng cao.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n Editor](https://your-n8n-instance.com/) và đăng nhập.
2. Nhấn vào "Import from URL" và dán link workflow: [https://n8n.io/workflows/3107](https://n8n.io/workflows/3107).
3. Hoặc tải file JSON về máy và import từ local file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "When clicking ‘Test workflow’" (manualTrigger)**
   - Không cần cấu hình gì, chỉ dùng để test workflow.

2. **Node "Claude 3.5 Sonnet" và "Claude 3.5 Haiku" (lmChatAnthropic)**
   - Cấu hình credentials: Chọn "anthropicApi" và nhập API Key từ Anthropic.
   - Đảm bảo tài khoản có đủ credit để sử dụng mô hình này.

3. **Node "Perplexity" (lmChatOpenRouter)**
   - Cấu hình credentials: Chọn "openRouterApi" và nhập API Key từ OpenRouter.
   - Đặt model: `perplexity/llama-3.1-sonar-small-128k-online`.

4. **Node "Airtable" (airtable)**
   - Cấu hình credentials: Chọn "airtableTokenApi" và nhập API Key từ Airtable.
   - Điền các tham số:
     - Base ID: ID của Airtable base bạn sử dụng.
     - Table Name: Tên bảng chứa dữ liệu đầu tư.
     - Các trường dữ liệu cần lưu (Company, Funding Amount, Round, Date...).

5. **Node "Techcrunch (TC)" và "Venturebeat (VB)" (httpRequest)**
   - Không cần cấu hình gì, chỉ thực hiện GET request đến sitemap của Techcrunch và Venturebeat.

6. **Node "Deep Research" và "JINA Deep Search" (httpRequest)**
   - Cấu hình credentials: Chọn "httpHeaderAuth" và nhập API Key tương ứng.
   - (Tùy chọn) Bạn có thể bỏ qua node này nếu không cần chức năng tìm kiếm nâng cao.

7. **Node "Prompts" (set)**
   - Cấu hình các prompt cho các mô hình AI, đặc biệt chú ý đến:
     - Prompt cho việc trích xuất thông tin từ bài báo.
     - Prompt cho việc phân tích sâu về công ty.

8. **Node "Structured Output Parser" và "Auto-fixing Output Parser" (outputParserStructured, outputParserAutofixing)**
   - Cấu hình schema JSON cho dữ liệu đầu ra mong muốn.
   - Đảm bảo schema này phù hợp với cấu trúc bảng Airtable của bạn.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, nhấn "Execute Workflow" để test.
2. Kiểm tra kết quả trên Airtable để đảm bảo dữ liệu được lưu đúng.
3. Bật "Active" workflow để chạy tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh các từ khóa lọc**: Chỉnh sửa node "Filter" và "Filter1" để thay đổi các từ khóa quan trọng như "raised", "funding" để phù hợp với nhu cầu nghiên cứu của bạn.

2. **Thêm nguồn tin tức**: Bạn có thể thêm các nguồn tin tức khác bằng cách sao chép và sửa các node "Techcrunch (TC)" và "Venturebeat (VB)" để kết nối với các sitemap khác.

3. **Tự động hóa báo cáo**: Kết nối với các node email hoặc Slack để nhận báo cáo hàng ngày về các startup vừa nhận được đầu tư.

4. **Phân tích sâu hơn**: Sử dụng node "Route to Deep Research" để kích hoạt một workflow con để phân tích sâu hơn về các công ty tiềm năng.

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để tự động hóa quy trình nghiên cứu đầu tư startup, từ theo dõi tin tức đến lưu trữ và phân tích dữ liệu. Với sự kết hợp của AI và Airtable, bạn có thể tiết kiệm hàng giờ mỗi ngày và tập trung vào những quyết định đầu tư quan trọng nhất. Hãy thử ngay và tối ưu hóa quy trình của bạn!