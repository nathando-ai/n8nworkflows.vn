---
title: "🚀 Tự Động Hóa Meta Ads Webhook: Nhận Dữ Liệu Quảng Cáo, Ghi Log Google Sheets & Cảnh Báo Slack (100% Không Code)"
description: "Workflow này tự động nhận và xử lý tất cả webhook từ Meta Ads Account, ghi chi tiết vào Google Sheets và gửi báo cáo tổng hợp hàng ngày qua Slack. Giúp các sếp marketing tiết kiệm 10+ giờ/tháng và tránh mất mát dữ liệu do quảng cáo bị treo."
slug: "tieu-dong-hoa-meta-ads-webhook-ghi-log-google-sheets-canh-bao-slack"
tags: [n8n, automation, meta-ads, google-sheets, slack, marketing-automation, webhook]
keywords: [n8n workflow meta ads, tự động hóa quảng cáo facebook, ghi log webhook google sheets, cảnh báo slack từ meta ads, tự động hóa marketing không code]
---

# 🚀 **Tự Động Hóa Meta Ads Webhook: Nhận Dữ Liệu Quảng Cáo, Ghi Log Google Sheets & Cảnh Báo Slack**

### **🔥 Nỗi Đau Của Các Sếp Marketing Hiện Nay**
Hàng ngày, các sếp marketing phải:
- **Theo dõi thủ công** tất cả các sự kiện từ Meta Ads (Creative Fatigue, Ad Recommendations, Product Set Issues...) trên bảng điều khiển Meta Business Suite.
- **Ghi chép vào Excel/Google Sheets** để phân tích sau, dẫn đến **sai sót, mất thời gian và khó theo dõi lịch sử**.
- **Không biết kịp thời** khi quảng cáo bị treo hoặc gặp vấn đề (ví dụ: Creative Fatigue) vì không có cảnh báo tự động.
- **Phải liên hệ Meta Support** để khắc phục vấn đề, mất thêm thời gian và chi phí.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Nhận tự động** tất cả webhook từ Meta Ads Account (100% không cần code).
✅ **Ghi log chi tiết** vào Google Sheets (mỗi loại sự kiện vào tab riêng).
✅ **Cảnh báo Slack** khi có sự kiện mới (tổng hợp số lượng, loại sự kiện).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/tháng** không phải theo dõi thủ công Meta Ads.
- **Tránh mất mát quảng cáo** do Creative Fatigue hoặc Product Set Issues không được xử lý kịp thời.
- **Dữ liệu hoàn toàn chính xác** (không sai sót như ghi chép tay).
- **Báo cáo tự động** qua Slack, giúp team marketing phản ứng nhanh chóng.
- **Lưu trữ lịch sử** trên Google Sheets để phân tích dài hạn.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Meta Business Suite** (đã cấu hình Webhook cho Ad Account).
2. **Google Sheets** với **6 tab riêng** (tên tab phải chính xác):
   - `creative_fatigue`
   - `ad_recommendations`
   - `ads_async_creation_request`
   - `in_process_ad_objects`
   - `product_set_issue`
   - `with_issues_ad_objects`
3. **Tài khoản Slack** (để nhận báo cáo tổng hợp).
4. **API Key & Credentials**:
   - **Google Sheets OAuth 2.0** (để ghi log).
   - **Slack Token** (để gửi thông báo).
5. **VPS Self-hosted n8n** (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12223](https://n8n.io/workflows/12223) hoặc copy toàn bộ JSON từ link trên.
- **Mở n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

:::note[**Lưu ý quan trọng**]
- **Không thay đổi cấu trúc** của workflow (sắp xếp node, tên node).
- **Không xóa node** nào, chỉ cần cấu hình lại tham số.
:::

---

### **2. Các Bước Cấu Hình BẮT BUỘC**
#### **🔹 Bước 1: Cấu Hình Webhook Meta Ads**
- **Node: `Webhook: Meta (ad_account)`**
  - Thiết lập **path** = `meta-ads-ad-account-webhook` (không đổi).
  - Chọn **Method** = `POST`.
  - **Enable Webhook** để Meta Ads có thể gửi dữ liệu.

#### **🔹 Bước 2: Cấu Hình Verify Token (Trang Web Meta)**
- **Tại Meta Business Suite**:
  1. Đi đến **Settings** → **Webhooks**.
  2. Thêm **Verify Token** (phải trùng với giá trị trong node `Verify: token` của workflow).
     - **Verify Token** trong workflow mặc định là `$meta_webhook_verify_token` (sẽ được cấu hình sau).
  3. **Callback URL** = `https://[your-n8n-domain]/meta-ads-ad-account-webhook` (địa chỉ VPS của bạn).

#### **🔹 Bước 3: Cấu Hình Credentials Google Sheets**
- **Node: `Log Creative Fatigue`, `Log Ad Recommendations`, ... (tất cả node Google Sheets)**
  - Chọn **Credentials** = `googleSheetsOAuth2Api`.
  - **Sheet Name** = Tên tab tương ứng (ví dụ: `creative_fatigue`).
  - **Operation** = `append` (thêm dữ liệu mới vào cuối bảng).

#### **🔹 Bước 4: Cấu Hình Slack Notification**
- **Node: `Slack: send summary`**
  - Chọn **Credentials** = `slack`.
  - **Channel ID** = ID của channel Slack muốn nhận báo cáo (lấy từ `https://slack.com/apps/A0F7XCTLQ/token`).
  - **Message Format**:
    ```json
    {
      "text": "🚨 Meta Ads Webhook Alert: {{ $json.count }} events received today",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Tổng số sự kiện:* {{ $json.count }}\n*Loại sự kiện:* {{ $json.event_type }}"
          }
        }
      ]
    }
    ```

#### **🔹 Bước 5: Cấu Hình `Set: event field`**
- **Node này** sẽ tổng hợp tất cả sự kiện trước khi gửi báo cáo Slack.
- **Không cần thay đổi** (n8n tự động xử lý).

#### **🔹 Bước 6: Test Workflow**
1. **Nhấn `Execute`** trên node `Webhook: Meta (ad_account)`.
2. **Sử dụng tool test Meta Ads Webhook**:
   👉 [meta-ads-webhook-tester](https://github.com/KhatkevichKirill/meta-ads-webhook-tester) (để gửi dữ liệu mẫu).
3. **Kiểm tra**:
   - Dữ liệu có ghi vào Google Sheets không?
   - Slack có nhận được báo cáo không?

---

### **3. Kích Hoạt Workflow ⚡️**
- **Bật `Active`** trên workflow.
- **Kiểm tra log** để đảm bảo không có lỗi.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CẬP NHẬT & TỰ ĐỘNG HÓA NÊN HIỂU**]
1. **Lưu log chi tiết hơn**:
   - Thêm cột `timestamp` vào Google Sheets để theo dõi thời gian sự kiện xảy ra.
   - Sử dụng **n8n-node-dateTime** để thêm thời gian hiện tại vào dữ liệu.

2. **Cảnh báo cấp độ**:
   - Tạo **các channel Slack khác** cho các loại sự kiện nghiêm trọng (ví dụ: `product_set_issue` → Channel `#urgent-ads`).
   - Sử dụng **n8n-node-switch** để phân loại sự kiện.

3. **Báo cáo định kỳ**:
   - Sử dụng **n8n-node-cron** để gửi báo cáo hàng tuần/tháng qua Email (nếu cần).

4. **Kết hợp với Meta Ads API**:
   - Tự động **tắt quảng cáo bị Creative Fatigue** bằng cách gọi API Meta Ads từ n8n.

5. **Backup dữ liệu**:
   - Sử dụng **n8n-node-googleDrive** để sao lưu dữ liệu Google Sheets hàng ngày.
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing khỏi việc theo dõi thủ công Meta Ads, đồng thời **giảm thiểu rủi ro** khi quảng cáo bị treo do không xử lý kịp thời. **Chỉ cần 30 phút cấu hình**, bạn đã có một hệ thống tự động hóa hoàn chỉnh!

**🚀 Hãy áp dụng ngay và tiết kiệm 10+ giờ/tháng!**
- **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
- **Test với dữ liệu mẫu** trước khi chuyển sang live.
- **Tối ưu hóa Slack Channel** để nhận báo cáo hiệu quả.

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/12223) | 📌 [Cấu hình Google Sheets](https://docs.google.com/spreadsheets/create) | 🚀 [Đăng ký VPS n8n](https://tino.vn/vps-n8n?affid=388)**