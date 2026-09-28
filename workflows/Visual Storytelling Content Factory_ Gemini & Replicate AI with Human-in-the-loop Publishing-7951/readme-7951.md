---
title: "🚀 Tự động hóa nội dung đa phương tiện với Gemini AI và Replicate: Workflow n8n hoàn chỉnh"
description: "Tự động tạo nội dung hình ảnh, video và bài đăng mạng xã hội với Gemini AI và Replicate trong n8n. Tiết kiệm thời gian và nâng cao hiệu quả nội dung với workflow 100% không cần code."
slug: "tu-dong-hoa-noi-dung-da-phuong-tien-voi-gemini-ai-va-replicate"
tags: [n8n, automation, no-code, content creation, multimodal AI]
keywords: [n8n workflow, tự động hóa nội dung, Gemini AI, Replicate, tạo nội dung tự động]
---

# 🚀 Tự động hóa nội dung đa phương tiện với Gemini AI và Replicate: Workflow n8n hoàn chỉnh

[Các sếp nội dung và marketing đang gặp khó khăn khi tạo nội dung đa phương tiện chất lượng cho các nền tảng khác nhau. Workflow này giúp tự động hóa toàn bộ quy trình từ tạo nội dung đến xuất bản trên các nền tảng mạng xã hội chính với Gemini AI và Replicate.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian tạo nội dung đa phương tiện
- Tạo nội dung nhất quán trên các nền tảng khác nhau
- Tự động hóa quy trình phê duyệt nội dung qua Slack
- Tăng tốc độ xuất bản nội dung lên 5 lần
- Tạo nội dung chất lượng cao với AI Gemini 2.5 Flash
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản [Replicate](https://replicate.com/)
- Tài khoản [Blotato](https://tinyurl.com/blotatoapp)
- Tài khoản [OpenRouter](https://openrouter.ai/) (để sử dụng Gemini AI)
- Tài khoản Slack và Slack Bot
- Cài đặt Blotato community node trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/7951)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán link workflow vào và nhấn "OK"

Hoặc bạn có thể copy/paste JSON workflow sau vào n8n Editor:

```json
{
  "nodes": [
    // Danh sách các nodes từ workflow gốc
  ],
  "connections": [
    // Danh sách các kết nối giữa nodes
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

1. **OpenRouter Chat Model nodes**:
   - Tạo credentials cho OpenRouter API trong n8n
   - Đảm bảo chọn model "google/gemini-2.5-flash" trong cả hai node OpenRouter Chat Model

2. **Slack nodes**:
   - Tạo credentials cho Slack API trong n8n
   - Chỉnh sửa tên kênh Slack trong cả hai node "Request Approval" và "Request Approval for Video"
   - Đảm bảo bot Slack có quyền gửi và nhận tin nhắn trong kênh này

3. **Blotato nodes**:
   - Tạo credentials cho Blotato API trong n8n
   - Kết nối các tài khoản mạng xã hội cần xuất bản nội dung (Instagram, Facebook, TikTok)

4. **HTTP nodes (Generate an Image và Generate a video)**:
   - Sử dụng credentials từ Replicate trong cả hai node này

5. **Creative Director và Creative Technician Brief nodes**:
   - Chỉnh sửa prompt trong hai node này để phù hợp với chủ đề nội dung của bạn

6. **Limit node**:
   - Kích hoạt node này trong quá trình test để giới hạn số lượng hình ảnh/video được tạo

#### 3. Kích hoạt ⚡️
1. Test run workflow với nút "Execute workflow" để kiểm tra toàn bộ quy trình
2. Kiểm tra từng bước từ tạo nội dung đến xuất bản trên các nền tảng
3. Sau khi test thành công, thay thế nút "Execute workflow" bằng "Schedule Trigger" để chạy workflow theo lịch

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nội dung**:
   - Chỉnh sửa prompt trong hai node đầu tiên để tạo nội dung phù hợp với thương hiệu của bạn
   - Thêm các bước xử lý ảnh/video bổ sung trong node "Resize Image" và "Resize Image: Add Borders"

2. **Kết nối thêm nền tảng**:
   - Kết nối thêm các tài khoản mạng xã hội khác được hỗ trợ bởi Blotato
   - Thêm các bước xuất bản tự động lên các nền tảng khác như Twitter, LinkedIn

3. **Tích hợp với các công cụ khác**:
   - Kết nối với các công cụ quản lý nội dung như WordPress, Notion
   - Thêm bước lưu trữ nội dung đã tạo trong Google Drive hoặc Dropbox

4. **Tối ưu hóa hiệu suất**:
   - Sử dụng node "Schedule Trigger" để chạy workflow theo lịch
   - Thêm bước lưu log hoạt động của workflow để theo dõi hiệu suất

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa nội dung đa phương tiện với Gemini AI và Replicate. Bằng cách tích hợp các công cụ AI và mạng xã hội, các sếp có thể tiết kiệm thời gian đáng kể trong quá trình tạo nội dung và duy trì sự nhất quán trên các nền tảng khác nhau. Hãy thử nghiệm và tùy chỉnh workflow này để phù hợp với nhu cầu cụ thể của doanh nghiệp của bạn!