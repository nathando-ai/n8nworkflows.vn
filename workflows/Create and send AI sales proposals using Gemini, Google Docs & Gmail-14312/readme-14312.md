---
title: "🚀 Tự Động Hóa Tạo & Gửi Proposal Bán Hàng AI Chuyên Nghiệp Với Gemini, Google Docs & Gmail"
description: "Workflow tự động hóa hoàn toàn từ việc thu thập lead đến gửi proposal bán hàng cá nhân hóa bằng AI, tiết kiệm 80% thời gian so với thủ công. Áp dụng ngay cho doanh nghiệp B2B, startup hoặc team sales!"
slug: "tieu-dong-hoa-tao-gui-proposal-ai-google-gemini"
tags: [n8n, automation, ai-gemini, google-docs, gmail, sales-automation, no-code]
keywords: [tự động hóa proposal bán hàng, gemini ai n8n, google docs tự động, gửi proposal email tự động, workflow n8n bán hàng]
---

# 🚀 **Tự Động Hóa Tạo & Gửi Proposal Bán Hàng AI Chuyên Nghiệp Với Gemini, Google Docs & Gmail**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp Sales**
Hàng ngày, các sếp phải:
- **Lặp đi lặp lại** việc tạo proposal từ mẫu, thay đổi nội dung cho từng khách hàng.
- **Tốn thời gian** tìm kiếm thông tin khách hàng, tổng hợp yêu cầu, và viết lại từ đầu.
- **Mất kiểm soát** khi phải theo dõi nhiều lead cùng lúc, dễ quên gửi proposal kịp thời.
- **Không cá nhân hóa** đủ để tăng tỷ lệ chuyển đổi (conversion rate).

**Workflow này giải quyết tất cả!** Sử dụng **AI Gemini** để tự động tạo nội dung proposal chuyên nghiệp, **Google Docs** để thiết kế mẫu đẹp mắt, và **Gmail** để gửi tự động—**không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** so với viết proposal thủ công.
✅ **Proposal cá nhân hóa 100%** dựa trên dữ liệu khách hàng từ Google Sheets.
✅ **Tự động cập nhật CRM HubSpot** khi có lead mới.
✅ **Gửi email tự động** với file PDF đính kèm, không quên gửi.
✅ **Dễ dàng mở rộng** cho nhiều khách hàng cùng lúc (batch processing).
✅ **Chất lượng cao** nhờ AI Gemini phân tích yêu cầu và đề xuất giải pháp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (Google Sheets, Google Drive, Google Docs, Gmail) với quyền **quản trị viên**.
2. **Tài khoản HubSpot** (để cập nhật contact và deal).
3. **API Key Gemini** (từ [Google AI Studio](https://aistudio.google/)).
4. **File mẫu proposal** trên Google Docs (có **placeholder** như `{{AI_Summary}}`, `{{AI_Solution}}`, `{{Client_Name}}`).
5. **Bảng Google Sheets** với cột bắt buộc:
   - **Client Name** (Tên khách hàng)
   - **Email** (Email liên hệ)
   - **Goals** (Yêu cầu của khách hàng)
   - **Budget** (Ngân sách, nếu có)
   *(Cách cấu trúc chi tiết ở phần **Cấu Hình Workflow**)*

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/14312) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Workflow Name** (ví dụ: **"AI Proposal Generator"**).
4. Nhấn **Import** → Workflow sẽ xuất hiện trên dashboard.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Create Workflow**.
2. Chọn **Import** → **Paste JSON** → Dán toàn bộ mã JSON từ [đây](https://n8n.io/workflows/14312).
3. Nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **9 node** quan trọng, các sếp phải cấu hình kỹ lưỡng:

#### **🔹 Node 1: Google Sheets Trigger (Khởi động workflow)**
- **Cấu hình:**
  - Chọn **Google Sheets** → **New Row** (để workflow chạy khi có dòng mới trong sheet).
  - **Sheet Name:** Tên bảng chứa lead (ví dụ: **"Leads"**).
  - **Trigger Column:** Cột bắt buộc (ví dụ: **"Status"** → giá trị mới là **"New Lead"**).
  - **Credentials:** Chọn tài khoản Google đã kết nối.

#### **🔹 Node 2: Loop Over Items (Xử lý batch)**
- **Cấu hình:**
  - **Batch Size:** 1 (hoặc số lượng lead muốn xử lý cùng lúc).
  - **Item:** Chọn `$node["Google Sheets Trigger"].json` (dữ liệu từ sheet).

#### **🔹 Node 3: Message a Model (Gemini AI Tạo Nội Dung)**
- **Cấu hình:**
  - **Model:** Chọn **Gemini Pro** (hoặc **Gemini Flash** nếu muốn tiết kiệm chi phí).
  - **Prompt Template:**
    ```plaintext
    Tôi là một chuyên gia bán hàng AI. Dựa trên thông tin sau, hãy tạo một proposal bán hàng chuyên nghiệp cho khách hàng {Client_Name} với yêu cầu: {Goals}. Proposal phải bao gồm:
    1. Tóm tắt vấn đề của khách hàng (1 đoạn ngắn).
    2. Giải pháp cụ thể của công ty tôi (sử dụng từ khóa: {Industry}).
    3. 3 lợi ích chính của giải pháp này.
    4. Gợi ý thời gian triển khai và ngân sách (nếu có).
    Đảm bảo nội dung chuyên nghiệp, ngắn gọn và có placeholder để thay thế sau: {{AI_Summary}}, {{AI_Solution}}.
    ```
  - **Input Data:** Chọn `$node["Loop Over Items"].json` (dữ liệu từ sheet).
  - **Credentials:** Điền **API Key Gemini** (từ [Google AI Studio](https://aistudio.google/)).

#### **🔹 Node 4: Code (JavaScript2) - Sắp Xếp Dữ liệu**
- **Cấu hình:**
  - **Code:**
    ```javascript
    // Lấy dữ liệu từ AI và sheet
    const aiResponse = $input.all();
    const clientData = aiResponse[0].json;

    // Thay thế placeholder trong nội dung AI
    const summary = clientData.AI_Summary.replace(/{{AI_Summary}}/g, clientData.AI_Summary);
    const solution = clientData.AI_Solution.replace(/{{AI_Solution}}/g, clientData.AI_Solution);

    // Trả về dữ liệu đã xử lý
    return {
      json: {
        ...clientData,
        AI_Proposal: `${summary}\n\n${solution}`,
        Client_Name: clientData.Client_Name,
        Email: clientData.Email,
        Goals: clientData.Goals
      }
    };
    ```
  - **Output:** Chọn **JSON** → **json**.

#### **🔹 Node 5: Create or Update a Contact (HubSpot)**
- **Cấu hình:**
  - **Operation:** Chọn **Create or Update**.
  - **Properties:**
    - **email:** `$node["Code"].json.Email`
    - **firstname:** `$node["Code"].json.FirstName` (nếu có)
    - **lastname:** `$node["Code"].json.LastName` (nếu có)
    - **hs_object_association_object_id:** (nếu liên quan đến deal)
  - **Credentials:** Chọn **Private App Token** của HubSpot (tạo tại **Settings → Private Apps**).

#### **🔹 Node 6: Update a Document (Google Docs)**
- **Cấu hình:**
  - **File ID:** ID của file mẫu proposal (lấy từ liên kết Google Docs: `https://docs.google.com/document/d/[FILE_ID]/edit`).
  - **Operation:** Chọn **Update**.
  - **Content:** Chọn `$node["Code"].json.AI_Proposal` (nội dung từ AI).
  - **Credentials:** Tài khoản Google đã kết nối.

#### **🔹 Node 7: Copy File (Google Drive) → Tạo File PDF**
- **Cấu hình:**
  - **Source File ID:** ID của file Google Docs vừa cập nhật.
  - **Destination File Name:** `Proposal_${$node["Code"].json.Client_Name}.pdf`
  - **Mime Type:** `application/pdf`
  - **Credentials:** Tài khoản Google.

#### **🔹 Node 8: Send a Message (Gmail)**
- **Cấu hình:**
  - **To:** `$node["Code"].json.Email` (email khách hàng).
  - **Subject:** `Proposal cho ${$node["Code"].json.Client_Name}`
  - **Body:**
    ```plaintext
    Chào {Client_Name},

    Tôi rất vui khi gửi proposal cho bạn! Dưới đây là giải pháp chi tiết phù hợp với yêu cầu của {Goals}:

    {AI_Proposal}

    File PDF đính kèm để tham khảo. Hãy liên hệ với tôi nếu có bất kỳ câu hỏi nào!

    Trân trọng,
    [Tên của bạn]
    [Chức vụ]
    [Số điện thoại]
    ```
  - **Attachments:** Chọn file PDF từ **Node 7**.
  - **Credentials:** Tài khoản Gmail đã kết nối.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Thêm một dòng mới vào **Google Sheets** với cột bắt buộc (Client Name, Email, Goals).
   - Chạy **Test Execution** trên node **Google Sheets Trigger**.
   - Kiểm tra:
     - AI có tạo nội dung không?
     - HubSpot có cập nhật contact không?
     - Email có gửi thành công không?
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa AI Prompt**
- **Thay đổi tone** cho phù hợp với ngành nghề:
  - **Ngành SaaS:** "Tạo proposal với tone chuyên nghiệp, nhấn mạnh ROI và tính dễ sử dụng."
  - **Ngành Marketing:** "Sử dụng từ ngữ hấp dẫn, ví dụ về thành công của khách hàng khác."
- **Thêm placeholder** cho giá trị cụ thể:
  ```plaintext
  {{Pricing_Plan}}: Gói {Plan_Name} với giá {Price}/tháng.
  ```

### **2. Kết Nối Với Slack/Telegram**
- Thêm **node Slack** hoặc **Telegram Bot** sau **Node 8** để thông báo khi proposal được gửi thành công:
  ```plaintext
  Proposal đã được gửi cho {Client_Name} tại {Email}!
  ```

### **3. Lưu Log & Báo Cáo**
- Sử dụng **node StickyNote** (hoặc **Google Sheets**) để ghi lại lịch sử:
  - Ngày gửi, tên khách hàng, trạng thái (Gửi thành công/Thất bại).
- **Tự động gửi báo cáo hàng tuần** bằng **node Gmail** hoặc **Slack**.

### **4. Mở Rộng Cho Nhiều Khách Hàng**
- **Batch Processing:** Đặt **Batch Size = 5** trong **Loop Over Items** để xử lý 5 lead cùng lúc.
- **Lọc lead** trong Google Sheets:
  - Chỉ chạy workflow khi cột **"Status"** = **"New Lead"**.

### **5. Tự Động Cập Nhật Mẫu Proposal**
- Sử dụng **node Google Drive Watch** để theo dõi thay đổi trong file mẫu và tự động cập nhật.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp sales để tập trung vào **quan hệ khách hàng** và **đàm phán**, thay vì mất thời gian viết proposal. Với **AI Gemini**, nội dung luôn **chuyên nghiệp và cá nhân hóa**, trong khi **Google Docs & Gmail** đảm bảo **tự động hóa hoàn toàn** từ thu thập lead đến gửi proposal.

**🚀 Hành động ngay:**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình tài khoản** (Google, HubSpot, Gemini).
3. **Thêm lead đầu tiên** vào Google Sheets và **chạy thử!**

**Nếu gặp vấn đề**, các sếp có thể:
- **Comment** bên dưới để được hỗ trợ.
- **Xem video hướng dẫn** từ [iTechNotion](https://itechnotion.com/).
- **Tư vấn 1:1** với đội ngũ chuyên gia tại [n8n Community](https://community.n8n.io/).

**Chúc các sếp thành công với việc tự động hóa proposal bán hàng!** 💼✨