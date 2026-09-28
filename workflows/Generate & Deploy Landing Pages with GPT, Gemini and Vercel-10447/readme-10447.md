---
title: "🚀 Tự Động Tạo & Deploy Landing Page Lên Vercel Bằng AI (GPT-4o-mini & Gemini)"
description: "Hướng dẫn cấu hình workflow n8n giúp biến ý tưởng văn bản thành landing page hoàn chỉnh, có hình ảnh độc quyền và live deploy trên Vercel chỉ trong vài phút."
slug: "tu-dong-tao-va-deploy-landing-page-voi-ai-va-vercel"
tags: [n8n, automation, ai, openai, google-gemini, vercel, landing-page]
keywords: [n8n workflow, tạo landing page bằng ai, deploy vercel tự động, gpt-4o-mini, google gemini, cloudinary]
---

# 🚀 Tự Động Tạo & Deploy Landing Page Lên Vercel Bằng AI (GPT-4o-mini & Gemini)

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thuê designer cắt HTML/CSS hay tốn hàng giờ đồng hồ kéo thả trên các công cụ làm landing page truyền thống mỗi khi cần dựng một trang web thử nghiệm ý tưởng (MVP)? 

Bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ mạnh mẽ mang tên **Generate & Deploy Landing Pages with GPT, Gemini and Vercel** do tác giả *Lachlan* xây dựng. Workflow này kết hợp sức mạnh đa phương thức (multimodal AI) để biến một câu lệnh văn bản (chat prompt) thành một trang landing page chuẩn responsive, đi kèm hình ảnh hero độc quyền và tự động publish live URL lên Vercel!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ gọi AI và deploy mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ ý tưởng thô sơ qua khung chat đến mã nguồn HTML hoàn chỉnh và link public.
- **Tích hợp AI thông minh:** Sử dụng OpenAI GPT-4o-mini để viết mã HTML/CSS tối ưu và Google Gemini để tạo hình ảnh minh họa chất lượng cao.
- **Quản lý phiên linh hoạt (Session Memory):** Cho phép các sếp chỉnh sửa lặp lại (ví dụ: *"làm chữ to lên"*, *"đổi ảnh nền khác"*) ngay trong cùng một phiên chat.
- **Deploy thần tốc:** Tự động đẩy code lên Vercel và trả về link live để chia sẻ với khách hàng hoặc đội ngũ ngay lập tức.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Đã cấu hình n8n Data Table với 2 cột: `sessionID` và `html`).
- **OpenAI Account & API Key** (Dùng cho node GPT-4o-mini sinh prompt ảnh và mã HTML).
- **Google Cloud Platform (GCP) / Gemini API Key** (Dùng cho node tạo ảnh Google Gemini). *Lưu ý: Có thể thay thế bằng DALL·E của OpenAI nếu thích đơn giản.*
- **Cloudinary Account** (Dùng làm cloud lưu trữ hình ảnh hero được generate ra).
- **Vercel Account & Bearer Token / Header Auth** (Dùng để thực hiện lệnh deploy tự động).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn hoặc copy trực tiếp mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Paste JSON** để nạp toàn bộ 20 nodes vào hệ thống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các phân đoạn (Step) xử lý từ tư duy AI đến hạ tầng cloud, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Step 1 - Quản lý bộ nhớ phiên (Memory):**
  - Tại node **Get memory for current session** và **Save HTML to Memory Table** (kiểu `dataTable`), hãy đổi tên bảng dữ liệu (ví dụ: `html_memory_mini_loveable`) thành tên Data Table thực tế đã tạo trong n8n của các sếp. Đảm bảo bảng có 2 cột `sessionID` và `html`.
- **Step 2 & 3 & 4 - Xử lý Hình ảnh (Gemini & Cloudinary):**
  - Node **Generate an image1** (`googleGemini`): Cung cấp credentials `googlePalmApi` chuẩn từ Google Cloud.
  - Node **Upload Image to Cloudinary** (`httpRequest`): Thay thế đoạn `<your_cloud_key>` trong đường dẫn URL HTTP request bằng Cloudinary cloud name thực tế của các sếp.
- **Step 5 - Sinh mã HTML:**
  - Node **Generate HTML (OpenAI)** (`openAi`): Cắm credentials `openAiApi` và có thể tùy chỉnh model (`gpt-4o-mini` hoặc `gpt-4o`) tùy thuộc vào độ phức tạp của trang web muốn tạo.
- **Step 7 - Deploy lên Vercel:**
  - Các node liên quan đến Vercel (`Deploy to Vercel`, `list deployments`, `Fetch Latest Deployment URL1`, `Make Deployment URL Public`,...) sử dụng chung credentials `httpHeaderAuth`. Các sếp cần cấu hình Header Authorization chứa Vercel API Token (Bearer Token) của mình.

#### 3. Kích hoạt ⚡️
- Sử dụng **Chat input** (`chatTrigger`) để gửi một câu lệnh thử nghiệm (Ví dụ: *"Tạo một landing page giới thiệu dịch vụ thiết kế nội thất tối giản"*).
- Bấm **Test step** hoặc **Execute Workflow** để kiểm tra toàn bộ luồng từ việc sinh ảnh, upload Cloudinary, tạo HTML cho đến khi nhận được link Vercel trả về ở node **Respond to Chat**.
- Sau khi test thành công, gạt công tắc **Active** góc trên bên phải để đưa workflow vào trạng thái vận hành tự động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat nội bộ:** Thay vì dùng giao diện chat mặc định của n8n, các sếp có thể đổi `chatTrigger` thành **Telegram Trigger** hoặc **Slack Trigger** để ra lệnh tạo landing page ngay trên điện thoại hoặc nhóm chat công ty.
- **Tự động dọn dẹp (Optional Cleanup Flow):** Workflow có sẵn một nhánh phụ trợ chuyên xóa các deployment cũ trên Vercel (chỉ giữ lại 2 bản gần nhất). Các sếp hãy cân nhắc bật nhánh này nếu sợ tài khoản Vercel bị tràn giới hạn project miễn phí.
- **Tùy biến Prompt HTML:** Tinh chỉnh system prompt bên trong node OpenAI sinh HTML để áp dụng riêng bộ nhận diện thương hiệu, màu sắc chủ đạo hoặc framework CSS (như Tailwind CSS) theo ý muốn doanh nghiệp.

---

### 📌 Kết luận
Workflow **Generate & Deploy Landing Pages with GPT, Gemini and Vercel** là một vũ khí cực kỳ lợi hại cho các mác-kê-tinh (marketer), lập trình viên tự do hay các nhà sáng lập startup muốn thử nghiệm thị trường (Validation MVP) với tốc độ ánh sáng. Hãy triển khai ngay trên hệ thống n8n của các sếp để tối ưu hóa năng suất làm việc từ hôm nay!