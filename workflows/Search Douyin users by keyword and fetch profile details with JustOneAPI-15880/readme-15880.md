---
title: "🔍 Tự Động Hóa Tìm Kiếm Người Dùng Douyin & Lấy Thông Tin Chi Tiết Với JustOneAPI (Không Code)"
description: "Workflow tự động hóa tìm kiếm người dùng Douyin theo từ khóa và lấy thông tin chi tiết (UID, hồ sơ, hoạt động) chỉ trong vài giây, giúp các sếp nghiên cứu thị trường TikTok Trung Quốc một cách hiệu quả và tiết kiệm thời gian."
slug: "tu-dong-hoa-tim-kiem-douyin-justoneapi"
tags: [n8n, automation, market-research, tiktok, justoneapi]
keywords: [n8n workflow tìm kiếm Douyin, tự động hóa nghiên cứu thị trường TikTok Trung Quốc, lấy thông tin người dùng Douyin, JustOneAPI, API Douyin]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Người Dùng Douyin & Lấy Thông Tin Chi Tiết Với JustOneAPI**

### **Giải pháp cho các sếp muốn nghiên cứu thị trường TikTok Trung Quốc mà không cần viết code**
Hiện nay, Douyin (TikTok Trung Quốc) là nền tảng xã hội có **trên 700 triệu người dùng hàng tháng**, trở thành một kho báu cho nghiên cứu thị trường, phân tích đối thủ cạnh tranh và phát hiện xu hướng mới. Tuy nhiên, việc **tìm kiếm người dùng theo từ khóa và lấy thông tin chi tiết** như UID, hồ sơ, hoạt động, hoặc thậm chí là dữ liệu tương tác vẫn là một **công việc thủ công, tốn thời gian và khó khăn** với các công cụ truyền thống.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tìm kiếm người dùng Douyin theo từ khóa** (ví dụ: "sản phẩm du lịch", "nhà hàng Việt Nam", "thời trang trẻ trung").
✅ **Lấy thông tin chi tiết** (UID, tên, giới tính, địa chỉ, số follower, nội dung video, thời gian đăng tải).
✅ **Tự động hóa toàn bộ quy trình** chỉ với **một cú nhấp chuột**, không cần viết code.
✅ **Hoạt động 24/7** khi cài đặt trên VPS, giúp các sếp **nhận dữ liệu liên tục** mà không phụ thuộc vào thời gian làm việc.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **giờ đồng hồ** tìm kiếm thủ công xuống còn **vài giây** với một workflow tự động.
- **Dữ liệu chính xác và toàn diện**: Lấy thông tin **UID, hồ sơ, hoạt động, tương tác** của người dùng Douyin một cách chính xác.
- **Phân tích thị trường hiệu quả**: Dễ dàng **so sánh đối thủ**, **phát hiện xu hướng**, hoặc **tìm kiếm khách hàng mục tiêu** trên Douyin.
- **Hoạt động liên tục**: Khi cài đặt trên VPS, workflow **chạy tự động** theo lịch trình (ví dụ: tìm kiếm hàng ngày).
- **Không cần kỹ năng code**: Sử dụng **n8n (no-code)**, các sếp chỉ cần **cấu hình API và copy/paste JSON** là có thể sử dụng.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản JustOneAPI** (đăng ký tại [justoneapi.com](https://www.justoneapi.com/)) và **API Key**.
✔ **Base URL của JustOneAPI** (thường là `https://api.justoneapi.com`).
✔ **Từ khóa tìm kiếm** (ví dụ: "sản phẩm du lịch", "nhà hàng Việt Nam").
✔ **VPS (nếu muốn chạy 24/7)** để lưu trữ workflow và hoạt động liên tục.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Workflow đã được **tạo sẵn trên n8n.io** (ID: [15880](https://n8n.io/workflows/15880)). Các sếp có thể:
- **Tải file JSON** từ link trên và import vào n8n Editor.
- **Copy/paste JSON** từ link trên vào **Import Workflow** trong n8n.

**Cách import từ JSON:**
1. Mở **n8n Editor** trên trang web hoặc VPS.
2. Nhấn **Import Workflow** (icon "cloud upload").
3. Chọn file JSON hoặc **copy toàn bộ mã JSON** từ [đây](https://n8n.io/workflows/15880) và dán vào ô **Paste JSON**.
4. Nhấn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **9 node**, nhưng các node quan trọng nhất cần cấu hình là:

#### **🔹 Node 1: "Set API and Search Parameters" (type: set)**
- **Cấu hình:**
  - Thêm **API Key** của JustOneAPI vào trường `apiKey`.
  - Thêm **Base URL** của JustOneAPI (ví dụ: `https://api.justoneapi.com`).
  - Thêm **từ khóa tìm kiếm** vào trường `keyword` (ví dụ: `"sản phẩm du lịch"`).
  - Thêm **số lượng kết quả muốn lấy** vào trường `limit` (mặc định là 10).

#### **🔹 Node 3: "Search Douyin Users by Keyword" (type: httpRequest)**
- **Cấu hình:**
  - **Method:** `POST`
  - **URL:** `https://api.justoneapi.com/douyin/search`
  - **Headers:**
    ```
    Content-Type: application/json
    Authorization: Bearer {API_KEY}
    ```
  - **Body (JSON):**
    ```json
    {
      "keyword": "{{$node["Set API and Search Parameters"].json["keyword"]}}",
      "limit": "{{$node["Set API and Search Parameters"].json["limit"]}}"
    }
    ```

#### **🔹 Node 5: "Extract SecUIDs from Results" (type: code)**
- **Lưu ý:** Node này **tự động xử lý** để lấy **SecUID** (mã duy nhất của người dùng Douyin) từ kết quả tìm kiếm.
- **Không cần chỉnh sửa** nếu workflow đã được cấu hình đúng.

#### **🔹 Node 7: "Fetch User Details from Douyin" (type: httpRequest)**
- **Cấu hình:**
  - **Method:** `POST`
  - **URL:** `https://api.justoneapi.com/douyin/user/detail`
  - **Headers:**
    ```
    Content-Type: application/json
    Authorization: Bearer {API_KEY}
    ```
  - **Body (JSON):**
    ```json
    {
      "secUid": "{{$node["Extract SecUIDs from Results"].json["secUid"]}}"
    }
    ```

#### **🔹 Node 9: "Output Final User Profiles" (type: set)**
- **Lưu ý:** Node này **hiển thị kết quả cuối cùng** bao gồm:
  - Tên người dùng
  - UID (SecUID)
  - Số follower
  - Địa chỉ
  - Nội dung video gần đây
  - Thời gian đăng tải

---

### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhấn **Run Workflow** và kiểm tra kết quả trong **Output Final User Profiles**.
   - Nếu có lỗi, kiểm tra lại **API Key** và **URL** trong các node `httpRequest`.

2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.
   - Nếu muốn **chạy tự động**, cài đặt workflow trên **VPS** và sử dụng **n8n Trigger** (Webhook) để kích hoạt định kỳ.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
- **Lưu dữ liệu vào Google Sheets/Excel**:
  - Thêm **node Google Sheets** sau "Output Final User Profiles" để **lưu kết quả tự động** vào bảng tính.
  - Cài đặt **lịch trình chạy hàng ngày** để cập nhật dữ liệu mới.

- **Gửi báo cáo qua Email/Slack**:
  - Sử dụng **node Email** (Gmail/SMTP) hoặc **node Slack** để **báo cáo kết quả** mỗi khi workflow chạy.
  - Ví dụ: Gửi **danh sách người dùng mới** hoặc **thông tin đối thủ cạnh tranh**.

- **Lọc và phân tích dữ liệu**:
  - Sử dụng **node Code** để **lọc người dùng** theo tiêu chí (ví dụ: số follower > 1000).
  - Xây dựng **báo cáo tự động** với **node PDF** hoặc **node Notion**.

- **Kết hợp với LLM (AI Chatbot)**:
  - Sử dụng **node LLM** (như Mistral AI, OpenAI) để **tóm tắt thông tin** từ hồ sơ người dùng.
  - Ví dụ: AI tự động **phân tích xu hướng** từ nội dung video của người dùng.

- **Duy trì log hoạt động**:
  - Thêm **node Database** (như MongoDB hoặc PostgreSQL) để **lưu lịch sử tìm kiếm**.
  - Sử dụng **node Log** để **in ra console** khi có lỗi xảy ra.
:::

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **nghiên cứu thị trường Douyin một cách tự động hóa**, **tiết kiệm thời gian** và **nhận dữ liệu chính xác**. Với **JustOneAPI** và **n8n**, các sếp không cần viết code mà vẫn có thể **tìm kiếm người dùng, lấy thông tin chi tiết và phân tích dữ liệu** một cách hiệu quả.

**Hành động ngay hôm nay:**
1. **Đăng ký JustOneAPI** và lấy **API Key**.
2. **Import workflow** vào n8n và **cấu hình API Key**.
3. **Test run** và **bật Active** để bắt đầu nghiên cứu!
4. **Cài đặt trên VPS** để **chạy 24/7** và **tự động hóa toàn bộ quy trình**.

👉 **Bắt đầu từ [đây](https://n8n.io/workflows/15880)** và **tìm hiểu thêm về JustOneAPI tại [justoneapi.com](https://www.justoneapi.com/)**!

---