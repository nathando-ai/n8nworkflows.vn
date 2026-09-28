---
title: "🤖 **Tự Động Hoá Scraping Facebook Group: Bài Tích Hợp Posts, Comments & Sub-comments Vào Supabase (Không Cần Code!)""
description: "Workflow này tự động lấy dữ liệu từ nhóm Facebook (bài viết, bình luận và phản hồi) và lưu trữ vào cơ sở dữ liệu Supabase, giúp các sếp phân tích thị trường một cách nhanh chóng và chính xác 24/7. Giảm thiểu công việc thủ công, tiết kiệm thời gian lên đến 80%!"
slug: "tieu-dong-hoa-scraping-facebook-group-den-supabase"
tags: [n8n, automation, market-research, facebook-scraping, supabase, apify, no-code]
keywords: [tự động hóa scrap facebook group, lấy dữ liệu facebook group, supabase automation, apify n8n, phân tích thị trường tự động]
---

# 🚀 **Tự Động Hoá Scraping Dữ Liệu Facebook Group: Từ Posts → Comments → Sub-comments → Supabase**

### **💡 Nỗi Đau Của Các Sếp Trong Phân Tích Thị Trường**
Hàng ngày, các sếp phải:
- **Tìm kiếm thủ công** trên nhóm Facebook để theo dõi xu hướng, phản hồi khách hàng hay cạnh tranh.
- **Sao chép dữ liệu** từ bài viết, bình luận và phản hồi vào Excel/Google Sheets, dễ bị lỗi và mất thời gian.
- **Không cập nhật kịp thời**, dẫn đến quyết định sai lầm khi thị trường thay đổi nhanh chóng.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy toàn bộ bài viết** từ nhóm Facebook.
✅ **Scrape bình luận và phản hồi (sub-comments)** của mỗi bài viết.
✅ **Lưu trữ dữ liệu vào Supabase** (cơ sở dữ liệu cloud tiên tiến) để phân tích dễ dàng.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tìm kiếm thủ công trên Facebook, tự động cập nhật dữ liệu mỗi khi có bài viết mới.
- **Dữ liệu chính xác & toàn diện**: Lấy cả **posts, comments và sub-comments**, không bỏ sót bất kỳ phản hồi nào.
- **Phân tích thị trường chuyên nghiệp**: Dữ liệu được lưu vào **Supabase** (có thể kết nối với Tableau, Power BI hoặc Python cho phân tích sâu).
- **Hoạt động liên tục**: Workflow chạy tự động, không phụ thuộc vào giờ làm việc của nhân viên.
- **Tính bảo mật cao**: Dữ liệu được lưu trữ trên **Supabase** (chứ không phải trên Facebook API công khai).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (để scraping Facebook):
   - [Đăng ký miễn phí Apify](https://apify.com/)
   - **API Key**: Tạo tại [Apify Console](https://apify.com/console/settings/api-keys).
2. **Tài khoản Supabase** (để lưu trữ dữ liệu):
   - [Đăng ký Supabase](https://supabase.com/)
   - **URL Database** và **API Key**: Tạo tại **Project Settings > API**.
3. **URL của nhóm Facebook** cần scraping (cần phải là nhóm **public** hoặc các sếp có quyền truy cập).
4. **Cấu trúc bảng trong Supabase** (workflow sẽ tạo 3 bảng: `posts`, `comments`, `sub_comments`).

---
:::note[Lưu ý quan trọng]
- **Facebook không cho phép scraping tự động** trên các nhóm private. Workflow này chỉ hoạt động với **nhóm công khai** hoặc nhóm các sếp có quyền truy cập.
- **Apify có giới hạn scraping**: Nếu nhóm Facebook có nhiều bài viết, các sếp cần nâng cấp gói Apify để tránh bị chặn.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/10370](https://n8n.io/workflows/10370) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **3 phần chính**, các sếp cần cấu hình cẩn thận:

##### **🔹 Phần 1: Scraping Posts**
- **Node "Run an Actor" (Apify)**:
  - **Actor**: Chọn **"facebook-group-scraper"** (hoặc tương tự, tùy thuộc vào Apify).
  - **Input Data**:
    ```json
    {
      "groupUrl": "https://www.facebook.com/groups/your-group-name/",
      "maxItems": 100
    }
    ```
  - **Credentials**: Chọn `apifyApi` (đã cấu hình trước khi import).

- **Node "Add A Post" (Supabase)**:
  - **Table**: `posts`
  - **Columns**: `title`, `content`, `url`, `createdAt` (cần điều chỉnh theo cấu trúc bảng của các sếp).

##### **🔹 Phần 2: Scraping Comments**
- **Node "ScrapeComments" (Apify)**:
  - **Actor**: Chọn **"facebook-comment-scraper"** (hoặc tương tự).
  - **Input Data**:
    ```json
    {
      "postUrl": "{{$node["Get dataset items"].jsonpath("$.items[*]")}}",
      "maxItems": 50
    }
    ```
  - **Credentials**: `apifyApi`.

- **Node "Add A Comment" (Supabase)**:
  - **Table**: `comments`
  - **Columns**: `postId`, `content`, `author`, `createdAt`.

##### **🔹 Phần 3: Scraping Sub-comments**
- **Node "Split Out"**:
  - Chọn `subComments` (nếu dữ liệu có cấu trúc phù hợp).
- **Node "Add A Comment" (Supabase - Sub-comments)**:
  - **Table**: `sub_comments`
  - **Columns**: `commentId`, `content`, `author`, `createdAt`.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow với **1-2 bài viết** để kiểm tra dữ liệu được lưu vào Supabase như mong muốn.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** để chạy tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm **node Slack/Telegram** để thông báo khi có bài viết mới hoặc phản hồi quan trọng.
   - Ví dụ: Khi có **comment có từ khóa "khiếu nại"**, workflow gửi tin nhắn cảnh báo.

2. **Lưu Log & Monitoring**:
   - Thêm **node "Set"** để lưu **log scraping** vào Supabase (bảng `logs`).
   - Sử dụng **n8n Dashboard** để theo dõi status của workflow.

3. **Tự động Gửi Báo Cáo**:
   - Kết hợp với **node Email** hoặc **Google Sheets** để gửi báo cáo định kỳ (ví dụ: hàng tuần).

4. **Tối Ưu Hiệu Suất**:
   - Nếu nhóm Facebook lớn, các sếp có thể **tăng `maxItems`** trong Apify (nhưng cần nâng cấp gói).
   - Sử dụng **Supabase Real-time** để cập nhật dữ liệu ngay khi có thay đổi.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời cung cấp **dữ liệu thị trường chính xác và toàn diện**. Bằng cách tự động hóa scraping từ Facebook và lưu trữ vào **Supabase**, các sếp có thể:
✔ **Phân tích xu hướng** một cách nhanh chóng.
✔ **Theo dõi phản hồi khách hàng** kịp thời.
✔ **Cập nhật dữ liệu 24/7** mà không cần can thiệp.

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa phân tích thị trường của mình!** 🚀

---
:::tip[Gợi ý tiếp theo]
- Nếu cần **scraping từ Instagram**, các sếp có thể kết hợp với **Apify Actor Instagram Scraper**.
- Để **tăng tính bảo mật**, các sếp có thể **mã hóa API Key** trong n8n.
:::

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/10370) | [Hướng dẫn cài n8n Self-hosted](https://docs.n8n.io/hosting/installation/)**