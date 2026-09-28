---
title: "🚀 Tự Động Hóa Onboarding Creator Cá Nhân Hóa Trên HubSpot Với AI GPT-4 & Dữ Liệu Influencer.club"
description: "Workflow tự động hóa 100% không code giúp các sếp enrich dữ liệu creator từ email, phân loại theo tier và niche, cá nhân hóa trải nghiệm onboarding trên HubSpot để tăng tỷ lệ activation lên 30-50%. Sử dụng API influencers.club + GPT-4 để phân tích đa nền tảng (Instagram, TikTok, YouTube, Twitch...) và tối ưu hóa quy trình hợp tác."
slug: "tieu-dong-hoa-onboarding-creator-ca-nhan-hoa-tren-hubspot"
tags: [n8n, automation, hubspot, ai, influencer-marketing, gpt-4, no-code]
keywords: [tự động hóa hubspot, cá nhân hóa onboarding creator, influencers.club api, gpt-4 tự động hóa, workflow n8n cho marketing, enrich creator data]
---

# 🚀 **Tự Động Hóa Onboarding Creator Cá Nhân Hóa Trên HubSpot Với AI GPT-4 & Dữ Liệu Influencer.club**

### **Giải pháp cho vấn đề:**
Các sếp đang gặp khó khăn khi phải **thủ công** phân tích và cá nhân hóa trải nghiệm cho mỗi creator mới ký hợp tác. Thời gian tiêu tốn, tỷ lệ activation thấp, và thiếu tính chính xác trong phân loại niche/tier khiến quy trình trở nên rườm rà. **Workflow này tự động hóa toàn bộ quy trình** từ enrich dữ liệu creator (từ email) đến phân loại tier/niche, sau đó cá nhân hóa onboarding trên HubSpot – giúp tăng **tỷ lệ activation lên 30-50%** mà không cần viết một dòng code nào!

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10-15 giờ/ngày** cho team marketing: Không cần thủ công enrich dữ liệu creator từ nhiều nền tảng (Instagram, TikTok, YouTube, Twitch, OnlyFans...).
- **Cá nhân hóa trải nghiệm onboarding**: Mỗi creator nhận được nội dung và gợi ý phù hợp với niche và tier của mình (Nano, Micro, Macro).
- **Tăng tỷ lệ activation**: Dữ liệu chính xác từ AI + rules giúp chọn module phù hợp, giảm tỷ lệ drop-off.
- **Hoạt động 24/7**: Workflow chạy tự động khi có creator mới signup, không phụ thuộc vào giờ làm việc.
- **Dữ liệu toàn diện**: Lấy thông tin từ **200+ insights** của influencers.club (demographics, analytics, social graph) và phân tích bằng GPT-4.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản HubSpot**:
   - **HubSpot Developer API Key** (để trigger mới contact được tạo).
   - **HubSpot App Token** (để update record sau khi enrich).
2. **API Key influencers.club**:
   - [Đăng ký API Key miễn phí](https://influencers.club/developers) (cần email và tên công ty).
3. **OpenAI API Key**:
   - [Mã API GPT-4](https://platform.openai.com/account/api-keys) (chọn model `gpt-4o-mini` để tiết kiệm chi phí).
4. **N8n Self-hosted** (không dùng phiên bản cloud):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
5. **Dữ liệu mẫu (optional)**:
   - Email của creator để test workflow (ví dụ: `creator@example.com`).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1: Import từ file JSON**
  1. Tải workflow từ [n8n.io/workflows/13302](https://n8n.io/workflows/13302) (chọn **Export JSON**).
  2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
  3. Chọn **Create new workflow** và nhấn **Import**.

- **Cách 2: Copy/Paste JSON**
  1. Mở n8n Editor → **Create new workflow**.
  2. Nhấn **Import** → Chọn **Paste JSON** và dán toàn bộ mã JSON từ [n8n.io/workflows/13302](https://n8n.io/workflows/13302).
  3. Nhấn **Import**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **12 node** với logic phức tạp. Dưới đây là hướng dẫn **cấu hình chi tiết** cho từng node quan trọng:

#### **🔹 Node 1: HubSpot Trigger1 (hubspotTrigger)**
- **Mục đích**: Nhận signal khi có creator mới signup trên HubSpot.
- **Cấu hình**:
  - **Credentials**: Chọn `hubspotDeveloperApi` (đã cấu hình trước).
  - **Operation**: Chọn `contact.created`.
  - **Filter**: Thêm điều kiện để chỉ lấy contact mới (ví dụ: `properties.createdAt > now-1d`).
  - **Output**: Node này sẽ trả về `contactId` và `email` của creator mới.

#### **🔹 Node 2: Get Contact by ID (hubspot)**
- **Mục đích**: Lấy chi tiết contact từ HubSpot (bao gồm email).
- **Cấu hình**:
  - **Credentials**: Chọn `hubspotAppToken`.
  - **Operation**: Chọn `get`.
  - **Parameters**:
    - `id`: Điền `${$node["HubSpot Trigger1"].json["contactId"]}` (dynamic reference).
    - `properties`: Chọn `email` (để enrich sau).

#### **🔹 Node 3: Extract Email (set)**
- **Mục đích**: Trích xuất email từ contact để gửi đến influencers.club API.
- **Cấu hình**:
  - **Expression**: Điền `${$node["Get Contact by ID"].json["properties"]["email"]}`.

#### **🔹 Node 4: Enrich by Email (httpRequest)**
- **Mục đích**: Gọi API influencers.club để enrich dữ liệu creator từ email.
- **Cấu hình**:
  - **Credentials**: Chọn `httpHeaderAuth` (đã cấu hình API Key influencers.club).
  - **Method**: `POST`.
  - **URL**: `https://api.influencers.club/public/v1/creators/enrich/email/`.
  - **Headers**:
    - `Authorization`: `Bearer YOUR_API_KEY` (thay bằng API Key của bạn).
    - `Content-Type`: `application/json`.
  - **Body**:
    ```json
    {
      "email": "{{$node["Extract Email"].json["email"]}}"
    }
    ```
  - **Error Handling**:
    - Nếu API trả về lỗi (status code != 200), node **Stop and Error** sẽ kích hoạt (node 11).

#### **🔹 Node 5: AI Niche Analyzer (chainLlm)**
- **Mục đích**: Sử dụng GPT-4 phân tích niche chính của creator.
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: `gpt-4o-mini` (đã cấu hình trước).
  - **Prompt Template** (cần chỉnh sửa):
    ```plaintext
    Analyze the following creator data and determine their primary niche.
    Data: {{$node["Enrich by Email"].json["data"]}}
    Return structured JSON with:
    {
      "primary_niche": "string",
      "secondary_niches": ["string", "string"],
      "recommended_modules": ["onboarding_step1", "onboarding_step2"]
    }
    ```
  - **Output Parser**: Chọn `Structured Output Parser` (node 12) để đảm bảo dữ liệu trả về đúng format JSON.

#### **🔹 Node 6: Tier Classifier (code)**
- **Mục đích**: Phân loại creator theo tier (Nano, Micro, Macro) dựa trên follower count.
- **Cấu hình**:
  - **Code JavaScript**:
    ```javascript
    const followerCount = {{$node["Enrich by Email"].json["data"]["follower_count"]}};
    let tier;

    if (followerCount < 10000) {
      tier = "nano";
    } else if (followerCount < 100000) {
      tier = "micro";
    } else {
      tier = "macro";
    }

    return {
      tier: tier,
      follower_count: followerCount
    };
    ```
  - **Output**: Node này sẽ trả về `tier` và `follower_count`.

#### **🔹 Node 7: Merge AI + Rules (merge)**
- **Mục đích**: Gộp kết quả từ AI (niche) và rules (tier) thành một dataset duy nhất.
- **Cấu hình**:
  - **Merge Strategy**: Chọn `All properties`.
  - **Input**: Kết nối với node `AI Niche Analyzer` và `Tier Classifier`.

#### **🔹 Node 8: Aggregate Final Data (aggregate)**
- **Mục đích**: Tạo một dataset cuối cùng để update vào HubSpot.
- **Cấu hình**:
  - **Aggregate Strategy**: Chọn `All properties`.
  - **Output**: Dữ liệu sẵn sàng để update vào contact HubSpot.

#### **🔹 Node 9: Update CRM Record (hubspot)**
- **Mục đích**: Cập nhật contact trên HubSpot với dữ liệu enrich.
- **Cấu hình**:
  - **Credentials**: Chọn `hubspotAppToken`.
  - **Operation**: Chọn `update`.
  - **Parameters**:
    - `id`: `${$node["HubSpot Trigger1"].json["contactId"]}`.
    - **Properties để update** (ví dụ):
      ```json
      {
        "primary_niche": "{{$node["Merge AI + Rules"].json["primary_niche"]}}",
        "tier": "{{$node["Merge AI + Rules"].json["tier"]}}",
        "follower_count": "{{$node["Merge AI + Rules"].json["follower_count"]}}",
        "platform_links": "{{$node["Enrich by Email"].json["data"]["platform_links"]}}",
        "onboarding_modules": "{{$node["Merge AI + Rules"].json["recommended_modules"]}}"
      }
      ```

#### **🔹 Node 10: Stop and Error (stopAndError)**
- **Mục đích**: Dừng workflow nếu có lỗi (ví dụ: API influencers.club trả về lỗi).
- **Cấu hình**:
  - **Error Condition**: Kiểm tra `statusCode` từ node `Enrich by Email` (node 4).
  - Nếu `statusCode` != 200, workflow sẽ dừng và gửi thông báo lỗi.

#### **🔹 Node 11: Structured Output Parser (outputParserStructured)**
- **Mục đích**: Đảm bảo output từ GPT-4 đúng format JSON.
- **Cấu hình**:
  - **Schema**:
    ```json
    {
      "primary_niche": "string",
      "secondary_niches": ["string"],
      "recommended_modules": ["string"]
    }
    ```

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và nhập email mẫu (ví dụ: `test@example.com`).
   - Kiểm tra kết quả ở node `Update CRM Record` (node 9) để đảm bảo dữ liệu update vào HubSpot chính xác.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi có creator mới signup.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**CÁC Ý TƯỞNG MỞ RỘNG**]
1. **Gửi thông báo cá nhân hóa đến creator**:
   - Sử dụng node **Slack/Email** để gửi message cá nhân hóa dựa trên `primary_niche` và `tier`.
   - Ví dụ: Nếu creator là **Micro Influencer** trong niche **Fitness**, gửi link module onboarding phù hợp.

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử enrich và update contact.

3. **Báo cáo định kỳ**:
   - Sử dụng node **HubSpot Analytics** hoặc **Google Data Studio** để tạo báo cáo về:
     - Số creator được enrich mỗi tháng.
     - Phân bố theo tier/niche.
     - Tỷ lệ activation theo module onboarding.

4. **Kết hợp với CRM khác**:
   - Thay thế node `HubSpot Trigger1` bằng **Zapier** hoặc **Make (Integromat)** để trigger từ CRM khác (Salesforce, Pipedrive...).

5. **Optimize chi phí OpenAI**:
   - Thay `gpt-4o-mini` bằng `gpt-3.5-turbo` (rẻ hơn) nếu không cần độ chính xác cao.
   - Cắt giảm prompt để giảm token usage.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng team marketing** khỏi công việc thủ công phức tạp, đồng thời **tăng tỷ lệ activation** nhờ cá nhân hóa trải nghiệm onboarding. Với **AI GPT-4 + dữ liệu influencer.club**, các sếp có thể:
✅ **Enrich dữ liệu creator** từ email trong giây lát.
✅ **Phân loại chính xác** theo tier và niche.
✅ **Cá nhân hóa onboarding** để tăng engagement.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hành động ngay**:
1. [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) để self-host n8n.
2. [Đăng ký API influencers.club](https://influencers.club/developers) và OpenAI.
3. Import workflow và **bật chạy** để tự động hóa quy trình!

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp lỗi API, kiểm tra **credentials** và **rate limit** của influencers.club.
- Đối với creator có email không tồn tại trong database, node `Enrich by Email` sẽ trả về `null` và workflow sẽ dừng (do node `Stop and Error`). Có thể thêm logic fallback bằng node **If** để xử lý trường hợp này.