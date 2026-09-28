---
title: "🚀 Tự động phát hiện xu hướng mạng xã hội và tạo ý tưởng bài viết với Claude AI và Google Sheets"
description: "Workflow n8n này tự động thu thập xu hướng từ Twitter, Reddit và Google Trends, sau đó sử dụng Claude AI để tạo ý tưởng bài viết và lưu vào Google Sheets. Tiết kiệm thời gian và tăng hiệu quả nội dung cho các sếp."
slug: "tu-dong-phat-hien-xu-huong-mang-xa-hoi-tao-idea-bai-viet-voi-claude-ai-va-google-sheets"
tags: [n8n, automation, no-code, content creation, multimodal AI]
keywords: [n8n workflow, tự động hóa, tạo nội dung, AI, mạng xã hội]
---

# 🚀 Tự động phát hiện xu hướng mạng xã hội và tạo ý tưởng bài viết với Claude AI và Google Sheets

[Các sếp] có biết không? Với việc nội dung ngày càng trở nên quan trọng trong thời đại số, việc tạo ra nội dung hấp dẫn và phù hợp với xu hướng luôn là thách thức lớn. Thay vì phải theo dõi từng trang mạng xã hội và nghĩ ra ý tưởng bài viết, các sếp có thể tự động hóa toàn bộ quy trình này với workflow n8n này.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập xu hướng từ nhiều nguồn khác nhau.
- **Tăng hiệu quả nội dung**: Tạo ra ý tưởng bài viết phù hợp với xu hướng và thương hiệu.
- **Tăng cường tương tác**: Đề xuất thời gian đăng bài tối ưu để tăng tương tác.
- **Quản lý nội dung dễ dàng**: Lưu trữ và theo dõi tất cả ý tưởng trong Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Twitter API (để lấy xu hướng từ Twitter).
- Tài khoản Reddit API (để lấy xu hướng từ Reddit).
- Tài khoản Anthropic API (để sử dụng Claude AI).
- Tài khoản Google Sheets API (để lưu ý tưởng bài viết).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15017](https://n8n.io/workflows/15017) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào **Import from File** và chọn file JSON đã tải về.
3. Hoặc, copy toàn bộ nội dung JSON từ trang web và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Receive Trend Request"**: Cấu hình webhook với path là `social-trends` và method là `POST`.
- **Node "Validate Config & Build Parameters"**: Cập nhật thông tin về thương hiệu, lĩnh vực và các tham số khác trong phần code.
- **Node "Fetch Twitter Trending Topics"**: Cấu hình credentials cho Twitter API.
- **Node "Fetch Reddit Hot Topics"**: Cấu hình credentials cho Reddit API.
- **Node "Claude AI Model"**: Cấu hình credentials cho Anthropic API và chọn model `claude-sonnet-4-20250514`.
- **Node "Log Ideas to Google Sheets"**: Cấu hình credentials cho Google Sheets API và chỉ định tên sheet và phạm vi để lưu ý tưởng.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**: Gửi một yêu cầu POST đến webhook với payload mẫu như sau:
```json
{
  "platforms": ["twitter", "instagram", "linkedin"],
  "niche": "AI & Technology",
  "trendSources": ["twitter", "reddit", "google"],
  "contentTypes": ["educational", "entertaining", "news"],
  "targetAudience": "tech professionals, 25-45",
  "brandVoice": "professional yet approachable",
  "minTrendScore": 60,
  "maxIdeasPerTrend": 3,
  "includeVisuals": true
}
```
2. **Bật Active workflow**: Sau khi test thành công, kích hoạt workflow để nó chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo khi có ý tưởng mới hoặc khi workflow hoàn thành.
- **Lưu log hoạt động**: Thêm node để ghi log các hoạt động quan trọng của workflow.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp các ý tưởng bài viết hàng tuần.
- **Tích hợp với các công cụ khác**: Kết nối với các công cụ như Canva, Unsplash để tạo nội dung trực tiếp từ ý tưởng.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và tăng hiệu quả nội dung bằng cách tự động hóa việc phát hiện xu hướng và tạo ý tưởng bài viết. Với các bước cấu hình đơn giản và kết quả rõ ràng, các sếp có thể áp dụng ngay để nâng cao hiệu suất làm việc.