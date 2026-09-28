---
title: "🚀 **Tự Động Học Instagram Miễn Phí: Auto-Liker 24/7 với Phantombuster, GPT-4o & Cookie Rotation**"
description: "Workflow tự động hóa học Instagram bằng cách tự động like post mới từ hashtag cụ thể, tránh bị chặn với cookie rotation và GPT-4o. Giúp tăng engagement mà không cần code, hoạt động 24/7 với lịch trình tự động."
slug: "tieu-dong-ho-instagram-auto-liker-phantombuster-gpt-4o"
tags: [n8n, automation, social-media, instagram-growth, ai-driven, phantombuster, gpt-4o, cookie-rotation]
keywords: [tự động hóa instagram, auto liker instagram, phantombuster n8n, gpt-4o tự động hóa, cookie rotation instagram, tăng engagement instagram]
---

# 🚀 **Tự Động Học Instagram Miễn Phí: Auto-Liker 24/7 với Phantombuster, GPT-4o & Cookie Rotation**

### **💡 Bạn đã bao giờ mệt mỏi vì phải like post thủ công trên Instagram để tăng engagement cho tài khoản?**
Hay phải lo lắng về việc bị chặn vì like quá nhiều từ cùng một cookie? **Workflow này giải quyết tất cả!** Với sự kết hợp giữa **Phantombuster** (scrape post), **GPT-4o** (tạo hashtag mới), và **cookie rotation tự động**, bạn có thể **like hàng chục post mỗi ngày mà không bị chặn**, tất cả chỉ với một workflow tự động hóa trên **n8n**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Like hàng trăm post mỗi ngày mà không cần thủ công.
✅ **Tránh bị chặn**: Cookie rotation tự động thay đổi sau mỗi like.
✅ **Tăng engagement**: Like post mới từ hashtag liên quan, giúp tài khoản được ưa thích hơn.
✅ **Hoạt động 24/7**: Lịch trình tự động chạy theo thời gian bạn thiết lập.
✅ **Tối ưu hóa với AI**: GPT-4o tự động tạo hashtag mới để tránh bị flag.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Phantombuster** (để scrape post Instagram).
✔ **API Key OpenAI** (để sử dụng GPT-4o tạo hashtag).
✔ **Tài khoản Microsoft SharePoint** (để lưu cookie và dữ liệu đã like).
✔ **Cookie Instagram** (tải từ [Instagram Cookie Generator](https://instagram-cookie-generator.com/) hoặc tự tạo).
✔ **Tài khoản n8n** (cài đặt trên VPS hoặc dùng phiên bản cloud).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6765](https://n8n.io/workflows/6765).
- **Import vào n8n Editor**:
  - Mở n8n Workflow Editor.
  - Nhấn **Import** và chọn file JSON vừa tải.
  - Hoặc **copy/paste** JSON vào ô **Import Workflow**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Credentials (Bắt buộc)**
| Node | Credentials cần thiết | Ghi chú |
|------|----------------------|---------|
| **Phantombuster** | `phantombusterApi` | Tạo credential trong **n8n Credentials** với API Key từ Phantombuster. |
| **OpenAI (GPT-4o)** | `openAiApi` | Điền API Key từ tài khoản OpenAI. |
| **Microsoft SharePoint** | `microsoftSharePointOAuth2Api` | Cấu hình OAuth2 với tài khoản SharePoint. |

#### **🔹 Cấu hình SharePoint (Lưu cookie & dữ liệu)**
- **Tên file cookie**: `instagram_cookies.csv` (nên đặt trong thư mục chung).
- **Tên file đã like**: `instagram_posts_already_liked.csv` (để tránh like trùng).
- **Cấu hình SharePoint**:
  - **Upload CSV**: Đặt đường dẫn đến `instagram_cookies.csv`.
  - **Download/Update file**: Chỉnh tên file `instagram_posts_already_liked.csv`.

#### **🔹 Cấu hình GPT-4o (Tạo hashtag mới)**
- **Prompt mặc định**:
  ```plaintext
  Generate a new Instagram hashtag for [NICHE] niche. The hashtag should be trending and not too broad. Avoid banned or overused tags.
  ```
- **Sửa prompt** để phù hợp với ngành hàng của bạn (ví dụ: `niche: du lịch`, `niche: marketing`).

#### **🔹 Cấu hình Phantombuster (Scrape post)**
- **Hashtag Agent**: Điền hashtag mục tiêu (ví dụ: `#duhocvietnam`).
- **Autoliking Agent**: Chỉnh `ENV_MAX_POSTS_PER_HASHTAG` (mặc định là 12 post/ngày).
- **Rate Limiting**: Cấu hình **Wait nodes** để tránh bị chặn (mặc định 2h/cron).

#### **🔹 Cấu hình Lịch trình (Schedule Trigger)**
- **Cron Expression**: `0 0 */2 * * *` (chạy 2 lần/ngày, ví dụ 12h và 24h).
- **Test Run**: Nhấn **Run Workflow** để kiểm tra trước khi kích hoạt.

### **3. Kích hoạt ⚡️**
- **Test Run**: Chạy workflow với dữ liệu mẫu để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **🔹 Tăng hiệu quả với Slack/Telegram**
- Thêm **Node Slack/Telegram** để thông báo khi like thành công.
- Ví dụ:
  ```javascript
  // Node Code (thêm vào workflow)
  $node.success.data.forEach(post => {
    $node.next({
      text: `🔥 Like thành công post: ${post.url}`
    });
  });
  ```

### **🔹 Lưu log hoạt động**
- Thêm **Node Set** để lưu log vào SharePoint hoặc Google Sheets.
- Ví dụ:
  ```javascript
  // Node Code (lưu log)
  const logData = {
    timestamp: new Date().toISOString(),
    postUrl: $node.input.data.url,
    status: "success"
  };
  $node.next(logData);
  ```

### **🔹 Sử dụng nhiều cookie**
- Nếu có nhiều cookie, **tăng số lượng trong SharePoint** và điều chỉnh **Select Cookie** để chọn ngẫu nhiên.

### **🔹 Tăng số like/ngày**
- **Giảm thời gian Wait**: Từ 2h/cron xuống 1h.
- **Tăng `ENV_MAX_POSTS_PER_HASHTAG`** (nhưng không quá 15 post/ngày để tránh bị chặn).

---

## 📌 **Kết luận**
Workflow này giúp **tự động hóa hoàn toàn quá trình like Instagram**, tiết kiệm thời gian và tăng engagement cho tài khoản. **Không cần code, không bị chặn**, và hoạt động 24/7 với **GPT-4o + Phantombuster + Cookie Rotation**.

🚀 **Hãy áp dụng ngay và xem tài khoản Instagram của bạn được tăng trưởng như thế nào!**

---
**Cần hỗ trợ?** Liên hệ Plemeo tại [info@plemeo.de](mailto:info@plemeo.de) hoặc truy cập [plemeo.ai](https://plemeo.ai).