---
title: "🚀 Tự Động Hoá Chuyển Đổi Bài Blog RSS Sang Nội Dung Mạng Xã Hội Với OpenAI, Google Sheets, Gmail & Slack"
description: "Workflow tự động hóa chuyển đổi bài viết blog từ RSS thành nội dung LinkedIn, Twitter, và blog SEO tối ưu bằng AI, đồng thời lưu lịch trình, gửi draft email và chia sẻ trên Slack. Giúp các sếp tiết kiệm thời gian viết nội dung và duy trì sự hiện diện 24/7 trên mạng xã hội."
slug: "tieu-dong-rss-sang-noi-dung-mang-xa-hoi-voi-openai"
tags: [n8n, automation, no-code, content-repurposing, ai-content-creation]
keywords: [n8n workflow tự động, chuyển đổi nội dung blog, AI viết nội dung mạng xã hội, tự động hóa marketing, RSS to social media]
---

# 🚀 **Tự Động Hoá Chuyển Đổi Bài Blog RSS Sang Nội Dung Mạng Xã Hội Với AI**

### **Giải Pháp Cho Những Người Đang Mất Thời Gian Viết Nội Dung Mạng Xã Hội**
Các sếp có blog, kênh YouTube, hoặc newsletter đang phải tốn thời gian viết lại nội dung cho LinkedIn, Twitter, và Facebook? Hay đang phải thuê người viết nội dung cho từng kênh? **Workflow này sẽ tự động hóa toàn bộ quá trình** bằng AI, giúp bạn tiết kiệm **tối thiểu 10 giờ/tuần** và duy trì sự hiện diện 24/7 trên mạng xã hội **không cần viết một dòng nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI tự động viết lại bài blog thành nội dung LinkedIn, Twitter, và blog SEO trong **vài giây**.
- **Nội dung cá nhân hóa**: Dùng giọng điệu và phong cách riêng của brand (cấu hình trong node **Set Brand & Source**).
- **Lưu lịch trình**: Tất cả nội dung được ghi vào **Google Sheets** để quản lý dễ dàng.
- **Review trước khi chia sẻ**: Nội dung được gửi dưới dạng **draft email** để các sếp kiểm tra trước khi đăng.
- **Chia sẻ trong Slack**: Nội dung được tự động gửi đến kênh Slack của team để đồng bộ.
- **Hoạt động liên tục**: Workflow chạy hàng ngày theo lịch trình, không cần can thiệp thủ công.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (API Key) để sử dụng AI viết nội dung.
2. **Google Sheets** để lưu lịch trình nội dung (cần chia sẻ quyền chỉnh sửa cho n8n).
3. **Tài khoản Gmail** (để tạo draft email cho review).
4. **Tài khoản Slack** (để chia sẻ nội dung trong kênh team).
5. **RSS Feed** của blog hoặc kênh nội dung bạn muốn chuyển đổi (ví dụ: RSS từ WordPress, Medium, hoặc Substack).
6. **Thời gian cấu hình**: ~5 phút để thiết lập các credential và node **Set Brand & Source**.

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/16158](https://n8n.io/workflows/16158) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/16158) và paste vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** để import:
  ```bash
  n8n import workflow.json --name "Repurpose RSS to Social Content"
  ```

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
#### **A. Cấu Hình Credentials**
Các sếp cần thiết lập **credentials** cho các node sau:
| **Node**               | **Tham Số Cần Điền**                          | **Lưu Ý**                                                                 |
|------------------------|-----------------------------------------------|---------------------------------------------------------------------------|
| **OpenAI (lmChatOpenAi)** | API Key OpenAI                              | Sử dụng mô hình `gpt-4o-mini` để tiết kiệm chi phí.                      |
| **Google Sheets**      | Sheet ID và tên Sheet                         | Chọn sheet có cấu trúc cột phù hợp (ví dụ: `Date`, `Title`, `Content`). |
| **Gmail**              | Email và Password (hoặc OAuth 2.0)           | Chọn **Draft** để nội dung được gửi dưới dạng draft chờ review.          |
| **Slack**              | Token Slack và kênh chia sẻ                  | Chọn kênh team để nội dung được share tự động.                          |

#### **B. Cấu Hình Node "Set Brand & Source"**
- Mở node này và điền:
  - **Feed URL**: Link RSS của blog (ví dụ: `https://tinhn.vn/feed/`).
  - **Audience**: Đối tượng mục tiêu (ví dụ: "Marketers Việt Nam").
  - **Brand Voice**: Giọng điệu của brand (ví dụ: "Chuyên nghiệp, thân thiện, ngắn gọn").
  - **Output Format**: Chọn các loại nội dung cần tạo (SEO title, LinkedIn post, Twitter thread).

#### **C. Cấu Hình Node "Repurpose into Content"**
- Node này sử dụng **LangChain + OpenAI** để chuyển đổi bài blog thành:
  ```json
  {
    "seo_title": "Tiêu đề SEO tối ưu",
    "meta_description": "Mô tả meta SEO",
    "blog_post": "Bài blog viết lại",
    "linkedin_post": "Bài viết LinkedIn",
    "twitter_thread": "Thread Twitter",
    "hashtags": ["#Marketing", "#AI", "#Automation"]
  }
  ```
- **Lưu ý**: Nếu muốn thay đổi mô hình AI, chỉnh node **OpenAI Chat Model** (đã mặc định là `gpt-4o-mini`).

#### **D. Cấu Hình Node "Take Newest Only"**
- Node này **lọc bài mới nhất** từ RSS để tránh reprocessing.
- Nếu muốn lấy nhiều bài, tăng giá trị **Limit** (mặc định là 1).

#### **E. Cấu Hình Node "Save to Content Calendar"**
- Chọn **Operation = Append** để thêm nội dung mới vào sheet.
- Đảm bảo sheet có **cột phù hợp** (ví dụ: `Date`, `Title`, `LinkedIn Post`).

#### **F. Cấu Hình Node "Draft for Review"**
- Node này tạo **draft email** với nội dung AI viết.
- Các sếp có thể chỉnh **tiêu đề email** và **người nhận** trong node này.

#### **G. Cấu Hình Node "Share in Slack"**
- Chọn **Channel** và **format** (Markdown hoặc Plain Text) để chia sẻ.
- Ví dụ:
  ```markdown
  📢 **Bài mới từ Blog**:
  *Tiêu đề*: [SEO Title]
  *Nội dung*: [LinkedIn Post]
  *Link*: [RSS Link]
  ```

### **3. Kích Hoạt ⚡️**
1. **Test Run**: Chạy workflow với **1 bài mẫu** để kiểm tra kết quả.
   - Mở node **Every Day** và chọn **Run Once**.
   - Kiểm tra:
     - Nội dung có được viết lại không?
     - Draft email có được tạo không?
     - Slack có nhận được thông báo không?
2. **Bật Active**: Sau khi test thành công, bật **Active** cho workflow.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tăng Tính Cá Nhân Hóa**
- **Thêm Prompt Tùy Chỉnh**: Trong node **Repurpose into Content**, chỉnh sửa **prompt** để AI viết theo phong cách riêng:
  ```json
  "prompt": "Viết một bài LinkedIn post ngắn gọn (dưới 1000 ký tự), chuyên nghiệp và hấp dẫn, với giọng điệu {brand_voice}. Đảm bảo bao gồm {hashtags} và link đến bài blog: {rss_link}."
  ```
- **Dùng Templates**: Lưu các template khác nhau cho từng kênh (LinkedIn, Twitter) trong **Sticky Note** và gọi trong node **Set**.

### **2. Tích Hợp Auto-Publish**
- **LinkedIn**: Sử dụng node **LinkedIn API** để tự động đăng bài sau khi review.
- **Twitter/X**: Kết nối với **Buffer** hoặc **Hootsuite** để lịch trình tweet.
- **Facebook**: Sử dụng **Facebook Graph API** để đăng bài tự động.

### **3. Lưu Log & Báo Cáo**
- **Node StickyNote**: Lưu log của mỗi run để theo dõi lỗi hoặc cải tiến.
- **Google Sheets Dashboard**: Tạo một sheet tổng hợp để theo dõi:
  - Số lượng bài viết được tự động hóa.
  - Thời gian chạy.
  - Tỷ lệ thành công/thất bại.

### **4. Backfill Lịch Sử**
- Giảm giá trị **Limit** trong node **Take Newest Only** xuống 0 để lấy tất cả bài từ RSS.
- Sau khi backfill xong, đặt lại **Limit = 1** để chỉ lấy bài mới.

### **5. Tối Ưu Chi Phí OpenAI**
- **Sử dụng mô hình rẻ**: `gpt-4o-mini` (mặc định) hoặc `gpt-3.5-turbo` để giảm chi phí.
- **Cache kết quả**: Nếu nội dung giống nhau, AI sẽ trả kết quả cũ (tiết kiệm token).

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc viết nội dung mạng xã hội từ blog RSS, **không cần viết một dòng nào**. Bằng cách kết hợp **AI, Google Sheets, Gmail, và Slack**, bạn sẽ:
✅ **Tiết kiệm thời gian** viết nội dung.
✅ **Duy trì sự hiện diện 24/7** trên mạng xã hội.
✅ **Cải thiện SEO** với bài blog viết lại.
✅ **Đồng bộ team** thông qua Slack.

**Hành động ngay**: Import workflow này và bắt đầu tự động hóa nội dung của mình! Nếu có vấn đề, hãy liên hệ với [n8n Community](https://community.n8n.io/) hoặc comment bên dưới.

---
**🚀 Cài đặt n8n trên VPS để workflow chạy 24/7!**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)