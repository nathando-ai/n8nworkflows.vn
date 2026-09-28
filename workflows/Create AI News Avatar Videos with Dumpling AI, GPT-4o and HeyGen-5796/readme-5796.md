---
title: "🤖 Tự Động Hoạt Hình AI Tóm Tắt Tin AI Mới Nhất - Không Cần Code!"
description: "Workflow tự động hóa tạo video hoạt hình avatar từ tin tức AI mới nhất bằng Dumpling AI, GPT-4o và HeyGen - tiết kiệm 10 giờ/tháng cho các sếp content!"
slug: "tay-dong-hoat-hinh-ai-tom-tat-tin-ai-moi-nhat"
tags: [n8n, automation, content-creation, multimodal-ai, ai-video]
keywords: [tự động hóa video AI, hoạt hình avatar tin tức, n8n workflow AI, tạo video từ tin tức, GPT-4o tự động]
---

# 🚀 **Tự Động Tạo Video Hoạt Hình Avatar Tóm Tắt Tin AI Mới Nhất - Không Cần Code!**

### **Giải pháp cho các sếp content:**
Bạn đã từng phải mất **10 giờ/ngày** để tìm tin tức AI mới nhất, viết script, và tạo video hoạt hình? Hay phải lo lắng rằng video của mình **lỗi thời** chỉ sau vài giờ? **Workflow này tự động hóa toàn bộ quy trình** - từ tìm kiếm tin tức đến tạo video avatar hoàn chỉnh - chỉ trong **vài phút mỗi giờ**!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho việc tạo video content.
- **Video luôn mới nhất** (cập nhật tự động mỗi giờ).
- **Chất lượng chuyên nghiệp** với avatar AI và script do GPT-4o viết.
- **Danh sách video được lưu trữ** trên Google Sheets để theo dõi.
- **Cá nhân hóa** được dễ dàng (thay đổi chủ đề, avatar, giọng nói).
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản API**:
   - [Dumpling AI](https://dumpling.ai/) (tìm kiếm và trích xuất tin tức).
   - [HeyGen](https://www.heygen.com/) (tạo video hoạt hình avatar).
   - [OpenAI](https://platform.openai.com/) (API key cho GPT-4o).
   - [Google Sheets](https://sheets.google.com/) (để lưu URL video).
2. **Tham số cấu hình**:
   - **Chủ đề tin tức** (ví dụ: "AI Agent" → thay đổi thành "AI Chatbot" nếu muốn).
   - **Avatar mẫu** (cài đặt trên HeyGen trước).
   - **Giọng nói** (lựa chọn trong HeyGen).
   - **Style video** (ví dụ: "Casual", "Professional").
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/5796](https://n8n.io/workflows/5796) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **14 node** chính, các sếp cần chú ý cấu hình sau:

#### **A. Cấu hình API Keys & Credentials**
| **Node**                     | **Lưu ý cấu hình**                                                                 | **Tham số cần điền**                          |
|------------------------------|------------------------------------------------------------------------------------|-----------------------------------------------|
| **Dumpling AI**              | Thêm **HTTP Header Auth** với API Key từ Dumpling AI.                              | `Authorization: Bearer YOUR_DUMPLING_API_KEY` |
| **GPT-4o Model**             | Chọn **OpenAI API** và nhập `openAiApi` (tạo trong n8n Credentials).                | `model: gpt-4o-mini`                          |
| **HeyGen**                   | Thêm **HTTP Header Auth** với API Key từ HeyGen (Bearer Token).                     | `Authorization: Bearer YOUR_HEYGEN_API_KEY`    |
| **Google Sheets**            | Chọn **Google Sheets OAuth2** và chọn sheet cần ghi dữ liệu.                       | `Sheet Name`: "Video_Links"                   |

#### **B. Cấu hình nội dung**
1. **Thay đổi chủ đề tin tức**:
   - Trong node **"Dumpling AI: Search AI News"**, thay đổi tham số `query` từ `"AI Agent"` thành chủ đề mong muốn (ví dụ: `"AI Chatbot"`).
2. **Cấu hình avatar & giọng nói**:
   - Trong node **"HeyGen: Generate Avatar Video"**, điền:
     - `avatar_id`: ID avatar đã tạo trên HeyGen.
     - `voice_id`: ID giọng nói (ví dụ: `female_english_1`).
     - `style`: `"casual"` hoặc `"professional"`.
3. **Thời gian chạy**:
   - Node **"Schedule Trigger"** chạy **mỗi giờ** (thay đổi trong `cron` nếu muốn khác).

#### **C. Test Run & Bật Workflow**
1. **Test với dữ liệu mẫu**:
   - Chạy **Manual Trigger** để kiểm tra workflow.
   - Kiểm tra:
     - Tin tức được tìm kiếm và trích xuất chính xác.
     - Script video được GPT-4o viết hợp lý.
     - Video được tạo thành công trên HeyGen.
2. **Bật Active**:
   - Sau khi test thành công, bật **Active** cho workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** sau node **"Google Sheets: Log Video URL"** để thông báo video mới được tạo.
2. **Lưu log chi tiết**:
   - Thêm node **Google Drive** hoặc **Notion** để lưu log toàn bộ quá trình (tin tức, script, lỗi...).
3. **Tự động chia sẻ video**:
   - Kết hợp với **YouTube API** hoặc **Facebook API** để tự động upload video lên kênh.
4. **Thay đổi chủ đề tự động**:
   - Sử dụng **Google Trends API** để động thái chủ đề tin tức theo xu hướng.

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp content để tập trung vào chiến lược nội dung hơn. **Chỉ cần cài đặt 1 lần**, nó sẽ tự động tạo video hoạt hình tóm tắt tin tức AI mới nhất **mỗi giờ** - với chất lượng chuyên nghiệp và không cần code!

👉 **Bắt đầu ngay**: Import workflow, cấu hình API, và **bật tự động hóa** cho content của mình! 🚀

---
**Ghi chú cuối cùng**:
- Nếu gặp lỗi, kiểm tra **API Key** và **credentials** trong n8n.
- Để tối ưu, các sếp có thể **thêm node "Error Handling"** để xử lý trường hợp Dumpling AI hoặc HeyGen trả về lỗi.