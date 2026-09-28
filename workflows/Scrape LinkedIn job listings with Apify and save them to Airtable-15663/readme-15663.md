---
title: "🚀 Tự Động Hoàn Chỉnh Scrape Job LinkedIn → Airtable (Không Cần Code)"
description: "Workflow tự động hóa lấy danh sách tuyển dụng từ LinkedIn mỗi tuần vào Airtable, tiết kiệm 10+ giờ công sức cho bộ phận HR. Hoạt động 24/7, GDPR-compliant, và dễ dàng tùy chỉnh."
slug: "tieu-dong-scrape-linkedin-airtable"
tags: [n8n, automation, hr, linkedin-scraper, airtable, apify]
keywords: [tự động hóa scrape linkedin, lấy job linkedin vào airtable, workflow n8n hr, apify actor, tự động hóa tuyển dụng]
---

# 🚀 **Tự Động Scrape Job LinkedIn → Airtable (Không Cần Code)**

### **Nỗi Đau Của Các Sếp HR**
Mỗi tuần, bộ phận HR phải thủ công:
- **Tìm kiếm** các vị trí tuyển dụng trên LinkedIn theo nhiều keyword khác nhau.
- **Lưu trữ** thông tin vào Airtable (hoặc Excel) để theo dõi ứng viên.
- **Cập nhật** danh sách định kỳ, mất **10+ giờ/tháng** chỉ vì công việc lặp lại.

**Workflow này giải quyết tất cả!** Chỉ cần **cài đặt 1 lần**, nó sẽ:
✅ **Scrape** tất cả job posting từ LinkedIn theo các keyword bạn định nghĩa.
✅ **Lưu trữ** dữ liệu vào Airtable (hoặc cơ sở dữ liệu khác) **mỗi tuần tự động**.
✅ **Tiết kiệm** 100% thời gian thủ công, giảm thiểu sai sót.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho bộ phận HR.
- **Dữ liệu chính xác 100%**, không bị lỗi copy-paste.
- **Tự động cập nhật** mỗi tuần (hoặc theo lịch bạn đặt).
- **Dễ dàng mở rộng** (thêm keyword, thay đổi nguồn dữ liệu).
- **GDPR-compliant** (nếu tự host trên VPS).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (để scrape LinkedIn):
   - [Đăng ký Apify](https://apify.com/) (miễn phí cho 100 run/tháng).
   - **Lấy API Token**: Tạo tại [Apify Dashboard](https://apify.com/dashboard/tokens) → **Personal Access Token**.
2. **Tài khoản Airtable**:
   - [Đăng ký Airtable](https://airtable.com/) (miễn phí cho 1 bảng dữ liệu).
   - **Lấy API Key**: Tạo tại [Airtable API Keys](https://airtable.com/api).
3. **Bảng Airtable** để lưu kết quả:
   - Tạo 1 bảng mới với các trường phù hợp (ví dụ: `Tên Công Ty`, `Mô Tả Vị Trí`, `Liên Hệ`, `Ngày Bài Viết`).
4. **VPS (nếu muốn chạy 24/7)**:
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n Workflow](https://n8n.io/workflows/15663) (ấn **Export** trên canvas).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON vừa tải.
- **Hoặc copy JSON** từ file → Paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **4 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: "Every Week at 10am" (ScheduleTrigger)**
- **Chỉnh lịch chạy**:
  - Mặc định là **mỗi tuần lúc 10h sáng** (UTC).
  - **Cách chỉnh**:
    - Nhấn **Edit** → Chọn **Time Zone** (Việt Nam: `Asia/Ho_Chi_Minh`).
    - Đặt **Frequency** theo nhu cầu (ví dụ: **Daily**, **Weekly**, **Monthly**).

##### **🔹 Node 2: "Set Search Queries" (Set Node)**
- **Cập nhật keyword tìm kiếm**:
  - Mở **Edit Fields** → Thay đổi giá trị trong `Query 1`, `Query 2`, `Query 3` (ví dụ: `"Software Engineer"`, `"Data Analyst"`, `"Product Manager"`).
  - **Mở rộng**: Thêm nhiều keyword hơn bằng cách sao chép `Query 3` và đổi tên.

##### **🔹 Node 3: "Run Apify Actor and Fetch Results" (HTTP Request)**
- **Cấu hình Apify Actor**:
  - **URL Apify Actor**: Thay đổi thành **ID Actor của bạn** (ví dụ: `https://api.apify.com/v2/actors/your-actor-id/run`).
    - **Lấy ID Actor**:
      1. Tạo **Actor mới** trên [Apify Dashboard](https://apify.com/dashboard/actors).
      2. Chọn **Actor LinkedIn Job Scraper** (hoặc tự tạo Actor bằng Python/JS).
      3. Copy **Actor ID** từ URL (ví dụ: `your-actor-id` trong `https://apify.com/your-actor-id`).
  - **Headers**:
    - Thêm `Authorization: Bearer YOUR_APIFY_API_TOKEN` (điền token từ bước chuẩn bị).
  - **Body (JSON)**:
    ```json
    {
      "input": {
        "searchQueries": [
          "{{$node["Set Search Queries"].json["Query 1"]}}",
          "{{$node["Set Search Queries"].json["Query 2"]}}",
          "{{$node["Set Search Queries"].json["Query 3"]}}"
        ]
      }
    }
    ```
    *(Nếu Apify Actor yêu cầu cấu hình khác, tham khảo [docs Apify](https://docs.apify.com/api/actors/run).)*

##### **🔹 Node 4: "Create Record in Airtable" (Airtable Node)**
- **Kết nối Airtable**:
  - Nhấn **Edit** → Chọn **Airtable Token** (điền `airtableTokenApi` từ bước chuẩn bị).
- **Chọn Base & Table**:
  - **Base**: Chọn **Airtable Base** bạn muốn lưu dữ liệu.
  - **Table**: Chọn **Table** phù hợp (ví dụ: `Job Listings`).
- **Mapping Fields**:
  - Cấu hình **mapping** giữa dữ liệu từ Apify và trường trong Airtable.
  - Ví dụ:
    | Apify Field (JSON Path)       | Airtable Field |
    |-------------------------------|----------------|
    | `$.data[0].title`             | `Tên Công Việc` |
    | `$.data[0].company`           | `Công Ty`      |
    | `$.data[0].description`       | `Mô Tả`        |
    | `$.data[0].publishedAt`       | `Ngày Bài Viết`|
    | `$.data[0].url`               | `Link Job`     |

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** → Kiểm tra kết quả trong Airtable.
  - Nếu có lỗi, kiểm tra **Logs** trong node HTTP Request.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM TIẾP]
1. **Thêm Slack/Telegram Notification**:
   - Sau node Airtable, thêm **Slack Node** hoặc **Telegram Bot Node** để thông báo khi scrape thành công.
   - Ví dụ: `Tự động scrape LinkedIn thành công! Có {{$node["Create Record in Airtable"].json.length}} job mới.`
2. **Lưu Log vào Google Sheets**:
   - Thêm **Google Sheets Node** để ghi lịch sử scrape (giúp theo dõi lỗi).
3. **Tùy Chỉnh Apify Actor**:
   - Nếu muốn scrape **nhiều hơn 3 keyword**, tăng số lượng `searchQueries` trong Body HTTP Request.
   - Sử dụng **Actor khác** (ví dụ: scrape **Indeed**, **Glassdoor**) bằng cách thay đổi URL Actor.
4. **Xử Lý Lỗi**:
   - Thêm **Error Handling** bằng **If Node** để gửi email (Gmail Node) khi scrape thất bại.
5. **Tự Host GDPR-Compliant**:
   - Nếu lưu trữ dữ liệu nhạy cảm, **tự host n8n trên VPS** (không qua n8n.cloud).
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng bộ phận HR khỏi công việc lặp lại**, giúp các sếp:
✔ **Tiết kiệm 10+ giờ/tháng**.
✔ **Có dữ liệu tuyển dụng chính xác, cập nhật mỗi tuần**.
✔ **Dễ dàng mở rộng** (thêm keyword, thay đổi nguồn dữ liệu).

**Hành động ngay!**
1. **Chuẩn bị tài khoản Apify + Airtable** (nếu chưa có).
2. **Import workflow** và **cấu hình theo hướng dẫn**.
3. **Bật Active** và **quên đi công việc thủ công!**

---
**Cần hỗ trợ thêm?**
- **Liên hệ Allan Vaccarizi** (tác giả workflow) tại:
  - [LinkedIn](https://www.linkedin.com/in/allanvaccarizi/)
  - [Growth-AI.fr](https://www.growth-ai.fr/)
- **Cần workflow tùy chỉnh?** Đăng ký [dịch vụ custom](https://www.growth-ai.fr/) để có giải pháp phù hợp với doanh nghiệp của các sếp!

---
**💡 Lưu ý cuối:**
- **Apify có giới hạn free** (100 run/tháng). Nếu scrape nhiều job, cần **upgrade plan**.
- **Airtable free** chỉ cho 1 bảng dữ liệu. Nếu cần nhiều bảng, **upgrade plan Pro**.