---
title: "🎥 Tự Động Hóa Sáng Tạo Nội Dung Video AI Cho Mạng Xã Hội Với Perplexity & OpenAI - N8n"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp tạo ra hàng loạt ý tưởng video AI chất lượng cao cho TikTok, Instagram, YouTube chỉ trong vài giây mỗi ngày. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công, đồng thời đảm bảo nội dung cá nhân hóa và liên tục."
slug: "tieu-dong-hoa-tao-noi-dung-video-ai-perplexity-openai"
tags: [n8n, automation, content-creation, ai-multimodal, openai, perplexity, google-sheets, no-code]
keywords: [n8n workflow tự động hóa, tạo nội dung video AI, tự động hóa sáng tạo nội dung, Perplexity API, OpenAI API, tự động hóa content marketing, tự động hóa TikTok/Instagram]
---

# 🚀 **Tự Động Hóa Sáng Tạo Nội Dung Video AI Cho Mạng Xã Hội Với Perplexity & OpenAI**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tạo hàng trăm ý tưởng video AI** chỉ trong vài giây mỗi ngày.
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Cập nhật nội dung liên tục** mà không cần can thiệp.
- **Tích hợp với Google Sheets** để quản lý và phân tích hiệu quả.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải ngồi suy nghĩ hoặc viết nội dung thủ công hàng ngày.
- **Nội dung cá nhân hóa**: Hệ thống tự động tạo ý tưởng phù hợp với ngành nghề, thị trường mục tiêu của doanh nghiệp.
- **Hoạt động liên tục 24/7**: Workflow chạy tự động theo lịch trình, đảm bảo nội dung luôn được cập nhật.
- **Dữ liệu tập trung**: Tất cả ý tưởng được lưu vào Google Sheets, dễ dàng theo dõi và phân tích.
- **Tích hợp AI cao cấp**: Sử dụng Perplexity và OpenAI để tạo ra nội dung sáng tạo, chuyên nghiệp.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Perplexity API**: [Đăng ký tại đây](https://www.perplexity.ai/account/api/keys).
- **Tài khoản OpenAI API**: [Đăng ký tại đây](https://platform.openai.com/).
- **Tài khoản Google Sheets**: [Mẫu template đã sẵn sàng](https://docs.google.com/spreadsheets/d/1UcvTSCuKN_rXm6amblLyZ_Ogfk5tKuryYEBAlRoznpQ/edit?usp=sharing).
- **Tài khoản Gmail**: Để nhận thông báo khi workflow hoàn thành.
- **VPS cho n8n (khuyến nghị)**: Để workflow chạy ổn định 24/7.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấn **"Create new workflow"** và chọn **"Import from JSON"**.
3. Dán JSON từ [link gốc](https://n8n.io/workflows/5995) hoặc tải file JSON từ trang này.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình API Keys**
- **Perplexity API**:
  - Mở các node `Topic 1`, `Topic 2`, `Topic 3` và điền **Perplexity API Key** vào trường `Authorization`.
  - Cập nhật **niche** (ngành nghề) phù hợp với doanh nghiệp trong các node này.

- **OpenAI API**:
  - Đi đến **Credentials** trong n8n và thêm **OpenAI API Key** với tên `openAiApi`.
  - Trong node `Content Generation`, chọn `openAiApi` trong trường `credentials`.

#### **B. Cấu hình Google Sheets**
- **Tải và sử dụng template**: [Mẫu Google Sheets](https://docs.google.com/spreadsheets/d/1UcvTSCuKN_rXm6amblLyZ_Ogfk5tKuryYEBAlRoznpQ/edit?usp=sharing).
- Trong node `Save Data`, chọn **Google Sheets OAuth2 API** với tên `googleSheetsOAuth2Api`.
- Chọn **Sheet Name** và **Range** phù hợp (ví dụ: `Sheet1!A1`).

#### **C. Cập nhật thông tin cá nhân**
- Trong node `About me`, cập nhật thông tin về doanh nghiệp (ví dụ: tên, ngành nghề, mục tiêu nội dung).

#### **D. Thiết lập lịch trình**
- Node `Schedule Trigger` sẽ chạy workflow theo lịch trình (ví dụ: hàng ngày lúc 8h sáng). Các sếp có thể điều chỉnh thời gian trong node này.

#### **E. Cấu hình Gmail**
- Trong node `Notify user`, chọn **Gmail OAuth2** với tên `gmailOAuth2`.
- Điền địa chỉ email muốn nhận thông báo khi workflow hoàn thành.

### **3. Kích hoạt ⚡️**
1. **Test Run**: Nhấn **"Run"** để kiểm tra workflow với dữ liệu mẫu.
2. **Active Workflow**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Tích hợp Slack/Telegram**: Thay vì Gmail, các sếp có thể gửi thông báo qua Slack hoặc Telegram để theo dõi kết quả.
- **Lưu log hoạt động**: Sử dụng node `stickyNote` để ghi lại các lỗi hoặc thông tin debug.
- **Tự động gửi báo cáo**: Kết hợp với **Google Sheets** để tạo báo cáo định kỳ về hiệu quả của nội dung.
- **Tối ưu hóa nội dung**: Sử dụng node `code` để thêm logic xử lý dữ liệu (ví dụ: loại bỏ nội dung trùng lặp).
:::

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa sáng tạo nội dung video AI mà không cần viết code. Với **Perplexity và OpenAI**, hệ thống sẽ tạo ra hàng loạt ý tưởng sáng tạo, phù hợp với ngành nghề và thị trường mục tiêu. **Bắt đầu ngay** và tiết kiệm thời gian, công sức cho việc tạo nội dung hàng ngày!

👉 **Bắt đầu tự động hóa ngay hôm nay!** [Tải workflow](https://n8n.io/workflows/5995) và cài đặt trên VPS của mình.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Cần hỗ trợ?** Liên hệ với **GainFlow AI** qua email: [info.gainflow@gmail.com](mailto:info.gainflow@gmail.com) hoặc điền form: [https://docs.google.com/forms/d/e/1FAIpQLSfIiXdw4HMcI2HM-Obng13j_RFiKv7X-mjOVm_mcy2ucRA8EA/viewform](https://docs.google.com/forms/d/e/1FAIpQLSfIiXdw4HMcI2HM-Obng13j_RFiKv7X-mjOVm_mcy2ucRA8EA/viewform).