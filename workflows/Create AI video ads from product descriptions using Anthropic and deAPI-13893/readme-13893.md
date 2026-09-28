---
title: "🎬 Tự Động Hóa Quảng Cáo Video AI Từ Mô Tả Sản Phẩm - Không Cần Code!"
description: "Workflow này tự động chuyển mô tả sản phẩm thành video quảng cáo chuyên nghiệp bằng AI, từ tạo hình ảnh hero đến video động hình, và gửi kết quả qua email - tiết kiệm thời gian lên đến 90% cho các sếp marketing."
slug: "tieu-dong-hoa-quang-cao-video-ai-tu-mo-ta-san-pham"
tags: [n8n, automation, ai-video, deapi, anthropic, content-creation, no-code]
keywords: [n8n workflow video quảng cáo, tự động hóa quảng cáo AI, tạo video từ mô tả sản phẩm, deapi n8n, Anthropic Claude, marketing tự động]
---

# 🚀 Tạo Video Quảng Cáo AI Từ Mô Tả Sản Phẩm - Không Cần Code!

## 💡 Giải Pháp Cho Nỗi Đau Của Các Sếp Marketing
Hàng ngày, các sếp phải:
- **Tốn thời gian** viết script và thiết kế hình ảnh cho từng sản phẩm
- **Khó tạo hình ảnh/video chuyên nghiệp** với ngân sách hạn chế
- **Không có thời gian** theo dõi xu hướng thiết kế mới
- **Phải quản lý nhiều công cụ** khác nhau (AI, thiết kế, email)

Workflow này **tự động hóa toàn bộ quy trình** bằng AI, từ mô tả sản phẩm đến video quảng cáo hoàn chỉnh - chỉ cần nhập thông tin vào form!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tạo video quảng cáo chỉ trong vài phút thay vì nhiều giờ
- **Chất lượng chuyên nghiệp**: Video động hình với hiệu ứng camera và chuyển động tự động
- **Tùy chỉnh hoàn toàn**: Thiết kế phù hợp với từng sản phẩm và phong cách thương hiệu
- **Hoạt động liên tục**: Workflow chạy tự động 24/7 khi có yêu cầu mới
- **Không giới hạn sản phẩm**: Áp dụng cho tất cả loại sản phẩm từ điện thoại đến đồ gia dụng
:::

---

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản deAPI** (miễn phí 1000 credit/month):
   - [Đăng ký deAPI](https://deapi.ai) (sử dụng mã giới thiệu **N8NDEAPI** để nhận 500 credit thêm)
   - Cài đặt **n8n node deAPI** trong n8n Community:
     ```bash
     npx n8n install @n8n-nodes-base/deapi
     ```

2. **Tài khoản Anthropic** (miễn phí với giới hạn):
   - [Đăng ký Anthropic](https://www.anthropic.com/)
   - API Key sẽ được sử dụng cho AI Agent

3. **Tài khoản Gmail** (hoặc thay thế bằng Slack/Teams):
   - Cấu hình OAuth2 trong n8n

4. **n8n instance** trên HTTPS (cần thiết cho các node hoạt động chính xác)

---

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
Các sếp có thể import workflow bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/13893](https://n8n.io/workflows/13893) và import vào n8n Editor
- **Copy/paste JSON** từ link trên vào n8n Editor

:::note[Lưu ý quan trọng]
- **Không thay đổi cấu trúc** của các node liên quan đến AI Agent và deAPI
- **Không xóa node Structured Output Parser** - nó đảm bảo định dạng JSON chính xác
:::

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

#### a) Cấu hình Credentials
Các sếp cần thiết lập các credentials sau trong **Settings > Credentials**:

1. **deApi**:
   - API Key từ tài khoản deAPI
   - Chọn **deAPI** trong danh sách nodes

2. **anthropicApi**:
   - API Key từ tài khoản Anthropic
   - Chọn **Anthropic Chat Model** trong danh sách nodes

3. **gmailOAuth2**:
   - Cấu hình OAuth2 cho tài khoản Gmail
   - Chọn **Gmail** trong danh sách nodes

#### b) Cấu hình Node AI Agent
- Trong node **AI Agent**:
  - Chọn **Claude Opus 4.6** trong danh sách model
  - Đảm bảo **Structured Output Parser** được kết nối với node này

#### c) Cấu hình Node deAPI
- Trong node **deAPI Generate Image**:
  - Đảm bảo tham số `prompt` lấy từ `$json.output.boosted_image_prompt`
- Trong node **deAPI Generate Video**:
  - Đảm bảo tham số `prompt` lấy từ `$('AI Agent').item.json.output.boosted_video_prompt`

#### d) Cấu hình Node Form Trigger
- Thêm các trường:
  - **Product Name** (required)
  - **Product Description** (required)
  - **Visual Style** (optional)
  - **Email** (required)

### 3. Kích hoạt ⚡️
1. **Test run** với dữ liệu mẫu:
   ```json
   {
     "Product Name": "Sony WH-1000XM6",
     "Product Description": "Premium wireless noise-cancelling headphones with 40-hour battery life, multipoint connection, and adaptive sound control. Ultralight carbon fiber headband with soft-fit leather ear cushions.",
     "Visual Style": "modern, minimalist, dark background",
     "Email": "your@gmail.com"
   }
   ```
2. **Bật Active workflow** khi đã kiểm tra thành công

---

## ✍️ Mẹo & gợi ý nâng cao

### 1. Tích hợp với Slack/Teams thay vì Gmail
- Thay thế node **Gmail** bằng node **Slack** hoặc **Microsoft Teams**
- Cấu hình webhook trong Slack/Teams và sử dụng node tương ứng

### 2. Lưu log hoạt động
- Thêm node **StickyNote** sau node **Gmail** để lưu kết quả:
  ```json
  {
    "title": "Video Ad Generated",
    "content": "Product: {{ $node["Product Details Form"].json["Product Name"] }}\nVideo: {{ $json.output.url }}"
  }
  ```

### 3. Tự động gửi báo cáo hàng tuần
- Sử dụng node **Set** để lưu danh sách email đã gửi
- Tạo workflow mới với node **Schedule** (hàng tuần) + node **Gmail** để gửi báo cáo tổng hợp

### 4. Tối ưu hóa prompt cho từng loại sản phẩm
- Tạo các template prompt riêng cho từng danh mục sản phẩm (điện thoại, đồ gia dụng...)
- Sử dụng node **Set** để lưu template và gọi trong AI Agent

### 5. Thêm tính năng preview
- Sử dụng node **deAPI Preview** (nếu có) để cho phép xem trước video trước khi gửi

---

## 📌 Kết luận

Workflow này **giải phóng thời gian** cho các sếp marketing để tập trung vào chiến lược hơn, đồng thời **tăng cường hiệu quả quảng cáo** với video chuyên nghiệp được tạo tự động. Bằng cách kết hợp sức mạnh của **AI Agent (Anthropic)**, **deAPI** và **n8n**, các sếp có thể:
- **Tạo video quảng cáo trong vài phút** thay vì nhiều giờ
- **Đảm bảo nhất quán chất lượng** cho tất cả sản phẩm
- **Tiết kiệm chi phí** so với việc thuê designer
- **Hoạt động 24/7** mà không cần can thiệp

**Hành động ngay hôm nay!**
1. Import workflow vào n8n của mình
2. Cấu hình các credentials theo hướng dẫn
3. Test với một sản phẩm mẫu
4. Tích hợp vào hệ thống marketing của doanh nghiệp

👉 [Tải workflow ngay](https://n8n.io/workflows/13893) và bắt đầu tự động hóa quảng cáo của bạn!

---