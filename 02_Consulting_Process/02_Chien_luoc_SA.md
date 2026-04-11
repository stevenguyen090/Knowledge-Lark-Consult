---
type: Process Detail
role: Lark Solution Architect
phase: 2
---
# Giai đoạn 2: Lên Chiến lược & Kiến trúc Giải pháp (SA)

**Mô tả:** Kiến trúc sư giải pháp (Lark Solution Architect - SA) chuyển đổi các Nỗi đau đã đóng khung (Locked Pains) thành một bản thiết kế hệ thống hoàn chỉnh có thể cấu hình được trên hệ sinh thái Lark Suite (Base, Approval, AnyCross, Messenger/Bot, Open API). 

**Khi nào bắt đầu:** Chỉ kích hoạt khi **ĐÃ CÓ BA REPORT** hoàn chỉnh (Hard Gate). Nếu BA Report thiếu Pain Points hoặc Constraints, SA phải từ chối thiết kế để tránh rủi ro đập đi xây lại.

---

## Các bước triển khai chi tiết (12 Bước Solution Design)

1. **Reframe Pain:** Đi từ `Pain ID` của BA, viết lại thành `Design Problem` (Bài toán thiết kế cấp hệ thống).
2. **Định vị Lark:** Xác định rõ Lark đóng vai trò gì. (Ví dụ: Collaboration Hub, Workflow Engine, Operational Layer...). Lưu ý: Lark KHÔNG BAO GIỜ là ERP/CRM sinh ra dữ liệu gốc (nếu DN đã có Core system).
3. **Chiến lược Tích hợp:** Lên chiến lược `Keep` (Giữ lại), `Integrate` (Tích hợp API/AnyCross), hay `Replace` (Thay thế bằng Base) đối với các phần mềm cũ của khách.
4. **High-level Architecture:** Vẽ ranh giới phân định hệ thống. Liệt kê các Module Lark lõi sẽ dùng.
5. **Data Schema (Lark Base):** Hệ thống hóa cấu trúc Bảng và Trường dữ liệu. **Bắt buộc tuân thủ [[Tpl_LarkBase_Convention]]** — Áp dụng đúng quy tắc đặt tên thân thiện (Friendly Naming), Mandatory Fields (Mã, Trạng thái, Ngày tạo...), Field Type Mapping chuẩn. Không nên lập bảng >15 field cho Phase 1.
6. **Automation & Approval:** Thiết kế Triggers, Actions và luồng duyệt Approval Workflow nhiều cấp.
7. **Detailed Process:** Map giải pháp chi tiết vào từng quy trình cốt lõi (Ai làm gì trên Lark, tự động gửi bot báo thế nào).
8. **Data Ownership:** Xác định nguyên tắc "Single Source of Truth" duy nhất cho mỗi thực thể dữ liệu.
9. **KPI & ROI Mapping:** Map trực tiếp Giải pháp Lark với `Pain ID` tương ứng và chỉ tiêu thay đổi (Ví dụ: Thời gian duyệt 3 ngày -> 4 tiếng).
10. **Phased Rollout Plan:** Chia lộ trình triển khai thành 3 giai đoạn để MVP vận hành trước. Tuyệt đối không tung toàn bộ tính năng ở tuần đầu tiên (Ví dụ: Core Foundation -> Automation -> Integration/AnyCross).
11. **AppScript / WebJob Strategy:** Đánh giá xem giải pháp có cần xử lý ngoài Lark không (xem mục dưới).
12. **API Catalog & Integration Spec:** Nếu có tích hợp hệ thống ngoài, bắt buộc lập bảng API Catalog chuẩn (xem mục dưới).

---

## 📌 Bước 11 — AppScript / WebJob Strategy

### Khi nào cần AppScript thay vì Lark Automation thuần?

Lark Automation (trigger/action native) **không đủ** cho các trường hợp sau — cần AppScript hoặc WebJob chạy ngoài:

| Tình huống | Dấu hiệu nhận biết | Giải pháp đề xuất |
|---|---|---|
| **Realtime nặng** | Sync dữ liệu liên tục giữa Lark Base và Google Sheet / Spreadsheet / hệ thống ERP | AppScript with time-trigger (mỗi 1-5 phút) |
| **Logic phức tạp** | Tính toán nhiều bảng, điều kiện lồng nhau, phân bổ tự động (lương, KPI, tồn kho) | AppScript hoặc Python WebJob |
| **Batch processing** | Gửi hàng loạt thông báo, tổng hợp dữ liệu cuối ngày/tuần | Google Apps Script Trigger hoặc Scheduled Job |
| **Xử lý file** | Parse Excel/PDF upload, đọc nội dung file đính kèm | Python WebJob qua Webhook |
| **Fallback khi Lark API rate limit** | Cần queue và retry khi call API thất bại | WebJob với retry logic |

### Kiến trúc AppScript tiêu biểu

```
[Lark Base / Lark Bot Event]
    → Webhook → AppScript Web App (doPost)
        → Xử lý logic
        → Gọi Lark Open API để ghi/đọc Base
        → (Tùy chọn) Ghi log vào Google Sheet
```

### Quy tắc khi đề xuất AppScript

- **Ưu tiên Lark native trước** — chỉ dùng AppScript khi native không đủ.
- **Ghi rõ WebJob interval** trong SA Report: mỗi 5 phút? 10 phút? hay event-driven?
- **Logging bắt buộc:** Mọi AppScript phải ghi log ra một Sheet "Logs" để debug.
- **Không để credentials trong code:** Dùng `PropertiesService.getScriptProperties()`.

---

## 📌 Bước 12 — API Catalog & Integration Spec

Khi giải pháp cần tích hợp hệ thống ngoài (MISA, KiotViet, Zalo OA, ERP...), SA **bắt buộc** lập bảng API Catalog đầy đủ trước khi bàn giao UML Engineer.

### Bảng API Catalog chuẩn

| # | Tên API / Endpoint | Phương thức | Mục đích | Auth | Webhook? | Event Webhook | Retry? | Miss Event? | Ghi chú |
|---|---|---|---|---|---|---|---|---|---|
| 1 | `/v1/orders` | GET | Lấy danh sách đơn hàng | API Key / OAuth2 | ❌ | — | ✅ Exponential Backoff | N/A | Polling mỗi 5 phút |
| 2 | `/v1/order/created` | WEBHOOK | Nhận đơn hàng mới | HMAC Signature | ✅ | `order.created` | ✅ | ⚠️ Không có — cần polling bù | Cần lưu event_id để dedup |

### Checklist tích hợp bắt buộc phải trả lời

| Câu hỏi | Đã xác nhận? |
|---|---|
| Endpoint API là gì? Base URL + path cụ thể | [ ] |
| Cơ chế xác thực: API Key / OAuth2 / Basic Auth / HMAC? | [ ] |
| Token có TTL không? Cần refresh flow không? | [ ] |
| Hệ thống đối tác có cung cấp Webhook không? | [ ] |
| Nếu có Webhook: danh sách event nào được push? | [ ] |
| Có cơ chế retry khi call API thất bại không? | [ ] |
| Nếu Webhook miss event (down server, timeout): có API để bù không? | [ ] |
| Rate limit của API là bao nhiêu req/phút? | [ ] |
| Môi trường Sandbox/Test khả dụng không? | [ ] |

### Chiến lược xử lý Miss Event

```
Webhook nhận → Lưu vào Queue (Google Sheet / DB nhỏ)
    → Xử lý → Đánh dấu processed
    → WebJob định kỳ: polling API để bù các event bị miss
    → Dùng event_id / timestamp để deduplication
```

---

## Tiêu chuẩn đầu ra (Input / Output)
- **Input:** BA Report (Danh sách Pain Points Locked, Ràng buộc về ngân sách, Plan của Lark Pro/Enterprise).
- **Output:** Báo cáo **SA Report** gồm 12 phần, đặc biệt có mục `Handoff notes` rất rõ (Danh sách Actor, hệ thống, quy trình cần vẽ) để kỹ sư UML chặng sau xây dựng sơ đồ chính xác tuyệt đối.

## Các Template liên quan
- Mẫu Kiến trúc Giải pháp: [[Tpl_SA_Report]]
- Quy ước đặt tên Lark Base: [[Tpl_LarkBase_Convention]]
