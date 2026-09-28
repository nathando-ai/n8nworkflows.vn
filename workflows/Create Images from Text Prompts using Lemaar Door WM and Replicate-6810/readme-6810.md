---
title: "🎨 Tự Động Hoá Sáng Tạo Hình Ảnh Từ Văn Bản Bằng AI (Lemaar-Door WM + Replicate) - Không Cần Code"
description: "Tự động hóa quy trình tạo hình ảnh từ văn bản bằng AI tiên tiến Lemaar-Door WM thông qua API Replicate, tiết kiệm thời gian và nâng cao hiệu suất sáng tạo nội dung. Workflow này hoạt động hoàn toàn tự động, không cần viết code."
slug: "tu-dong-hoa-tao-hinh-anh-tu-van-ban-bang-ai"
tags: [n8n, automation, ai-generate-images, replicate-api, content-creation, multimodal-ai]
keywords: [n8n workflow tạo hình ảnh từ văn bản, tự động hóa sáng tạo nội dung AI, Lemaar-Door WM, Replicate API, không cần code, tự động hóa nội dung marketing]
---

# 🚀 **Tự Động Hoá Sáng Tạo Hình Ảnh Từ Văn Bản Bằng AI (Lemaar-Door WM + Replicate)**

## 📌 **Nỗi Đau Của Các Sếp**
Các sếp thường phải mất nhiều thời gian để:
- **Tìm kiếm và chọn hình ảnh phù hợp** cho bài viết, bài đăng mạng xã hội hay quảng cáo.
- **Chỉnh sửa và tối ưu hóa hình ảnh** để phù hợp với nội dung.
- **Đợi lâu** khi sử dụng các công cụ AI tạo hình ảnh truyền thống (chậm, không ổn định).
- **Không có sự tự động hóa** để tạo hình ảnh từ văn bản một cách nhanh chóng và chính xác.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động hóa quy trình tạo hình ảnh từ văn bản bằng AI tiên tiến **Lemaar-Door WM** thông qua **API Replicate**, giúp các sếp tiết kiệm thời gian và nâng cao hiệu suất sáng tạo nội dung.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tạo hình ảnh từ văn bản chỉ trong vài giây, không cần chờ đợi.
- **Chất lượng cao**: Hình ảnh được sinh ra bởi AI tiên tiến **Lemaar-Door WM**, phù hợp với mọi nội dung.
- **Tự động hóa hoàn toàn**: Không cần viết code, chỉ cần nhập văn bản và kích hoạt workflow.
- **Cá nhân hóa**: Tùy chỉnh kích thước, phong cách và các tham số khác để phù hợp với dự án.
- **Hoạt động liên tục**: Workflow có thể chạy 24/7 trên VPS, tự động tạo hình ảnh theo lịch trình.
- **Dễ dàng mở rộng**: Kết hợp với Slack, Email hoặc Google Drive để tự động chia sẻ kết quả.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Replicate API**:
   - Đăng ký tại [Replicate](https://replicate.com/) và lấy **API Token**.
   - [Hướng dẫn lấy API Token](https://replicate.com/docs/api-tokens).
2. **Workflow n8n**:
   - Cài đặt n8n trên máy chủ hoặc VPS (self-hosted) để chạy 24/7.
   - [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/).
3. **Tham số tùy chỉnh (optional)**:
   - Văn bản (prompt) để tạo hình ảnh.
   - Tham số tùy chỉnh như kích thước, seed, hoặc các lựa chọn khác (nếu cần).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/6810](https://n8n.io/workflows/6810).
- **Nhấn vào "Import"** trong n8n Editor và chọn file JSON.
- **Hoặc copy/paste** JSON vào ô "Import from JSON" và nhấn "Import".

#### 2. **Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **13 node** chính, các sếp cần chú ý cấu hình các node sau:

##### **a. Node "Set API Token"**
- **Mục đích**: Cấu hình token API của Replicate.
- **Cách làm**:
  - Mở node này và thay thế `'YOUR_REPLICATE_API_TOKEN'` bằng **API Token** của bạn.
  - **Lưu ý**: Token này **không được chia sẻ** với ai cả, vì nó liên quan đến tài khoản Replicate.

##### **b. Node "Set Other Parameters"**
- **Mục đích**: Cấu hình các tham số đầu vào cho mô hình AI.
- **Cách làm**:
  - **Tham số bắt buộc**:
    - `prompt`: Văn bản mô tả hình ảnh cần tạo (ví dụ: *"A futuristic city at night with neon lights"*).
  - **Tham số tùy chọn** (nếu cần):
    - `width`, `height`, `seed`, `go_fast`, `extra_lora`, v.v.
  - **Gợi ý**:
    - Để mặc định các tham số khác nếu chưa rõ, sau đó thử nghiệm.
    - Tham khảo [Detailed Parameter Guide](https://replicate.com/creativeathive/lemaar-door-wm) để tùy chỉnh.

##### **c. Node "Create Other Prediction"**
- **Mục đích**: Gửi yêu cầu tạo hình ảnh đến API Replicate.
- **Lưu ý**:
  - Node này sẽ trả về **prediction ID** để theo dõi trạng thái.
  - **Không cần chỉnh sửa** nếu đã cấu hình token và tham số đúng.

##### **d. Node "Wait 5s" & "Wait 10s"**
- **Mục đích**: Chờ đợi API hoàn thành việc tạo hình ảnh.
- **Lưu ý**:
  - Workflow sẽ tự động kiểm tra trạng thái và tiếp tục khi hình ảnh hoàn tất.
  - **Không cần chỉnh sửa** trừ khi cần thay đổi thời gian chờ.

##### **e. Node "Is Complete?" & "Has Failed?"**
- **Mục đích**: Kiểm tra trạng thái của yêu cầu.
- **Lưu ý**:
  - Node này sẽ **lọc** kết quả thành hai đường dẫn:
    - **Thành công**: Nếu hình ảnh đã tạo xong.
    - **Thất bại**: Nếu có lỗi xảy ra.

##### **f. Node "Display Result"**
- **Mục đích**: Hiển thị kết quả cuối cùng.
- **Lưu ý**:
  - Kết quả sẽ bao gồm **URL download** hình ảnh và các thông tin liên quan.
  - Các sếp có thể **tùy chỉnh** cách hiển thị kết quả (ví dụ: gửi qua Email, Slack, hoặc lưu vào Google Drive).

##### **g. Node "Log Request" (Code Node)**
- **Mục đích**: Ghi log để theo dõi và debug.
- **Lưu ý**:
  - Node này **không cần chỉnh sửa** trừ khi các sếp muốn thêm logic logging riêng.

#### 3. **Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **"Run"** để thử nghiệm với một **văn bản mẫu** (prompt).
  - Kiểm tra kết quả trong tab **"Executions"**.
- **Bật Active**:
  - Sau khi test thành công, chuyển workflow sang **trạng thái "Active"**.
  - **Lưu ý**: Workflow sẽ tự động chạy khi kích hoạt **Manual Trigger**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH SỬ DỤNG HIỆU QUẢ]
1. **Tự động tạo hình ảnh cho nội dung**:
   - Kết hợp với **Google Sheets** hoặc **Notion** để tự động tạo hình ảnh cho mỗi bài viết.
   - Ví dụ: Khi có một bài viết mới được thêm vào Google Sheets, workflow sẽ tự động tạo hình ảnh phù hợp.

2. **Gửi kết quả qua Slack/Email**:
   - Sử dụng **node Slack** hoặc **node Email** để tự động thông báo kết quả cho team.
   - Ví dụ: Khi hình ảnh tạo xong, workflow sẽ gửi **URL download** qua Slack.

3. **Lưu log và báo cáo**:
   - Sử dụng **node Set** hoặc **node Code** để lưu log vào **Google Drive** hoặc **Database**.
   - Tạo **báo cáo định kỳ** về số lượng hình ảnh tạo thành công/thất bại.

4. **Tùy chỉnh kích thước và phong cách**:
   - Thử nghiệm với các tham số như `width`, `height`, `seed` để tạo ra phong cách khác nhau.
   - Ví dụ: Sử dụng `seed` để tạo ra cùng một hình ảnh với các biến thể nhỏ.

5. **Kết hợp với LLM (Large Language Model)**:
   - Sử dụng **node LLM** (nếu có) để tự động tạo **prompt** từ văn bản đầu vào.
   - Ví dụ: Nếu đầu vào là *"Bài viết về du lịch Hà Nội"*, workflow sẽ tự động tạo prompt như *"A vibrant street scene in Hanoi at sunset with traditional architecture"*.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc tạo hình ảnh thủ công, đồng thời **nâng cao chất lượng nội dung** bằng cách sử dụng AI tiên tiến. Với **tự động hóa hoàn toàn**, các sếp có thể:
✅ **Tạo hình ảnh từ văn bản chỉ trong vài giây**.
✅ **Tùy chỉnh kích thước, phong cách và tham số**.
✅ **Hoạt động 24/7** trên VPS, không cần can thiệp thủ công.
✅ **Kết hợp với các dịch vụ khác** (Slack, Email, Google Drive) để tối ưu hóa quy trình làm việc.

**Hãy thử nghiệm ngay và tự động hóa quy trình sáng tạo của mình!** 🚀

---
**🔗 Tài Liệu Tham Khảo**:
- [Replicate API Docs](https://replicate.com/docs)
- [Model Lemaar-Door WM](https://replicate.com/creativeathive/lemaar-door-wm)
- [n8n Documentation](https://docs.n8n.io/)
- [Youtube của Yaron Been](https://www.youtube.com/@YaronBeen/videos) (Tác giả workflow)
- [LinkedIn của Yaron Been](https://www.linkedin.com/in/yaronbeen/) (Hỗ trợ kỹ thuật)