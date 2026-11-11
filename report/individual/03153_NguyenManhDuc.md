# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603153
- Ngày / CVAT local: 11/11 / CVAT local
- Công cụ đã dùng: SAM2

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp


| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | [easy_semantic.zip](../../submissions/easy_semantic.zip) |3 / 3 |  |
| medium_instance | [medium_instance.zip](../../submissions/medium_instance.zip) |3 / 3 |  |
| hard_panoptic | [hard_panoptic.zip](../../submissions/hard_panoptic.zip) |2 / 2 |  |
| cp1_holes | [cp1_holes.zip](../../submissions/cp1_holes.zip)| 1 / 1 |  |
| cp2_slice | [cp2_slice.zip](../../submissions/cp2_slice.zip) | 1 / 1 |  |
| cp3_thin | [cp3_thin.zip](../../submissions/cp3_thin.zip) |1 / 1 |  |
| cp4_curb | [cp4_curb.zip](../../submissions/cp4_curb.zip) | 1 / 1 |  | 
  cp5_occlusion |  [cp5_occlusion.zip](../../submissions/cp5_occlusion.zip) |1 / 1 |  |
| cp6_coverage | [cp6_coverage.zip](../../submissions/cp6_coverage.zip) | 1 / 1 |  |
| **Tổng tối đa** | | | **100** |



## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: ảnh 000000181542.jpg object đầu tiên vẽ là 1 người ở vị trí giữa ảnh
- Class và quy tắc tôi dùng để chọn biên: class person và vẽ theo đường viền phần cơ thể và quần áo nhìn thấy, dừng ở chỗ tiếp giáp với nền

- Nếu không dùng gợi ý: không dùng; vì người phụ nữ giữa ảnh rất dễ quan sát

## 3. Một lỗi tôi tìm thấy và sửa



- Task/ảnh/vùng: Job 10, ảnh `000000336232.jpg`, khi dùng Segment Anything để tạo mask cho một người (class `person`)
- Lỗi thuộc loại: Khác – lỗi kết nối công cụ AI.
- Bằng chứng tôi nhìn thấy: Sau khi  bấm Interact, CVAT hiện “Interaction error occurred” và “Network is unreachable” ở địa chỉ `host.docker.internal:65343`. Lần thao tác đó không tạo được mask.
- Quy tắc và hành động sửa: thử tải lại Job. Khi lỗi vẫn xuất hiện, kiểm tra kết nối giữa CVAT và SAM. Sau khi cấu hình lại đường kết nối qua Nuclio, SAM đã trả kết quả với ảnh thử.
- Sau sửa đã Save và export lại chưa? đã save và export lại



## 4. Ba ca chưa chắc hoặc đã cân nhắc



| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| Medium · 000000181542.jpg|Phần thân xe bên trái và bánh xe lộ ra bên phải là cùng một xe bị che  | So hướng xe và vị trí bánh trước so với thân. Người phụ nữ đứng giữa hai phần nhìn thấy| Nếu xác định là cùng xe, giữ một instance motorcycle cho các phần nhìn thấy và chừa vùng người phụ nữ che. |
| Hard · 000000460147.jpg | Gộp cả cụm thành một mask truck, hay tách xe tải và từng ô tô đang được chở? | Nhìn ở đuôi xe thấy ô tô nằm trên hai tầng. Mỗi chiếc có thân và kính riêng, còn khung chở thuộc xe tải. | Tạo một instance truck cho phần xe tải nhìn thấy và một instance car cho từng ô tô xác định được. |
| Hard · 000000350023.jpg| Nhãn traffic light bao gồm cả thanh ngang đỡ đèn, hay chỉ gồm từng cụm đèn? | Có hai điểm sáng xanh ở hai vị trí khác nhau trên cùng thanh ngang. Danh sách lớp Hard có traffic light nhưng không có pole. | tách hai cụm đèn thành hai instance traffic light. Phần thanh ngang đỡ đèn có cần đưa vào mask không ạ? |
