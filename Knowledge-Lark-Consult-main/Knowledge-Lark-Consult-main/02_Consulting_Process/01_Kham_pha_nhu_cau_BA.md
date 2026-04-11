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

---

#### 1.1 Business Archetype & Scale
**Mô tả:** Xác định quy mô và loại hình doanh nghiệp để định khung toàn bộ quá trình phân tích. Loại hình ảnh hưởng đến luồng tiền, cấu trúc nhân sự, và mức độ phức tạp của quy trình.

| Trường thông tin | Giá trị mẫu | Ghi chú |
|---|---|---|
| Loại hình kinh doanh | B2B / B2C / B2B2C / Retail | Chọn loại phù hợp nhất |
| Quy mô nhân sự | < 50 / 50–200 / 200–1000 / > 1000 | SME, Growth, hay Enterprise |
| Số lượng chi nhánh/văn phòng | 1 trụ sở, 3 chi nhánh | Ảnh hưởng đến phân quyền dữ liệu |
| Lĩnh vực/Ngành | Bán lẻ, Sản xuất, Dịch vụ... | Xác định domain knowledge cần chuẩn bị |
| Giai đoạn tăng trưởng | Startup / Growth / Mature | Ảnh hưởng đến độ ưu tiên giải pháp |

---

#### 1.2 Value Flow
**Mô tả:** Vẽ chuỗi giá trị (Value Chain) và cách doanh nghiệp kiếm tiền. Đây là nền tảng để hiểu quy trình nào tạo ra doanh thu trực tiếp và quy trình nào là hỗ trợ.

| Trường thông tin | Giá trị mẫu | Ghi chú |
|---|---|---|
| Nguồn thu nhập chính | Bán sản phẩm, phí dịch vụ, hoa hồng | Liệt kê tất cả các luồng doanh thu |
| Hoạt động tạo giá trị cốt lõi | Sản xuất, Phân phối, Tư vấn | Đây là nơi pain point thường xuất hiện |
| Chuỗi giá trị (Input → Process → Output) | Đơn hàng → Sản xuất → Giao hàng | Vẽ dạng flowchart nếu phức tạp |
| Khách hàng cuối (End Customer) | Doanh nghiệp vừa miền Nam | Ai đang trả tiền cho dịch vụ |
| Điểm tiếp xúc khách hàng chính | Zalo, Email, Gặp trực tiếp | Kênh nào đang tạo ra giao dịch |

---

#### 1.3 Domain Knowledge
**Mô tả:** Xây dựng vốn thuật ngữ và hiểu biết về ngành trước khi gặp khách hàng. Nếu BA dùng sai từ chuyên ngành, toàn bộ uy tín sẽ bị mất.

| Trường thông tin | Giá trị mẫu | Ghi chú |
|---|---|---|
| Thuật ngữ nghiệp vụ đặc thù | SKU, BOM, MRP (Sản xuất) | Tra cứu theo ngành trước buổi gặp |
| Quy định pháp lý liên quan | Nghị định 13/2023/NĐ-CP (PDPA) | Đặc biệt quan trọng cho ngành tài chính, y tế |
| Quy chế/chính sách nội bộ phổ biến ngành | Chính sách hoa hồng đại lý | Hiểu để không đề xuất giải pháp vi phạm |
| Đặc thù vận hành theo mùa | Tháng 1-2 là đỉnh điểm đặt hàng | Ảnh hưởng đến thiết kế khả năng mở rộng |
| Đối thủ cạnh tranh và benchmark | Doanh nghiệp X đang dùng SAP | Giúp định vị giải pháp phù hợp |

---

#### 1.4 End-to-End Processes
**Mô tả:** Liệt kê đầy đủ các quy trình chuẩn theo cấu trúc Trigger → Steps → End State. Đây là phần cốt lõi nhất — mỗi quy trình sau này sẽ trở thành một luồng nghiệp vụ trong hệ thống.

> Format mỗi quy trình: `[Trigger] → [Bước 1: Actor - Hành động] → ... → [End State]`

| Trường thông tin | Giá trị mẫu | Ghi chú |
|---|---|---|
| Tên quy trình | Quy trình Duyệt đề xuất mua hàng | Đặt tên ngắn gọn, dùng làm định danh |
| Trigger (Sự kiện kích hoạt) | Nhân viên gửi form đề xuất mua | Ai làm gì để bắt đầu? |
| Actor tham gia | Nhân viên, Trưởng phòng, Kế toán, GĐ | Danh sách tất cả vai trò tham gia |
| Các bước thực hiện (tuần tự) | Điền form → Trình duyệt → Phê duyệt → Thanh toán | Số bước, thứ tự |
| Điều kiện rẽ nhánh | Nếu > 10tr: cần GĐ ký; < 10tr: TP ký | Logic điều kiện phân luồng |
| Thông tin/Dữ liệu nhập tại mỗi bước | Mã hàng, Số lượng, Nhà cung cấp | **Đây là nguồn xác định field trong ERD** |
| End State (Trạng thái kết thúc) | Đơn mua được duyệt và chuyển kho | Kết quả mong đợi khi hoàn thành |
| Thời gian thực hiện trung bình | 2–3 ngày làm việc | Baseline đo lường cải tiến |
| Ngoại lệ thường gặp | Sếp vắng, không ai duyệt thay | Pain point phổ biến |

---

#### 1.5 Roles & Responsibilities
**Mô tả:** Xác định chính xác ai làm gì, ai có quyền quyết định, và ai sẽ là người dùng hệ thống hàng ngày. Thiếu bước này dẫn đến thiết kế phân quyền sai.

| Role / Bộ phận | Chức danh cụ thể | Ra quyết định? | Người vận hành? | Sẽ hưởng lợi? | Có thể phản đối? | Ghi chú |
|---|---|---|---|---|---|---|
| Ban Giám Đốc | CEO, GĐ Điều hành | ✅ Chính | ❌ | ✅ (Dashboard) | 🟡 (nếu phức tạp) | Cần báo cáo nhanh, không cần thao tác nhiều |
| Quản lý cấp trung | Trưởng phòng, Giám Sát | ✅ Một phần | ✅ | ✅ | 🟡 | Người dùng chính, cần UX tốt |
| Nhân viên vận hành | Nhân viên kinh doanh, Kho | ❌ | ✅ Hàng ngày | ✅ (nếu đơn giản) | 🔴 (nếu thêm bước) | Thiết kế form cần cực kỳ đơn giản |
| Kế toán | Kế toán trưởng, Nhân viên KT | ❌ | ✅ | ✅ | 🟡 | Cần xuất báo cáo, tích hợp số liệu |

---

#### 1.6 Dự đoán Pain Points
**Mô tả:** Dựa trên quy mô và ngành, dự đoán các loại điểm nghẽn thường gặp trước khi gặp khách hàng. Điều này giúp BA đặt câu hỏi Socratic chính xác hơn, nhanh chóng khai thác vấn đề thực sự.

| Loại Pain | Dự đoán Pain Point | Quy mô thường gặp | Mức độ ưu tiên dự kiến |
|---|---|---|---|
| Operational | Quy trình thủ công, mất thời gian xử lý đơn | SME, Growth | 🔴 High |
| Visibility | Leader không có báo cáo thời gian thực | Tất cả quy mô | 🟡 Medium |
| Data Coordination | Dữ liệu phân tán (Excel, Zalo, giấy tờ) | SME < 200 người | 🔴 High |
| Growth | Không scale được khi tăng nhân sự/chi nhánh | Growth stage | 🟡 Medium |
| Compliance | Thiếu audit trail, khó kiểm soát nội bộ | Enterprise | 🟡 Medium |

---

#### 1.7 Current Systems
**Mô tả:** Kiểm kê toàn bộ công cụ đang sử dụng và đánh giá rủi ro. Đây là cơ sở để thiết kế migration strategy và tránh đề xuất giải pháp xung đột với hệ thống hiện tại.

| Nghiệp vụ | Công cụ đang dùng | Người dùng chính | Rủi ro dữ liệu | Ghi chú tích hợp |
|---|---|---|---|---|
| Quản lý đơn hàng | Excel + Zalo | Kinh doanh | Mất dữ liệu, không audit trail | Cần migration hoặc kết nối API |
| Chấm công | Máy chấm tay + Excel | HR | Sai sót tính công, khó tổng hợp | Xem xét tích hợp Lark Attendance |
| Phê duyệt nội bộ | Email + giấy ký | Tất cả | Mất hồ sơ, chậm xử lý | Lark Approval phù hợp |
| Kế toán | MISA, Fast | Kế toán | Hệ thống legacy, cần giữ nguyên | Chỉ xuất dữ liệu sang, không thay thế |
| Giao tiếp nội bộ | Zalo Group | Tất cả | Lẫn lộn cá nhân/công việc | Migrate sang Lark Messenger |

---

#### 1.8 Constraints
**Mô tả:** Xác định các ràng buộc cứng không thể thay đổi. Thiết kế giải pháp vượt quá constraints sẽ dẫn đến thất bại triển khai dù giải pháp đúng về kỹ thuật.

| Loại ràng buộc | Chi tiết | Mức độ cứng | Ghi chú |
|---|---|---|---|
| Ngân sách | Tối đa X triệu/năm (bao gồm license + implementation) | 🔴 Cứng | Ảnh hưởng đến gói Lark đề xuất |
| Timeline | Go-live trước ngày DD/MM/YYYY | 🔴 Cứng | Xác định scope MVP |
| Nhân sự IT nội bộ | Không có / Có 1 IT generalist | 🟡 Mềm | Ảnh hưởng đến độ phức tạp vận hành |
| Bảo mật dữ liệu | Không lưu cloud nước ngoài / Cần on-premise | 🔴 Cứng | Lark on-premise vs Cloud |
| Hệ sinh thái hiện tại | Đang dùng Lark Basic / Pro / Enterprise | 🔴 Cứng | Inventory feature theo gói |
| Kháng thay đổi (Change Resistance) | Nhân viên lớn tuổi, quen làm giấy | 🟡 Mềm | Cần đào tạo, UI đơn giản |

---

#### 1.9 Discovery Questions
**Mô tả:** Chuẩn bị bộ câu hỏi Socratic để phỏng vấn stakeholder. Câu hỏi tốt không hỏi "Anh muốn gì?" mà hỏi "Điều gì xảy ra khi...?", "Ai quyết định khi...?", "Mất bao lâu để...?".

| Nhóm câu hỏi | Câu hỏi mẫu | Mục tiêu khai thác |
|---|---|---|
| Về quy trình hiện tại | "Anh/Chị có thể walk me through một ngày làm việc điển hình?" | Hiểu quy trình thực tế, không phải quy trình trên giấy |
| Về nỗi đau | "Điều gì tốn nhiều thời gian nhất trong tuần của anh/chị?" | Xác định pain point ưu tiên cao |
| Về quyết định | "Ai là người cuối cùng phê duyệt [X]? Điều gì xảy ra nếu họ vắng mặt?" | Mapping phân quyền thực tế |
| Về dữ liệu | "Khi cần báo cáo [X], anh/chị lấy dữ liệu từ đâu? Mất bao lâu?" | Xác định nguồn dữ liệu và khoảng cách với nhu cầu |
| Về kỳ vọng | "Nếu 3 tháng nữa hệ thống hoạt động tốt, anh/chị kỳ vọng thấy điều gì khác biệt?" | Calibrate definition of success |
| Về ràng buộc | "Có điều gì chúng ta tuyệt đối không được thay đổi không?" | Phát hiện constraints ẩn |

---

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
