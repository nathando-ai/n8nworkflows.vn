---
title: "🚀 Tự Động Hoà Newsletter Song Ngữ (Tiếng Việt & Tiếng Đức) Với AI GPT-4o, Ảnh & Video - HubSpot & SharePoint"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp tạo newsletter song ngữ chuyên nghiệp, tích hợp hình ảnh AI, video tự động và phân phối đến HubSpot hoặc lưu trữ trên SharePoint chỉ với một yêu cầu đơn giản."
slug: "tieu-dong-hoa-newsletter-song-ngu-ai-gpt4o-hubspot-sharepoint"
tags: [n8n, automation, no-code, ai-multimodal, hubspot, sharepoint, gpt-4o, ai-image-video]
keywords: [n8n workflow tự động hóa newsletter, tạo newsletter song ngữ bằng AI, tự động hóa marketing, HubSpot automation, SharePoint automation, GPT-4o tự động hóa]
---

# 🚀 Tự Động Hoà Newsletter Song Ngữ (Tiếng Việt & Tiếng Đức) Với AI GPT-4o, Ảnh & Video

## 📌 **Giải Pháp Cho Nỗi Đau Của Các Sếp Marketing**
Hàng tuần, các sếp phải mất **giờ đồng hồ** để viết, thiết kế và phân phối newsletter song ngữ (Việt - Đức) cho khách hàng quốc tế. Quá trình này đòi hỏi:
✅ **Sáng tạo nội dung** (viết tiếng Đức và tiếng Việt)
✅ **Thiết kế hình ảnh** (hoặc thuê designer)
✅ **Chỉnh sửa video** (nếu có)
✅ **Phân phối đến khách hàng** (HubSpot, email, SharePoint...)

**Workflow này tự động hóa toàn bộ quy trình chỉ với một yêu cầu đơn giản:** *"Tạo newsletter về chủ đề XYZ và lưu vào SharePoint/HubSpot."*

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với viết thủ công.
- **Chất lượng chuyên nghiệp** với nội dung song ngữ chính xác, hình ảnh video AI.
- **Phân phối tự động** đến HubSpot hoặc lưu trữ trên SharePoint.
- **Hoạt động 24/7** mà không cần can thiệp người dùng.
- **Cá nhân hóa** theo yêu cầu của khách hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản OpenAI** (để sử dụng GPT-4o và các model AI khác).
2. **Microsoft 365** (SharePoint và Outlook để lưu trữ và phân phối).
3. **HubSpot App Token** (để phân phối newsletter đến khách hàng).
4. **API Key FAL AI** (để tạo video và âm thanh tự động).
5. **Gmail OAuth2** (để gửi yêu cầu phê duyệt).
6. **HTML Template** (cần chứa các placeholder cho AI thay thế).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### 1. **Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [n8n.io/workflows/5988](https://n8n.io/workflows/5988) hoặc copy/paste JSON vào **n8n Editor**.
- **Bước 2:** Nhấn **"Import"** và chọn **"From JSON"** trong giao diện n8n.

### 2. **Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **43 node** phức tạp, nhưng chỉ cần chú ý đến các phần sau:

#### **A. Cấu Hình Credentials (Tài Khoản)**
- **OpenAI API Key** → Đăng ký tại [OpenAI](https://platform.openai.com/) và thêm vào **Credential Manager** của n8n (không điền trực tiếp vào node).
- **Microsoft SharePoint OAuth2** → Cài đặt tại [Microsoft App Registration](https://portal.azure.com/).
- **HubSpot App Token** → Tạo tại [HubSpot Developer](https://developers.hubspot.com/).
- **Microsoft Outlook OAuth2** → Cài đặt từ [Microsoft 365 Admin](https://admin.microsoft.com/).
- **FAL AI API Key** → Đăng ký tại [FAL AI](https://fal.ai/) và thêm vào **Configuration Settings** node.

#### **B. Cấu Hình Template HTML**
- **Yêu cầu bắt buộc:** Template phải chứa **placeholder** sau (định dạng **{{KEY}}**):
  ```html
  {{INTRODUCTION_DE}} {{TOPIC_DE}} {{DESCRIPTION_DE}}
  {{TEASER1_DE}} {{TEASER2_DE}} {{TEASER3_DE}} {{CTA_DE}} {{FOOTER_TEXT_DE}} {{FOOTER_NAME_DE}}
  {{TOPIC_TITLE_EN}} {{INTRODUCTION_EN}} {{TOPIC_EN}} {{DESCRIPTION_EN}} {{TEASER1_EN}} {{TEASER2_EN}} {{TEASER3_EN}} {{CTA_EN}} {{FOOTER_TEXT_EN}} {{FOOTER_NAME_EN}}
  ```
- **Lưu file HTML** vào SharePoint (đường dẫn phải khớp với node **"Get Newsletter Template"**).

#### **C. Cấu Hình AI Prompt (Nếu Muốn Thay Đổi)**
- Mở node **"AI Agent"** và chỉnh sửa **prompt** để AI sinh nội dung phù hợp với yêu cầu cụ thể.

#### **D. Cấu Hình Phân phối (HubSpot/SharePoint)**
- **HubSpot:** Chỉnh sửa node **"HubSpot"** để lấy danh sách liên hệ.
- **SharePoint:** Đổi **Folder ID** trong node **"Upload HTML"**, **"Upload JPG"**, **"Upload Video URL"** để lưu vào thư mục mong muốn.

### 3. **Kích Hoạt ⚡️**
- **Test Run:** Gửi yêu cầu mẫu (ví dụ: `{"text": "Tạo newsletter về AI và tự động hóa"}`) qua **Webhook**.
- **Bật Active:** Sau khi kiểm tra, nhấn **"Active"** để workflow chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm kênh phân phối khác (Slack/Telegram):**
   - Sau node **"WF Result"**, thêm node **Slack** hoặc **Telegram Bot** để thông báo kết quả.

2. **Lưu log hoạt động:**
   - Thêm node **Set** trước node **"Send message"** để ghi lại thời gian và trạng thái vào SharePoint.

3. **Tự động gửi báo cáo định kỳ:**
   - Sử dụng **n8n Cron Trigger** để gửi báo cáo tổng hợp newsletter đã tạo hàng tháng.

4. **Tối ưu video/audio:**
   - Chỉnh sửa **ENV_FALAI_VIDEO_DURATION** trong **"Configuration Settings"** để thay đổi thời lượng video (5s hoặc 10s).

5. **Sử dụng model AI khác:**
   - Thay **gpt-4o** bằng **gpt-4-turbo** (nếu muốn tiết kiệm chi phí) trong node **"chatgpt-4o"**.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing để tập trung vào chiến lược hơn, thay vì làm việc thủ công với newsletter. **Chỉ cần một yêu cầu đơn giản**, AI sẽ tự động:
✔ **Viết nội dung song ngữ** (Việt - Đức).
✔ **Tạo hình ảnh & video** từ AI.
✔ **Phân phối đến HubSpot** hoặc lưu vào **SharePoint**.

**Hãy thử ngay và tự động hóa newsletter của mình!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::