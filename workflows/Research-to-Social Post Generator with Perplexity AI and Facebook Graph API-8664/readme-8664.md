---
title: "🚀 Tự Động Hóa Từ Nghiên Cứu Đến Bài Đăng Facebook: Sử Dụng Perplexity AI + Graph API (N8N)"
description: "Workflow tự động hóa hoàn toàn không cần code giúp marketers, content team nhanh chóng chuyển đổi ý tưởng từ chat thành bài đăng Facebook chuyên nghiệp, được nghiên cứu sâu và cá nhân hóa. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công!"
slug: "tu-dong-hoa-tu-nghien-cuu-den-bai-dang-facebook"
tags: [n8n, automation, social-media, ai-multimodal, facebook-graph-api, openai, perplexity-ai]
keywords: [n8n workflow tự động hóa, tự động hóa bài đăng facebook, ai viết bài đăng facebook, nghiên cứu tự động hóa, n8n với perplexity ai, tự động hóa content marketing]
---

# 🚀 **Tự Động Hóa Từ Nghiên Cứu Đến Bài Đăng Facebook: Sử Dụng Perplexity AI + Graph API**

### **Giải pháp cho marketers, founders và content team**
Bạn đã bao giờ phải mất **3-5 tiếng** để nghiên cứu, viết và đăng một bài đăng Facebook chuyên nghiệp? Hay phải lo lắng bài đăng không đủ hấp dẫn, thiếu tính cá nhân hóa? **Workflow này sẽ thay đổi mọi thứ!**

Với **n8n + Perplexity AI + OpenAI**, bạn chỉ cần **gửi một yêu cầu chat đơn giản**, hệ thống sẽ tự động:
✅ **Tìm kiếm và tổng hợp thông tin mới nhất** từ Perplexity AI
✅ **Tạo bài đăng hoàn chỉnh** với tiêu đề hấp dẫn, nội dung ngắn gọn và CTA hiệu quả
✅ **Đăng tự động lên Facebook Page** của bạn (hoặc gửi qua review trước khi đăng)

**Kết quả?** Bài đăng **chuyên nghiệp, cá nhân hóa và được nghiên cứu kỹ lưỡng**, tiết kiệm **80% thời gian** so với cách làm thủ công!

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 3-5 tiếng xuống còn **5-10 phút** cho mỗi bài đăng.
- **Nội dung chuyên nghiệp**: Bài đăng được viết bởi AI với **tôn chỉ phù hợp**, tiêu đề hấp dẫn và CTA hiệu quả.
- **Nghiên cứu sâu**: Dữ liệu từ Perplexity AI đảm bảo **tin tức mới nhất và chính xác**.
- **Tự động hóa hoàn chỉnh**: Từ chat đến đăng bài, **không cần can thiệp thủ công**.
- **Cá nhân hóa**: Dễ dàng điều chỉnh **tôn chỉ, phong cách** phù hợp với brand của bạn.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
✔ **Tài khoản n8n** (Cloud hoặc **Self-hosted** để ổn định 24/7)
✔ **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/))
✔ **Facebook Page** với quyền **publish permissions** (đăng ký tại [Meta for Developers](https://developers.facebook.com/))
✔ **Workflow nghiên cứu Perplexity** (nếu muốn tích hợp nghiên cứu sâu)
✔ **Nghiên cứu về cấu trúc bài đăng** (để tối ưu hóa prompt)
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8664](https://n8n.io/workflows/8664) hoặc copy/paste JSON vào **n8n Editor**.
- **Khuyến nghị**: Sử dụng **n8n Self-hosted** để tránh giới hạn của phiên bản Cloud.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Credentials (BẮT BUỘC)**
- **OpenAI API Key**: Đăng ký tại [OpenAI](https://platform.openai.com/) và thêm vào **Credentials** của n8n.
- **Facebook Page Access Token**: Tạo tại [Meta for Developers](https://developers.facebook.com/) với quyền `publish_pages`.

#### **🔹 Cấu hình các Node quan trọng**
| **Node** | **Lưu ý cấu hình** |
|----------|---------------------|
| **💬 Chat Trigger** | Giữ nguyên hoặc cập nhật **greeting** và **ví dụ prompt** để người dùng dễ sử dụng. |
| **🔍 Tool: Call Perplexity Researcher** | Điền `RESEARCH_WORKFLOW_ID` của workflow Perplexity (nếu có). |
| **📊 Agent: Topic + Research** | Cập nhật **prompt** để AI hiểu rõ yêu cầu nghiên cứu. |
| **📄 Parser: Article JSON** | Kiểm tra **cấu trúc JSON** để đảm bảo dữ liệu được trích xuất chính xác. |
| **📝 Agent: Create Post Content** | Điều chỉnh **tôn chỉ, phong cách** phù hợp với brand (ví dụ: thân thiện, chuyên nghiệp, hài hước). |
| **📤 Publish: Facebook Graph API** | Điền `YOUR_FACEBOOK_PAGE_ID` và chọn `edge` là `feed`. **Không kích hoạt trong giai đoạn test!** |

#### **🔹 Node CONFIG (Set fields) 🔧**
- Đây là nơi **cập nhật các tham số chung** như:
  - **Tôn chỉ bài đăng** (ví dụ: "Thân thiện", "Chuyên nghiệp", "Hài hước").
  - **Số lượng hashtag** (nếu cần).
  - **Cấu trúc tiêu đề** (ví dụ: "🔥 [Tên chủ đề] – [Lời khuyên/kinh nghiệm]").

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với một **prompt mẫu**:
   ```
   "Viết một bài đăng về cách tăng doanh số bán hàng cho shop e-commerce trong tháng 12"
   ```
2. Kiểm tra **các bước**:
   - AI có tìm kiếm được thông tin từ Perplexity không?
   - Bài đăng có được viết với **tôn chỉ phù hợp** không?
   - **Facebook API** có đăng bài thành công không?
3. **Bật Active** khi đã kiểm tra xong.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **🔹 Tích hợp với Slack/Telegram**
- Sử dụng **Node Webhook** để gửi kết quả bài đăng lên **Slack/Telegram** trước khi đăng.
- **Cách làm**:
  1. Thêm **Node Webhook** sau **Agent: Create Post Content**.
  2. Cấu hình **URL Webhook** của Slack/Telegram.
  3. Kích hoạt **review manual** trước khi đăng.

### **🔹 Lưu log và báo cáo**
- Sử dụng **Node Google Sheets** hoặc **Notion** để lưu **tất cả bài đăng** đã tự động hóa.
- **Cách làm**:
  1. Thêm **Node Google Sheets** sau **Publish: Facebook Graph API**.
  2. Cấu hình **Sheet Name** và **Range** để lưu dữ liệu.

### **🔹 Tùy chỉnh cho nhiều nền tảng**
- **Viết lại prompt** để tạo bài đăng cho **LinkedIn, Twitter, Instagram**.
- **Cách làm**:
  1. Sử dụng **Node Set** để chia nhánh workflow.
  2. Cập nhật **Agent: Create Post Content** cho từng nền tảng.

### **🔹 Thêm bước review trước khi đăng**
- Sử dụng **Node Slack/Email** để gửi bài đăng cho **team review** trước khi đăng.
- **Cách làm**:
  1. Thêm **Node Slack/Email** sau **Agent: Create Post Content**.
  2. Cấu hình **message template** để team review dễ dàng.

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp marketers, founders và content team, giúp họ tập trung vào **strategy** thay vì làm việc thủ công. **Chỉ cần một yêu cầu chat**, hệ thống sẽ tự động:
✔ **Nghiên cứu** thông tin mới nhất từ Perplexity AI.
✔ **Viết bài đăng** chuyên nghiệp với tôn chỉ phù hợp.
✔ **Đăng tự động** lên Facebook (hoặc gửi qua review).

**Hãy thử ngay và tiết kiệm thời gian cho mình!** 🚀

---
### **📌 Bài viết liên quan**
- [Tự động hóa bài đăng LinkedIn với n8n](link)
- [Sử dụng Perplexity AI trong n8n](link)
- [Cách cài n8n Self-hosted trên VPS](link)