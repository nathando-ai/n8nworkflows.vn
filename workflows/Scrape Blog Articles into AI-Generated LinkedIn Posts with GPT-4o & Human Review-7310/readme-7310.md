---
title: "🚀 Tự Động Hoá Scrape Bài Blog → Tạo Bài Post LinkedIn AI + Xét Duyệt Con Người (GPT-4o + gotoHuman)"
description: "Workflow tự động hóa scrape bài viết từ blog n8n, tự động tạo bài post LinkedIn bằng GPT-4o, sau đó gửi cho con người xét duyệt trước khi đăng. Giúp tiết kiệm 8h/ngày, đảm bảo nội dung phù hợp brand và chính xác."
slug: "tieu-dong-hoa-scrape-blog-den-post-linkedin-ai-gotoHuman"
tags: [n8n, automation, no-code, ai-content, gotoHuman, linkedin-automation, gpt-4o, social-media]
keywords: [tự động hóa scrape blog, tạo bài post linkedin bằng ai, gotoHuman n8n, workflow n8n tự động, tự động hóa nội dung social media, gpt-4o cho linkedin]
---

# 🚀 **Scrape Blog → Tạo Post LinkedIn AI + Xét Duyệt Con Người (GPT-4o + gotoHuman)**

### **Giải pháp tự động hóa hoàn toàn cho việc chia sẻ tin tức từ blog n8n lên LinkedIn**
Hàng ngày, các sếp phải dành **từ 2-3 tiếng** để:
- Scan blog n8n để tìm bài mới.
- Tóm tắt nội dung và viết bài post LinkedIn.
- Xét duyệt nội dung trước khi đăng để đảm bảo **phù hợp brand** và **chính xác thông tin**.
- Tránh rủi ro khi AI tạo ra nội dung sai lệch hoặc không phù hợp.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Scrape** bài viết mới từ blog n8n.
✅ **Tóm tắt** bằng GPT-4o (mô hình mới nhất của OpenAI).
✅ **Tạo bài post LinkedIn** tự động.
✅ **Xét duyệt con người** trước khi đăng (tránh sai sót).
✅ **Đăng tự động** khi được phê duyệt.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **24/7 không gián đoạn**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8h/ngày** (từ việc scan, viết, xét duyệt thủ công).
- **Nội dung phù hợp brand** (con người kiểm tra trước khi đăng).
- **Tăng độ tin cậy** (tránh sai sót của AI).
- **Hoạt động liên tục** (không phụ thuộc vào giờ làm việc).
- **Tối ưu hóa SEO** (bài post được AI tối ưu từ bài viết gốc).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản gotoHuman** (dùng để xét duyệt nội dung).
✔ **API Key gotoHuman** (cần import template xét duyệt ID: `sMxevC9tSAgdfWsr6XIW`).
✔ **Tài khoản OpenAI** (để sử dụng GPT-4o).
✔ **Tài khoản LinkedIn** (đăng bài tự động).
✔ **VPS n8n** (để chạy workflow 24/7).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/7310](https://n8n.io/workflows/7310) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7310) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình gotoHuman**
1. **Cài đặt node gotoHuman** (nếu chưa có):
   - Mở **n8n Editor** → **Add Node** → Tìm `@gotohuman/n8n-nodes-gotohuman` và cài đặt.
2. **Tạo tài khoản gotoHuman** và lấy **API Key**.
3. **Import template xét duyệt**:
   - Vào [gotoHuman Dashboard](https://app.gotohuman.com/) → **Templates** → Nhập ID: `sMxevC9tSAgdfWsr6XIW` → Import.
4. **Cấu hình node `Human approval`**:
   - Chọn **Credentials** → Nhập **API Key** của gotoHuman.
   - Chọn **Review Template** là `"n8n news to post"`.

##### **B. Cấu hình OpenAI (GPT-4o)**
1. Vào node **`OpenAI Chat Model`** và **`OpenAI Chat Model1`**:
   - Chọn **Credentials** → Nhập **API Key OpenAI**.
   - Đảm bảo **Model** là `gpt-4o-mini` (hoặc `gpt-4o` nếu có budget).

##### **C. Cấu hình LinkedIn**
1. Vào node **`Create a post`**:
   - Chọn **Credentials** → Nhập **OAuth Token** của LinkedIn (cần tạo từ [LinkedIn Developer Portal](https://www.linkedin.com/developers/)).
   - **Lưu ý:** Node này cần **quyền đăng bài tự động** (cần cấp phép từ LinkedIn).

##### **D. Cấu hình Schedule Trigger**
- Node **`Schedule Trigger`** chạy hàng ngày (mặc định là 24h).
- **Lưu ý:** Theo ghi chú trong workflow, cần thay `<=24` thành `<=48` (hoặc `<=24` nếu muốn chạy chính xác 24h).

##### **E. Cấu hình Fetch Article (LLM-friendly)**
- Node **`Fetch Article (LLM-friendly)`** sử dụng **Jina.ai** để scrape nội dung.
- **Không cần cấu hình thêm** (n8n tự động lấy URL từ bài viết gốc).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **Manual Trigger** để kiểm tra workflow.
   - Kiểm tra:
     - AI có tóm tắt bài viết không?
     - Bài post LinkedIn có hợp lý không?
     - gotoHuman có nhận được yêu cầu xét duyệt không?
2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển **Status** từ **Inactive** → **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
#### **1. Tối ưu hóa prompt cho AI**
- **Cải thiện chất lượng bài post** bằng cách chỉnh sửa **prompt** trong node **`Draft LinkedIn Post`**.
- Ví dụ:
  ```json
  "prompt": "Tóm tắt bài viết này thành một bài post LinkedIn ngắn gọn (100-150 từ), phù hợp với brand n8n. Đảm bảo:
  - Nêu rõ **điểm mới** của bài viết.
  - Kết thúc bằng **call-to-action** (CTA) như: 'Bạn có thể tự động hóa gì bằng n8n không? Để lại comment!'.
  - Tránh lặp lại nội dung quá nhiều."
  ```

#### **2. Lưu log hoạt động**
- Thêm node **`stickyNote`** sau **`Human approval`** để ghi lại:
  - Thời gian bài viết được tạo.
  - Người xét duyệt.
  - Lời phản hồi (nếu có).

#### **3. Gửi báo cáo định kỳ**
- Sử dụng **node `set`** + **`scheduleTrigger`** để gửi **báo cáo tuần/Tháng** về:
  - Số bài viết được tạo.
  - Số bài được đăng.
  - Thời gian trung bình xét duyệt.

#### **4. Kết hợp với Slack/Telegram**
- Thêm node **`webhook`** để gửi thông báo:
  - Khi bài viết được tạo.
  - Khi bài viết được phê duyệt.
  - Khi bài viết bị từ chối (với lý do).

---

### 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi việc viết bài post LinkedIn thủ công, đồng thời **đảm bảo chất lượng** nhờ xét duyệt con người. **Chỉ cần cài đặt 1 lần**, workflow sẽ hoạt động tự động hàng ngày!

**🚀 Hành động ngay:**
1. **Cài đặt VPS n8n** (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test Run** trước khi bật chế độ tự động.

**Nếu có vấn đề, hãy comment bên dưới hoặc liên hệ support n8n/gotoHuman!** 💬

---