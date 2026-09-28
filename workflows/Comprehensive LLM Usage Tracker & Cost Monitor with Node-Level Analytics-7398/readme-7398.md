---
title: "🚀 Theo dõi chi phí LLM & Phân tích chi tiết từng node"
description: "Giải pháp tự động ghi nhận chi phí sử dụng LLM, phân tích chi tiết từng node và gửi báo cáo chi phí ngay khi workflow chạy."
slug: "theo-doi-chi-phi-llm"
tags: [n8n, automation, no-code, ai, cost-monitoring]
keywords: [n8n workflow, tự động hóa, LLM, chi phí, phân tích]
---

# 🚀 Theo dõi chi phí LLM & Phân tích chi tiết từng node

Bạn đang chạy nhiều workflow LLM trên n8n nhưng không biết chi phí thực tế của từng mô hình? Bạn muốn có báo cáo chi phí ngay sau mỗi lần thực thi, đồng thời kiểm tra xem các mô hình đã được định nghĩa đúng chưa? Workflow **Comprehensive LLM Usage Tracker & Cost Monitor with Node-Level Analytics** chính là giải pháp 100% không cần code giúp bạn:

- Ghi nhận chi phí sử dụng LLM theo từng node.
- Kiểm tra và cảnh báo khi có mô hình chưa được định nghĩa.
- Tự động gửi báo cáo chi phí tới email, Slack hoặc bất kỳ kênh nào bạn muốn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải tính chi phí thủ công sau mỗi lần chạy.
- **Chính xác**: Đo lường chi phí theo token thực tế, tránh sai lệch do ước lượng.
- **Cá nhân hóa**: Định nghĩa tên chuẩn cho từng mô hình, dễ dàng so sánh và báo cáo.
- **Hoạt động liên tục**: Workflow tự động chạy 24/7, gửi báo cáo ngay khi có dữ liệu mới.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đăng ký và cài đặt n8n (Self-hosted hoặc n8n.cloud).
- **Credentials**:
  - `n8nApi` – để lấy thông tin thực thi (Get an execution).
- **Định nghĩa mô hình**:
  - Trong phần **Defined by User** (bên dưới), bạn cần nhập danh sách tên mô hình và giá (đơn vị: token/triệu).
- **Kênh gửi báo cáo** (tùy chọn):
  - Email, Slack, Telegram, hoặc webhook tùy ý.

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc: <https://n8n.io/workflows/7398>.
2. Mở n8n Editor → **Import** → **JSON** → dán nội dung JSON hoặc tải file.
3. Nhấn **Import**. Workflow sẽ xuất hiện trong danh sách workflow của bạn.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Mô tả | Cấu hình cần chỉnh |
|------|-------|---------------------|
| **Get an execution** | Lấy dữ liệu thực thi hiện tại | Credentials: `n8nApi` |
| **When Exc.** | Trigger khi có thực thi mới | Không cần chỉnh |
| **Extract all model names** | Phân tích tên mô hình từ logs | Không cần chỉnh |
| **model prices** | Định nghĩa giá token/triệu cho từng mô hình | Thêm vào `Set` các trường `modelName`, `pricePerMToken` |
| **Standardize names** | Chuẩn hoá tên mô hình | Thêm trường `standardName` |
| **Check correctly defined** | Kiểm tra mô hình đã được định nghĩa | Không cần chỉnh |
| **Stop and Error** | Dừng workflow khi có lỗi | Không cần chỉnh |
| **If not passed** | Xử lý khi mô hình chưa được định nghĩa | Không cần chỉnh |
| **Merge** | Gộp dữ liệu từ các node | Không cần chỉnh |
| **Smart Extract LLM data** | Trích xuất dữ liệu chi tiết LLM | Không cần chỉnh |
| **Calculate cost** | Tính toán chi phí | Đảm bảo trường `pricePerMToken` đã có |
| **Test id** | Trigger thủ công để test | Không cần chỉnh |

#### Định nghĩa mô hình (Defined by User)

- **Model name**: Tên mô hình trong logs (ví dụ: `gpt-4`, `text-davinci-003`).
- **Standard name**: Tên chuẩn để tìm giá (có thể giống hoặc khác).
- **Price per million tokens**: Giá token/triệu (ví dụ: `0.03` USD).

> **Lưu ý**: Nếu bạn muốn sử dụng cùng tên cho cả hai, vẫn cần nhập cả hai trường để workflow có thể tìm giá chính xác.

#### Định nghĩa giá (model prices)

Trong node **model prices** (Set), bạn cần thêm các trường như:

```json
{
  "modelName": "gpt-4",
  "standardName": "gpt-4",
  "pricePerMToken": 0.03
}
```

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow thủ công bằng nút **Execute once**. Kiểm tra console log xem có lỗi không.
2. **Bật Active**: Khi đã chắc chắn, chuyển workflow sang trạng thái **Active**.
3. **Gửi báo cáo**: Thêm node gửi email/Slack vào cuối workflow nếu muốn tự động nhận báo cáo.

## ✍️ Mẹo & gợi ý nâng cao

- **Gửi báo cáo định kỳ**: Thêm node **Cron** để gửi báo cáo chi phí hàng ngày/tuần.
- **Lưu log chi phí**: Kết nối với Google Sheets hoặc Airtable để lưu lịch sử chi phí.
- **Kết hợp Slack**: Thêm node **Slack** để gửi cảnh báo khi chi phí vượt ngưỡng đã định.
- **Tích hợp với Telegram**: Dùng node **Telegram** để nhận thông báo nhanh chóng.

## 📌 Kết luận

Workflow này giúp các sếp tiết kiệm thời gian, giảm rủi ro sai lệch chi phí và tăng tính minh bạch trong quản lý tài nguyên LLM. Hãy thử ngay, điều chỉnh theo nhu cầu và chia sẻ trải nghiệm của bạn!