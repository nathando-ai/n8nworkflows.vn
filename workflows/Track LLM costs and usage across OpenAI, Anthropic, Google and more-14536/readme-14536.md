---
title: "💰 Theo dõi chi phí và sử dụng LLM trên OpenAI, Anthropic, Google và nhiều hơn nữa"
description: "Hướng dẫn tự động hóa theo dõi chi phí và sử dụng LLM trên các nền tảng AI hàng đầu. Tiết kiệm thời gian và tối ưu hóa chi phí cho các dự án AI của bạn."
slug: "theo-doi-chi-phi-llm-openai-anthropic-google"
tags: [n8n, automation, no-code, AI, LLM, OpenAI, Anthropic, Google]
keywords: [n8n workflow, tự động hóa, theo dõi chi phí LLM, AI cost tracking, OpenAI, Anthropic, Google]
---

# 💰 Theo dõi chi phí và sử dụng LLM trên OpenAI, Anthropic, Google và nhiều hơn nữa

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý chi phí sử dụng LLM. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động thu thập dữ liệu chi phí sử dụng LLM từ nhiều nền tảng
- Tính toán chi phí thực tế cho từng cuộc gọi LLM
- Tạo báo cáo tổng hợp chi tiết về sử dụng LLM
- Theo dõi hiệu suất và tối ưu hóa chi phí AI
- Nhận cảnh báo khi chi phí vượt ngưỡng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n API đã được cấu hình
- Quyền truy cập vào các workflow cần theo dõi
- Kiến thức cơ bản về JavaScript (cho việc chỉnh sửa code nodes)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/14536)
2. Click vào nút "Import" và sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Get Execution Data** node:
   - Chọn credentials "n8nApi" đã được cấu hình
   - Đảm bảo API key có quyền truy cập đầy đủ vào các workflow cần theo dõi

2. **Standardize Names** node:
   - Kiểm tra và cập nhật danh sách tên mô hình trong biến `standardize_names_dic`
   - Đảm bảo tất cả các mô hình sử dụng trong các workflow mục tiêu đều được định nghĩa

3. **Model Prices** node:
   - Xem lại và cập nhật giá các mô hình trong biến `MODEL_PRICES`
   - Giá được tính theo 1 triệu token

4. **Execute Workflow** nodes trong các workflow mục tiêu:
   - Thêm node này vào cuối các workflow cần theo dõi
   - Chọn workflow này trong trường "Workflow to Execute"
   - Tắt tùy chọn "Wait For Sub-Workflow Completion"
   - Truyền dữ liệu đầu vào: `{ "executionId": "{{ $execution.id }}" }`

#### 3. Kích hoạt ⚡️
1. Test run với một execution ID mẫu trong node "Test with Execution ID"
2. Kiểm tra kết quả đầu ra trong node "Generate Summary"
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Lưu trữ lịch sử**: Kết nối workflow với Google Sheets hoặc cơ sở dữ liệu để lưu trữ lịch sử sử dụng LLM
2. **Cảnh báo ngưỡng**: Thiết lập cảnh báo khi chi phí vượt quá ngưỡng đã định
3. **Bảng điều khiển**: Tạo bảng điều khiển với dữ liệu tổng hợp từ node "Generate Summary"
4. **Tích hợp Slack**: Gửi báo cáo hàng ngày về sử dụng LLM vào kênh Slack

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để theo dõi và quản lý chi phí sử dụng LLM trên nhiều nền tảng AI hàng đầu. Bằng cách tự động hóa quá trình thu thập và phân tích dữ liệu, các sếp có thể tối ưu hóa chi phí AI và nâng cao hiệu suất của các dự án AI của mình. Hãy áp dụng ngay để bắt đầu tiết kiệm thời gian và tiền bạc!