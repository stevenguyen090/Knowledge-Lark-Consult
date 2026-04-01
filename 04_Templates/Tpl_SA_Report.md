---
type: Template
target: SA Report
---
# Báo Cáo Kiến Trúc Giải Pháp SA — [Tên Khách Hàng]
**Ngày tạo:** [YYYY-MM-DD] | **Tham chiếu:** [Tên file BA Report] | **Kế hoạch Lark:** [Pro/Enterprise]

## 1. Map Pain Point vào Vấn đề Thiết kế
- CHUYỂN HOÁ: Pain P-01 (Giấy tờ chậm) -> Design Problem (Thiếu quy trình Approval số hoá liên kết với hệ thống nhắc hẹn).

## 2. Vai Trò của Lark
- Lark đóng vai trò là "Workflow Engine" và "Operational Layer". Mọi thứ Transactional (Ví dụ hoá đơn đỏ) vẫn để ở ERP.

## 3. Chiến Lược Tích Hợp (Integration Strategy)
| Tên Hệ Thống Khách Hàng | Loại | Chiến Lược (Keep/Replace/Integrate) | Giải thích |
|---|---|---|---|
| MISA / KiotViet | Kế toán/Hàng | Keep | Đồng bộ đơn hàng về Base thông qua Anycross (Chỉ đọc) |

## 4. Kiến Trúc High-Level
- Ranh giới giải pháp: Nhân viên dùng Lark Chat để trình duyệt -> Flow về Lark Base -> Data đẩy về Cấp quản lý phân tích ở Bitable Dashboard.

## 5. Schema Lark Base (Sơ đồ bảng dữ liệu)
> ⚠️ **Bắt buộc tuân thủ:** [[Tpl_LarkBase_Convention]] khi đặt tên bảng, trường và chọn field type.
> Tên Bảng: `Đơn hàng` - Purpose: Theo dõi đơn.
> Fields: `Mã đơn hàng (AutoNumber)`, `Sản phẩm (SingleSelect)`, `Thành tiền (Currency)`, `Trạng thái (SingleSelect)`. Views: Kanban theo trạng thái.

## 6. Lên cấu trúc Automation & Approval
> **Automation ID:** AUT-001 | **Trigger:** Trạng thái Order = Đã chuẩn bị | **Action:** Gắn thẻ tin nhắn (Tag) Bot báo Sales.
> **Approval Flow:** Form yêu cầu -> Node 1 (Quản lý trực tiếp) -> Node 2 (Branch: Nếu >5 triệu -> Giám đốc).

## 7. Giải pháp chi tiết theo Quy Trình
- Bước 1 -> Nhân sự làm A -> Cập nhật Base B -> Bot C cảnh báo sếp.

## 8. Data Flow & Ownership
- Entity A (Sản phẩm) -> Source of Truth: KiotViet. Mọi dữ liệu về Lark chỉ để lookup/sync tự động 1 chiều để tham khảo. 

## 9. KPI & Đo lường ROI
| Pain ID | Cấu phần giải pháp | Cột mốc KPI (Baseline -> Target) |
|---|---|---|
| P-01 | Lark Approval / SLA | Phê duyệt 3 ngày -> 3h trên Điện thoại. |

## 10. Lộ Trình Triển Khai (Phased Rollout)
- **Phase 1 (Tuần 1-3):** Dọn dẹp data cũ, số hoá 3 bảng Core, Flow Approval chuẩn.
- **Phase 2 (Tuần 4-5):** Gắn Automation gửi Messenger, Dashboard báo cáo sếp.
- **Phase 3 (Tuần 6+):** AnyCross nối với tool ngoài.

## 11. Các Ràng buộc & Câu hỏi Mở
## 12. Handoff Notes cho UML Engineer
- "Draw 1 Sequence diagram for the Approval workflow. Export ERD base with PlantUML using Text/Link formats for Phase 5 to run Lark Auto-build."
