---
title: "🎬 Tự Động Hoạt Động: Tạo Video Tin Tức AI với HeyGen + Đăng Trên Tất Cả Mạng Xã Hội (Plug & Play)"
description: "Workflow tự động hóa AI hoàn chỉnh giúp các sếp tạo video tin tức chuyên nghiệp với avatar AI (HeyGen), viết caption tự động, và đăng lên Instagram, TikTok, YouTube, LinkedIn... chỉ trong vài giây. Giảm thời gian sản xuất nội dung xuống 0% và mở rộng phạm vi tiếp cận đến 100% mạng xã hội. Không cần code, chỉ cần copy/paste và chạy 24/7."
slug: "tay-dong-hoat-dong-tao-video-tin-tuc-ai-heygen-va-dang-tren-mang-xa-hoi"
tags: [n8n, automation, ai, marketing, social-media, heygen, openai, no-code]
keywords: [tự động hóa video tin tức AI, heygen n8n workflow, đăng video lên tất cả mạng xã hội tự động, tạo video avatar AI, tự động viết caption cho video, n8n ai automation]
---

# 🚀 **Tự Động Hoạt Động: Tạo Video Tin Tức AI với HeyGen + Đăng Trên Tất Cả Mạng Xã Hội**

### **🔥 Giải pháp cho các sếp bị "chìm" trong công việc viết video và đăng tải nội dung**
Hàng ngày, các sếp phải:
- **Tìm kiếm tin tức** từ Hacker News hoặc nguồn tin khác.
- **Viết kịch bản** cho video (hoặc thuê người viết).
- **Tạo video** từ đầu (hoặc thuê người tạo).
- **Chỉnh sửa caption** dài và ngắn.
- **Đăng tải lên 5-10+ mạng xã hội** khác nhau.
- **Quản lý lịch trình** để nội dung được đăng đúng thời điểm.

**Kết quả?** Thời gian và công sức bị "chìm" trong công việc thủ công, trong khi nội dung không được tối ưu hóa cho từng nền tảng. **Workflow này giải quyết tất cả!** Với AI và tự động hóa, các sếp chỉ cần **nhấp một nút**, workflow sẽ:
✅ **Tự động lấy tin tức** từ Hacker News (hoặc nguồn khác).
✅ **Viết kịch bản video** bằng AI (OpenAI).
✅ **Tạo video avatar AI** với HeyGen (người mẫu 3D siêu thực).
✅ **Viết caption dài và ngắn** tự động.
✅ **Tải video và caption lên Blotato** (hoặc dịch vụ tương tự).
✅ **Đăng tự động lên Instagram, TikTok, YouTube, LinkedIn, Twitter, Facebook, Pinterest, Threads, Bluesky...** (tất cả chỉ với một workflow).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và tính riêng tư.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** trong việc tạo và đăng nội dung.
- **Nội dung chuyên nghiệp** với avatar AI (HeyGen) và caption viết bởi AI (OpenAI).
- **Đăng tải tự động** lên **10+ mạng xã hội** chỉ với một workflow.
- **Hoạt động liên tục** (24/7) mà không cần can thiệp thủ công.
- **Tối ưu SEO** với caption và mô tả video được viết tự động.
- **Mở rộng phạm vi tiếp cận** đến người dùng trên tất cả các nền tảng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản HeyGen** (để tạo video avatar AI):
   - API Key của HeyGen (mua gói phù hợp).
   - [Đăng ký HeyGen](https://www.heygen.com/) (nếu chưa có).
2. **Tài khoản Blotato** (hoặc dịch vụ tương tự như Zapier/Integromat):
   - API Key hoặc credentials để upload video và caption.
   - [Đăng ký Blotato](https://blotato.com/) (nếu chưa có).
3. **Tài khoản OpenAI** (để viết kịch bản và caption):
   - API Key của OpenAI (mua gói phù hợp).
   - [Đăng ký OpenAI](https://platform.openai.com/) (nếu chưa có).
4. **Tài khoản mạng xã hội** (cần kết nối với Blotato):
   - Instagram, TikTok, YouTube, LinkedIn, Twitter, Facebook, Pinterest, Threads, Bluesky (tùy chọn).
5. **Nguồn tin tức** (cần cấu hình trong node `Fetch HN Front Page`):
   - Hacker News (sử dụng node `hackerNewsTool`).
   - Hoặc nguồn tin khác (ví dụ: RSS feed, API tin tức).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3538) và import vào n8n Editor.
- **Copy/paste JSON** từ link trên vào n8n Editor (tab "Import").

:::note[Lưu ý]
- **Không** cần chỉnh sửa toàn bộ workflow, chỉ cần **cấu hình các node quan trọng** như hướng dẫn bên dưới.
- Nếu sử dụng **n8n Cloud**, lưu ý kiểm tra giới hạn node và API calls.
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Dưới đây là **danh sách node cần cấu hình chi tiết**:

##### **A. Cấu hình nguồn tin tức (Fetch HN Front Page)**
- Node: `Fetch HN Front Page` (type: `hackerNewsTool`).
- **Cần thiết**:
  - Chọn **API Key** của Hacker News (nếu có) hoặc sử dụng API công khai.
  - Thiết lập **lịch trình lấy tin tức** (ví dụ: mỗi 6 giờ).

##### **B. Cấu hình AI Agent (Write Script)**
- Node: `AI Agent` (type: `agent`).
- **Cần thiết**:
  - Kết nối với **OpenAI API Key** (đã cấu hình trong `Setup Heygen`).
  - Thiết lập **prompt** cho AI viết kịch bản (ví dụ: *"Viết kịch bản video 60 giây về tin tức [TITLE] với phong cách chuyên nghiệp và hấp dẫn"*).

##### **C. Cấu hình HeyGen (Create Avatar Video)**
- Node: `Setup Heygen` (type: `set`).
- **Cần thiết**:
  - Điền **API Key HeyGen** vào biến `HEYGEN_API_KEY`.
  - Chọn **avatar mẫu** (ví dụ: avatar nam/nữ với phong cách chuyên nghiệp).
  - Thiết lập **thời lượng video** (ví dụ: 60 giây).

- Node: `Create Avatar Video` (type: `httpRequest`).
  - **Cần thiết**:
    - Điền **URL API HeyGen** để tạo video (tham khảo [HeyGen API Docs](https://docs.heygen.com/)).
    - Thiết lập **tham số input** như `script`, `avatar_id`, `voice_id`.

##### **D. Cấu hình OpenAI (Write Long/Short Caption)**
- Node: `Write Long Caption` và `Write Short Caption` (type: `openAi`).
- **Cần thiết**:
  - Kết nối với **OpenAI API Key**.
  - Thiết lập **prompt** cho caption dài (ví dụ: *"Viết mô tả chi tiết cho video tin tức [TITLE] với từ khóa SEO: [KEYWORDS]"*).
  - Thiết lập **prompt** cho caption ngắn (ví dụ: *"Viết caption ngắn gọn cho Instagram/TikTok: [TITLE]"*).

##### **E. Cấu hình Blotato (Upload & Publish)**
- Node: `Upload to Blotato` (type: `httpRequest`).
  - **Cần thiết**:
    - Điền **API Key Blotato** (hoặc credentials).
    - Thiết lập **URL upload video** và **tham số file**.
  - Node: `Upload to Blotato - Image` (type: `httpRequest`).
    - **Cần thiết**: Upload **thumbnail** cho video (nếu cần).

- Các node **Publish via Blotato** (ví dụ: `[Instagram] Publish via Blotato`):
  - **Cần thiết**:
    - Chọn **mạng xã hội** muốn đăng (ví dụ: Instagram, TikTok).
    - Điền **credentials** của tài khoản mạng xã hội (nếu Blotato hỗ trợ).
    - Thiết lập **thời gian đăng** (ví dụ: ngay lập tức hoặc theo lịch).

##### **F. Cấu hình Schedule Trigger**
- Node: `Schedule Trigger` (type: `scheduleTrigger`).
  - **Cần thiết**:
    - Chọn **lịch trình** (ví dụ: mỗi ngày lúc 8h sáng).
    - Thiết lập **timezone** phù hợp.

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với **1 tin tức mẫu**:
   - Chạy workflow với **1 bài tin** từ Hacker News.
   - Kiểm tra **video avatar**, **caption**, và **đăng tải** lên mạng xã hội.
2. **Bật Active workflow**:
   - Sau khi test thành công, **bật workflow** để chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Telegram/Slack**:
   - Thêm node **Slack/Telegram** để thông báo khi video được tạo/xong.
2. **Lưu log hoạt động**:
   - Sử dụng node **Set** để lưu **URL video**, **caption**, và **thời gian đăng** vào Google Sheets.
3. **Tối ưu caption cho SEO**:
   - Sử dụng **prompt AI** với từ khóa SEO (ví dụ: *"Viết caption với từ khóa: 'tự động hóa n8n', 'HeyGen AI', 'video tin tức'"*).
4. **Chọn avatar phù hợp**:
   - Thử nghiệm với **nhiều avatar mẫu** của HeyGen để chọn phong cách phù hợp với brand.
5. **Đăng tải theo lịch trình**:
   - Sử dụng **Blotato** hoặc **Zapier** để **đăng video vào thời điểm tối ưu** (ví dụ: sáng sớm hoặc buổi tối).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn chỉnh** để các sếp:
✔ **Tạo video tin tức AI** chỉ trong vài giây.
✔ **Đăng tải tự động** lên **tất cả mạng xã hội**.
✔ **Tiết kiệm thời gian** và **tăng hiệu quả marketing**.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test run** với 1 tin tức mẫu.
3. **Bật workflow** và để nó chạy tự động mỗi ngày!

**🚀 Cùng tự động hóa công việc của mình ngay hôm nay!** Nếu có vấn đề, các sếp có thể tham khảo [n8n Community](https://community.n8n.io/) hoặc liên hệ với tác giả [Sam Yassine](https://n8n.io/workflows/3538) để hỗ trợ.

---
**💡 Lưu ý cuối cùng**:
- Nếu **HeyGen/Blotato** có giới hạn API, các sếp nên **cập nhật tài khoản** để workflow không bị gián đoạn.
- **Monitor workflow** thường xuyên để đảm bảo hoạt động ổn định.