---
type: User Guide
client: Nga Fashion
solution: Auto-Scheduling — Hệ thống Phân ca Tự động cho Team Sales
version: 1.1
created: 2026-04-11
status: Draft
---

# 📘 Tài Liệu Hướng Dẫn Sử Dụng Hệ Thống — Nga Fashion

> **Dành cho:** Chị Nga & Team Sales
> **Phiên bản:** v1.1 | **Ngày cập nhật:** 2026-04-11

---

## 📌 PHẦN 1: TỔNG QUAN QUY TẮC PHÂN CA (RULES)

Để hệ thống tự động xếp ca chính xác, các quy tắc sau đã được thiết lập:

1. **Quỹ thời gian:**
   - **Full-time (FT):** Làm 6 ngày/tuần.
   - **Part-time (PT):** Tổng giờ bằng 1/2 nhân sự FT.
2. **Ngày nghỉ (Off-day):** Phải rơi vào Chủ Nhật hoặc Thứ Hai.
3. **Làm thêm (Extra Shifts):** 1 nhân sự có thể làm **2 ca/ngày** (ưu tiên các ca không trùng giờ).
4. **Định biên ca đêm:** Ca Tối đêm (Online) luôn cần 2 PT hoặc 1 FT.
5. **Hình thức:** Tối đa 2 ngày làm tại nhà (Online) mỗi tuần cho FT.

---

## 🏗️ PHẦN 2: HƯỚNG DẪN THAO TÁC (USER FLOW)

### Bước 1: Khai báo ngày nghỉ & Nhân sự
Trước khi bắt đầu tuần mới, Quản lý vào bảng `tbl_NhanSu` để xác định ngày nghỉ (CN hoặc T2) cho từng người.

### Bước 2: Kích hoạt Tự động xếp ca
- Tại giao diện Lark Base, nhấn nút **"Auto-Schedule"**.
- Hệ thống (qua Script/API) sẽ tự động tính toán và tạo các dòng lịch làm việc trong bảng `tbl_LichLamViec`.

### Bước 3: Kiểm tra và Điều chỉnh
- Chuyển sang chế độ xem **Calendar View** để quan sát trực quan.
- Hệ thống sẽ đánh dấu 🔴 nếu có bất kỳ vi phạm nào (Ví dụ: FT làm thiếu ngày, PT lố giờ).
- Quản lý có quyền kéo thả hoặc sửa trực tiếp để tối ưu lại theo tình hình thực tế.

### Bước 4: Công bố lịch tự động
- Vào 20h00 tối Thứ 7 hàng tuần, Lark Bot sẽ tự động gửi thông báo lịch làm việc vào nhóm chat chung.

---

## ❓ PHẦN 3: CÁC CÂU HỎI THƯỜNG GẶP

| Câu hỏi | Trả lời |
|---|---|
| Có thể chỉnh lịch sau khi đã Auto-Schedule không? | Có, Quản lý hoàn toàn có thể sửa thủ công sau khi hệ thống gợi ý. |
| Nếu có người xin nghỉ đột xuất? | Quản lý xóa ca của người đó và gán cho người khác, hệ thống sẽ tự cập nhật lại Validator. |
| Tại sao hệ thống báo đỏ? | Rê chuột vào ô Validator để xem lý do (Ví dụ: "Lố giờ PT"). |

---
