---
title: "🍕 Tự Động Hóa Quá Trình Đặt Món Pizza với Chatbot AI GPT-3.5 - Theo Dõi Menu, Đơn Hàng & Trạng Thái"
description: "Giải pháp tự động hóa hoàn toàn không code để tạo chatbot đặt món pizza thông minh, tích hợp GPT-3.5, theo dõi đơn hàng và cập nhật trạng thái thực thời. Giúp các sếp tiết kiệm 100% thời gian quản lý đơn hàng và cải thiện trải nghiệm khách hàng."
slug: "tự-dộng-hoa-chatbot-dat-mon-pizza-gpt-3-5"
tags: [n8n, automation, ai, chatbot, no-code, langchain, openai]
keywords: [n8n workflow chatbot, tự động hóa đặt món pizza, GPT-3.5 n8n, theo dõi đơn hàng tự động, chatbot AI không code]
---

# 🚀 **Chatbot Đặt Món Pizza AI: Từ Menu Đến Theo Dõi Đơn Hàng - Không Cần Code!**

### **Nỗi Đau Của Các Sếp: Quản Lý Đơn Hàng Pizza Cố Gắng Và Mất Thời Gian**
Hàng ngày, các quán pizza phải đối mặt với:
- **Sự chậm trễ** khi khách hàng phải gọi điện hoặc chat để đặt món, tra cứu trạng thái đơn hàng.
- **Lỗi nhân sự** khi nhân viên phải nhắc nhở khách hàng về trạng thái đơn hàng, dẫn đến mất thời gian và trải nghiệm khách hàng kém.
- **Không theo dõi được** đơn hàng một cách tự động, khiến việc cập nhật trạng thái trở nên phức tạp.

**Giải pháp?** Một **chatbot AI thông minh** tích hợp với GPT-3.5, tự động xử lý đặt món, theo dõi trạng thái và cập nhật thông tin cho khách hàng **24/7** – **không cần code!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian** của nhân viên: Chatbot tự động xử lý đặt món, tra cứu đơn hàng và cập nhật trạng thái.
- **Trải nghiệm khách hàng nâng cao**: Khách hàng có thể đặt món, tra cứu đơn hàng và nhận thông báo trạng thái **tự động** qua chatbot.
- **Tối ưu hóa quản lý đơn hàng**: Theo dõi trạng thái đơn hàng từ đặt món đến giao hàng một cách **liên tục và chính xác**.
- **Cải thiện doanh thu**: Khách hàng có thể đặt món bất kỳ lúc nào, không phụ thuộc vào giờ mở cửa của quán.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** với API Key (để sử dụng GPT-3.5).
2. **API Key của OpenAI** (để kết nối với node `Chat OpenAI`).
3. **Dữ liệu sản phẩm pizza** (danh sách món ăn, giá, mô tả) để chatbot trích xuất khi khách hàng đặt món.
4. **Dịch vụ lưu trữ đơn hàng** (ví dụ: Google Sheets, Firebase, hoặc cơ sở dữ liệu riêng) để chatbot theo dõi trạng thái đơn hàng.
5. **Ngôn ngữ lập trình cơ bản** (không cần code để cấu hình workflow, nhưng cần hiểu cơ bản về API và JSON).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/3049](https://n8n.io/workflows/3049) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng **8 node** chính, mỗi node đều cần cấu hình kỹ lưỡng:

##### **A. Cấu Hình Node `Chat OpenAI` (GPT-3.5)**
- **Credentials:** Chọn `openAiApi` (đã cấu hình trước khi import).
- **Model:** Chọn `gpt-3.5-turbo` (hoặc phiên bản mới nhất).
- **Prompt:** Cần **tùy chỉnh** để chatbot hiểu rõ yêu cầu đặt món, tra cứu đơn hàng và cập nhật trạng thái.
  ```json
  "prompt": "Bạn là một chatbot quản lý đơn hàng pizza. Hãy xử lý các yêu cầu sau:
  1. Hiển thị menu pizza với danh sách món ăn, giá và mô tả.
  2. Xác nhận đơn hàng khi khách đặt món.
  3. Theo dõi trạng thái đơn hàng (chờ chuẩn bị, đang nấu, sẵn sàng giao, đã giao).
  4. Cập nhật trạng thái đơn hàng tự động khi có thay đổi."
  ```

##### **B. Cấu Hình Node `Get Products` (Lấy Danh Sách Món)**
- **Method:** `GET` hoặc `POST` (tùy thuộc vào API của bạn).
- **URL:** Địa chỉ API trả về danh sách món pizza (ví dụ: `https://api-quanpizza.com/products`).
- **Headers:** Thêm `Authorization` nếu cần (nếu API yêu cầu API Key).
- **Response Format:** Chọn `JSON` và **mapping** dữ liệu sao cho chatbot hiểu được tên món, giá và mô tả.

##### **C. Cấu Hình Node `Order Product` (Xử Lý Đơn Hàng)**
- **Method:** `POST` (để gửi đơn hàng lên API).
- **URL:** Địa chỉ API xử lý đơn hàng (ví dụ: `https://api-quanpizza.com/orders`).
- **Body:** Điền thông tin đơn hàng từ chatbot (khách hàng, món ăn, số lượng, địa chỉ giao hàng).
  ```json
  {
    "customer": "$$.json.customer",
    "items": "$$.json.items",
    "address": "$$.json.address",
    "status": "chờ chuẩn bị"
  }
  ```

##### **D. Cấu Hình Node `Get Order` (Tra Cứu Trạng Thái Đơn Hàng)**
- **Method:** `GET` với tham số `orderId` (để lấy trạng thái đơn hàng).
- **URL:** `https://api-quanpizza.com/orders/{orderId}`.
- **Response Format:** Chọn `JSON` và **mapping** để chatbot hiểu trạng thái đơn hàng.

##### **E. Cấu Hình Node `Window Buffer Memory` (Giữ Lịch Sử Chat)**
- **Window Size:** Chọn `5` (lưu 5 lần tương tác gần nhất để chatbot nhớ trạng thái đơn hàng).
- **Key:** Đặt tên khóa lưu trữ (ví dụ: `order_history`).

##### **F. Cấu Hình Node `AI Agent` (Logic Xử Lý)**
- **Tool Usage:** Chọn tất cả các tool (`Calculator`, `Get Products`, `Order Product`, `Get Order`).
- **Prompt:** Tùy chỉnh để AI quyết định sử dụng tool nào khi khách hàng gửi tin nhắn.
  ```json
  "prompt": "Hãy xử lý yêu cầu của khách hàng bằng cách sử dụng các công cụ sau:
  - Nếu khách hỏi menu: sử dụng `Get Products`.
  - Nếu khách đặt món: sử dụng `Order Product`.
  - Nếu khách tra cứu đơn hàng: sử dụng `Get Order`.
  - Nếu cần tính toán giá: sử dụng `Calculator`."
  ```

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Gửi tin nhắn mẫu đến chatbot (ví dụ: *"Hãy cho tôi xem menu pizza"* hoặc *"Tôi muốn đặt 2 món Pepperoni và 1 món Margherita"*).
- **Bật Active:** Sau khi test thành công, bật workflow để hoạt động 24/7.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC TỐT NHẤT]
1. **Kết Nối Slack/Telegram:** Thêm node `Slack` hoặc `Telegram` để chatbot gửi thông báo trạng thái đơn hàng tự động.
   ```json
   {
     "node": "slack",
     "operation": "sendMessage",
     "text": "Đơn hàng #{{$node["Get Order"].json.id}} đã được giao!"
   }
   ```
2. **Lưu Log Đơn Hàng:** Sử dụng node `Google Sheets` hoặc `Airtable` để lưu lịch sử đơn hàng.
3. **Cập Nhật Menu Tự Động:** Nếu danh sách món thay đổi, sử dụng node `Set` để cập nhật API.
4. **Hỗ Trợ Nhiều Ngôn Ngữ:** Tùy chỉnh prompt để chatbot hiểu và trả lời bằng nhiều ngôn ngữ.
:::

---

### 📌 **Kết Luận**
Với **workflow này**, các sếp không chỉ tự động hóa quá trình đặt món pizza mà còn **tối ưu hóa quản lý đơn hàng** một cách hoàn toàn tự động. **Không cần code**, chỉ cần cấu hình và bật workflow là xong!

**Hành động ngay:**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7.
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Test và bật hoạt động** để chatbot bắt đầu làm việc!

👉 **Bắt đầu tự động hóa ngay hôm nay!** 🚀