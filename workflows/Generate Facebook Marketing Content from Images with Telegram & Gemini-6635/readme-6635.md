---
title: "🚀 Tự Động Hóa Tạo Nội Dung Marketing Facebook Từ Ảnh qua Telegram + AI Gemini (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tạo nội dung marketing Facebook từ ảnh chia sẻ trên Telegram, với AI Gemini tự động viết bài, hashtag, CTA và gửi đến Facebook chỉ trong vài giây. Giảm thời gian tạo nội dung 90% và tăng hiệu quả quảng bá thương hiệu."
slug: "tieu-dong-hoa-tao-noi-dung-marketing-facebook-tu-anh-telegram-ai-gemini"
tags: [n8n, automation, content-creation, ai-gemini, facebook-marketing, telegram-bot, no-code]
keywords: [n8n workflow facebook marketing, tự động hóa tạo nội dung facebook, ai gemini viết bài, telegram bot tạo nội dung, tự động hóa marketing không code, workflow n8n content creation]
---

# 🚀 **Tự Động Hóa Tạo Nội Dung Marketing Facebook Từ Ảnh qua Telegram + AI Gemini**

### **Giải pháp cho các sếp:**
Bạn đã bao giờ phải mất **giờ đồng hồ** để viết bài marketing cho Facebook từ một ảnh sản phẩm, logo hoặc hình ảnh thương hiệu? Hay phải **lặp đi lặp lại** các từ khóa, hashtag và call-to-action (CTA) mà không đảm bảo tính sáng tạo? **Workflow này sẽ thay bạn làm tất cả!**

Với **n8n + AI Gemini**, bạn chỉ cần **chia sẻ ảnh lên Telegram**, workflow sẽ tự động:
✅ **Viết bài marketing** (headline, nội dung chi tiết, hashtag, CTA) phù hợp với thương hiệu.
✅ **Xem xét và phê duyệt** nội dung qua Telegram (không cần chỉnh sửa thủ công).
✅ **Đăng bài lên Facebook** một cách tự động, tiết kiệm thời gian và tăng hiệu quả.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
### **✅ Tiết kiệm thời gian lên đến 90%**
Không cần viết bài từ đầu, AI Gemini tự động tạo nội dung **phù hợp với thương hiệu** chỉ trong vài giây.

### **✅ Nội dung chuyên nghiệp & cá nhân hóa**
- **Headline hấp dẫn** (ví dụ: *"Khám phá sản phẩm mới của chúng tôi – Giảm 50% chỉ trong tuần này!"*)
- **Nội dung chi tiết** (mô tả sản phẩm, lợi ích, cách sử dụng)
- **Hashtag phù hợp** (tự động tìm kiếm từ khóa hot)
- **CTA mạnh mẽ** (gợi ý hành động như *"Mua ngay"*, *"Đăng ký ngay"*)

### **✅ Quản lý dễ dàng qua Telegram**
- **Phê duyệt nội dung** chỉ bằng một cú nhấp chuột (APPROVE/REJECT).
- **Sửa đổi nhanh** nếu cần (AI sẽ tái xử lý theo yêu cầu).

### **✅ Đăng bài tự động lên Facebook**
Không cần copy-paste thủ công, nội dung được **tự động đăng** lên trang Facebook của bạn.

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:

### **1. Tài khoản & API Keys**
| **Dịch vụ**       | **Thông tin cần thiết**                          | **Lưu ý** |
|-------------------|--------------------------------------------------|-----------|
| **Telegram Bot**  | Token API (tạo từ [@BotFather](https://t.me/BotFather)) | Cần tạo bot riêng và thêm admin vào nhóm. |
| **OpenRouter API**| API Key (đăng ký tại [OpenRouter](https://openrouter.ai/)) | Chọn mô hình **`google/gemini-2.5-flash-lite`** (miễn phí). |
| **Facebook Page**  | **Access Token** (Graph API) + **Page ID** | Cần quyền **Page Admin** và **Marketing API Access**. |
| **n8n Self-Hosted** | VPS hoặc máy chủ riêng (gợi ý [TinoHost](https://tino.vn/)) | Đảm bảo RAM ≥ 2GB cho AI chạy ổn định. |

### **2. Cài đặt bổ sung**
- **Node LangChain** (đã tích hợp trong workflow, không cần cài thêm).
- **n8n Community Nodes** (cập nhật phiên bản mới nhất).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/6635](https://n8n.io/workflows/6635).
2. **Mở n8n Editor** → **Import** → Chọn file JSON vừa tải.
3. **Chọn phiên bản n8n** phù hợp (n8n 1.x hoặc 2.x).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** → **Create new workflow**.
2. **Nhấn "Import"** → **Paste JSON** từ [đây](https://n8n.io/workflows/6635) (copy toàn bộ mã).
3. **Chọn phiên bản n8n** và nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: Trigger from Telegram**
- **Cấu hình:**
  - **Credentials:** Chọn `telegramApi` (đã tạo trước).
  - **Webhook URL:** Lấy từ n8n (cấu hình trong **Settings → Webhooks**).
  - **Filter:** Chỉ kích hoạt khi có **photo hoặc text** (để trống để nhận tất cả).

#### **🔹 Node 2 & 3: Extract Telegram Metadata & Get Telegram File Info**
- **Không cần chỉnh**, workflow tự động lấy **file_id** và **chat_id** từ Telegram.

#### **🔹 Node 4 & 5: Build & Download Telegram Image**
- **Không cần chỉnh**, workflow tự động **tạo URL download** và **tải ảnh** từ Telegram.

#### **🔹 Node 6 & 7: Generate Marketing Content (AI Agent)**
- **Cấu hình AI:**
  - **Model:** Đã mặc định là `google/gemini-2.5-flash-lite` (không cần đổi).
  - **Prompt:** Workflow tự động xây dựng từ **caption** và **thương hiệu** (nếu có).
  - **Credentials:** Chọn `openRouterApi` (đã tạo trước).

#### **🔹 Node 8: Parse AI Output**
- **Không cần chỉnh**, workflow tự động **tách JSON** thành:
  - **Headline**
  - **Content**
  - **Hashtags**
  - **CTA**
  - **Approval ID** (mã duy nhất cho mỗi bài)

#### **🔹 Node 9 & 10: Approval Decision (If & Switch)**
- **Không cần chỉnh**, workflow tự động **kiểm tra** nội dung đã được phê duyệt hay chưa.

#### **🔹 Node 11-14: Telegram Interaction (Send for Approval)**
- **Cấu hình:**
  - **Credentials:** Chọn `telegramApi`.
  - **Message:** Workflow tự động gửi **headline + content** cho người dùng phê duyệt.
  - **Operation:** Đặt là `sendAndWait` (đợi phản hồi APPROVE/REJECT).

#### **🔹 Node 15: Publish Post to Facebook**
- **Cấu hình:**
  - **Method:** `POST`
  - **URL:** `https://graph.facebook.com/v19.0/{PAGE_ID}/feed`
  - **Headers:**
    - `Authorization: Bearer {ACCESS_TOKEN}`
    - `Content-Type: multipart/form-data`
  - **Body:**
    - `message`: `{content}`
    - `picture`: `{image_data}` (dữ liệu ảnh từ Telegram)
    - `name`: `{headline}`
    - `caption`: `{hashtags} {content}`

#### **🔹 Node 16: Notify Facebook Success**
- **Cấu hình:**
  - **Credentials:** `telegramApi`.
  - **Message:** `"Bài đã đăng thành công lên Facebook! 🎉"`

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với một ảnh mẫu:
   - Gửi ảnh lên Telegram bot.
   - Kiểm tra **AI có viết bài không?** (nếu không, kiểm tra **OpenRouter API Key**).
   - **Phê duyệt** nội dung qua Telegram (nhập `APPROVE`).
   - Kiểm tra **Facebook** xem bài đã đăng không.

2. **Bật Active workflow**:
   - Nhấn **Active** ở góc trên bên phải.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 1. Tối ưu AI với Prompt cá nhân hóa**
- **Thêm biến `brand_style`** vào prompt để AI viết bài phù hợp với **ngôn ngữ thương hiệu** của bạn.
  - Ví dụ:
    ```json
    {
      "brand_style": "Tôn trọng khách hàng, giọng điệu thân thiện, sử dụng từ khóa 'Chất lượng cao' và 'Dịch vụ tận tâm'"
    }
    ```
- **Cách làm:**
  - Thêm **Sticky Note** trước node **Generate Marketing Content**.
  - Điền vào `brand_style` như trên.

### **🔹 2. Lưu log tất cả bài viết**
- **Thêm node `Set`** sau **Publish Post to Facebook** để lưu:
  - **Headline**
  - **Content**
  - **Hashtags**
  - **Approval ID**
  - **Timestamp**
- **Gửi log lên Google Sheets/Notion** để theo dõi hiệu suất.

### **🔹 3. Gửi báo cáo tuần/Tháng**
- **Tạo workflow mới** kết hợp với **Google Sheets** để:
  - **Tính số bài đăng thành công**.
  - **Tính engagement (like, comment)** từ Facebook.
  - **Gửi báo cáo tự động** qua Telegram/Email.

### **🔹 4. Kết hợp với Slack/Email**
- **Thay thế Telegram** bằng **Slack** hoặc **Email** để phê duyệt nội dung.
- **Cách làm:**
  - Thay node `telegram` bằng `slack` hoặc `email`.
  - Cấu hình **credentials** tương ứng.

### **🔹 5. Xử lý lỗi tự động**
- **Thêm node `Set Error Handling`** để:
  - Nếu **Facebook API lỗi**, gửi thông báo Telegram.
  - Nếu **AI không trả lời**, tái xử lý với prompt khác.

---

## 📌 **Kết luận**
### **Workflow này giúp các sếp:**
✔ **Tiết kiệm thời gian** (không cần viết bài thủ công).
✔ **Tăng hiệu quả marketing** (nội dung chuyên nghiệp, tự động đăng).
✔ **Quản lý dễ dàng** (phê duyệt qua Telegram, theo dõi trên Facebook).

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Telegram + OpenRouter + Facebook**.
3. **Test với một ảnh** và **bật tự động hóa**!

**🚀 Còn chần chừ gì nữa? AI đã sẵn sàng viết bài cho bạn!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/6635)**
**💬 Có vấn đề? Hỏi tại [Community n8n](https://community.n8n.io/)**