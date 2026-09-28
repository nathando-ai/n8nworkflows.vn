---
title: "🚀 Tự động hóa tổng hợp tin tức QA Testing và gửi cập nhật Telegram với Gemini và OpenAI"
description: "Hướng dẫn chi tiết cách tự động hóa việc tổng hợp tin tức QA Testing từ nhiều nguồn RSS, xử lý bằng AI và gửi thông báo lên Telegram mỗi 3 giờ."
slug: "tu-dong-hoa-tong-hop-tin-qa-testing-telegram-gemini-openai"
tags: [n8n, automation, no-code, AI, Telegram, RSS]
keywords: [n8n workflow, tự động hóa, tổng hợp tin tức, AI, Telegram, QA Testing]
---

# 🚀 Tự động hóa tổng hợp tin tức QA Testing và gửi cập nhật Telegram với Gemini và OpenAI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp trong lĩnh vực QA khi phải theo dõi hàng chục nguồn tin tức hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code để tổng hợp thông tin chất lượng cao.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi ngày chỉ để theo dõi tin tức QA hàng ngày
- Nhận thông tin tổng hợp chất lượng cao từ nhiều nguồn tin khác nhau
- Tự động lọc và loại bỏ tin tức trùng lặp
- Tích hợp AI để tạo tóm tắt kỹ thuật chuyên nghiệp
- Nhận thông báo tức thì trên Telegram với định dạng dễ đọc
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram với bot đã tạo
- API Key từ Google Gemini (PaLM)
- API Key từ OpenAI (GPT-4o-mini)
- Danh sách URL nguồn tin RSS (The Test Tribe, Medium, Cypress, Dev.to)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13832](https://n8n.io/workflows/13832)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Input Feeds List"**:
   - Chỉnh sửa danh sách URL nguồn tin RSS trong phần "Set" của node này
   - Thêm/xóa URL theo nhu cầu của các sếp

2. **Node "Send News To Telegram Channel" và "Send News To Telegram Channel1"**:
   - Tạo bot Telegram mới và lấy API Token
   - Tạo nhóm Telegram và lấy Chat ID
   - Thêm credentials trong n8n Editor: `Telegram API` với API Token vừa lấy
   - Trong mỗi node Telegram, điền Chat ID vào trường "Chat ID"

3. **Node "OpenAI"**:
   - Thêm credentials `OpenAI API` với API Key từ OpenAI
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng GPT-4o-mini

4. **Node "Gemini"**:
   - Thêm credentials `Google PaLM API` với API Key từ Google Cloud
   - Đảm bảo tài khoản Google Cloud đã kích hoạt Google Gemini API

5. **Node "Schedular"**:
   - Điều chỉnh thời gian chạy theo nhu cầu (mặc định là mỗi 3 giờ)

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test chạy dữ liệu mẫu
2. Kiểm tra kết quả trên Telegram để đảm bảo thông báo được gửi đúng
3. Bật Active workflow bằng cách click vào nút "Activate" ở góc trên bên phải

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh từ khóa lọc**:
   - Trong node "Filter by today's news", điều chỉnh danh sách từ khóa trong phần "Conditions" để phù hợp với lĩnh vực QA của các sếp

2. **Thêm nguồn tin**:
   - Mở rộng danh sách nguồn tin trong node "Input Feeds List" để theo dõi nhiều nguồn hơn

3. **Tùy chỉnh tóm tắt AI**:
   - Điều chỉnh prompt trong node "Gemini" và "OpenAI" để tạo tóm tắt phù hợp hơn với nhu cầu

4. **Thêm kênh thông báo**:
   - Sao chép node Telegram và cấu hình để gửi thông báo đến nhiều nhóm khác nhau

### 📌 Kết luận
Workflow này giúp các sếp QA tiết kiệm thời gian quý giá, tập trung vào công việc cốt lõi hơn. Với khả năng tự động hóa hoàn chỉnh và tích hợp AI, các sếp có thể nhận thông tin tổng hợp chất lượng cao từ nhiều nguồn tin khác nhau một cách nhanh chóng và dễ dàng. Hãy áp dụng ngay để nâng cao hiệu suất làm việc trong lĩnh vực QA!