---
title: "🚀 Bypass Cloudflare Turnstile Tự Động cho Web Scraping với 2Captcha - Giải Pháp Không Cần Code"
description: "Giải quyết vấn đề bị chặn bởi Cloudflare Turnstile khi scraping website, tự động hóa việc giải Captcha bằng 2Captcha và Puppeteer trong n8n. Tiết kiệm thời gian, tăng hiệu suất scraping 100% tự động."
slug: "bypass-cloudflare-turnstile-voi-2captcha"
tags: [n8n, automation, web-scraping, 2captcha, cloudflare-turnstile, no-code, puppeteer]
keywords: [bypass turnstile n8n, tự động hóa scraping website, giải captcha 2captcha, cloudflare turnstile bypass, n8n workflow scraping]
---

# 🚀 **Bypass Cloudflare Turnstile Tự Động cho Web Scraping với 2Captcha**

### **Nỗi Đau Của Các Sếp Khi Scraping Website**
Các sếp thường gặp phải tình trạng bị **Cloudflare Turnstile** chặn khi cố gắng scraping dữ liệu từ website. Hệ thống này yêu cầu giải Captcha trước khi cho phép truy cập, làm chậm quá trình và thậm chí khiến dự án bị treo. **Giải pháp thủ công** đòi hỏi phải giải Captcha một cách thủ công, mất thời gian và không hiệu quả.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động hóa giải Captcha** với 2Captcha (dịch vụ giải Captcha chuyên nghiệp).
✅ **Bypass Turnstile** một cách an toàn và hiệu quả với Puppeteer.
✅ **Chạy 24/7** trên VPS, không cần can thiệp thủ công.
✅ **Không cần viết code**, chỉ cần cấu hình trong n8n.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải giải Captcha thủ công, workflow tự động hóa toàn bộ quá trình.
- **Tăng hiệu suất scraping**: Scraping liên tục mà không bị chặn bởi Turnstile.
- **Độ chính xác cao**: Puppeteer và 2Captcha đảm bảo giải Captcha chính xác.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không cần can thiệp.
- **Giảm chi phí**: Tránh mất thời gian và công sức của nhân viên.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản 2Captcha** (đăng ký tại [2captcha.com](https://2captcha.com/)) và **API Key**.
2. **URL mục tiêu** (website cần scraping).
3. **VPS tự host n8n** (để workflow chạy liên tục).
4. **Puppeteer** (đã được cài sẵn trong n8n, không cần cài thêm).
5. **Thông tin API Key** của 2Captcha để tạo task Captcha.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [link gốc](https://n8n.io/workflows/7151) hoặc sử dụng file JSON đã cung cấp.
2. Mở **n8n Editor** và chọn **Import Workflow**.
3. Chọn file JSON hoặc dán JSON vào ô nhập liệu.

:::note[LƯU Ý]
Nếu import từ link, hãy **đăng nhập vào tài khoản n8n** trước để workflow được tải đầy đủ.
:::

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **13 node**, các sếp cần chú ý cấu hình các node quan trọng sau:

##### **A. Cấu Hình Node "Set destination_url value"**
- **Node loại**: `set`
- **Cần thiết**: Điền **URL website** cần scraping vào biến `destination_url`.

##### **B. Cấu Hình Node "Create Captcha Task"**
- **Node loại**: `httpRequest`
- **Cần thiết**:
  - **Method**: `POST`
  - **URL**: `https://2captcha.com/in.php?key=<API_KEY>&method=userrecaptcha&googlekey=<SITEKEY>&pageurl=<URL>`
    - Thay `<API_KEY>` bằng **API Key** của 2Captcha.
    - Thay `<SITEKEY>` bằng **Sitekey** được trích xuất từ website (node sau sẽ xử lý).
    - Thay `<URL>` bằng **URL website** cần scraping.
  - **Headers**:
    ```json
    {
      "Content-Type": "application/x-www-form-urlencoded"
    }
    ```

##### **C. Cấu Hình Node "Get Captcha Solution"**
- **Node loại**: `httpRequest`
- **Cần thiết**:
  - **Method**: `GET`
  - **URL**: `https://2captcha.com/res.php?key=<API_KEY>&action=get&id=<CAPTCHA_ID>`
    - Thay `<API_KEY>` bằng **API Key** của 2Captcha.
    - Thay `<CAPTCHA_ID>` bằng **ID task** được trả về từ node "Create Captcha Task".
  - **Headers**:
    ```json
    {
      "Content-Type": "application/x-www-form-urlencoded"
    }
    ```

##### **D. Cấu Hình Node "Puppeteer"**
- **Node loại**: `n8n-nodes-puppeteer.puppeteer`
- **Cần thiết**:
  - **Action**: `Go to URL` (để truy cập website).
  - **URL**: `$node["Get destination web page"].json()["url"]` (trích xuất từ node trước).
  - **Cần thêm script JavaScript** để nhập **solution Captcha** vào form:
    ```javascript
    const solution = $node["Get Captcha Solution"].json()["solution"];
    await page.evaluate((solution) => {
      const input = document.querySelector('input[name="g-recaptcha-response"]');
      if (input) {
        input.value = solution;
      }
    }, solution);
    ```
  - **Chờ Turnstile hoàn tất** bằng cách thêm script:
    ```javascript
    await page.waitForFunction(() => {
      const turnstile = document.querySelector('div[class*="cf-turnstile"]');
      return !turnstile;
    });
    ```

##### **E. Cấu Hình Node "Pass CF Turnstile check using 2Captcha"**
- **Node loại**: `executeWorkflow`
- **Cần thiết**:
  - **Workflow**: Chọn workflow **Puppeteer** để thực hiện việc bypass Turnstile.
  - **Input**: Truyền **solution Captcha** từ node "Get Captcha Solution".

##### **F. Cấu Hình Node "Check Captcha Status"**
- **Node loại**: `switch`
- **Cần thiết**:
  - **Condition**: Kiểm tra trạng thái của task Captcha từ 2Captcha.
  - **Nếu trạng thái là "done"**: Tiếp tục quá trình scraping.
  - **Nếu trạng thái là "error"**: Dừng workflow và báo lỗi.

##### **G. Cấu Hình Node "Raise runIndex error"**
- **Node loại**: `stopAndError`
- **Cần thiết**:
  - **Sử dụng** khi task Captcha bị lỗi hoặc không hoàn tất trong thời gian quy định.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Test Workflow** và nhập **URL website** vào node "Set destination_url value".
   - Kiểm tra các node liên quan (Create Captcha Task, Get Captcha Solution, Puppeteer) để đảm bảo hoạt động đúng.
2. **Bật Active Workflow**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỜNG MỞ RỘNG]
1. **Lưu Log Scraping**:
   - Sử dụng node **Google Sheets** hoặc **Slack** để ghi lại kết quả scraping và trạng thái của task Captcha.
   - Ví dụ: Gửi thông báo Slack khi task Captcha hoàn tất thành công.

2. **Kết Hợp với Email Alert**:
   - Nếu workflow gặp lỗi, hãy cấu hình node **Email** để gửi báo cáo lỗi đến email của các sếp.

3. **Tối Ưu Hóa Thời Gian Chờ**:
   - Thay đổi thời gian chờ trong node **Wait 30 seconds** để phù hợp với tốc độ của website.

4. **Sử Dụng Proxy**:
   - Nếu website yêu cầu proxy, cấu hình **Puppeteer** để sử dụng proxy:
     ```javascript
     const puppeteer = require('puppeteer');
     const browser = await puppeteer.launch({
       args: ['--proxy-server=your_proxy_ip:port']
     });
     ```

5. **Bypass Multi-Turnstile**:
   - Nếu website có nhiều loại Turnstile, các sếp có thể mở rộng workflow bằng cách thêm các task Captcha khác (như **hCaptcha** hoặc **FunCaptcha**).
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình scraping website mà không bị chặn bởi Cloudflare Turnstile. Với **2Captcha** và **Puppeteer**, workflow hoạt động **100% tự động**, tiết kiệm thời gian và tăng hiệu suất.

**Hãy áp dụng ngay và bắt đầu scraping website một cách hiệu quả!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::