# Acceptance Criteria & Definition of Done
## Dự án: Mượn sách trực tuyến

> **Lưu ý:** Các quy tắc chưa được nêu trong User Story được ghi là *giả định* để có thể viết AC kiểm thử được. Cần PO xác nhận trước khi triển khai chính thức.

---

## 1. Story 1 — Đặt mượn online một cuốn sách đang có sẵn

**User Story:** Là một độc giả, tôi muốn đặt mượn online một cuốn sách đang có sẵn để tôi không mất công đến thư viện rồi mới biết sách đã có người mượn.

### Bảng Acceptance Criteria

| AC# | Loại | Given | When | Then |
|---|---|---|---|---|
| S1-AC1 | Happy path | Độc giả đang sử dụng hệ thống và cuốn sách còn bản có thể cho mượn | Độc giả chọn đặt mượn cuốn sách đó | Hệ thống xác nhận đặt mượn thành công và hiển thị thông tin sách cùng thời hạn giữ sách 48 giờ |
| S1-AC2 | Negative | Cuốn sách không còn bản nào có thể cho mượn | Độc giả chọn đặt mượn cuốn sách đó | Hệ thống từ chối yêu cầu và thông báo sách hiện không có sẵn để đặt mượn |
| S1-AC3 | Edge | Chỉ còn đúng 1 bản có thể cho mượn và bản đó vẫn chưa được đặt hoặc cho người khác mượn | Độc giả chọn đặt mượn cuốn sách đó | Hệ thống xác nhận đặt mượn thành công và chỉ ghi nhận một yêu cầu giữ bản sách đó |
| S1-AC4 | Edge | Cuốn sách đã được một độc giả khác đặt giữ hoặc mượn trước khi yêu cầu hiện tại được xử lý | Độc giả chọn đặt mượn cuốn sách đó | Hệ thống từ chối yêu cầu và thông báo sách không còn sẵn có |

### Câu hỏi làm rõ cho PO
1. Độc giả có cần đăng nhập hoặc đáp ứng điều kiện thẻ thư viện nào trước khi đặt mượn không?
2. “Có sẵn” nghĩa là còn bản sách chưa được mượn, hay cũng phải loại trừ các bản đang được người khác giữ chỗ?
3. Thời hạn 48 giờ bắt đầu từ thời điểm nào: lúc đặt mượn thành công hay lúc thư viện xác nhận sách đã sẵn sàng?

---

## 2. Story 2 — Nhận thông báo khi sách đặt trước đã có sẵn

**User Story:** Là một độc giả, tôi muốn nhận thông báo khi sách tôi đặt trước đã có sẵn để tôi kịp đến nhận sách trước khi hết thời gian giữ chỗ.

### Giả định
- “Đặt trước” là một yêu cầu đã được ghi nhận trước đó.
- Kênh thông báo và nội dung cụ thể cần được PO xác nhận. Trong AC dưới đây, “thông báo” là thông báo được hiển thị qua kênh mà thư viện hỗ trợ.

### Bảng Acceptance Criteria

| AC# | Loại | Given | When | Then |
|---|---|---|---|---|
| S2-AC1 | Happy path | Độc giả có yêu cầu đặt trước hợp lệ và sách chuyển sang trạng thái có sẵn để nhận | Thư viện xác nhận sách đã sẵn sàng | Độc giả nhận được thông báo cho biết sách đã có sẵn và thời hạn giữ chỗ 48 giờ |
| S2-AC2 | Negative | Yêu cầu đặt trước của độc giả chưa có sách sẵn sàng để nhận | Hệ thống kiểm tra điều kiện gửi thông báo | Độc giả không nhận thông báo “sách đã sẵn sàng” khi sách chưa có sẵn |
| S2-AC3 | Edge | Sách đã sẵn sàng và thông báo đã được gửi cho yêu cầu đặt trước đó | Trạng thái sách được cập nhật lại nhưng không phát sinh một lượt sẵn sàng mới | Hệ thống không gửi lặp lại cùng một thông báo sẵn sàng cho cùng một lượt giữ chỗ |
| S2-AC4 | Edge | Sách đã sẵn sàng để nhận nhưng thời hạn giữ chỗ 48 giờ đã kết thúc | Độc giả mở thông tin yêu cầu đặt trước | Hệ thống hiển thị rằng thời hạn giữ chỗ đã hết và không thể coi yêu cầu đó là lượt giữ chỗ còn hiệu lực |

### Câu hỏi làm rõ cho PO
1. Thông báo được gửi qua kênh nào: thông báo trong ứng dụng, email hay SMS?
2. Thời hạn 48 giờ bắt đầu từ lúc sách chuyển sang sẵn sàng hay lúc thông báo được gửi thành công?
3. Nếu gửi thông báo thất bại, hệ thống có thử gửi lại không? Nếu có, thử lại bao nhiêu lần?

---

## 3. Story 3 — Giới hạn số sách một độc giả được mượn cùng lúc

**User Story:** Là một thủ thư, tôi muốn giới hạn số sách một độc giả được mượn cùng lúc để tránh tình trạng một người giữ hết sách.

### Giả định nghiệp vụ
- Tạm giả định mỗi độc giả được mượn tối đa **5 cuốn sách đang mượn cùng lúc**.
- Sách đang được giữ chỗ nhưng chưa nhận **chưa được tính** vào giới hạn mượn; cần PO xác nhận quy tắc này.
- “Đang mượn” là sách đã được giao cho độc giả và chưa được ghi nhận trả.

### Bảng Acceptance Criteria

| AC# | Loại | Given | When | Then |
|---|---|---|---|---|
| S3-AC1 | Happy path | Độc giả đang mượn 4 cuốn và chưa có vi phạm điều kiện mượn khác | Thủ thư ghi nhận cho độc giả mượn thêm 1 cuốn | Hệ thống chấp nhận việc mượn và số sách đang mượn của độc giả là 5 |
| S3-AC2 | Negative | Độc giả đang mượn 5 cuốn | Thủ thư ghi nhận cho độc giả mượn thêm 1 cuốn | Hệ thống từ chối việc mượn thêm và thông báo độc giả đã đạt giới hạn 5 cuốn |
| S3-AC3 | Edge | Độc giả đang mượn 6 cuốn do dữ liệu cũ hoặc ngoại lệ trước đó | Thủ thư thử ghi nhận thêm một lượt mượn | Hệ thống từ chối lượt mượn mới và hiển thị rằng độc giả đang vượt giới hạn cho phép |
| S3-AC4 | Ràng buộc nghiệp vụ | Độc giả đang mượn 5 cuốn và đã trả thành công 1 cuốn, nên còn 4 cuốn đang mượn | Thủ thư ghi nhận cho độc giả mượn thêm 1 cuốn | Hệ thống chấp nhận lượt mượn mới và số sách đang mượn trở lại là 5 |

### Câu hỏi làm rõ cho PO
1. Giới hạn chính thức là bao nhiêu cuốn mỗi độc giả? Có khác nhau theo loại thẻ hoặc nhóm độc giả không?
2. Sách đang được giữ chỗ 48 giờ có tính vào giới hạn mượn không, hay chỉ tính sách đã nhận tại quầy?
3. Sách quá hạn hoặc sách đang trong quy trình trả có được tính vào số sách đang mượn không?

---

## 4. Definition of Done (DoD) — Áp dụng chung cho mọi Product Backlog Item

Một Product Backlog Item chỉ được xem là Done khi đáp ứng tất cả tiêu chí DoD áp dụng cho nhóm.

- [ ] Mã nguồn đã được review và được chấp thuận theo quy trình của nhóm.
- [ ] Các bài kiểm thử tự động phù hợp với thay đổi đã chạy đạt; kiểm thử hồi quy liên quan không phát hiện lỗi mới.
- [ ] Các Acceptance Criteria của story đã được kiểm tra và đều đạt.
- [ ] Không còn lỗi nghiêm trọng hoặc lỗi mức cao chưa được xử lý theo ngưỡng chất lượng đã thống nhất của nhóm.
- [ ] Thay đổi đã được tích hợp vào nhánh/môi trường tích hợp chung và build thành công.
- [ ] Tài liệu liên quan đã được cập nhật nếu thay đổi ảnh hưởng đến cách sử dụng hoặc vận hành.
- [ ] Các kiểm tra chất lượng và bảo mật bắt buộc của nhóm đã đạt.
- [ ] Kết quả kiểm thử và các lỗi còn tồn tại (nếu có, không cản trở DoD) đã được ghi nhận rõ ràng.

### Ví dụ áp dụng DoD cho 3 story
- **Story 1:** AC đặt mượn đều đạt, code được review, test đạt và thay đổi được tích hợp.
- **Story 2:** AC thông báo đều đạt, kiểm thử các tình huống gửi thông báo đã chạy và thay đổi được review/tích hợp.
- **Story 3:** AC giới hạn số sách đều đạt, kiểm thử các trường hợp tại giới hạn 4, 5 và vượt 5 cuốn đã chạy đạt; code được review và tích hợp.

> DoD là tiêu chuẩn chung của nhóm, không thay thế AC riêng của từng story. Các tiêu chí cụ thể như mức độ nghiêm trọng của lỗi, phạm vi test hồi quy và quy trình triển khai cần được nhóm thống nhất.

---

## 5. Story 1 đã đạt AC nhưng code chưa được review theo DoD. Đã Done chưa?

**Chưa.** Dù Story 1 đã đáp ứng tất cả AC, code review vẫn là tiêu chí bắt buộc trong DoD của nhóm; vì vậy story chưa được công nhận là Done cho đến khi hoàn tất review và đáp ứng các tiêu chuẩn DoD còn lại.
