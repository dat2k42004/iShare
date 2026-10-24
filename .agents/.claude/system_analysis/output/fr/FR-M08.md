---
module: M08
ten_module: Moderation
ma_tai_lieu: FR-M08
phien_ban: 1.7
trang_thai: Đã chốt
ngay: 2026-10-24
tac_gia: Phạm Văn Đức
moc_nguon: DEC-271, QA-477, ISS-415, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M08 Moderation

| Mã tài liệu | FR-M08 |
|---|---|
| Dự án | iShare |
| Module | M08 — Moderation |
| Trạng thái | Đã chốt |
| Phiên bản | 1.7 |
| Ngày | 2026-10-24 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Kiểm duyệt giữ cho nội dung trên iShare phù hợp với học sinh THPT. Người dùng báo cáo bài viết, bình luận, người dùng
hoặc nhóm vi phạm; Mod và Admin xử lý các báo cáo theo hàng chờ, ẩn nội dung vi phạm, cảnh cáo và ban người vi phạm.
AI hỗ trợ quét bình luận và tự cảnh cáo khi độ tin cậy cao, nhưng không bao giờ tự ban: quyết định nặng luôn do con người.
Mọi thao tác kiểm duyệt được ghi vào nhật ký để minh bạch và để xét khiếu nại.

### 1.2 Phạm vi

**Trong phạm vi:**

- Báo cáo: người dùng đã đăng nhập báo cáo bài viết, bình luận, người dùng, nhóm; lý do riêng theo từng loại đối tượng;
  bằng chứng (tối đa 3 ảnh) và mô tả (bắt buộc khi chọn "Khác").
- Vụ báo cáo và hàng chờ: gom các báo cáo đang mở về cùng một đối tượng thành một vụ; điểm ưu tiên của vụ; Mod "Nhận xử
  lý" để giữ vụ, tự nhả khi không thao tác; lịch sử báo cáo của đối tượng.
- Xử lý vụ báo cáo: kết luận có vi phạm hoặc không, kèm lý do do Mod tự xác định; ẩn bài, ẩn bình luận; cảnh cáo hoặc ban
  người vi phạm; Mod, Admin xem nội dung đã xóa, tự ẩn của đối tượng trong ngữ cảnh báo cáo.
- Xét bài viết bị gắn cờ sau khi sửa (giữ bài hoặc ẩn bài).
- Nội dung thông báo kết quả xử lý, tách theo người nhận: người báo cáo chỉ biết kết quả chung; người vi phạm biết lý do,
  mức xử lý và đường dẫn khiếu nại.
- Quét AI bình luận sau khi đăng, kích hoạt theo tốc độ trả lời trong luồng; bình luận bị AI gắn cờ được ẩn và đưa vào
  hàng chờ cho Mod.
- Cảnh cáo: AI tự cảnh cáo khi độ tin cậy cao, đưa Mod quyết khi ở mức trung bình; Mod cảnh cáo khi xử lý báo cáo. Ba mức
  LIGHT, MEDIUM, HEAVY; thời gian thử thách, tự giảm mức khi hết thời gian thử thách; hạn chế theo mức; trạng thái cảnh
  cáo riêng tư, người dùng xem được mức của mình. Mod, Admin bỏ cảnh cáo do AI ra.
- Ban: ban tạm thời tự leo thang theo số lần bị ban, ban vĩnh viễn thủ công; người đang ở mức HEAVY vi phạm tiếp thì chuyển
  sang ban; gỡ ban. Ban luôn do Mod hoặc Admin.
- Nhật ký kiểm duyệt: nội dung ghi; quyền xem (Admin toàn bộ, Mod của mình, ngoại lệ khi xét khiếu nại); giữ vĩnh viễn.
- Chỉ số báo cáo sai/ác ý cho Mod tham khảo; không tự phạt người báo cáo.
- Xử lý nhóm bị báo cáo: Ẩn nhóm, Khóa nhóm và mở khóa nhóm (mở rộng phạm vi đã được chấp nhận).
- Hành vi của M08 khi công tắc AI hoặc công tắc Moderation tắt (chỉ còn kiểm duyệt thủ công) và khi AI lỗi lúc quét bình
  luận.

**Ngoài phạm vi:**

- Quét bài trước khi đăng, quét lại khi sửa hoặc khi hiện lại bài tự ẩn, hàng chờ duyệt bài chờ đăng (đăng hoặc từ chối),
  khóa bài, chặn tạo bài theo mức cảnh cáo — M03 Post & Content.
- Hiển thị bình luận bị ẩn trong luồng, chặn bình luận ở mức HEAVY, nút báo cáo đặt trên bình luận — M04 Comment.
  Chủ nội dung xem lại nội dung của mình đã bị xử lý — M03, M04.
- Ghi thao tác Tag, Topic của Mod (M05 dùng nhật ký kiểm duyệt của M08). Giảm hạng tìm kiếm nội dung của người ở mức
  HEAVY — M06 Search.
- Kênh gửi thông báo (trong ứng dụng, email) — M07 Notification.
- Khiếu nại cảnh cáo, ban, bài bị gỡ; hàng chờ khiếu nại; đảo ngược xử lý khi khiếu nại thành công — M09 Appeal.
- Đổi vai trò, Mod bị ban thì mất vai trò Mod, công tắc AI, nhật ký thao tác Admin — M10 Admin Panel.
- Trạng thái tài khoản BANNED, màn hình tài khoản bị khóa, tự về ACTIVE khi ban tạm thời hết hạn — M01 Authentication &
  Account.
- Kiểm duyệt cấp nhóm (Group Mod, cổng duyệt bài của nhóm), đăng ẩn danh — M11 Group.
- Trừ điểm khi nội dung bị gỡ vì vi phạm, loại người ở mức HEAVY hoặc bị ban khỏi bảng xếp hạng, nhãn "Tài khoản đã bị
  khóa" — M12 Gamification.
- Gọi AI, thời gian chờ và thử lại, nhóm vi phạm AI phát hiện được, nhật ký quyết định AI, vòng phản hồi đánh giá AI —
  M13 AI Layer.
- Thống kê kiểm duyệt — M15 Analytics & Stats.
- Đã quyết không làm: báo cáo tin nhắn chat ở MS1; AI tự ban; tự động phạt người báo cáo sai; Mod, Admin gỡ avatar, bio;
  gỡ đánh dấu Accepted Answer (MS1 không có Accepted Answer); khách báo cáo; cấu hình thời hạn, ngưỡng kiểm duyệt qua giao
  diện; ngưỡng AI thay đổi theo mức cảnh cáo; thao tác suspend, vô hiệu hóa tài khoản người khác; xử lý (ẩn, cảnh cáo, ban)
  ngoài vụ báo cáo; rút, sửa báo cáo đã gửi; bỏ ẩn nhóm.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Báo cáo | Một lần người dùng đã đăng nhập tố cáo một đối tượng vi phạm, gồm lý do, mô tả (tùy chọn) và bằng chứng (tùy chọn). |
| Đối tượng bị báo cáo | Một bài viết, một bình luận, một người dùng hoặc một nhóm mà báo cáo nhắm tới; xác định bằng loại đối tượng và chính đối tượng đó. |
| Người báo cáo | Người dùng đã gửi một báo cáo. |
| Người bị báo cáo | Tác giả của bài viết, bình luận bị báo cáo, chính người dùng bị báo cáo, hoặc Owner của nhóm bị báo cáo. |
| Lý do báo cáo | Lựa chọn người báo cáo chọn từ danh sách riêng của loại đối tượng (BR-M08-02). |
| Bằng chứng | Ảnh người báo cáo đính kèm báo cáo (BR-M08-03). |
| Vụ báo cáo (vụ) | Tập các báo cáo đang mở về cùng một đối tượng. Mỗi báo cáo trong vụ giữ nguyên dữ liệu riêng của nó. |
| Hàng chờ báo cáo | Danh sách các vụ đang mở mà Mod, Admin xử lý, xếp theo điểm ưu tiên. |
| Mức nặng của lý do | Trọng số gắn với mỗi lý do báo cáo, dùng để tính điểm ưu tiên: 10 (nặng), 5 (trung bình), 2 (nhẹ) theo BR-M08-06. |
| Điểm ưu tiên | Con số quyết định thứ tự của vụ trong hàng chờ (BR-M08-06). |
| Nhận xử lý | Thao tác Mod, Admin giữ một vụ cho riêng mình; trong lúc giữ, người khác không xử lý được vụ đó. |
| Kết luận vụ | Việc Mod, Admin đang giữ vụ đóng vụ với một trong hai kết quả: Có xử lý (đã xử lý nội dung hoặc người vi phạm) hoặc Bác bỏ (không phát hiện vi phạm), kèm lý do kết luận. |
| Lý do kết luận | Lý do do Mod, Admin tự xác định khi kết luận vụ; không bắt buộc trùng lý do người báo cáo đã chọn. |
| Lịch sử báo cáo của đối tượng | Các vụ đã kết luận trước đó về cùng một đối tượng, kèm kết luận. |
| Chỉ số tập trung | Chỉ số tham khảo về một người báo cáo, cho biết họ có dồn báo cáo bị bác bỏ vào cùng một đối tượng hay không (BR-M08-19). |
| Điểm quét | Con số từ 0 đến 1 mà việc quét AI trả về cho một bài viết hoặc bình luận: điểm cao nhất trong bốn nhóm vi phạm AI phát hiện; điểm càng cao càng có khả năng vi phạm. |
| Luồng bình luận | Một bình luận gốc cùng mọi trả lời thuộc nó (định nghĩa ở M04). |
| Tốc độ trả lời | Số trả lời mới trong một luồng bình luận trong một khoảng thời gian trượt. |
| Ngưỡng tốc độ | Số trả lời trong một luồng trong khoảng thời gian trượt mà khi đạt tới thì kích hoạt việc quét AI luồng; giá trị chưa chốt (TBD-M08-04). |
| Đã quét với nội dung hiện tại | Bình luận đã được quét AI sau lần sửa nội dung gần nhất (hoặc sau khi đăng, nếu chưa sửa). |
| Trạng thái kiểm duyệt của bài | Bình thường, Bị gắn cờ, Bị ẩn (định nghĩa ở M03; FR-M03 gọi Bị ẩn là "Bị Mod ẩn" để tách khỏi bài Tự ẩn). Bị ẩn là trạng thái "Mod gỡ bài". |
| Trạng thái kiểm duyệt của bình luận | Bình thường, Bị ẩn (định nghĩa ở M04). |
| Nội dung bị gắn cờ | Bài viết ở trạng thái Bị gắn cờ, hoặc bình luận bị AI ẩn với điểm quét từ 0,5 đến dưới 0,9, đang chờ Mod xét trong một vụ. |
| Cảnh cáo | Một lần người dùng bị ghi nhận vi phạm, do AI tự ra hoặc do Mod, Admin ra. |
| Số lần cảnh cáo | Số cảnh cáo đang được tính của một người dùng; quyết định mức cảnh cáo. |
| Mức cảnh cáo | Sạch (0 lần), LIGHT (1–2 lần), MEDIUM (3–4 lần), HEAVY (5–6 lần). |
| Thời gian thử thách | Khoảng thời gian gắn với mức cảnh cáo hiện tại (LIGHT 7 ngày, MEDIUM 10 ngày, HEAVY 15 ngày), tính đủ N × 24 giờ kể từ lúc cảnh cáo hoặc lúc giảm mức; hạn chế của mức áp dụng trong khoảng này. |
| Vi phạm khi đang HEAVY | Lần vi phạm thứ 7 trở lên: người dùng đang ở mức HEAVY lại bị xác định vi phạm. |
| Ban | Khóa tài khoản do Mod, Admin quyết định; tài khoản chuyển sang BANNED (M01). |
| Ban tạm thời | Ban có thời hạn, ra bằng thao tác "Ban"; thời hạn theo số lần đã bị ban (BR-M08-34). "Suspend" trong draft là ban tạm thời. |
| Ban vĩnh viễn | Ban không có thời hạn; ra bằng thao tác "Ban vĩnh viễn" hoặc là lần ban thứ 3 trở đi của thao tác "Ban". |
| Số lần đã bị ban | Số ban trước đó của người dùng, dùng để tính thời hạn của thao tác "Ban": gồm mọi ban từng có hiệu lực, kể cả ban được gỡ sớm và ban vĩnh viễn thủ công; không gồm ban bị lật do khiếu nại. |
| Gỡ ban | Thao tác Mod, Admin kết thúc một ban đang hiệu lực; tài khoản về ACTIVE. |
| Thao tác kiểm duyệt | Thao tác của Mod, Admin hoặc AI được ghi vào nhật ký kiểm duyệt (BR-M08-39). |
| Nhật ký kiểm duyệt | Danh sách các thao tác kiểm duyệt, mỗi dòng gồm người làm, loại thao tác, đối tượng, lý do, thời điểm. |
| Công tắc AI tổng, công tắc Moderation | Hai công tắc ở M10. Công tắc Moderation chỉ có tác dụng khi công tắc AI tổng bật; tắt một trong hai thì không quét, không tự cảnh cáo. |
| Hằng số chính sách | Thời gian thử thách, thời hạn ban, các ngưỡng kiểm duyệt; không cấu hình qua giao diện. |
| Giờ Việt Nam | Múi giờ Asia/Ho_Chi_Minh (UTC+7), không đổi giờ mùa hè; mọi ranh giới ngày và hiển thị thời gian tính theo múi giờ này. |
| Mục do AI tạo | Một báo cáo trong vụ có người báo cáo là "Hệ thống (AI)", do hệ thống tạo khi AI phát hiện nội dung cần Mod xem; lý do là nhóm vi phạm AI phát hiện; tính như một báo cáo. |
| Yêu cầu ban | Đánh dấu trên một vụ khi người đang ở mức HEAVY vi phạm tiếp; Mod, Admin quyết và chọn "Ban". |
| Trạng thái kiểm duyệt của nhóm | Bình thường, Bị khóa, Bị ẩn. Do Mod, Admin quyết khi xử lý vụ về nhóm; M11 áp lên cách nhóm hiển thị. |
| Ẩn nhóm | Thao tác chuyển nhóm sang Bị ẩn: nhóm và mọi nội dung không hiện với ai, kể cả thành viên và Owner; không có bỏ ẩn. |
| Khóa nhóm | Thao tác chuyển nhóm sang Bị khóa: nhóm vẫn hiện, nội dung cũ vẫn đọc được, nhưng đăng bài, bình luận, upvote, bình chọn, tham gia, mời đều bị chặn; Mod, Admin mở khóa được. |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |
| BR | Business Rule — quy tắc nghiệp vụ |
| AI | Trí tuệ nhân tạo; trong tài liệu này là dịch vụ AI kiểm duyệt bên thứ ba (M13) |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-271, QA-477, ISS-415, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Ban, gỡ ban làm đổi trạng thái tài khoản; màn hình tài khoản bị khóa; nhật ký kiểm duyệt giữ khi tài khoản bị xóa. |
| M02 User Profile | Xử lý báo cáo người dùng không gồm gỡ avatar, bio; mức cảnh cáo không hiện trên hồ sơ. |
| M03 Post & Content | Trạng thái kiểm duyệt của bài; bài bị gắn cờ sau khi quét lại; hạn chế tạo bài theo mức cảnh cáo; bài đã xóa, tự ẩn xem được trong báo cáo. |
| M04 Comment | Trạng thái kiểm duyệt của bình luận; bình luận bị ẩn; hạn chế bình luận ở mức HEAVY; bình luận đã xóa xem được trong báo cáo. |
| M05 Topic & Tag | Thao tác Tag, Topic của Mod ghi vào nhật ký kiểm duyệt. |
| M06 Search | Nội dung của người ở mức HEAVY bị giảm hạng tìm kiếm. |
| M07 Notification | Gửi thông báo kết quả xử lý, cảnh cáo, ban, gỡ ban. |
| M09 Appeal | Khiếu nại cảnh cáo, ban, bài bị gỡ; đảo ngược xử lý; Mod xem nhật ký của Mod khác khi xét khiếu nại. |
| M10 Admin Panel | Công tắc AI và Moderation; phân quyền Admin, Mod; nhật ký thao tác Admin. |
| M11 Group | Báo cáo nhóm; kiểm duyệt cấp nhóm chồng lên kiểm duyệt hệ thống. |
| M12 Gamification | Trừ điểm khi nội dung bị gỡ; loại người ở mức HEAVY hoặc bị ban khỏi bảng xếp hạng. |
| M13 AI Layer | Điểm AI kiểm duyệt, ngưỡng, xử lý khi AI lỗi. |
| M15 Analytics & Stats | Thống kê báo cáo, cảnh cáo, ban, gỡ ban; mức cảnh cáo của tài khoản. |
| M16 Chat & Messaging | Tin nhắn chưa báo cáo được ở MS1. |
| M14 Feed & Discovery | Mức cảnh cáo không hiện và không làm bài bị loại hay hạ điểm ở feed; báo cáo bài hiện trong feed. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Không báo cáo được, không có thao tác nào trong module này. |
| User | Người dùng đã đăng nhập. Báo cáo bài viết, bình luận, người dùng, nhóm của người khác; xem mức cảnh cáo của chính mình. |
| Mod | Có quyền của User. Xem hàng chờ, nhận xử lý và kết luận vụ báo cáo; trong vụ đang giữ: ẩn bài viết, bình luận, ẩn hoặc khóa nhóm, cảnh cáo, ban người dùng không có vai trò Mod, Admin; bỏ cảnh cáo do AI ra; gỡ ban, mở khóa nhóm; xem nhật ký các vụ mình đã xử lý. Không thấy, không nhận vụ nhắm vào chính mình. |
| Admin | Có các quyền của Mod; cảnh cáo, ban tài khoản Mod; xem toàn bộ nhật ký kiểm duyệt. Tài khoản Admin không bị cảnh cáo, ban; Admin không thấy, không nhận vụ nhắm vào chính mình. |
| Người bị báo cáo | Vai trò theo ngữ cảnh: tác giả của bài, bình luận bị báo cáo, người dùng bị báo cáo, hoặc Owner của nhóm bị báo cáo; nhận thông báo kết quả chi tiết khi vụ Có xử lý. |
| Người báo cáo | Vai trò theo ngữ cảnh: người dùng đã gửi một báo cáo trong vụ, hoặc "Hệ thống (AI)" với mục do AI tạo; người dùng chỉ nhận kết quả chung. |
| Hệ thống | Quét AI luồng bình luận, tạo mục do AI phát hiện trong hàng chờ, tự cảnh cáo bằng AI, tự nhả vụ, giảm mức cảnh cáo khi hết thời gian thử thách, ghi nhật ký. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Báo cáo bài viết, bình luận, người dùng, nhóm của người khác | ✗ | ✓ | ✓ | ✓ | FR-M08-01.02, FR-M08-01.06 |
| Báo cáo nội dung của chính mình hoặc chính mình | ✗ | ✗ | ✗ | ✗ | FR-M08-01.15 |
| Rút, sửa báo cáo đã gửi | ✗ | ✗ | ✗ | ✗ | FR-M08-01.18 |
| Xem hàng chờ vụ báo cáo | ✗ | ✗ | ✓ | ✓ | FR-M08-02.01, FR-M08-02.04 |
| Nhận xử lý vụ báo cáo | ✗ | ✗ | ✓ | ✓ | FR-M08-03.01, FR-M08-03.06 |
| Xem chi tiết vụ: các báo cáo, người báo cáo, bằng chứng, lịch sử báo cáo của đối tượng, chỉ số báo cáo sai | ✗ | ✗ | ✓ | ✓ | FR-M08-04.01, FR-M08-04.03, FR-M08-04.04, FR-M08-04.08 |
| Xem nội dung đã xóa, tự ẩn, đã xóa hẳn của đối tượng trong vụ | ✗ | ✗ | ✓ | ✓ | FR-M08-04.02, FR-M08-04.07, FR-M08-04.08 |
| Kết luận vụ báo cáo | ✗ | ✗ | ✓ | ✓ | FR-M08-05.01, FR-M08-05.07 |
| Xem, nhận vụ nhắm vào chính mình (nội dung của mình, tài khoản của mình) | ✗ | ✗ | ✗ | ✗ | FR-M08-02.06, FR-M08-03.07 |
| Ẩn bài viết, bình luận của người khác (trong vụ đang giữ) | ✗ | ✗ | ✓ | ✓ | FR-M08-06.01, FR-M08-06.02, FR-M08-06.04, FR-M08-06.06 |
| Xét nội dung bị gắn cờ (giữ hoặc ẩn) | ✗ | ✗ | ✓ | ✓ | FR-M08-07.01, FR-M08-07.02, FR-M08-07.08 |
| Cảnh cáo người dùng (trong vụ đang giữ) | ✗ | ✗ | ✓ | ✓ | FR-M08-10.01, FR-M08-10.07, FR-M08-10.11 |
| Bỏ cảnh cáo do AI ra | ✗ | ✗ | ✓ | ✓ | FR-M08-11.01, FR-M08-11.02 |
| Ban (thời hạn leo thang), Ban vĩnh viễn (trong vụ đang giữ) | ✗ | ✗ | ✓ | ✓ | FR-M08-14.01, FR-M08-14.02, FR-M08-14.07, FR-M08-14.14 |
| Gỡ ban | ✗ | ✗ | ✓ | ✓ | FR-M08-15.01, FR-M08-15.04 |
| Cảnh cáo, ban tài khoản Mod | ✗ | ✗ | ✗ | ✓ | FR-M08-10.08, FR-M08-14.09 |
| Cảnh cáo, ban tài khoản Admin | ✗ | ✗ | ✗ | ✗ | FR-M08-10.09, FR-M08-14.10 |
| Ẩn nhóm, khóa nhóm (trong vụ đang giữ) | ✗ | ✗ | ✓ | ✓ | FR-M08-18.01, FR-M08-18.04, FR-M08-18.10 |
| Mở khóa nhóm | ✗ | ✗ | ✓ | ✓ | FR-M08-18.07, FR-M08-18.10 |
| Xem mức cảnh cáo, thời gian thử thách | ✗ | ✓ (của mình) | ✓ | ✓ | FR-M08-13.01, FR-M08-13.02 |
| Xem nhật ký kiểm duyệt | ✗ | ✗ | ✓ (của mình) | ✓ | FR-M08-17.01, FR-M08-17.02, FR-M08-17.05 |
| Xem thao tác của Mod khác trong nhật ký | ✗ | ✗ | ✓ (khi xét khiếu nại về thao tác đó) | ✓ | FR-M08-17.03, FR-M08-17.04 |
| Xem danh tính người báo cáo | ✗ | ✗ | ✓ | ✓ | FR-M08-04.01, FR-M08-05.06 |
| Báo cáo bài viết, bình luận, tài khoản của Admin hoặc nhóm có Owner là Admin | ✗ | ✗ | ✗ | ✗ | FR-M08-01.20 |
| Thấy, nhận vụ về bài viết, bình luận, tài khoản của một Mod khác | ✗ | ✗ | ✗ | ✓ | FR-M08-02.09, FR-M08-03.09 |

<!-- Ô nói thẳng: hàng 1 Guest ✗ và User ✓ (DEC-072 "Only logged-in users can report", QA-011, DM-1.3 "Report content");
     hàng 2–3 (DEC-191); hàng 4–8, 10–15 cột Mod, Admin (DM-1.3 "Review reports, Moderate content", DEC-090 "Shared with Mod",
     DEC-075, DM-10.2, DEC-161, DEC-180, DEC-078, QA-019 "Ban/Unban: cả MOD và ADMIN", "Override AI warn: MOD ✓, ADMIN ✓",
     DEC-080, DEC-179, DEC-184, DEC-185); "trong vụ đang giữ" (DEC-190); hàng 9, 16, 17 (DEC-189); hàng 18–19 (DEC-194);
     hàng 20 (DEC-079 "visible only to the user themselves and to mods"); hàng 21–22 (DEC-081).
     Ô suy ra: hàng 1 cột Mod, Admin (Mod, Admin cũng là người dùng đã đăng nhập; DM-1.3); cột Guest ở mọi hàng (QA-011, QA-227:
     mọi tương tác cần đăng nhập); cột User ở các hàng chỉ Mod, Admin làm (DEC-090, DM-1.3); hàng 20 cột Admin (Admin có quyền của
     Mod); hàng 23 cột Mod, Admin (mỗi báo cáo giữ người báo cáo, DEC-076; chỉ số tính theo người báo cáo, DEC-082) và cột User
     (người bị xử lý không thấy danh tính người báo cáo, DEC-179).
     Thêm ở phiên bản 1.3 (DEC-195, nói thẳng): hai hàng cuối.
-->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M08-01 | Báo cáo bài viết, bình luận, người dùng hoặc nhóm | User, Mod, Admin | Người dùng chọn "Báo cáo" trên một bài viết, bình luận, hồ sơ người dùng hoặc nhóm |
| FR-M08-02 | Xem hàng chờ vụ báo cáo | Mod, Admin | Mod hoặc Admin mở hàng chờ báo cáo |
| FR-M08-03 | Nhận và nhả vụ báo cáo | Mod, Admin | Mod hoặc Admin chọn "Nhận xử lý" một vụ; hoặc vụ đã nhận không có thao tác trong 30 phút |
| FR-M08-04 | Xem chi tiết vụ báo cáo | Mod, Admin | Mod hoặc Admin mở một vụ trong hàng chờ |
| FR-M08-05 | Kết luận vụ báo cáo | Mod, Admin | Mod hoặc Admin đang giữ vụ chọn kết luận có vi phạm hoặc không vi phạm |
| FR-M08-06 | Ẩn bài viết, bình luận vi phạm | Mod, Admin | Mod hoặc Admin chọn ẩn bài viết hoặc bình luận khi xử lý |
| FR-M08-07 | Xét nội dung bị gắn cờ | Hệ thống; Mod, Admin | Bài viết bị gắn cờ sau khi quét lại (hệ thống đưa vào vụ); Mod hoặc Admin mở một vụ có mục do AI tạo |
| FR-M08-08 | Quét AI luồng bình luận | Hệ thống | Số trả lời trong một luồng vượt ngưỡng tốc độ trong khoảng thời gian trượt |
| FR-M08-09 | Tự cảnh cáo bằng AI | Hệ thống | Kết quả quét AI một bài viết hoặc bình luận cho điểm từ 0,9 trở lên |
| FR-M08-10 | Cảnh cáo người dùng | Mod, Admin | Mod hoặc Admin chọn cảnh cáo người vi phạm khi xử lý |
| FR-M08-11 | Bỏ cảnh cáo do AI ra | Mod, Admin | Mod hoặc Admin chọn bỏ một cảnh cáo do AI tự ra |
| FR-M08-12 | Giảm mức cảnh cáo khi hết thời gian thử thách | Hệ thống | Thời gian thử thách của mức cảnh cáo hiện tại kết thúc |
| FR-M08-13 | Xem mức cảnh cáo của mình | User | Người dùng mở phần trạng thái cảnh cáo của mình |
| FR-M08-14 | Ban người dùng | Mod, Admin | Mod hoặc Admin chọn "Ban" hoặc "Ban vĩnh viễn"; hoặc người đang ở mức HEAVY vi phạm tiếp |
| FR-M08-15 | Gỡ ban | Mod, Admin | Mod hoặc Admin chọn gỡ ban một tài khoản BANNED |
| FR-M08-16 | Ghi nhật ký kiểm duyệt | Hệ thống | Mod, Admin hoặc AI vừa thực hiện một thao tác kiểm duyệt |
| FR-M08-17 | Xem nhật ký kiểm duyệt | Admin, Mod | Admin hoặc Mod mở nhật ký kiểm duyệt |
| FR-M08-18 | Ẩn, khóa và mở khóa nhóm | Mod, Admin | Mod hoặc Admin đang giữ vụ về một nhóm chọn "Ẩn nhóm" hoặc "Khóa nhóm"; hoặc chọn mở khóa một nhóm Bị khóa |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Must** (bảng MoSCoW Summary của module-registry: Must gồm M01–M10, M13;
cột MoSCoW ở dòng M08 của bảng Module List bị lệch nên không dùng). Không có yêu cầu ngoại lệ về ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M08-01 Báo cáo bài viết, bình luận, người dùng hoặc nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập báo cáo một bài viết, bình luận, người dùng hoặc nhóm vi phạm, kèm lý do, mô tả và bằng chứng.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-01.01 | Khi người dùng đã đăng nhập chọn "Báo cáo" trên một bài viết, bình luận, hồ sơ người dùng hoặc nhóm, hệ thống phải hiển thị danh sách lý do của đúng loại đối tượng đó (BR-M08-02). |
| FR-M08-01.02 | Khi người dùng gửi một báo cáo hợp lệ, hệ thống phải lưu báo cáo với người báo cáo, loại đối tượng, đối tượng, lý do, mô tả, bằng chứng và trạng thái Mở. |
| FR-M08-01.03 | Khi lưu một báo cáo về đối tượng đang có vụ Mở, hệ thống phải thêm báo cáo vào vụ đó (BR-M08-05). |
| FR-M08-01.04 | Khi lưu một báo cáo về đối tượng không có vụ Mở, hệ thống phải mở một vụ mới cho đối tượng và đưa vụ vào hàng chờ báo cáo (BR-M08-05). |
| FR-M08-01.05 | Khi thêm báo cáo vào một vụ, hệ thống phải tính lại điểm ưu tiên của vụ theo BR-M08-06. |
| FR-M08-01.06 | Nếu người chưa đăng nhập chọn báo cáo, hệ thống phải từ chối báo cáo. |
| FR-M08-01.07 | Nếu báo cáo không có lý do, hệ thống phải từ chối gửi. |
| FR-M08-01.08 | Nếu lý do là "Khác" mà mô tả trống, hệ thống phải từ chối gửi (BR-M08-04). |
| FR-M08-01.09 | Nếu người báo cáo đính kèm ảnh bằng chứng thứ tư, hệ thống phải từ chối ảnh đó (BR-M08-03). |
| FR-M08-01.10 | Nếu một ảnh bằng chứng lớn hơn 5MB hoặc có định dạng khác JPEG, PNG, WebP, hệ thống phải từ chối ảnh đó (BR-M08-03). |
| FR-M08-01.11 | Nếu đối tượng là bài viết thuộc nhóm Private mà người báo cáo không là thành viên, hệ thống phải từ chối báo cáo (BR-M08-45). |
| FR-M08-01.12 | Nếu đối tượng không còn hiển thị với người báo cáo, hệ thống phải từ chối báo cáo (BR-M08-47). |
| FR-M08-01.13 | Hệ thống phải cho báo cáo bài viết đang ở mức Khóa toàn bộ (BR-M08-45). |
| FR-M08-01.14 | Hệ thống phải cho báo cáo bình luận bất kể bình luận đã được quét AI hay chưa. |
| FR-M08-01.15 | Nếu người dùng báo cáo bài viết, bình luận hoặc tài khoản của chính mình, hệ thống phải từ chối báo cáo (BR-M08-47). |
| FR-M08-01.16 | Nếu người báo cáo đã có một báo cáo trong vụ đang Mở của cùng đối tượng, hệ thống phải từ chối báo cáo mới (BR-M08-47). |
| FR-M08-01.17 | Hệ thống phải cho người đang ở mức cảnh cáo HEAVY gửi báo cáo (BR-M08-47). |
| FR-M08-01.18 | Hệ thống phải không cho người báo cáo rút hoặc sửa báo cáo đã gửi (BR-M08-47). |
| FR-M08-01.19 | Hệ thống phải chỉ nhận một lý do cho mỗi báo cáo (BR-M08-02). |
| FR-M08-01.20 | Nếu đối tượng là bài viết, bình luận hoặc tài khoản của Admin, hoặc nhóm có Owner là Admin, hệ thống phải từ chối báo cáo (BR-M08-55). |

### 5.2 FR-M08-02 Xem hàng chờ vụ báo cáo

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin xem các vụ báo cáo đang mở, kể cả vụ do AI tạo, xếp theo mức ưu tiên.

**Lý do:** Để nhiều Mod cùng xử lý hàng chờ mà không trùng việc, các vụ được xếp theo mức ưu tiên và nhận xử lý theo cơ chế khóa vụ; không có hạn xử lý.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-02.01 | Khi Mod hoặc Admin mở hàng chờ báo cáo, hệ thống phải hiển thị mọi vụ đang Mở, gồm cả vụ do AI tạo, xếp theo điểm ưu tiên từ cao xuống thấp (BR-M08-06, BR-M08-07). |
| FR-M08-02.02 | Hệ thống phải đánh dấu trong hàng chờ các vụ đang được giữ. |
| FR-M08-02.03 | Hệ thống phải giữ vụ trong hàng chờ cho tới khi vụ được kết luận, không đặt hạn xử lý. |
| FR-M08-02.04 | Nếu người mở hàng chờ không có vai trò Mod hoặc Admin, hệ thống phải từ chối. |
| FR-M08-02.05 | Trong khi công tắc AI tổng hoặc công tắc Moderation tắt, hệ thống phải vẫn cho Mod, Admin xử lý các vụ trong hàng chờ báo cáo. |
| FR-M08-02.06 | Hệ thống phải không hiển thị cho một Mod hoặc Admin các vụ nhắm vào bài viết, bình luận hoặc tài khoản của chính người đó (BR-M08-46). |
| FR-M08-02.07 | Nếu hai vụ có cùng điểm ưu tiên, hệ thống phải xếp vụ mở trước đứng trước (BR-M08-07). |
| FR-M08-02.08 | Hệ thống phải đánh dấu trong hàng chờ các vụ là yêu cầu ban (BR-M08-36). |
| FR-M08-02.09 | Hệ thống phải chỉ hiển thị cho Admin các vụ nhắm vào bài viết, bình luận hoặc tài khoản của một Mod, không hiển thị cho các Mod khác (BR-M08-46). |

### 5.3 FR-M08-03 Nhận và nhả vụ báo cáo

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin nhận giữ một vụ để xử lý, và tự nhả vụ khi người giữ không còn thao tác.

**Lý do:** Để nhiều Mod cùng xử lý hàng chờ mà không trùng việc (cơ chế nhận xử lý, tự nhả sau 30 phút).

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-03.01 | Khi Mod hoặc Admin chọn "Nhận xử lý" một vụ Mở chưa ai giữ, hệ thống phải ghi người đó là người giữ vụ. |
| FR-M08-03.02 | Nếu vụ đang được người khác giữ, hệ thống phải từ chối "Nhận xử lý" (BR-M08-08). |
| FR-M08-03.03 | Nếu người không giữ vụ thực hiện thao tác xử lý (ẩn, cảnh cáo, ban, kết luận) trên một vụ, hệ thống phải từ chối thao tác đó (BR-M08-08). |
| FR-M08-03.04 | Khi người giữ không có thao tác nào trên vụ trong 30 phút, hệ thống phải nhả vụ về trạng thái chưa ai giữ (BR-M08-09). |
| FR-M08-03.05 | Nếu vụ đã được kết luận, hệ thống phải từ chối "Nhận xử lý". |
| FR-M08-03.06 | Nếu người chọn "Nhận xử lý" không có vai trò Mod hoặc Admin, hệ thống phải từ chối. |
| FR-M08-03.07 | Nếu một Mod hoặc Admin chọn "Nhận xử lý" một vụ nhắm vào bài viết, bình luận hoặc tài khoản của chính mình, hệ thống phải từ chối (BR-M08-46). |
| FR-M08-03.08 | Hệ thống phải tính 30 phút không thao tác từ thao tác cuối của người giữ trên vụ: mở xem vụ, ẩn nội dung, cảnh cáo, ban, kết luận (BR-M08-09). |
| FR-M08-03.09 | Nếu một Mod chọn "Nhận xử lý" một vụ nhắm vào bài viết, bình luận hoặc tài khoản của một Mod khác, hệ thống phải từ chối (BR-M08-46). |

### 5.4 FR-M08-04 Xem chi tiết vụ báo cáo

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin xem đủ thông tin của một vụ để đánh giá: các báo cáo, đối tượng, lịch sử báo cáo của đối tượng và chỉ số báo cáo sai của người báo cáo.

**Lý do:** Mod xem toàn bộ lịch sử báo cáo của đối tượng làm bối cảnh; chỉ số tập trung cao là dấu hiệu dùng báo cáo để quấy rối có chủ đích, khác với nhầm lẫn thật thà.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-04.01 | Khi Mod hoặc Admin mở một vụ, hệ thống phải hiển thị từng báo cáo trong vụ với người báo cáo, lý do, mô tả và bằng chứng. |
| FR-M08-04.02 | Khi Mod hoặc Admin mở một vụ, hệ thống phải hiển thị đối tượng bị báo cáo, kể cả khi bài viết, bình luận đó đã bị tác giả xóa, đã xóa hẳn hoặc đang Tự ẩn (BR-M08-15). |
| FR-M08-04.03 | Khi Mod hoặc Admin mở một vụ, hệ thống phải hiển thị lịch sử báo cáo của đối tượng: các vụ đã kết luận trước đó và kết luận của chúng (BR-M08-11). |
| FR-M08-04.04 | Khi Mod hoặc Admin mở một vụ, hệ thống phải hiển thị chỉ số tập trung của từng người báo cáo trong vụ, tính cho đối tượng của vụ đó (BR-M08-19). |
| FR-M08-04.05 | Khi Mod hoặc Admin mở một vụ, hệ thống phải hiển thị mức cảnh cáo hiện tại của người bị báo cáo. |
| FR-M08-04.06 | Nếu đối tượng là bài đăng ẩn danh hoặc của tác giả đang DEACTIVATED, hệ thống phải hiển thị danh tính thật của tác giả cho Mod, Admin. |
| FR-M08-04.07 | Hệ thống phải không cho Mod, Admin xem nội dung đã xóa, tự ẩn, đã xóa hẳn của người khác ngoài vụ, lịch sử báo cáo và khiếu nại liên quan tới chính nội dung đó (BR-M08-15). |
| FR-M08-04.08 | Nếu người mở vụ không có vai trò Mod hoặc Admin, hệ thống phải từ chối. |
| FR-M08-04.09 | Khi vụ có mục do AI tạo, hệ thống phải hiển thị người báo cáo của mục đó là "Hệ thống (AI)" và lý do là nhóm vi phạm AI phát hiện (BR-M08-49). |
| FR-M08-04.10 | Khi đối tượng là một nhóm, hệ thống phải hiển thị Owner của nhóm là người bị báo cáo (BR-M08-50). |

### 5.5 FR-M08-05 Kết luận vụ báo cáo

**Yêu cầu cấp trên:** Hệ thống phải cho phép người đang giữ vụ kết luận vụ, đóng mọi báo cáo trong vụ và báo kết quả cho người báo cáo và người bị báo cáo.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-05.01 | Khi người giữ vụ kết luận Có xử lý hoặc Bác bỏ kèm lý do kết luận, hệ thống phải chuyển vụ sang Đã xử lý và lưu kết luận, lý do kết luận, người kết luận, thời điểm kết luận. |
| FR-M08-05.02 | Khi vụ chuyển sang Đã xử lý, hệ thống phải chuyển mọi báo cáo Mở trong vụ sang Đã xử lý với kết luận của vụ (BR-M08-10). |
| FR-M08-05.03 | Hệ thống phải cho lý do kết luận khác với lý do người báo cáo đã chọn. |
| FR-M08-05.04 | Khi vụ chuyển sang Đã xử lý, hệ thống phải gửi cho mọi người báo cáo là người dùng trong vụ cùng một kết quả chung theo BR-M08-12 (qua M07). |
| FR-M08-05.05 | Khi vụ được kết luận Có xử lý, hệ thống phải gửi cho người bị báo cáo thông báo gồm lý do kết luận và mức xử lý (BR-M08-13, qua M07). |
| FR-M08-05.06 | Hệ thống phải không cho người bị báo cáo thấy danh tính người báo cáo, lý do họ chọn, mô tả và bằng chứng (BR-M08-14). |
| FR-M08-05.07 | Nếu người kết luận khác người đang giữ vụ, hệ thống phải từ chối kết luận (BR-M08-08). |
| FR-M08-05.08 | Nếu vụ đã ở Đã xử lý, hệ thống phải từ chối kết luận lại. |
| FR-M08-05.09 | Nếu người giữ vụ kết luận mà không nhập lý do kết luận, hệ thống phải từ chối kết luận. |
| FR-M08-05.10 | Khi vụ được kết luận Bác bỏ, hệ thống phải không gửi thông báo cho người bị báo cáo (BR-M08-13). |
| FR-M08-05.11 | Khi thông báo cho người bị báo cáo về một cảnh cáo, một ban hoặc một bài viết bị ẩn, hệ thống phải kèm đường dẫn khiếu nại (M09); với bình luận bị ẩn, nhóm bị ẩn hoặc bị khóa thì không kèm (BR-M08-13). |

### 5.6 FR-M08-06 Ẩn bài viết, bình luận vi phạm

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin ẩn bài viết, bình luận vi phạm của người khác trong một vụ.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-06.01 | Khi Mod hoặc Admin đang giữ vụ ẩn bài viết của vụ, hệ thống phải chuyển trạng thái kiểm duyệt của bài sang Bị ẩn (BR-M08-16). |
| FR-M08-06.02 | Khi Mod hoặc Admin đang giữ vụ ẩn bình luận của vụ, hệ thống phải chuyển trạng thái kiểm duyệt của bình luận sang Bị ẩn (BR-M08-16). |
| FR-M08-06.03 | Hệ thống phải không cho Mod, Admin xóa bài viết, bình luận của người khác (BR-M08-16). |
| FR-M08-06.04 | Nếu người ẩn không có vai trò Mod hoặc Admin, hệ thống phải từ chối. |
| FR-M08-06.05 | Nếu bài viết, bình luận đã ở trạng thái Bị ẩn, hệ thống phải từ chối ẩn lại. |
| FR-M08-06.06 | Nếu Mod, Admin ẩn bài viết, bình luận ngoài một vụ mình đang giữ, hệ thống phải từ chối (BR-M08-48). |

### 5.7 FR-M08-07 Xét nội dung bị gắn cờ

**Yêu cầu cấp trên:** Hệ thống phải đưa nội dung bị AI gắn cờ vào hàng chờ báo cáo và cho phép Mod, Admin xét: giữ hoặc ẩn, và quyết có cảnh cáo tác giả không.

**Lý do:** Con người luôn quyết định cuối cùng; AI kiểm duyệt chỉ đưa ra dự đoán và độ tin cậy, không tự quyết tuyệt đối với trường hợp nhạy cảm.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-07.01 | Khi Mod hoặc Admin xét một bài viết Bị gắn cờ và giữ bài, hệ thống phải chuyển bài về trạng thái kiểm duyệt Bình thường. |
| FR-M08-07.02 | Khi Mod hoặc Admin xét một bài viết Bị gắn cờ và ẩn bài, hệ thống phải chuyển bài sang Bị ẩn. |
| FR-M08-07.03 | Khi Mod hoặc Admin xét một bình luận bị AI ẩn với điểm quét từ 0,5 đến dưới 0,9 và kết luận không vi phạm, hệ thống phải chuyển bình luận về Bình thường. |
| FR-M08-07.04 | Khi Mod hoặc Admin xét một bình luận bị AI ẩn với điểm quét từ 0,5 đến dưới 0,9 và kết luận vi phạm, hệ thống phải giữ bình luận ở Bị ẩn. |
| FR-M08-07.05 | Khi Mod hoặc Admin xét nội dung có điểm quét từ 0,5 đến dưới 0,9, hệ thống phải cho Mod, Admin quyết có cảnh cáo tác giả hay không (BR-M08-23). |
| FR-M08-07.06 | Hệ thống phải hiển thị nội dung bị gắn cờ của người khác cho Mod, Admin khi xét. |
| FR-M08-07.07 | Nếu nội dung không còn ở trạng thái chờ xét, hệ thống phải từ chối thao tác xét. |
| FR-M08-07.08 | Nếu người xét không có vai trò Mod hoặc Admin, hệ thống phải từ chối. |
| FR-M08-07.09 | Khi một bài viết chuyển sang Bị gắn cờ sau khi quét lại (M03), hệ thống phải thêm một mục do "Hệ thống (AI)" tạo vào vụ đang Mở của bài, hoặc mở vụ mới nếu bài không có vụ Mở (BR-M08-49). |
| FR-M08-07.10 | Hệ thống phải không đổi trạng thái kiểm duyệt của bài viết, bình luận khi nhận báo cáo của người dùng (BR-M08-48). |

### 5.8 FR-M08-08 Quét AI luồng bình luận

**Yêu cầu cấp trên:** Hệ thống phải quét AI các luồng bình luận đang có nhiều trả lời trong thời gian ngắn, rồi ẩn hoặc đưa Mod xét các bình luận có điểm quét cao.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-08.01 | Ở nơi công tắc AI tổng và công tắc Moderation đều bật, khi số trả lời của một luồng trong khoảng thời gian trượt đạt ngưỡng tốc độ trở lên (BR-M08-20), hệ thống phải quét AI các bình luận của luồng chưa được quét với nội dung hiện tại (BR-M08-21). |
| FR-M08-08.02 | Hệ thống phải không quét bình luận lúc bình luận được đăng (BR-M08-20). |
| FR-M08-08.03 | Khi tác giả sửa một bình luận, hệ thống phải chờ lần kích hoạt kế tiếp của luồng mới quét lại bình luận đó (BR-M08-21). |
| FR-M08-08.04 | Khi quét xong một bình luận với điểm quét từ 0,9 trở lên, hệ thống phải chuyển bình luận sang Bị ẩn mà không đưa vào hàng chờ (BR-M08-22). |
| FR-M08-08.05 | Khi quét xong một bình luận với điểm quét từ 0,5 đến dưới 0,9, hệ thống phải chuyển bình luận sang Bị ẩn và thêm một mục do "Hệ thống (AI)" tạo vào vụ đang Mở của bình luận, hoặc mở vụ mới (BR-M08-22, BR-M08-49). |
| FR-M08-08.06 | Khi quét xong một bình luận với điểm quét dưới 0,5, hệ thống phải giữ nguyên trạng thái kiểm duyệt của bình luận. |
| FR-M08-08.07 | Khi AI ẩn một bình luận, hệ thống phải gửi cho tác giả thông báo trong ứng dụng "Bình luận của bạn đã bị ẩn" (qua M07). |
| FR-M08-08.08 | Khi quét xong một bình luận, hệ thống phải ghi nhận bình luận đã được quét với nội dung hiện tại. |
| FR-M08-08.09 | Nếu quét một bình luận thất bại sau một lần thử lại, hệ thống phải giữ nguyên trạng thái bình luận và ghi lỗi cho Admin (BR-M08-27). |
| FR-M08-08.10 | Trong khi công tắc AI tổng hoặc công tắc Moderation tắt, hệ thống phải không quét luồng bình luận (BR-M08-26). |
| FR-M08-08.11 | Hệ thống phải lấy điểm quét của một bài viết, bình luận là điểm cao nhất trong bốn nhóm vi phạm AI trả về (BR-M08-51). |
| FR-M08-08.12 | Khi quét một luồng bình luận, hệ thống phải không gửi quét các bình luận của Admin (BR-M08-55). |

### 5.9 FR-M08-09 Tự cảnh cáo bằng AI

**Yêu cầu cấp trên:** Hệ thống phải tự ra cảnh cáo cho tác giả khi kết quả quét AI một bài viết hoặc bình luận có độ tin cậy cao, và không bao giờ tự ban.

**Lý do:** Mô hình "AI cảnh cáo, con người ban": giữ con người trong vòng quyết định với quyết định nghiêm trọng, đồng thời tận dụng AI cho quy mô. Người dùng bị cảnh cáo sai có thể khiếu nại (M09).

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-09.01 | Ở nơi công tắc AI tổng và công tắc Moderation đều bật, khi kết quả quét một bài viết (M03) hoặc bình luận có điểm quét từ 0,9 trở lên, hệ thống phải tự ra một cảnh cáo cho tác giả với người ra là AI (BR-M08-23). |
| FR-M08-09.02 | Khi kết quả quét có điểm quét từ 0,5 đến dưới 0,9, hệ thống phải không tự cảnh cáo mà để Mod, Admin quyết khi xét (BR-M08-23). |
| FR-M08-09.03 | Khi kết quả quét có điểm quét dưới 0,5, hệ thống phải không cảnh cáo tác giả. |
| FR-M08-09.04 | Khi một cảnh cáo được ra, hệ thống phải cập nhật số lần cảnh cáo, mức cảnh cáo và thời gian thử thách của người bị cảnh cáo theo BR-M08-28, BR-M08-29. |
| FR-M08-09.05 | Khi AI ra một cảnh cáo, hệ thống phải gửi cho người bị cảnh cáo thông báo cảnh cáo trong ứng dụng kèm đường dẫn khiếu nại (qua M07). |
| FR-M08-09.06 | Hệ thống phải không để AI ban tài khoản, dù điểm quét cao tới đâu (BR-M08-33). |
| FR-M08-09.07 | Trong khi công tắc AI tổng hoặc công tắc Moderation tắt, hệ thống phải không tự cảnh cáo (BR-M08-26). |
| FR-M08-09.08 | Khi kết quả quét có điểm quét từ 0,9 trở lên với nội dung của tác giả có vai trò Mod, hệ thống phải không tự cảnh cáo mà thêm một mục do "Hệ thống (AI)" tạo vào vụ của nội dung đó để Admin quyết có cảnh cáo hay không (BR-M08-46). |
| FR-M08-09.09 | Khi kết quả quét có điểm quét từ 0,9 trở lên với nội dung của tác giả có vai trò Admin, hệ thống phải không tự cảnh cáo (BR-M08-46). |
| FR-M08-09.10 | Hệ thống phải dùng cùng ngưỡng 0,9 và 0,5 cho mọi tác giả, không phụ thuộc mức cảnh cáo của tác giả (BR-M08-24). |
| FR-M08-09.11 | Nếu tác giả đang ở mức HEAVY, hệ thống phải không ra cảnh cáo mới mà tạo yêu cầu ban theo FR-M08-14.11 (BR-M08-36). |
| FR-M08-09.12 | Khi một lần quét cho điểm từ 0,9 trở lên với nhiều nội dung của cùng một tác giả, hệ thống phải ra một cảnh cáo cho mỗi nội dung (BR-M08-23). |

### 5.10 FR-M08-10 Cảnh cáo người dùng

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin cảnh cáo người vi phạm trong một vụ đang giữ.

**Lý do:** Mô hình "AI cảnh cáo, con người ban"; Mod, Admin vẫn tự cảnh cáo được khi xử lý.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-10.01 | Khi Mod hoặc Admin đang giữ vụ cảnh cáo người vi phạm, hệ thống phải lưu một cảnh cáo với người ra là Mod hoặc Admin đó, lý do và vụ liên quan. |
| FR-M08-10.02 | Khi Mod hoặc Admin ra một cảnh cáo, hệ thống phải cập nhật số lần cảnh cáo, mức cảnh cáo và thời gian thử thách của người bị cảnh cáo theo BR-M08-28, BR-M08-29. |
| FR-M08-10.03 | Khi Mod hoặc Admin ra một cảnh cáo, hệ thống phải gửi cho người bị cảnh cáo thông báo cảnh cáo trong ứng dụng kèm đường dẫn khiếu nại (qua M07). |
| FR-M08-10.04 | Hệ thống phải cho Mod, Admin cảnh cáo người báo cáo của vụ khi đánh giá người đó báo cáo ác ý (BR-M08-18). |
| FR-M08-10.05 | Hệ thống phải không tự cảnh cáo hay phạt người báo cáo có báo cáo bị Bác bỏ (BR-M08-18). |
| FR-M08-10.06 | Khi xử lý vụ báo cáo người dùng, hệ thống phải chỉ cho Mod, Admin cảnh cáo hoặc ban, không cho gỡ, sửa avatar, bio của người đó (BR-M08-17). |
| FR-M08-10.07 | Nếu người ra cảnh cáo không có vai trò Mod hoặc Admin, hệ thống phải từ chối. |
| FR-M08-10.08 | Nếu người bị cảnh cáo có vai trò Mod mà người ra cảnh cáo là Mod, hệ thống phải từ chối cảnh cáo (BR-M08-46). |
| FR-M08-10.09 | Nếu người bị cảnh cáo có vai trò Admin, hệ thống phải từ chối cảnh cáo (BR-M08-46). |
| FR-M08-10.10 | Nếu người vi phạm đang ở mức HEAVY, hệ thống phải từ chối cảnh cáo mới và để Mod, Admin chọn Ban (BR-M08-36). |
| FR-M08-10.11 | Nếu Mod, Admin cảnh cáo ngoài một vụ mình đang giữ, hệ thống phải từ chối (BR-M08-48). |

### 5.11 FR-M08-11 Bỏ cảnh cáo do AI ra

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin bỏ một cảnh cáo do AI tự ra.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-11.01 | Hệ thống phải cho Mod, Admin bỏ một cảnh cáo có người ra là AI. |
| FR-M08-11.02 | Nếu người bỏ cảnh cáo không có vai trò Mod hoặc Admin, hệ thống phải từ chối. |
| FR-M08-11.03 | Khi một cảnh cáo bị bỏ, hệ thống phải giảm số lần cảnh cáo của người đó 1 lần và tính lại mức cảnh cáo theo số lần còn lại (BR-M08-54). |
| FR-M08-11.04 | Khi một cảnh cáo bị bỏ, hệ thống phải giữ bản ghi cảnh cáo và đánh dấu "đã bỏ" (BR-M08-54). |
| FR-M08-11.05 | Khi một cảnh cáo bị bỏ, hệ thống phải giữ nguyên thời điểm kết thúc thời gian thử thách hiện tại (BR-M08-54). |

### 5.12 FR-M08-12 Giảm mức cảnh cáo khi hết thời gian thử thách

**Yêu cầu cấp trên:** Hệ thống phải tự giảm mức cảnh cáo của người dùng khi hết thời gian thử thách.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-12.01 | Khi thời gian thử thách của mức cảnh cáo hiện tại kết thúc, hệ thống phải giảm mức cảnh cáo của người dùng một bậc (BR-M08-30). |
| FR-M08-12.02 | Khi mức cảnh cáo của người dùng thay đổi, hệ thống phải áp hạn chế của mức mới (BR-M08-31). |
| FR-M08-12.03 | Hệ thống phải tính thời gian thử thách N ngày là đủ N × 24 giờ kể từ lúc cảnh cáo hoặc lúc giảm mức (BR-M08-29). |
| FR-M08-12.04 | Khi giảm mức, hệ thống phải đặt số lần cảnh cáo bằng số lần cao nhất của mức mới: 4 khi về MEDIUM, 2 khi về LIGHT, 0 khi về Sạch (BR-M08-30). |
| FR-M08-12.05 | Khi giảm về MEDIUM hoặc LIGHT, hệ thống phải bắt đầu thời gian thử thách của mức mới ngay lúc giảm (BR-M08-30). |

### 5.13 FR-M08-13 Xem mức cảnh cáo của mình

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng xem mức cảnh cáo của chính mình và giữ trạng thái cảnh cáo riêng tư với người khác.

**Lý do:** Trạng thái cảnh cáo hoàn toàn riêng tư để tránh học sinh bị cảnh cáo bị bắt nạt.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-13.01 | Hệ thống phải cho người dùng xem mức cảnh cáo hiện tại và thời điểm kết thúc thời gian thử thách của chính mình. |
| FR-M08-13.02 | Nếu người xem khác chính người đó và không có vai trò Mod hoặc Admin, hệ thống phải không hiển thị mức cảnh cáo của người đó (BR-M08-32). |
| FR-M08-13.03 | Hệ thống phải không hiển thị mức cảnh cáo trên bài viết, bình luận, hồ sơ (BR-M08-32). |

### 5.14 FR-M08-14 Ban người dùng

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin ban người dùng trong một vụ: ban có thời hạn leo thang hoặc ban vĩnh viễn.

**Lý do:** Mô hình "AI cảnh cáo, con người ban": giữ con người trong vòng quyết định với quyết định nghiêm trọng.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-14.01 | Khi Mod hoặc Admin đang giữ vụ chọn "Ban" người vi phạm, hệ thống phải tạo một ban Đang hiệu lực với thời hạn theo số lần đã bị ban (BR-M08-34), lý do, người ban và thời điểm bắt đầu. |
| FR-M08-14.02 | Khi Mod hoặc Admin đang giữ vụ chọn "Ban vĩnh viễn" người vi phạm, hệ thống phải tạo một ban vĩnh viễn Đang hiệu lực, không theo cách tính leo thang (BR-M08-35). |
| FR-M08-14.03 | Khi một ban được tạo, hệ thống phải chuyển tài khoản bị ban sang BANNED (M01). |
| FR-M08-14.04 | Khi một ban được tạo, hệ thống phải gửi cho người bị ban thông báo ban trong ứng dụng và email, kèm lý do và đường dẫn khiếu nại (qua M07). |
| FR-M08-14.05 | Khi Mod hoặc Admin ban một tài khoản có vai trò Mod, hệ thống phải thu hồi vai trò Mod của tài khoản đó. |
| FR-M08-14.06 | Hệ thống phải không cho AI tạo ban (BR-M08-33). |
| FR-M08-14.07 | Nếu người ban không có vai trò Mod hoặc Admin, hệ thống phải từ chối. |
| FR-M08-14.08 | Khi ban tạm thời hết thời hạn, hệ thống phải chuyển ban sang Hết hạn (BR-M08-37). |
| FR-M08-14.09 | Nếu người bị ban có vai trò Mod mà người ban là Mod, hệ thống phải từ chối ban (BR-M08-46). |
| FR-M08-14.10 | Nếu người bị ban có vai trò Admin, hệ thống phải từ chối ban (BR-M08-46). |
| FR-M08-14.11 | Khi người đang ở mức HEAVY bị xác định vi phạm tiếp (AI cho điểm từ 0,9 trở lên, hoặc Mod kết luận vi phạm trong vụ), hệ thống phải đánh dấu vụ của nội dung đó là yêu cầu ban, mở vụ nếu nội dung chưa có vụ Mở (BR-M08-36). |
| FR-M08-14.12 | Hệ thống phải tính số lần đã bị ban gồm mọi ban từng có hiệu lực, kể cả ban được gỡ sớm và ban vĩnh viễn, trừ ban bị lật do khiếu nại (BR-M08-34). |
| FR-M08-14.13 | Nếu tài khoản đang có một ban Đang hiệu lực, hệ thống phải từ chối ban mới (BR-M08-52). |
| FR-M08-14.14 | Nếu Mod, Admin ban ngoài một vụ mình đang giữ, hệ thống phải từ chối (BR-M08-48). |

### 5.15 FR-M08-15 Gỡ ban

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin gỡ ban đang hiệu lực.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-15.01 | Khi Mod hoặc Admin gỡ một ban Đang hiệu lực, hệ thống phải chuyển ban sang Đã gỡ và chuyển tài khoản về ACTIVE (M01) (BR-M08-38). |
| FR-M08-15.02 | Khi một ban được gỡ, hệ thống phải gửi cho người được gỡ ban thông báo gỡ ban trong ứng dụng và email (qua M07). |
| FR-M08-15.03 | Nếu ban không còn Đang hiệu lực, hệ thống phải từ chối gỡ ban. |
| FR-M08-15.04 | Nếu người gỡ ban không có vai trò Mod hoặc Admin, hệ thống phải từ chối. |
| FR-M08-15.05 | Hệ thống phải cho Mod, Admin gỡ ban trực tiếp trên tài khoản, không cần vụ (BR-M08-48). |

### 5.16 FR-M08-16 Ghi nhật ký kiểm duyệt

**Yêu cầu cấp trên:** Hệ thống phải ghi mọi thao tác kiểm duyệt của Mod, Admin và AI vào nhật ký kiểm duyệt và giữ vĩnh viễn.

**Lý do:** Nhật ký kiểm duyệt có giá trị minh bạch và truy vết, nên được giữ vĩnh viễn như thông lệ với dữ liệu nhật ký.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-16.01 | Khi Mod, Admin hoặc AI cảnh cáo, ban, ẩn nội dung hoặc kết luận vụ, hệ thống phải ghi một dòng nhật ký gồm người làm, loại thao tác, đối tượng, lý do và thời điểm (BR-M08-39). |
| FR-M08-16.02 | Khi Mod hoặc Admin vô hiệu hóa, kích hoạt lại Tag hoặc đổi Topic, Tag trên bài người khác (M05), hệ thống phải ghi một dòng nhật ký (BR-M08-39). |
| FR-M08-16.03 | Hệ thống phải giữ mọi dòng nhật ký kiểm duyệt vĩnh viễn, không xóa (BR-M08-40). |
| FR-M08-16.04 | Nếu người làm đã xóa tài khoản, hệ thống phải hiển thị người làm là "[Người dùng đã xóa]" và vẫn cho tra cứu dòng nhật ký qua username (BR-M08-40). |
| FR-M08-16.05 | Khi Mod hoặc Admin gỡ ban, bỏ cảnh cáo do AI ra, ẩn, khóa hoặc mở khóa nhóm, hệ thống phải ghi một dòng nhật ký (BR-M08-39). |
| FR-M08-16.06 | Hệ thống phải không cho sửa dòng nhật ký kiểm duyệt (BR-M08-40). |
| FR-M08-16.07 | Hệ thống phải không ghi nhật ký việc nhận và tự nhả vụ (BR-M08-39). |

### 5.17 FR-M08-17 Xem nhật ký kiểm duyệt

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin xem toàn bộ nhật ký kiểm duyệt và Mod xem phần nhật ký của mình.

**Lý do:** Mod không xét khiếu nại về hành động của chính mình (xung đột lợi ích); chỉ khi xét khiếu nại về thao tác của Mod khác, Mod mới được xem thao tác đó.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-17.01 | Khi Admin mở nhật ký kiểm duyệt, hệ thống phải hiển thị mọi dòng nhật ký của mọi người làm. |
| FR-M08-17.02 | Khi Mod mở nhật ký kiểm duyệt, hệ thống phải hiển thị danh sách các vụ chính Mod đó đã xử lý. |
| FR-M08-17.03 | Khi Mod đang xét một khiếu nại (M09) về thao tác của Mod khác, hệ thống phải hiển thị chi tiết thao tác đó cho Mod đang xét. |
| FR-M08-17.04 | Nếu Mod xem thao tác của Mod khác ngoài trường hợp ở FR-M08-17.03, hệ thống phải từ chối (BR-M08-41). |
| FR-M08-17.05 | Nếu người mở nhật ký không có vai trò Mod hoặc Admin, hệ thống phải từ chối. |
| FR-M08-17.06 | Khi Admin lọc nhật ký kiểm duyệt theo người làm, hệ thống phải chỉ hiển thị các dòng của người làm đó (BR-M08-41). |

### 5.18 FR-M08-18 Ẩn, khóa và mở khóa nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin ẩn hoặc khóa một nhóm vi phạm trong vụ báo cáo nhóm, và mở khóa nhóm đã khóa.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M08-18.01 | Khi Mod hoặc Admin đang giữ vụ về một nhóm chọn "Ẩn nhóm", hệ thống phải chuyển trạng thái kiểm duyệt của nhóm sang Bị ẩn (BR-M08-50). |
| FR-M08-18.02 | Trong khi nhóm ở trạng thái Bị ẩn, hệ thống phải không hiển thị nhóm và mọi nội dung của nhóm với bất kỳ ai, kể cả thành viên và Owner (M11) (BR-M08-50). |
| FR-M08-18.03 | Hệ thống phải không có thao tác bỏ ẩn nhóm (BR-M08-50). |
| FR-M08-18.04 | Khi Mod hoặc Admin đang giữ vụ về một nhóm chọn "Khóa nhóm", hệ thống phải chuyển trạng thái kiểm duyệt của nhóm sang Bị khóa (BR-M08-50). |
| FR-M08-18.05 | Trong khi nhóm ở trạng thái Bị khóa, hệ thống phải chặn với mọi người, kể cả Owner và Group Mod, các thao tác trong nhóm theo danh sách của M11 (BR-M11-28), gồm đăng bài, bình luận, upvote, bình chọn poll, tham gia và mời thành viên (BR-M08-50). |
| FR-M08-18.06 | Trong khi nhóm ở trạng thái Bị khóa, hệ thống phải vẫn cho người được phép xem nhóm đọc nội dung, lưu bài và báo cáo (BR-M08-50). |
| FR-M08-18.07 | Khi Mod hoặc Admin mở khóa một nhóm Bị khóa, hệ thống phải chuyển nhóm về Bình thường mà không cần vụ (BR-M08-50). |
| FR-M08-18.08 | Hệ thống phải cho Mod, Admin ẩn một nhóm đang Bị khóa trong một vụ sau (BR-M08-50). |
| FR-M08-18.09 | Nếu nhóm đã ở trạng thái Bị ẩn, hệ thống phải từ chối khóa, ẩn lại hoặc mở khóa nhóm. |
| FR-M08-18.10 | Nếu người thực hiện không có vai trò Mod hoặc Admin, hệ thống phải từ chối ẩn, khóa, mở khóa nhóm. |
| FR-M08-18.11 | Khi vụ về một nhóm được kết luận Có xử lý, hệ thống phải gửi thông báo kết quả cho Owner của nhóm, không kèm đường dẫn khiếu nại (BR-M08-13, BR-M08-50). |

### 5.19 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M08-01 | Ràng buộc | Chỉ người dùng đã đăng nhập được báo cáo; Guest không báo cáo được. | — |
| BR-M08-02 | Ràng buộc | Lý do báo cáo theo loại đối tượng. Bài viết (8): Spam/Quảng cáo; Nội dung sai/hiểu nhầm; Đạo văn/Vi phạm bản quyền; Quấy rối/Bắt nạt; Ngôn từ thù ghét/Phân biệt; Nội dung người lớn/Không phù hợp; Bạo lực/Đe dọa; Khác. Bình luận (7): như bài viết, bỏ Đạo văn/Vi phạm bản quyền. Người dùng (2): Quấy rối/Bắt nạt có hệ thống; Khác. Nhóm (4): Nội dung người lớn/Không phù hợp; Group giả mạo; Quấy rối/Bắt nạt có hệ thống; Khác. Mỗi báo cáo chọn đúng một lý do. | Báo cáo một bình luận: danh sách có 7 lý do, không có "Đạo văn/Vi phạm bản quyền". Báo cáo một người dùng: chỉ có 2 lý do. Thấy bài vừa spam vừa sai lệch: gửi hai báo cáo. |
| BR-M08-03 | Ràng buộc | Bằng chứng tối đa 3 ảnh, mỗi ảnh tối đa 5MB, định dạng JPEG, PNG hoặc WebP. | 3 ảnh 4MB: nhận. Ảnh thứ 4: từ chối. Ảnh đúng 5MB: nhận; ảnh 5,1MB: từ chối. Tệp PDF: từ chối. |
| BR-M08-04 | Ràng buộc | Mô tả là tùy chọn; bắt buộc khi lý do là "Khác". | Lý do "Spam/Quảng cáo", mô tả trống: nhận. Lý do "Khác", mô tả trống: từ chối. |
| BR-M08-05 | Kích hoạt | Báo cáo mới về một đối tượng đang có vụ Mở được thêm vào vụ đó. Đối tượng không có vụ Mở (chưa từng bị báo cáo, hoặc mọi vụ trước đã kết luận) thì hệ thống mở vụ mới; vụ đã kết luận không bao giờ mở lại. | Bài P có vụ V1 đang mở với 2 báo cáo; báo cáo thứ 3 vào V1 (3 báo cáo). V1 kết luận lúc 10:00; báo cáo mới lúc 10:05 mở vụ V2; lịch sử của P có V1. |
| BR-M08-06 | Tính toán | Điểm ưu tiên của vụ = mức nặng cao nhất trong các lý do của các báo cáo trong vụ + số báo cáo trong vụ × 2. Mức nặng: 10 — Bạo lực/Đe dọa; Nội dung người lớn/Không phù hợp; Ngôn từ thù ghét/Phân biệt; Quấy rối/Bắt nạt (kể cả "có hệ thống"); Group giả mạo. 5 — Nội dung sai/hiểu nhầm; Đạo văn/Vi phạm bản quyền. 2 — Spam/Quảng cáo; Khác. Mục do AI tạo tính là một báo cáo với lý do là nhóm vi phạm AI phát hiện. | 1 báo cáo "Bạo lực": 10 + 1 × 2 = 12. 5 báo cáo "Spam": 2 + 5 × 2 = 12. 3 báo cáo "Spam": 2 + 3 × 2 = 8. 1 "Spam" + 1 "Nội dung sai": max(2, 5) + 2 × 2 = 9. |
| BR-M08-07 | Ràng buộc | Hàng chờ xếp vụ theo điểm ưu tiên từ cao xuống thấp; hai vụ bằng điểm thì vụ mở trước đứng trước; không có hạn xử lý. | Vụ V1 (12, mở 08:00), V3 (12, mở 09:00), V4 (9), V2 (8): thứ tự V1, V3, V4, V2. |
| BR-M08-08 | Ràng buộc | Mỗi vụ tại một thời điểm chỉ có một Mod hoặc Admin giữ; người khác không nhận, không kết luận được vụ đang được giữ. | — |
| BR-M08-09 | Kích hoạt | Vụ đang được giữ tự được nhả khi người giữ không có thao tác nào trên vụ trong 30 phút. Thao tác gồm: mở xem vụ, ẩn nội dung, cảnh cáo, ban, kết luận. | Nhận lúc 10:00, mở xem bằng chứng lúc 10:20, không làm gì thêm: tự nhả lúc 10:50; lúc 10:49 vẫn đang giữ. |
| BR-M08-10 | Sự kiện | Khi vụ được kết luận, mọi báo cáo đang mở trong vụ cùng chuyển sang Đã xử lý với kết luận của vụ (Có xử lý hoặc Bác bỏ). Lý do kết luận do Mod, Admin tự xác định. | Vụ có 3 báo cáo (2 "Spam", 1 "Khác"); Mod kết luận Có xử lý với lý do "Quấy rối": cả 3 báo cáo thành Đã xử lý, Có xử lý. |
| BR-M08-11 | Sự kiện | Khi xử lý vụ, Mod, Admin thấy lịch sử báo cáo của đối tượng: các vụ trước và kết luận của chúng. | — |
| BR-M08-12 | Sự kiện | Mọi người báo cáo là người dùng trong vụ nhận cùng một kết quả chung, dùng cho mọi loại đối tượng: "đã có biện pháp xử lý" khi Có xử lý, "không phát hiện vi phạm" khi Bác bỏ; câu chữ chốt khi thiết kế. Không thấy mức xử lý dành cho người bị báo cáo. Mục do AI tạo không có thông báo cho người báo cáo. | Minh báo cáo tài khoản Lan, Mod kết luận Có xử lý và ban Lan 30 ngày: Minh nhận "đã có biện pháp xử lý", không biết Lan bị ban. |
| BR-M08-13 | Sự kiện | Chỉ khi vụ được kết luận Có xử lý, người bị báo cáo mới nhận thông báo chi tiết: lý do kết luận, mức xử lý (mức cảnh cáo, ban, nội dung bị ẩn, nhóm bị ẩn hoặc khóa). Đường dẫn khiếu nại (M09) chỉ kèm khi việc xử lý khiếu nại được: cảnh cáo, ban, bài viết bị ẩn. Vụ Bác bỏ: người bị báo cáo không nhận thông báo. Với vụ về nhóm, người bị báo cáo là Owner. | Bài của Bình bị ẩn và Bình bị cảnh cáo: Bình nhận lý do, "bài bị ẩn, cảnh cáo mức LIGHT", có đường dẫn khiếu nại. Bình luận của An bị ẩn: An nhận lý do, không có đường dẫn khiếu nại. Vụ về bài của Bình bị Bác bỏ: Bình không nhận gì. |
| BR-M08-14 | Ràng buộc | Người bị báo cáo không bao giờ thấy danh tính người báo cáo, lý do người báo cáo chọn, mô tả và bằng chứng. | — |
| BR-M08-15 | Ràng buộc | Mod, Admin chỉ xem nội dung đã xóa, tự ẩn, đã xóa hẳn của người khác trong ngữ cảnh kiểm duyệt của chính nội dung đó: vụ đang mở, lịch sử báo cáo, khiếu nại (M09); không duyệt, không tìm kiếm nội dung đó ở nơi khác. Bài Nháp, Bị từ chối của người khác không hiện với Mod, Admin. | — |
| BR-M08-16 | Ràng buộc | Với bình luận của người khác, Mod, Admin chỉ có thao tác Ẩn; với bài viết, "gỡ" hay "xóa" bài là Ẩn (trạng thái Bị ẩn). Mod, Admin không xóa nội dung của người khác. | — |
| BR-M08-17 | Ràng buộc | Báo cáo người dùng chỉ được xử lý bằng cảnh cáo hoặc ban; Mod, Admin không gỡ, không sửa avatar, bio của người khác. | — |
| BR-M08-18 | Sự kiện | Không có phạt tự động cho báo cáo sai hoặc ác ý. Mod, Admin tự đánh giá và có thể cảnh cáo người báo cáo ác ý bằng cảnh cáo thông thường. | — |
| BR-M08-19 | Tính toán | Chỉ số tập trung của một người báo cáo, tính cho đối tượng của vụ đang xem = số báo cáo của người đó nhắm vào đối tượng này và bị Bác bỏ ÷ tổng số báo cáo của người đó đã được xử lý; chỉ tính báo cáo được xử lý trong 90 × 24 giờ gần nhất. | Minh có 10 báo cáo đã xử lý trong 90 × 24 giờ: 6 bị Bác bỏ nhắm vào Lan, 2 bị Bác bỏ nhắm vào bài Y, 2 Có xử lý. Mod mở vụ về Lan: chỉ số của Minh = 6 ÷ 10 = 0,6. Mod mở vụ về bài Y: 2 ÷ 10 = 0,2. Báo cáo được xử lý đúng 90 × 24 giờ trước lúc xem: không tính. |
| BR-M08-20 | Kích hoạt | Hệ thống quét AI một luồng bình luận khi số trả lời của luồng trong khoảng thời gian trượt đạt ngưỡng tốc độ trở lên (giá trị tạm "10 trả lời trong 5 phút"); chỉ đếm trả lời, không đếm bình luận gốc. Bình luận không được quét khi đăng. | Với giá trị tạm: trả lời thứ 1 lúc 10:00, thứ 10 lúc 10:04: kích hoạt lúc 10:04. Chỉ có 9 trả lời trong 10:00–10:05: không kích hoạt. |
| BR-M08-21 | Ràng buộc | Mỗi lần kích hoạt, hệ thống quét bình luận gốc và mọi trả lời của luồng chưa được quét với nội dung hiện tại. Sửa bình luận không tự kích hoạt quét; bình luận đã sửa chỉ được quét lại ở lần kích hoạt sau. | Luồng có gốc G và trả lời T1–T9 đã quét; T3 được sửa, thêm T10–T15. Lần kích hoạt sau quét T3, T10–T15; không quét lại G, T1, T2, T4–T9. |
| BR-M08-22 | Suy diễn | Kết quả quét bình luận: điểm ≥ 0,9 → Bị ẩn ngay, không qua Mod; 0,5 ≤ điểm < 0,9 → Bị ẩn và vào hàng chờ cho Mod xét; điểm < 0,5 → giữ nguyên. | 0,9: ẩn ngay. 0,89: ẩn, vào hàng chờ. 0,5: ẩn, vào hàng chờ. 0,49: giữ nguyên. |
| BR-M08-23 | Suy diễn | Nhánh cảnh cáo, áp cho cả bài viết (khi M03 quét) và bình luận: điểm ≥ 0,9 → AI tự cảnh cáo tác giả, mỗi nội dung một cảnh cáo; 0,5 ≤ điểm < 0,9 → Mod, Admin quyết có cảnh cáo hay không khi xét; điểm < 0,5 → không cảnh cáo. Hai nhánh (nội dung, cảnh cáo) chạy độc lập trên cùng một kết quả quét. Ngoại lệ với tác giả là Mod, Admin: BR-M08-46; tác giả đang ở HEAVY: BR-M08-36. | Bình luận 0,95: bị ẩn ngay và tác giả bị AI cảnh cáo. Một lần quét bắt 3 bình luận ≥ 0,9 của Lan (đang Sạch): Lan nhận 3 cảnh cáo, lên MEDIUM. Bài vừa gửi 0,7: chờ Mod duyệt (M03); Mod quyết cả việc đăng và việc cảnh cáo. Bình luận 0,3: không ẩn, không cảnh cáo. |
| BR-M08-24 | Ràng buộc | Các ngưỡng 0,9 và 0,5 là giá trị tạm, dùng chung cho bài viết, bình luận, cho cả hai nhánh và cho mọi tác giả; mức cảnh cáo của tác giả không làm đổi ngưỡng. | Minh (Sạch) và Lan (HEAVY) cùng có bình luận 0,6: cả hai đều bị ẩn và chờ Mod xét. |
| BR-M08-25 | Sự kiện | AI chỉ phát hiện bốn nhóm vi phạm: Quấy rối, Ngôn từ thù ghét, Nội dung người lớn, Bạo lực. Spam, Đạo văn/Vi phạm bản quyền, Nội dung sai/gây hiểu nhầm chỉ được phát hiện qua báo cáo. | — |
| BR-M08-26 | Suy diễn | Khi công tắc AI tổng hoặc công tắc Moderation tắt, hệ thống không quét luồng bình luận và AI không tự cảnh cáo; nội dung đăng bình thường và chỉ dựa vào báo cáo. | — |
| BR-M08-27 | Suy diễn | Nếu quét một bình luận thất bại sau một lần thử lại, bình luận giữ nguyên trạng thái và lỗi được ghi lại cho Admin. | — |
| BR-M08-28 | Tính toán | Mức cảnh cáo theo số lần cảnh cáo: 0 → Sạch; 1–2 → LIGHT; 3–4 → MEDIUM; 5–6 → HEAVY. | 2 lần → LIGHT; cảnh cáo thứ 3 → MEDIUM; 6 lần → HEAVY. |
| BR-M08-29 | Ràng buộc | Thời gian thử thách: LIGHT 7 ngày, MEDIUM 10 ngày, HEAVY 15 ngày; N ngày là đủ N × 24 giờ kể từ lúc cảnh cáo hoặc lúc giảm mức. Cảnh cáo mới không làm đổi mức thì chỉ đặt lại thời gian thử thách của mức hiện tại. | Có 1 lần (LIGHT) lúc 09:00 01/10: hết thử thách 09:00 08/10. Cảnh cáo thứ 2 lúc 14:00 05/10: vẫn LIGHT, hết thử thách 14:00 12/10. |
| BR-M08-30 | Kích hoạt | Hết thời gian thử thách, mức cảnh cáo tự giảm một bậc và số lần cảnh cáo trở thành số lần cao nhất của mức mới: HEAVY → MEDIUM (4 lần), MEDIUM → LIGHT (2 lần), LIGHT → Sạch (0 lần). Mức mới bắt đầu thời gian thử thách của nó ngay lúc giảm. | Cảnh cáo thứ 6 lúc 09:00 01/10 (HEAVY) → 09:00 16/10 MEDIUM, 4 lần → 09:00 26/10 LIGHT, 2 lần → 09:00 02/11 Sạch, 0 lần. Bị cảnh cáo ngày 20/10 (đang MEDIUM, 4 lần): 5 lần, quay lại HEAVY, thử thách 15 ngày từ lúc đó. |
| BR-M08-31 | Ràng buộc | Hạn chế trong thời gian thử thách: LIGHT không hạn chế. MEDIUM không tạo bài mới (phạm vi do M03 định nghĩa), bình luận vẫn được. HEAVY không tạo bài mới, không tạo bình luận mới (vẫn sửa, xóa nội dung cũ của mình, bình chọn, báo cáo); nội dung hiện có bị giảm hạng tìm kiếm ×0,5 (M06); bị loại khỏi bảng xếp hạng công khai (M12). | Người ở MEDIUM: gửi bài mới bị từ chối, viết bình luận được. Người ở HEAVY: viết bình luận bị từ chối, sửa bình luận cũ vẫn được (M04). |
| BR-M08-32 | Ràng buộc | Trạng thái cảnh cáo là riêng tư: chỉ chính người đó và Mod, Admin thấy; không hiện trên bài viết, bình luận, hồ sơ. Ngoại lệ duy nhất là việc người ở mức HEAVY bị loại khỏi bảng xếp hạng (M12). | — |
| BR-M08-33 | Sự kiện | AI không bao giờ ban, dù độ tin cậy cao tới đâu; mọi ban do Mod hoặc Admin thực hiện. | — |
| BR-M08-34 | Tính toán | Thời hạn của thao tác "Ban" theo số lần đã bị ban: chưa từng bị ban → 30 ngày; đã bị ban 1 lần → 90 ngày; đã bị ban từ 2 lần → vĩnh viễn. Số lần đã bị ban gồm mọi ban từng có hiệu lực, kể cả ban được gỡ sớm và ban vĩnh viễn thủ công; không tính ban bị lật do khiếu nại. | Lần đầu: 30 ngày. Ban trước được Mod gỡ sau 5 ngày: lần này 90 ngày. Ban trước bị lật do khiếu nại: lần này 30 ngày. Đã có hai ban (một hết hạn, một được gỡ): lần này vĩnh viễn. |
| BR-M08-35 | Ràng buộc | "Ban vĩnh viễn" là thao tác riêng, bỏ qua cách tính leo thang, dùng cho vi phạm nghiêm trọng ngay lần đầu. | Người chưa từng bị ban, vi phạm nghiêm trọng: Mod chọn "Ban vĩnh viễn" → vĩnh viễn ngay. |
| BR-M08-36 | Kích hoạt | Người đang ở mức HEAVY lại bị xác định vi phạm (AI cho điểm ≥ 0,9, hoặc Mod kết luận vi phạm trong vụ) thì không nhận cảnh cáo mới. Vụ của nội dung đó được đánh dấu là yêu cầu ban (mở vụ nếu chưa có); Mod hoặc Admin quyết và chọn "Ban". AI không tự ban. | Lan có 6 cảnh cáo (HEAVY), chưa từng bị ban; bình luận mới của Lan được AI chấm 0,95: bình luận bị ẩn, không có cảnh cáo thứ 7, vụ của bình luận là yêu cầu ban; Mod chọn "Ban" → Lan bị ban 30 ngày. |
| BR-M08-37 | Kích hoạt | Ban tạm thời hết hạn thì tài khoản tự về ACTIVE ngay lúc hết hạn (M01). | Ban 30 ngày từ 01/10: tự về ACTIVE ngày 31/10. |
| BR-M08-38 | Sự kiện | Mod hoặc Admin gỡ ban thì tài khoản về ACTIVE ngay (M01). | — |
| BR-M08-39 | Sự kiện | Hệ thống ghi vào nhật ký kiểm duyệt mỗi thao tác: cảnh cáo, bỏ cảnh cáo do AI ra, ban, gỡ ban, ẩn nội dung, ẩn, khóa và mở khóa nhóm, kết luận vụ, vô hiệu hóa và kích hoạt lại Tag, đổi Topic/Tag trên bài người khác (M05); mỗi dòng gồm người làm (Mod, Admin hoặc AI), loại thao tác, đối tượng, lý do, thời điểm. Không ghi việc nhận và tự nhả vụ. Thao tác của Admin còn được ghi ở nhật ký thao tác Admin (M10). | — |
| BR-M08-40 | Ràng buộc | Nhật ký kiểm duyệt được giữ vĩnh viễn; dòng nhật ký không sửa, không xóa được. Người làm đã xóa tài khoản hiện "[Người dùng đã xóa]" nhưng vẫn tra được qua username. | — |
| BR-M08-41 | Ràng buộc | Quyền xem nhật ký: Admin xem toàn bộ và lọc được theo người làm (để theo dõi từng Mod, M10); Mod xem danh sách vụ mình đã xử lý; Mod xem thao tác của Mod khác chỉ khi đang xét khiếu nại về chính thao tác đó (M09). | — |
| BR-M08-42 | Sự kiện | Thời gian thử thách, thời hạn ban và các ngưỡng kiểm duyệt là hằng số chính sách: không đổi được qua giao diện, chỉ đổi qua triển khai. | — |
| BR-M08-43 | Ràng buộc | Mọi thời điểm hiển thị và mọi ranh giới ngày theo lịch tính theo giờ Việt Nam; các thời hạn tính bằng ngày (thời gian thử thách, thời hạn ban, cửa sổ 90 ngày) là đủ N × 24 giờ. | — |
| BR-M08-44 | Sự kiện | Nội dung trong nhóm vẫn báo cáo được và vẫn do Mod, Admin hệ thống xử lý; cổng duyệt của nhóm (M11) chỉ thêm vào, không thay thế. | — |
| BR-M08-45 | Ràng buộc | Bài đang ở mức Khóa toàn bộ vẫn báo cáo được. Bài trong nhóm đã chuyển Private không báo cáo được bởi người không phải thành viên (M11). | — |
| BR-M08-46 | Ràng buộc | Chỉ Admin cảnh cáo, ban tài khoản Mod. Vụ nhắm vào bài viết, bình luận hoặc tài khoản của một Mod chỉ Admin thấy, nhận và xử lý; các Mod khác không thấy vụ đó. Tài khoản Admin không bị cảnh cáo, ban. AI không tự cảnh cáo Mod, Admin; nội dung của Mod có điểm quét ≥ 0,9 được đưa vào vụ để Admin quyết. Mod, Admin không thấy, không nhận vụ nhắm vào bài viết, bình luận hoặc tài khoản của chính mình. | Bình luận của Mod M1 bị báo cáo: M1 và Mod M2 đều không thấy vụ trong hàng chờ; Admin nhận vụ, ẩn bình luận và cảnh cáo M1 được. Bình luận của M1 được quét 0,95: bị ẩn, không có cảnh cáo tự động, vụ chờ Admin quyết. |
| BR-M08-47 | Ràng buộc | Gửi báo cáo: không báo cáo được bài viết, bình luận, tài khoản của chính mình; khi đối tượng đang có vụ Mở, một người chỉ có một báo cáo trong vụ đó; người ở mức HEAVY vẫn báo cáo được; đối tượng không còn hiển thị với người báo cáo thì bị từ chối; báo cáo đã gửi không rút, không sửa được. | Minh báo cáo bài P lúc 10:00 (vụ V1 mở); báo cáo lại P lúc 10:30: bị từ chối. V1 kết luận lúc 11:00; Minh báo cáo P lúc 12:00: nhận, mở vụ V2. |
| BR-M08-48 | Sự kiện | Ẩn nội dung, cảnh cáo, ban, ẩn và khóa nhóm chỉ làm được trong một vụ mà người làm đang giữ; Mod tự phát hiện vi phạm thì báo cáo trước rồi nhận xử lý. Ngoại lệ: gỡ ban và mở khóa nhóm làm trực tiếp, không cần vụ. Báo cáo của người dùng không làm đổi trạng thái kiểm duyệt của bài viết, bình luận; chỉ AI quét lại (M03) mới làm bài Bị gắn cờ. | Bài P của Bình bị 3 người báo cáo: P vẫn hiển thị cho tới khi Mod kết luận. |
| BR-M08-49 | Kích hoạt | Các việc do AI phát hiện cần Mod xem trở thành mục do "Hệ thống (AI)" tạo trong hàng chờ báo cáo: bình luận bị AI ẩn với điểm 0,5–< 0,9; bài Bị gắn cờ sau khi quét lại; nội dung của Mod có điểm ≥ 0,9; yêu cầu ban (BR-M08-36). Đối tượng đang có vụ Mở thì mục được thêm vào vụ đó, không thì mở vụ mới. Lý do của mục là nhóm vi phạm AI phát hiện; mục tính là một báo cáo. | Bình luận C bị AI chấm Quấy rối 0,7, chưa có vụ: vụ mới, điểm 10 + 1 × 2 = 12. C đã có vụ với 2 báo cáo "Spam" (điểm 2 + 2 × 2 = 6): thêm mục AI, điểm max(2, 10) + 3 × 2 = 16. |
| BR-M08-50 | Ràng buộc | Vụ về một nhóm: người bị báo cáo là Owner. Mod, Admin đang giữ vụ có thể Ẩn nhóm hoặc Khóa nhóm, và có thể cảnh cáo, ban Owner theo BR-M08-46. Ẩn nhóm: nhóm và mọi nội dung không hiện với ai, kể cả thành viên và Owner; dữ liệu giữ nguyên; không có bỏ ẩn. Khóa nhóm: nhóm và nội dung cũ vẫn hiện như trước; đăng bài, bình luận, upvote, bình chọn poll, tham gia, mời thành viên bị chặn với mọi người, kể cả Owner và Group Mod, cùng các thao tác quản lý nhóm theo danh sách đầy đủ của M11 (BR-M11-28); lưu bài, báo cáo vẫn được; Mod, Admin mở khóa trực tiếp. Nhóm Bị khóa có thể bị Ẩn ở vụ sau; nhóm Bị ẩn không khóa, không mở khóa được. | Nhóm giả mạo bị Ẩn: biến mất với mọi người, không hiện lại. Nhóm có bắt nạt trong bình luận bị Khóa 1 tuần rồi Mod mở khóa: trong thời gian khóa vẫn đọc được, không ai đăng được. |
| BR-M08-51 | Tính toán | Điểm quét của một bài viết, bình luận = điểm cao nhất trong bốn nhóm vi phạm AI trả về; nhóm có điểm cao nhất là lý do của mục do AI tạo. | Quấy rối 0,92, Bạo lực 0,10, Thù ghét 0,05, Người lớn 0,01: điểm quét 0,92, lý do "Quấy rối/Bắt nạt". |
| BR-M08-52 | Ràng buộc | Không ban chồng: tài khoản đang có ban Đang hiệu lực thì không ban mới được; muốn đổi sang vĩnh viễn thì gỡ ban rồi chọn "Ban vĩnh viễn". | Lan đang bị ban 30 ngày; Mod chọn "Ban vĩnh viễn": bị từ chối. Mod gỡ ban rồi chọn "Ban vĩnh viễn": được; ban đã gỡ vẫn tính vào số lần đã bị ban. |
| BR-M08-53 | Sự kiện | Thao tác của Mod, Admin với tài khoản người vi phạm chỉ có cảnh cáo, "Ban" và "Ban vĩnh viễn". "Suspend" trong draft là ban tạm thời; không có thao tác suspend hay vô hiệu hóa tài khoản người khác. | — |
| BR-M08-54 | Sự kiện | Cảnh cáo bị Mod, Admin bỏ (cảnh cáo do AI ra) hoặc bị lật khi khiếu nại thành công (M09): số lần cảnh cáo giảm 1, mức tính lại theo số lần còn lại; bản ghi cảnh cáo giữ, đánh dấu "đã bỏ" hoặc "bị lật"; thời điểm kết thúc thời gian thử thách hiện tại không đổi. | Lan có 3 lần (MEDIUM, hết thử thách 09:00 20/10); Mod bỏ cảnh cáo AI thứ 3: Lan còn 2 lần, về LIGHT, vẫn hết thử thách 09:00 20/10. |
| BR-M08-55 | Ràng buộc | Không ai báo cáo được bài viết, bình luận, tài khoản của Admin, hay nhóm có Owner là Admin. Nội dung của Admin không bị AI quét: bài của Admin đăng không qua quét trước (M03), bình luận của Admin không được quét khi quét luồng. Hệ quả đã chấp nhận: nội dung của Admin không có kiểm duyệt hệ thống. | Minh bấm "Báo cáo" trên bình luận của Admin A → bị từ chối. Luồng có 12 trả lời, 2 trong đó của Admin A → khi quét luồng, 2 trả lời của A không được gửi quét. |

### 5.20 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Báo cáo | Người báo cáo (người dùng, hoặc "Hệ thống (AI)" với mục do AI tạo); loại đối tượng (bài viết, bình luận, người dùng, nhóm); đối tượng; một lý do (BR-M08-02); mô tả; bằng chứng (tối đa 3 ảnh); trạng thái (Mở, Đã xử lý); kết luận khi đã xử lý (Có xử lý, Bác bỏ) | Thuộc một Vụ báo cáo; người báo cáo là Tài khoản (M01); đối tượng là Bài viết (M03), Bình luận (M04), Tài khoản (M01) hoặc Nhóm (M11) |
| Vụ báo cáo | Loại đối tượng; đối tượng; các báo cáo; trạng thái (Mở, Đã xử lý); điểm ưu tiên; thời điểm mở; đánh dấu yêu cầu ban; người đang giữ; thời điểm thao tác cuối của người giữ; kết luận (Có xử lý, Bác bỏ); lý do kết luận; người kết luận; thời điểm kết luận | Gồm một hoặc nhiều Báo cáo; các vụ cùng đối tượng tạo thành lịch sử báo cáo của đối tượng; có thể dẫn tới Cảnh cáo, Ban, việc ẩn nội dung, ẩn hoặc khóa nhóm |
| Cảnh cáo | Người bị cảnh cáo; người ra (AI, Mod hoặc Admin); lý do; thời điểm; vụ hoặc nội dung liên quan; trạng thái (Đang tính, Đã bỏ, Bị lật) | Thuộc một Tài khoản (M01); có thể gắn với một Vụ báo cáo hoặc một lần quét AI; khiếu nại được một lần (M09) |
| Trạng thái cảnh cáo của người dùng | Số lần cảnh cáo; mức cảnh cáo (Sạch, LIGHT, MEDIUM, HEAVY); thời điểm kết thúc thời gian thử thách | Một cho mỗi Tài khoản (M01) |
| Ban | Người bị ban; loại (tạm thời, vĩnh viễn); thời hạn; thời điểm bắt đầu; lý do; người ban (Mod hoặc Admin); trạng thái (Đang hiệu lực, Hết hạn, Đã gỡ, Bị lật) | Thuộc một Tài khoản (M01); làm tài khoản chuyển BANNED; khiếu nại được một lần (M09) |
| Dòng nhật ký kiểm duyệt | Người làm (Mod, Admin hoặc AI); loại thao tác; đối tượng; lý do; thời điểm | Trỏ tới đối tượng của thao tác (bài viết, bình luận, tài khoản, nhóm, Tag, vụ báo cáo) |

<!-- Thuộc tính do M08 đặt trên thực thể của module khác: trạng thái kiểm duyệt của Bài viết (M03), của Bình luận (M04) và của
     Nhóm (M11: Bình thường, Bị khóa, Bị ẩn — DEC-194); dấu "đã quét với nội dung hiện tại" của Bình luận (DEC-077).
     "Người đang giữ", "thời điểm thao tác cuối" suy ra từ DEC-075, DEC-190. "Thời điểm mở" suy ra từ DEC-190 (bằng điểm thì vụ mở
     trước đứng trước). "Thời điểm kết luận" suy ra từ DEC-082, DEC-192 (báo cáo xử lý trong 90 × 24 giờ). "Người kết luận" suy ra từ
     DEC-081. Trạng thái Đã bỏ, Bị lật của Cảnh cáo từ DEC-188. Kết quả quét AI thô thuộc nhật ký quyết định AI (M13). -->

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Báo cáo | FR-M08-01.02; mục do AI: FR-M08-07.09, FR-M08-08.05, FR-M08-09.08, FR-M08-14.11 | FR-M08-04.01, FR-M08-04.09 | Trạng thái, kết luận: FR-M08-05.02; nội dung báo cáo: Không có (FR-M08-01.18) | Không có (FR-M08-01.18) |
| Vụ báo cáo | FR-M08-01.04, FR-M08-07.09, FR-M08-08.05 | FR-M08-02.01, FR-M08-04.01, FR-M08-17.02 | Giữ, nhả: FR-M08-03.01, FR-M08-03.04; kết luận: FR-M08-05.01; điểm ưu tiên: FR-M08-01.05; yêu cầu ban: FR-M08-14.11 | Không có (BR-M08-05: vụ đã kết luận giữ làm lịch sử) |
| Cảnh cáo | FR-M08-09.01, FR-M08-10.01 | FR-M08-04.05, FR-M08-13.01 | Bỏ: FR-M08-11.01, FR-M08-11.04; lật khi khiếu nại thành công: M09 | Không có (FR-M08-11.04: bản ghi giữ, đánh dấu) |
| Trạng thái cảnh cáo của người dùng | FR-M08-09.04, FR-M08-10.02 | FR-M08-04.05, FR-M08-13.01; M03, M04, M06, M12 đọc để áp hạn chế | FR-M08-09.04, FR-M08-10.02, FR-M08-12.01, FR-M08-12.04, FR-M08-11.03; M09 | Không có (một cho mỗi tài khoản) |
| Ban | FR-M08-14.01, FR-M08-14.02 | M01 (màn hình tài khoản bị khóa) | Gỡ: FR-M08-15.01; hết hạn: FR-M08-14.08; lật: M09 | Không có (bản ghi giữ, đánh dấu bị lật khi khiếu nại thành công) |
| Dòng nhật ký kiểm duyệt | FR-M08-16.01, FR-M08-16.02, FR-M08-16.05 | FR-M08-17.01, FR-M08-17.02, FR-M08-17.03 | Không có (FR-M08-16.06) | Không có (FR-M08-16.03) |
| Trạng thái kiểm duyệt của nhóm (thuộc tính của Nhóm, M11) | M11 (nhóm mới ở Bình thường) | M11 áp hiển thị, chặn thao tác | FR-M08-18.01, FR-M08-18.04, FR-M08-18.07 | Không có |

### 5.21 Chuyển trạng thái

#### Báo cáo

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người dùng gửi báo cáo, hoặc hệ thống tạo mục do AI phát hiện | Với người dùng: đã đăng nhập, không phải nội dung của mình, chưa có báo cáo trong vụ đang Mở, lý do, mô tả, bằng chứng hợp lệ (BR-M08-02 đến BR-M08-04, BR-M08-47) | Mở | FR-M08-01.02, FR-M08-08.05, FR-M08-07.09 |
| Mở | Vụ chứa báo cáo được kết luận | — | Đã xử lý | FR-M08-05.02 |

#### Vụ báo cáo

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Có báo cáo hoặc mục do AI tạo về một đối tượng | Đối tượng chưa có vụ Mở (BR-M08-05) | Mở, chưa ai giữ | FR-M08-01.04, FR-M08-07.09, FR-M08-08.05 |
| Mở, chưa ai giữ | Mod hoặc Admin chọn "Nhận xử lý" | Vụ không nhắm vào chính người nhận | Mở, đang được giữ | FR-M08-03.01, FR-M08-03.07 |
| Mở, đang được giữ | Người giữ không thao tác 30 phút | — | Mở, chưa ai giữ | FR-M08-03.04, FR-M08-03.08 |
| Mở, đang được giữ | Người giữ kết luận Có xử lý hoặc Bác bỏ | Có lý do kết luận | Đã xử lý | FR-M08-05.01, FR-M08-05.09 |

#### Mức cảnh cáo của người dùng

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Tài khoản được tạo (M01) | — | Sạch | M01 |
| Sạch | Nhận cảnh cáo | — | LIGHT | FR-M08-09.04, FR-M08-10.02 |
| LIGHT | Nhận cảnh cáo | Số lần cảnh cáo trở thành 3 | MEDIUM | FR-M08-09.04, FR-M08-10.02 |
| MEDIUM | Nhận cảnh cáo | Số lần cảnh cáo trở thành 5 | HEAVY | FR-M08-09.04, FR-M08-10.02 |
| LIGHT | Nhận cảnh cáo | Mức không đổi | LIGHT (đặt lại thời gian thử thách) | FR-M08-09.04, FR-M08-10.02 |
| MEDIUM | Nhận cảnh cáo | Mức không đổi | MEDIUM (đặt lại thời gian thử thách) | FR-M08-09.04, FR-M08-10.02 |
| HEAVY | Vi phạm tiếp | — | HEAVY (không cảnh cáo mới; vụ thành yêu cầu ban) | FR-M08-09.11, FR-M08-10.10, FR-M08-14.11 |
| HEAVY | Hết thời gian thử thách | — | MEDIUM (4 lần) | FR-M08-12.01, FR-M08-12.04 |
| MEDIUM | Hết thời gian thử thách | — | LIGHT (2 lần) | FR-M08-12.01, FR-M08-12.04 |
| LIGHT | Hết thời gian thử thách | — | Sạch (0 lần) | FR-M08-12.01, FR-M08-12.04 |
| LIGHT | Bỏ cảnh cáo AI, hoặc khiếu nại cảnh cáo thành công (M09) | Số lần còn lại là 0 | Sạch | FR-M08-11.03; M09 |
| MEDIUM | Bỏ cảnh cáo AI, hoặc khiếu nại cảnh cáo thành công (M09) | Số lần còn lại là 2 | LIGHT | FR-M08-11.03; M09 |
| HEAVY | Bỏ cảnh cáo AI, hoặc khiếu nại cảnh cáo thành công (M09) | Số lần còn lại là 4 | MEDIUM | FR-M08-11.03; M09 |

#### Ban

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Mod hoặc Admin đang giữ vụ chọn "Ban" hoặc "Ban vĩnh viễn" | Tài khoản không có ban Đang hiệu lực; người bị ban không phải Admin; người bị ban là Mod thì người ban là Admin | Đang hiệu lực | FR-M08-14.01, FR-M08-14.02, FR-M08-14.13 |
| Đang hiệu lực | Hết thời hạn (M01) | Ban tạm thời | Hết hạn | FR-M08-14.08 |
| Đang hiệu lực | Mod hoặc Admin gỡ ban | — | Đã gỡ | FR-M08-15.01 |
| Đang hiệu lực | Khiếu nại ban thành công (M09) | — | Bị lật | M09 |

#### Trạng thái kiểm duyệt của bài viết (phần M08)

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| Bình thường | Quét lại sau khi sửa cho điểm ≥ 0,5 (M03) | — | Bị gắn cờ | M03; FR-M08-07.09 |
| Bị gắn cờ | Mod, Admin xét và giữ bài | — | Bình thường | FR-M08-07.01 |
| Bị gắn cờ | Mod, Admin xét và ẩn bài | — | Bị ẩn | FR-M08-07.02 |
| Bình thường | Mod, Admin ẩn bài khi xử lý vụ | — | Bị ẩn | FR-M08-06.01 |
| Bị ẩn | Khiếu nại bài bị gỡ thành công (M09) | — | Bình thường | M09 |

#### Trạng thái kiểm duyệt của bình luận (phần M08)

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| Bình thường | Quét luồng cho điểm ≥ 0,9 | — | Bị ẩn | FR-M08-08.04 |
| Bình thường | Quét luồng cho điểm từ 0,5 đến dưới 0,9 | Bình luận vào vụ trong hàng chờ | Bị ẩn | FR-M08-08.05 |
| Bị ẩn | Mod, Admin xét bình luận đang chờ và kết luận không vi phạm | Bình luận vào hàng chờ do điểm từ 0,5 đến dưới 0,9 | Bình thường | FR-M08-07.03 |
| Bình thường | Mod, Admin ẩn bình luận khi xử lý vụ | — | Bị ẩn | FR-M08-06.02 |

#### Trạng thái kiểm duyệt của nhóm

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Nhóm được tạo (M11) | — | Bình thường | M11 |
| Bình thường | Mod, Admin đang giữ vụ về nhóm chọn "Khóa nhóm" | — | Bị khóa | FR-M08-18.04 |
| Bị khóa | Mod, Admin mở khóa nhóm | — | Bình thường | FR-M08-18.07 |
| Bình thường | Mod, Admin đang giữ vụ về nhóm chọn "Ẩn nhóm" | — | Bị ẩn | FR-M08-18.01 |
| Bị khóa | Mod, Admin đang giữ một vụ sau về nhóm chọn "Ẩn nhóm" | — | Bị ẩn | FR-M08-18.08 |

<!-- Báo cáo: Đã xử lý là trạng thái cuối. Vụ: Đã xử lý là trạng thái cuối, không mở lại (BR-M08-05).
     Ban: Hết hạn, Đã gỡ, Bị lật là trạng thái cuối của bản ghi ban; tài khoản về ACTIVE (M01).
     Báo cáo của người dùng không đổi trạng thái kiểm duyệt của bài viết, bình luận (BR-M08-48); dòng "báo cáo gắn cờ bài" đã bỏ theo DEC-190.
     Bị ẩn của bình luận do điểm ≥ 0,9 hoặc do Mod ẩn là trạng thái cuối (bình luận không có khiếu nại); không hiện lại khi cảnh cáo,
     ban liên quan bị lật trên khiếu nại (DEC-201, M09).
     Nhóm Bị ẩn là trạng thái cuối: không có bỏ ẩn (FR-M08-18.03, FR-M08-18.09).
     "HEAVY → vi phạm tiếp" không đổi mức cảnh cáo; sau khi bị ban, mức cảnh cáo vẫn chạy theo thời gian thử thách. -->

### 5.22 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Cung cấp | M01 | Ban làm tài khoản chuyển BANNED, gỡ ban đưa về ACTIVE; lý do ban cho màn hình tài khoản bị khóa | FR-M08-14.01, FR-M08-14.03, FR-M08-15.01 |
| Dùng | M01 | Trạng thái tài khoản; ban tạm thời hết hạn thì tài khoản tự về ACTIVE; người làm đã xóa tài khoản tra cứu qua username; danh tính tác giả đã vô hiệu hóa | FR-M08-14.08, FR-M08-16.04, FR-M08-04.06 |
| Cung cấp | M02 | Mức cảnh cáo không hiện trên hồ sơ; xử lý báo cáo người dùng chỉ bằng cảnh cáo hoặc ban, không gỡ, sửa avatar, bio | FR-M08-13.03, FR-M08-10.06 |
| Cung cấp | M03 | Trạng thái kiểm duyệt của bài sau khi Mod xét, ẩn; báo cáo không đổi trạng thái của bài; mức cảnh cáo MEDIUM, HEAVY để chặn tạo bài mới; nhánh cảnh cáo khi M03 quét bài | FR-M08-06.01, FR-M08-07.01, FR-M08-07.02, FR-M08-07.10, FR-M08-09.01, FR-M08-12.02 |
| Dùng | M03 | Điểm quét bài khi gửi và khi quét lại; bài Bị gắn cờ được đưa vào vụ; bài đã xóa, đã xóa hẳn, tự ẩn được giữ để xem trong vụ | FR-M08-04.02, FR-M08-07.09, FR-M08-09.01 |
| Cung cấp | M04 | Trạng thái kiểm duyệt của bình luận sau khi quét, xét, ẩn; mức HEAVY để chặn tạo bình luận mới | FR-M08-06.02, FR-M08-07.03, FR-M08-08.04, FR-M08-08.05, FR-M08-12.02 |
| Dùng | M04 | Bình luận và luồng bình luận để quét; nội dung bình luận đã xóa được giữ để xem trong vụ | FR-M08-04.02, FR-M08-08.01 |
| Cung cấp | M05 | Nhật ký kiểm duyệt ghi việc vô hiệu hóa, kích hoạt lại Tag và đổi Topic, Tag trên bài người khác | FR-M08-16.02 |
| Cung cấp | M06 | Mức HEAVY để giảm hạng tìm kiếm nội dung hiện có ×0,5 | FR-M08-09.04, FR-M08-10.02 |
| Cung cấp | M07 | Sự kiện thông báo: kết quả báo cáo cho người báo cáo và người bị báo cáo, cảnh cáo, ban và gỡ ban (kèm email), "Bình luận của bạn đã bị ẩn" | FR-M08-05.04, FR-M08-05.05, FR-M08-08.07, FR-M08-09.05, FR-M08-10.03, FR-M08-14.04, FR-M08-15.02, FR-M08-18.11 |
| Cung cấp | M09 | Cảnh cáo, ban, kết luận vụ để khiếu nại; đường dẫn khiếu nại chỉ cho cảnh cáo, ban, bài bị ẩn; nhật ký cho Mod xét khiếu nại về thao tác của Mod khác | FR-M08-05.11, FR-M08-17.03 |
| Dùng | M09 | Khiếu nại thành công lật cảnh cáo (giảm số lần), lật ban (về ACTIVE, không tính vào số lần đã bị ban), hiện lại bài bị gỡ | FR-M08-14.12 |
| Dùng | M10 | Công tắc AI tổng và công tắc Moderation; việc thu hồi vai trò Mod khi Mod bị ban | FR-M08-08.10, FR-M08-09.07, FR-M08-14.05 |
| Cung cấp | M10 | Sự kiện ban một tài khoản Mod để M10 thu hồi vai trò Mod; nhật ký kiểm duyệt lọc theo người làm để Admin theo dõi Mod | FR-M08-14.05, FR-M08-17.06 |
| Dùng | M16 | Tin nhắn chat chưa báo cáo được, không bị quét AI ở MS1 (TBD-M08-01); nội dung tin bị thu hồi được giữ (xóa mềm) cho báo cáo tin nhắn ở phase sau | — |
| Cung cấp | M11 | Trạng thái kiểm duyệt của nhóm (Bình thường, Bị khóa, Bị ẩn) để M11 ẩn nhóm, chặn thao tác trong nhóm bị khóa | FR-M08-18.02, FR-M08-18.05, FR-M08-18.06 |
| Dùng | M11 | Nhóm là đối tượng báo cáo, Owner là người bị báo cáo; nhóm Private chặn báo cáo của người ngoài; danh tính thật của bài ẩn danh | FR-M08-01.11, FR-M08-04.06, FR-M08-04.10 |
| Cung cấp | M12 | Nội dung bị Mod, Admin gỡ vì vi phạm (để trừ điểm ngay); bình luận bị AI tự ẩn với điểm quét ≥ 0,9 (trừ điểm ngay) và kết luận của Mod, Admin với bình luận bị AI ẩn 0,5–< 0,9 (vi phạm thì trừ điểm, DEC-241); mức HEAVY và tài khoản BANNED (loại khỏi bảng xếp hạng, nhãn "Tài khoản đã bị khóa") | FR-M08-06.01, FR-M08-06.02, FR-M08-09.04, FR-M08-14.03, FR-M08-08.04, FR-M08-07.03, FR-M08-07.04 |
| Dùng | M13 | Gọi AI kiểm duyệt, điểm bốn nhóm vi phạm, thời gian chờ và một lần thử lại; nhật ký quyết định AI | FR-M08-08.01, FR-M08-08.09, FR-M08-08.11 |
| Cung cấp | M15 | Dữ liệu báo cáo, kết luận, cảnh cáo (kèm mức đạt sau cảnh cáo), ban, gỡ ban cho thống kê kiểm duyệt; mức cảnh cáo của tài khoản cho thống kê người dùng | FR-M08-05.01, FR-M08-09.01, FR-M08-09.04, FR-M08-10.01, FR-M08-10.02, FR-M08-14.01, FR-M08-15.01 |
| Cung cấp | M13 | Kích hoạt quét luồng bình luận theo tốc độ trả lời (bình luận của Admin không gửi quét) | FR-M08-08.01, FR-M08-08.12 |
| Cung cấp | M14 | Mức cảnh cáo không hiện trên bài ở feed và không làm bài bị loại hay hạ điểm Trending Post; báo cáo bài từ feed theo luồng báo cáo chung | FR-M08-13.03, FR-M08-01.01 |

### 5.23 AI hỗ trợ và hành vi khi tắt AI

- Khi AI bật (công tắc AI tổng và công tắc Moderation đều bật): quét luồng bình luận khi số trả lời đạt ngưỡng tốc độ
  (FR-M08-08.01, FR-M08-08.04 đến FR-M08-08.06); điểm quét là điểm cao nhất trong bốn nhóm (FR-M08-08.11); tự cảnh cáo khi điểm
  quét ≥ 0,9, để Mod quyết khi từ 0,5 đến dưới 0,9 (FR-M08-09.01, FR-M08-09.02); cùng ngưỡng cho mọi tác giả (FR-M08-09.10).
  Nội dung AI gắn cờ cần Mod xem trở thành mục do "Hệ thống (AI)" tạo trong hàng chờ báo cáo (FR-M08-07.09, FR-M08-08.05).
  AI không bao giờ ban (FR-M08-09.06, FR-M08-14.06) và không tự cảnh cáo Mod, Admin (FR-M08-09.08, FR-M08-09.09).
- Khi AI tắt: không quét bình luận, không tự cảnh cáo (FR-M08-08.10, FR-M08-09.07); kiểm duyệt chỉ dựa vào báo cáo và hàng chờ
  báo cáo vẫn hoạt động (FR-M08-02.05).
- Khi AI lỗi lúc quét bình luận: bình luận giữ nguyên, lỗi được ghi cho Admin (FR-M08-08.09).
- Quét bài trước khi đăng và khi quét lại thuộc M03; cách gọi AI, thời gian chờ, thử lại thuộc M13.

### 5.24 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.25 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-15 | Tạo mới | Phạm Văn Đức |
| 1.0 | 2026-10-15 | Chốt sau 7 bước; câu trả lời bước 6 ghi ở DEC-186–DEC-194, QA-352–QA-369, ISS-292–ISS-309; thêm FR-M08-18 Ẩn, khóa nhóm (mở rộng phạm vi) | Phạm Văn Đức |
| 1.1 | 2026-10-20 | Đối chiếu với FR-M06: ghi cách M06 áp giảm hạng ×0,5 (DEC-211) ở C.2; không đổi yêu cầu. Chốt bản 1.1 | Phạm Văn Đức |
| 1.2 | 2026-10-21 | Đối chiếu với FR-M10 (DEC-224, DEC-227): Admin lọc nhật ký kiểm duyệt theo người làm (FR-M08-17.06, BR-M08-41); thêm dòng "Cung cấp M10"; C.1, C.2. Chốt bản 1.2 | Phạm Văn Đức |
| 1.3 | 2026-10-23 | Rà lại với register tới DEC-247: không báo cáo được Admin, vụ về Mod chỉ Admin xử lý, bình luận của Admin không bị quét (DEC-195: BR-M08-46, BR-M08-55, FR-M08-01.20, FR-M08-02.09, FR-M08-03.09, FR-M08-08.12); thông báo cảnh cáo kèm đường dẫn khiếu nại (DEC-197); đóng TBD-M08-03 (DEC-201), thu hẹp TBD-M08-02 (DEC-239); dòng Cung cấp M12 thêm bình luận bị AI ẩn (DEC-241); thêm dòng Cung cấp M13 khớp FR-M13. Chốt bản 1.3 | Phạm Văn Đức |
| 1.4 | 2026-10-24 | Đối chiếu với FR-M16: đóng TBD-M08-02 (DEC-248: thu hồi tin nhắn là xóa mềm); dòng Dùng M16; C.1 OPEN-011, C.2. Không đổi yêu cầu. Chốt bản 1.4 | Phạm Văn Đức |
| 1.5 | 2026-10-24 | Đối chiếu với FR-M14: thêm dòng Cung cấp M14 (mức cảnh cáo riêng tư ở feed, báo cáo bài từ feed) và dòng M14 ở mục 3.2; không đổi yêu cầu. Chốt bản 1.5 | Phạm Văn Đức |
| 1.6 | 2026-10-24 | Đối chiếu với FR-M15: dòng Cung cấp M15 thêm mức cảnh cáo của tài khoản (cùng mức đạt sau mỗi cảnh cáo) và gỡ ban; sửa mục 3.2; không đổi yêu cầu. Chốt bản 1.6 | Phạm Văn Đức |
| 1.7 | 2026-10-24 | Rà soát chéo toàn bộ FR (review-cross-module.md): FR-M08-18.05, BR-M08-50 trỏ danh sách thao tác bị chặn khi nhóm Bị khóa sang BR-M11-28 (DEC-235); C.1, C.2. Chốt bản 1.7 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M08-01 | DEC-072, DEC-073, DEC-076, DM-1.3, QA-011, GL:USER, MR-M08 | Nói thẳng | — |
| FR-M08-01.01 | DEC-072 | Nói thẳng | — |
| FR-M08-01.02 | DEC-076, DEC-072 | Nói thẳng | — |
| FR-M08-01.03 | DEC-076 | Nói thẳng | — |
| FR-M08-01.04 | DEC-076 | Nói thẳng | — |
| FR-M08-01.05 | DEC-075 | Suy ra | Điểm ưu tiên phụ thuộc lý do và số báo cáo trong vụ ⇒ mỗi báo cáo mới làm đổi điểm |
| FR-M08-01.06 | DEC-072, QA-011 | Nói thẳng | — |
| FR-M08-01.07 | DEC-072, DEC-073 | Suy ra | Mô tả chỉ bắt buộc khi lý do là "Khác" ⇒ mỗi báo cáo phải có lý do |
| FR-M08-01.08 | DEC-073 | Nói thẳng | — |
| FR-M08-01.09 | DEC-073 | Suy ra | "max 3 images" ⇒ từ chối ảnh thứ 4 |
| FR-M08-01.10 | DEC-073, DEC-130 | Suy ra | "5MB/file" và whitelist ảnh ⇒ từ chối ảnh vượt giới hạn hoặc sai định dạng |
| FR-M08-01.11 | DEC-108 | Nói thẳng | — |
| FR-M08-01.12 | DEC-191, QA-363 | Nói thẳng | — |
| FR-M08-01.13 | DEC-167 | Nói thẳng | — |
| FR-M08-01.14 | DEC-077 | Nói thẳng | DEC-077 "Report system works independently of velocity/scan status at all times" |
| FR-M08-01.15 | DEC-191, QA-364 | Nói thẳng | — |
| FR-M08-01.16 | DEC-191, QA-364 | Nói thẳng | — |
| FR-M08-01.17 | DEC-191, QA-364 | Nói thẳng | — |
| FR-M08-01.18 | DEC-191, QA-368 | Nói thẳng | — |
| FR-M08-01.19 | DEC-190, QA-357 | Nói thẳng | — |
| FR-M08-01.20 | DEC-195 | Nói thẳng | — |
| FR-M08-02 | DEC-075, DEC-076, DEC-090, DM-1.3, MR-FB-M08, MR-M08 | Nói thẳng | — |
| FR-M08-02.01 | DEC-075, DEC-090, DEC-190 | Nói thẳng | — |
| FR-M08-02.02 | DEC-075 | Suy ra | Vụ đang được giữ thì người khác không nhận được (BR-M08-08) ⇒ hàng chờ phải cho biết vụ nào đang được giữ |
| FR-M08-02.03 | DEC-075 | Nói thẳng | DEC-075 "No SLA deadline" |
| FR-M08-02.04 | DEC-090, DM-1.3 | Suy ra | Chỉ Mod, Admin xử lý báo cáo ⇒ người khác bị từ chối |
| FR-M08-02.05 | DEC-008, DEC-099, MR-FB-M08 | Nói thẳng | — |
| FR-M08-02.06 | DEC-189, QA-355, QA-365 | Nói thẳng | — |
| FR-M08-02.07 | DEC-190, QA-357 | Nói thẳng | — |
| FR-M08-02.08 | DEC-190, DEC-187 | Nói thẳng | — |
| FR-M08-02.09 | DEC-195 | Nói thẳng | — |
| FR-M08-03 | DEC-075 | Nói thẳng | Nhả tự động sau 30 phút không thao tác thuộc cùng chức năng |
| FR-M08-03.01 | DEC-075 | Nói thẳng | — |
| FR-M08-03.02 | DEC-075 | Suy ra | "lock a case" ⇒ không ai khác nhận được vụ đang khóa |
| FR-M08-03.03 | DEC-075 | Suy ra | Nhận xử lý là cách chia vụ giữa các Mod ⇒ chỉ người giữ xử lý vụ |
| FR-M08-03.04 | DEC-075, DEC-190 | Nói thẳng | — |
| FR-M08-03.05 | DEC-076 | Suy ra | Vụ đã kết luận không mở lại (BR-M08-05) ⇒ không nhận lại được |
| FR-M08-03.06 | DEC-090, DM-1.3 | Suy ra | Chỉ Mod, Admin xử lý báo cáo |
| FR-M08-03.07 | DEC-189, QA-355, QA-365 | Nói thẳng | — |
| FR-M08-03.08 | DEC-190, QA-365 | Nói thẳng | — |
| FR-M08-03.09 | DEC-195 | Nói thẳng | — |
| FR-M08-04 | DEC-076, DEC-079, DEC-082, DEC-168, DEC-179, DEC-184, DEC-185 | Nói thẳng | — |
| FR-M08-04.01 | DEC-076 | Nói thẳng | — |
| FR-M08-04.02 | DEC-179, DEC-184, DEC-185 | Nói thẳng | — |
| FR-M08-04.03 | DEC-076 | Nói thẳng | — |
| FR-M08-04.04 | DEC-082, DEC-192 | Nói thẳng | — |
| FR-M08-04.05 | DEC-079, DEC-080 | Suy ra | Trạng thái cảnh cáo hiện với Mod (DEC-079); mức HEAVY quyết định việc chuyển sang ban (DEC-080) ⇒ Mod cần thấy mức khi xử lý |
| FR-M08-04.06 | QA-015, DEC-150 | Nói thẳng | — |
| FR-M08-04.07 | DEC-179, DEC-184, DEC-185, DEC-168 | Nói thẳng | — |
| FR-M08-04.08 | DEC-090, DM-1.3 | Suy ra | Chỉ Mod, Admin xử lý báo cáo |
| FR-M08-04.09 | DEC-190, DEC-186 | Nói thẳng | — |
| FR-M08-04.10 | DEC-194, QA-369 | Nói thẳng | — |
| FR-M08-05 | DEC-074, DEC-076, DM-1.3, DEC-090 | Nói thẳng | — |
| FR-M08-05.01 | DEC-076, DEC-081, DEC-082 | Nói thẳng | Người kết luận, thời điểm kết luận suy ra từ DEC-081 (danh sách vụ Mod đã xử lý), DEC-082 (báo cáo xử lý trong 90 ngày) |
| FR-M08-05.02 | DEC-076 | Nói thẳng | — |
| FR-M08-05.03 | DEC-076 | Nói thẳng | — |
| FR-M08-05.04 | DEC-074, DEC-076, DEC-192, DEC-065 | Nói thẳng | — |
| FR-M08-05.05 | DEC-074, DEC-065 | Nói thẳng | — |
| FR-M08-05.06 | DEC-179 | Nói thẳng | — |
| FR-M08-05.07 | DEC-075 | Suy ra | Chỉ người giữ vụ xử lý vụ (khóa vụ) |
| FR-M08-05.08 | DEC-076 | Suy ra | Vụ đã kết luận không mở lại (BR-M08-05) |
| FR-M08-05.09 | DEC-192, QA-362 | Nói thẳng | — |
| FR-M08-05.10 | DEC-192, QA-362 | Nói thẳng | — |
| FR-M08-05.11 | DEC-192, DEC-115 | Nói thẳng | — |
| FR-M08-06 | DM-10.2, DEC-161, DEC-180, GL:Moderator (MOD), DEC-190 | Nói thẳng | — |
| FR-M08-06.01 | DEC-161, DM-10.2 | Nói thẳng | — |
| FR-M08-06.02 | DEC-180, DM-10.2 | Nói thẳng | — |
| FR-M08-06.03 | DEC-161, DEC-180 | Nói thẳng | — |
| FR-M08-06.04 | DM-10.2, DEC-090 | Suy ra | Thao tác ẩn chỉ có ở Mod, Admin |
| FR-M08-06.05 | DEC-161, DEC-180 | Suy ra | Bị ẩn là trạng thái đích của thao tác ẩn ⇒ ẩn lại là thao tác trùng |
| FR-M08-06.06 | DEC-190, QA-356 | Nói thẳng | — |
| FR-M08-07 | DEC-032, DEC-077, DEC-098, DEC-161, DEC-168, DEC-190 | Nói thẳng | — |
| FR-M08-07.01 | DEC-032, DEC-161 | Nói thẳng | — |
| FR-M08-07.02 | DEC-032, DEC-161 | Nói thẳng | — |
| FR-M08-07.03 | DEC-098, DEC-077 | Suy ra | DEC-098 "hold for mod review" ⇒ Mod xét không vi phạm thì bình luận hiện lại |
| FR-M08-07.04 | DEC-098, DEC-077 | Suy ra | Mod xét và xác nhận vi phạm ⇒ bình luận tiếp tục bị ẩn |
| FR-M08-07.05 | DEC-078, DEC-098 | Nói thẳng | — |
| FR-M08-07.06 | DEC-168 | Nói thẳng | — |
| FR-M08-07.07 | DEC-161, DEC-098 | Suy ra | Chỉ nội dung Bị gắn cờ hoặc bình luận đang chờ mới có đường chuyển trạng thái ở 5.21 |
| FR-M08-07.08 | DEC-090, DM-1.3 | Suy ra | Chỉ Mod, Admin kiểm duyệt nội dung |
| FR-M08-07.09 | DEC-190, QA-361 | Nói thẳng | — |
| FR-M08-07.10 | DEC-190, QA-360 | Nói thẳng | — |
| FR-M08-08 | DEC-077, DEC-098, DEC-099, DEC-008, QA-017, DM-11.1, MR-FB-M08, GL:AI Moderation | Nói thẳng | — |
| FR-M08-08.01 | DEC-077, DEC-093, DEC-186 | Nói thẳng | — |
| FR-M08-08.02 | DEC-077, QA-017 | Nói thẳng | DEC-077 thay phần bình luận của QA-017 |
| FR-M08-08.03 | DEC-077 | Nói thẳng | — |
| FR-M08-08.04 | DEC-098 | Nói thẳng | — |
| FR-M08-08.05 | DEC-098, DEC-077, DEC-190 | Nói thẳng | — |
| FR-M08-08.06 | DEC-098 | Nói thẳng | — |
| FR-M08-08.07 | DEC-180, DEC-065 | Nói thẳng | — |
| FR-M08-08.08 | DEC-077 | Suy ra | DEC-077 chỉ quét bình luận "not yet scanned with current content version" ⇒ phải ghi nhận đã quét |
| FR-M08-08.09 | DEC-099 | Nói thẳng | — |
| FR-M08-08.10 | DEC-008, DEC-093, DEC-099 | Nói thẳng | — |
| FR-M08-08.11 | DEC-186, QA-366 | Nói thẳng | — |
| FR-M08-08.12 | DEC-195 | Nói thẳng | — |
| FR-M08-09 | DEC-078, DEC-098, QA-019 | Nói thẳng | — |
| FR-M08-09.01 | DEC-078, DEC-098 | Nói thẳng | — |
| FR-M08-09.02 | DEC-078, DEC-098 | Nói thẳng | — |
| FR-M08-09.03 | DEC-098 | Nói thẳng | — |
| FR-M08-09.04 | DEC-079, QA-020, DEC-188 | Nói thẳng | — |
| FR-M08-09.05 | DEC-065, DEC-078, DEC-197 | Nói thẳng | — |
| FR-M08-09.06 | DEC-078, DEC-080, QA-019 | Nói thẳng | — |
| FR-M08-09.07 | DEC-093, DEC-099 | Nói thẳng | — |
| FR-M08-09.08 | DEC-186, DEC-189, DEC-190 | Nói thẳng | Việc đưa vào vụ suy từ DEC-190: mọi xử lý qua vụ |
| FR-M08-09.09 | DEC-186, DEC-189 | Nói thẳng | — |
| FR-M08-09.10 | DEC-186, QA-352 | Nói thẳng | — |
| FR-M08-09.11 | DEC-187, QA-354 | Nói thẳng | — |
| FR-M08-09.12 | DEC-186, QA-366 | Nói thẳng | — |
| FR-M08-10 | DEC-078, DEC-079, DEC-082, DEC-177, DM-10.2, QA-019 | Nói thẳng | — |
| FR-M08-10.01 | DEC-078, DEC-098, DEC-190 | Nói thẳng | — |
| FR-M08-10.02 | DEC-079, QA-020, DEC-188 | Nói thẳng | — |
| FR-M08-10.03 | DEC-065, DEC-074, DEC-197 | Nói thẳng | — |
| FR-M08-10.04 | DEC-082 | Nói thẳng | — |
| FR-M08-10.05 | DEC-082 | Nói thẳng | — |
| FR-M08-10.06 | DEC-177 | Nói thẳng | — |
| FR-M08-10.07 | DEC-090, DEC-078 | Suy ra | Chỉ AI, Mod, Admin ra cảnh cáo; người dùng thường không có thao tác này |
| FR-M08-10.08 | DEC-189, QA-355 | Nói thẳng | — |
| FR-M08-10.09 | DEC-189, QA-355 | Nói thẳng | — |
| FR-M08-10.10 | DEC-187, QA-354 | Nói thẳng | — |
| FR-M08-10.11 | DEC-190, QA-356 | Nói thẳng | — |
| FR-M08-11 | QA-019 | Nói thẳng | QA-019 "Override AI warn: MOD ✓, ADMIN ✓" |
| FR-M08-11.01 | QA-019 | Nói thẳng | QA-019 "Override AI warn: MOD ✓, ADMIN ✓" |
| FR-M08-11.02 | QA-019 | Suy ra | Chỉ Mod, Admin có quyền bỏ cảnh cáo do AI ra |
| FR-M08-11.03 | DEC-188, QA-366 | Nói thẳng | — |
| FR-M08-11.04 | DEC-188, QA-366 | Nói thẳng | — |
| FR-M08-11.05 | DEC-188, QA-366 | Nói thẳng | — |
| FR-M08-12 | QA-020, DEC-079 | Nói thẳng | Cơ chế tự giảm mức từ QA-020; thời gian thử thách 7/10/15 ngày từ DEC-079 |
| FR-M08-12.01 | QA-020, DEC-079, DEC-188 | Nói thẳng | — |
| FR-M08-12.02 | DEC-079 | Suy ra | Hạn chế gắn với mức (DEC-079) ⇒ đổi mức thì đổi hạn chế |
| FR-M08-12.03 | DEC-188, QA-358 | Nói thẳng | — |
| FR-M08-12.04 | DEC-188, QA-358 | Nói thẳng | — |
| FR-M08-12.05 | DEC-188, QA-358 | Nói thẳng | — |
| FR-M08-13 | DEC-079 | Nói thẳng | DEC-079 "visible only to the user themselves and to mods" |
| FR-M08-13.01 | DEC-079, DEC-086 | Suy ra | DEC-079 "visible only to the user themselves"; thời điểm kết thúc thời gian thử thách là hạn khiếu nại cảnh cáo (DEC-086) ⇒ người dùng cần thấy |
| FR-M08-13.02 | DEC-079 | Nói thẳng | Phần Admin suy ra: Admin có quyền của Mod |
| FR-M08-13.03 | DEC-079 | Nói thẳng | — |
| FR-M08-14 | DEC-080, DEC-090, QA-019, DM-10.2, DEC-177 | Nói thẳng | — |
| FR-M08-14.01 | DEC-080, QA-019, DEC-190 | Nói thẳng | — |
| FR-M08-14.02 | DEC-080 | Nói thẳng | — |
| FR-M08-14.03 | DEC-018, QA-018 | Nói thẳng | — |
| FR-M08-14.04 | DEC-065, DEC-085, QA-019 | Nói thẳng | — |
| FR-M08-14.05 | QA-013, DEC-189 | Nói thẳng | QA-013 "Auto-revoke khi MODERATOR bị ban"; việc đổi vai trò thực hiện ở M10 |
| FR-M08-14.06 | DEC-078, DEC-080 | Nói thẳng | — |
| FR-M08-14.07 | QA-019, DEC-090 | Suy ra | QA-019 "Ban/Unban: cả MOD và ADMIN" ⇒ người khác bị từ chối |
| FR-M08-14.08 | DEC-152 | Nói thẳng | Tài khoản về ACTIVE do M01 |
| FR-M08-14.09 | DEC-189, QA-355 | Nói thẳng | — |
| FR-M08-14.10 | DEC-189, QA-355 | Nói thẳng | — |
| FR-M08-14.11 | DEC-187, DEC-190, QA-354 | Nói thẳng | — |
| FR-M08-14.12 | DEC-187, QA-359 | Nói thẳng | — |
| FR-M08-14.13 | DEC-187, QA-367 | Nói thẳng | — |
| FR-M08-14.14 | DEC-190, QA-356 | Nói thẳng | — |
| FR-M08-15 | QA-019, QA-018 | Nói thẳng | QA-019 "Ban/Unban: cả MOD và ADMIN" |
| FR-M08-15.01 | QA-019, QA-018 | Nói thẳng | — |
| FR-M08-15.02 | DEC-065 | Nói thẳng | — |
| FR-M08-15.03 | QA-019 | Suy ra | Chỉ ban đang hiệu lực mới có đường sang Đã gỡ (5.21) |
| FR-M08-15.04 | QA-019 | Suy ra | QA-019 "Ban/Unban: cả MOD và ADMIN" ⇒ người khác bị từ chối |
| FR-M08-15.05 | DEC-190 | Nói thẳng | DEC-190 nêu gỡ ban là ngoại lệ của "mọi xử lý qua vụ" |
| FR-M08-16 | DEC-081, DEC-146, DEC-129 | Nói thẳng | — |
| FR-M08-16.01 | DEC-081 | Nói thẳng | — |
| FR-M08-16.02 | DEC-146 | Nói thẳng | — |
| FR-M08-16.03 | DEC-129 | Nói thẳng | — |
| FR-M08-16.04 | DEC-156 | Nói thẳng | — |
| FR-M08-16.05 | DEC-193, QA-367, QA-369 | Nói thẳng | — |
| FR-M08-16.06 | DEC-193, QA-367 | Nói thẳng | — |
| FR-M08-16.07 | DEC-193, QA-367 | Nói thẳng | — |
| FR-M08-17 | DEC-081, DEC-090, DEC-224 | Nói thẳng | — |
| FR-M08-17.01 | DEC-081, DEC-090 | Nói thẳng | — |
| FR-M08-17.02 | DEC-081 | Nói thẳng | — |
| FR-M08-17.03 | DEC-081, QA-021 | Nói thẳng | — |
| FR-M08-17.04 | DEC-081 | Nói thẳng | — |
| FR-M08-17.05 | DEC-081 | Suy ra | Nhật ký chỉ dành cho Admin, Mod |
| FR-M08-17.06 | DEC-224 | Nói thẳng | — |
| FR-M08-18 | DEC-194, QA-369, DEC-072 | Nói thẳng | Mở rộng phạm vi đã được chấp nhận (CC-02) |
| FR-M08-18.01 | DEC-194, QA-369 | Nói thẳng | — |
| FR-M08-18.02 | DEC-194 | Nói thẳng | — |
| FR-M08-18.03 | DEC-194 | Nói thẳng | — |
| FR-M08-18.04 | DEC-194, QA-369 | Nói thẳng | — |
| FR-M08-18.05 | DEC-194, DEC-235 | Nói thẳng | Danh sách đầy đủ thuộc M11 (DEC-235) |
| FR-M08-18.06 | DEC-194 | Nói thẳng | — |
| FR-M08-18.07 | DEC-194 | Nói thẳng | — |
| FR-M08-18.08 | DEC-194 | Nói thẳng | — |
| FR-M08-18.09 | DEC-194 | Suy ra | Bị ẩn là trạng thái cuối, không có thao tác bỏ ẩn ⇒ không thao tác nào khác áp lên nhóm Bị ẩn |
| FR-M08-18.10 | DEC-194, DEC-090 | Suy ra | Thao tác thuộc Mod, Admin |
| FR-M08-18.11 | DEC-194, DEC-192 | Nói thẳng | — |
| BR-M08-01 | DEC-072, QA-011 | Nói thẳng | — |
| BR-M08-02 | DEC-072, DEC-190, QA-357 | Nói thẳng | — |
| BR-M08-03 | DEC-073, DEC-130 | Nói thẳng | Định dạng ảnh lấy từ DEC-130 (whitelist ảnh dùng chung) |
| BR-M08-04 | DEC-073 | Nói thẳng | — |
| BR-M08-05 | DEC-076 | Nói thẳng | — |
| BR-M08-06 | DEC-075, DEC-190, QA-357 | Nói thẳng | — |
| BR-M08-07 | DEC-075, DEC-190, QA-357 | Nói thẳng | — |
| BR-M08-08 | DEC-075 | Suy ra | DEC-075 "mod clicks Nhận xử lý to lock a case" ⇒ người khác không nhận, không kết luận được vụ đang khóa |
| BR-M08-09 | DEC-075, DEC-190, QA-365 | Nói thẳng | — |
| BR-M08-10 | DEC-076 | Nói thẳng | — |
| BR-M08-11 | DEC-076 | Nói thẳng | — |
| BR-M08-12 | DEC-074, DEC-076, DEC-192, QA-362 | Nói thẳng | — |
| BR-M08-13 | DEC-074, DEC-192, DEC-115, DEC-194, QA-362 | Nói thẳng | — |
| BR-M08-14 | DEC-179 | Nói thẳng | — |
| BR-M08-15 | DEC-179, DEC-184, DEC-185, DEC-168 | Nói thẳng | — |
| BR-M08-16 | DEC-161, DEC-180 | Nói thẳng | — |
| BR-M08-17 | DEC-177 | Nói thẳng | — |
| BR-M08-18 | DEC-082 | Nói thẳng | — |
| BR-M08-19 | DEC-082, DEC-192, QA-365 | Nói thẳng | — |
| BR-M08-20 | DEC-077, DEC-186, QA-366 | Nói thẳng | Giá trị "10 replies in 5 min" là giá trị tạm của nguồn (TBD-M08-04) |
| BR-M08-21 | DEC-077 | Nói thẳng | — |
| BR-M08-22 | DEC-098, DEC-077 | Nói thẳng | — |
| BR-M08-23 | DEC-078, DEC-098, DEC-186, QA-366 | Nói thẳng | — |
| BR-M08-24 | DEC-098, DEC-186, QA-352 | Nói thẳng | — |
| BR-M08-25 | DEC-097 | Nói thẳng | — |
| BR-M08-26 | DEC-008, DEC-093, DEC-099 | Nói thẳng | — |
| BR-M08-27 | DEC-099 | Nói thẳng | — |
| BR-M08-28 | DEC-079 | Nói thẳng | — |
| BR-M08-29 | DEC-079, QA-020, DEC-188, QA-358 | Nói thẳng | — |
| BR-M08-30 | QA-020, DEC-188, QA-358 | Nói thẳng | — |
| BR-M08-31 | DEC-079, DEC-163, DEC-178, DEC-118, DEC-191 | Nói thẳng | — |
| BR-M08-32 | DEC-079, DEC-118 | Nói thẳng | — |
| BR-M08-33 | DEC-078, DEC-080, QA-019 | Nói thẳng | — |
| BR-M08-34 | DEC-080, DEC-187, QA-359 | Nói thẳng | — |
| BR-M08-35 | DEC-080 | Nói thẳng | — |
| BR-M08-36 | DEC-080, DEC-187, DEC-190, QA-354 | Nói thẳng | — |
| BR-M08-37 | DEC-152 | Nói thẳng | — |
| BR-M08-38 | QA-019, QA-018 | Nói thẳng | — |
| BR-M08-39 | DEC-081, DEC-146, DEC-094, DEC-193 | Nói thẳng | — |
| BR-M08-40 | DEC-129, DEC-156, DEC-193 | Nói thẳng | — |
| BR-M08-41 | DEC-081, DEC-224 | Nói thẳng | — |
| BR-M08-42 | DEC-090 | Nói thẳng | — |
| BR-M08-43 | DEC-127, DEC-188 | Nói thẳng | — |
| BR-M08-44 | DEC-104 | Nói thẳng | — |
| BR-M08-45 | DEC-167, DEC-108 | Nói thẳng | — |
| BR-M08-46 | DEC-189, DEC-186, QA-355, QA-365, DEC-195 | Nói thẳng | — |
| BR-M08-47 | DEC-191, QA-363, QA-364, QA-368 | Nói thẳng | — |
| BR-M08-48 | DEC-190, QA-356, QA-360 | Nói thẳng | — |
| BR-M08-49 | DEC-190, DEC-186, QA-361 | Nói thẳng | — |
| BR-M08-50 | DEC-194, QA-369 | Nói thẳng | — |
| BR-M08-51 | DEC-186, QA-366 | Nói thẳng | — |
| BR-M08-52 | DEC-187, QA-367 | Nói thẳng | — |
| BR-M08-53 | DEC-187, QA-353, DM-10.3 | Nói thẳng | — |
| BR-M08-54 | DEC-188, QA-366 | Nói thẳng | — |
| BR-M08-55 | DEC-195 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Mâu thuẫn | Ngưỡng AI có phụ thuộc mức cảnh cáo của tác giả không (QA-020 có, DEC-098 một cặp 0,9/0,5)? | A — một cặp 0,9/0,5 cho mọi người. | ISS-292, QA-352, DEC-186 |
| Q-02 | Mâu thuẫn | "Suspend", "Disable account" (draft) có là thao tác riêng không (DEC-080 chỉ có ban)? | A — suspend là ban tạm thời; không có suspend, disable riêng. | ISS-293, QA-353, DEC-187 |
| Q-03 | Mâu thuẫn | Vi phạm lần thứ 7 (đang HEAVY) chuyển sang ban thế nào ("auto-ban" của DEC-080 so với "AI never auto-bans")? | A — không ghi cảnh cáo thứ 7; vụ thành yêu cầu ban, Mod, Admin quyết và chọn Ban. | ISS-294, QA-354, DEC-187 |
| Q-04 | Thiếu chi tiết | Người dùng có báo cáo được nội dung, tài khoản của chính mình không? | Không. | ISS-304, QA-364, DEC-191 |
| Q-05 | Thiếu chi tiết | Ai cảnh cáo, ban được tài khoản Mod, Admin; Mod có xử lý vụ nhắm vào chính mình không? | (1) Chỉ Admin cảnh cáo, ban Mod; (2) Admin không bị cảnh cáo, ban; (3) AI không tự cảnh cáo Mod (để Admin quyết), Admin; (4) Mod không thấy, không nhận vụ nhắm vào chính mình. | ISS-295, QA-355, DEC-189 |
| Q-06 | Thiếu chi tiết | Mod, Admin có ẩn, cảnh cáo, ban ngoài một vụ không? | A — mọi xử lý qua vụ; Mod tự phát hiện thì tự báo cáo rồi nhận xử lý. | ISS-296, QA-356, DEC-190 |
| Q-07 | Mơ hồ | Mức nặng của lý do; số lý do mỗi báo cáo; thứ tự khi bằng điểm? | Nặng 10, Trung bình 5, Nhẹ 2 (BR-M08-06); một lý do; vụ mở trước đứng trước. | ISS-297, QA-357, DEC-190 |
| Q-08 | Mơ hồ | "30 phút không thao tác" tính từ thao tác nào? | Thao tác cuối của người giữ: mở xem vụ, ẩn, cảnh cáo, ban, kết luận. | ISS-305, QA-365, DEC-190 |
| Q-09 | Mơ hồ | Chỉ số tập trung lấy đối tượng nào; mốc 90 ngày? | Đối tượng của vụ đang xem; 90 × 24 giờ. | ISS-305, QA-365, DEC-192 |
| Q-10 | Mơ hồ | Ngưỡng tốc độ "vượt" hay "đạt"; đếm gì? | Đạt ngưỡng trở lên; chỉ đếm trả lời. | ISS-306, QA-366, DEC-186 |
| Q-11 | Mơ hồ | Điểm quét lấy từ bốn nhóm thế nào? | Điểm cao nhất; nhóm đó là lý do của mục do AI tạo. | ISS-306, QA-366, DEC-186 |
| Q-12 | Mơ hồ | Một lần quét bắt nhiều nội dung ≥ 0,9 của cùng người: mấy cảnh cáo? | Mỗi nội dung một cảnh cáo. | ISS-306, QA-366, DEC-186 |
| Q-13 | Mơ hồ | Hết thời gian thử thách: số lần còn lại, thử thách của mức mới, cách tính ngày? | A và (i) — về số lần cao nhất của mức dưới, thử thách nối tiếp; N × 24 giờ. | ISS-298, QA-358, DEC-188 |
| Q-14 | Mơ hồ | Ban nào tính vào số lần đã bị ban? | A — mọi ban từng có hiệu lực, trừ ban bị lật do khiếu nại. | ISS-299, QA-359, DEC-187 |
| Q-15 | Thiếu chi tiết | Báo cáo trùng của cùng người khi vụ còn mở? | Từ chối. | ISS-304, QA-364, DEC-191 |
| Q-16 | Thiếu chi tiết | Bỏ hoặc lật cảnh cáo: bản ghi, số lần, mức, thử thách? | Số lần giảm 1, mức tính lại; bản ghi giữ, đánh dấu; thời điểm kết thúc thử thách không đổi. | ISS-306, QA-366, DEC-188 |
| Q-17 | Thiếu chi tiết | Nhật ký ghi thêm gì; có sửa được không? | Ghi thêm gỡ ban, bỏ cảnh cáo AI, ẩn, khóa, mở khóa nhóm; không ghi nhận, nhả vụ; không sửa, không xóa. | ISS-307, QA-367, DEC-193 |
| Q-18 | Mơ hồ | Báo cáo có làm bài chuyển Bị gắn cờ (tạm ẩn) không? | A — không; chỉ AI quét lại. | ISS-300, QA-360, DEC-190 |
| Q-19 | Mơ hồ | Nội dung AI gắn cờ, yêu cầu ban nằm ở hàng chờ nào? | A — chung hàng chờ báo cáo, mục do "Hệ thống (AI)" tạo. | ISS-301, QA-361, DEC-190 |
| Q-20 | Cần cân nhắc | Báo cáo nhóm: người bị báo cáo là ai; Mod xử lý nhóm bằng thao tác gì (mở rộng phạm vi)? | Owner; hỗ trợ cả Ẩn nhóm (không bỏ ẩn) và Khóa nhóm (mở khóa trực tiếp). Mở rộng phạm vi được chấp nhận (CC-02). | ISS-309, QA-369, DEC-194 |
| Q-21 | Thiếu chi tiết | Người ở HEAVY có báo cáo được không? | Có. | ISS-304, QA-364, DEC-191 |
| Q-22 | Thiếu chi tiết | Lý do kết luận khi Bác bỏ; thông báo người bị báo cáo khi Bác bỏ; kết quả chung cho người báo cáo? | A — lý do bắt buộc; không thông báo khi Bác bỏ; hai ý chung, câu chữ chốt khi thiết kế. | ISS-302, QA-362, DEC-192 |
| Q-23 | Thiếu chi tiết | Ban chồng lên ban đang hiệu lực? | Từ chối; gỡ ban rồi Ban vĩnh viễn. | ISS-307, QA-367, DEC-187 |
| Q-24 | Thiếu chi tiết | Báo cáo đối tượng không còn hiển thị với người báo cáo? | A — từ chối. | ISS-303, QA-363, DEC-191 |
| Q-25 | Thiếu chi tiết | Admin có xử lý vụ nhắm vào chính mình không? | Không thấy, không nhận (như Mod). | ISS-305, QA-365, DEC-189 |
| Q-26 | Cần cân nhắc | Người báo cáo có rút, sửa báo cáo không (mở rộng phạm vi)? | Không. | ISS-308, QA-368, DEC-191 |

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|
| TBD-M08-01 | Báo cáo tin nhắn chat (đối tượng "Message" của draft) | Thấp | OPEN-003 hoãn có chủ đích; MS1 không làm |
| TBD-M08-02 | (Đã đóng ở phiên bản 1.4 — DEC-248: thu hồi tin nhắn là xóa mềm, nội dung giữ, không ai xem được ở MS1; phần nhóm đã đóng ở phiên bản 1.3 — DEC-239) | Thấp | — |
| TBD-M08-03 | (Đã đóng ở phiên bản 1.3 — DEC-201: bình luận bị ẩn vẫn Bị ẩn khi cảnh cáo, ban gắn với nó bị lật) | Thấp | Đã chốt |
| TBD-M08-04 | Ngưỡng tốc độ trả lời và khoảng thời gian trượt để kích hoạt quét luồng (giá trị tạm "10 trả lời trong 5 phút") | Trung bình | Nguồn (DEC-077) để ngỏ có chủ đích: cần dữ liệu dùng thật để chỉnh |
| TBD-M08-05 | Ngưỡng 0,9 và 0,5 là giá trị tạm | Thấp | Nguồn (DEC-098) để ngỏ có chủ đích: chỉnh theo dữ liệu thật (DEC-133) |

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|
| CC-01 | Người báo cáo rút hoặc sửa báo cáo đã gửi (Q-26) | Mở rộng phạm vi: nguồn chưa có chức năng này | Không làm (DEC-191) |
| CC-02 | Mod, Admin ẩn hoặc khóa nhóm bị báo cáo (Q-20) | Mở rộng phạm vi: nguồn có lý do báo cáo nhóm (DEC-072) nhưng M08 chưa có thao tác xử lý nhóm | Chấp nhận: Ẩn nhóm và Khóa nhóm (DEC-194) |

## Phụ lục C. Sổ nguồn

**Owner keywords:** M08, report, reports, reported, reporter, reporters, reporting, báo cáo, report queue, report case, case grouping, Nhận xử lý, claim, claim-based, resolution_reason, dismissed, moderation, moderate, kiểm duyệt, moderation queue, mod queue, warning, warnings, warn, warned, cảnh cáo, warn level, warn-level, LIGHT, MEDIUM, HEAVY, probation, ban, bans, banned, BANNED, Ban vĩnh viễn, permanent ban, temporary ban, unban, gỡ ban, khóa tài khoản, Tài khoản đã bị khóa, escalation, audit log, nhật ký kiểm duyệt, target_concentration, false report, malicious, velocity, post-scan, pre-scan, mod_state, UNDER_REVIEW, under_review, FLAGGED, Bị gắn cờ, HIDDEN, hide, hidden, bị ẩn, auto-warn, auto-ban, auto-hide, Moderation API, severity, severity_weight, suspend, Accepted Answer, vi phạm
**Dependency keywords:** post, bài viết, comment, bình luận, user, group, nhóm, message, tin nhắn, notification, thông báo, appeal, khiếu nại, AI_ENABLED, AI off, admin, leaderboard, search, downrank, account_state, lock_level, timezone, image, ảnh, threshold, ngưỡng, confidence
**Mục draft của module:** DM-10 (gồm DM-10.1, DM-10.2, DM-10.3, DM-10.4), DM-11.1, DM-6.3
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-027, QA-076 (liên kết độc hại ở hồ sơ, M02); DEC-048, GL:Topic, DM-3.1, QA-004, QA-195, QA-221, QA-225, QA-232, ISS-163, OPEN-006 ("ban đầu" — từ tiếng Việt, không phải ban); DEC-050, QA-104 (cảnh báo mềm khi gợi ý Topic, M05); DEC-051, DEC-141 (Tag, Topic bị ẩn khỏi danh sách, M05); DEC-095 (công nghệ embedding); DEC-105, DEC-110 (nội dung nhóm bị ẩn khi xóa nhóm, nhóm Private ẩn khỏi tìm kiếm, M11); DEC-120, ISS-148 (nút vote bị ẩn, M12); DEC-139, QA-265 ("report" là báo cáo audit của quy trình tài liệu); DEC-149 (email cảnh báo trước khi xóa tài khoản, M01); QA-006 ("báo cáo luận văn"); QA-210 (thuộc tính ẩn của tab trình duyệt, M16); ISS-070 ("heavy extensions" của trình soạn, M04); QA-069 (danh sách theo dõi có ẩn không, M02); DG-1 (kiểm duyệt nêu chung trong giới thiệu dự án); DG-7, DM-13 (sơ đồ kiến trúc); DEC-038 (bài đã xóa ẩn khỏi feed, M03); DM-9.1, QA-037, GL:Accepted Answer (Accepted Answer trong điểm, tìm kiếm, thuật ngữ); ISS-164, QA-222 ("kiểm duyệt" thành viên mới của Group Chat, M16)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DEC-072 | Sở hữu | Sửa một phần bởi DEC-191, DEC-194 | FR-M08-01, FR-M08-18, BR-M08-01, BR-M08-02 | Nhóm A. Đối tượng báo cáo (bài, bình luận, người dùng, nhóm) và lý do riêng theo loại; chỉ người đã đăng nhập |
| DEC-073 | Sở hữu | Hiện hành | FR-M08-01, BR-M08-03, BR-M08-04 | Nhóm A. Bằng chứng tối đa 3 ảnh, 5MB/ảnh; mô tả chỉ bắt buộc khi lý do "Khác" |
| DEC-074 | Sở hữu | Sửa một phần bởi DEC-192 | FR-M08-05, FR-M08-10, BR-M08-12, BR-M08-13 | Nhóm A. Nội dung thông báo kết quả tách theo người nhận (người báo cáo / người vi phạm); kênh gửi thuộc M07 |
| DEC-075 | Sở hữu | Sửa một phần bởi DEC-190 | FR-M08-01, FR-M08-02, FR-M08-03, FR-M08-05, BR-M08-06, BR-M08-07, BR-M08-08, BR-M08-09 | Nhóm A. Điểm ưu tiên của vụ; Mod "Nhận xử lý" để khóa vụ, tự nhả sau 30 phút không thao tác; không có hạn xử lý |
| DEC-076 | Sở hữu | Hiện hành | FR-M08-01, FR-M08-02, FR-M08-03, FR-M08-04, FR-M08-05, BR-M08-05, BR-M08-10, BR-M08-11, BR-M08-12 | Nhóm A. Gom báo cáo đang mở thành một vụ theo đối tượng; vụ mới khi đối tượng đã xử lý; lịch sử báo cáo; lý do kết luận |
| DEC-077 | Sở hữu | Sửa một phần bởi DEC-098, DEC-180, DEC-186, DEC-190 | FR-M08-01, FR-M08-07, FR-M08-08, BR-M08-20, BR-M08-21, BR-M08-22 | Nhóm A. Quét AI bình luận sau khi đăng, kích hoạt theo tốc độ trả lời; AI gắn cờ → ẩn và vào hàng chờ |
| DEC-078 | Sở hữu | Sửa một phần bởi DEC-186 | FR-M08-07, FR-M08-09, FR-M08-10, FR-M08-14, BR-M08-23, BR-M08-33 | Nhóm A. Cách ra cảnh cáo: AI tự cảnh cáo khi độ tin cậy cao, Mod quyết khi thấp; Mod cảnh cáo khi xử lý vụ; ban luôn do người |
| DEC-079 | Sở hữu | Sửa một phần bởi DEC-118, DEC-122, DEC-163, DEC-178, DEC-188 | FR-M08-04, FR-M08-09, FR-M08-10, FR-M08-12, FR-M08-13, BR-M08-28, BR-M08-29, BR-M08-31, BR-M08-32 | Nhóm A. Ba mức cảnh cáo, thời gian thử thách, hạn chế theo mức; trạng thái cảnh cáo riêng tư. ISS-154, ISS-REWD-02, MR-M12, QA-199 chỉ nhắc lại DEC-118, DEC-122 |
| DEC-080 | Sở hữu | Sửa một phần bởi DEC-152, DEC-187 | FR-M08-04, FR-M08-09, FR-M08-14, BR-M08-33, BR-M08-34, BR-M08-35, BR-M08-36 | Nhóm A. Ban tạm thời leo thang 30/90 ngày/vĩnh viễn; ban vĩnh viễn thủ công; vi phạm khi đang HEAVY thì chuyển sang ban |
| DEC-081 | Sở hữu | Sửa một phần bởi DEC-146, DEC-193, DEC-224 | FR-M08-05, FR-M08-16, FR-M08-17, BR-M08-39, BR-M08-41, FR-M08-17.06 | Nhóm A. Nhật ký kiểm duyệt: trường ghi; Admin xem toàn bộ, Mod xem của mình, ngoại lệ khi xét khiếu nại |
| DEC-082 | Sở hữu | Sửa một phần bởi DEC-192 | FR-M08-04, FR-M08-05, FR-M08-10, BR-M08-18, BR-M08-19 | Nhóm A. Báo cáo sai/ác ý: không tự phạt; chỉ số target_concentration 90 ngày cho Mod tham khảo |
| DEC-083 | Phụ thuộc | Hiện hành | Chuyển M04 | Nhóm A. M04: bình luận có trạng thái kiểm duyệt Bình thường/Bị ẩn — yêu cầu bổ sung cho M04 (FR-M04 đã nhận) |
| DM-10 | Sở hữu | Hiện hành | Không áp dụng: chỉ là tiêu đề mục draft, nội dung ở DM-10.1–DM-10.4 | Nhóm A. Draft: tiêu đề mục 10 Moderation / Administration |
| DM-10.1 | Sở hữu | Bị thay bởi DEC-072, DEC-076, QA-218 | — | Nhóm A. Draft: đối tượng báo cáo (gồm Message), 7 lý do chung, 4 trạng thái báo cáo |
| DM-10.2 | Sở hữu | Sửa một phần bởi DEC-161, DEC-169, DEC-180, DEC-187 | FR-M08-06, FR-M08-10, FR-M08-14 | Nhóm A. Draft: thao tác Mod/Admin — ẩn/khóa/xóa bài, ẩn/xóa bình luận, gỡ Accepted Answer, warn, suspend, ban. Khóa bài thuộc M03. "Suspend" là ban tạm thời (DEC-187) |
| DM-10.3 | Sở hữu | Sửa một phần bởi DEC-090, DEC-187, DEC-189 | BR-M08-53 | Nhóm A. Draft: Admin xem người dùng, đổi vai trò, vô hiệu hóa, suspend, ban. Đổi vai trò thuộc M10; suspend là ban tạm thời, không có disable (DEC-187) |
| DM-10.4 | Sở hữu | Trùng với DEC-081 | — | Nhóm A. Draft: nhật ký gồm người làm, thao tác, đối tượng, lý do, thời điểm |
| DM-11.1 | Sở hữu | Sửa một phần bởi DEC-077, DEC-097, DEC-098 | FR-M08-08 | Nhóm A. Draft: AI kiểm duyệt bài, bình luận → dự đoán + độ tin cậy → quy tắc → đăng/xét/từ chối. Phần quét bài trước khi đăng thuộc M03 |
| DM-6.3 | Sở hữu | Bị thay bởi QA-218 | — | Nhóm A. Draft: báo cáo tin nhắn tái dùng cơ chế báo cáo chung (đối chiếu QA-218, OPEN-003 ở bước 2) |
| ISS-104 | Sở hữu | Trùng với DEC-072 | — | Nhóm A. Đối tượng, lý do báo cáo |
| ISS-105 | Sở hữu | Trùng với DEC-075 | — | Nhóm A. Luồng báo cáo: ưu tiên, nhận xử lý, thông báo |
| ISS-106 | Sở hữu | Trùng với DEC-076 | — | Nhóm A. Báo cáo trùng đối tượng |
| ISS-107 | Sở hữu | Trùng với DEC-077 | — | Nhóm A. Quét AI bình luận |
| ISS-108 | Sở hữu | Trùng với DEC-078 | — | Nhóm A. Cách ra cảnh cáo |
| ISS-109 | Sở hữu | Trùng với DEC-079 | — | Nhóm A. Hạn chế theo mức cảnh cáo |
| ISS-110 | Sở hữu | Trùng với DEC-080 | — | Nhóm A. Loại ban |
| ISS-111 | Sở hữu | Trùng với DEC-081 | — | Nhóm A. Nhật ký kiểm duyệt |
| ISS-112 | Sở hữu | Trùng với DEC-082 | — | Nhóm A. Báo cáo sai/ác ý |
| QA-134 | Sở hữu | Trùng với DEC-072 | — | Nhóm A. Lý do riêng theo loại đối tượng |
| QA-135 | Sở hữu | Trùng với DEC-072 | — | Nhóm A. Khách không báo cáo được |
| QA-136 | Sở hữu | Trùng với DEC-073 | — | Nhóm A. Bằng chứng, mô tả |
| QA-137 | Sở hữu | Trùng với DEC-074 | — | Nhóm A. Ai thấy gì trong kết quả xử lý |
| QA-138 | Sở hữu | Trùng với DEC-075 | — | Nhóm A. Chia hàng chờ giữa nhiều Mod: nhận xử lý, tự nhả 30 phút |
| QA-139 | Sở hữu | Trùng với DEC-075 | — | Nhóm A. Ưu tiên lấy mức nặng cao nhất trong vụ |
| QA-140 | Sở hữu | Trùng với DEC-076 | — | Nhóm A. Báo cáo trùng gom thành vụ |
| QA-141 | Sở hữu | Trùng với DEC-077 | — | Nhóm A. Bình luận quét sau khi đăng theo tốc độ trả lời |
| QA-142 | Sở hữu | Trùng với DEC-077 | — | Nhóm A. Phạm vi quét: cả luồng chưa quét với nội dung hiện tại |
| QA-143 | Sở hữu | Trùng với DEC-077 | — | Nhóm A. Sửa không tự kích hoạt quét lại |
| QA-144 | Sở hữu | Trùng với DEC-078 | — | Nhóm A. AI tự cảnh cáo khi độ tin cậy cao; AI không ban |
| QA-145 | Sở hữu | Trùng với DEC-079 | — | Nhóm A. LIGHT không hạn chế |
| QA-146 | Sở hữu | Trùng với DEC-079 | — | Nhóm A. Trạng thái cảnh cáo riêng tư |
| QA-147 | Sở hữu | Trùng với DEC-080 | — | Nhóm A. Thời hạn ban leo thang hoặc vĩnh viễn thủ công |
| QA-148 | Sở hữu | Trùng với DEC-081 | — | Nhóm A. Quyền xem nhật ký kiểm duyệt |
| QA-149 | Sở hữu | Trùng với DEC-082 | — | Nhóm A. Phát hiện báo cáo ác ý |
| MR-M08 | Sở hữu | Sửa một phần bởi DEC-186, DEC-187, DEC-188, DEC-189, DEC-190, DEC-191, DEC-192, DEC-193, DEC-194 | FR-M08-01, FR-M08-02 | Nhóm A. Dòng module-registry của M08; cột MoSCoW lệch (xem 4.5) |
| DEC-186 | Sở hữu | Sửa một phần bởi DEC-195 | FR-M08-04, FR-M08-08, FR-M08-09, BR-M08-20, BR-M08-23, BR-M08-24, BR-M08-46, BR-M08-49, BR-M08-51 | Nhóm A. Ngưỡng AI cho mọi người, điểm quét, ngưỡng tốc độ, cảnh cáo AI |
| DEC-187 | Sở hữu | Hiện hành | FR-M08-02, FR-M08-09, FR-M08-10, FR-M08-14, BR-M08-34, BR-M08-36, BR-M08-52, BR-M08-53 | Nhóm A. Chỉ cảnh cáo và ban; lần vi phạm thứ 7; đếm số lần ban; không ban chồng |
| DEC-188 | Sở hữu | Hiện hành | FR-M08-09, FR-M08-10, FR-M08-11, FR-M08-12, BR-M08-29, BR-M08-30, BR-M08-43, BR-M08-54 | Nhóm A. Giảm mức cảnh cáo, N × 24 giờ, bỏ hoặc lật cảnh cáo |
| DEC-189 | Sở hữu | Sửa một phần bởi DEC-195 | FR-M08-02, FR-M08-03, FR-M08-09, FR-M08-10, FR-M08-14, BR-M08-46 | Nhóm A. Xử lý tài khoản Mod, Admin; vụ nhắm vào chính mình |
| DEC-190 | Sở hữu | Hiện hành | FR-M08-01, FR-M08-02, FR-M08-03, FR-M08-04, FR-M08-06, FR-M08-07, FR-M08-08, FR-M08-09, FR-M08-10, FR-M08-14, FR-M08-15, BR-M08-02, BR-M08-06, BR-M08-07, BR-M08-09, BR-M08-36, BR-M08-48, BR-M08-49 | Nhóm A. Mọi xử lý qua vụ; mục do AI tạo; mức nặng; báo cáo không ẩn bài |
| DEC-191 | Sở hữu | Sửa một phần bởi DEC-195 | FR-M08-01, BR-M08-31, BR-M08-47 | Nhóm A. Quy tắc gửi báo cáo |
| DEC-192 | Sở hữu | Hiện hành | FR-M08-04, FR-M08-05, FR-M08-18, BR-M08-12, BR-M08-13, BR-M08-19 | Nhóm A. Kết luận vụ, thông báo, chỉ số tập trung |
| DEC-193 | Sở hữu | Hiện hành | FR-M08-16, BR-M08-39, BR-M08-40 | Nhóm A. Bổ sung nhật ký kiểm duyệt |
| DEC-194 | Sở hữu | Hiện hành | FR-M08-04, FR-M08-18, BR-M08-13, BR-M08-50 | Nhóm A. Ẩn, khóa nhóm (mở rộng phạm vi) |
| ISS-292 | Sở hữu | Trùng với DEC-186 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-293 | Sở hữu | Trùng với DEC-187 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-294 | Sở hữu | Trùng với DEC-187 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-295 | Sở hữu | Trùng với DEC-189 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-296 | Sở hữu | Trùng với DEC-190 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-297 | Sở hữu | Trùng với DEC-190 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-298 | Sở hữu | Trùng với DEC-188 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-299 | Sở hữu | Trùng với DEC-187 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-300 | Sở hữu | Trùng với DEC-190 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-301 | Sở hữu | Trùng với DEC-190 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-302 | Sở hữu | Trùng với DEC-192 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-303 | Sở hữu | Trùng với DEC-191 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-304 | Sở hữu | Trùng với DEC-191 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-305 | Sở hữu | Trùng với DEC-189 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-306 | Sở hữu | Trùng với DEC-186 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-307 | Sở hữu | Trùng với DEC-187 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-308 | Sở hữu | Trùng với DEC-191 | — | Nhóm A. Câu hỏi FR M08 |
| ISS-309 | Sở hữu | Trùng với DEC-194 | — | Nhóm A. Câu hỏi FR M08 |
| QA-352 | Sở hữu | Hiện hành | FR-M08-09, BR-M08-24 | Nhóm A. Câu trả lời FR M08 |
| QA-353 | Sở hữu | Hiện hành | BR-M08-53 | Nhóm A. Câu trả lời FR M08 |
| QA-354 | Sở hữu | Hiện hành | FR-M08-09, FR-M08-10, FR-M08-14, BR-M08-36 | Nhóm A. Câu trả lời FR M08 |
| QA-355 | Sở hữu | Hiện hành | FR-M08-02, FR-M08-03, FR-M08-10, FR-M08-14, BR-M08-46 | Nhóm A. Câu trả lời FR M08 |
| QA-356 | Sở hữu | Hiện hành | FR-M08-06, FR-M08-10, FR-M08-14, BR-M08-48 | Nhóm A. Câu trả lời FR M08 |
| QA-357 | Sở hữu | Hiện hành | FR-M08-01, FR-M08-02, BR-M08-02, BR-M08-06, BR-M08-07 | Nhóm A. Câu trả lời FR M08 |
| QA-358 | Sở hữu | Hiện hành | FR-M08-12, BR-M08-29, BR-M08-30 | Nhóm A. Câu trả lời FR M08 |
| QA-359 | Sở hữu | Hiện hành | FR-M08-14, BR-M08-34 | Nhóm A. Câu trả lời FR M08 |
| QA-360 | Sở hữu | Hiện hành | FR-M08-07, BR-M08-48 | Nhóm A. Câu trả lời FR M08 |
| QA-361 | Sở hữu | Hiện hành | FR-M08-07, BR-M08-49 | Nhóm A. Câu trả lời FR M08 |
| QA-362 | Sở hữu | Hiện hành | FR-M08-05, BR-M08-12, BR-M08-13 | Nhóm A. Câu trả lời FR M08 |
| QA-363 | Sở hữu | Hiện hành | FR-M08-01, BR-M08-47 | Nhóm A. Câu trả lời FR M08 |
| QA-364 | Sở hữu | Hiện hành | FR-M08-01, BR-M08-47 | Nhóm A. Câu trả lời FR M08 |
| QA-365 | Sở hữu | Hiện hành | FR-M08-02, FR-M08-03, BR-M08-09, BR-M08-19, BR-M08-46 | Nhóm A. Câu trả lời FR M08 |
| QA-366 | Sở hữu | Hiện hành | FR-M08-08, FR-M08-09, FR-M08-11, BR-M08-20, BR-M08-23, BR-M08-51, BR-M08-54 | Nhóm A. Câu trả lời FR M08 |
| QA-367 | Sở hữu | Hiện hành | FR-M08-14, FR-M08-16, BR-M08-52 | Nhóm A. Câu trả lời FR M08 |
| QA-368 | Sở hữu | Hiện hành | FR-M08-01, BR-M08-47 | Nhóm A. Câu trả lời FR M08 |
| QA-369 | Sở hữu | Hiện hành | FR-M08-04, FR-M08-16, FR-M08-18, BR-M08-50 | Nhóm A. Câu trả lời FR M08 |
| DEC-006 | Nhắc tới | Hiện hành | Không áp dụng: Cả 5 năng lực AI bắt buộc, gồm AI kiểm duyệt | Nhóm B. Cả 5 năng lực AI bắt buộc, gồm AI kiểm duyệt |
| DEC-008 | Sở hữu | Sửa một phần bởi DEC-093, DEC-099 | FR-M08-02, FR-M08-08, BR-M08-26 | Nhóm B. Hành vi khi AI tắt: M08 chỉ còn hàng chờ thủ công. DEC-092, ISS-200, QA-259 chỉ làm rõ nơi lưu cờ |
| DEC-012 | Phụ thuộc | Sửa một phần bởi DEC-031, DEC-032, DEC-033 | Chuyển M03 | Nhóm B. M03: bài có 3 trường trạng thái; Mod đặt trạng thái kiểm duyệt |
| DEC-013 | Phụ thuộc | Sửa một phần bởi DEC-032, DEC-034, DEC-161 | Chuyển M03 | Nhóm B. M03: quét bài trước khi đăng, quét lại khi sửa; AI tắt thì bỏ quét |
| DEC-018 | Phụ thuộc | Sửa một phần bởi DEC-085 | FR-M08-14 | Nhóm B. M01: trạng thái tài khoản BANNED |
| DEC-019 | Phụ thuộc | Sửa một phần bởi DEC-150, DEC-156 | Chuyển M01 | Nhóm B. M01: màn hình BANNED (lý do, thời gian khiếu nại, nút khiếu nại). DEC-148, DEC-149 (ngoài bảng nguồn) chỉ sửa thời hạn, username, email; màn hình BANNED giữ nguyên |
| DEC-025 | Nhắc tới | Sửa một phần bởi DEC-172 | Không áp dụng: M02: danh sách theo dõi không hiện tài khoản BANNED | Nhóm B. M02: danh sách theo dõi không hiện tài khoản BANNED. DEC-171 (ngoài bảng nguồn) chỉ sửa quyền Guest |
| DEC-031 | Phụ thuộc | Hiện hành | Chuyển M03 | Nhóm B. M03: trạng thái đăng của bài; Bị từ chối do Mod |
| DEC-032 | Sở hữu | Sửa một phần bởi DEC-161, DEC-190 | FR-M08-07 | Nhóm B. Trạng thái kiểm duyệt bài Bị gắn cờ/Bị ẩn do AI, báo cáo, Mod; tác giả phải khiếu nại. Định nghĩa trạng thái ở M03 |
| DEC-033 | Phụ thuộc | Sửa một phần bởi DEC-167 | Chuyển M03 | Nhóm B. M03: khóa bài (Mod khóa toàn bộ); bài hiển thị khi trạng thái kiểm duyệt Bình thường |
| DEC-034 | Phụ thuộc | Sửa một phần bởi DEC-098 | Chuyển M03 | Nhóm B. M03: quét trước khi đăng; Mod duyệt bài chờ đăng |
| DEC-041 | Nhắc tới | Hiện hành | Không áp dụng: M04: nội dung xấu trong bình luận xử lý bằng báo cáo | Nhóm B. M04: nội dung xấu trong bình luận xử lý bằng báo cáo |
| DEC-065 | Phụ thuộc | Sửa một phần bởi DEC-151, DEC-180 | FR-M08-05, FR-M08-08, FR-M08-09, FR-M08-10, FR-M08-14, FR-M08-15 | Nhóm B. M07: sự kiện thông báo kết quả báo cáo, cảnh cáo, ban/gỡ ban (email cho ban). DEC-147 (ngoài bảng nguồn) chỉ thêm sự kiện liên kết Google |
| DEC-084 | Phụ thuộc | Hiện hành | Chuyển M09 | Nhóm B. M09: khiếu nại dùng chung giới hạn bằng chứng với báo cáo |
| DEC-085 | Phụ thuộc | Hiện hành | FR-M08-14 | Nhóm B. M09: tài khoản bị ban vẫn đăng nhập, chỉ thấy màn hình khóa và gửi khiếu nại |
| DEC-086 | Phụ thuộc | Hiện hành | FR-M08-13 | Nhóm B. M09: hạn khiếu nại theo thời gian thử thách, thời hạn ban |
| DEC-087 | Phụ thuộc | Hiện hành | Chuyển M09 | Nhóm B. M09: mỗi xử lý báo cáo, cảnh cáo, ban khiếu nại một lần |
| DEC-088 | Phụ thuộc | Hiện hành | Chuyển M09 | Nhóm B. M09: hàng chờ khiếu nại tách khỏi hàng chờ báo cáo, cùng cơ chế nhận xử lý |
| DEC-089 | Phụ thuộc | Hiện hành | Chuyển M09 | Nhóm B. M09: khiếu nại thành công — ban về ACTIVE (giữ bản ghi, đánh dấu bị lật); cảnh cáo giảm số lần |
| DEC-090 | Sở hữu | Hiện hành | FR-M08-02, FR-M08-03, FR-M08-04, FR-M08-05, FR-M08-06, FR-M08-07, FR-M08-10, FR-M08-14, FR-M08-17, FR-M08-18, BR-M08-42 | Nhóm B. Mod và Admin cùng xử lý báo cáo, cảnh cáo, ban; Admin xem toàn bộ nhật ký; hằng số chính sách không cấu hình qua giao diện. DEC-141 (ngoài bảng nguồn) chỉ sửa phần Topic |
| DEC-093 | Phụ thuộc | Hiện hành | FR-M08-08, FR-M08-09, BR-M08-26 | Nhóm B. M10: công tắc Moderation gồm quét trước khi đăng, quét bình luận, tự cảnh cáo |
| DEC-094 | Phụ thuộc | Sửa một phần bởi DEC-227 | BR-M08-39 | Nhóm B. M10: nhật ký thao tác Admin (gồm ban, cảnh cáo), chỉ ghi thêm. DEC-227 (đối chiếu FR-M10): nhật ký Admin ghi song song thao tác kiểm duyệt của Admin; DEC-228 (ngoài bảng nguồn) chỉ sửa lý do, thứ tự, lọc của nhật ký Admin |
| DEC-097 | Phụ thuộc | Hiện hành | BR-M08-25 | Nhóm B. M13: AI chỉ phát hiện 4 nhóm; Spam, đạo văn, sai lệch chỉ qua báo cáo |
| DEC-098 | Sở hữu | Sửa một phần bởi DEC-161, DEC-186 | FR-M08-07, FR-M08-08, FR-M08-09, FR-M08-10, BR-M08-22, BR-M08-23, BR-M08-24 | Nhóm B. Hai nhánh ngưỡng 0,9/0,5: nhánh cảnh cáo; nhánh nội dung với bình luận (bài thuộc M03). Ranh giới với M13 cần xác nhận. DEC-166 (ngoài bảng nguồn) chỉ sửa phần bài bị AI từ chối (M03) |
| DEC-099 | Sở hữu | Hiện hành | FR-M08-02, FR-M08-08, FR-M08-09, BR-M08-26, BR-M08-27 | Nhóm B. AI tắt → không quét, chỉ dựa vào báo cáo; AI lỗi khi quét bình luận → giữ nguyên, ghi lỗi. Phần bài thuộc M03, thời gian chờ thuộc M13 |
| DEC-100 | Nhắc tới | Hiện hành | Không áp dụng: M13: quét do hệ thống kích hoạt, không cần giới hạn tần suất | Nhóm B. M13: quét do hệ thống kích hoạt, không cần giới hạn tần suất. DEC-144 (ngoài bảng nguồn) chỉ sửa giới hạn gợi ý Topic |
| DEC-102 | Nhắc tới | Hiện hành | Không áp dụng: M11: quyền Group Mod trong nhóm | Nhóm B. M11: quyền Group Mod trong nhóm |
| DEC-104 | Phụ thuộc | Hiện hành | BR-M08-44 | Nhóm B. M11: kiểm duyệt nhóm chồng lên M08; báo cáo và Mod hệ thống vẫn áp dụng cho nội dung nhóm |
| DEC-107 | Nhắc tới | Hiện hành | Không áp dụng: M11: Owner bị ban thì tự chuyển quyền chủ nhóm | Nhóm B. M11: Owner bị ban thì tự chuyển quyền chủ nhóm |
| DEC-108 | Phụ thuộc | Hiện hành | FR-M08-01, BR-M08-45 | Nhóm B. M11: nhóm chuyển Private thì người ngoài không báo cáo được bài |
| DEC-109 | Nhắc tới | Hiện hành | Không áp dụng: M11: xử lý cấp nhóm không có khiếu nại | Nhóm B. M11: xử lý cấp nhóm không có khiếu nại |
| DEC-113 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B. M12: trừ điểm khi nội dung bị Mod/Admin gỡ vì vi phạm |
| DEC-115 | Phụ thuộc | Hiện hành | FR-M08-05, BR-M08-13 | Nhóm B. M09: khiếu nại bài bị gỡ; thành công thì gỡ cả cảnh cáo, ban đi kèm |
| DEC-118 | Phụ thuộc | Hiện hành | BR-M08-31, BR-M08-32 | Nhóm B. M12: HEAVY bị loại khỏi bảng xếp hạng — ngoại lệ của tính riêng tư cảnh cáo |
| DEC-122 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B. M12: tài khoản BANNED bị loại khỏi bảng xếp hạng, nhãn "Tài khoản đã bị khóa"; nội dung vi phạm xử lý riêng qua M08 |
| DEC-126 | Nhắc tới | Hiện hành | Không áp dụng: M14: mọi tương tác, kể cả báo cáo, cần đăng nhập | Nhóm B. M14: mọi tương tác, kể cả báo cáo, cần đăng nhập |
| DEC-127 | Phụ thuộc | Hiện hành | BR-M08-43 | Nhóm B. Dùng chung: múi giờ tính thời gian thử thách |
| DEC-129 | Sở hữu | Sửa một phần bởi DEC-156, DEC-179, DEC-184 | FR-M08-16, BR-M08-40 | Nhóm B. Nhật ký kiểm duyệt giữ vĩnh viễn |
| DEC-130 | Phụ thuộc | Hiện hành | FR-M08-01, BR-M08-03 | Nhóm B. Dùng chung: ảnh tải lên chỉ JPEG/PNG/WebP, không quét virus (ảnh bằng chứng). DEC-160 (ngoài bảng nguồn) chỉ thêm tài liệu đính kèm bài |
| DEC-131 | Phụ thuộc | Sửa một phần bởi DEC-146, DEC-154 | Chuyển M01 | Nhóm B. M01: trang chính sách nêu nội dung được AI bên thứ ba kiểm duyệt |
| DEC-133 | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B. M13: nhật ký quyết định AI, tách khỏi nhật ký kiểm duyệt |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ (gửi email thông báo ban) | Nhóm B. Công nghệ (gửi email thông báo ban) |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ | Nhóm B. Công nghệ |
| DEC-145 | Nhắc tới | Hiện hành | Không áp dụng: M05: Trending chỉ tính bài không bị ẩn do kiểm duyệt | Nhóm B. M05: Trending chỉ tính bài không bị ẩn do kiểm duyệt |
| DEC-146 | Sở hữu | Hiện hành | FR-M08-16, BR-M08-39 | Nhóm B. Thêm thao tác Tag, đổi Topic/Tag bài người khác vào nhật ký kiểm duyệt (sửa DEC-081) |
| DEC-150 | Phụ thuộc | Hiện hành | FR-M08-04 | Nhóm B. M01: Mod, Admin xem bài ẩn và danh tính tác giả đã vô hiệu hóa để xử lý |
| DEC-151 | Nhắc tới | Hiện hành | Không áp dụng: M01: tài khoản BANNED được đặt lại mật khẩu để khiếu nại | Nhóm B. M01: tài khoản BANNED được đặt lại mật khẩu để khiếu nại |
| DEC-152 | Phụ thuộc | Hiện hành | FR-M08-14, BR-M08-37 | Nhóm B. M01: ban tạm thời hết hạn thì tự về ACTIVE (sửa DEC-080); nút OK màn hình khóa |
| DEC-153 | Nhắc tới | Hiện hành | Không áp dụng: M01: tài khoản BANNED không có trong gợi ý nhắc tên | Nhóm B. M01: tài khoản BANNED không có trong gợi ý nhắc tên |
| DEC-154 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: trang chính sách — dữ liệu báo cáo, cảnh cáo, ban giữ vì an toàn cộng đồng; điều khoản kiểm duyệt |
| DEC-156 | Phụ thuộc | Hiện hành | FR-M08-16, BR-M08-40 | Nhóm B. M01: nhật ký kiểm duyệt được giữ khi tài khoản bị xóa. DEC-159 (ngoài bảng nguồn) chỉ thêm dữ liệu bị xóa không thuộc M08 |
| DEC-161 | Sở hữu | Sửa một phần bởi DEC-185 | FR-M08-06, FR-M08-07, BR-M08-16 | Nhóm B. Mod gỡ bài = Bị ẩn; quét lại khi sửa → Bị gắn cờ chờ Mod xét. Phần quét thuộc M03 |
| DEC-162 | Nhắc tới | Sửa một phần bởi DEC-184 | Không áp dụng: M03: bài bị Mod ẩn không sửa được, phải khiếu nại | Nhóm B. M03: bài bị Mod ẩn không sửa được, phải khiếu nại |
| DEC-163 | Phụ thuộc | Hiện hành | BR-M08-31 | Nhóm B. M03: phạm vi "không tạo bài mới" ở MEDIUM/HEAVY |
| DEC-167 | Phụ thuộc | Hiện hành | FR-M08-01, BR-M08-45 | Nhóm B. M03: bài khóa toàn bộ vẫn báo cáo được |
| DEC-168 | Sở hữu | Sửa một phần bởi DEC-185 | FR-M08-04, FR-M08-07, BR-M08-15 | Nhóm B. Mod, Admin xem bài Bị gắn cờ, Bị Mod ẩn qua M08/M09 |
| DEC-169 | Sở hữu | Hiện hành | Không áp dụng: MS1 không có Accepted Answer (ghi ở 1.2) | Nhóm B. MS1 không có Accepted Answer — loại thao tác gỡ Accepted Answer của DM-10.2 |
| DEC-172 | Nhắc tới | Hiện hành | Không áp dụng: M02: danh sách theo dõi không hiện tài khoản BANNED | Nhóm B. M02: danh sách theo dõi không hiện tài khoản BANNED |
| DEC-174 | Nhắc tới | Hiện hành | Không áp dụng: M02: bookmark bài bị ẩn do kiểm duyệt | Nhóm B. M02: bookmark bài bị ẩn do kiểm duyệt |
| DEC-175 | Nhắc tới | Hiện hành | Không áp dụng: M02: tab bài trên hồ sơ không hiện bài bị ẩn | Nhóm B. M02: tab bài trên hồ sơ không hiện bài bị ẩn |
| DEC-177 | Sở hữu | Hiện hành | FR-M08-10, FR-M08-14, BR-M08-17 | Nhóm B. Xử lý báo cáo người dùng chỉ bằng cảnh cáo hoặc ban; Mod, Admin không gỡ avatar, bio |
| DEC-178 | Phụ thuộc | Hiện hành | BR-M08-31 | Nhóm B. M04: HEAVY chỉ chặn tạo bình luận mới; bình luận bị ẩn không sửa, xóa |
| DEC-179 | Sở hữu | Hiện hành | FR-M08-04, FR-M08-05, BR-M08-14, BR-M08-15 | Nhóm B. Mod, Admin xem nội dung bình luận đã xóa trong báo cáo, lịch sử báo cáo, khiếu nại. Xóa mềm thuộc M04 |
| DEC-180 | Sở hữu | Hiện hành | FR-M08-06, FR-M08-08, BR-M08-16 | Nhóm B. Mod, Admin chỉ có thao tác Ẩn với bình luận ("xóa bình luận" ở DM-10.2 = Ẩn). Hiển thị cho tác giả thuộc M04 |
| DEC-181 | Nhắc tới | Hiện hành | Không áp dụng: M04: hiển thị luồng có bình luận bị ẩn | Nhóm B. M04: hiển thị luồng có bình luận bị ẩn |
| DEC-182 | Nhắc tới | Hiện hành | Không áp dụng: M04: bình luận bị ẩn không tính vào số bình luận | Nhóm B. M04: bình luận bị ẩn không tính vào số bình luận |
| DEC-183 | Nhắc tới | Hiện hành | Không áp dụng: M04: trích dẫn bình luận đã bị ẩn | Nhóm B. M04: trích dẫn bình luận đã bị ẩn |
| DEC-184 | Sở hữu | Hiện hành | FR-M08-04, BR-M08-15 | Nhóm B. Mod, Admin xem bài Đã xóa hẳn trong báo cáo, lịch sử báo cáo, khiếu nại. Dữ liệu bài thuộc M03 |
| DEC-185 | Sở hữu | Hiện hành | FR-M08-04, BR-M08-15 | Nhóm B. Mod, Admin xem bài Tự ẩn trong báo cáo, lịch sử báo cáo, khiếu nại. Quét lại khi hiện lại thuộc M03 |
| DG-4 | Nhắc tới | Sửa một phần bởi DEC-169 | Không áp dụng: Bản đồ module: mục 10 Report / Moderation / Admin | Nhóm B. Bản đồ module: mục 10 Report / Moderation / Admin |
| DG-5 | Phụ thuộc | Sửa một phần bởi DEC-169 | Không áp dụng: dùng chung, không quy định hành vi riêng của M08 | Nhóm B. Dùng chung: con người quyết định cuối; AI kiểm duyệt không tự quyết tuyệt đối; ẩn danh vẫn lưu danh tính cho Mod |
| DG-6 | Phụ thuộc | Sửa một phần bởi DEC-077, QA-007 | Chuyển M13 | Nhóm B. M13: AI kiểm duyệt bắt buộc, trả dự đoán + độ tin cậy |
| DG-8 | Nhắc tới | Hiện hành | Không áp dụng: Không làm: AI tự quyết reputation/badge/Accepted Answer | Nhóm B. Không làm: AI tự quyết reputation/badge/Accepted Answer |
| DM-1.3 | Sở hữu | Hiện hành | FR-M08-01, FR-M08-02, FR-M08-03, FR-M08-04, FR-M08-05, FR-M08-07 | Nhóm B. Draft quyền: User báo cáo; Mod xét báo cáo, kiểm duyệt nội dung, quản lý người dùng |
| DM-11 | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B. M13: AI không tự quyết tuyệt đối với case nhạy cảm |
| DM-11.5 | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B. M13: vòng phản hồi — Mod đánh giá dự đoán AI (ranh giới cần xác nhận) |
| DM-2.1 | Nhắc tới | Sửa một phần bởi DEC-031, DEC-032, DEC-033, DEC-145, DEC-169 | Không áp dụng: M03: trạng thái bài trong draft; bài ẩn danh lưu danh tính để Mod xử lý báo cáo | Nhóm B. M03: trạng thái bài trong draft; bài ẩn danh lưu danh tính để Mod xử lý báo cáo |
| DM-4.2 | Nhắc tới | Hiện hành | Không áp dụng: M04: bình luận có thao tác Report | Nhóm B. M04: bình luận có thao tác Report |
| DM-4.2.1 | Nhắc tới | Bị thay bởi DEC-169 | — | Nhóm B. Draft: Mod gỡ Accepted Answer gian lận; MS1 không làm (DEC-169) |
| DM-5.3 | Phụ thuộc | Sửa một phần bởi DEC-104 | Chuyển M11 | Nhóm B. M11: bài trong nhóm dùng chung Report, Moderation, AI Moderation |
| DM-8.1 | Phụ thuộc | Sửa một phần bởi DEC-065, DEC-169 | Chuyển M07 | Nhóm B. M07: sự kiện "Report được xử lý", "Post hoàn tất moderation" |
| DM-9.5 | Nhắc tới | Hiện hành | Không áp dụng: M15: thống kê báo cáo, kiểm duyệt | Nhóm B. M15: thống kê báo cáo, kiểm duyệt |
| DM-x02 | Nhắc tới | Sửa một phần bởi DEC-169, QA-007 | Không áp dụng: Danh sách phạm vi: Report, Moderation, Admin Audit Log, AI Content Moderation | Nhóm B. Danh sách phạm vi: Report, Moderation, Admin Audit Log, AI Content Moderation |
| DM-x03 | Nhắc tới | Hiện hành | Không áp dụng: Ngoài phạm vi: AI tự quyết reputation/badge/Accepted Answer | Nhóm B. Ngoài phạm vi: AI tự quyết reputation/badge/Accepted Answer |
| GL:AI Moderation | Sở hữu | Hiện hành | FR-M08-08 | Nhóm B. Thuật ngữ AI Moderation: dự đoán + độ tin cậy |
| GL:Anonymous Post | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: bài ẩn danh vẫn lưu danh tính thật cho kiểm duyệt |
| GL:Comment | Nhắc tới | Sửa một phần bởi DEC-169 | Không áp dụng: Bình luận báo cáo được | Nhóm B. Bình luận báo cáo được |
| GL:Feedback / Evaluation Loop | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B. M13: đo độ chính xác AI để chỉnh ngưỡng |
| GL:Group | Nhắc tới | Hiện hành | Không áp dụng: M11: nhóm dùng lại cơ chế Report | Nhóm B. M11: nhóm dùng lại cơ chế Report |
| GL:Moderator (MOD) | Sở hữu | Sửa một phần bởi DEC-161, DEC-180, DEC-187 | FR-M08-06 | Nhóm B. Thuật ngữ Mod: ẩn/khóa/xóa, xét báo cáo, warn/suspend/ban. "suspend" là ban tạm thời (DEC-187) |
| GL:USER | Sở hữu | Hiện hành | FR-M08-01 | Nhóm B. Thuật ngữ USER: được báo cáo |
| ISS-038 | Sở hữu | Trùng với QA-019 | — | Nhóm B. Ban: ai có quyền, thời hạn, quyền của AI |
| ISS-039 | Phụ thuộc | Trùng với QA-016 | — | Nhóm B. M11: kiểm duyệt nhóm và kiểm duyệt hệ thống |
| ISS-044 | Phụ thuộc | Trùng với DEC-013 | — | Nhóm B. M03: trạng thái kiểm duyệt bài, chính sách quét |
| ISS-050 | Sở hữu | Bị thay bởi DEC-072 | — | Nhóm B. Loại vi phạm khi báo cáo |
| ISS-064 | Phụ thuộc | Trùng với DEC-031 | — | Nhóm B. M03: luồng trạng thái bài |
| ISS-068 | Phụ thuộc | Trùng với DEC-034 | — | Nhóm B. M03: luồng quét trước khi đăng |
| ISS-098 | Phụ thuộc | Trùng với DEC-065 | — | Nhóm B. M07: sự kiện thông báo, email chỉ cho bảo mật/ban |
| ISS-114 | Phụ thuộc | Trùng với DEC-085 | — | Nhóm B. M09: tài khoản bị ban truy cập khiếu nại |
| ISS-115 | Phụ thuộc | Trùng với DEC-086 | — | Nhóm B. M09: hạn khiếu nại |
| ISS-116 | Phụ thuộc | Trùng với DEC-088 | — | Nhóm B. M09: hàng chờ khiếu nại |
| ISS-117 | Phụ thuộc | Trùng với DEC-089 | — | Nhóm B. M09: đảo ngược khi khiếu nại thành công |
| ISS-119 | Sở hữu | Trùng với DEC-090 | — | Nhóm B. Phạm vi Admin riêng và dùng chung với Mod |
| ISS-122 | Phụ thuộc | Trùng với DEC-093 | — | Nhóm B. M10: công tắc AI theo module |
| ISS-126 | Phụ thuộc | Trùng với DEC-097 | — | Nhóm B. M13: nhóm vi phạm AI phát hiện được |
| ISS-127 | Sở hữu | Trùng với DEC-098 | — | Nhóm B. Ngưỡng tự cảnh cáo / tự từ chối |
| ISS-133 | Phụ thuộc | Trùng với DEC-104 | — | Nhóm B. M11: kiểm duyệt nhóm và M08 |
| ISS-139 | Nhắc tới | Trùng với DEC-109 | — | Nhóm B. M11: xử lý cấp nhóm không khiếu nại |
| ISS-142 | Phụ thuộc | Trùng với DEC-113 | — | Nhóm B. M12: trừ điểm khi nội dung bị gỡ vì vi phạm |
| ISS-144 | Phụ thuộc | Trùng với DEC-115 | — | Nhóm B. M09: khiếu nại bài bị gỡ |
| ISS-154 | Phụ thuộc | Trùng với DEC-122 | — | Nhóm B. M12: tài khoản BANNED trên bảng xếp hạng, hồ sơ |
| ISS-159 | Nhắc tới | Trùng với QA-217 | — | Nhóm B. M16: không quét AI tin nhắn |
| ISS-160 | Sở hữu | Trùng với QA-218 | — | Nhóm B. Báo cáo tin nhắn không làm ở MS1 (OPEN-003) |
| ISS-161 | Nhắc tới | Trùng với QA-219 | — | Nhóm B. M16: giới hạn tần suất chat bù cho việc chưa có báo cáo |
| ISS-166 | Nhắc tới | Trùng với QA-227 | — | Nhóm B. M14: khách cần đăng nhập để tương tác, báo cáo |
| ISS-176 | Nhắc tới | Trùng với QA-236 | — | Nhóm B. M14: Trending không loại bài của BANNED/HEAVY |
| ISS-178 | Nhắc tới | Trùng với QA-241 | — | Nhóm B. M15: chỉ Admin xem thống kê |
| ISS-179 | Nhắc tới | Trùng với QA-242 | — | Nhóm B. M15: thống kê người dùng theo mức cảnh cáo |
| ISS-180 | Nhắc tới | Trùng với QA-243 | — | Nhóm B. M15: thống kê bài theo trạng thái kiểm duyệt |
| ISS-181 | Nhắc tới | Trùng với QA-244 | — | Nhóm B. M15: thống kê kiểm duyệt |
| ISS-189 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm B. Dùng chung: múi giờ |
| ISS-191 | Sở hữu | Trùng với DEC-129 | — | Nhóm B. Giữ nhật ký kiểm duyệt vĩnh viễn |
| ISS-193 | Phụ thuộc | Trùng với DEC-131 | — | Nhóm B. M01: công bố việc AI bên thứ ba xử lý nội dung |
| ISS-195 | Phụ thuộc | Trùng với DEC-133 | — | Nhóm B. M13: nhật ký đầu ra AI |
| ISS-199 | Nhắc tới | Trùng với DEC-136 | — | Nhóm B. Công nghệ (email) |
| ISS-200 | Nhắc tới | Hiện hành | Không áp dụng: M10: nơi lưu cờ AI | Nhóm B. M10: nơi lưu cờ AI |
| ISS-234 | Phụ thuộc | Trùng với DEC-150 | — | Nhóm B. M01: Mod xem bài ẩn của tác giả đã vô hiệu hóa |
| ISS-244 | Phụ thuộc | Trùng với DEC-152 | — | Nhóm B. M01: ban tạm thời hết hạn |
| ISS-262 | Sở hữu | Trùng với DEC-161 | — | Nhóm B. Trạng thái kiểm duyệt bài mới; "gỡ bài" là gì |
| ISS-265 | Phụ thuộc | Trùng với DEC-163 | — | Nhóm B. M03: MEDIUM, HEAVY chặn thao tác nào trên bài |
| ISS-272 | Sở hữu | Trùng với DEC-169 | — | Nhóm B. Accepted Answer không có ở MS1 |
| ISS-276 | Nhắc tới | Trùng với DEC-172 | — | Nhóm B. M02: danh sách theo dõi và tài khoản BANNED |
| ISS-281 | Sở hữu | Trùng với DEC-177 | — | Nhóm B. Mod không gỡ avatar, bio khi xử lý báo cáo người dùng |
| ISS-282 | Phụ thuộc | Trùng với DEC-178 | — | Nhóm B. M04: sửa, xóa bình luận ở HEAVY, khi bị ẩn |
| ISS-283 | Sở hữu | Trùng với DEC-179 | — | Nhóm B. Mod xem nội dung bình luận đã xóa trong báo cáo |
| ISS-285 | Sở hữu | Trùng với DEC-180 | — | Nhóm B. Mod chỉ có thao tác Ẩn bình luận; quét AI bình luận giữ nguyên |
| ISS-286 | Nhắc tới | Trùng với DEC-181 | — | Nhóm B. M04: hiển thị luồng có bình luận bị ẩn |
| ISS-291 | Sở hữu | Trùng với DEC-185 | — | Nhóm B. Mod xem bài Tự ẩn bị báo cáo |
| ISS-ADMN-01 | Sở hữu | Bị thay bởi DEC-080 | — | Nhóm B. Ngưỡng số lần cảnh cáo để AI chuyển lên (Open; đối chiếu DEC-080 ở bước 2). Register vẫn ghi Open; DEC-080 đã đặt ngưỡng (vi phạm khi đang HEAVY) |
| ISS-AI-01 | Phụ thuộc | Bị thay bởi DEC-098 | — | Nhóm B. M13: hiệu chỉnh ngưỡng AI (Open; đối chiếu DEC-098 ở bước 2). Register vẫn ghi Open; DEC-098 đã đặt ngưỡng tạm 0,9/0,5 |
| ISS-REWD-02 | Phụ thuộc | Trùng với DEC-118 | — | Nhóm B. M12: mức cảnh cáo và bảng xếp hạng |
| OPEN-003 | Sở hữu | Hiện hành | Không áp dụng: báo cáo tin nhắn ngoài phạm vi MS1 (ghi ở 1.2 và B.2) | Nhóm B. Hoãn có chủ đích: chưa có báo cáo tin nhắn ở MS1 |
| OPEN-008 | Phụ thuộc | Sửa một phần bởi DEC-154, DEC-156 | Chuyển M01 | Nhóm B. M01: privacy — giữ nhật ký vĩnh viễn so với xóa dữ liệu cá nhân. Phần còn mở không chạm M08 |
| OPEN-011 | Nhắc tới | Sửa một phần bởi DEC-239, DEC-248 | Không áp dụng: M11, M16: xét áp nguyên tắc xóa mềm cho nội dung báo cáo được | Nhóm B. M11, M16: xét áp nguyên tắc xóa mềm cho nội dung báo cáo được |
| OPEN-012 | Phụ thuộc | Bị thay bởi DEC-201 | — | Nhóm B. M09: bình luận bị ẩn có hiện lại khi khiếu nại cảnh cáo/ban thành công |
| QA-007 | Nhắc tới | Hiện hành | Không áp dụng: AI Moderation API miễn phí | Nhóm B. AI Moderation API miễn phí |
| QA-011 | Sở hữu | Hiện hành | FR-M08-01, BR-M08-01 | Nhóm B. Khách không báo cáo bài, bình luận. DEC-171 (ngoài bảng nguồn) chỉ sửa quyền Guest xem hồ sơ |
| QA-013 | Phụ thuộc | Hiện hành | FR-M08-14 | Nhóm B. M10: Mod bị ban thì tự mất vai trò Mod |
| QA-015 | Phụ thuộc | Hiện hành | FR-M08-04 | Nhóm B. M11: Mod, Admin thấy danh tính thật của bài ẩn danh để cảnh cáo, ban |
| QA-016 | Phụ thuộc | Sửa một phần bởi DEC-104 | Chuyển M11 | Nhóm B. M11: Mod hệ thống can thiệp nội dung nhóm bất kỳ lúc nào |
| QA-017 | Sở hữu | Sửa một phần bởi DEC-077 | FR-M08-08 | Nhóm B. AI kiểm duyệt quét cả bài và bình luận. DEC-050 (ngoài bảng nguồn) sửa phần gợi ý Topic |
| QA-018 | Phụ thuộc | Sửa một phần bởi DEC-018, DEC-019, QA-019, DEC-152 | FR-M08-14, FR-M08-15, BR-M08-38 | Nhóm B. M01: cảnh cáo giữ ACTIVE; ban → BANNED; gỡ ban → ACTIVE. DEC-149 (ngoài bảng nguồn) sửa phần vô hiệu hóa |
| QA-019 | Sở hữu | Sửa một phần bởi QA-021, DEC-078, DEC-080, DEC-088, DEC-115, DEC-187, DEC-189 | FR-M08-09, FR-M08-10, FR-M08-11, FR-M08-14, FR-M08-15, BR-M08-33, BR-M08-38 | Nhóm B. Ban/gỡ ban do Mod và Admin; AI cảnh cáo, không ban; chuyển lên khi đạt ngưỡng cảnh cáo. Phần khiếu nại thuộc M09. Cơ chế chuyển lên ban: Q-03 |
| QA-020 | Sở hữu | Sửa một phần bởi DEC-079, DEC-186, DEC-188 | FR-M08-09, FR-M08-10, FR-M08-12, BR-M08-29, BR-M08-30 | Nhóm B. Mức cảnh cáo, thời gian thử thách tự giảm mức; chỉ báo công khai (bị thay); ngưỡng AI theo mức (bỏ, DEC-186) |
| QA-024 | Nhắc tới | Hiện hành | Không áp dụng: M13 thành Must vì M08 phụ thuộc | Nhóm B. M13 thành Must vì M08 phụ thuộc |
| QA-028 | Phụ thuộc | Trùng với DEC-012 | — | Nhóm B. M03: ai quyết định trạng thái nào của bài |
| QA-029 | Phụ thuộc | Bị thay bởi DEC-032 | — | Nhóm B. M03: giá trị trạng thái kiểm duyệt bài |
| QA-030 | Phụ thuộc | Trùng với DEC-013 | — | Nhóm B. M03: quét trước khi đăng |
| QA-042 | Sở hữu | Bị thay bởi DEC-072 | — | Nhóm B. 5 loại vi phạm + Khác (đối chiếu DEC-072 ở bước 2) |
| QA-062 | Phụ thuộc | Trùng với DEC-018 | — | Nhóm B. M01: trạng thái tài khoản |
| QA-063 | Phụ thuộc | Trùng với DEC-019 | — | Nhóm B. M01: màn hình BANNED |
| QA-082 | Phụ thuộc | Trùng với DEC-031 | — | Nhóm B. M03: giá trị trạng thái đăng |
| QA-083 | Phụ thuộc | Trùng với DEC-032 | — | Nhóm B. M03: giá trị trạng thái kiểm duyệt |
| QA-085 | Phụ thuộc | Trùng với DEC-034 | — | Nhóm B. M03: quét trước khi đăng chặn đăng |
| QA-094 | Nhắc tới | Trùng với DEC-041 | — | Nhóm B. M04: bình luận xấu → báo cáo |
| QA-123 | Phụ thuộc | Trùng với DEC-065 | — | Nhóm B. M07: danh sách sự kiện thông báo |
| QA-124 | Phụ thuộc | Trùng với DEC-065 | — | Nhóm B. M07: sự kiện có email (ban/gỡ ban) |
| QA-150 | Phụ thuộc | Trùng với DEC-084 | — | Nhóm B. M09: nội dung khiếu nại, bằng chứng như báo cáo |
| QA-151 | Phụ thuộc | Trùng với DEC-085 | — | Nhóm B. M09: tài khoản bị ban vào trang khiếu nại |
| QA-152 | Phụ thuộc | Trùng với DEC-085 | — | Nhóm B. M09: email ban dẫn tới khiếu nại |
| QA-153 | Phụ thuộc | Trùng với DEC-086 | — | Nhóm B. M09: hạn khiếu nại cảnh cáo, ban |
| QA-154 | Phụ thuộc | Hiện hành | Chuyển M09 | Nhóm B. M09: hạn khiếu nại ban vĩnh viễn |
| QA-156 | Phụ thuộc | Trùng với DEC-088 | — | Nhóm B. M09: hàng chờ khiếu nại tách riêng |
| QA-157 | Phụ thuộc | Trùng với DEC-088 | — | Nhóm B. M09: thứ tự ưu tiên khiếu nại |
| QA-158 | Phụ thuộc | Trùng với DEC-088 | — | Nhóm B. M09: Mod không thấy khiếu nại về hành động của mình |
| QA-159 | Phụ thuộc | Trùng với DEC-089 | — | Nhóm B. M09: khiếu nại thành công |
| QA-160 | Sở hữu | Trùng với DEC-090 | — | Nhóm B. Phạm vi Admin riêng và dùng chung với Mod |
| QA-165 | Phụ thuộc | Trùng với DEC-093 | — | Nhóm B. M10: công tắc AI tổng và theo module |
| QA-170 | Phụ thuộc | Trùng với DEC-097 | — | Nhóm B. M13: AI không phủ mọi lý do báo cáo |
| QA-171 | Sở hữu | Trùng với DEC-098 | — | Nhóm B. Điểm ≥ 0,9 tự ẩn bình luận, bỏ qua Mod |
| QA-172 | Sở hữu | Trùng với DEC-098 | — | Nhóm B. Cùng ngưỡng cho cổng nội dung và cảnh cáo |
| QA-175 | Phụ thuộc | Trùng với DEC-099 | — | Nhóm B. M13: thời gian chờ gọi AI |
| QA-177 | Phụ thuộc | Trùng với DEC-099 | — | Nhóm B. M03: quét bài lỗi thì giữ chờ Mod |
| QA-180 | Nhắc tới | Trùng với DEC-102 | — | Nhóm B. M11: quyền vai trò trong nhóm |
| QA-182 | Phụ thuộc | Trùng với DEC-104 | — | Nhóm B. M11: kiểm duyệt nhóm và M08 |
| QA-187 | Nhắc tới | Trùng với DEC-109 | — | Nhóm B. M11: xử lý cấp nhóm không khiếu nại |
| QA-191 | Phụ thuộc | Trùng với DEC-113 | — | Nhóm B. M12: trừ điểm ngay khi Mod/Admin gỡ nội dung vi phạm |
| QA-193 | Phụ thuộc | Trùng với DEC-115 | — | Nhóm B. M09: khiếu nại bài bị gỡ |
| QA-199 | Phụ thuộc | Trùng với DEC-118 | — | Nhóm B. M12: HEAVY và bảng xếp hạng |
| QA-204 | Phụ thuộc | Trùng với DEC-122 | — | Nhóm B. M12: tài khoản BANNED và bảng xếp hạng |
| QA-205 | Phụ thuộc | Trùng với DEC-122 | — | Nhóm B. M12: nhãn "Tài khoản đã bị khóa" |
| QA-214 | Nhắc tới | Hiện hành | Không áp dụng: M16: tin nhắn thu hồi xóa hẳn, không thuộc kiểm duyệt | Nhóm B. M16: tin nhắn thu hồi xóa hẳn, không thuộc kiểm duyệt |
| QA-217 | Nhắc tới | Hiện hành | Không áp dụng: M16: không quét AI tin nhắn | Nhóm B. M16: không quét AI tin nhắn |
| QA-218 | Sở hữu | Hiện hành | Không áp dụng: báo cáo tin nhắn ngoài phạm vi MS1 (ghi ở 1.2 và B.2) | Nhóm B. Không làm báo cáo tin nhắn ở MS1 (OPEN-003) |
| QA-219 | Nhắc tới | Hiện hành | Không áp dụng: M16: giới hạn tần suất chat | Nhóm B. M16: giới hạn tần suất chat |
| QA-223 | Nhắc tới | Hiện hành | Không áp dụng: M07: email chỉ cho mật khẩu, vô hiệu hóa, ban, khiếu nại | Nhóm B. M07: email chỉ cho mật khẩu, vô hiệu hóa, ban, khiếu nại |
| QA-227 | Nhắc tới | Trùng với DEC-126 | — | Nhóm B. M14: khách cần đăng nhập để báo cáo |
| QA-236 | Nhắc tới | Hiện hành | Không áp dụng: M14: Trending không loại bài của BANNED/HEAVY | Nhóm B. M14: Trending không loại bài của BANNED/HEAVY |
| QA-241 | Nhắc tới | Hiện hành | Không áp dụng: M15: chỉ Admin xem thống kê | Nhóm B. M15: chỉ Admin xem thống kê |
| QA-242 | Nhắc tới | Hiện hành | Không áp dụng: M15: thống kê theo mức cảnh cáo | Nhóm B. M15: thống kê theo mức cảnh cáo |
| QA-243 | Nhắc tới | Hiện hành | Không áp dụng: M15: thống kê bài theo trạng thái kiểm duyệt | Nhóm B. M15: thống kê bài theo trạng thái kiểm duyệt |
| QA-244 | Nhắc tới | Hiện hành | Không áp dụng: M15: thống kê báo cáo, cảnh cáo, ban, khiếu nại | Nhóm B. M15: thống kê báo cáo, cảnh cáo, ban, khiếu nại |
| QA-248 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm B. Dùng chung: múi giờ |
| QA-250 | Sở hữu | Trùng với DEC-129 | — | Nhóm B. Giữ nhật ký kiểm duyệt vĩnh viễn |
| QA-251 | Phụ thuộc | Trùng với DEC-130 | — | Nhóm B. Dùng chung: ảnh bằng chứng báo cáo 5MB, chỉ định dạng ảnh |
| QA-252 | Phụ thuộc | Trùng với DEC-131 | — | Nhóm B. M01: công bố AI bên thứ ba |
| QA-254 | Phụ thuộc | Trùng với DEC-133 | — | Nhóm B. M13: nhật ký đầu ra AI |
| QA-263 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ | Nhóm B. Công nghệ |
| QA-290 | Sở hữu | Trùng với DEC-146 | — | Nhóm B. Ghi thao tác Tag/Topic của Mod vào nhật ký kiểm duyệt |
| QA-294 | Phụ thuộc | Trùng với DEC-150 | — | Nhóm B. M01: Mod xem bài ẩn của tác giả đã vô hiệu hóa |
| QA-301 | Nhắc tới | Trùng với DEC-153 | — | Nhóm B. M01: BANNED không có trong gợi ý nhắc tên |
| QA-304 | Phụ thuộc | Trùng với DEC-152 | — | Nhóm B. M01: ban tạm thời hết hạn tự về ACTIVE |
| QA-308 | Nhắc tới | Trùng với DEC-151 | — | Nhóm B. M01: BANNED đặt lại mật khẩu để khiếu nại |
| QA-312 | Phụ thuộc | Trùng với DEC-156 | — | Nhóm B. M01: nhật ký kiểm duyệt gắn tài khoản đã xóa qua username |
| QA-314 | Phụ thuộc | Trùng với DEC-154 | — | Nhóm B. M01: trang chính sách có mục kiểm duyệt, cảnh cáo, khóa tài khoản |
| QA-322 | Sở hữu | Trùng với DEC-161 | — | Nhóm B. Bài mới ở Bình thường; "gỡ" bài là ẩn |
| QA-325 | Phụ thuộc | Trùng với DEC-163 | — | Nhóm B. M03: MEDIUM, HEAVY chặn thao tác nào |
| QA-328 | Nhắc tới | Hiện hành | Không áp dụng: M03: bài bị AI tự từ chối, khiếu nại qua M09 | Nhóm B. M03: bài bị AI tự từ chối, khiếu nại qua M09. Trùng với DEC-166 (ngoài bảng nguồn) |
| QA-329 | Phụ thuộc | Trùng với DEC-167 | — | Nhóm B. M03: khóa toàn bộ vẫn cho báo cáo |
| QA-332 | Sở hữu | Trùng với DEC-169 | — | Nhóm B. MS1 không có Accepted Answer |
| QA-336 | Nhắc tới | Trùng với DEC-172 | — | Nhóm B. M02: danh sách theo dõi không hiện tài khoản bị ban |
| QA-341 | Sở hữu | Trùng với DEC-177 | — | Nhóm B. Mod không gỡ avatar, bio |
| QA-342 | Phụ thuộc | Trùng với DEC-178 | — | Nhóm B. M04: sửa, xóa bình luận ở HEAVY, khi bị ẩn |
| QA-343 | Sở hữu | Trùng với DEC-179 | — | Nhóm B. Nội dung báo cáo được chỉ xóa mềm, Mod xem lại |
| QA-345 | Sở hữu | Trùng với DEC-180 | — | Nhóm B. Mod chỉ có thao tác Ẩn bình luận; giữ quét AI bình luận |
| QA-346 | Nhắc tới | Trùng với DEC-181 | — | Nhóm B. M04: bình luận gốc bị ẩn còn trả lời |
| QA-349 | Phụ thuộc | Trùng với DEC-179 | — | Nhóm B. M03, M04: chủ nội dung xem lại nội dung bị xử lý, không thấy thông tin người báo cáo |
| QA-351 | Sở hữu | Trùng với DEC-185 | — | Nhóm B. Mod xem bài Tự ẩn trong báo cáo |
| F-GRP-04 | Nhắc tới | Hiện hành | Không áp dụng: M11: công tắc duyệt trước trong nhóm | Nhóm B. M11: công tắc duyệt trước trong nhóm |
| F-POST-07 | Phụ thuộc | Hiện hành | Chuyển M03 | Nhóm B. M03: mô hình 3 trường trạng thái bài |
| F-POST-08 | Phụ thuộc | Sửa một phần bởi DEC-034, DEC-098, DEC-161 | Chuyển M03 | Nhóm B. M03: quét trước khi đăng |
| MR-A01 | Nhắc tới | Hiện hành | Không áp dụng: M16: còn OPEN-003 (chưa báo cáo tin nhắn) | Nhóm B. M16: còn OPEN-003 (chưa báo cáo tin nhắn) |
| MR-A02 | Nhắc tới | Hiện hành | Không áp dụng: M14: Trending và BANNED/HEAVY | Nhóm B. M14: Trending và BANNED/HEAVY |
| MR-A03 | Nhắc tới | Hiện hành | Không áp dụng: M15: thống kê kiểm duyệt | Nhóm B. M15: thống kê kiểm duyệt |
| MR-A04 | Phụ thuộc | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi riêng của M08 | Nhóm B. Phase 6: múi giờ, giữ nhật ký kiểm duyệt |
| MR-FB-M08 | Sở hữu | Sửa một phần bởi DEC-099 | FR-M08-02, FR-M08-08 | Nhóm B. AI tắt: chỉ hàng chờ kiểm duyệt thủ công |
| MR-M01 | Phụ thuộc | Sửa một phần bởi DEC-150, DEC-151, DEC-152, DEC-153 | Chuyển M01 | Nhóm B. M01: trạng thái tài khoản BANNED. DEC-147, DEC-148, DEC-149 (ngoài bảng nguồn) không chạm M08 |
| MR-M03 | Phụ thuộc | Sửa một phần bởi DEC-184, DEC-185 | Chuyển M03 | Nhóm B. M03: trạng thái bài, quét trước khi đăng. DEC-160 (ngoài bảng nguồn) không chạm M08 |
| MR-M07 | Phụ thuộc | Sửa một phần bởi DEC-135, QA-257 | Chuyển M07 | Nhóm B. M07: email chỉ cho bảo mật và ban |
| MR-M09 | Phụ thuộc | Hiện hành | Chuyển M09 | Nhóm B. M09: khiếu nại cảnh cáo, ban |
| MR-M11 | Nhắc tới | Hiện hành | Không áp dụng: M11: phụ thuộc M08 | Nhóm B. M11: phụ thuộc M08 |
| MR-M12 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B. M12: HEAVY, BANNED bị loại khỏi bảng xếp hạng |
| MR-M13 | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B. M13: Moderation API 4 nhóm, ngưỡng 0,9/0,5, AI tắt và AI lỗi |
| MR-M15 | Nhắc tới | Hiện hành | Không áp dụng: M15: phụ thuộc M08 | Nhóm B. M15: phụ thuộc M08 |
| DEC-039 | Nhắc tới | Sửa một phần bởi DEC-183 | Không áp dụng: M04: trình soạn bình luận (DEC-083 dẫn tới) | Nhóm C. M04: trình soạn bình luận (DEC-083 dẫn tới) |
| QA-021 | Phụ thuộc | Hiện hành | FR-M08-17 | Nhóm C. M09: Mod không xét khiếu nại về hành động của mình (DEC-081 dẫn tới cho ngoại lệ xem nhật ký) |
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M08 | Nhóm D. Dùng chung; không quy định hành vi M08 |
| DEC-132 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M08 | Nhóm D. Dùng chung; không quy định hành vi M08. DEC-141, DEC-144 (ngoài bảng nguồn) chỉ sửa phần Topic |
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ | Nhóm D. Công nghệ |
| DEC-135 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: kênh thời gian thực cho thông báo; không quy định hành vi M08 | Nhóm D. Dùng chung: kênh thời gian thực cho thông báo; không quy định hành vi M08 |
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M08 | Nhóm D. Dùng chung; không quy định hành vi M08. DEC-155, DEC-157 (ngoài bảng nguồn) chỉ sửa phần đồng ý chính sách |
| ISS-190 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M08 |
| ISS-192 | Phụ thuộc | Trùng với DEC-130 | — | Nhóm D. Dùng chung: tải ảnh (ảnh bằng chứng) |
| ISS-194 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M08 |
| ISS-196 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M08 | Nhóm D. Dùng chung; không quy định hành vi M08 |
| ISS-197 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Công nghệ |
| ISS-198 | Nhắc tới | Trùng với DEC-135 | — | Nhóm D. Dùng chung; không quy định hành vi M08 |
| ISS-201 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M08 | Nhóm D. Dùng chung; không quy định hành vi M08 |
| ISS-202 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M08 | Nhóm D. Dùng chung; không quy định hành vi M08 |
| ISS-203 | Nhắc tới | Trùng với QA-263 | — | Nhóm D. Công nghệ |
| ISS-204 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M08 |
| QA-249 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M08 |
| QA-253 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M08 |
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M08 | Nhóm D. Dùng chung; không quy định hành vi M08 |
| QA-256 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Công nghệ |
| QA-257 | Nhắc tới | Trùng với DEC-135 | — | Nhóm D. Dùng chung; không quy định hành vi M08 |
| QA-258 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Công nghệ |
| QA-259 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M08 | Nhóm D. Dùng chung; không quy định hành vi M08 |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M08 | Nhóm D. Dùng chung; không quy định hành vi M08 |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M08 | Nhóm D. Dùng chung; không quy định hành vi M08 |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M08 | Nhóm D. Dùng chung; không quy định hành vi M08 |
| QA-264 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M08 |
| MR-A05 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ | Nhóm D. Công nghệ |
| DEC-224 | Phụ thuộc | Hiện hành | FR-M08-17, FR-M08-17.06, BR-M08-41 | Nhóm B (đối chiếu FR-M10). M10: Admin theo dõi Mod qua nhật ký kiểm duyệt lọc theo người làm |
| DEC-227 | Phụ thuộc | Hiện hành | Chuyển M10 | Nhóm B (đối chiếu FR-M10). M10: phạm vi nhật ký thao tác Admin, gồm thao tác kiểm duyệt của Admin ghi song song với nhật ký kiểm duyệt |
| DEC-195 | Sở hữu | Hiện hành | FR-M08-01, FR-M08-02, FR-M08-03, FR-M08-08, BR-M08-46, BR-M08-55 | Nhóm B (rà lại 1.3). M09: không báo cáo được Admin; vụ về Mod chỉ Admin xử lý; nội dung Admin không bị quét. DEC-240 chỉ sửa phần bài của Owner nhóm |
| DEC-197 | Sở hữu | Hiện hành | FR-M08-09, FR-M08-10 | Nhóm B (rà lại 1.3). M09: mọi thông báo về thao tác khiếu nại được đều kèm đường dẫn khiếu nại |
| DEC-201 | Phụ thuộc | Hiện hành | Chuyển M09 | Nhóm B (rà lại 1.3). M09: bình luận bị ẩn không hiện lại khi cảnh cáo, ban liên quan bị lật; đóng OPEN-012 |
| DEC-239 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B (rà lại 1.3). M11: nội dung nhóm mất đi đều là xóa mềm; đóng phần M11 của OPEN-011 |
| DEC-241 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B (rà lại 1.3). M12: bình luận bị AI ẩn ≥ 0,9 trừ điểm ngay; 0,5–< 0,9 trừ khi Mod kết luận vi phạm |
| DEC-248 | Nhắc tới | Hiện hành | Không áp dụng: đóng TBD-M08-02 | Đối chiếu FR-M16 (bản 1.4). M16: thu hồi tin nhắn là xóa mềm |
| DEC-235 | Phụ thuộc | Hiện hành | FR-M08-18.05; Chuyển M11 | Rà soát chéo 2026-10-24. M11: nhóm Bị khóa chặn thêm các thao tác quản lý của Owner, Group Mod |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| DM-10.1, QA-042, ISS-050 → DEC-072, DEC-076 → DEC-191, DEC-194; DM-6.3 → QA-218 | Đối tượng báo cáo: bài viết, bình luận, người dùng, nhóm; không có tin nhắn ở MS1 (QA-218, OPEN-003 → TBD-M08-01). Lý do riêng theo loại (bài 8, bình luận 7, người dùng 2, nhóm 4), mỗi báo cáo một lý do (DEC-190). Trạng thái báo cáo Mở → Đã xử lý (có xử lý / bác bỏ). Không báo cáo nội dung, tài khoản của chính mình; một người chỉ một báo cáo trong vụ đang Mở; người ở HEAVY vẫn báo cáo; đối tượng không còn hiển thị thì từ chối; không rút, không sửa (DEC-191). Vụ về nhóm: người bị báo cáo là Owner, xử lý bằng Ẩn hoặc Khóa nhóm (DEC-194). |
| DM-10.2, GL:Moderator (MOD) → DEC-161, DEC-169, DEC-180, DEC-187 | Mod, Admin "xóa bài" là ẩn bài (Bị ẩn); "xóa bình luận" là ẩn bình luận; không có gỡ Accepted Answer; khóa bài thuộc M03. Cảnh cáo, ban giữ nguyên. "Suspend" là ban tạm thời; không có thao tác suspend riêng (DEC-187). |
| DM-10.3 → DEC-080, DEC-090, DEC-187, DEC-189 | Ban do Mod và Admin cùng làm; chỉ Admin cảnh cáo, ban tài khoản Mod; tài khoản Admin không bị cảnh cáo, ban (DEC-189); đổi vai trò thuộc M10. Không có "Disable account"; "Suspend account" là ban tạm thời (DEC-187). |
| DM-10.4 → DEC-081 → DEC-146, DEC-193, DEC-224 | Nhật ký ghi: người làm (Mod, Admin hoặc AI), loại thao tác (cảnh cáo, bỏ cảnh cáo AI, ban, gỡ ban, ẩn nội dung, ẩn, khóa, mở khóa nhóm, kết luận vụ; vô hiệu hóa, kích hoạt lại Tag và đổi Topic/Tag trên bài người khác), đối tượng, lý do, thời điểm. Không ghi nhận, nhả vụ; dòng nhật ký không sửa, không xóa (DEC-193). Quyền xem giữ nguyên DEC-081. Admin lọc nhật ký theo người làm để theo dõi từng Mod (DEC-224). |
| DEC-081, DEC-129 → DEC-156, DEC-179, DEC-184 | Nhật ký giữ vĩnh viễn. Người làm đã xóa tài khoản hiện "[Người dùng đã xóa]" nhưng vẫn tra được qua username. Câu "bài, bình luận bị xóa hẳn" trong DEC-129 không còn đúng: bài, bình luận chỉ xóa mềm. |
| QA-017, DM-11.1, DG-6 → DEC-077 → DEC-098, DEC-180, DEC-186, DEC-190 | Bình luận đăng ngay, không quét mặc định; chỉ quét cả luồng khi số trả lời trong khoảng thời gian trượt đạt ngưỡng tốc độ trở lên (chỉ đếm trả lời; con số chưa chốt, TBD-M08-04). Điểm quét là điểm cao nhất trong bốn nhóm (DEC-186). Điểm ≥ 0,9: ẩn ngay, không qua Mod; 0,5 đến < 0,9: ẩn và thành mục do "Hệ thống (AI)" tạo trong vụ ở hàng chờ báo cáo (DEC-190); < 0,5: giữ nguyên. Bình luận bị ẩn không hiện trong luồng với ai, kể cả tác giả. DEC-097: AI không phát hiện Spam, đạo văn, sai lệch; các loại này chỉ qua báo cáo. |
| QA-019 → DEC-078 → DEC-098, DEC-186 | AI chỉ tự cảnh cáo khi điểm ≥ 0,9, mỗi nội dung một cảnh cáo; từ 0,5 đến < 0,9 thì Mod quyết khi xét. Ý "AI cảnh cáo trực tiếp nội dung borderline" của QA-019 bị thay. AI không bao giờ ban; không tự cảnh cáo Mod (nội dung của Mod ≥ 0,9 đưa vào vụ để Admin quyết) và Admin (DEC-186, DEC-189). Mod, Admin được bỏ cảnh cáo do AI ra (QA-019); hệ quả theo DEC-188. |
| QA-019, ISS-ADMN-01 → DEC-080 → DEC-152, DEC-187; QA-018 → QA-019 | Người đang ở HEAVY vi phạm tiếp (lần thứ 7) không nhận cảnh cáo mới; vụ của nội dung đó thành yêu cầu ban, Mod, Admin quyết và chọn "Ban" (DEC-187). Ban tạm thời 30 ngày → 90 ngày → vĩnh viễn theo số lần đã bị ban: tính mọi ban từng có hiệu lực, kể cả ban được gỡ sớm và ban vĩnh viễn thủ công, trừ ban bị lật do khiếu nại (DEC-187). Ban vĩnh viễn thủ công. Không ban chồng. Hết hạn thì tự về ACTIVE (DEC-152, M01). Gỡ ban do Mod hoặc Admin, trực tiếp không qua vụ (QA-019 thay "admin unban" của QA-018; DEC-190). Chỉ Admin ban Mod (DEC-189). |
| QA-020 → DEC-079 → DEC-118, DEC-122, DEC-163, DEC-178, DEC-188; QA-020 → DEC-186 | Mức theo số lần cảnh cáo (1–2 LIGHT, 3–4 MEDIUM, 5–6 HEAVY) giữ. Thời gian thử thách 7/10/15 ngày thay 5/10/14, tính đủ N × 24 giờ (DEC-188). Cảnh cáo mới không đổi mức thì chỉ đặt lại thời gian thử thách (QA-020). Hết thời gian thử thách: giảm một bậc, số lần về số lần cao nhất của mức dưới (4, 2, 0), mức mới có thời gian thử thách riêng nối tiếp (DEC-188). Bỏ hoặc lật cảnh cáo: số lần giảm 1, bản ghi giữ, thời điểm kết thúc thử thách không đổi (DEC-188). Chỉ báo công khai của QA-020 bị thay bằng riêng tư hoàn toàn; ngoại lệ duy nhất: HEAVY và BANNED bị loại khỏi bảng xếp hạng (M12; ISS-154, ISS-REWD-02, MR-M12, QA-199 nhắc lại). MEDIUM, HEAVY chặn đưa bài chưa từng công khai ra công khai (DEC-163); HEAVY chỉ chặn tạo bình luận mới (DEC-178). Ngưỡng AI theo mức cảnh cáo của QA-020 bị bỏ: một cặp 0,9/0,5 cho mọi người (DEC-186). |
| QA-019, QA-020 → QA-021, DEC-088, DEC-115 | Phần khiếu nại thuộc M09: Mod xét khiếu nại trừ hành động của chính mình; có khiếu nại bài bị gỡ (không có cho bình luận). |
| ISS-AI-01 → DEC-098 → DEC-161, DEC-186 | Một cặp ngưỡng tạm 0,9/0,5 dùng cho cả cổng nội dung và cảnh cáo, cả bài và bình luận, mọi tác giả (DEC-186). Quét lại bài đã sửa ≥ 0,5 → Bị gắn cờ, không tự từ chối. DEC-166 (ngoài bảng nguồn) chỉ sửa phần bài bị AI từ chối (M03). |
| DEC-008, MR-FB-M08 → DEC-093, DEC-099 | Khi công tắc AI tổng hoặc công tắc Moderation tắt: không quét, nội dung đăng thẳng, chỉ dựa vào báo cáo; "hàng chờ thủ công" là hàng chờ báo cáo. AI lỗi khi quét bình luận: giữ nguyên, ghi lỗi cho Admin. DEC-092, ISS-200, QA-259 chỉ làm rõ nơi lưu cờ (M10). |
| DEC-012, QA-029 → DEC-032 → DEC-161 → DEC-185; DEC-032 → DEC-190; DEC-168 → DEC-185; DEC-013 → DEC-034, DEC-161 | Trạng thái kiểm duyệt bài: Bình thường, Bị gắn cờ, Bị ẩn; "gỡ" là Bị ẩn. Chỉ AI quét lại (M03) làm bài Bị gắn cờ; báo cáo của người dùng không đổi trạng thái (DEC-190). Bài Bị gắn cờ thành mục do AI tạo trong vụ ở hàng chờ báo cáo (DEC-190). Mod, Admin xem bài Bị gắn cờ, Bị ẩn qua M08, M09; bài Tự ẩn, Đã xóa hẳn chỉ trong báo cáo, lịch sử báo cáo, khiếu nại. Quét bài thuộc M03. |
| DEC-065 → DEC-151, DEC-180 | Sự kiện kết quả báo cáo, cảnh cáo: trong ứng dụng; ban, gỡ ban: trong ứng dụng và email; thêm "Bình luận của bạn đã bị ẩn" (trong ứng dụng). DEC-147 (ngoài bảng nguồn) chỉ thêm sự kiện liên kết Google. |
| DM-4.2.1, DG-4, DG-5, GL:Comment, DM-2.1, DM-8.1, DM-x02 → DEC-169 | Không có Accepted Answer ở MS1. |
| QA-016, DM-5.3 → DEC-104 | Báo cáo M08 và Mod hệ thống áp dụng cả cho nội dung nhóm; cổng duyệt của nhóm thuộc M11. |
| DEC-019 → DEC-150, DEC-156; QA-018 → DEC-018, DEC-019, DEC-152; DEC-018 → DEC-085 | M01: màn hình BANNED (lý do, thời gian khiếu nại, nút khiếu nại, OK đăng xuất) giữ nguyên. DEC-148, DEC-149 (ngoài bảng nguồn) chỉ sửa thời hạn vô hiệu hóa, username, email. |
| DEC-131 → DEC-146, DEC-154; OPEN-008 → DEC-154, DEC-156 | M01: trang chính sách. Phần còn mở của OPEN-008 (email liên hệ, nhận bản sao dữ liệu) không chạm M08. |
| DEC-033 → DEC-167; DEC-162 → DEC-184; DEC-012 → DEC-031, DEC-033; DEC-034 → DEC-098; F-POST-08 → DEC-034, DEC-098, DEC-161; MR-M03 → DEC-184, DEC-185 | M03, giữ như FR-M03. Bài khóa toàn bộ vẫn báo cáo được (DEC-167). |
| DEC-025 → DEC-172; MR-M01 → DEC-150, DEC-151, DEC-152, DEC-153; MR-M07 → DEC-135, QA-257; DEC-039 → DEC-183; DG-6 → QA-007; DM-x02 → QA-007 | Chỉ sửa phần thuộc module khác, không đổi nội dung M08. |
| DEC-075 → DEC-190; QA-019 → DEC-189 | Mọi xử lý (ẩn nội dung, cảnh cáo, ban, ẩn, khóa nhóm) chỉ trong vụ đang giữ; ngoại lệ gỡ ban, mở khóa nhóm. Điểm ưu tiên = mức nặng cao nhất + số báo cáo × 2, mức nặng 10/5/2 (BR-M08-06); bằng điểm thì vụ mở trước đứng trước; 30 phút không thao tác tính từ thao tác cuối của người giữ (mở xem, ẩn, cảnh cáo, ban, kết luận). Mod, Admin không thấy, không nhận vụ nhắm vào chính mình (DEC-189). |
| DEC-074, DEC-082 → DEC-192 | Lý do kết luận bắt buộc với cả Có xử lý và Bác bỏ. Người báo cáo nhận một trong hai ý chung ("đã có biện pháp xử lý", "không phát hiện vi phạm") cho mọi loại đối tượng; mục do AI tạo không có thông báo. Người bị báo cáo chỉ nhận thông báo khi Có xử lý; đường dẫn khiếu nại chỉ kèm với cảnh cáo, ban, bài bị ẩn. Chỉ số tập trung tính cho đối tượng của vụ đang xem, trong 90 × 24 giờ. |
| MR-M08 → DEC-186, DEC-187, DEC-188, DEC-189, DEC-190, DEC-191, DEC-192, DEC-193, DEC-194 | Dòng module-registry của M08 được bổ sung bởi các quyết định FR M08 (DEC-186 đến DEC-194); nội dung hiện hành như các chuỗi trên. |
| Mục ngoài bảng nguồn | DEC-141 (DEC-090), DEC-144 (DEC-100), DEC-160 (DEC-130), DEC-141, DEC-144 (DEC-132), DEC-155, DEC-157 (DEC-138), DEC-159 (DEC-156), DEC-171 (DEC-025, QA-011), DEC-050 (QA-017), DEC-147, DEC-148, DEC-149 (MR-M01), DEC-160 (MR-M03): chỉ sửa phần không thuộc M08. |
| DEC-079 → DEC-211; QA-011 → DEC-208 (M06) | M08 vẫn chỉ cung cấp mức HEAVY cho M06. Cách áp do M06 quyết: Điểm cuối của bài × 0,5, ở cả tìm ngữ nghĩa và full-text, chỉ khi xếp theo Liên quan; không giảm hạng khi xếp Mới nhất, Nhiều upvote nhất; không hiện dấu hiệu (DEC-211, khớp BR-M08-31). DEC-208 chỉ nói cách Guest tìm bài. |
| DEC-094 → DEC-227, DEC-228; QA-013 → DEC-223; DEC-065 → DEC-221 (đối chiếu FR-M10) | Nhật ký thao tác Admin (M10) ghi song song thao tác kiểm duyệt của Admin; nhật ký kiểm duyệt M08 không đổi, chỉ thêm việc Admin lọc theo người làm (DEC-224). Mod bị ban vẫn mất vai trò Mod (M10 thực hiện); tự từ chức và sự kiện "Đề xuất làm Admin" thuộc M10, M07, không chạm M08. |
| DEC-189, DEC-191, DEC-186 → DEC-195 | Vụ về bài viết, bình luận, tài khoản của Mod chỉ Admin thấy và xử lý; không ai báo cáo được Admin (bài, bình luận, tài khoản, nhóm có Owner là Admin); nội dung của Admin không bị AI quét. Các phần khác của DEC-189, DEC-191, DEC-186 giữ nguyên. |
| DEC-074, DEC-078 → DEC-192 → DEC-197 | Mọi thông báo về thao tác khiếu nại được (cảnh cáo kể cả do AI, ban, bài bị ẩn) kèm đường dẫn khiếu nại; bình luận bị ẩn, nhóm bị ẩn hoặc khóa thì không. |
| OPEN-012 → DEC-201 | Bình luận bị ẩn không hiện lại khi cảnh cáo, ban gắn với nó bị lật. |
| OPEN-011 → DEC-239, DEC-248 | Đã đóng: nội dung nhóm mất đi đều là xóa mềm (DEC-239); thu hồi tin nhắn chat là xóa mềm, nội dung giữ, không ai xem được ở MS1 (DEC-248). TBD-M08-02 đóng. |
| DEC-194 → DEC-235 | Nhóm Bị khóa: M08 quyết việc khóa và mở khóa; danh sách đầy đủ thao tác bị chặn và vẫn được làm thuộc M11 (BR-M11-28), gồm thêm duyệt, gỡ, kick, chặn, bổ nhiệm, đổi cài đặt, xóa nhóm, Owner rời nhóm (rà soát chéo 2026-10-24). |
| DEC-065 → DEC-231, DEC-237, DEC-246; DEC-104 → DEC-230, DEC-233, DEC-240; DEC-108 → DEC-234; DEC-118 → DEC-242, DEC-246; DEC-167, QA-018 → DEC-246; DEC-195 → DEC-240 | Không đổi hành vi M08. DEC-231, DEC-237, DEC-246: sự kiện thông báo của M11, M12 (đạt huy hiệu là "mốc điểm"); DEC-230, DEC-233, DEC-240: cổng duyệt của nhóm và hàng chờ của Mod hệ thống cho bài của Owner nhóm (M03, M11); Mod, Admin không là thành viên chỉ xem nội dung nhóm Private trong vụ đang giữ, như FR-M08 đã ghi; DEC-234: người ngoài nhóm báo cáo bài nhóm Public như bài thường; DEC-242, DEC-246: bảng xếp hạng (M12), mức HEAVY và BANNED vẫn bị loại; DEC-240: Admin vẫn không bị quét. |
