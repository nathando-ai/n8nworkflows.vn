---
title: "🎨 Tự động tạo quảng cáo hài hước từ bài đăng Reddit với Dumpling AI và GPT-4o"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi những nỗi đau từ Reddit thành quảng cáo hài hước bằng AI, tiết kiệm thời gian và tăng hiệu quả marketing"
slug: "tu-dong-tao-quang-cao-hai-huoc-tu-reddit"
tags: [n8n, automation, content creation, multimodal AI, marketing]
keywords: [n8n workflow, tự động hóa nội dung, quảng cáo hài hước, Reddit marketing, AI tạo hình ảnh]
---

# 🎨 Tự động tạo quảng cáo hài hước từ bài đăng Reddit với Dumpling AI và GPT-4o

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian so với làm thủ công
- Tạo ra 10 góc quảng cáo hài hước từ mỗi bài đăng Reddit
- Tự động phân loại và lọc những bài đăng có giá trị
- Tạo hình ảnh quảng cáo chuyên nghiệp từ mô tả văn bản
- Lưu trữ tự động các hình ảnh tạo ra trong Google Drive
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (để sử dụng GPT-4o)
- Tài khoản Reddit Developer (để truy cập API Reddit)
- Tài khoản Google Drive (để lưu trữ hình ảnh)
- API key của Dumpling AI (để tạo hình ảnh)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5394](https://n8n.io/workflows/5394)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When a Form is Submitted"**:
   - Cấu hình form để nhận mô tả sản phẩm từ người dùng
   - Đảm bảo form có trường nhập liệu cho mô tả sản phẩm

2. **Node "Generate Reddit Keyword from Product Description"**:
   - Cấu hình credentials OpenAI API
   - Đảm bảo model được chọn là "gpt-4o-mini"

3. **Node "Search Reddit Posts Using Keyword"**:
   - Cấu hình credentials Reddit OAuth2 API
   - Đặt số lượng bài đăng cần tìm kiếm (gợi ý: 50-100 bài)

4. **Node "Filter Posts With 2+ Upvotes and Text"**:
   - Điều chỉnh điều kiện lọc theo nhu cầu (ví dụ: 5+ upvotes)

5. **Node "Classify Post Relevance to Product"**:
   - Cấu hình credentials OpenAI API
   - Đảm bảo model được chọn là "gpt-4o-mini"

6. **Node "Generate 10 Ad Angles From Reddit Posts"**:
   - Cấu hình credentials OpenAI API
   - Đảm bảo model được chọn là "gpt-4o-mini"

7. **Node "Rank Top 10 Ad Angles"**:
   - Cấu hình credentials OpenAI API
   - Đảm bảo model được chọn là "gpt-4o-mini"

8. **Node "Create Comic Prompts from Ad Angles"**:
   - Cấu hình credentials OpenAI API
   - Đảm bảo model được chọn là "gpt-4o-mini"

9. **Node "Generate Comic Image via Dumpling AI"**:
   - Cấu hình credentials HTTP Header Auth
   - Đảm bảo API endpoint của Dumpling AI được cấu hình chính xác

10. **Node "Upload Image to Google Drive"**:
    - Cấu hình credentials Google Drive OAuth2 API
    - Chọn thư mục lưu trữ trong Google Drive

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả ở mỗi node để đảm bảo dữ liệu được xử lý đúng
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Telegram**: Thêm node gửi thông báo khi workflow hoàn thành
2. **Lưu log hoạt động**: Thêm node lưu log các bài đăng được xử lý
3. **Tạo báo cáo định kỳ**: Thêm node tổng hợp và gửi báo cáo hàng tuần
4. **Tối ưu hóa hình ảnh**: Thêm node xử lý hình ảnh trước khi upload lên Google Drive

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình chuyển đổi những nỗi đau từ Reddit thành quảng cáo hài hước, tiết kiệm thời gian và tăng hiệu quả marketing. Bằng cách tích hợp AI và tự động hóa, các sếp có thể tạo ra nội dung hấp dẫn, phù hợp với tâm lý người dùng và tăng khả năng chuyển đổi. Hãy thử ngay và xem kết quả thay đổi như thế nào!