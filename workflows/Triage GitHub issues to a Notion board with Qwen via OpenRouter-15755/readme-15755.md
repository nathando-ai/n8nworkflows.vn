---
title: "🚀 Tự động phân loại issue GitHub lên Notion bằng AI Qwen thông qua OpenRouter"
description: "Hướng dẫn chi tiết cách tự động phân loại issue GitHub lên Notion bằng AI Qwen thông qua OpenRouter, tiết kiệm thời gian và nâng cao hiệu quả quản lý dự án"
slug: "tu-dong-phan-loai-issue-github-len-notion-bang-ai-qwen"
tags: [n8n, automation, no-code, github, notion, ai, openrouter]
keywords: [n8n workflow, tự động hóa, quản lý issue, ai triage, github automation, notion integration]
---

# 🚀 Tự động phân loại issue GitHub lên Notion bằng AI Qwen thông qua OpenRouter

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý hàng trăm issue trên GitHub thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động phân loại issue mà không cần can thiệp thủ công
- **Nâng cao hiệu quả**: AI phân loại chính xác hơn con người trong nhiều trường hợp
- **Tích hợp liền mạch**: Dữ liệu được đồng bộ tự động giữa GitHub và Notion
- **Hoạt động liên tục**: Workflow chạy 24/7 mà không cần giám sát
- **Dễ dàng tùy chỉnh**: Có thể điều chỉnh các tiêu chí phân loại theo nhu cầu dự án
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GitHub với quyền tạo Fine-grained Personal Access Token
- Tài khoản Notion với quyền tạo internal integration
- API key từ OpenRouter (hoặc bất kỳ dịch vụ LLM nào tương thích OpenAI)
- Notion database được cấu hình sẵn với các trường dữ liệu cần thiết
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15755)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node quan trọng cần cấu hình:**
1. **When Issue Opened (githubTrigger)**
   - Thiết lập credentials cho GitHub API
   - Cấu hình Owner và Repository để theo dõi issue từ repo cụ thể

2. **Verify Notion Duplicate (notion)**
   - Thiết lập credentials cho Notion API
   - Chỉ định Database ID của Notion database bạn đã tạo

3. **OpenAI Qwen-3 Model (lmChatOpenAi)**
   - Thiết lập credentials với OpenRouter API key
   - Đảm bảo model được cấu hình là "qwen/qwen3-235b-a22b-2507"

4. **Add to Notion Board (notion)**
   - Thiết lập credentials cho Notion API
   - Chỉ định Database ID của Notion database bạn đã tạo

#### 3. Kích hoạt ⚡️
1. Test run workflow với một issue mẫu trên GitHub của bạn
2. Kiểm tra kết quả trên Notion database và GitHub issue
3. Bật Active workflow để bắt đầu tự động hóa thực sự

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Discord**: Thêm node để gửi thông báo khi issue được phân loại
2. **Tự động gán nhãn**: Sử dụng nhãn được đề xuất từ AI để tự động gán nhãn trên GitHub
3. **Xử lý hàng loạt**: Thêm chức năng xử lý tất cả issue chưa được phân loại
4. **Bảng điều khiển Notion**: Tạo các view tùy chỉnh trong Notion để theo dõi issue theo mức độ ưu tiên

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa quá trình phân loại issue GitHub lên Notion bằng AI. Với việc tích hợp liền mạch và khả năng tùy chỉnh cao, các sếp có thể nâng cao hiệu quả quản lý dự án một cách đáng kể. Hãy thử ngay và trải nghiệm sự khác biệt!