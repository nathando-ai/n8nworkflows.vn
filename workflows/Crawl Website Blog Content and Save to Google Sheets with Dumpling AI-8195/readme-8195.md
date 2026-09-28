---
title: "🚀 Tự Động Hóa Audit Blog: Crawl Nội Dung Website & Lưu Trữ Trên Google Sheets Với Dumpling AI"
description: "Giải pháp tự động hóa 100% không code để các sếp crawl toàn bộ nội dung blog của đối thủ, phân tích URL liên quan và lưu trữ kết quả vào Google Sheets định dạng chuyên nghiệp. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-audit-blog-crawl-website-google-sheets"
tags: [n8n, automation, market-research, ai-multimodal, google-sheets, web-scraping]
keywords: [tự động hóa audit blog, crawl website blog, dumpling ai n8n, lưu dữ liệu google sheets, phân tích đối thủ cạnh tranh]
---

# 🚀 **Tự Động Hóa Audit Blog: Crawl Website & Lưu Trữ Trên Google Sheets Với Dumpling AI**

### **Giải pháp cho các sếp cần phân tích nội dung blog đối thủ mà không cần viết code**
Hiện nay, việc phân tích nội dung blog của đối thủ để nghiên cứu xu hướng, nội dung hot hoặc gap content là một trong những công việc khó khăn và tốn thời gian nhất trong marketing digital. Các sếp thường phải:
- **Thủ công nhập URL** vào các công cụ crawl như Ahrefs, SEMrush hoặc Screaming Frog.
- **Lọc thủ công** các trang blog liên quan từ kết quả crawl.
- **Scrape nội dung** từng trang một và lưu vào Excel/Google Sheets.
- **Đánh giá chất lượng** nội dung theo nhiều tiêu chí khác nhau.

**Kết quả?** Thời gian và công sức bỏ ra quá lớn, còn kết quả lại không được chính xác hoặc cập nhật kịp thời.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động crawl website** từ URL đầu vào và phát hiện tất cả các trang blog.
✅ **Lọc và trích xuất nội dung** từ các trang blog bằng Dumpling AI (AI Multimodal của n8n).
✅ **Lưu trữ dữ liệu** vào Google Sheets với định dạng chuyên nghiệp, sẵn sàng phân tích.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị giới hạn bởi phiên bản miễn phí của n8n, các sếp nên **self-host** trên VPS riêng. Đây là giải pháp tối ưu nhất để:
- **Không bị giới hạn số lượng workflow** (n8n Cloud chỉ cho phép 3 workflow).
- **Tăng tốc độ xử lý** (self-hosted có thể xử lý nhiều request đồng thời).
- **Bảo mật dữ liệu** (dữ liệu crawl và nội dung blog không lưu trên máy chủ của n8n).

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh để chạy workflow này ổn định)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Dữ liệu chính xác và toàn diện**: Crawl tất cả trang blog, không bỏ sót URL nào.
- **Cập nhật tự động**: Khi URL mới được thêm vào website, workflow sẽ tự động crawl và cập nhật.
- **Dữ liệu sẵn sàng phân tích**: Lưu vào Google Sheets với định dạng chuyên nghiệp, có thể kết hợp với Power BI, Looker Studio hoặc Excel.
- **Không cần kỹ năng code**: Sử dụng n8n với giao diện drag-and-drop, dễ dàng tùy chỉnh.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để tạo và quản lý Google Sheets).
2. **API Key của Dumpling AI** (n8n sẽ sử dụng để crawl và scrape nội dung).
   - Đăng ký tại: [https://dumpling.ai](https://dumpling.ai)
   - Sau khi đăng ký, lấy **API Key** từ Dashboard.
3. **Credentials cho Google Sheets OAuth2** (để workflow có quyền truy cập vào Sheets).
   - Cách thiết lập:
     - Vào n8n Editor → **Credentials** → **Add Credential** → Chọn **Google Sheets OAuth2**.
     - Theo hướng dẫn để kết nối tài khoản Google.
4. **URL của website cần crawl** (các sếp sẽ nhập vào form khi kích hoạt workflow).

---
:::note[Lưu ý quan trọng]
- **Dumpling AI có giới hạn request** (miễn phí: ~1000 request/tháng). Nếu crawl nhiều website, các sếp nên nâng cấp plan.
- **Google Sheets cần quyền chỉnh sửa tự động**: Đảm bảo tài khoản OAuth2 có quyền **Editor** trên Sheet.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng hai cách:
- **Tải file JSON** từ [n8n.io/workflows/8195](https://n8n.io/workflows/8195) và import vào n8n Editor.
- **Copy JSON** từ trang trên và paste vào **Import Workflow** trong n8n Editor.

**Cách import:**
1. Mở n8n Editor (n8n.io hoặc self-hosted).
2. Nhấn **Import** → **Import from JSON**.
3. Chọn file JSON hoặc paste JSON từ trang n8n.io.
4. Nhấn **Import**.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng sau:

##### **A. Node "Form Submission" (Trigger)**
- **Tên node**: Form Submission
- **Cấu hình**:
  - Thêm **1 field text** với tên `clientUrl` (đây là URL website cần crawl).
  - Ví dụ: Nếu các sếp muốn crawl website của đối thủ là `https://doithu.com`, sẽ nhập URL này vào form.

##### **B. Node "Create Blog Audit Sheet" (Google Sheets)**
- **Tên node**: Create Blog Audit Sheet
- **Cấu hình**:
  - Chọn **credentials**: `googleSheetsOAuth2Api` (đã thiết lập trước).
  - **Spreadsheet Name**: Đặt tên Sheet theo định dạng `Blog_Audit_[Tên_DoiThu]_[NgayThang]` (ví dụ: `Blog_Audit_VietNamNet_202405`).
  - **Sheet Name**: `Audit_Data`.

##### **C. Node "Dumpling AI: Crawl Website" (HTTP Request)**
- **Tên node**: Dumpling AI: Crawl Website
- **Cấu hình**:
  - **Credentials**: `httpHeaderAuth` (n8n sẽ tự tạo, không cần thiết lập trước).
  - **Method**: `POST`
  - **URL**: `https://api.dumpling.ai/crawl`
  - **Headers**:
    ```
    Content-Type: application/json
    Authorization: Bearer [API_KEY_DUMPLING_AI]
    ```
  - **Body (JSON)**:
    ```json
    {
      "url": "{{ $node["Form Submission"].json["clientUrl"] }}",
      "depth": 2,
      "followLinks": true,
      "filter": {
        "path": ["/blog", "/san-pham", "/tin-tuc"] // Thêm các path blog của đối thủ
      }
    }
    ```
    - **Lưu ý**: Thay đổi `path` để phù hợp với cấu trúc URL của website cần crawl.

##### **D. Node "Extract Blog URLs" (Code)**
- **Tên node**: Extract Blog URLs
- **Cấu hình**:
  - Mở **Code Editor** và thay đổi logic để lọc URL blog.
  - **Mẫu code**:
    ```javascript
    // Lấy danh sách URL từ crawl
    const crawledUrls = $input.all();

    // Lọc URL chứa từ khóa blog (ví dụ: /blog/, /tin-tuc/, /article/)
    const blogUrls = crawledUrls
      .filter(url => {
        return url.url.includes('/blog/') ||
               url.url.includes('/tin-tuc/') ||
               url.url.includes('/article/');
      })
      .map(url => ({
        url: url.url,
        title: url.title,
        statusCode: url.statusCode
      }));

    // Trả về kết quả
    return blogUrls;
    ```

##### **E. Node "Dumpling AI: Scrape Blog Pages" (HTTP Request)**
- **Tên node**: Dumpling AI: Scrape Blog Pages
- **Cấu hình**:
  - **Method**: `POST`
  - **URL**: `https://api.dumpling.ai/scrape`
  - **Headers**:
    ```
    Content-Type: application/json
    Authorization: Bearer [API_KEY_DUMPLING_AI]
    ```
  - **Body (JSON)**:
    ```json
    {
      "urls": "{{ $node["Extract Blog URLs"].json }}"
    }
    ```
  - **Lưu ý**: Đảm bảo `API_KEY_DUMPLING_AI` được điền chính xác.

##### **F. Node "Save Blog Data to Google Sheets" (Google Sheets)**
- **Tên node**: Save Blog Data to Google Sheets
- **Cấu hình**:
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Spreadsheet ID**: Lấy từ URL của Sheet (ví dụ: `https://docs.google.com/spreadsheets/d/[SPREADSHEET_ID]/edit`).
  - **Sheet Name**: `Audit_Data`.
  - **Operation**: `append` (lưu dữ liệu mới vào cuối Sheet).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với URL mẫu:
   - Nhập URL của website vào form (ví dụ: `https://doithu.com`).
   - Chạy workflow và kiểm tra kết quả trong Google Sheets.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động tạo Sheet mới cho mỗi URL**:
   - Sử dụng node **Code** để tự động tạo tên Sheet theo định dạng `Blog_Audit_[Tên_DoiThu]_[NgayThang]` thay vì nhập thủ công.

2. **Gửi báo cáo định kỳ qua Email/Slack**:
   - Kết hợp với node **Email** hoặc **Slack** để gửi báo cáo tự động hàng tuần.
   - Ví dụ: Sau khi crawl xong, workflow gửi link Sheet qua Email của các sếp.

3. **Lọc nội dung blog theo từ khóa**:
   - Sử dụng Dumpling AI để phân tích nội dung và đánh giá chất lượng (ví dụ: độ dài bài viết, từ khóa chính, chất lượng SEO).
   - Thêm node **Code** để phân tích và lưu kết quả vào Sheet.

4. **Lưu log hoạt động**:
   - Sử dụng node **Sticky Note** hoặc **Database** (n8n-nodes-base.database) để lưu lịch sử crawl và trạng thái của workflow.

5. **Kết hợp với Power BI/Looker Studio**:
   - Sau khi dữ liệu được lưu vào Google Sheets, các sếp có thể kết nối với **Power BI** hoặc **Looker Studio** để tạo báo cáo visualize.

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa việc crawl và phân tích nội dung blog của đối thủ. Bằng cách sử dụng **Dumpling AI** và **n8n**, các sếp có thể:
✔ **Tiết kiệm thời gian** lên đến 80% so với cách làm thủ công.
✔ **Nhận dữ liệu chính xác và cập nhật** mỗi khi website đối thủ có nội dung mới.
✔ **Lưu trữ và phân tích dễ dàng** với Google Sheets.

**Hành động ngay hôm nay!**
1. **Self-host n8n** trên VPS để đảm bảo workflow hoạt động ổn định.
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Nhập URL website** và bắt đầu crawl!

**Nếu các sếp cần hỗ trợ thêm**, có thể liên hệ với cộng đồng n8n hoặc để lại comment bên dưới. Chúc các sếp thành công! 🚀