---
type: Process Detail
role: UML Engineer & Base Auto-Builder
phase: 3 & 5
---
# Giai đoạn 3 & 5: Thiết kế UML & Xây dựng Tự động

**Mô tả:** UML Engineer là người dịch bản Thiết kế của SA thành các bản vẽ cấu trúc thực thi chính xác (bằng PlantUML) dựa trên luồng nghiệp vụ. Một sơ đồ ERD đúng chuẩn ở bước này KHÔNG ĐƯỢC PHÉP sai lầm vì nó sẽ là **Input đầu vào bắt buộc** cho quá trình Auto-Build (Tạo cấu trúc Lark Base tự động thông qua AI + Lark MCP API).

**Khi nào bắt đầu:** Khi có bản SA Report cùng "Handoff Notes" chỉ định rõ ràng các hệ thống, luồng dữ liệu và thực thể từ Solution Architect.

---

## Cấp độ dùng UML Theo Từng Giai Đoạn (Phase-Aware)

| Giai đoạn | Mục đích | Sơ đồ sử dụng (PlantUML) |
|---|---|---|
| **Phase 1 (BA)** | Hiểu tổng quan | **Context Diagram**, **Value Stream Map**, Actor, Không vẽ API. |
| **Phase 2 (BA)** | Xác nhận Pain Points | **AS-IS Process Flow (Swimlane)**, bôi đỏ các điểm nghẽn, lỗi. |
| **Phase 3 (SA)** | Trình bày luồng TO-BE | **Context Diagram**, **Sequence Diagram** (Bot/Approve), **Data ERD**. |

---

## Các bước triển khai chi tiết Giai đoạn 3

1. **Parse Input từ SA Report:** Nhận chính xác tên hệ thống (Lark Approval, Lark Base, ERP cũ...), Actor và Quy tắc tích hợp.
2. **Context Diagram:** Sơ đồ C4 Level 0, chỉ bóc tách tương tác giữa Người dùng cuối và Hệ sinh thái giải pháp. Đo lường KPI trực tiếp trên mũi tên của biểu đồ.
3. **Swimlane Activity:** Vẽ luồng thao tác. Nêu rõ Actor A tạo Ticket ở Base -> Automation trigger -> Approver nhận tin ở Bot.
4. **Message Sequence:** Minh hoạ luồng đằng sau hệ thống. Lark gọi Webhook sang ERP, ERP báo status OK, Lark push thẻ tin nhắn (Card) cho nhân viên.
5. **Blueprint ERD (Base Architecture):** Vẽ sơ đồ thực thể liên kết (ERD) dùng cú pháp PlantUML chặt chẽ. **Bắt buộc tuân thủ [[Tpl_LarkBase_Convention]]** — Đánh dấu Type theo ký hiệu chuẩn `(SingleSelect)`, `(AutoNumber)`, `(DuplexLink)`... Đối chiếu Checklist trước khi chuyển sang Giai đoạn 5.

---

## Chuẩn bị chạy Build Phase (Phase 5)
Kỹ sư dùng sơ đồ ERD từ Giai đoạn 3 làm Input cho công cụ Auto-Build (`lark-mcp`). Các yêu cầu cho ERD (**xem chi tiết tại [[Tpl_LarkBase_Convention]]**):
- Chú thích loại trường theo ký hiệu chuẩn: `(Text)`, `(SingleSelect)`, `(DuplexLink)`, `(Person)`...
- Xác định rõ quan hệ `1:1`, `1:N`, `N:N` để bot Lark hiểu và thiết lập `multiple: true/false` trong Base.
- Primary Key (Trường đầu tiên) bắt buộc — đặt theo `<entity>_id`.
- Đủ 5 Mandatory Fields: ID, trang_thai, dt_created, dt_modified, nguoi_tao.

## Tiêu chuẩn đầu ra (Input / Output)
- **Input:** SA Report & Handoff Notes.
- **Output:** Các bản Code / Diagram PlantUML chuẩn syntax đã qua Quality Gate. Yêu cầu có sự đồng thuận từ Khách hàng vào file ERD trước khi tạo Base.

## Các Template liên quan
- Hướng dẫn cú pháp/Template vẽ UML: [[Tpl_UML_Guide]]
- Quy ước đặt tên Lark Base: [[Tpl_LarkBase_Convention]]
