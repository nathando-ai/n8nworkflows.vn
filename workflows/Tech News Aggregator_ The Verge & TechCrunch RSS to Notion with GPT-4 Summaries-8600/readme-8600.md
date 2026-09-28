---
title: "🚀 Tự động tổng hợp tin tức công nghệ từ The Verge & TechCrunch vào Notion với tóm tắt AI"
description: "Hướng dẫn tự động hóa quy trình tổng hợp tin tức công nghệ từ 2 nguồn hàng đầu The Verge và TechCrunch, xử lý bằng AI GPT-4 và lưu vào Notion với chỉ 1 click"
slug: "tu-dong-tong-hop-tin-tuc-cong-nghe-the-verge-techcrunch-notion-ai"
tags: [n8n, automation, no-code, AI, Notion, RSS, LangChain]
keywords: [n8n workflow, tự động hóa tin tức, AI tóm tắt, Notion database, LangChain, OpenAI]
---

# 🚀 Tự động tổng hợp tin tức công nghệ từ The Verge & TechCrunch vào Notion với tóm tắt AI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi thủ công tin tức công nghệ từ nhiều nguồn khác nhau, mất thời gian xử lý và lưu trữ. Giới thiệu workflow như giải pháp tự động hóa hoàn chỉnh với AI tóm tắt.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tổng hợp tin tức từ 2 nguồn hàng đầu mỗi ngày
- **Tóm tắt thông minh**: Sử dụng AI GPT-4 để tạo tóm tắt ngắn gọn, chính xác
- **Lưu trữ chuyên nghiệp**: Tự động lưu vào Notion với định dạng chuẩn
- **Tránh trùng lặp**: Sử dụng mã hóa SHA256 để phát hiện và loại bỏ tin tức trùng lặp
- **Tự động hóa hoàn chỉnh**: Chạy định kỳ hoặc kích hoạt thủ công theo nhu cầu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Notion với Database đã tạo (cấu trúc phù hợp với workflow)
- API Key từ OpenAI (để sử dụng GPT-4)
- Tài khoản n8n đã cài đặt các credentials: Notion API và OpenAI API
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/8600)
2. Copy toàn bộ JSON workflow
3. Trong n8n Editor, nhấn "Import from JSON" và dán nội dung đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger"**:
   - Cấu hình thời gian chạy định kỳ (ví dụ: mỗi ngày lúc 8:00 AM)
   - Hoặc sử dụng node "When clicking ‘Execute workflow’" để kích hoạt thủ công

2. **Node "OpenAI Chat Model"**:
   - Chọn credentials OpenAI API đã cấu hình
   - Đảm bảo model được chọn là "gpt-4.1-mini" (hoặc phiên bản mới nhất của GPT-4)

3. **Node "Create a database page"**:
   - Cấu hình credentials Notion API
   - Điền ID của Notion Database cần lưu tin tức
   - Kiểm tra cấu trúc dữ liệu phù hợp với workflow (bắt buộc có trường "Hash" để lưu mã SHA256)

4. **Node "TechCrunch" và "The Verge"**:
   - Kiểm tra URL feed RSS có hoạt động hay không
   - Có thể thay đổi số lượng bài viết lấy mỗi lần chạy (mặc định là 10)

#### 3. Kích hoạt ⚡️
1. Chạy test với 1-2 bài viết mẫu để kiểm tra toàn bộ chuỗi xử lý
2. Sau khi xác nhận hoạt động ổn, bật chế độ Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh tóm tắt**: Chỉnh sửa prompt trong node "Basic LLM Chain" để thay đổi cách AI tóm tắt tin tức
2. **Thêm thông báo**: Kết nối với Slack/Telegram để nhận thông báo khi có tin tức mới
3. **Lưu log**: Thêm node lưu log các bài viết đã xử lý vào Google Sheets hoặc Notion khác
4. **Phân loại tin tức**: Sử dụng AI để tự động phân loại tin tức theo chủ đề

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc theo dõi và xử lý tin tức công nghệ. Với sự kết hợp của tự động hóa và trí tuệ nhân tạo, các sếp có thể tập trung vào những công việc quan trọng hơn trong công việc hàng ngày. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn!