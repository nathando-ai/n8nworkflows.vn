---
title: "🎨 **Tự Động Hóa Sắp Xếp Icon UI Theo Tiêu Chuẩn Apple HIG + Gemini AI (Không Cần Code!)**"
description: "Workflow tự động phân loại và sắp xếp lại icon toolbar theo tiêu chuẩn thiết kế người dùng (Apple HIG) và nhận được đề xuất tối ưu từ Gemini AI. Giúp các sếp thiết kế UI tiết kiệm 80% thời gian so với làm thủ công."
slug: "tieu-chuan-apple-hig-gemini-ai-sap-xep-icon-ui"
tags: [n8n, automation, ai-summarization, ui-ux, apple-hig, gemini-ai, no-code]
keywords: [tự động hóa icon ui, gemini ai sắp xếp icon, tiêu chuẩn apple hig, thiết kế ui no-code, n8n workflow ui design]
---

# 🎨 **Tự Động Hóa Sắp Xếp Icon Toolbar Theo Tiêu Chuẩn Apple HIG + Gemini AI**

### **Nỗi Đau Của Các Sếp Thiết Kế UI**
Làm việc với các bộ icon toolbar trong ứng dụng, các sếp thường phải:
- **Phân loại icon thủ công** theo chức năng (đọc tài liệu Apple HIG mất hàng giờ).
- **Sắp xếp lại thứ tự** sao cho logic nhất, nhưng không biết có tối ưu không?
- **Lặp lại công việc** mỗi khi có thay đổi mới, dẫn đến hiệu suất thấp và dễ mắc lỗi.

**Workflow này giải quyết tất cả!** Nó tự động phân tích và sắp xếp lại icon theo tiêu chuẩn **Apple Human Interface Guidelines (HIG)**, đồng thời **tận dụng trí tuệ nhân tạo Gemini AI** để đề xuất bố cục tối ưu nhất.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** so với làm thủ công (không cần đọc tài liệu HIG chi tiết).
✅ **Sắp xếp icon theo logic Apple HIG** (mặc dù không phải là người thiết kế chuyên nghiệp).
✅ **Đề xuất bố cục tối ưu** từ Gemini AI, giúp UI trở nên thân thiện hơn.
✅ **Hoạt động liên tục** (không cần can thiệp thủ công).
✅ **Cập nhật tự động** khi có thay đổi mới trong danh sách icon.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
- **Tài khoản Google Cloud** (để sử dụng **Gemini API**).
- **API Key Google Palm API** (để kết nối với Gemini).
- **Danh sách icon** (có thể nhập qua form hoặc file JSON).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/8206](https://n8n.io/workflows/8206) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/8206](https://n8n.io/workflows/8206).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
3. Chọn **Create new workflow** và nhấn **Import**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **9 node** quan trọng, các sếp cần cấu hình như sau:

#### **🔹 Node "On form submission" (formTrigger)**
- **Mục đích**: Nhận đầu vào từ form (danh sách icon cần phân loại).
- **Cấu hình**:
  - Thêm **fields** cho form bao gồm:
    - `icons` (loại: **JSON** hoặc **Text**) → Nhập danh sách icon dưới dạng JSON (ví dụ: `[{"name": "Settings", "function": "account"}, {"name": "Search", "function": "find"}]`).
    - `screen` (loại: **Text**) → Mô tả ngắn về màn hình (nếu có).

#### **🔹 Node "Gemini" & "Gemini: Reordering" (lmChatGoogleGemini)**
- **Mục đích**: Gọi API Gemini để phân tích và sắp xếp lại icon.
- **Cấu hình**:
  - **Credentials**: Chọn `googlePalmApi` (đã cấu hình trước).
  - **Prompt**:
    - **Node "Gemini"**:
      ```plaintext
      Analyze the following UI icons based on Apple HIG standards. Return a structured JSON with:
      - Categories (e.g., "Account", "Navigation", "Settings")
      - Priority (1-5, where 1 is most important)
      - Example: [{"name": "Settings", "category": "Account", "priority": 3}]
      ```
    - **Node "Gemini: Reordering"**:
      ```plaintext
      Reorder the following icons based on Apple HIG best practices. Return a JSON array with the new order.
      Example: ["Search", "Settings", "Profile"]
      ```

#### **🔹 Node "Code: Clean Outcome" (code)**
- **Mục đích**: Lọc và định dạng kết quả từ Gemini thành dạng dễ sử dụng.
- **Cấu hình**:
  - Sử dụng **JavaScript** để xử lý JSON đầu ra:
    ```javascript
    return {
      json: JSON.parse(item.json.output).map(item => ({
        name: item.name,
        category: item.category || "Uncategorized",
        priority: item.priority || 5
      }))
    };
    ```

#### **🔹 Node "AI Agent: Icon Categorizer" (agent)**
- **Mục đích**: Tự động phân loại icon theo logic AI.
- **Cấu hình**:
  - **Prompt mặc định** đã được tối ưu, không cần chỉnh sửa (nếu muốn thay đổi, cập nhật trong **Settings** của node).

#### **🔹 Node "UI Guidance" & "Basic LLM Chain: Reordering" (chainLlm)**
- **Mục đích**: Đề xuất bố cục UI tối ưu từ Gemini.
- **Cấu hình**:
  - **Prompt**:
    ```plaintext
    Based on the following categorized icons, suggest an optimal toolbar layout for a macOS/iOS app.
    Return a JSON with:
    - "recommended_order": ["icon1", "icon2", ...]
    - "notes": "Explanation for the order"
    ```

#### **🔹 Node "Code: Clean Outcomes" (code)**
- **Mục đích**: Lọc kết quả cuối cùng từ LLM Chain.
- **Cấu hình**:
  - Sử dụng **JavaScript** để trích xuất dữ liệu cần thiết:
    ```javascript
    return {
      recommended_order: JSON.parse(item.json.output).recommended_order,
      notes: JSON.parse(item.json.output).notes
    };
    ```

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập danh sách icon vào form (ví dụ: `[{"name": "Search", "function": "find"}, {"name": "Settings", "function": "account"}]`).
   - Chạy workflow và kiểm tra kết quả phân loại/sắp xếp.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi có form submission.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** để nhận báo cáo kết quả tự động.
   - Ví dụ: Khi workflow hoàn thành, gửi tin nhắn như:
     ```plaintext
     🚀 **Kết quả sắp xếp icon UI:**
     - Thứ tự mới: Search → Settings → Profile
     - Ghi chú: "Sắp xếp theo thứ tự sử dụng phổ biến (Apple HIG)"
     ```

2. **Lưu Log Lịch Sử**:
   - Thêm node **Set** hoặc **Database** (n8n-nodes-base.database) để lưu lịch sử phân loại.
   - Giúp theo dõi thay đổi và so sánh giữa các phiên bản.

3. **Tích Hợp với Figma/Adobe XD**:
   - Sau khi sắp xếp xong, tự động gửi kết quả đến **Figma API** để cập nhật UI.
   - Sử dụng node **HTTP Request** với API Figma.

4. **Tối Ưu Prompt Gemini**:
   - Nếu muốn kết quả chính xác hơn, cập nhật prompt trong node **Gemini** theo mẫu:
     ```plaintext
     You are an expert in Apple HIG. Analyze the icons and return a JSON with:
     - "categories": { "Navigation": ["icon1", "icon2"], ... }
     - "priority": { "icon1": 1, "icon2": 2, ... }
     ```

---

## 📌 **Kết Luận**
Workflow này **giúp các sếp thiết kế UI tự động hóa 100% quá trình phân loại và sắp xếp icon**, dựa trên **tiêu chuẩn Apple HIG** và **trí tuệ nhân tạo Gemini AI**. Không cần viết một dòng code, chỉ cần nhập danh sách icon và workflow sẽ xử lý tất cả!

**Hành động ngay hôm nay**:
1. **Import workflow** vào n8n của mình.
2. **Nhập danh sách icon** và xem kết quả thần kỳ!
3. **Tích hợp với Slack/Figma** để tối ưu hóa workflow.

👉 **[Tải workflow ngay từ n8n.io](https://n8n.io/workflows/8206)** và bắt đầu tự động hóa UI của bạn! 🚀