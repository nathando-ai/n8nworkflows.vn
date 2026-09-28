---
title: "🚀 Chuyển Tin Nhắn Telegram Sang Bài Đăng LinkedIn Chuyên Nghiệp Với Gemini AI & Hệ Thống Phê Duyệt Tự Động"
description: "Workflow tự động hóa 100% không code giúp các sếp chuyển đổi tin nhắn Telegram thành bài đăng LinkedIn chuyên nghiệp, tối ưu SEO và phù hợp với định dạng bài viết dài (2800 ký tự), với sự hỗ trợ của AI Gemini và hệ thống phê duyệt 2 bước. Giảm thời gian tạo nội dung từ 2 giờ xuống chỉ 5 phút, đồng thời đảm bảo chất lượng cao và tính cá nhân hóa."
slug: "chuyen-doi-tin-nhan-telegram-sang-bai-dang-linkedin-chuyen-nghiep"
tags: [n8n, automation, content-creation, ai-gemini, linkedin-automation, telegram-bot, no-code]
keywords: [tự động hóa bài đăng linkedin, chuyển đổi tin nhắn telegram thành bài viết, ai gemini tạo nội dung, workflow n8n linkedin, tự động hóa nội dung marketing, tự động hóa content creation]
---

# 🚀 **Tự Động Hóa Chuyển Tin Nhắn Telegram Thành Bài Đăng LinkedIn Chuyên Nghiệp Với Gemini AI**

## **Nỗi Đau Của Các Sếp Trong Tạo Nội Dung LinkedIn**
Các sếp và chuyên gia marketing thường phải đối mặt với những thách thức sau khi tạo nội dung cho LinkedIn:
- **Tốn thời gian quá lâu**: Viết một bài đăng chất lượng từ đầu đến cuối có thể mất từ 1-2 giờ, trong khi đó thời gian thực hiện các nhiệm vụ khác bị trì hoãn.
- **Không đảm bảo chất lượng**: Nội dung viết tay dễ bị thiếu logic, thiếu SEO, hoặc không phù hợp với định dạng bài viết dài (2800 ký tự) của LinkedIn.
- **Không cá nhân hóa**: Các bài đăng thường thiếu tính độc đáo và liên kết với xu hướng thị trường hiện tại.
- **Không kiểm soát được quá trình phê duyệt**: Sau khi viết xong, phải gửi qua nhiều vòng phê duyệt, gây chậm trễ và mất hiệu quả.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa toàn bộ quy trình** từ nhận tin nhắn Telegram đến đăng bài trên LinkedIn.
✅ **Sử dụng AI Gemini** để tạo nội dung chuyên nghiệp, phù hợp với định dạng LinkedIn, với tone voice chuyên nghiệp và tối ưu SEO.
✅ **Hệ thống phê duyệt 2 bước** qua Telegram, cho phép các sếp kiểm soát và chỉnh sửa trước khi đăng bài.
✅ **Tích hợp web scraping và tìm kiếm thông tin thời sự** để nội dung luôn cập nhật và liên quan đến xu hướng thị trường.
✅ **Lưu trữ và theo dõi tất cả quá trình** trên Google Sheets, giúp quản lý và phân tích hiệu quả.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 2 giờ viết bài xuống chỉ **5 phút** để gửi yêu cầu và phê duyệt.
- **Nội dung chuyên nghiệp**: AI Gemini đảm bảo bài viết có **tone voice chuyên nghiệp**, **cấu trúc logic**, và **tối ưu SEO**.
- **Cá nhân hóa cao**: Nội dung được tạo dựa trên **tin nhắn Telegram** của các sếp, đồng thời tích hợp **thông tin thời sự** từ Brave Search và Firecrawl.
- **Hệ thống phê duyệt minh bạch**: Các sếp có thể **xem trước bài viết**, **chỉnh sửa**, hoặc **từ chối** trước khi đăng.
- **Tự động đăng bài**: Sau khi phê duyệt, bài viết sẽ được đăng trực tiếp lên LinkedIn **không cần can thiệp thủ công**.
- **Lưu trữ và theo dõi**: Tất cả quá trình được ghi lại trên **Google Sheets**, giúp quản lý và phân tích hiệu quả.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và API keys sau:
1. **Telegram Bot**:
   - Tạo một bot Telegram và lấy **API Token** từ [@BotFather](https://t.me/BotFather).
   - Cấu hình bot trong **Telegram Trigger** và **Telegram** nodes.
   - **Lưu ý**: Chỉ cho phép **người dùng đã được whitelist** (danh sách trong node `Authorized Telegram Users`) gửi tin nhắn.

2. **LinkedIn API**:
   - Tạo một ứng dụng LinkedIn Developer và lấy **OAuth 2.0 API Key**.
   - Cấu hình trong node `Create a post` để đăng bài tự động.

3. **Google Sheets**:
   - Tạo một bảng Google Sheets để **lưu trữ lịch sử yêu cầu**, **bài viết đã tạo**, và **trạng thái phê duyệt**.
   - Cấu hình **Google OAuth 2.0 API** trong node `Log Initial Request` và các node liên quan.

4. **Google Gemini API**:
   - Đăng ký API Key từ [Google AI Studio](https://makersuite.google.com/) và cấu hình trong node `lmChatGoogleGemini`.

5. **Firecrawl API** (để web scraping):
   - Đăng ký API Key từ [Firecrawl](https://firecrawl.io/) và cấu hình trong node `Scrape a url and get its content`.

6. **Brave Search API** (để tìm kiếm thông tin thời sự):
   - Đăng ký API Key từ [Brave Search](https://search.brave.com/) và cấu hình trong node `Web Search for the related content`.

7. **LangChain & Output Parser** (để xử lý đầu ra AI):
   - Các node này đã được tích hợp sẵn trong workflow, không cần cấu hình thêm.

---
:::warning[LƯU Ý QUAN TRỌNG]
- **Self-hosted n8n** là lựa chọn tối ưu để workflow chạy 24/7 mà không bị giới hạn bởi phiên bản miễn phí.
- **Không sử dụng phiên bản n8n miễn phí** vì nó có giới hạn về số lượng workflow và thời gian chạy.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7466](https://n8n.io/workflows/7466) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file JSON.
- **Không chỉnh sửa trực tiếp trên canvas** nếu chưa hiểu rõ logic, để tránh lỗi.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này phức tạp với **43 nodes**, nhưng có một số node **quan trọng nhất** cần cấu hình cẩn thận:

##### **A. Cấu Hình Credentials (Tài Khoản API)**
| **Node**                     | **Credentials Cần Cấu Hình**          | **Lưu Ý**                                                                 |
|------------------------------|----------------------------------------|----------------------------------------------------------------------------|
| Telegram Trigger             | `telegramApi`                          | Điền **API Token** của bot Telegram.                                      |
| Telegram (gửi tin nhắn)      | `telegramApi`                          | Sử dụng cùng API Token như trên.                                         |
| LinkedIn                     | `linkedInOAuth2Api`                    | Điền **Client ID** và **Client Secret** từ LinkedIn Developer.           |
| Google Sheets                | `googleSheetsOAuth2Api`                | Cấu hình OAuth 2.0 từ Google Cloud Console.                                |
| Firecrawl                    | `firecrawlApi`                         | Điền **API Key** từ Firecrawl.                                            |
| Brave Search                 | `braveSearchApi`                       | Điền **API Key** từ Brave Search.                                          |
| Google Gemini (AI)           | `googlePalmApi`                        | Điền **API Key** từ Google AI Studio.                                     |

##### **B. Cấu Hình Node Quan Trọng**
1. **`Telegram Trigger`**:
   - Chọn **Webhook URL** từ n8n và gửi cho **bot Telegram** để nhận tin nhắn.
   - Cấu hình **filter** để chỉ chấp nhận tin nhắn từ **người dùng đã whitelist** (node `Authorized Telegram Users`).

2. **`Authorized Telegram Users`**:
   - Danh sách **chat ID** của các sếp được phép sử dụng workflow.
   - **Cách lấy chat ID**: Gửi tin nhắn cho bot Telegram và kiểm tra URL trong phản hồi (ví dụ: `https://api.telegram.org/bot<TOKEN>/getUpdates`).

3. **`Intent Categorization` (AI phân loại nội dung)**:
   - Node này sử dụng **Gemini AI** để phân loại tin nhắn Telegram thành:
     - **URL** (để web scraping).
     - **Topic** (để tìm kiếm thông tin thời sự).
     - **Content** (đã sẵn sàng viết bài).
     - **Mixed** (kombine cả URL và Topic).
   - **Lưu ý**: Cấu hình **Prompt** trong node `lmChatGoogleGemini` để AI hiểu rõ yêu cầu.

4. **`Content Router` (If node)**:
   - Xác định **con đường xử lý** dựa trên phân loại:
     - **URL Path** → Web scraping (Firecrawl).
     - **Topic Path** → Tìm kiếm Brave Search.
     - **Direct Path** → Viết bài ngay.
     - **Mixed** → Gộp cả hai.

5. **`Loop Over URLs` (Split in Batches)**:
   - Nếu tin nhắn chứa **nhiều URL**, node này sẽ **chia thành batch** để web scraping hiệu quả.

6. **`Google Gemini Model With Parser`**:
   - Node này **tạo bài viết LinkedIn** dựa trên:
     - Nội dung gốc từ Telegram.
     - Thông tin scraped từ Firecrawl.
     - Kết quả tìm kiếm từ Brave Search.
   - **Lưu ý**: Cấu hình **Prompt** để AI tạo bài viết **chuyên nghiệp**, **có tone voice phù hợp**, và **tối ưu SEO**.

7. **`Interactive Preview & Approval`**:
   - Sau khi AI tạo bài viết, nó sẽ được **gửi preview** qua Telegram với:
     - **Nội dung bài viết**.
     - **Số ký tự** (đảm bảo dưới 2800).
     - **Hashtag phân tích**.
     - **Nút phê duyệt/ chỉnh sửa/ từ chối**.
   - **Cách cấu hình**:
     - Node `Send Preview to Telegram` → Chọn **template tin nhắn** với các nút tương tác.
     - Node `Route Actions` → Xác định hành động khi người dùng chọn **Approve/Edit/Reject**.

8. **`Create a post` (LinkedIn)**:
   - Chỉ hoạt động khi **Approve** được chọn.
   - **Lưu ý**: Kiểm tra **permissions** của LinkedIn API để đảm bảo đăng bài thành công.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run với Dữ Liệu Mẫu**:
   - Gửi một tin nhắn mẫu qua Telegram (ví dụ: *"Tôi muốn viết bài về AI và tự động hóa"*).
   - Theo dõi quá trình trong **n8n Editor** để kiểm tra các node hoạt động như thế nào.

2. **Bật Active Workflow**:
   - Sau khi kiểm tra xong, **bật workflow** và **đăng ký Webhook URL** trong Telegram bot.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram Cho Nhóm Phê Duyệt**:
   - Thay vì chỉ sử dụng Telegram, các sếp có thể **tích hợp Slack** để phê duyệt bài viết qua kênh nhóm.
   - **Cách làm**: Sử dụng node `slack` (nếu có) hoặc chuyển đổi tin nhắn Telegram sang Slack bằng một workflow nhỏ.

2. **Lưu Log & Báo Cáo Hàng Tuần**:
   - Sử dụng **Google Sheets** để **tạo báo cáo tự động** về:
     - Số bài viết đã tạo.
     - Trạng thái phê duyệt.
     - Thời gian xử lý trung bình.
   - **Cách làm**: Tạo một workflow nhỏ sử dụng node `googleSheets` để **tổng hợp dữ liệu** và gửi báo cáo qua Email/Telegram.

3. **Tối Ưu AI với Prompt Tùy Chỉnh**:
   - Nếu các sếp muốn **tone voice** khác nhau (ví dụ: **chuyên nghiệp hơn** hoặc **thân thiện hơn**), hãy **cập nhật Prompt** trong node `lmChatGoogleGemini`.
   - **Ví dụ Prompt**:
     ```
     Tôi là một chuyên gia marketing. Viết một bài đăng LinkedIn chuyên nghiệp (2000-2800 ký tự) về chủ đề [TOPIC]. Bài viết phải:
     1. Có tiêu đề hấp dẫn.
     2. Cấu trúc rõ ràng: Giới thiệu -> Thông tin chi tiết -> Kết luận.
     3. Sử dụng từ khóa SEO: [KEYWORDS].
     4. Có ít nhất 3 hashtag liên quan.
     5. Tone voice chuyên nghiệp, không quá dài dòng.
     ```

4. **Tự Động Xóa Bài Viết Sau Thời Gian**:
   - Nếu không muốn bài viết cũ vẫn hiện trên LinkedIn, các sếp có thể **tích hợp node `linkedIn` để xóa bài viết** sau một thời gian (ví dụ: 6 tháng).
   - **Cách làm**: Sử dụng node `googleSheets` để **lưu thời gian đăng bài** và sau đó chạy một workflow nhỏ để xóa.

5. **Tích Hợp Google Drive Cho Ảnh & File Đính Kèm**:
   - Nếu các sếp muốn **đính kèm ảnh** vào bài viết, hãy cấu hình node `googleDrive` để tải ảnh từ Google Drive và gắn vào bài viết LinkedIn.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa toàn bộ quy trình tạo và đăng bài LinkedIn** mà không cần viết code. Với sự hỗ trợ của **Gemini AI**, **web scraping**, và **hệ thống phê duyệt 2 bước**, các sếp có thể:
✔ **Tiết kiệm thời gian** lên đến **90%** trong việc tạo nội dung.
✔ **Đảm bảo chất lượng** với bài viết chuyên nghiệp, tối ưu SEO.
✔ **Cá nhân hóa nội dung** dựa trên tin nhắn Telegram và xu hướng thị trường.
✔ **Quản lý dễ dàng** với hệ thống log và báo cáo tự động.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7.
2. **Cấu hình tất cả credentials** như hướng dẫn trên.
3. **Test với tin