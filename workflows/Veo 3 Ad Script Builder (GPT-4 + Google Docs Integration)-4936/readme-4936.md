---
title: "🚀 Tự động hóa Tạo Script Quảng Cáo với GPT-4 + Google Docs - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động hóa việc tạo script quảng cáo 3A (Audience, Action, Appeal) bằng công nghệ AI và Google Docs, tiết kiệm thời gian và nâng cao hiệu quả marketing"
slug: "tu-dong-hoa-tao-script-quang-cao-gpt4-google-docs"
tags: [n8n, automation, no-code, ai, marketing]
keywords: [n8n workflow, tự động hóa marketing, script quảng cáo, AI content, Google Docs]
---

# 🚀 Tự động hóa Tạo Script Quảng Cáo với GPT-4 + Google Docs - Workflow n8n

[Các sếp marketing] đang gặp khó khăn khi phải tạo hàng loạt script quảng cáo cho các kênh khác nhau (Facebook, Google Ads, TikTok...) với các đối tượng khách hàng khác nhau. Việc này tốn thời gian và dễ gây sai sót. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình tạo script quảng cáo 3A (Audience, Action, Appeal) bằng công nghệ AI tiên tiến và tích hợp trực tiếp với Google Docs.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tạo 10-20 script quảng cáo trong ngày thay vì 1-2 script/ngày
- Chất lượng cao: Script được tạo bởi AI GPT-4 với độ chính xác và sáng tạo vượt trội
- Tích hợp liền mạch: Kết quả tự động lưu vào Google Docs của các sếp
- Cá nhân hóa: Tạo script phù hợp với từng đối tượng khách hàng khác nhau
- Hoạt động liên tục: Tự động hóa hoạt động 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (để sử dụng Google Docs)
- API Key của OpenAI (để sử dụng GPT-4)
- Biểu mẫu (form) để nhận thông tin đầu vào (tên đối tượng, mục tiêu, thông tin sản phẩm...)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4936](https://n8n.io/workflows/4936)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

Hoặc copy/paste JSON sau vào n8n Editor:
```json
{
  "nodes": [
    {
      "name": "On form submission",
      "type": "formTrigger",
      "typeVersion": 1,
      "position": [0, 0]
    },
    {
      "name": "Build Persona",
      "type": "openAi",
      "typeVersion": 1,
      "position": [200, 0]
    },
    {
      "name": "Build Environment",
      "type": "openAi",
      "typeVersion": 1,
      "position": [400, 0]
    },
    {
      "name": "Generate Copy",
      "type": "openAi",
      "typeVersion": 1,
      "position": [600, 0]
    },
    {
      "name": "Google Docs",
      "type": "googleDocs",
      "typeVersion": 1,
      "position": [800, 0]
    }
  ],
  "connections": [
    {
      "node": "On form submission",
      "type": "main",
      "index": 0,
      "target": "Build Persona"
    },
    {
      "node": "Build Persona",
      "type": "main",
      "index": 0,
      "target": "Build Environment"
    },
    {
      "node": "Build Environment",
      "type": "main",
      "index": 0,
      "target": "Generate Copy"
    },
    {
      "node": "Generate Copy",
      "type": "main",
      "index": 0,
      "target": "Google Docs"
    }
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Cấu hình biểu mẫu để nhận các thông tin đầu vào cần thiết (tên đối tượng, mục tiêu, thông tin sản phẩm...)
   - Đảm bảo các trường dữ liệu được đặt tên phù hợp với các node OpenAI tiếp theo

2. **Node "Build Persona"**:
   - Chọn credentials OpenAI đã cấu hình
   - Điền prompt phù hợp để tạo persona khách hàng (ví dụ: "Tạo profile chi tiết cho đối tượng khách hàng {{name}} với đặc điểm {{description}}")

3. **Node "Build Environment"**:
   - Chọn credentials OpenAI đã cấu hình
   - Điền prompt phù hợp để phân tích môi trường (ví dụ: "Phân tích môi trường quảng cáo cho sản phẩm {{product}} với đối tượng {{persona}}")

4. **Node "Generate Copy"**:
   - Chọn credentials OpenAI đã cấu hình
   - Điền prompt phù hợp để tạo script quảng cáo (ví dụ: "Tạo script quảng cáo 3A cho sản phẩm {{product}} với đối tượng {{persona}} trong môi trường {{environment}}")

5. **Node "Google Docs"**:
   - Chọn credentials Google Workspace đã cấu hình
   - Chỉ định ID tài liệu Google Docs để lưu kết quả
   - Điền tên sheet phù hợp (ví dụ: "Script Quảng Cáo {{product}} - {{date}}")

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trong Google Docs để đảm bảo script được tạo đúng như mong đợi
3. Nếu mọi thứ ổn, click vào nút "Activate Workflow" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack/Teams**: Thêm node Slack hoặc Microsoft Teams để thông báo khi có script mới được tạo
2. **Lưu log hoạt động**: Thêm node Google Sheets để lưu log các script đã tạo và thời gian tạo
3. **Tự động gửi báo cáo**: Thêm node Email để gửi báo cáo hàng tuần về các script đã tạo
4. **Tối ưu hóa prompt**: Thử nghiệm với các prompt khác nhau để đạt được kết quả tốt nhất cho từng loại sản phẩm và đối tượng khách hàng

### 📌 Kết luận
Workflow này giúp các sếp marketing tự động hóa toàn bộ quy trình tạo script quảng cáo, tiết kiệm thời gian và nâng cao hiệu quả marketing. Với sự kết hợp của công nghệ AI tiên tiến và tích hợp liền mạch với Google Docs, các sếp có thể tạo ra hàng loạt script chất lượng cao một cách nhanh chóng và dễ dàng. Hãy áp dụng ngay workflow này để nâng cao hiệu quả marketing của doanh nghiệp!