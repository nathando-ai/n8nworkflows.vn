---
title: "🚀 Tự Động Hóa Báo Cáo Thông Tin Thị Trường Multi-Platform Với Gemini AI & Decodo - Giúp Các Sếp Tiết Kiệm 20+ Giờ/Năm"
description: "Workflow tự động hóa thu thập, phân tích và tổng hợp thông tin từ Facebook, Instagram, Google trên toàn cầu bằng AI Gemini, gửi báo cáo định kỳ qua email. Giúp các sếp theo dõi xu hướng thị trường, đối thủ cạnh tranh và cơ hội kinh doanh 24/7 mà không cần code."
slug: "tieu-dong-hoa-bao-cao-thong-tin-thi-truong-multi-platform"
tags: [n8n, automation, ai-gemini, market-research, decodo, no-code]
keywords: [n8n workflow, tự động hóa báo cáo thị trường, gemini ai, decodo api, scrap facebook instagram google, báo cáo định kỳ email]
---

# 🚀 **Tự Động Hóa Báo Cáo Thông Tin Thị Trường Multi-Platform Với Gemini AI & Decodo**

### **Giải pháp cho các sếp muốn theo dõi xu hướng thị trường, đối thủ cạnh tranh và cơ hội kinh doanh mà không cần viết một dòng code nào!**

Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- **Tìm kiếm** thông tin trên Facebook, Instagram, Google về đối thủ, xu hướng thị trường, hoặc sản phẩm mới.
- **Lọc và tổng hợp** dữ liệu từ hàng trăm bài đăng, bài viết, hoặc tin tức.
- **Phân tích** nội dung để rút ra thông tin giá trị như chiến lược marketing, phản hồi khách hàng, hoặc cơ hội mới.
- **Gửi báo cáo** định kỳ cho ban lãnh đạo, nhưng lại bị quên hoặc không kịp thời.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Thu thập** dữ liệu từ **Facebook, Instagram, và Google** trên toàn cầu.
✅ **Lọc và phân tích** nội dung bằng **AI Gemini** để rút ra thông tin quan trọng.
✅ **Tổng hợp** báo cáo định kỳ và **gửi qua email** cho các sếp mỗi ngày.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 20+ giờ/năm** cho việc thu thập và phân tích dữ liệu thủ công.
- **Theo dõi đối thủ và xu hướng thị trường** một cách chính xác và liên tục.
- **Cá nhân hóa báo cáo** với thông tin phân tích sâu bằng AI Gemini.
- **Hoạt động tự động** 24/7, không phụ thuộc vào giờ làm việc của nhân viên.
- **Tăng cường quyết định kinh doanh** với dữ liệu thời thực và phân tích chất lượng cao.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Decodo API** (để scrap dữ liệu từ Facebook, Instagram, Google):
   - **Yêu cầu**: Giao diện **Web Scraping API Advanced** (có thể thử miễn phí).
   - **Hướng dẫn lấy token**: [Tại đây](https://github.com/Decodo/n8n-nodes-decodo/tree/main).
2. **Tài khoản Gmail** (để gửi báo cáo định kỳ):
   - **Yêu cầu**: OAuth 2.0 được cấu hình trong n8n.
3. **API Key Google Gemini** (để phân tích nội dung bằng AI):
   - **Lấy tại**: [Google AI Studio](https://makersuite.google.com/app/apikey).
4. **Danh sách vùng (Regions) và từ khóa (Keywords)**:
   - Ví dụ: `["Germany", "France", "USA"]` và `["marketing", "competitor", "new product"]`.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/10692](https://n8n.io/workflows/10692).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô `Paste JSON`.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Credentials**
1. **Decodo API**:
   - **Tạo credential mới** trong n8n:
     - Mở **Credentials** → **Add Credential** → Chọn **Decodo**.
     - Dán **token** từ Decodo vào trường `Authentication Token`.
   - **Lưu ý**: Nếu không có token, các sếp phải **mở gói Advanced** trên Decodo (có thể thử miễn phí).

2. **Gmail OAuth2**:
   - **Tạo credential mới** trong n8n:
     - Mở **Credentials** → **Add Credential** → Chọn **Gmail OAuth2**.
     - Đăng nhập tài khoản Gmail và cấp quyền cho n8n.

3. **Google Gemini API**:
   - **Không cần credential riêng** (n8n sẽ tự động lấy từ biến môi trường `GOOGLE_API_KEY`).
   - **Cách thiết lập**:
     - Mở **Settings** → **Environment Variables** → Thêm biến `GOOGLE_API_KEY` với giá trị API Key của Gemini.

---

#### **B. Cấu hình Node "Set - Regions"**
- **Node này định nghĩa danh sách vùng và từ khóa** mà workflow sẽ thu thập dữ liệu.
- **Cách chỉnh sửa**:
  - Nhấp vào node → Mở **Code Editor** (nút `...` → **Edit Code**).
  - **Sửa dữ liệu JSON** theo mẫu:
    ```json
    [
      {
        "region": "Germany",
        "keywords": ["marketing", "competitor"]
      },
      {
        "region": "France",
        "keywords": ["new product", "trend"]
      }
    ]
    ```
  - **Lưu ý**: Các sếp có thể thêm/bớt vùng và từ khóa tùy ý.

---

#### **C. Cấu hình Node "Schedule Trigger"**
- **Node này định thời gian chạy workflow** (mặc định là **6:00 AM hàng ngày**).
- **Cách chỉnh sửa**:
  - Nhấp vào node → Mở **Settings** → Chọn **Cron Expression**.
  - **Cập nhật biểu thức** theo nhu cầu (ví dụ: `0 6 * * *` để chạy lúc 6:00 AM).

---

#### **D. Cấu hình Node "Draft Executive Email"**
- **Node này tạo nội dung email** từ dữ liệu phân tích.
- **Cách chỉnh sửa**:
  - Nhấp vào node → Mở **Code Editor** (nút `...` → **Edit Code**).
  - **Sửa template email** để phù hợp với nội dung báo cáo (ví dụ: thay đổi tiêu đề, nội dung chi tiết).
  - **Lưu ý**: Nếu không muốn chỉnh sửa, giữ nguyên template mặc định.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra workflow):
   - Nhấp vào nút **Run Workflow** và chọn **Test Run**.
   - **Kiểm tra kết quả** trong node `Send Daily Report` (nếu có lỗi, sửa lại credentials hoặc logic).
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Status** từ `Inactive` sang `Active`.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để gửi báo cáo ngay khi có kết quả mới.
2. **Lưu log vào Google Sheets**:
   - Thêm node **Google Sheets** để ghi lại lịch sử báo cáo và dữ liệu phân tích.
3. **Tự động gửi báo cáo cho nhiều người nhận**:
   - Sử dụng node **Gmail Merge** để gửi email cho nhiều địa chỉ cùng lúc.
4. **Cập nhật từ khóa tự động**:
   - Sử dụng node **Google Sheets** để lấy danh sách từ khóa từ một sheet và truyền vào node `Set - Regions`.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** trong việc thu thập và phân tích dữ liệu.
✔ **Theo dõi thị trường và đối thủ** một cách tự động và chính xác.
✔ **Cập nhật ban lãnh đạo** với báo cáo định kỳ, chất lượng cao.

**Hãy import workflow ngay hôm nay và bắt đầu tự động hóa báo cáo thị trường của mình!** 🚀
Nếu có vấn đề, các sếp có thể tham khảo [hướng dẫn chi tiết của Decodo](https://github.com/Decodo/n8n-nodes-decodo/tree/main) hoặc liên hệ cộng đồng n8n tại [n8n.io/community](https://n8n.io/community).