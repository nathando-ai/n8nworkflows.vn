---
title: "🎙️ Tự Động Chuyển Bài Blog Sang Tập Podcast Với GPT-4o, ElevenLabs & Google Drive - Không Cần Code!"
description: "Workflow tự động hóa chuyển đổi bài viết blog thành tập podcast chuyên nghiệp với giọng nói AI, âm thanh chất lượng cao và phân phối tự động qua Google Drive. Giúp các sếp tiết kiệm 10+ giờ/tháng, đồng thời mở rộng nội dung sang định dạng âm thanh để thu hút khán giả mới."
slug: "tieu-dong-chuyen-bai-blog-sang-podcast-voi-gpt-4o"
tags: [n8n, automation, content-creation, ai-multimodal, google-drive, elevenlabs, gpt-4o]
keywords: [tự động hóa podcast, chuyển bài blog sang âm thanh, n8n workflow podcast, AI tạo giọng nói, tự động hóa nội dung, podcast tự động]
---

# 🚀 **Tự Động Chuyển Bài Blog Sang Tập Podcast Với AI - Không Cần Code!**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm 10+ giờ/tháng** viết và thu âm podcast thủ công.
- **Mở rộng nội dung** sang định dạng âm thanh để thu hút khán giả mới (người lắng nghe thay vì đọc).
- **Chất lượng chuyên nghiệp** với giọng nói AI tự nhiên (thông qua ElevenLabs) và âm thanh ổn định.
- **Tự động hóa hoàn toàn** từ blog → podcast → phân phối, **không cần can thiệp thủ công**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS ổn định. Dưới đây là 2 lựa chọn tối ưu:
👉 **[VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Chuyển đổi **tự động** từ bài blog sang podcast trong **vài phút**, thay vì mất **1-2 giờ/episode** thủ công.
✅ **Chất lượng chuyên nghiệp**: Giọng nói AI **tự nhiên** (thông qua ElevenLabs) và âm thanh **được tối ưu** cho podcast.
✅ **Phân phối tự động**: Podcast được **tạo file MP3** và lưu trên **Google Drive**, sẵn sàng chia sẻ qua email, Slack hoặc RSS.
✅ **Hoạt động liên tục**: Workflow **bật tự động** hàng ngày, không cần can thiệp (dùng **Schedule Trigger**).
✅ **Mở rộng nội dung**: Khán giả mới **lắng nghe** thay vì đọc, tăng engagement và reach.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| **Dịch vụ**               | **Thông tin cần thiết**                                                                 | **Liên kết đăng ký**                                                                 |
|---------------------------|-------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| **Google Drive**          | - Tài khoản Google (để lưu file podcast).                                               | [Google Drive](https://drive.google.com/)                                             |
|                           | - **API Key** (nếu cần quyền truy cập API).                                            | [Google Cloud Console](https://console.cloud.google.com/)                            |
| **Azure OpenAI (GPT-4o)** | - **API Key** và **Endpoint** của Azure OpenAI.                                          | [Azure OpenAI](https://azure.microsoft.com/en-us/products/cognitive-services/openai/) |
| **ElevenLabs (Tạo giọng nói)** | - **API Key** (miễn phí hoặc trả phí).                                                   | [ElevenLabs](https://elevenlabs.io/)                                                 |
| **Slack**                 | - **Token OAuth** (để gửi thông báo khi podcast hoàn thành).                          | [Slack API](https://api.slack.com/apps)                                               |
| **Gmail**                 | - Tài khoản Gmail (để gửi email thông báo hoặc file podcast).                           | [Gmail](https://mail.google.com/)                                                    |
| **RSS Feed (Blog)**       | - **URL RSS** của blog (để workflow theo dõi bài mới).                                  | [Tìm RSS Feed](https://www.rss.com/)                                                |

### **2. Cài đặt bổ sung**
- **Node `@n8n/n8n-nodes-langchain`**: Các sếp cần **cài đặt thủ công** từ [n8n Community](https://community.n8n.io/) (do workflow sử dụng **AI Agent** và **LLM**).
- **Node `httpRequest`**: Để gọi API của ElevenLabs (nếu không dùng node chính thức của ElevenLabs).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/11897](https://n8n.io/workflows/11897) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n.cloud).
3. Nhấn **Import** → **Paste JSON** và chọn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/11897](https://n8n.io/workflows/11897) (chọn **Export as JSON**).
2. **Dán vào n8n Editor** và nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này **không hoạt động ngay** sau khi import. Các sếp cần **cấu hình cẩn thận** các node sau:

#### **🔹 Node "Trigger: New Blog Post" (RSS Feed Read)**
- **Cấu hình**:
  - **URL RSS**: Điền **URL RSS của blog** (ví dụ: `https://blog.example.com/feed.xml`).
  - **Query**: Chọn **title** và **content** (để workflow lấy tiêu đề và nội dung bài viết).
  - **Filter**: Bật **Only new items** để chỉ lấy bài mới.

#### **🔹 Node "Azure OpenAI Chat Model" (lmChatAzureOpenAi)**
- **Cấu hình**:
  - **API Key**: Điền **API Key Azure OpenAI** (từ [Azure Portal](https://portal.azure.com/)).
  - **Endpoint**: Điền **Endpoint** của mô hình GPT-4o (ví dụ: `https://your-resource.openai.azure.com/`).
  - **Model**: Chọn **gpt-4o** (hoặc mô hình tương thích).
  - **Prompt**: Workflow đã **sẵn sàng** với **prompt chuyển đổi blog → script podcast**. Các sếp **không cần chỉnh** (nếu muốn tối ưu, có thể thêm **các instruction cụ thể** như:
    ```json
    "Chuyển bài viết này thành script podcast với:
    - Cấu trúc: Mở đầu (giới thiệu), Nội dung chính (tóm tắt), Kết luận (call-to-action).
    - Thời lượng: ~15-20 phút.
    - Giọng điệu: Chuyên nghiệp nhưng thân thiện, phù hợp với podcast."
    ```

#### **🔹 Node "AI Agent Rewrite to Podcast Script" (Agent)**
- **Cấu hình**:
  - **Credentials**: Chọn **Azure OpenAI** (đã cấu hình ở node trước).
  - **Input**: Workflow tự động lấy **nội dung bài blog** từ node **RSS Feed Read**.
  - **Lưu ý**: Node này **sử dụng LangChain Agent** để tối ưu quá trình chuyển đổi. **Không cần chỉnh** nếu muốn sử dụng mặc định.

#### **🔹 Node "Generate Audio" (HTTP Request)**
- **Cấu hình**:
  - **URL**: Điền **API Endpoint của ElevenLabs** (ví dụ: `https://api.elevenlabs.io/v1/text-to-speech/`).
  - **Headers**:
    - `xi-api-key`: Điền **API Key ElevenLabs**.
    - `Content-Type`: `application/json`.
  - **Body**:
    ```json
    {
      "text": "{{$json.content}}",  // Nội dung script từ AI
      "voice": "your-voice-id",      // ID giọng nói (miễn phí: "Aaron", "Elijah", "Joanna")
      "model_id": "eleven_multilingual_v2"
    }
    ```
  - **Lưu ý**:
    - **Tải ID giọng nói miễn phí** từ [ElevenLabs Dashboard](https://elevenlabs.io/voices).
    - Nếu **không dùng node HTTP Request**, các sếp có thể **cài node ElevenLabs chính thức** từ [n8n Community](https://community.n8n.io/).

#### **🔹 Node "Podcast Feed Builder" (Code)**
- **Cấu hình**:
  - **Script**: Workflow đã **sẵn sàng** để tạo **file RSS podcast**. Các sếp **không cần chỉnh** (nếu muốn tùy biến, có thể sửa trong **Code Node** để thay đổi:
    - **Tiêu đề podcast**.
    - **Mô tả**.
    - **Link cover image**.
    - **Cấu trúc RSS** (ví dụ: thêm **chương trình chi tiết**).

#### **🔹 Node "Upload file" (Google Drive)**
- **Cấu hình**:
  - **Credentials**: Chọn **Google Drive** (đã cấu hình trước).
  - **Folder**: Chọn **thư mục** để lưu file podcast (ví dụ: `Podcasts/Audio Files`).
  - **File Name**: Đặt định dạng tự động như:
    `Podcast_Episode_{{$json.title}}_{{$json.date}}.mp3`
  - **Lưu ý**: Workflow sẽ **tạo file MP3** từ âm thanh ElevenLabs và **lưu trên Google Drive**.

#### **🔹 Node "Notify Team" (Slack/Gmail)**
- **Cấu hình**:
  - **Slack**:
    - **Token OAuth**: Điền từ [Slack API](https://api.slack.com/apps).
    - **Channel**: Chọn **#general** hoặc channel riêng.
    - **Message**: Workflow sẽ gửi **thông báo khi podcast hoàn thành** (ví dụ: `Podcast mới được tạo: [Tiêu đề]`).
  - **Gmail**:
    - **Credentials**: Chọn **Gmail**.
    - **Email To**: Điền email của mình hoặc team.
    - **Subject**: `Podcast mới: {{$json.title}}`.
    - **Body**: Gửi **link Google Drive** hoặc **file MP3**.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Nhấn **Run Workflow** và chọn **1 bài blog mẫu** từ RSS.
   - Kiểm tra:
     - Script podcast được tạo không?
     - Âm thanh được sinh ra không?
     - File được upload lên Google Drive không?
     - Thông báo Slack/Gmail được gửi không?
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** và **cấu hình Schedule Trigger** (nếu muốn chạy hàng ngày).

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu chất lượng âm thanh**
- **Chọn giọng nói phù hợp**: ElevenLabs có **nhiều giọng nói miễn phí** (ví dụ: `Aaron` cho giọng nam trung tính, `Joanna` cho giọng nữ).
- **Sử dụng mô hình âm thanh cao cấp**: Nếu có budget, dùng **mô hình ElevenLabs Pro** (chất lượng âm thanh tốt hơn).
- **Thêm hiệu ứng âm thanh**: Sử dụng **node `code`** để thêm **âm thanh mở đầu/ kết thúc** (ví dụ: jingle podcast).

### **2. Tự động chia sẻ podcast**
- **Gửi qua Email tự động**: Sử dụng **node Gmail** để gửi **file MP3** cho khách hàng/đối tác.
- **Upload lên Spotify/Apple Podcasts**: Sử dụng **API của các nền tảng podcast** (ví dụ: [Spotify API](https://developer.spotify.com/documentation/web-api/)) để tự động cập nhật.
- **Tạo QR Code**: Sử dụng **node `code`** để tạo **QR Code** dẫn đến file podcast và gửi qua Slack/Email.

### **3. Theo dõi và báo cáo**
- **Lưu log hoạt động**: Sử dụng **node `stickyNote`** để ghi lại **lịch sử podcast** (tiêu đề, ngày tạo, trạng thái).
- **Báo cáo định kỳ**: Sử dụng **node `scheduleTrigger`** để gửi **báo cáo tuần/month** qua Slack/Email (ví dụ: số lượng podcast tạo, thời lượng trung bình).

### **4. Tùy biến script podcast**
- **Thêm giới thiệu/quảng cáo**: Sử dụng **node `set`** để chèn **lời giới thiệu** hoặc **quảng cáo sản phẩm** vào script.
- **Chia nhỏ bài viết**: Nếu bài blog dài, sử dụng **node `splitInBatches`** để chia thành **nhiều tập podcast**.

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy content** thay vì **việc thủ công**. Với **AI + tự động hóa**, các sếp có thể:
✅ **Tạo podcast hàng ngày** mà không cần thu âm.
✅ **Mở rộng nội dung** sang định dạng âm thanh.
✅ **Tiết kiệm chi phí** so với thu âm chuyên nghiệp.

**Bắt đầu ngay!**
1. **Import workflow** và **cấu hình API keys**.
2. **Test với 1 bài blog mẫu**.
3. **Bật Active** và **để nó chạy tự động**.

**Nếu gặp vấn đề**, các sếp có thể:
- **Tra cứu trên [n8n Community](https://community.n8n.io/)**.
- **Đăng ký hỗ trợ** từ [n8n Support](https://n8n.io/support).

---
**🚀 Hãy tự động hóa podcast của mình ngay hôm nay!** 🎧💻