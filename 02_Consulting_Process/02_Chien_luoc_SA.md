---
type: Process Detail
role: Lark Solution Architect
phase: 2
---
# Giai đoạn 2: Lên Chiến lược & Kiến trúc Giải pháp (SA)

**Mô tả:** Kiến trúc sư giải pháp (Lark Solution Architect - SA) chuyển đổi các Nỗi đau đã đóng khung (Locked Pains) thành một bản thiết kế hệ thống hoàn chỉnh có thể cấu hình được trên hệ sinh thái Lark Suite (Base, Approval, AnyCross, Messenger/Bot, Open API). 

**Khi nào bắt đầu:** Chỉ kích hoạt khi **ĐÃ CÓ BA REPORT** hoàn chỉnh (Hard Gate). Nếu BA Report thiếu Pain Points hoặc Constraints, SA phải từ chối thiết kế để tránh rủi ro đập đi xây lại.

---

## Các bước triển khai chi tiết (10 Bước Solution Design)
1. **Reframe Pain:** Đi từ `Pain ID` của BA, viết lại thành `Design Problem` (Bài toán thiết kế cấp hệ thống).
2. **Định vị Lark:** Xác định rõ Lark đóng vai trò gì. (Ví dụ: Collaboration Hub, Workflow Engine, Operational Layer...). Lưu ý: Lark KHÔNG BAO GIỜ là ERP/CRM sinh ra dữ liệu gốc (nếu DN đã có Core system).
3. **Chiến lược Tích hợp:** Lên chiến lược `Keep` (Giữ lại), `Integrate` (Tích hợp API/AnyCross), hay `Replace` (Thay thế bằng Base) đối với các phần mềm cũ của khách.
4. **High-level Architecture:** Vẽ ranh giới phân định hệ thống. Liệt kê các Module Lark lõi sẽ dùng.
5. **Data Schema (Lark Base):** Hệ thống hóa cấu trúc Bảng và Trường dữ liệu. **Bắt buộc tuân thủ [[Tpl_LarkBase_Convention]]** — Áp dụng đúng tiền tố (`tbl_`, `fk_`, `calc_`...), Mandatory Fields (ID, trạng thái, audit), Field Type Mapping chuẩn. Không nên lập bảng >15 field cho Phase 1.
6. **Automation & Approval:** Thiết kế Triggers, Actions và luồng duyệt Approval Workflow nhiều cấp.
7. **Detailed Process:** Map giải pháp chi tiết vào từng quy trình cốt lõi (Ai làm gì trên Lark, tự động gửi bot báo thế nào).
8. **Data Ownership:** Xác định nguyên tắc "Single Source of Truth" duy nhất cho mỗi thực thể dữ liệu.
9. **KPI & ROI Mapping:** Map trực tiếp Giải pháp Lark với `Pain ID` tương ứng và chỉ tiêu thay đổi (Ví dụ: Thời gian duyệt 3 ngày -> 4 tiếng).
10. **Phased Rollout Plan:** Chia lộ trình triển khai thành 3 giai đoạn để MVP vận hành trước. Tuyệt đối không tung toàn bộ tính năng ở tuần đầu tiên (Ví dụ: Core Foundation -> Automation -> Integration/AnyCross).

---

## Tiêu chuẩn đầu ra (Input / Output)
- **Input:** BA Report (Danh sách Pain Points Locked, Ràng buộc về ngân sách, Plan của Lark Pro/Enterprise).
- **Output:** Báo cáo **SA Report** gồm 12 phần, đặc biệt có mục `Handoff notes` rất rõ (Danh sách Actor, hệ thống, quy trình cần vẽ) để kỹ sư UML chặng sau xây dựng sơ đồ chính xác tuyệt đối.

## Các Template liên quan
- Mẫu Kiến trúc Giải pháp: [[Tpl_SA_Report]]
- Quy ước đặt tên Lark Base: [[Tpl_LarkBase_Convention]]
