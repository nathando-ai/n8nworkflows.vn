---
title: "🚀 Tự Động Hóa Tóm Tắt RSS Hàng Ngày Với Gemini AI + Slack + Chia Sẻ X (Twitter) - Cách Sử Dụng Chi Tiết"
description: "Workflow tự động hóa lấy RSS feed hàng ngày, tóm tắt nội dung bằng AI Gemini, gửi thông báo Slack và cho phép chia sẻ bài viết trên X (Twitter) chỉ với 1 nút. Giúp tiết kiệm thời gian theo dõi tin tức, tăng hiệu quả công việc cho các sếp và content creator."
slug: "tieu-dong-hoa-rss-gemini-slack-x"
tags: [n8n, automation, ai-summarization, slack-integration, rss-feed, google-gemini, content-creation]
keywords: [tự động hóa rss với gemini ai, gửi tin tức slack, chia sẻ bài viết x từ slack, workflow n8n rss, tự động hóa content creation]
---

# 🚀 **Tự Động Hóa Tóm Tắt RSS Hàng Ngày Với Gemini AI + Slack + Chia Sẻ X (Twitter)**

### **Giải pháp hoàn hảo cho các sếp và content creator muốn:**
- **Tiết kiệm thời gian** theo dõi hàng trăm nguồn tin tức hàng ngày.
- **Nhận tóm tắt AI** chất lượng cao từ bài viết dài bằng Gemini.
- **Chia sẻ bài viết** trên X (Twitter) chỉ với 1 cú nhấp chuột từ Slack.
- **Hoạt động tự động** 24/7 mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Với chi phí thấp nhưng hiệu suất cao, các sếp có thể lựa chọn:
👉 **[VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý nhanh cho AI Gemini)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần phải đọc hàng trăm bài viết mỗi ngày.
✅ **Tóm tắt AI chất lượng**: Gemini tự động tóm tắt nội dung chính của bài viết.
✅ **Gửi thông báo Slack**: Nhận tin tức mới ngay trên Slack, không bỏ lỡ bất kỳ tin tức nào.
✅ **Chia sẻ X (Twitter) dễ dàng**: Chỉ cần nhấn nút trong Slack để chia sẻ bài viết.
✅ **Hoạt động tự động**: Workflow chạy hàng ngày mà không cần can thiệp.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Slack**:
   - Một **Slack App** đã được tạo và cấp quyền `chat:write` (hướng dẫn [tại đây](https://api.slack.com/apps)).
   - **API Token** của Slack (được gọi là `slackApi` trong workflow).

2. **API Key Google Gemini**:
   - **Tài khoản Google Cloud** và **API Key** từ [Google AI Studio](https://aistudio.google.com/api-keys).
   - Đăng ký và cấp quyền cho **Gemini API** (mã `googlePalmApi` trong workflow).

3. **Danh sách RSS Feed**:
   - Các URL RSS của các nguồn tin tức mà các sếp muốn theo dõi (cấu hình trong **node `Config`**).

4. **(Tùy chọn) Sub-workflow chia sẻ X (Twitter)**:
   - Nếu muốn chia sẻ bài viết trên X, cần một **sub-workflow** riêng (có thể import từ [đây](https://n8n.io/workflows/11813) hoặc tự tạo).

---

## 🚀 **Cách Import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/11813) (ấn `Export` trên canvas).
- **Nhấn `Import`** trong n8n Editor và chọn file JSON.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Credentials**
- **Slack**:
  - Mở node **"Send a message"** → Chọn `slackApi` → Điền **API Token** từ Slack App.
  - Chọn **Channel** hoặc **User** muốn nhận thông báo.

- **Google Gemini**:
  - Mở node **"Google Gemini Chat Model"** → Chọn `googlePalmApi` → Điền **API Key** từ Google AI Studio.

#### **B. Cấu hình RSS Feed**
- Mở node **"Config"** → Sửa đổi tham số `rssUrls` để thêm/diệt URL RSS:
  ```json
  {
    "rssUrls": [
      "https://example.com/rss-feed-1",
      "https://example.com/rss-feed-2"
    ],
    "takeCount": 5  // Số bài viết lấy từ mỗi RSS (mặc định 5)
  }
  ```
  - **Lưu ý**: Các sếp có thể điều chỉnh `takeCount` để lấy nhiều/n้อย bài viết hơn.

#### **C. Cấu hình AI Agent (Tùy chọn)**
- Node **"AI Agent (Access URL)"** sử dụng **LangChain Agent** để gọi API Gemini.
- Các sếp có thể chỉnh sửa **Prompt** trong node **"Format Request"** để điều chỉnh cách AI tóm tắt:
  ```json
  {
    "prompt": "Tóm tắt bài viết này trong 3 câu ngắn gọn, nhấn mạnh điểm chính."
  }
  ```

#### **D. Sub-workflow chia sẻ X (Twitter) (Nếu có)**
- Nếu muốn chia sẻ bài viết trên X, cần một **sub-workflow** riêng (ví dụ: sử dụng **Twitter API**).
- Node **"Call Sub-workflow"** sẽ gọi sub-workflow này khi người dùng nhấn nút chia sẻ trong Slack.

#### **E. Kích hoạt Schedule Trigger**
- Node **"Schedule Trigger"** sẽ chạy workflow hàng ngày (mặc định là **lúc 8h sáng**).
- Các sếp có thể chỉnh sửa thời gian trong node này:
  - **Cron expression**: `0 8 * * *` (8h sáng hàng ngày).

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn `Run` để kiểm tra workflow với dữ liệu mẫu.
   - Kiểm tra Slack để xem thông báo có xuất hiện không.

2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Lọc RSS Feed theo từ khóa**:
   - Sử dụng node **"Filter Rss Feeds"** (Code) để chỉ lấy bài viết chứa từ khóa cụ thể (ví dụ: "AI", "n8n").

2. **Gửi báo cáo định kỳ**:
   - Thêm node **Google Sheets** hoặc **Email** để gửi báo cáo tổng hợp hàng tuần.

3. **Tích hợp với Notion/Google Docs**:
   - Sử dụng node **Notion API** hoặc **Google Docs** để lưu tóm tắt bài viết vào tài liệu.

4. **Cập nhật Slack Bot**:
   - Thay đổi avatar và tên bot Slack để phù hợp với brand của công ty.

5. **Optimize AI Prompt**:
   - Chỉnh sửa **Prompt** trong node **"Format Request"** để AI tóm tắt theo phong cách riêng (ví dụ: ngắn gọn, chuyên nghiệp, hoặc hài hước).

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp và content creator muốn tự động hóa việc theo dõi tin tức, tóm tắt bằng AI và chia sẻ trên X (Twitter) một cách dễ dàng. **Không cần code**, chỉ cần cấu hình vài bước là có thể tiết kiệm **hàng giờ mỗi ngày**!

👉 **Hãy import ngay và bắt đầu tự động hóa công việc của mình!**
👉 **Có vấn đề?** Đăng ký [VPS n8n](https://tino.vn/vps-n8n?affid=388) để workflow chạy ổn định 24/7.

---
**Chúc các sếp thành công!** 🚀