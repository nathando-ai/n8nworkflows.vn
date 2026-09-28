---
title: "🎧 **Tự Động Hóa Spotify với GPT-4: Tạo Playlist & Kiểm Soát Nghe Nhạc Mới Mắt - Không Cần Code!**"
description: "Workflow này giúp các sếp tự động tạo playlist Spotify cá nhân hóa từ yêu cầu bằng lời nói, thêm nhạc vào playlist, và kiểm soát player Spotify (bắt đầu, tạm dừng, chuyển bài) chỉ với một chatbot AI. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công!"
slug: "tieu-dong-hoa-spotify-voi-gpt-4"
tags: [n8n, automation, spotify, ai-chatbot, gpt-4, no-code, langchain]
keywords: [n8n workflow spotify, tự động hóa spotify, chatbot gpt-4 spotify, tạo playlist tự động, kiểm soát spotify bằng ai]
---

# 🎧 **Tự Động Hóa Spotify với GPT-4: Playlist & Kiểm Soát Nghe Nhạc Mới Mắt**

### **🚀 Giải pháp cho các sếp muốn nghe nhạc "thông minh" mà không cần tay nghề kỹ thuật**
Có bao giờ các sếp cảm thấy chán ngấy với việc tạo playlist thủ công trên Spotify? Hay muốn nghe nhạc theo cảm xúc nhưng lại phải mất thời gian tìm kiếm và thêm bài hát một cách mệt mỏi? **Workflow này sẽ thay thế toàn bộ quá trình đó bằng một chatbot AI thông minh**, chỉ cần nói yêu cầu là nó tự động:
- **Tạo playlist** với tên phù hợp và nội dung phù hợp với tâm trạng.
- **Tìm kiếm và thêm bài hát** từ Spotify vào playlist.
- **Kiểm soát player** (bắt đầu, tạm dừng, chuyển bài) chỉ bằng lời nói.

Không cần viết một dòng code nào cả!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Nhờ đó, chatbot sẽ luôn sẵn sàng phản hồi ngay khi các sếp gọi tên nó.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** so với cách tạo playlist thủ công.
✅ **Playlists cá nhân hóa** dựa trên cảm xúc, thời gian hoặc chủ đề yêu cầu.
✅ **Kiểm soát Spotify bằng giọng nói** (bắt đầu, tạm dừng, chuyển bài) như một DJ ảo.
✅ **Hoạt động liên tục** (24/7) khi self-host trên VPS.
✅ **Không cần kỹ thuật** – chỉ cần cài đặt và chạy.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (để sử dụng GPT-4.1-mini):
   - API Key từ [OpenAI](https://platform.openai.com/account/api-keys).
2. **Tài khoản Spotify Developer**:
   - Đăng ký tại [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/) và lấy **Client ID & Client Secret**.
   - Cấu hình OAuth 2.0 cho ứng dụng.
3. **Tài khoản Spotify cá nhân** (để kiểm soát playlist và player).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/5923](https://n8n.io/workflows/5923) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/5923) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **22 node** và **2 nhánh chính**:
- **Nhánh trên**: Xử lý yêu cầu từ chatbot (tạo playlist, thêm nhạc).
- **Nhánh dưới**: Kiểm soát player Spotify (bắt đầu, tạm dừng, chuyển bài).

##### **A. Cấu hình Credentials**
| **Node**               | **Credentials cần thiết**       | **Lưu ý** |
|------------------------|----------------------------------|------------|
| **OpenAI Chat Model**  | `openAiApi` (API Key OpenAI)     | Điền vào **AI** > **OpenAI** trong n8n. |
| **Spotify nodes**      | `spotifyOAuth2Api`               | Cấu hình OAuth 2.0 cho Spotify. |
| **Agent & Tools**      | Không cần thêm (sử dụng credentials đã có). | |

##### **B. Cấu hình cụ thể các node quan trọng**
1. **When chat message received** (`chatTrigger`):
   - Đặt **Trigger Type** là **"Chat Trigger"** để chatbot phản hồi khi được gọi.
   - **Prompt mẫu**:
     ```
     Tôi muốn nghe nhạc gì? (Ví dụ: "Tạo một playlist nhạc điện tử cho buổi workout", "Bắt đầu playlist 'Chill Vibes'")
     ```

2. **Ideate playlist** (`chainLlm`):
   - **Prompt** đã được cấu hình sẵn, nhưng các sếp có thể **tùy chỉnh** để phù hợp với phong cách của mình.
   - Ví dụ:
     ```
     Tạo một playlist tên "Tâm trạng [tâm trạng yêu cầu]" với [số bài hát] bài nhạc phù hợp với [mood].
     ```

3. **Create playlist** (`spotify`):
   - **Resource**: `playlist`
   - **Operation**: `create`
   - **Tham số cần điền**:
     - `name`: Tên playlist (do AI tự động tạo).
     - `description`: Mô tả (tùy chọn).

4. **Add track to playlist** (`spotify`):
   - **Resource**: `playlist`
   - **Operation**: `addTrack`
   - **Tham số cần điền**:
     - `playlistId`: ID của playlist vừa tạo.
     - `tracks`: Mảng ID bài hát (do AI tìm kiếm).

5. **Spotify Tools (Pause/Resume/Next Song)**:
   - **Operation**: `pause`, `resume`, `nextSong`.
   - **Không cần tham số thêm**, chỉ cần chọn **credentials** là `spotifyOAuth2Api`.

##### **C. Kích hoạt Workflow**
1. **Test Run**:
   - Gửi một yêu cầu mẫu như:
     ```
     "Tạo một playlist nhạc rock cho buổi tối, sau đó bắt đầu nghe."
     ```
   - Kiểm tra:
     - Playlist có được tạo không?
     - Bài hát có được thêm không?
     - Player có bắt đầu không?

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh AI Prompt**:
   - Mở node **Ideate playlist** (`chainLlm`) và chỉnh sửa **system prompt** để phù hợp với phong cách của các sếp.
   - Ví dụ:
     ```
     Bạn là một DJ AI thông minh. Khi được yêu cầu tạo playlist, hãy:
     1. Lựa chọn tên playlist phù hợp với tâm trạng.
     2. Chọn tối đa 10 bài nhạc mới nhất (trong 6 tháng gần đây).
     3. Tránh trùng lặp bài hát.
     ```

2. **Kết hợp với Slack/Telegram**:
   - Sử dụng **n8n-nodes-slack** hoặc **n8n-nodes-telegram** để chatbot phản hồi trên Slack/Telegram thay vì chỉ trong n8n.

3. **Lưu log hoạt động**:
   - Thêm node **n8n-nodes-base.googleSheets** để ghi lại lịch sử yêu cầu và kết quả.
   - Ví dụ:
     ```
     - Yêu cầu: "Tạo playlist nhạc pop".
     - Kết quả: Playlist "Pop Vibes 2024" với 8 bài hát.
     - Thời gian: 12:34 PM.
     ```

4. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n-nodes-base.email** để gửi email báo cáo hàng tuần về:
     - Số playlist được tạo.
     - Thời gian nghe trung bình.
     - Top 3 playlist được nghe nhiều nhất.

---

### 📌 **Kết luận**
Workflow này không chỉ **tự động hóa việc tạo playlist Spotify** mà còn **kiểm soát player như một DJ ảo**, giúp các sếp **nghe nhạc một cách thông minh và tiết kiệm thời gian**. **Không cần viết code**, chỉ cần import và chạy!

**Hành động ngay**:
1. **Self-host n8n** trên VPS để workflow hoạt động 24/7.
2. **Import workflow** và cấu hình credentials.
3. **Test với yêu cầu đầu tiên** và trải nghiệm sự "thông minh" của AI!

👉 [Tải workflow ngay](https://n8n.io/workflows/5923) và bắt đầu tự động hóa Spotify của mình!