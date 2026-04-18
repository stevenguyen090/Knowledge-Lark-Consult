---
type: BA Report
client: Nga Fashion
project: Phân Ca Quản Lý Cửa Hàng
version: 1.0
---

# Báo cáo Phân tích Kinh doanh (BA Report) — Nga Fashion

**Ngày tạo:** 2026-04-11 | **Prepared by:** Consultant | **Trạng thái:** Phase 1 Complete
## 1. Bối Cảnh (Business Context)
- Cửa hàng thời trang SME (Nga Fashion).
- Đội ngũ nhân sự bán hàng cần lên lịch ca làm việc theo tuần.
- Mô hình vận hành cần đảm bảo bao phủ thời gian mở cửa cửa hàng thông qua các ca làm việc nối tiếp hoặc song song, đồng thời tuân thủ gắt gao các quy định về quỹ thời gian và ngày nghỉ của từng loại hình nhân sự.

## 2. Kiến Thức Nghiệp Vụ (Domain Knowledge)
- **Cơ cấu nhân sự:** 5 người, trong đó gồm 3 Full-time (FT) và 2 Part-time (PT).
- **Ca làm việc tiêu chuẩn:**
  - Ca 1 (Sáng sớm): `06:00 - 09:00` (3 giờ) — Thường là ca tuỳ chọn hoặc tăng cường.
  - **Ngày nghỉ ca (Off-day):** Mỗi nhân sự được nghỉ 1 buổi/tuần, bắt buộc rơi vào Chủ Nhật hoặc Thứ Hai.
  - **Làm thêm ca:** Cho phép 1 nhân sự làm 2 ca trong 1 ngày (ưu tiên các ca không trùng giờ).
  - **Định biên ca Tối đêm:** Cần ít nhất 2 Part-time hoặc 1 Full-time làm thêm/trực online để đảm bảo vận hành.
  - **Địa điểm:** Sáng sớm & Tối đêm (Online tại nhà); Sáng chiều & Chiều tối (Offline tại cửa hàng). Tối đa 2 ngày làm tại nhà/tuần cho FT.

## 3. Quy Trình Chi Tiết (End-to-End Processes)

**Tên quy trình:** Lên lịch làm việc hàng tuần

| Bước | Actor | Hành động | Thông tin nhập vào | Thông tin đầu ra | Công cụ hiện tại |
|---|---|---|---|---|---|
| 1 | Cửa hàng trưởng | Nhận lịch đăng ký hoặc tự phân bổ | Tên NV, Ngày làm, Ca làm | Draft lịch làm việc | Sổ tay / Excel / Zalo |
| 2 | Cửa hàng trưởng | Cân đối và đối soát ràng buộc | So sánh giờ, đếm số ngày, kiểm tra off-day | Lịch chuẩn | Não bộ / Excel |
| 3 | Cửa hàng trưởng | Công bố lịch làm việc tuần | File lịch | File / Ảnh | Zalo Group |

## 4. Các Bộ Phận Tham Gia (Roles & Responsibilities)
| Role / Bộ phận | Người ra quyết định? | Người vận hành? | Chú thích | Mô tả vai trò, trách nhiệm |
| -------------- | -------------------- | --------------- | -------------- | ----------------------------------------------------------------------------------- |
| Trưởng Cửa Hàng | Yes | Yes | Người phân ca | Trực tiếp kéo thả, sắp xếp lịch ca, cân đối điều chỉnh khi có người xin nghỉ đột xuất. |
| Nhân viên Bán Hàng | No | No | FT / PT | Nhận lịch làm việc, có mặt tại cửa hàng đúng ca được phân công. |

## 5. Công Cụ Hiện Tại (Current Systems & Tooling)
| Phân loại | Công cụ đang dùng | Rủi ro rò rỉ / Lỗi dữ liệu |
|---|---|---|
| Xếp lịch (Scheduling) | Excel / Viết tay và gửi Zalo | Tốn vài giờ mỗi tuần; Dễ tính sai giờ của PT; Khó kiểm soát ngày Off-day có tuân thủ hay không. Khó điều chỉnh khi có thay đổi. |

## 6. Điểm Nghẽn Giả Định (Hypothesized Pain Points)
- Quản lý cửa hàng mất quá nhiều thời gian để kiểm tra chéo (cross-check) xem đã chia ca công bằng chưa.
- Nhân viên cảm thấy ca làm không đồng đều.

## 7. ĐIỂM NGHẼN ĐÃ XÁC NHẬN (PAIN LOCK)
- **PAIN ID:** P-01
- **TITLE:** Khó khăn trong việc đối soát ràng buộc xếp ca (Constraint Validation).
- **STATEMENT:** *"Mỗi tuần xếp ca lại, việc đảm bảo giờ của PT bằng 1/2 FT, rồi FT đủ 6 ngày làm, nghỉ đúng Chủ Nhật/Thứ 2 là rất đau đầu. Xếp xong tính lại cứ bị dư hoặc thiếu giờ."*
- **IMPACT:** Tổn thất thời gian của Quản lý hàng tuần, nguy cơ xếp sai dẫn đến tranh chấp lương/giờ làm của nhân viên.
- **SEVERITY:** 🔴 Critical
- **ROOT CAUSE:** Tính toán thủ công bằng mắt và trí nhớ.
- **SOLUTION EXPECTATION:** Hệ thống tự động gợi ý/xếp ca (Auto-scheduling) dựa trên các ràng buộc đã thiết lập. Quản lý chỉ cần kiểm duyệt lại.

## 8. Ràng Buộc Thiết Kế (Constraints)
- Ngân sách và công cụ: Sử dụng hệ sinh thái Lark Base (không sử dụng phần mềm mua ngoài cồng kềnh).

## 9. Câu Hỏi Khám Phá (Discovery Questions)
- Ca Sáng sớm (06:00-09:00) có nhân sự chuyên trách không hay ai cũng có thể làm?
- Có những ngày dồn đông khách cần thêm người thì có vi phạm luật 1 ngày/người/ca không hay có thể tăng cường 2 người cùng 1 ca?

## 10. Handoff Notes for Solution Architect
- Hệ thống hướng tới **Auto-Schedule** (Tự động gợi ý lịch). 
- Cần xử lý logic phức tạp thông qua **Lark Base Script** hoặc **AppScript API** để phân bổ ca dựa trên tổ hợp nhân sự hiện có (3 FT, 2 PT), đảm bảo coverage ca đêm và giới hạn 2 ngày Online/tuần cho FT.
