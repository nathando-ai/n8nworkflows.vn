---
title: "🎬 **Tự Động Hóa Tạo & Chỉnh Sửa Clip Video AI Từ Text/Nghĩa Lời - Grok Imagine Video (n8n + Grok 4.1 Fast)**"
description: "Workflow tự động hóa hoàn toàn bằng n8n giúp các sếp tạo và chỉnh sửa clip video AI từ yêu cầu bằng văn bản hoặc hình ảnh chỉ trong vài giây, với chất lượng cao và không cần kỹ năng code. Giúp tiết kiệm thời gian lên tới 90% so với cách làm thủ công."
slug: "tay-dong-hoa-tao-chinh-sua-clip-video-ai-grok-imagine"
tags: [n8n, automation, ai-chatbot, grok-4-1-fast, content-creation, video-editing]
keywords: [n8n workflow video ai, tự động hóa tạo video từ text, grok imagine video, chatbot video editing, n8n + langchain, tự động hóa marketing]
---

# 🚀 **Tạo & Chỉnh Sửa Clip Video AI Từ Yêu Cầu Văn Bản - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Trong Tạo Video**
Các sếp thường phải mất **giờ đồng hồ** để:
- **Tìm kiếm và chọn hình ảnh** phù hợp cho video.
- **Chỉnh sửa video thủ công** trên Premiere Pro/CapCut, mất thời gian và dễ sai sót.
- **Tạo video từ text** bằng cách phải gọi API hoặc sử dụng công cụ phức tạp.
- **Đợi kết quả** vì quá trình xử lý diễn ra đồng bộ (không async).

**Workflow này giải quyết tất cả!** Với **AI Grok Imagine Video** kết hợp **n8n**, các sếp chỉ cần **gửi yêu cầu bằng văn bản** (hoặc upload hình ảnh), hệ thống sẽ tự động:
✅ **Tạo video từ text** (Text-to-Video).
✅ **Chỉnh sửa video** theo yêu cầu (Edit Video).
✅ **Tạo video từ hình ảnh** (Image-to-Video).
✅ **Trả về kết quả** trong thời gian **ít nhất 10 giây** (do async processing).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 90%** so với cách làm thủ công.
- **Chất lượng video cao** do sử dụng **Grok 4.1 Fast** (AI tiên tiến của xAI).
- **Tự động hóa hoàn toàn** - không cần can thiệp người dùng giữa quá trình.
- **Cá nhân hóa video** theo từng yêu cầu cụ thể (chỉnh sửa, thêm hiệu ứng, thay đổi âm nhạc...).
- **Hoạt động 24/7** - workflow chạy tự động khi có yêu cầu mới.
- **Dễ dàng mở rộng** - kết nối với Slack/Telegram, lưu log, hoặc gửi báo cáo định kỳ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản OpenRouter** (để sử dụng **Grok 4.1 Fast**):
   - [Đăng ký OpenRouter](https://openrouter.ai/) và lấy **API Key**.
   - Cấu hình **credentials** trong n8n với tên: `openRouterApi`.
   - Tham số `model`: `x-ai/grok-4.1-fast`.

2. **Tài khoản Fal.run** (để xử lý API video):
   - [Đăng ký Fal.run](https://fal.run/) và lấy **API Key** (nếu có).
   - Cấu hình **credentials** trong n8n với tên: `httpHeaderAuth` (sử dụng **Header Auth** với header `Authorization: Bearer <API_KEY>`).

3. **FTP Server** (để upload hình ảnh tạm thời):
   - Các sếp có thể dùng **BunnyCDN** (miễn phí) hoặc VPS riêng.
   - Cấu hình **credentials** trong n8n với tên: `ftp` (tham số `host`, `port`, `username`, `password`).

4. **Workflow phụ (nếu chưa có)**:
   - Workflow này gọi **3 workflow phụ** để xử lý:
     - `Run Text-to-Video`
     - `Run Image-to-Video`
     - `Run Video-to-Video`
   - Nếu chưa có, các sếp có thể **tạo mới** hoặc sử dụng [template của Davide](https://n8n.io/workflows/13182).

5. **N8n Self-hosted** (khuyến nghị):
   - Để workflow hoạt động 24/7 ổn định, các sếp nên **cài n8n trên VPS riêng**.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13182](https://n8n.io/workflows/13182).
- Trong **n8n Editor**, nhấn **Import** và chọn file JSON tải xuống.
- **Hoặc copy/paste** toàn bộ JSON vào **Import Workflow** (tab bên trái).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này **phức tạp** vì sử dụng **Agent + Async Processing**, nên các sếp cần chú ý:

##### **A. Cấu Hình Credentials**
- **OpenRouter (Grok 4.1 Fast)**:
  - Node: `Grok 4.1 Fast` (type: `lmChatOpenRouter`).
  - Điền `API Key` vào `openRouterApi` (credentials).
  - Tham số `model` đã được đặt sẵn là `x-ai/grok-4.1-fast`.

- **Fal.run (HTTP Header Auth)**:
  - Các node `Text to Video`, `Image to Video`, `Edit Video` (type: `httpRequest`).
  - Cấu hình `httpHeaderAuth` với header:
    ```json
    {
      "Authorization": "Bearer YOUR_FAL_RUN_API_KEY"
    }
    ```
  - **Lưu ý**: Nếu không có API Key, các sếp có thể **bỏ qua** và sử dụng **URL API công khai** (nếu có).

- **FTP (Upload Hình Ảnh)**:
  - Node: `Upload image` (type: `ftp`).
  - Điền thông tin FTP vào `ftp` credentials (host, port, username, password).
  - Tham số `path` đã được đặt sẵn: `=/n3wstorage/test/{{ $binary.data0.fileName }}`.

##### **B. Cấu Hình Agent (Grok Imagine Video Agent)**
- Node: `Grok Imagine Video Agent` (type: `agent`).
  - Agent này **xác thực yêu cầu** từ người dùng và **lựa chọn công cụ** (Text-to-Video, Image-to-Video, Edit Video).
  - **Lưu ý**:
    - Nếu agent **không hoạt động**, kiểm tra:
      - `Grok 4.1 Fast` có trả về kết quả hợp lệ không?
      - Các `HTTP Request` (Fal.run) có kết nối thành công không?
      - Tham số `input` của agent có đúng định dạng không?

##### **C. Cấu Hình Async Processing (Wait & Poll)**
- Workflow sử dụng **cách thức "Wait + Poll"** để kiểm tra trạng thái xử lý video:
  - Các node `Get status`, `Get status1`, `Get status2` (type: `httpRequest`) **lặp lại** để kiểm tra trạng thái video qua `requestId`.
  - **Lưu ý**:
    - Thay đổi thời gian `Wait 10 sec.` nếu video xử lý chậm hơn (ví dụ: 20 giây).
    - Kiểm tra **URL API** của Fal.run để đảm bảo `Get status` trả về dữ liệu chính xác.

##### **D. Cấu Hình Trigger (When Chat Message Received)**
- Node: `When chat message received` (type: `chatTrigger`).
  - Đây là **điểm bắt đầu** của workflow.
  - Các sếp cần **kết nối** nó với **chatbot** (Slack, Discord, Telegram, hoặc Webhook).
  - **Lưu ý**:
    - Nếu sử dụng **Slack**, cần cấu hình `Slack App` và `Webhook URL`.
    - Nếu sử dụng **Telegram**, cần lấy `Webhook URL` từ BotFather.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi yêu cầu **text** hoặc **upload hình ảnh** vào chatbot.
   - Kiểm tra:
     - Agent có phân loại yêu cầu (Text-to-Video, Image-to-Video, Edit Video) không?
     - Video có được tạo/chỉnh sửa thành công không?
     - URL video có trả về không?

2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển workflow từ **Draft** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM TIẾP THEO]
1. **Kết Nối Với Slack/Telegram**:
   - Sử dụng node `Slack` hoặc `Telegram Bot` để nhận yêu cầu và trả kết quả.
   - Ví dụ: Khi video hoàn thành, gửi **thông báo + URL video** về Slack.

2. **Lưu Log & Theo Dõi**:
   - Sử dụng node `Set` hoặc `Google Sheets` để lưu **lịch sử yêu cầu**.
   - Ví dụ: Lưu `requestId`, `yêu cầu`, `URL video`, `thời gian xử lý`.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node `Execute Workflow` + `Schedule` để gửi **báo cáo tổng hợp** về số video tạo/chỉnh sửa hàng ngày.

4. **Tối Ưu Thời Gian Chờ**:
   - Nếu video xử lý lâu, tăng thời gian `Wait` (ví dụ: từ 10s → 30s).
   - Kiểm tra **API rate limit** của Fal.run để tránh bị chặn.

5. **Sử Dụng Multiple Agents**:
   - Tạo **nhiều agent** khác nhau để xử lý các loại yêu cầu khác nhau (ví dụ: Agent cho video marketing, Agent cho video tutorial).
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa tạo và chỉnh sửa video AI** một cách **siêu nhanh, chính xác và không cần code**. Với **Grok 4.1 Fast** và **n8n**, các sếp có thể:
✔ **Tiết kiệm thời gian** lên tới 90% so với cách làm thủ công.
✔ **Tạo video từ text/hình ảnh** chỉ trong vài giây.
✔ **Chỉnh sửa video** theo yêu cầu bằng văn bản.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay!**
1. **Cài n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình credentials.
3. **Test với yêu cầu mẫu** và bật workflow.
4. **Kết nối với Slack/Telegram** để sử dụng dễ dàng hơn.

👉 **Xem video hướng dẫn chi tiết** từ Davide trên [YouTube của anh](https://youtube.com/@n3witalia).

---
**Chúc các sếp thành công với tự động hóa video AI!** 🚀