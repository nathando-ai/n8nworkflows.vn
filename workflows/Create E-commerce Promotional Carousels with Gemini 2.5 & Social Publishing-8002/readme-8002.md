---
title: "🎨 Tự Động Hoàn Thành Carousel Quảng Cáo E-commerce Với Gemini 2.5 & AI Multimodal - Không Cần Code"
description: "Workflow này tự động tạo bộ ảnh carousel chuyên nghiệp, mô tả sản phẩm hấp dẫn và đăng tải lên mạng xã hội chỉ bằng 1 cú nhấp chuột. Giúp các sếp tiết kiệm 10+ giờ công mỗi tháng, tăng tỷ lệ chuyển đổi lên 30%."
slug: "tieu-dong-hoan-thanh-carousel-quang-cao-ecommerce-gemini-2-5"
tags: [n8n, automation, ecommerce, ai-multimodal, content-creation, gemini-2-5, social-media]
keywords: [n8n workflow ecommerce, tự động hóa quảng cáo, tạo carousel với gemini, ai tạo mô tả sản phẩm, đăng tải tự động facebook instagram]
---

# 🚀 **Tự Động Hoàn Thành Carousel Quảng Cáo E-commerce Với Gemini 2.5 & AI Multimodal**

### **Giải pháp hoàn hảo cho các sếp bán hàng online**
Bạn có bao giờ phải mất **30 phút đến 1 giờ** để tạo một bộ carousel quảng cáo cho mỗi sản phẩm mới? Hay phải **làm thủ công** mô tả sản phẩm, chọn ảnh, và đăng tải lên Facebook/Instagram? Với workflow này, **tất cả đều tự động hóa** chỉ bằng một cú nhấp chuột!

Workflow này kết hợp **Gemini 2.5 (AI Multimodal)** để:
✅ **Tạo 5 ảnh carousel chuyên nghiệp** từ mô tả sản phẩm
✅ **Viết mô tả sản phẩm hấp dẫn** bằng AI (OpenAI)
✅ **Tải ảnh lên imgbb** (miễn phí, không giới hạn)
✅ **Đăng tải tự động lên Facebook/Instagram** (hoặc bất kỳ nền tảng nào khác)

Kết quả? **Tiết kiệm 10+ giờ công mỗi tháng**, tăng **tỷ lệ tương tác lên 30%** và **chuyển đổi thành công cao hơn**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS. N8n chạy trên VPS sẽ **không bị giới hạn API call** và **hoạt động liên tục** dù máy tính của bạn tắt.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thiết kế ảnh thủ công, viết mô tả sản phẩm hay đăng tải lên mạng xã hội.
- **Nội dung chuyên nghiệp**: AI tạo **5 ảnh carousel khác nhau** và **mô tả sản phẩm hấp dẫn**, phù hợp với từng nhóm khách hàng.
- **Tăng tỷ lệ tương tác**: Carousel được tối ưu hóa để **giúp sản phẩm nổi bật hơn** trên Facebook/Instagram.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp của con người.
- **Tích hợp nhiều nền tảng**: Có thể đăng tải lên **Facebook, Instagram, Pinterest, hoặc bất kỳ nền tảng nào** thông qua API.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **API Key của Google Gemini 2.5** (để tạo ảnh và mô tả sản phẩm)
✔ **API Key của OpenAI** (để viết mô tả sản phẩm)
✔ **Tài khoản imgbb** (để upload ảnh miễn phí)
✔ **API Key của nền tảng đăng tải** (Facebook, Instagram, hoặc Pinterest)
✔ **Tài khoản n8n self-hosted** (để chạy workflow 24/7)

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import từ file JSON** hoặc **copy/paste JSON** vào n8n Editor.

**Bước 1:** Tải file JSON từ [n8n.io/workflows/8002](https://n8n.io/workflows/8002) hoặc sao chép mã JSON từ trang này.
**Bước 2:** Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **33 node**, nhưng chỉ cần chú ý đến các phần sau:

##### **A. Cấu hình API Keys**
- **Google Gemini 2.5** (node `Google Gemini Chat Model`):
  - Đi đến **Credentials** → Tạo mới **`googlePalmApi`** → Điền **API Key** từ Google Cloud.
- **OpenAI** (node `Generate Carousel Description`):
  - Tạo **`openAiApi`** → Điền **API Key** từ OpenAI.
- **Upload Post API** (node `Upload Post`):
  - Tạo **`uploadPostApi`** → Điền **API Key** của nền tảng đăng tải (Facebook, Instagram, Pinterest).

##### **B. Cấu hình Form Trigger**
- Node **`Photo Upload Form`** (formTrigger) sẽ **khởi động workflow** khi bạn gửi một **ảnh sản phẩm** và mô tả.
- Các sếp cần **cấu hình đường dẫn** (`path: "generate-ad"`) để workflow nhận được dữ liệu đầu vào.

##### **C. Cấu hình Gemini 2.5 để tạo ảnh**
- Node **`Gemini 2.5 Flash - Generate Image 2`** đến **`Gemini 2.5 Flash - Generate Image 5`** sẽ **tạo 5 ảnh carousel khác nhau**.
- Các sếp cần **điền Prompt** để AI hiểu rõ sản phẩm (ví dụ: *"Tạo 5 ảnh carousel cho sản phẩm áo thun premium, phong cách trẻ trung, màu sắc nổi bật"*).

##### **D. Cấu hình Upload Post**
- Node **`Upload Post`** sẽ **đăng tải carousel lên mạng xã hội**.
- Các sếp cần **chọn nền tảng** (Facebook, Instagram) và **cấu hình nội dung** (tiêu đề, mô tả, link sản phẩm).

#### **3. Kích hoạt ⚡️**
- **Test Run**: Nhấn **"Run Workflow"** với một **ảnh mẫu** và mô tả sản phẩm để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, **bật workflow** để nó hoạt động tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu Prompt cho Gemini 2.5**:
   - Để ảnh carousel **hấp dẫn hơn**, các sếp có thể **cập nhật Prompt** như:
     ```plaintext
     "Tạo 5 ảnh carousel cho sản phẩm [tên sản phẩm], phong cách [phong cách], màu sắc [màu sắc], với góc chụp khác nhau để phù hợp với Instagram Reels và Facebook Ads."
     ```
2. **Lưu log hoạt động**:
   - Thêm node **`n8n-nodes-base.manual`** để **xem lại lịch sử** của workflow.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng **node `n8n-nodes-base.email`** để **gửi báo cáo hoạt động** cho team marketing mỗi tuần.
4. **Kết hợp với Slack/Telegram**:
   - Thêm node **`n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** để **thông báo khi workflow hoàn thành**.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp bán hàng online muốn **tự động hóa toàn bộ quy trình tạo và đăng tải carousel quảng cáo**. Bằng cách **chỉ cần upload ảnh và mô tả sản phẩm**, AI sẽ **tự động tạo nội dung chuyên nghiệp** và **đăng tải lên mạng xã hội**.

**Hãy áp dụng ngay để tiết kiệm thời gian và tăng doanh số!** 🚀

---
**🔗 [Xem workflow gốc tại n8n.io](https://n8n.io/workflows/8002)**
**📌 [Tải file JSON](https://n8n.io/workflows/8002/download)** (nếu cần)