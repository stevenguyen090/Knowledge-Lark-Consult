---
type: Template
target: BA Report
---
# Báo cáo Phân tích Kinh doanh (BA Report) — [Tên Khách Hàng]
**Ngày tạo:** [YYYY-MM-DD] | **Prepared by:** Business Analyst | **Trạng thái:** [Phase 1 Complete / Pending Handoff]

## 1. Bối Cảnh (Business Context)
- Cấu trúc doanh nghiệp (SME/Growth/Enterprise).
- Tóm tắt chuỗi giá trị và cách kiếm tiền (Input → Process → Capture Revenue).

## 2. Kiến Thức Nghiệp Vụ (Domain Knowledge)
- Các thuật ngữ ngành, quy định pháp lý, quy chế nội bộ đặc thù.

## 3. Quy Trình Chi Tiết (End-to-End Processes)

> Format: [Trigger] → [Step 1: Actor làm gì/ra sao] → ... → [End State]

Với mỗi quy trình, bổ sung bảng dữ liệu actor thực hiện:

**Tên quy trình:** [Tên]

| Bước | Actor | Hành động | Thông tin nhập vào | Thông tin đầu ra | Công cụ hiện tại |
|---|---|---|---|---|---|
| 1 | [Vai trò] | [Làm gì] | [Điền gì, nhập gì] | [Tạo ra gì] | [Excel/Zalo/...] |
| 2 | | | | | |

## 4. Các Bộ Phận Tham Gia (Roles & Responsibilities)
| Role / Bộ phận | Người ra quyết định? | Người vận hành? | Chú thích      | Mô tả vai trò, trách nhiệm                                                          |
| -------------- | -------------------- | --------------- | -------------- | ----------------------------------------------------------------------------------- |
| Admin          | Yes                  | No              | Quyền cao nhất | Xem bảng lương, tạo bảng lương, quản lý chấm công của nhân sự, đi lương cho nhân sự |

## 5. Công Cụ Hiện Tại (Current Systems & Tooling)
| Phân loại | Công cụ đang dùng (Excel, Zalo...) | Rủi ro rò rỉ / Lỗi dữ liệu |
|---|---|---|
| Xét duyệt | Ký giấy cứng hằng tuần | Mất hồ sơ, không thống kê được |

## 6. Điểm Nghẽn Giả Định (Hypothesized Pain Points)
- [Operational] Pains...
- [Visibility] Leader thiếu góc nhìn...
*(Dự đoán chuyên gia - cần xác nhận).*

## 7. ĐIỂM NGHẼN ĐÃ XÁC NHẬN (PAIN LOCK)
> VÍ DỤ MỘT PAIN POINT:
- **PAIN ID:** P-01
- **TITLE:** Nút thắt quy trình Duyệt kho
- **STATEMENT:** "[Quote lời của khách hàng nói]"
- **IMPACT:** Tổn thất 10 giờ làm việc/tuần, kho chờ sếp lâu.
- **SEVERITY:** 🔴 Critical / 🟡 Significant 
- **ROOT CAUSE:** Do chưa có hệ thống flow tự động thông báo.

## 8. Ràng Buộc Thiết Kế (Constraints)
- Ngân sách (X triệu), Hệ sinh thái (Đang dùng Lark Basic/Pro/Enterprise)...
- Timeout: Cần go-live trước ngày...

## 9. Câu Hỏi Khám Phá (Discovery Questions)
- Bộ câu hỏi Socratic đã hỏi.

## 10. Handoff Notes for Solution Architect
- Các rủi ro lưu ý SA: "Giám đốc hay đổi ý, cần flow đơn giản trước", "Bảng này nên phân rõ quyền để nhân sự dưới không sửa bậy được".
