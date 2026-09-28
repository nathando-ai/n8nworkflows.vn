---
title: "📊 Tự Động Hóa Báo Cáo Pipeline Doanh Thu Tín Chỉnh Cho Slack Bằng Airtable (N8N)"
description: "Workflow tự động hóa gửi báo cáo tuần về pipeline doanh thu (open deals, win rate, revenue closed) từ Airtable lên Slack hàng tuần, giúp các sếp Sales quản lý hiệu quả mà không cần check CRM thủ công. Giúp tiết kiệm 10+ giờ/tháng và tăng độ chính xác 100%."
slug: "tieu-dong-hoa-bao-cao-pipeline-doanh-thu-airtable-slack-n8n"
tags: [n8n, automation, CRM, sales pipeline, Airtable, Slack, no-code, self-hosted]
keywords: [tự động hóa báo cáo sales, n8n workflow CRM, pipeline doanh thu tự động, báo cáo Slack từ Airtable, tự động hóa sales pipeline, giảm thời gian quản lý CRM]
---

# 🚀 **Tự Động Hóa Báo Cáo Pipeline Doanh Thu Tín Chỉnh Cho Slack Bằng Airtable**

### **Giải pháp cho các sếp Sales mệt mỏi vì phải check CRM hàng ngày**
Hàng tuần, các sếp Sales phải mất **30-60 phút** để tổng hợp:
- **Số lượng và giá trị pipeline đang mở** (open deals)
- **Top deal lớn nhất** đang chờ
- **Tỷ lệ thành công (win rate)** của team
- **Doanh thu đóng góp** từ các deal đã hoàn thành
- **Giá trị pipeline được tính trọng số** (weighted pipeline) dựa trên từng stage

**Kết quả?** Báo cáo không đồng bộ, mất thời gian, và không thể tự động hóa. **Workflow này giải quyết tất cả!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị giới hạn của n8n Cloud, các sếp nên **self-host** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tháng** không phải tổng hợp báo cáo thủ công.
✅ **Độ chính xác 100%** – Dữ liệu lấy trực tiếp từ Airtable, không sai sót.
✅ **Cá nhân hóa** – Báo cáo được gửi trực tiếp lên Slack với định dạng chuyên nghiệp.
✅ **Hoạt động tự động** – Không cần can thiệp, chạy hàng tuần mà không bị gián đoạn.
✅ **Tăng hiệu quả team** – Toàn bộ Sales team cùng nhìn thấy pipeline thực tế.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Airtable**:
- **Bảng dữ liệu Sales Pipeline** với các trường bắt buộc:
  - `Status` (giá trị: "Open" hoặc "Won")
  - `Value` (giá trị số của deal)
  *(Nếu có thêm trường như `Deal Owner`, `Close Date`, `Stage`, workflow có thể tùy chỉnh thêm)*
- **Token API Airtable** (tạo tại [Airtable API Docs](https://airtable.com/api))

📌 **Slack**:
- **Workspace Slack** với quyền truy cập vào **webhook URL** hoặc **OAuth Token** (tạo tại [Slack API](https://api.slack.com/apps))
- **Channel Slack** để gửi báo cáo (ví dụ: `#sales-report`)

📌 **n8n**:
- **Instance n8n Cloud** (miễn phí, nhưng giới hạn) hoặc **self-hosted** (khuyến nghị).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải workflow từ [n8n.io](https://n8n.io/workflows/6463) hoặc copy JSON từ [đây](https://github.com/n8n-io/workflows/blob/master/workflows/6463.json).

**Bước 2:** Mở **n8n Editor** và chọn:
- **Import Workflow** → Chọn file JSON hoặc **Paste JSON** từ clipboard.

**Bước 3:** Sau khi import, workflow sẽ có **7 nodes** như sau:
```
1. Schedule Trigger (đặt lịch chạy)
2. Search Open Deals (tìm deals đang mở)
3. Search Won Deals (tìm deals đã hoàn thành)
4. Merge Deals (ghép 2 dataset)
5. Slack Message Summary (tạo nội dung báo cáo)
6. Advanced Metrics (tính toán số liệu chi tiết)
7. Slack Message (gửi báo cáo lên Slack)
```

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

##### **🔹 Node 1: Schedule Trigger**
- **Thiết lập lịch chạy**:
  - Chọn **Weekly** (tuần) hoặc **Daily** (ngày).
  - Thời gian khuyến nghị: **Sáng thứ 2** (để team có báo cáo mới nhất vào đầu tuần).
  - Ví dụ: `0 0 * * 2` (chạy lúc 00:00 thứ 2 hàng tuần).

##### **🔹 Node 2 & 3: Search Open Deals & Search Won Deals**
- **Cấu hình Airtable**:
  - **Table Name**: Điền tên bảng Sales Pipeline của bạn (ví dụ: `Sales Pipeline`).
  - **View Name**: Nếu bảng có nhiều view, chọn view phù hợp (nếu không, để trống).
  - **Filter**:
    - **Search Open Deals**:
      ```json
      { "Status": "Open" }
      ```
    - **Search Won Deals**:
      ```json
      { "Status": "Won" }
      ```
  - **Fields to Return**: Chọn tất cả trường cần thiết (nếu không, thêm thủ công trong **Code Node** sau).

##### **🔹 Node 4: Merge Deals**
- **Kiểm tra kết nối**:
  - Node này tự động ghép 2 dataset từ **Open Deals** và **Won Deals**.
  - **Không cần chỉnh sửa** nếu dữ liệu từ Airtable ổn định.

##### **🔹 Node 5 & 6: Slack Message Summary & Advanced Metrics (Code Nodes)**
- **Mở Code Node** và chỉnh sửa **JavaScript** nếu cần:
  - **Slack Message Summary**:
    - Thay đổi **định dạng văn bản** (ví dụ: thay đổi màu sắc, biểu tượng 📈).
    - Thêm trường như `Deal Owner` hoặc `Close Date` vào báo cáo.
  - **Advanced Metrics**:
    - Nếu pipeline có **các stage khác nhau** (ví dụ: `Prospecting`, `Proposal`, `Negotiation`), chỉnh sửa **weighting** trong code để tính toán chính xác.
    - **Ví dụ code cơ bản**:
      ```javascript
      // Tính toán win rate
      const winRate = (wonDeals.length / (openDeals.length + wonDeals.length)) * 100;

      // Tính toán weighted pipeline (ví dụ: stage "Negotiation" = 0.7, "Proposal" = 0.5)
      const weightedPipeline = openDeals.reduce((sum, deal) => {
        const stageWeight = deal.Stage === "Negotiation" ? 0.7 :
                           deal.Stage === "Proposal" ? 0.5 : 0.3;
        return sum + (deal.Value * stageWeight);
      }, 0);
      ```

##### **🔹 Node 7: Slack Message**
- **Chọn Slack Credentials**:
  - Đăng nhập vào **Slack OAuth2 API** (tạo tại [Slack API](https://api.slack.com/apps)).
- **Cấu hình Channel**:
  - Điền **#channel-name** (ví dụ: `#sales-report`).
- **Thêm Attachments (tùy chọn)**:
  - Thêm **bảng biểu đồ** (nếu cần) bằng cách chỉnh sửa code trong **Slack Message Summary**.

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chọn **Run Workflow** để kiểm tra dữ liệu mẫu.
  - Kiểm tra **Slack** xem báo cáo có hiển thị đúng không.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** để workflow chạy tự động theo lịch.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Logs & Debugging**:
   - Sử dụng **Sticky Note Node** để ghi chú lỗi hoặc debug.
   - Ví dụ: Nếu **Airtable không trả về dữ liệu**, kiểm tra **filter** hoặc **token API**.

2. **Gửi Báo Cáo Định Kỳ**:
   - Nếu muốn gửi **ngày khác** (ví dụ: cuối tuần), chỉnh **Schedule Trigger**.
   - Hoặc **trigger thủ công** bằng **Webhook** (nếu cần báo cáo đặc biệt).

3. **Kết hợp với Email**:
   - Thêm **Node Email** để gửi báo cáo cho các sếp không dùng Slack.
   - Ví dụ: Sử dụng **n8n-nodes-base.email** với **SMTP** (Gmail, Outlook).

4. **Tự động Cập Nhật Airtable**:
   - Nếu pipeline thay đổi liên tục, thêm **Webhook** từ Airtable để cập nhật dữ liệu **real-time**.

5. **Tùy Chỉnh Định Dạng Slack**:
   - Sử dụng **Markdown** trong **Slack Message** để làm báo cáo chuyên nghiệp:
     ```markdown
     *📊 Weekly Sales Pipeline Report*
     *Date: {{ $node["Schedule Trigger"].json["$date"] }}*

     **Open Deals:** {{ openDeals.length }} (${{ totalOpenValue.toLocaleString() }})
     **Won Deals:** {{ wonDeals.length }} (${{ totalWonValue.toLocaleString() }})
     **Win Rate:** {{ winRate.toFixed(2) }}%
     **Top Deal:** ${{ topDealValue.toLocaleString() }} ({{ topDealName }})
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp Sales để tập trung vào **đàm phán và đóng deal** thay vì mất công tổng hợp báo cáo. **Chỉ cần 5 phút setup**, sau đó **tự động hóa hoàn toàn**!

**Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io](https://n8n.io/workflows/6463).
2. **Chỉnh sửa Airtable & Slack credentials**.
3. **Test & Active** để bắt đầu nhận báo cáo tự động hàng tuần.

**Cần hỗ trợ?** Hãy tham gia [n8n Discord](https://discord.com/invite/XPKeKXeB7d) hoặc [Forum n8n](https://community.n8n.io/) để được hỗ trợ chi tiết!

---
**💡 Lưu ý cuối cùng:**
- Nếu **self-host n8n**, các sếp có thể **tùy chỉnh thêm** workflow (ví dụ: thêm **LLM** để phân tích xu hướng, hoặc **Google Sheets** để lưu lịch sử).
- **N8N Cloud** cũng hoạt động, nhưng **self-host** ổn định hơn và không bị giới hạn.