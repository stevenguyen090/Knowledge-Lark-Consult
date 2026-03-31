---
type: Process Detail
role: Business Analyst
phase: 1
---
# Giai đoạn 1: Khám phá Nhu cầu & Xác nhận Nỗi đau (BA)

**Mô tả:** Vai trò của BA không chỉ là ghi chép quy trình, mà là xây dựng "sự thấu hiểu chung về thực trạng" làm cơ sở bảo vệ mọi quyết định thiết kế phía sau. Một "Pain Point" (Nỗi đau) chưa được khách hàng xác nhận thì chỉ là phỏng đoán. 

**Khi nào bắt đầu:** Ngay khi tiếp nhận thông tin khách hàng từ các nguồn (Cold Start, Partial Context, hoặc Rich Context). Sẽ áp dụng Socratic Questioning để làm rõ nếu thông tin khách hàng đưa ra quá mơ hồ hoặc đi thẳng vào giải pháp.

---

## Các bước triển khai chi tiết

### Bước 1: Nghiên cứu Domain (Domain Research Mode)
BA bắt buộc hoàn thiện 9 phần nghiên cứu trước khi đề xuất bất kỳ giải pháp nào. TUYỆT ĐỐI không bàn về System/Lark ở đây.
1. **Business Archetype & Scale:** Xác định quy mô & loại hình doanh nghiệp (B2B, B2C, Retail...).
2. **Value Flow:** Vẽ chuỗi giá trị (Value flow) & Mô hình kinh doanh kiếm tiền từ đâu.
3. **Domain Knowledge:** Củng cố định nghĩa, thuật ngữ theo ngành nghề cụ thể.
4. **End-to-End Processes:** Liệt kê các quy trình chuẩn (Trigger -> N Steps -> End State).
5. **Roles & Responsibilities:** Xác định ai làm gì, ai ra quyết định, ai sẽ hưởng lợi/phản đối.
6. **Dự đoán Pain Points:** Dự đoán các điểm nghẽn dựa theo quy mô (Operational, Visibility, Data coordination, Growth).
7. **Current Systems:** Nắm bắt công cụ hiện tại & rủi ro dữ liệu (Excel, Zalo, Giấy tờ...).
8. **Constraints:** Xác định ràng buộc ranh giới (Ngân sách, Nhân sự IT, Timeline, Bảo mật).
9. **Discovery Questions:** Chuẩn bị bộ câu hỏi Socratic để phỏng vấn/xác nhận với Stakeholder.

### Bước 2: Cổng Xác Nhận Nỗi Đau (Pain Confirmation Gate)
- Gặp trực tiếp C-Level / Quản lý để xác nhận các Pain Points dự đoán hoặc bổ sung Pain Points mới.
- Khóa (Lock) Pain Point: Một nỗi đau chỉ được xem là "Locked" khi được khách hàng chính thức xác nhận bằng lời. Dùng chuẩn cấu trúc Pain Lock: `PAIN ID`, `STATEMENT (Trích dẫn lời)`, `IMPACT (Ảnh hưởng)`, `SEVERITY`, `ROOT CAUSE`.

---

## Tiêu chuẩn đầu ra (Input / Output)
- **Input:** Thông tin ngành nghề cơ bản, tóm tắt sơ bộ từ Sale/Stakeholders.
- **Output (Hard Gate):** Bản báo cáo **BA Report** chứa 10 phần tiêu chuẩn. Bắt buộc phải có danh sách Pain Lock và Các ràng buộc (Constraints) để chuyển giao. Không có BA Report thì không được phép chuyển sang Giai đoạn 2.

## Các Template liên quan
- Mẫu Báo cáo Khám phá: [[Tpl_BA_Report]]
- Mẫu Thu thập thông tin Khách hàng nhanh: [[Tpl_Thong_tin_Khach]]
