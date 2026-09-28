---
title: "🚀 Tự Động Hóa Thông Tin Thông Minh về Đối Thủ: Từ Crunchbase Sang ClickUp (Không Cần Code)"
description: "Workflow tự động hóa lấy dữ liệu đối thủ từ Crunchbase và tạo nhiệm vụ theo dõi trên ClickUp, giúp các sếp tiết kiệm thời gian và không bỏ lỡ bất kỳ thông tin mới nào về đối thủ cạnh tranh."
slug: "tieu-dong-hoa-thong-tin-doi-thu-crunchbase-sang-clickup"
tags: [n8n, automation, marketing, crunchbase, clickup, no-code]
keywords: [n8n workflow, tự động hóa marketing, crunchbase api, clickup automation, theo dõi đối thủ cạnh tranh, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Thông Tin Thông Minh về Đối Thủ: Từ Crunchbase Sang ClickUp**

## 🔍 **Nỗi Đau Của Các Sếp: Thiếu Thông Tin Đối Thủ Kịp Thời**
Các sếp thường phải mất nhiều thời gian để theo dõi thông tin về đối thủ cạnh tranh thủ công: tra cứu trên Crunchbase, ghi chú vào Google Sheet, hoặc nhắc nhở đồng nghiệp kiểm tra. Kết quả là:
- **Thông tin không kịp thời**: Đối thủ có thông tin mới nhưng các sếp mới biết sau khi họ đã áp dụng.
- **Tốn thời gian**: Phải tra cứu, sao chép, và tạo nhiệm vụ cho từng đối thủ một.
- **Rủi ro bỏ sót**: Nhiều thông tin quan trọng bị quên hoặc không được theo dõi.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động hóa toàn bộ quy trình: từ lấy dữ liệu Crunchbase đến tạo nhiệm vụ trên ClickUp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thủ công trên Crunchbase hoặc tạo nhiệm vụ trên ClickUp.
- **Dữ liệu chính xác và kịp thời**: Lấy thông tin mới nhất từ API Crunchbase và chuyển ngay vào ClickUp.
- **Tự động hóa hoàn toàn**: Chỉ cần nhập tên đối thủ, workflow sẽ tự động xử lý.
- **Nhiệm vụ được theo dõi**: Mỗi thông tin mới đều được chuyển thành nhiệm vụ trên ClickUp, đảm bảo không bỏ sót.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **API Key của Crunchbase**:
   - Đăng ký tại [Crunchbase Developer Portal](https://developer.crunchbase.com/) để lấy API Key.
   - Lưu ý: API Key này sẽ được sử dụng trong node `Fetch Crunchbase Data`.
2. **Tài khoản ClickUp**:
   - Tạo một tài khoản ClickUp và chuẩn bị một **Space** hoặc **Board** để lưu nhiệm vụ.
   - Lưu ý: Các sếp cần **quyền tạo nhiệm vụ** trong ClickUp.
3. **Credentials trong n8n**:
   - Thiết lập **Crunchbase API Key** trong n8n (trong node `Fetch Crunchbase Data`).
   - Thiết lập **ClickUp API Key** và **Token** (trong node `Create Review Task in ClickUp`).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### 1. **Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấp vào **Create Workflow** → **Import Workflow**.
3. Chọn file JSON hoặc dán JSON từ [link gốc](https://n8n.io/workflows/4728) vào ô **Paste JSON**.
4. Nhấp **Import** để hoàn tất.

---
### 2. **Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **5 node chính**, các sếp cần chú ý cấu hình như sau:

#### **Node 1: Manual Trigger**
- **Chức năng**: Cho phép chạy workflow thủ công khi cần test hoặc điều chỉnh.
- **Lưu ý**: Node này không tự động kích hoạt, các sếp phải nhấp vào nút **Run Workflow** để bắt đầu.

#### **Node 2: Set Competitor Name**
- **Chức năng**: Nhập tên đối thủ cần theo dõi (ví dụ: "Stripe, Inc.").
- **Cấu hình**:
  - Điền vào trường `Competitor` với tên công ty cần tra cứu.
  - Ví dụ:
    ```json
    {
      "Competitor": "Stripe, Inc."
    }
    ```
- **Lưu ý**: Sau khi hoàn tất, các sếp có thể thay thế node này bằng một **list từ Google Sheet** hoặc **database** để tự động hóa hoàn toàn.

#### **Node 3: Generate Crunchbase Slug**
- **Chức năng**: Chuyển đổi tên công ty thành **slug** phù hợp với API Crunchbase (ví dụ: "Stripe, Inc." → "stripe-inc").
- **Cách hoạt động**:
  - Chuyển toàn bộ chữ thành chữ thường.
  - Loại bỏ dấu câu và thay thế khoảng trắng bằng dấu gạch nối (`-`).
- **Lưu ý**: Slug này sẽ được sử dụng trong API call tiếp theo.

#### **Node 4: Fetch Crunchbase Data**
- **Chức năng**: Lấy dữ liệu từ Crunchbase bằng API.
- **Cấu hình**:
  - **URL API**: `https://api.crunchbase.com/api/v4/entities/organizations/{slug}?user_key={API_KEY}`
    - Thay `{slug}` bằng kết quả từ node `Generate Crunchbase Slug`.
    - Thay `{API_KEY}` bằng API Key của Crunchbase (đã chuẩn bị trước).
  - **Headers**:
    - `Accept`: `application/json`
    - `Content-Type`: `application/json`
  - **Method**: `GET`
- **Lưu ý**:
  - Nếu API trả về lỗi, kiểm tra lại **API Key** và **slug**.
  - Dữ liệu trả về bao gồm: tên công ty, ngày cập nhật, tổng vốn đầu tư, trang web, và mô tả.

#### **Node 5: Create Review Task in ClickUp**
- **Chức năng**: Tạo nhiệm vụ trên ClickUp để theo dõi thông tin mới về đối thủ.
- **Cấu hình**:
  - **ClickUp API Key**: Đăng ký tại [ClickUp Developer Portal](https://clickup.com/api) để lấy.
  - **Token**: Tạo một **Personal Access Token** trong ClickUp.
  - **Thông tin nhiệm vụ**:
    - **Tiêu đề**: `Review Crunchbase Update: {Tên Công Ty}`
    - **Mô tả**: Bao gồm tất cả thông tin từ Crunchbase (ví dụ: tên công ty, ngày cập nhật, mô tả, vốn đầu tư, trang web).
    - **Board/List**: Chọn **Board** và **List** trong ClickUp để lưu nhiệm vụ.
- **Lưu ý**:
  - Đảm bảo **quyền tạo nhiệm vụ** trong ClickUp.
  - Các sếp có thể tùy chỉnh nội dung nhiệm vụ theo nhu cầu.

---
### 3. **Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhập tên đối thủ vào node `Set Competitor Name`.
   - Nhấp vào nút **Run Workflow** để kiểm tra.
   - Kiểm tra kết quả trong node `Fetch Crunchbase Data` và `Create Review Task in ClickUp`.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH TIẾP CẬN THÊM]
1. **Tự Động Hóa Theo Dõi Nhiều Đối Thủ**:
   - Thay vì nhập tên đối thủ thủ công, các sếp có thể sử dụng **Google Sheets** hoặc **Excel** để lưu danh sách đối thủ.
   - Sử dụng node **Google Sheets** để lấy danh sách và chuyển vào node `Set Competitor Name` bằng vòng lặp (`Loop`).

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node **Email** hoặc **Slack** để gửi báo cáo tổng hợp về các cập nhật mới nhất của đối thủ.
   - Ví dụ: Gửi email hàng tuần tổng hợp tất cả nhiệm vụ mới trên ClickUp.

3. **Lưu Log Dữ Liệu**:
   - Sử dụng node **Sticky Note** hoặc **Google Drive** để lưu lại lịch sử dữ liệu đã lấy từ Crunchbase.
   - Điều này giúp các sếp theo dõi sự thay đổi của đối thủ qua thời gian.

4. **Kết Hợp Với AI**:
   - Sử dụng node **LLM** (như Mistral AI) để phân tích dữ liệu và tạo báo cáo tự động về xu hướng của đối thủ.
   - Ví dụ: Nhận xét về sự tăng giảm vốn đầu tư hoặc thay đổi mô tả công ty.

5. **Thông Báo Trên Slack/Telegram**:
   - Khi có thông tin mới về đối thủ, workflow có thể gửi thông báo ngay lập tức trên Slack hoặc Telegram.
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thực hiện.
:::

---

## 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** quy trình theo dõi đối thủ cạnh tranh, từ tra cứu trên Crunchbase đến tạo nhiệm vụ trên ClickUp. Kết quả là:
✅ **Tiết kiệm thời gian** và công sức.
✅ **Dữ liệu kịp thời** và chính xác.
✅ **Không bỏ sót bất kỳ thông tin quan trọng nào**.

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa marketing của mình!** 🚀

---
**Nếu cần hỗ trợ thêm**, các sếp có thể liên hệ với tác giả Yaron Been qua:
- [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
- [YouTube](https://www.youtube.com/@YaronBeen/videos)