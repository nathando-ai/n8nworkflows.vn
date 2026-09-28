---
title: "🤖 Tự Động Hóa Chuyển Phiên Bản Ghi Âm Fathom Sang Google Docs Được Định Dạng Với Tóm Tắt AI Gemini - Giảm Thời Gian Làm Báo Cáo Gấp 10 Lần"
description: "Workflow tự động hóa hoàn toàn không cần code chuyển phiên bản ghi âm cuộc họp từ Fathom sang Google Docs định dạng chuyên nghiệp, tự động tóm tắt bằng AI Gemini với các điểm chính, quyết định và hành động cần thực hiện. Giúp các sếp tiết kiệm thời gian, tránh sai sót và tự động hóa lưu trữ báo cáo."
slug: "tieu-dong-hoa-chuyen-phien-ban-fathom-sang-google-docs-voi-gemini-ai"
tags: [n8n, automation, no-code, ai-gemini, google-drive, fathom, meeting-notes]
keywords: [n8n workflow tự động hóa, chuyển phiên bản Fathom sang Google Docs, AI Gemini tóm tắt cuộc họp, tự động hóa báo cáo cuộc họp, lưu trữ báo cáo định dạng chuyên nghiệp]
---

# 🚀 **Tự Động Hóa Chuyển Phiên Bản Ghi Âm Fathom Sang Google Docs Được Định Dạng Với AI Gemini**

### **Giải Pháp Cho Các Sếp Bận Rộn: Từ Báo Cáo Thủ Công Sang Tự Động Hóa 100% AI**
Các sếp đã từng phải mất **30-60 phút** để tóm tắt, định dạng và lưu trữ báo cáo cuộc họp từ Fathom? Hay phải **quên bỏ lại** một số điểm quan trọng trong quá trình ghi chép thủ công? Workflow này sẽ **tự động hóa toàn bộ quy trình**, giúp bạn:
✅ **Tiết kiệm 100% thời gian** cho việc tóm tắt và định dạng báo cáo.
✅ **Tránh sai sót** nhờ AI Gemini phân tích và tổng hợp thông tin chính xác.
✅ **Lưu trữ sạch sẽ** trên Google Drive với định dạng chuyên nghiệp.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Đây là giải pháp an toàn, không phụ thuộc vào dịch vụ cloud miễn phí có thể ngừng hoạt động bất kỳ lúc nào.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích**               | **Chi Tiết**                                                                 |
|----------------------------|------------------------------------------------------------------------------|
| **Tiết kiệm thời gian**    | Từ **30-60 phút** thành **0 phút** cho mỗi báo cáo cuộc họp.               |
| **Định dạng chuyên nghiệp** | Google Docs được tự động **định dạng, giảm margin, và tối ưu hóa** cho đọc. |
| **Tóm tắt AI chính xác**  | Gemini AI **phân tích sâu** và trích xuất **điểm chính, quyết định, hành động** từ phiên bản. |
| **Lưu trữ an toàn**       | Tất cả báo cáo được **tự động lưu trên Google Drive**, không lo mất dữ liệu. |
| **Không phụ thuộc vào Fathom** | Dữ liệu được **sao lưu độc lập**, không bị ảnh hưởng nếu Fathom thay đổi API. |

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Fathom** (miễn phí) với **API Webhook** được kích hoạt.
✔ **Tài khoản Google Drive & Google Docs** (OAuth2).
✔ **API Key Google Gemini** ([Miễn phí tại đây](https://makersuite.google.com/app/apikey)).
✔ **Webhook URL từ Fathom** (sẽ được cấu hình sau).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/9549](https://n8n.io/workflows/9549) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **12 node**, nhưng có **3 node quan trọng nhất** cần cấu hình cẩn thận:

##### **A. Cấu Hình Credentials (Tài Khoản)**
| **Node**                     | **Credentials Cần Thiết**               | **Lưu Ý**                                                                 |
|------------------------------|------------------------------------------|----------------------------------------------------------------------------|
| **Google Gemini Chat Model** | `googlePalmApi` (API Key Gemini)        | Đăng ký tại [Google AI Pricing](https://ai.google.dev/pricing).            |
| **Convert to Google Doc**    | `googleDriveOAuth2Api`                   | Cần **quyền chỉnh sửa Google Drive**.                                   |
| **Upload File as HTML**      | `googleDriveOAuth2Api`                   | Chọn **folder mục tiêu** để lưu báo cáo.                                 |
| **Delete HTML File**         | `googleDriveOAuth2Api`                   | **Không cần chỉnh sửa**, workflow tự động xóa file tạm.                  |

##### **B. Cấu Hình Webhook (Fathom)**
1. **Mở node `Get Fathom Meeting`** (Webhook).
2. **Test URL** trước:
   - **Test URL:** `https://[your-n8n-instance]/webhook/2fab6c8f-ade4-49ba-b160-7cf6aa11cb15`
   - **Production URL:** Sử dụng khi đã **kiểm tra thành công**.
3. **Cấu hình Fathom:**
   - Vào **Fathom Dashboard → Settings → API Access**.
   - **Thêm Webhook** với URL trên và **chọn tất cả sự kiện**, đặc biệt là **"Transcript"**.

##### **C. Cấu Hình AI Meeting Analysis (Prompt Gemini)**
- **Mở node `AI Meeting Analysis`** (Chain LLM).
- **Cấu hình Prompt** để điều chỉnh nội dung tóm tắt:
  ```json
  {
    "prompt": "Tóm tắt cuộc họp này thành một báo cáo chuyên nghiệp với các phần sau:
    1. **Điểm chính** (3-5 điểm quan trọng nhất).
    2. **Quốc định** (các quyết định đã được đưa ra).
    3. **Hành động** (ai phải làm gì và deadline).
    4. **Ghi chú bổ sung** (nếu có).
    Đảm bảo định dạng HTML với tiêu đề H2 cho mỗi phần và sử dụng danh sách có dấu (*)."
  }
  ```
- **Lưu ý:** Nếu muốn **thêm/loại bỏ phần**, chỉnh sửa tại đây.

##### **D. Định Dạng Google Doc (HTML → Doc)**
- **Mở node `Improve Page Layout`** (HTTP Request).
- **Chỉnh sửa margin** (nếu cần):
  ```json
  {
    "body": {
      "requestBody": {
        "margins": {
          "top": 0.5,
          "bottom": 0.5,
          "left": 0.5,
          "right": 0.5
        }
      }
    }
  }
  ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một phiên bản mẫu:
   - Gọi một cuộc họp ngắn trên Fathom và **kiểm tra Google Drive** xem báo cáo đã xuất hiện chưa.
2. **Bật Active** khi đã **xác nhận workflow hoạt động ổn định**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Gửi Thông Báo (Slack/Email)**
   - Sau node `Convert to Google Doc`, thêm **node Slack/Email** để thông báo khi báo cáo hoàn thành.
   - **Ví dụ:**
     ```json
     {
       "webhookUrl": "https://hooks.slack.com/services/...",
       "message": "📄 Báo cáo cuộc họp đã được tự động tạo: {{ $json["fileLink"] }}"
     }
     ```

2. **Lưu Log Dữ Liệu (Google Sheets)**
   - Thêm node **Google Sheets** sau `Convert to Google Doc` để **lưu lịch sử báo cáo**.
   - **Cấu hình:**
     - **Sheet Name:** `Meeting_Logs`
     - **Columns:** `Meeting_ID, Date, Summary, Actions`

3. **Tự Động Xóa Cuộc Hợp Sau Xử Lý**
   - Thêm node **Fathom API** (HTTP Request) để **xóa cuộc họp sau khi xử lý** (nếu không cần lưu trữ).

4. **Tối Ưu Hóa API Key Gemini**
   - Sử dụng **free tier** của Gemini (đủ cho **hàng ngàn cuộc họp/Tháng**).
   - **Lưu ý:** Nếu vượt quá giới hạn, cần **cập nhật API Key mới**.

---

### 📌 **Kết Luận: Tự Động Hóa Báo Cáo Cuộc Hợp - Không Cần Code!**
Workflows này **giải phóng thời gian** của các sếp để tập trung vào **strategy** thay vì **quá trình thủ công**. Với **AI Gemini**, báo cáo không chỉ được **tóm tắt nhanh**, mà còn **định dạng chuyên nghiệp**, **lưu trữ an toàn** trên Google Drive.

**Bắt đầu ngay hôm nay!**
1. **Import workflow** và cấu hình credentials.
2. **Test với một cuộc họp mẫu**.
3. **Bật Active** và **quên đi việc tóm tắt thủ công**.

👉 **[Tải workflow ngay](https://n8n.io/workflows/9549)** và **tự động hóa báo cáo cuộc họp** của mình!

---
**Cần hỗ trợ?** Đăng ký **VPS n8n** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow **không bị gián đoạn** và **hoạt động 24/7**! 🚀