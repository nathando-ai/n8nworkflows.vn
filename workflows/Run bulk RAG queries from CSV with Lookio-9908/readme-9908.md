---
title: "🔍 **Tự Động Hoá Query Bulk RAG từ CSV với Lookio – Không Cần Code!**"
description: "Tự động hóa việc gửi hàng loạt câu hỏi từ file CSV đến Lookio để lấy kết quả RAG (Retrieval-Augmented Generation) và xuất file CSV mới với cột Response tự động. Giúp tiết kiệm thời gian lên đến 90% so với cách làm thủ công."
slug: "tieu-dong-hoa-query-bulk-rag-lookio-csv"
tags: [n8n, automation, no-code, RAG, Lookio, AI, CSV, API, knowledge-retrieval]
keywords: [n8n workflow RAG, tự động hóa AI Lookio, query bulk từ CSV, RAG với n8n, tự động hóa knowledge retrieval, API Lookio]
---

# 🚀 **Tự Động Hoá Query Bulk RAG từ CSV với Lookio – Giải Pháp AI Cho Doanh Nghiệp**

### **💡 Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải:
- **Gõ hàng loạt câu hỏi** vào Lookio một cách thủ công để tra cứu thông tin từ bộ dữ liệu lớn?
- **Chờ đợi kết quả từng câu một**, mất nhiều giờ để hoàn thành?
- **Không thể tự động hóa** vì không biết code hoặc không có thời gian?
- **Muốn xuất kết quả** dưới dạng file CSV để phân tích hoặc chia sẻ với team?

**Workflow này giải quyết tất cả!** Với chỉ một file CSV chứa cột `Query`, bạn sẽ nhận được file CSV mới với cột `Response` tự động được Lookio trả về – **không cần viết một dòng code nào!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Hoàn thành hàng trăm câu hỏi trong vài phút thay vì nhiều giờ.
✅ **Chính xác 100%**: Lookio trả về kết quả dựa trên bộ dữ liệu đã upload, tránh sai sót của con người.
✅ **Tự động hóa liên tục**: Workflow hoạt động 24/7, không cần can thiệp thủ công.
✅ **Xuất file CSV sẵn sàng**: Kết quả được gộp vào file mới, dễ dàng chia sẻ hoặc phân tích.
✅ **Cá nhân hóa**: Thêm nhiều cột vào CSV để Lookio trả về thông tin chi tiết hơn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Lookio**:
   - Đăng ký tại [Lookio](https://www.lookio.app/) và tạo **1 assistant** (cài đặt bộ dữ liệu cần tra cứu).
   - Lấy **API Key** và **Assistant ID** từ Lookio (hướng dẫn tại [đây](https://docs.lookio.app/)).
2. **File CSV mẫu**:
   - File CSV phải có **cột `Query`** (dữ liệu trong cột này sẽ được gửi đến Lookio).
   - Ví dụ:
     ```
     Query
     "Tại sao doanh thu quý 2 giảm so với quý 1?"
     "Cách tính ROI cho dự án AI?"
     ```
3. **n8n Self-hosted** (không dùng phiên bản miễn phí):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [n8n.io/workflows/9908](https://n8n.io/workflows/9908).
- **Bước 2**:
  - Mở **n8n Editor** (trang chủ của n8n self-hosted).
  - Nhấp vào **Import** (icon "↑" ở góc trên bên phải).
  - Chọn file JSON vừa tải và nhấn **Import**.
  - **Hoặc** copy toàn bộ JSON và paste vào **Import Workflow** trong Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **12 node**, nhưng chỉ **5 node quan trọng** cần cấu hình kỹ:

##### **A. Node "Form Trigger" (Giao diện Upload CSV)**
- **Không cần chỉnh gì** nếu dùng mặc định.
- **Lưu ý**:
  - Workflow sẽ hiển thị một **form** cho phép bạn upload file CSV.
  - File CSV **phải có cột `Query`** (case-sensitive).

##### **B. Node "Lookio API call" (Gửi Query đến Lookio)**
- **Tham số cần thay đổi**:
  - **Header `api_key`**:
    - Điền **API Key** của Lookio (từ Dashboard Lookio).
    - Ví dụ:
      ```json
      {
        "api_key": "sk_your-lookio-api-key-here"
      }
      ```
  - **Query Parameter `assistant_id`**:
    - Điền **Assistant ID** của Lookio (từ trang quản lý assistant).
    - Ví dụ: `"assistant_id": "asst_1234567890abcdef"`
  - **Body Request**:
    - Để mặc định (n8n sẽ tự động gửi `Query` từ CSV).

##### **C. Node "Generate enriched CSV" (Xuất File CSV Kết Quả)**
- **Không cần chỉnh gì** nếu muốn file CSV có:
  - Cột `Query` (giữ nguyên).
  - Cột `Response` (được Lookio trả về).
- **Nếu muốn thêm cột khác**:
  - Sử dụng node **`Set`** để thêm dữ liệu trước khi xuất file.

##### **D. Node "Form ending and file download" (Hiển Thị Kết Quả)**
- **Không cần chỉnh gì** nếu muốn:
  - Hiển thị **link download** file CSV mới sau khi hoàn thành.
  - Hiển thị **thông báo thành công** (hoặc lỗi) cho người dùng.

##### **E. Node "Aggregate rows" (Gộp Dữ liệu Trước Xuất File)**
- **Không cần chỉnh gì** nếu muốn:
  - Workflow tự động gộp tất cả `Response` từ Lookio vào một file CSV duy nhất.

---
#### **3. Kích Hoạt ⚡️ Workflow**
- **Bước 1**: Nhấn **Active** (bật workflow).
- **Bước 2**: Upload **file CSV mẫu** (có cột `Query`) vào form.
- **Bước 3**: Chờ workflow hoàn thành (thông thường trong **vài phút** tùy số lượng query).
- **Bước 4**: Download file CSV mới từ form kết quả.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM THÊM HIỆU QUẢ]
1. **Thêm nhiều cột vào CSV**:
   - Sử dụng node **`Set`** để thêm cột `User`, `Priority`, hoặc `Timestamp` trước khi gửi query.
   - Ví dụ: Nếu muốn thêm cột `Department`, bạn có thể:
     ```json
     {
       "Department": "Marketing"
     }
     ```
   - Lookio sẽ trả về kết quả trong cột `Response` cùng với thông tin này.

2. **Lưu log hoạt động**:
   - Thêm node **`Slack`** hoặc **`Email`** để nhận thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi email báo cáo kết quả cho team.

3. **Tự động hóa định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/tuần với file CSV mới.
   - Ví dụ: Tải file CSV từ **Google Drive** hoặc **Dropbox** tự động.

4. **Kết hợp với LLM khác**:
   - Nếu muốn **sửa đổi kết quả** từ Lookio trước khi xuất file, thêm node **`LLM`** (như Mistral, GPT) để tổng hợp lại.

5. **Tối ưu API Key**:
   - Nếu sử dụng nhiều query, hãy **check rate limit** của Lookio và thêm **delay** giữa các request bằng node **`Set`** hoặc **`Delay`**.
   - Ví dụ:
     ```json
     {
       "delay": 2000 // 2 giây giữa mỗi request
     }
     ```
:::

---

### 📌 **Kết Luận: Áp Dụng Ngay Hôm Nay!**
Workflow này là **giải pháp hoàn hảo** cho các sếp:
- **Không biết code** nhưng muốn tự động hóa AI.
- **Cần tra cứu hàng loạt câu hỏi** từ bộ dữ liệu lớn.
- **Muốn tiết kiệm thời gian** và giảm sai sót thủ công.

**Hành động ngay**:
1. **Cài đặt n8n self-hosted** (nếu chưa có).
2. **Tạo assistant Lookio** và lấy API Key.
3. **Import workflow** và **chỉnh node `Lookio API call`**.
4. **Upload file CSV** và **download kết quả**!

**🚀 Cùng tự động hóa công việc AI của mình ngay bây giờ!** Nếu có vấn đề, hãy để lại comment dưới đây, các sếp sẽ được hỗ trợ chi tiết. 😊