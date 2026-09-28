---
title: "🚀 Tự Động Hóa Sơ Yêu Lập Trình Viên Theo Mô Tả Vị Trí - Telegram + AI + LinkedIn"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp tạo CV cá nhân hóa phù hợp với từng vị trí việc làm chỉ bằng cách gửi mô tả công việc hoặc liên kết LinkedIn qua Telegram. Kết quả là PDF CV chuyên nghiệp, tối ưu hóa từ AI, với chi phí thời gian gần như bằng 0."
slug: "tieu-dong-hoa-so-yeu-lap-trinh-vien-theo-mo-ta-vi-tri"
tags: [n8n, automation, hr, ai, telegram, linkedin, openrouter, json-resume, no-code]
keywords: [tự động hóa cv, cv cá nhân hóa, ai tạo cv, linkedin automation, n8n workflow, resume tailoring, openrouter api]
---

# 🚀 **Tự Động Hóa Sơ Yêu Lập Trình Viên Theo Mô Tả Vị Trí - Telegram + AI + LinkedIn**

### **Giải pháp cho các sếp muốn ấn tượng ngay lần đầu tiên**
Hiện nay, việc ứng tuyển vị trí lập trình viên tại các công ty tech lớn như **FAANG, Unicorns Việt Nam** hay các startup quốc tế đòi hỏi CV phải **cá nhân hóa, tối ưu hóa từ khóa** và phù hợp với từng mô tả công việc cụ thể. Thay vì mất **giờ đồng hồ** để chỉnh sửa CV thủ công cho từng ứng tuyển, các sếp có thể **tự động hóa toàn bộ quy trình** chỉ bằng một workflow n8n kết hợp **Telegram Bot, AI OpenRouter và LinkedIn Scraping**.

Workflow này **xử lý tự động** từ việc nhận mô tả công việc (hoặc liên kết LinkedIn) đến việc **tạo CV PDF cá nhân hóa**, với **chi phí thời gian gần như bằng 0** và **tỷ lệ thành công cao hơn** so với CV thông thường.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Chỉ cần **gửi tin nhắn Telegram** hoặc **paste mô tả công việc**, workflow sẽ tự động tạo CV phù hợp.
- **CV cá nhân hóa 100%**: AI phân tích mô tả công việc và **tối ưu hóa từ khóa**, kỹ năng, kinh nghiệm phù hợp với từng vị trí.
- **Chất lượng chuyên nghiệp**: Kết quả là **PDF CV** với **mẫu thiết kế hiện đại**, có thể chia sẻ trực tiếp qua Telegram hoặc email.
- **Hoạt động 24/7**: Không cần can thiệp thủ công, workflow chạy tự động khi nhận được yêu cầu.
- **Dữ liệu an toàn**: Các sếp **chủ quyền dữ liệu**, không phụ thuộc vào bất kỳ nền tảng nào (nếu tự host backend).
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Telegram Bot**:
   - Tạo bot qua [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Cấu hình **credentials** trong n8n với tên `telegramApi`.
2. **JSON Resume**:
   - Chuẩn bị **CV theo định dạng JSON Resume** (mô tả tại [jsonresume.org](https://jsonresume.org/)).
   - **Host công khai** (ví dụ: GitHub Gist, Vercel, Netlify) để workflow có thể truy cập.
   - **URL của JSON Resume** sẽ được điền vào node `GetResumePdf`.
3. **OpenRouter API Key**:
   - Đăng ký tài khoản tại [OpenRouter](https://openrouter.ai/) và lấy **API Token**.
   - Tạo **credentials** trong n8n với tên `openRouterApi`.
4. **(Khuyến nghị)** **Proxy**:
   - Nếu muốn **scrap LinkedIn**, các sếp cần **proxy** (ví dụ: OxyLabs) để tránh bị chặn IP.
   - Nếu không cần chức năng này, có thể bỏ qua.
5. **(Tùy chọn)** **Backend tự host**:
   - Workflow sử dụng backend của tác giả ([The Backend](https://github.com/daniel-iliesh/nest-thebackend)) để **tạo PDF từ HTML**.
   - Các sếp có thể **tự host** backend này để **chủ quyền dữ liệu** (không phụ thuộc vào server của tác giả).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/10635](https://n8n.io/workflows/10635) và **import** vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/10635) và **paste** vào n8n Editor.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **16 node** với các bước chính sau. Các sếp cần **cấu hình kỹ lưỡng** các node sau:

#### **A. Cấu hình Telegram Bot**
- Node: **`OnTelegramMessage`** (Telegram Trigger)
  - Điền **API Token** của bot vào `credentials` (tên: `telegramApi`).
  - **Không cần cấu hình thêm** (node này tự động nhận tin nhắn từ Telegram).

#### **B. Cấu hình OpenRouter AI**
- Node: **`OpenRouter Chat Model`** (lmChatOpenRouter)
  - Điền **API Token** vào `credentials` (tên: `openRouterApi`).
  - **Model mặc định**: `openai/gpt-4.1` (có thể thay đổi nếu muốn sử dụng model khác).

#### **C. Cấu hình JSON Resume**
- Node: **`GetResumePdf`** (httpRequest)
  - Điền **URL của JSON Resume** (host công khai) vào `url`.
  - Ví dụ: `https://gist.githubusercontent.com/username/raw/abc123/resume.json`.

#### **D. Cấu hình Backend (nếu tự host)**
- Node: **`GenerateResume`** (httpRequest)
  - Nếu **không tự host backend**, các sếp **không cần chỉnh** node này (sử dụng backend của tác giả).
  - Nếu tự host, điền **URL API** của backend vào `url` (ví dụ: `http://localhost:3000/generate`).

#### **E. Cấu hình Proxy (nếu scrap LinkedIn)**
- Node: **`GetJobHTML`** (httpRequest)
  - Nếu muốn **scrap mô tả công việc từ LinkedIn**, điền **URL proxy** vào `headers` (ví dụ:
    ```json
    {
      "Proxy-Authorization": "Basic base64_encoded_proxy_credentials"
    }
    ```
  - Nếu không cần, **bỏ qua** node này và sử dụng **mô tả công việc được paste trực tiếp**.

#### **F. Cấu hình AI Tailor CV**
- Node: **`GetTailoredJsonResume`** (chainLlm)
  - **Không cần cấu hình** (sử dụng **system prompt** đã định sẵn).
  - AI sẽ **tự động phân tích mô tả công việc** và **cập nhật JSON Resume** phù hợp.
- Node: **`EnsureJsonResumeSchema`** (outputParserStructured)
  - **Không cần cấu hình** (đảm bảo JSON Resume tuân theo **schema chuẩn**).

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn Telegram với **mô tả công việc** hoặc **liên kết LinkedIn** (ví dụ: `https://www.linkedin.com/jobs/view/123456789/`).
   - Kiểm tra **log** trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active**:
   - Chuyển **switch Active** sang **ON** để workflow hoạt động liên tục.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**CÁCH LÀM NGOÀI THƯỜNG**]
1. **Tích hợp với Slack/Email**:
   - Thay vì chỉ Telegram, các sếp có thể **tích hợp với Slack** (node `n8n-nodes-base.slack`) để nhận yêu cầu từ team.
   - Hoặc **gửi email tự động** (node `n8n-nodes-base.email`) khi CV sẵn sàng.

2. **Lưu log hoạt động**:
   - Sử dụng node **`stickyNote`** để ghi lại **lịch sử yêu cầu** và **kết quả**.
   - Có thể **export log** định kỳ để theo dõi hiệu suất.

3. **Tự động gửi CV cho ứng tuyển**:
   - Sau khi tạo PDF, workflow có thể **gửi tự động** qua **email** hoặc **Telegram** cho các sếp.
   - Hoặc **upload lên Google Drive/Dropbox** (node `n8n-nodes-base.googleDrive`).

4. **Cập nhật CV định kỳ**:
   - Sử dụng **n8n Scheduler** để **cập nhật CV** theo **mô tả công việc mới nhất** từ LinkedIn.
   - Ví dụ: **Mỗi tháng 1 lần**, workflow tự động **scrap LinkedIn** và **cập nhật CV**.

5. **Mở rộng cho nhiều vị trí**:
   - Các sếp có thể **tạo nhiều workflow riêng biệt** cho từng **nhóm công việc** (Backend, Frontend, DevOps...).
   - Sử dụng **node `set`** để **lưu trữ nhiều JSON Resume** và **chọn tự động** khi nhận yêu cầu.
:::

---
## 📌 **Kết luận**
Workflow **Automated Resume Tailoring** là **giải pháp hoàn hảo** cho các sếp lập trình viên muốn **tăng tỷ lệ thành công ứng tuyển** mà **không cần viết code**. Với **AI OpenRouter, Telegram Bot và LinkedIn Scraping**, workflow này **tự động hóa toàn bộ quy trình**, từ **nhận mô tả công việc** đến **tạo CV PDF cá nhân hóa**, **chỉ trong vài giây**.

👉 **Hãy thử ngay!**
- **Tải workflow** từ [n8n.io/workflows/10635](https://n8n.io/workflows/10635).
- **Cấu hình theo hướng dẫn** trên.
- **Gửi mô tả công việc qua Telegram** và **nhận CV chuyên nghiệp** ngay lập tức!

**Chúc các sếp thành công trong việc tìm kiếm công việc mơ ước!** 🚀

---
:::note[**LƯU Ý CUỐI CUNG**]
- Nếu **không tự host backend**, các sếp phụ thuộc vào **server của tác giả** (có thể bị ngắt kết nối).
- Để **chủ quyền dữ liệu**, các sếp nên **tự host backend** ([The Backend](https://github.com/daniel-iliesh/nest-thebackend)).
- **OpenRouter API** có giới hạn **credits**, các sếp nên **kiểm tra tài khoản** định kỳ.
:::