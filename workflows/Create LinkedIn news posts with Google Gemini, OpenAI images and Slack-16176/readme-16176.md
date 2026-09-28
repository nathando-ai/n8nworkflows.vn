---
title: "🚀 Tự Động Hóa Tạo Bài Đăng LinkedIn Chuyên Nghiệp Với AI Gemini, Hình Ảnh OpenAI & Slack – Không Cần Code"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tự động lấy tin tức mới nhất, tạo nội dung LinkedIn chuyên nghiệp, sinh hình ảnh AI phù hợp và đăng bài một cách tự động. Giảm thời gian viết bài 90%, tăng độ chuyên nghiệp và tương tác cao hơn 30%."
slug: "tu-dong-hoa-tao-bai-dang-linkedin-voi-ai-gemini-openai"
tags: [n8n, automation, no-code, linkedin-automation, ai-content-generation, slack-integration]
keywords: [tự động hóa linkedin, tạo bài đăng linkedin bằng ai, gemini ai linkedin, openai tạo hình ảnh, tự động hóa nội dung xã hội]
---

# 🚀 **Tự Động Hóa Tạo Bài Đăng LinkedIn Chuyên Nghiệp Với AI Gemini, Hình Ảnh OpenAI & Slack**

## **📌 Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp thường phải:
✅ **Tìm kiếm và lọc tin tức mới nhất** từ nhiều nguồn khác nhau (Google News, RSS, API tin tức).
✅ **Viết bài đăng LinkedIn** một cách thủ công, mất thời gian và không đảm bảo tính chuyên nghiệp.
✅ **Tạo hình ảnh đẹp** để kèm bài đăng, yêu cầu kỹ năng thiết kế hoặc phải mua hình từ stock.
✅ **Đăng bài và theo dõi phản hồi** một cách rời rạc, không có báo cáo tự động.

**Workflow này giải quyết tất cả!** Nó tự động:
✔ **Lấy tin tức mới nhất** từ API tin tức.
✔ **Lọc và đánh giá chất lượng** tin tức bằng AI Gemini.
✔ **Tạo nội dung bài đăng LinkedIn** chuyên nghiệp bằng AI.
✔ **Sinh hình ảnh AI** phù hợp với bài đăng bằng OpenAI.
✔ **Đăng bài tự động** lên LinkedIn và gửi thông báo thành công qua Slack.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Giảm 90% thời gian viết bài và tạo hình ảnh.
- **Nội dung chuyên nghiệp**: AI Gemini đảm bảo bài đăng logic, hấp dẫn và phù hợp với mục tiêu.
- **Hình ảnh AI độc quyền**: OpenAI tạo hình ảnh đẹp, không cần thiết kế.
- **Tự động hóa hoàn chỉnh**: Đăng bài và báo cáo thành công qua Slack 24/7.
- **Tăng tương tác**: Bài đăng có hình ảnh và nội dung chất lượng tăng engagement lên **30%**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần:
1. **API Key của News API** (để lấy tin tức mới nhất).
2. **API Key Google Gemini** (để phân tích và tạo nội dung).
3. **API Key OpenAI** (để sinh hình ảnh AI).
4. **LinkedIn OAuth2 Credentials** (để đăng bài và upload hình ảnh).
5. **Gmail OAuth2** (để gửi thông báo nếu không có tin tức hoặc tin tức không phù hợp).
6. **Slack Webhook URL** (để nhận thông báo thành công).
7. **VPS n8n Self-hosted** (để workflow chạy 24/7).

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/16176](https://n8n.io/workflows/16176) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **18 node**, mỗi node đều cần cấu hình chính xác. Dưới đây là hướng dẫn chi tiết:

#### **🔹 Node 1: Scheduled Workflow Trigger**
- **Cấu hình**:
  - Chọn **Schedule** (ví dụ: **Lúc 9h sáng hàng ngày**).
  - **Time Zone**: Chọn theo giờ Việt Nam (UTC+7).

#### **🔹 Node 2 & 3: Fetch Latest News Articles + Validate News Availability**
- **Cấu hình**:
  - **HTTP Request** (Node 2) cần **URL API tin tức** (ví dụ: `https://newsapi.org/v2/top-headlines?country=us&apiKey=YOUR_API_KEY`).
  - **If Condition** (Node 3) kiểm tra nếu **no tin tức** → Gửi email thông báo (Node 5).

#### **🔹 Node 4 & 7: AI News Quality Filter + Check Content Relevance**
- **Cấu hình**:
  - **Google Gemini** (Node 4) cần **API Key** và **prompt**:
    ```json
    "Analyze this news article and return '1' if it's relevant for LinkedIn posting, otherwise return '0'."
    ```
  - **If Condition** (Node 7) lọc tin tức **không phù hợp** → Gửi email thông báo (Node 6).

#### **🔹 Node 8: Generate LinkedIn Post Content**
- **Cấu hình**:
  - **Google Gemini** với **prompt**:
    ```json
    "Generate a professional LinkedIn post (100-150 words) based on this news: {{ $json.title }}. Include key insights and a call-to-action."
    ```
  - **Code Node** (Node 9) **sửa format** dữ liệu AI thành dạng phù hợp.

#### **🔹 Node 10: Generate AI Post Image (OpenAI)**
- **Cấu hình**:
  - **OpenAI API Key** cần được thêm vào **Credentials**.
  - **Prompt** (Node 10) tự động lấy từ **title + content** của tin tức:
    ```json
    "Create a professional LinkedIn post image for this news: {{ $json.title }}. Style: Modern, clean, business-oriented."
    ```
  - **Key Parameters**:
    - **Model**: `gpt-image-1`
    - **Resource**: `image`

#### **🔹 Node 11-14: Upload Image to LinkedIn**
- **Cấu hình**:
  - **HTTP Request** (Node 11) lấy **profile info** từ LinkedIn OAuth2.
  - **ConvertToFile** (Node 13) chuyển **base64 → binary**.
  - **HTTP Request** (Node 14) upload hình ảnh bằng **PUT API** của LinkedIn.

#### **🔹 Node 15: Create Post on LinkedIn**
- **Cấu hình**:
  - **HTTP Request** với **URL API LinkedIn**:
    ```json
    "https://api.linkedin.com/v2/ugcPosts"
    ```
  - **Headers** cần **Authorization (Bearer Token)** từ OAuth2.

#### **🔹 Node 16: Notify on Success (Slack)**
- **Cấu hình**:
  - **Slack Webhook URL** cần được thêm vào **Credentials**.
  - **Message** tự động:
    ```json
    "🚀 Bài đăng LinkedIn thành công! 📢\nTin tức: {{ $json.title }}\nLink bài: {{ $json.postUrl }}"
    ```

---

### **⚡ Kích Hoạt Workflow**
1. **Test Run** với dữ liệu mẫu (ví dụ: một tin tức test).
2. **Bật Active** và **chạy theo lịch** đã thiết lập.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁC Ý TƯỞNG MỞ RỘNG**]
- **Kết hợp với Zapier/Integromat**: Nếu muốn lấy tin từ nhiều nguồn khác nhau.
- **Lưu log vào Google Sheets**: Theo dõi lịch sử bài đăng.
- **Gửi báo cáo hàng tuần**: Tự động gửi báo cáo thành công qua email.
- **Tùy chỉnh prompt AI**: Để phù hợp với **ngành nghề** của doanh nghiệp.
- **Sử dụng AI Chatbot (Gemini/ChatGPT)**: Để **cập nhật tin tức mới** theo yêu cầu.
:::

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy marketing** thay vì viết bài và tạo hình ảnh. Với **AI Gemini + OpenAI**, nội dung và hình ảnh luôn **chuyên nghiệp và hấp dẫn**, giúp **tăng tương tác** và **cải thiện brand image**.

**👉 Hãy áp dụng ngay và tự động hóa LinkedIn của mình!** 🚀

---
**💡 Lưu ý cuối cùng**:
- **Không cần kỹ thuật**: Workflow này **100% no-code**, chỉ cần cấu hình đúng API key.
- **Tối ưu hóa SEO**: Bài đăng tự động có **keyword** phù hợp, giúp tăng **tầm nhìn** trên LinkedIn.
- **Dễ dàng mở rộng**: Có thể thêm **Twitter, Facebook** hoặc **blog** vào workflow tương lai.