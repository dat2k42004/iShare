---
module: M09
ten_module: Appeal
ma_tai_lieu: FR-M09
phien_ban: 1.0
trang_thai: Đã chốt
ngay: 2026-10-18
tac_gia: Phạm Văn Đức
moc_nguon: DEC-202, QA-383, ISS-323, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M09 Appeal

| Mã tài liệu | FR-M09 |
|---|---|
| Dự án | iShare |
| Module | M09 — Appeal |
| Trạng thái | Đã chốt |
| Phiên bản | 1.0 |
| Ngày | 2026-10-18 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Khiếu nại cho phép người dùng phản đối một quyết định kiểm duyệt mà họ cho là sai: cảnh cáo (do AI, Mod hoặc Admin ra),
ban, bài viết bị Mod, Admin gỡ vì vi phạm, hoặc bài viết bị AI tự từ chối. Người dùng gửi lời giải thích kèm bằng chứng
trong thời hạn gắn với xử lý; người bị ban vẫn đăng nhập được để khiếu nại lệnh ban. Mod, Admin xét khiếu nại theo một
hàng chờ riêng, không ai xét khiếu nại về thao tác của chính mình, và khiếu nại do Mod gửi chỉ Admin xét; khiếu nại được
chấp nhận thì xử lý bị lật.

### 1.2 Phạm vi

**Trong phạm vi:**

- Gửi khiếu nại: lời giải thích bắt buộc, bằng chứng tùy chọn (tối đa 3 ảnh, mỗi ảnh tối đa 5MB, như báo cáo). Đối tượng
  khiếu nại được: cảnh cáo (kể cả cảnh cáo do AI tự ra), ban tạm thời, ban vĩnh viễn, bài viết bị Mod, Admin gỡ vì vi
  phạm, bài viết bị AI tự từ chối (khiếu nại gộp với cảnh cáo AI ra cùng lần).
- Điều kiện gửi: hạn khiếu nại theo loại xử lý (cảnh cáo: 7, 10 hoặc 15 ngày theo mức của chính cảnh cáo đó; ban tạm
  thời: cả thời hạn ban; ban vĩnh viễn: 90 ngày; bài bị gỡ: 30 ngày; bài bị AI tự từ chối: theo hạn của cảnh cáo đi kèm,
  không có cảnh cáo thì 3 ngày), tính theo giờ Việt Nam; mỗi xử lý chỉ khiếu nại một lần; khiếu nại bị từ chối là cuối
  cùng; không rút, không sửa khiếu nại đã gửi.
- Lối vào khiếu nại: nút Khiếu nại trong mọi thông báo về một xử lý khiếu nại được, bất kể ai ra xử lý; nút "Gửi khiếu
  nại" trên màn hình tài khoản bị khóa (khi còn hạn); đường dẫn trong email ban, đi qua đăng nhập nếu cần. Trong lúc bị
  ban, tài khoản chỉ khiếu nại được chính lệnh ban.
- Hàng chờ khiếu nại: tách khỏi hàng chờ báo cáo; một danh sách chung xếp khiếu nại ban, rồi cảnh cáo, rồi bài viết,
  cùng loại thì gửi trước xét trước, lọc được theo loại; nhận xử lý và tự nhả sau 30 phút không thao tác.
- Người xét: Mod không thấy khiếu nại về thao tác của chính mình và khiếu nại do một Mod gửi; khiếu nại do Mod gửi chỉ
  Admin xét; Admin xét được mọi khiếu nại.
- Xét khiếu nại: chấp nhận hoặc từ chối, lý do kết luận bắt buộc; người xét xem chi tiết xử lý bị khiếu nại, nội dung
  liên quan (kể cả nội dung đã xóa, tự ẩn) và nhật ký quyết định AI của bài bị AI tự từ chối.
- Đảo ngược khi khiếu nại được chấp nhận: ban → bản ghi giữ, đánh dấu bị lật, tài khoản về hoạt động (người từng là Mod
  về với vai trò User); cảnh cáo → giảm số lần cảnh cáo, tính lại mức; bài bị gỡ → khôi phục bài, hoàn điểm đã trừ, lật
  cảnh cáo, ban đi kèm (mỗi xử lý đi kèm chỉ bị lật một lần, theo khiếu nại được chấp nhận trước); bài bị AI tự từ chối →
  đăng ngay không quét lại, lật cảnh cáo AI đi kèm. Vẫn lật khi xử lý đã kết thúc trước lúc xét.
- Người khiếu nại xem khiếu nại của mình, kết luận và lý do; mở xem lại (chỉ đọc) nội dung bị xử lý từ khiếu nại.
- Nội dung thông báo kết luận khiếu nại cho người khiếu nại.

**Ngoài phạm vi:**

- Ra cảnh cáo, ban, gỡ ban, ẩn bài; mức cảnh cáo và cách tính lại mức khi số lần giảm; số lần đã bị ban; nhật ký kiểm
  duyệt và quyền Mod xem thao tác của Mod khác khi xét khiếu nại; Admin không bị báo cáo, vụ về Mod chỉ Admin xử lý —
  M08 Moderation.
- Trạng thái BANNED, màn hình tài khoản bị khóa (lý do, thời gian khiếu nại còn lại, nút OK đăng xuất), đặt lại mật khẩu
  cho tài khoản BANNED, tự về ACTIVE khi ban tạm thời hết hạn — M01 Authentication & Account.
- Trạng thái kiểm duyệt và trạng thái đăng của bài, việc AI tự từ chối bài, bài của Admin không quét, không duyệt, tác
  giả xem lại bài đã bị xử lý — M03 Post & Content. Bình luận bị ẩn, chủ bình luận xem lại bình luận đã bị xử lý — M04
  Comment.
- Kênh gửi thông báo (trong ứng dụng, email) — M07 Notification.
- Phân quyền Admin, Mod; Mod bị ban mất vai trò Mod; đề xuất làm Mod; hằng số chính sách (thời hạn) không cấu hình qua
  giao diện — M10 Admin Panel.
- Trừ và hoàn điểm, huy hiệu, bảng xếp hạng — M12 Gamification.
- Nhật ký quyết định AI — M13 AI Layer.
- Thống kê khiếu nại theo loại và kết quả — M15 Analytics & Stats.
- Đã quyết không làm: khiếu nại của Admin (Admin không bị báo cáo, cảnh cáo, ban); khiếu nại bình luận bị ẩn, và bình
  luận hiện lại khi cảnh cáo, ban liên quan bị lật; khiếu nại thao tác kiểm duyệt cấp nhóm (Group Mod, Owner); khiếu nại
  nhóm bị ẩn hoặc bị khóa; khiếu nại việc giáng cấp Mod; khiếu nại cảnh cáo, bài bị gỡ trong lúc bị ban; khiếu nại riêng
  cảnh cáo AI ra cùng lần từ chối bài; gửi lại khiếu nại đã bị từ chối; rút, sửa khiếu nại; trả lại vai trò Mod khi lật
  ban; bước chuyển khiếu nại lên Admin riêng; AI xét khiếu nại; hạn khiếu nại không giới hạn cho ban vĩnh viễn; bản chụp
  nội dung lúc xử lý (xem B.3).

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Khiếu nại | Yêu cầu người dùng gửi để phản đối một xử lý kiểm duyệt mà họ cho là sai; trên giao diện gọi là "Khiếu nại". |
| Xử lý bị khiếu nại | Một trong: một cảnh cáo, một ban, một lần bài viết bị gỡ, một lần bài viết bị AI tự từ chối (BR-M09-01). Mỗi khiếu nại nhắm vào đúng một xử lý; khiếu nại gộp nhắm vào một lần từ chối bài cùng cảnh cáo AI ra cùng lần. |
| Loại khiếu nại | Ban, cảnh cáo hoặc bài viết; xác định theo xử lý bị khiếu nại. Khiếu nại bài bị gỡ và khiếu nại gộp đều thuộc loại bài viết. |
| Khiếu nại gộp | Một khiếu nại cho cả một bài bị AI tự từ chối và cảnh cáo AI ra cùng lần từ chối đó (BR-M09-24). |
| Người khiếu nại | Người dùng đã gửi khiếu nại; là người bị cảnh cáo, người bị ban, hoặc tác giả bài bị gỡ hay bị AI tự từ chối. |
| Người ra xử lý | Mod, Admin hoặc AI đã đưa ra xử lý bị khiếu nại. |
| Vai trò lúc bị xử lý | Vai trò của người khiếu nại tại thời điểm có xử lý; dùng để quyết ai xét khiếu nại. Mod bị ban mất vai trò Mod nhưng khiếu nại ban đó vẫn tính là khiếu nại do Mod gửi. |
| Bài bị gỡ | Bài viết bị Mod, Admin chuyển sang trạng thái kiểm duyệt Bị ẩn vì vi phạm (M03, M08; FR-M03 gọi là "Bị Mod ẩn"). |
| Bài bị AI tự từ chối | Bài viết mới gửi bị AI từ chối vì điểm quét từ 0,9 trở lên, trạng thái đăng Bị từ chối, chưa từng được đăng (M03). |
| Lời giải thích | Phần văn bản bắt buộc của khiếu nại, người khiếu nại trình bày vì sao xử lý là sai. |
| Bằng chứng | Ảnh người khiếu nại đính kèm khiếu nại (BR-M09-03). |
| Thời điểm gửi khiếu nại | Lúc hệ thống nhận một khiếu nại hợp lệ; dùng để so với hạn khiếu nại và để xếp thứ tự trong hàng chờ. |
| Hạn khiếu nại | Khoảng thời gian, tính từ lúc có xử lý, mà người bị xử lý được gửi khiếu nại (BR-M09-04). Quá hạn thì không gửi được nữa. |
| Thời gian thử thách | Khoảng thời gian gắn với mức cảnh cáo (LIGHT 7 ngày, MEDIUM 10 ngày, HEAVY 15 ngày), định nghĩa ở M08. |
| Ban tạm thời, ban vĩnh viễn | Ban có thời hạn (30 hoặc 90 ngày) và ban không thời hạn, định nghĩa ở M08. |
| Số lần cảnh cáo, mức cảnh cáo | Số cảnh cáo đang được tính và mức suy ra từ đó (Sạch, LIGHT, MEDIUM, HEAVY), định nghĩa ở M08. |
| Số lần đã bị ban | Số ban trước đó dùng để tính thời hạn ban, định nghĩa ở M08; không gồm ban bị lật. |
| Hàng chờ khiếu nại | Một danh sách chung các khiếu nại đang chờ xét, tách khỏi hàng chờ báo cáo của M08, xếp theo loại rồi thời điểm gửi, lọc được theo loại (BR-M09-09, BR-M09-10). |
| Nhận xử lý | Thao tác Mod, Admin giữ một khiếu nại cho riêng mình; trong lúc giữ, người khác không xét được khiếu nại đó. |
| Kết luận khiếu nại | Việc người đang giữ khiếu nại đóng khiếu nại với một trong hai kết quả: Chấp nhận hoặc Từ chối, kèm lý do kết luận. |
| Lý do kết luận khiếu nại | Lời người xét ghi khi kết luận; bắt buộc ở cả hai kết quả; người khiếu nại thấy được (BR-M09-27). |
| Lật | Hệ quả của khiếu nại được chấp nhận: xử lý bị khiếu nại thôi hiệu lực, bản ghi của nó được giữ và đánh dấu "bị lật". |
| Nhật ký quyết định AI | Bản ghi đầu ra của mỗi lần gọi AI, gắn với bài viết, bình luận liên quan (M13). |
| Màn hình tài khoản bị khóa | Màn hình duy nhất tài khoản BANNED thấy sau khi đăng nhập (M01). |
| Giờ Việt Nam | Múi giờ Asia/Ho_Chi_Minh (UTC+7), không đổi giờ mùa hè; mọi thời điểm hiển thị và ranh giới thời gian tính theo múi giờ này. |
| Hằng số chính sách | Hạn khiếu nại và giới hạn bằng chứng; không cấu hình qua giao diện. |
| Trạng thái khiếu nại | Chờ xét (chưa ai giữ hoặc đang được giữ) và Đã kết luận (Chấp nhận hoặc Từ chối). |
| Trạng thái của ban | Đang hiệu lực, Hết hạn, Đã gỡ (định nghĩa ở M08) và Bị lật (do khiếu nại được chấp nhận). |
| Trạng thái của cảnh cáo | Đang tính, Đã bỏ (định nghĩa ở M08) và Bị lật (do khiếu nại được chấp nhận). |
| Trạng thái kiểm duyệt, trạng thái đăng của bài | Bình thường, Bị ẩn; Chờ duyệt, Bị từ chối, Đã đăng (định nghĩa ở M03). |

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
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp; draft không có mục riêng cho khiếu nại |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-202, QA-383, ISS-323, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Tài khoản BANNED đăng nhập vào màn hình bị khóa, chỉ khiếu nại được lệnh ban; khiếu nại ban được chấp nhận đưa tài khoản về ACTIVE. |
| M03 Post & Content | Bài bị Mod ẩn ("gỡ") hoặc bị AI tự từ chối được khiếu nại; chấp nhận thì bài bị gỡ hiện lại, bài bị AI từ chối được đăng không quét lại; bài đã xóa, tự ẩn xem được trong khiếu nại. |
| M04 Comment | Bình luận không có khiếu nại riêng và không hiện lại khi cảnh cáo, ban liên quan bị lật; xem lại bình luận từ khiếu nại. |
| M07 Notification | Gửi thông báo kết luận khiếu nại; khiếu nại ban gửi cả email. |
| M08 Moderation | Cảnh cáo, ban, bài bị gỡ là đối tượng khiếu nại; nút Khiếu nại trong thông báo xử lý; lật cảnh cáo, ban; nhật ký kiểm duyệt cho người xét. |
| M10 Admin Panel | Xử lý khiếu nại dùng chung Mod, Admin; Mod bị ban mất vai trò Mod và không được trả lại khi lật ban; giáng cấp không khiếu nại. |
| M11 Group | Thao tác kiểm duyệt cấp nhóm không khiếu nại được. |
| M12 Gamification | Hoàn điểm khi khiếu nại bài bị gỡ thành công. |
| M13 AI Layer | Nhật ký quyết định AI làm căn cứ khi xét khiếu nại bài bị AI tự từ chối. |
| M15 Analytics & Stats | Thống kê khiếu nại theo loại và kết quả. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Không có thao tác nào; đường dẫn khiếu nại trong email ban đưa tới đăng nhập trước. |
| User | Người dùng đã đăng nhập, kể cả tài khoản BANNED (chỉ khiếu nại được lệnh ban). Gửi khiếu nại về cảnh cáo, ban, bài viết của mình bị gỡ hoặc bị AI tự từ chối; xem khiếu nại của mình. |
| Mod | Có quyền của User. Xem hàng chờ khiếu nại, nhận xử lý, xem chi tiết và kết luận khiếu nại, trừ khiếu nại về thao tác của chính mình và khiếu nại do một Mod gửi (không thấy trong hàng chờ). |
| Admin | Có các quyền của Mod; xét được mọi khiếu nại, kể cả về xử lý do chính mình ra; là người duy nhất xét khiếu nại do Mod gửi. Admin không bị báo cáo, cảnh cáo, ban và nội dung của Admin không bị AI quét, nên Admin không có khiếu nại. |
| Người khiếu nại | Vai trò theo ngữ cảnh: người dùng bị xử lý (người bị cảnh cáo, bị ban, tác giả bài bị gỡ hoặc bị AI tự từ chối) đã gửi khiếu nại. |
| Người ra xử lý | Vai trò theo ngữ cảnh: Mod, Admin hoặc AI đã đưa ra xử lý bị khiếu nại. Mod là người ra xử lý thì không xét khiếu nại đó. |
| Hệ thống | Tự nhả khiếu nại đã nhận mà không thao tác, đảo ngược xử lý khi khiếu nại được chấp nhận. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Gửi khiếu nại cảnh cáo | ✗ | ✓ (của mình) | ✓ (của mình) | — | FR-M09-01.01, FR-M09-01.08, FR-M09-01.09 |
| Gửi khiếu nại ban | ✗ | ✓ (của mình) | — | — | FR-M09-01.04, FR-M09-01.08, FR-M09-01.09 |
| Gửi khiếu nại bài viết bị gỡ hoặc bị AI tự từ chối | ✗ | ✓ (của mình) | ✓ (của mình) | — | FR-M09-01.03, FR-M09-01.08, FR-M09-01.09, FR-M09-01.20 |
| Gửi khiếu nại cảnh cáo, bài viết trong lúc tài khoản bị ban | ✗ | ✗ | — | — | FR-M09-01.18 |
| Khiếu nại riêng cảnh cáo AI ra cùng lần từ chối một bài | ✗ | ✗ | ✗ | — | FR-M09-01.21 |
| Gửi lại khiếu nại cho xử lý đã khiếu nại | ✗ | ✗ | ✗ | ✗ | FR-M09-01.14 |
| Khiếu nại một xử lý đã bị lật | ✗ | ✗ | ✗ | — | FR-M09-01.23 |
| Khiếu nại bình luận bị ẩn, nhóm bị ẩn hoặc khóa, thao tác kiểm duyệt cấp nhóm, việc giáng cấp Mod | ✗ | ✗ | ✗ | ✗ | FR-M09-01.15 |
| Rút, sửa khiếu nại đã gửi | ✗ | ✗ | ✗ | — | FR-M09-01.22 |
| Xem khiếu nại của mình, kết luận và lý do | ✗ | ✓ (của mình) | ✓ (của mình) | — | FR-M09-02.01, FR-M09-02.02, FR-M09-02.05 |
| Xem hàng chờ khiếu nại | ✗ | ✗ | ✓ | ✓ | FR-M09-03.01, FR-M09-03.02, FR-M09-03.07 |
| Thấy, nhận, xét khiếu nại về thao tác của chính mình | ✗ | ✗ | ✗ | ✓ | FR-M09-03.04, FR-M09-03.05, FR-M09-04.03, FR-M09-07.07, FR-M09-07.10 |
| Thấy, nhận, xét khiếu nại do một Mod gửi | ✗ | ✗ | ✗ | ✓ | FR-M09-03.08, FR-M09-04.08, FR-M09-06.08, FR-M09-07.12 |
| Xét khiếu nại về xử lý do Admin ra với người dùng không phải Mod | ✗ | ✗ | ✓ | ✓ | FR-M09-03.01, FR-M09-03.04 |
| Nhận xử lý khiếu nại | ✗ | ✗ | ✓ | ✓ | FR-M09-04.01, FR-M09-04.04 |
| Xem chi tiết khiếu nại: xử lý bị khiếu nại (kể cả thao tác của Mod khác), nội dung liên quan đã xóa, tự ẩn, nhật ký AI | ✗ | ✗ | ✓ | ✓ | FR-M09-06.01, FR-M09-06.03, FR-M09-06.04, FR-M09-06.05, FR-M09-06.06 |
| Chấp nhận hoặc từ chối khiếu nại | ✗ | ✗ | ✓ | ✓ | FR-M09-07.01, FR-M09-07.02, FR-M09-07.09, FR-M09-07.11 |

<!-- Ô nói thẳng: Guest ✗ ở hàng 1–3 (DEC-085, QA-152: tài khoản bị ban vẫn đăng nhập; đường dẫn đi qua đăng nhập);
     User ✓ hàng 1–3 (DEC-084, DEC-085, DEC-086, DEC-078, DEC-115, DEC-198); hàng 4 (DEC-197); hàng 5 (DEC-198, DEC-199);
     hàng 6 (DEC-087); hàng 7 (DEC-202); hàng 8 (DEC-115, DEC-180, DEC-194, DEC-109, DEC-091); hàng 9 (DEC-201); cột Mod,
     Admin hàng 11, 15–17 (DEC-090 "Shared with Mod: ... appeal handling", QA-020, DEC-081, DEC-133, DEC-179, DEC-184,
     DEC-185); hàng 12 (DEC-088, QA-021); hàng 13 (DEC-195); hàng 14 (QA-020, DEC-195: phần còn lại giữ nguồn).
     Ô suy ra: cột Guest các hàng 10–17 (mọi thao tác cần đăng nhập); cột User hàng 11–17 (chỉ Mod, Admin xét khiếu nại);
     hàng 1, 3 cột Mod (Mod bị Admin cảnh cáo, bị gỡ bài được, DEC-189, DEC-195); hàng 10 (chủ nội dung xem lại từ khiếu nại
     của mình, DEC-179, DEC-184).
     "—": Admin không bị báo cáo, cảnh cáo, ban, nội dung không bị quét nên không có khiếu nại (DEC-189, DEC-195); Mod bị ban
     thì mất vai trò Mod (QA-013, DEC-189) nên gửi khiếu nại ban với tư cách User. -->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M09-01 | Gửi khiếu nại | User | Người dùng chọn nút Khiếu nại trong thông báo về một xử lý, nút "Gửi khiếu nại" trên màn hình tài khoản bị khóa, hoặc đường dẫn khiếu nại trong email ban |
| FR-M09-02 | Xem khiếu nại của mình | User | Người khiếu nại mở khiếu nại của mình, hoặc mở thông báo kết luận khiếu nại |
| FR-M09-03 | Xem hàng chờ khiếu nại | Mod, Admin | Mod hoặc Admin mở hàng chờ khiếu nại |
| FR-M09-04 | Nhận và nhả khiếu nại | Mod, Admin; Hệ thống | Mod hoặc Admin chọn "Nhận xử lý" một khiếu nại; hoặc khiếu nại đã nhận không có thao tác trong 30 phút |
| FR-M09-05 | (Đã bỏ ở phiên bản 0.1 — chuyển lên Admin là quy tắc lọc ở FR-M09-03.09) | — | — |
| FR-M09-06 | Xem chi tiết khiếu nại | Mod, Admin | Mod hoặc Admin mở một khiếu nại trong hàng chờ |
| FR-M09-07 | Kết luận khiếu nại | Mod, Admin | Mod hoặc Admin đang giữ khiếu nại chọn chấp nhận hoặc từ chối |
| FR-M09-08 | Đảo ngược xử lý khi khiếu nại được chấp nhận | Hệ thống | Một khiếu nại được chấp nhận |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Must** (bảng MoSCoW Summary của module-registry: Must gồm M01–M10, M13;
cột MoSCoW ở dòng M09 của bảng Module List bị lệch nên không dùng). Không có yêu cầu ngoại lệ về ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M09-01 Gửi khiếu nại

**Yêu cầu cấp trên:** Hệ thống phải cho phép người bị xử lý gửi một khiếu nại về một cảnh cáo, một ban, một bài viết bị gỡ, hoặc một bài viết bị AI tự từ chối cùng cảnh cáo AI đi kèm, kèm lời giải thích và bằng chứng, trong hạn khiếu nại.

**Lý do:** Người bị xử lý sai cần có đường phản đối, kể cả với cảnh cáo AI tự ra khi AI sai. Bài bị AI tự từ chối được khiếu nại gộp với cảnh cáo đi kèm, để khi người xét xác nhận AI chấm sai thì bài cũng được đăng. Hạn khiếu nại ban vĩnh viễn giới hạn 90 ngày vì vụ cũ nhiều năm sau mất ngữ cảnh, Mod đã thay đổi và không còn cách giải quyết gọn. Chỉ khiếu nại bài, không khiếu nại bình luận, vì bài là tài sản giá trị hơn và số bình luận quá lớn để duy trì một hàng chờ khiếu nại.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M09-01.01 | Khi người dùng gửi một khiếu nại hợp lệ, hệ thống phải lưu khiếu nại với người khiếu nại, loại khiếu nại, xử lý bị khiếu nại, lời giải thích, bằng chứng, thời điểm gửi và trạng thái Chờ xét (BR-M09-01). |
| FR-M09-01.02 | Khi lưu một khiếu nại, hệ thống phải đưa khiếu nại vào hàng chờ khiếu nại, tách khỏi hàng chờ báo cáo (BR-M09-09). |
| FR-M09-01.03 | Khi lưu một khiếu nại, hệ thống phải gắn loại khiếu nại theo xử lý bị khiếu nại: ban, cảnh cáo, hoặc bài viết (bài bị gỡ, bài bị AI tự từ chối) (BR-M09-09). |
| FR-M09-01.04 | Khi tài khoản BANNED chọn "Gửi khiếu nại" trên màn hình tài khoản bị khóa, hệ thống phải mở trang gửi khiếu nại cho ban đang hiệu lực (BR-M09-07). |
| FR-M09-01.05 | Khi người chưa đăng nhập mở đường dẫn khiếu nại trong email ban, hệ thống phải đưa người đó qua đăng nhập rồi tới trang gửi khiếu nại (BR-M09-08). |
| FR-M09-01.06 | Khi người bị xử lý chọn nút Khiếu nại trong thông báo về một cảnh cáo, một ban, một bài bị gỡ hoặc một bài bị AI tự từ chối, bất kể người ra xử lý là AI, Mod hay Admin, hệ thống phải mở trang gửi khiếu nại cho đúng xử lý đó (BR-M09-28). |
| FR-M09-01.07 | Hệ thống phải cho khiếu nại cảnh cáo do AI tự ra như cảnh cáo do Mod, Admin ra (BR-M09-01). |
| FR-M09-01.08 | Nếu người gửi chưa đăng nhập, hệ thống phải từ chối khiếu nại. |
| FR-M09-01.09 | Nếu người gửi khác người bị xử lý (người bị cảnh cáo, người bị ban hoặc tác giả của bài), hệ thống phải từ chối khiếu nại. |
| FR-M09-01.10 | Nếu lời giải thích trống, hệ thống phải từ chối gửi khiếu nại (BR-M09-03). |
| FR-M09-01.11 | Nếu người khiếu nại đính kèm ảnh bằng chứng thứ tư, hệ thống phải từ chối ảnh đó (BR-M09-03). |
| FR-M09-01.12 | Nếu một ảnh bằng chứng lớn hơn 5MB hoặc có định dạng khác JPEG, PNG, WebP, hệ thống phải từ chối ảnh đó (BR-M09-03). |
| FR-M09-01.13 | Nếu đã hết hạn khiếu nại của xử lý (BR-M09-04, BR-M09-05), hệ thống phải từ chối khiếu nại. |
| FR-M09-01.14 | Nếu xử lý đã có một khiếu nại, đang chờ xét hoặc đã kết luận, hệ thống phải từ chối khiếu nại mới cho xử lý đó (BR-M09-06). |
| FR-M09-01.15 | Nếu người dùng khiếu nại một bình luận bị ẩn, một nhóm bị ẩn hoặc bị khóa, một thao tác kiểm duyệt cấp nhóm hoặc việc giáng cấp Mod, hệ thống phải từ chối khiếu nại (BR-M09-02). |
| FR-M09-01.16 | Hệ thống phải không xóa khiếu nại đã lưu, kể cả khi tài khoản người khiếu nại bị xóa (BR-M09-22). |
| FR-M09-01.17 | Hệ thống phải không cho đổi hạn khiếu nại và giới hạn bằng chứng qua giao diện (BR-M09-23). |
| FR-M09-01.18 | Trong khi tài khoản BANNED, nếu người dùng gửi khiếu nại một xử lý khác lệnh ban đang hiệu lực, hệ thống phải từ chối khiếu nại (BR-M09-07). |
| FR-M09-01.19 | Khi bài bị AI tự từ chối kèm một cảnh cáo AI, hệ thống phải gửi cho tác giả một thông báo nêu bài bị từ chối (chưa được đăng) và cảnh cáo, kèm một nút Khiếu nại cho cả hai (BR-M09-24). |
| FR-M09-01.20 | Khi tác giả khiếu nại một bài bị AI tự từ chối, hệ thống phải gộp bài và cảnh cáo AI ra cùng lần từ chối vào một khiếu nại (BR-M09-24). |
| FR-M09-01.21 | Nếu người dùng gửi khiếu nại riêng cho cảnh cáo AI ra cùng lần từ chối một bài, hệ thống phải từ chối khiếu nại riêng đó (BR-M09-24). |
| FR-M09-01.22 | Hệ thống phải không cho người khiếu nại rút hoặc sửa khiếu nại đã gửi (BR-M09-27). |
| FR-M09-01.23 | Nếu xử lý bị khiếu nại đã bị lật, hệ thống phải từ chối khiếu nại mới cho xử lý đó (BR-M09-29). |

### 5.2 FR-M09-02 Xem khiếu nại của mình

**Yêu cầu cấp trên:** Hệ thống phải cho phép người khiếu nại xem khiếu nại của mình cùng kết luận và lý do, và xem lại ở chế độ chỉ đọc nội dung của mình đã bị xử lý.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M09-02.01 | Khi người khiếu nại mở khiếu nại của mình, hệ thống phải hiển thị xử lý bị khiếu nại, lời giải thích, bằng chứng đã gửi và trạng thái của khiếu nại. |
| FR-M09-02.02 | Khi khiếu nại của người dùng đã kết luận, hệ thống phải hiển thị kết luận Chấp nhận hoặc Từ chối cùng lý do kết luận cho người khiếu nại (BR-M09-27). |
| FR-M09-02.03 | Khi người khiếu nại mở nội dung bị xử lý từ khiếu nại của mình, hệ thống phải hiển thị nội dung đó ở chế độ chỉ đọc, kể cả khi nội dung đã xóa hoặc đã xóa hẳn (BR-M09-21). |
| FR-M09-02.04 | Hệ thống phải không hiển thị cho người khiếu nại danh tính người báo cáo, lý do người báo cáo chọn, mô tả và bằng chứng của báo cáo (BR-M09-21). |
| FR-M09-02.05 | Nếu người dùng mở khiếu nại của người khác, hệ thống phải từ chối. |

### 5.3 FR-M09-03 Xem hàng chờ khiếu nại

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin xem các khiếu nại đang chờ xét trong một danh sách tách khỏi hàng chờ báo cáo, xếp theo loại và thời điểm gửi, lọc được theo loại.

**Lý do:** Hàng chờ khiếu nại tách khỏi hàng chờ báo cáo vì cần quy tắc phân công khác: Mod không xét khiếu nại về thao tác của chính mình.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M09-03.01 | Khi Mod hoặc Admin mở hàng chờ khiếu nại, hệ thống phải hiển thị các khiếu nại đang Chờ xét theo thứ tự khiếu nại ban, rồi khiếu nại cảnh cáo, rồi khiếu nại bài viết; cùng loại thì khiếu nại gửi trước đứng trước (BR-M09-10). |
| FR-M09-03.02 | Khi Mod hoặc Admin lọc hàng chờ khiếu nại theo một loại, hệ thống phải chỉ hiển thị khiếu nại của loại đó, khiếu nại gửi trước đứng trước (BR-M09-09). |
| FR-M09-03.03 | Hệ thống phải giữ hàng chờ khiếu nại tách khỏi hàng chờ báo cáo (BR-M09-09). |
| FR-M09-03.04 | Hệ thống phải không hiển thị trong hàng chờ của một Mod các khiếu nại về xử lý do chính Mod đó ra (BR-M09-12). |
| FR-M09-03.05 | Hệ thống phải hiển thị cho Admin mọi khiếu nại đang Chờ xét, kể cả khiếu nại về xử lý do chính Admin đó ra (BR-M09-12). |
| FR-M09-03.06 | Hệ thống phải hiển thị khiếu nại về cảnh cáo do AI tự ra và về bài bị AI tự từ chối trong hàng chờ của mọi Mod, trừ khiếu nại do một Mod gửi (BR-M09-14). |
| FR-M09-03.07 | Nếu người không có vai trò Mod hoặc Admin mở hàng chờ khiếu nại, hệ thống phải từ chối. |
| FR-M09-03.08 | Hệ thống phải không hiển thị cho Mod các khiếu nại do một Mod gửi, kể cả khi người gửi đã mất vai trò Mod vì bị ban (BR-M09-12). |
| FR-M09-03.09 | Khi không còn Mod nào khác người ra xử lý, hệ thống phải chỉ hiển thị khiếu nại về xử lý đó cho Admin, không có bước chuyển, đánh dấu hay thông báo riêng (BR-M09-13). |

### 5.4 FR-M09-04 Nhận và nhả khiếu nại

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin nhận xử lý một khiếu nại để xét, và tự nhả khiếu nại khi người giữ không thao tác trong 30 phút.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M09-04.01 | Khi Mod hoặc Admin chọn "Nhận xử lý" một khiếu nại Chờ xét chưa ai giữ, hệ thống phải ghi người đó là người đang giữ khiếu nại (BR-M09-11). |
| FR-M09-04.02 | Nếu khiếu nại đang được người khác giữ, hệ thống phải từ chối nhận xử lý (BR-M09-11). |
| FR-M09-04.03 | Nếu Mod chọn nhận xử lý một khiếu nại về xử lý do chính mình ra, hệ thống phải từ chối (BR-M09-12). |
| FR-M09-04.04 | Nếu người không có vai trò Mod hoặc Admin chọn nhận xử lý, hệ thống phải từ chối. |
| FR-M09-04.05 | Nếu khiếu nại đã kết luận, hệ thống phải từ chối nhận xử lý. |
| FR-M09-04.06 | Khi người giữ không có thao tác nào trên khiếu nại trong 30 phút, hệ thống phải nhả khiếu nại về Chờ xét chưa ai giữ (BR-M09-11). |
| FR-M09-04.07 | Khi người giữ mở xem khiếu nại, hệ thống phải tính lại 30 phút từ lúc mở xem (BR-M09-11). |
| FR-M09-04.08 | Nếu Mod chọn nhận xử lý một khiếu nại do một Mod gửi, hệ thống phải từ chối (BR-M09-12). |

### 5.5 FR-M09-05 (Đã bỏ ở phiên bản 0.1)

**Yêu cầu cấp trên:** (Đã bỏ ở phiên bản 0.1 — DEC-196: "chuyển lên Admin" là quy tắc lọc người thấy khiếu nại, không phải một chức năng; xem FR-M09-03.09, BR-M09-13.)

**Lý do:** Đã bỏ.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M09-05.01 | (Đã bỏ ở phiên bản 0.1 — thay bằng FR-M09-03.09.) |

### 5.6 FR-M09-06 Xem chi tiết khiếu nại

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin xem đầy đủ một khiếu nại cùng xử lý bị khiếu nại và căn cứ của xử lý đó.

**Lý do:** Mod, Admin cần xem lại được vì sao một xử lý được đưa ra, kể cả "tại sao AI quyết định vậy" khi người dùng khiếu nại bị AI xử lý oan.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M09-06.01 | Khi Mod hoặc Admin mở một khiếu nại, hệ thống phải hiển thị người khiếu nại, loại khiếu nại, lời giải thích, bằng chứng và thời điểm gửi (BR-M09-15). |
| FR-M09-06.02 | Khi Mod hoặc Admin mở một khiếu nại, hệ thống phải hiển thị chi tiết xử lý bị khiếu nại gồm người ra xử lý, loại xử lý, lý do và thời điểm (BR-M09-15). |
| FR-M09-06.03 | Khi Mod xét khiếu nại về xử lý do Mod khác ra, hệ thống phải hiển thị chi tiết thao tác đó cho Mod đang xét (BR-M09-15). |
| FR-M09-06.04 | Khi Mod hoặc Admin mở một khiếu nại có nội dung liên quan đã xóa, đã xóa hẳn hoặc tự ẩn, hệ thống phải hiển thị nội dung đó trong khiếu nại (BR-M09-15). |
| FR-M09-06.05 | Khi Mod hoặc Admin mở khiếu nại về bài bị AI tự từ chối, hệ thống phải hiển thị nhật ký quyết định AI của bài đó (BR-M09-15). |
| FR-M09-06.06 | Nếu người không có vai trò Mod hoặc Admin mở chi tiết khiếu nại của người khác, hệ thống phải từ chối. |
| FR-M09-06.07 | Nếu Mod mở chi tiết khiếu nại về xử lý do chính mình ra, hệ thống phải từ chối (BR-M09-12). |
| FR-M09-06.08 | Nếu Mod mở chi tiết một khiếu nại do một Mod gửi, hệ thống phải từ chối (BR-M09-12). |

### 5.7 FR-M09-07 Kết luận khiếu nại

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod, Admin đang giữ một khiếu nại kết luận Chấp nhận hoặc Từ chối kèm lý do, và báo kết luận cho người khiếu nại.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M09-07.01 | Khi người đang giữ chọn Chấp nhận kèm lý do kết luận, hệ thống phải chuyển khiếu nại sang Đã kết luận với kết luận Chấp nhận, ghi lý do, người kết luận và thời điểm kết luận. |
| FR-M09-07.02 | Khi người đang giữ chọn Từ chối kèm lý do kết luận, hệ thống phải chuyển khiếu nại sang Đã kết luận với kết luận Từ chối, ghi lý do, người kết luận và thời điểm kết luận. |
| FR-M09-07.03 | Khi khiếu nại bị từ chối, hệ thống phải giữ nguyên xử lý bị khiếu nại (BR-M09-19). |
| FR-M09-07.04 | Khi một khiếu nại ban được kết luận, hệ thống phải gửi kết luận kèm lý do cho người khiếu nại trong ứng dụng và qua email (BR-M09-20). |
| FR-M09-07.05 | Khi một khiếu nại cảnh cáo hoặc khiếu nại bài viết được kết luận, hệ thống phải gửi kết luận kèm lý do cho người khiếu nại chỉ trong ứng dụng (BR-M09-20). |
| FR-M09-07.06 | Nếu người kết luận khác người đang giữ khiếu nại, hệ thống phải từ chối kết luận (BR-M09-11). |
| FR-M09-07.07 | Nếu Mod kết luận khiếu nại về xử lý do chính mình ra, hệ thống phải từ chối (BR-M09-12). |
| FR-M09-07.08 | Nếu khiếu nại đã kết luận, hệ thống phải từ chối kết luận lại (BR-M09-06). |
| FR-M09-07.09 | Hệ thống phải chỉ nhận kết luận khiếu nại từ Mod hoặc Admin, không để AI kết luận khiếu nại (BR-M09-12). |
| FR-M09-07.10 | Hệ thống phải cho Admin kết luận mọi khiếu nại, kể cả khiếu nại về xử lý do chính Admin đó ra (BR-M09-12). |
| FR-M09-07.11 | Nếu người kết luận không nhập lý do kết luận, hệ thống phải từ chối kết luận (BR-M09-27). |
| FR-M09-07.12 | Nếu Mod kết luận một khiếu nại do một Mod gửi, hệ thống phải từ chối (BR-M09-12). |

### 5.8 FR-M09-08 Đảo ngược xử lý khi khiếu nại được chấp nhận

**Yêu cầu cấp trên:** Khi một khiếu nại được chấp nhận, hệ thống phải lật xử lý bị khiếu nại cùng hệ quả của nó trên tài khoản, mức cảnh cáo, bài viết và điểm.

**Lý do:** Số lần cảnh cáo được giảm như thể cảnh cáo chưa từng có, để cách tính leo thang LIGHT/MEDIUM/HEAVY luôn đúng; bản ghi ban được giữ lại để kiểm tra về sau.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M09-08.01 | Khi khiếu nại ban được chấp nhận, hệ thống phải chuyển ban sang Bị lật và giữ bản ghi ban, kể cả khi ban đã hết hạn hoặc đã được gỡ (BR-M09-16, BR-M09-25). |
| FR-M09-08.02 | Khi khiếu nại một ban đang hiệu lực được chấp nhận, hệ thống phải chuyển tài khoản về ACTIVE ngay lúc đó (BR-M09-16). |
| FR-M09-08.03 | Hệ thống phải không tính ban Bị lật vào số lần đã bị ban (BR-M09-16). |
| FR-M09-08.04 | Khi khiếu nại cảnh cáo được chấp nhận, hệ thống phải chuyển cảnh cáo sang Bị lật và giữ bản ghi cảnh cáo (BR-M09-17). |
| FR-M09-08.05 | Khi khiếu nại cảnh cáo được chấp nhận, hệ thống phải giảm số lần cảnh cáo hiện tại của người khiếu nại 1 lần, không xuống dưới 0, và tính lại mức cảnh cáo theo số lần còn lại (BR-M09-17, BR-M09-25). |
| FR-M09-08.06 | Khi mức cảnh cáo được tính lại do lật cảnh cáo, hệ thống phải áp ngay hạn chế của mức mới (BR-M09-17). |
| FR-M09-08.07 | Khi lật cảnh cáo, hệ thống phải giữ nguyên thời điểm kết thúc thời gian thử thách hiện tại (BR-M09-17). |
| FR-M09-08.08 | Khi khiếu nại bài bị gỡ được chấp nhận, hệ thống phải chuyển bài về trạng thái kiểm duyệt Bình thường (BR-M09-18). |
| FR-M09-08.09 | Khi khiếu nại bài bị gỡ được chấp nhận, hệ thống phải hoàn điểm đã trừ vì lần gỡ đó (BR-M09-18). |
| FR-M09-08.10 | Khi khiếu nại bài bị gỡ được chấp nhận, hệ thống phải lật cảnh cáo, ban ra cùng lần gỡ đó chưa bị lật theo FR-M09-08.01 đến FR-M09-08.07 (BR-M09-18, BR-M09-29). |
| FR-M09-08.11 | Khi khiếu nại ban của một người từng có vai trò Mod được chấp nhận, hệ thống phải giữ vai trò User cho tài khoản đó, không trả lại vai trò Mod (BR-M09-16). |
| FR-M09-08.12 | Khi khiếu nại gộp về một bài bị AI tự từ chối được chấp nhận, hệ thống phải chuyển bài sang Đã đăng ngay mà không quét lại (BR-M09-24). |
| FR-M09-08.13 | Khi khiếu nại gộp về một bài bị AI tự từ chối được chấp nhận, hệ thống phải lật cảnh cáo AI ra cùng lần từ chối theo FR-M09-08.04 đến FR-M09-08.07 (BR-M09-24). |
| FR-M09-08.14 | Nếu tác giả đã gửi lại bài trước khi khiếu nại gộp được kết luận, hệ thống phải chỉ lật cảnh cáo AI khi chấp nhận, giữ nguyên trạng thái hiện tại của bài (BR-M09-24). |
| FR-M09-08.15 | Khi lật một cảnh cáo hay một ban ra cùng lần ẩn một bình luận, hệ thống phải giữ bình luận đó ở trạng thái Bị ẩn (BR-M09-26). |
| FR-M09-08.16 | Nếu cảnh cáo hay ban ra cùng lần gỡ bài đã có khiếu nại riêng bị Từ chối, khi chấp nhận khiếu nại bài hệ thống phải không lật cảnh cáo hay ban đó (BR-M09-29). |
| FR-M09-08.17 | Khi chấp nhận khiếu nại của một xử lý đã bị lật, hệ thống phải giữ nguyên xử lý đó, không đổi gì thêm (BR-M09-29). |

### 5.9 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M09-01 | Sự kiện | Xử lý khiếu nại được: một cảnh cáo (do AI, Mod hoặc Admin ra); một ban tạm thời hoặc vĩnh viễn; một bài viết bị Mod, Admin gỡ vì vi phạm (trạng thái kiểm duyệt Bị ẩn); một bài viết bị AI tự từ chối, khiếu nại gộp với cảnh cáo AI ra cùng lần (BR-M09-24). Admin không bị báo cáo, cảnh cáo, ban và nội dung của Admin không bị AI quét, nên Admin không có khiếu nại. | — |
| BR-M09-02 | Ràng buộc | Không khiếu nại được: bình luận bị ẩn (do Mod, Admin hay AI); nhóm bị ẩn hoặc bị khóa; thao tác kiểm duyệt cấp nhóm của Group Mod, Owner; việc giáng cấp Mod. | — |
| BR-M09-03 | Ràng buộc | Khiếu nại gồm lời giải thích (bắt buộc) và bằng chứng (tùy chọn): tối đa 3 ảnh, mỗi ảnh tối đa 5MB, định dạng JPEG, PNG hoặc WebP — cùng giới hạn với bằng chứng của báo cáo. | Lời giải thích trống: từ chối. 3 ảnh 4MB: nhận. Ảnh thứ 4: từ chối. Ảnh đúng 5MB: nhận; ảnh 5,1MB: từ chối. Tệp PDF: từ chối. |
| BR-M09-04 | Tính toán | Hạn khiếu nại tính từ lúc có xử lý: cảnh cáo — 7, 10 hoặc 15 ngày theo mức mà chính cảnh cáo đó đưa người dùng tới (LIGHT, MEDIUM, HEAVY), không đổi khi có cảnh cáo sau hay khi giảm mức; ban tạm thời — bằng thời hạn ban (30 hoặc 90 ngày); ban vĩnh viễn — 90 ngày; bài bị gỡ — 30 ngày; bài bị AI tự từ chối — bằng hạn của cảnh cáo AI đi kèm, không có cảnh cáo đi kèm thì 3 ngày. "N ngày" là đủ N × 24 giờ, theo giờ Việt Nam. | Ban 30 ngày lúc 01/10 09:00: gửi được tới trước 31/10 09:00 (31/10 08:59 nhận; 31/10 09:00 từ chối). Ban vĩnh viễn lúc 01/10 09:00: tới trước 30/12 09:00. Bài bị gỡ lúc 05/10 14:00: tới trước 04/11 14:00. C1 lúc 01/10 09:00 (lần 1, LIGHT): tới trước 08/10 09:00; C2 lúc 05/10 09:00 (lần 2): tới trước 12/10 09:00, hạn của C1 vẫn là 08/10 09:00. Bài bị AI từ chối lúc 01/10 10:00 kèm cảnh cáo lần 3 (MEDIUM): tới trước 11/10 10:00; không kèm cảnh cáo (tác giả đang HEAVY): tới trước 04/10 10:00. |
| BR-M09-05 | Suy diễn | Quá hạn khiếu nại thì không gửi được khiếu nại cho xử lý đó; với ban vĩnh viễn, quyền khiếu nại mất hẳn. Nút "Gửi khiếu nại" trên màn hình tài khoản bị khóa chỉ hiện khi ban còn trong hạn khiếu nại. | Ban vĩnh viễn lúc 01/10 09:00: ngày 30/12 09:00 trở đi màn hình khóa chỉ còn lý do ban và nút OK. |
| BR-M09-06 | Ràng buộc | Mỗi xử lý chỉ được khiếu nại một lần. Khiếu nại bị từ chối là cuối cùng: không gửi lại cho cùng xử lý. Khiếu nại gộp tính là khiếu nại của cả bài và cảnh cáo AI đi kèm. | Lan khiếu nại cảnh cáo C1, bị từ chối: không gửi lại cho C1. Lan bị cảnh cáo C2 sau đó: khiếu nại C2 được. |
| BR-M09-07 | Ràng buộc | Tài khoản BANNED đăng nhập bình thường nhưng chỉ thấy màn hình tài khoản bị khóa và chỉ khiếu nại được chính lệnh ban đang hiệu lực (ngoài ra chỉ đặt lại mật khẩu ở M01). Cảnh cáo, bài bị gỡ chỉ khiếu nại được khi tài khoản ACTIVE và còn hạn. | An bị ban 30 ngày lúc 01/10 09:00, cùng vụ bài P bị gỡ: trong lúc bị ban chỉ khiếu nại được lệnh ban. Ban được lật ngày 05/10: An khiếu nại P được tới trước 31/10 09:00. |
| BR-M09-08 | Sự kiện | Email báo ban có đường dẫn tới trang khiếu nại; người chưa đăng nhập mở đường dẫn thì được đưa qua đăng nhập rồi tới trang khiếu nại. | — |
| BR-M09-09 | Ràng buộc | Hàng chờ khiếu nại tách khỏi hàng chờ báo cáo và là một danh sách chung cho ba loại: ban, cảnh cáo, bài viết. Mod, Admin lọc được theo loại. | — |
| BR-M09-10 | Ràng buộc | Thứ tự trong hàng chờ khiếu nại: khiếu nại ban, rồi khiếu nại cảnh cáo, rồi khiếu nại bài viết; cùng loại thì khiếu nại gửi trước đứng trước. | K4 (bài, gửi 06:00), K1 (bài, 07:00), K2 (cảnh cáo, 08:00), K3 (ban, 09:00): thứ tự K3, K2, K4, K1. Lọc "bài viết": K4, K1. |
| BR-M09-11 | Ràng buộc | Mỗi khiếu nại tại một thời điểm chỉ có một Mod hoặc Admin giữ; người khác không xét được khiếu nại đang được giữ. Khiếu nại đang được giữ tự được nhả khi người giữ không có thao tác nào trên khiếu nại trong 30 phút (cùng cơ chế với hàng chờ báo cáo). Thao tác gồm: mở xem khiếu nại, kết luận. | Nhận lúc 10:00, mở xem bằng chứng lúc 10:20, không làm gì thêm: tự nhả lúc 10:50; lúc 10:49 vẫn đang giữ. |
| BR-M09-12 | Ràng buộc | Mod không thấy, không nhận, không xét khiếu nại về xử lý do chính mình ra, và khiếu nại do một Mod gửi. Khiếu nại do Mod gửi chỉ Admin xét; vai trò tính theo lúc bị xử lý. Admin xét được mọi khiếu nại, kể cả về xử lý do chính Admin ra. AI không xét khiếu nại. | Mod A cảnh cáo Lan; Lan khiếu nại: Mod A không thấy; Mod B và Admin thấy. Admin Hà cảnh cáo Mod Minh; Minh khiếu nại: chỉ Admin thấy. Admin Hà ban Mod Minh (Minh mất vai trò Mod); Minh khiếu nại: chỉ Admin thấy. |
| BR-M09-13 | Suy diễn | Không có bước chuyển khiếu nại lên Admin riêng: khiếu nại về xử lý của Mod X hiện với các Mod khác X và Admin; khi không còn Mod nào khác X, chỉ Admin thấy khiếu nại. | Hệ thống chỉ có Mod Lan; Lan cảnh cáo An; An khiếu nại: chỉ Admin thấy, không có thông báo hay dấu "đã chuyển". |
| BR-M09-14 | Suy diễn | Cảnh cáo do AI tự ra và bài bị AI tự từ chối không có Mod là người ra xử lý, nên mọi Mod đều xét được khiếu nại về chúng, trừ khi người gửi là Mod (BR-M09-12). | — |
| BR-M09-15 | Sự kiện | Khi xét khiếu nại, người xét thấy: lời giải thích, bằng chứng; chi tiết xử lý bị khiếu nại (kể cả khi do Mod khác ra); nội dung liên quan, kể cả đã xóa, đã xóa hẳn, tự ẩn; với bài bị AI tự từ chối, nhật ký quyết định AI. Ngoài ngữ cảnh khiếu nại (và báo cáo ở M08), Mod, Admin không xem được các nội dung đã xóa, tự ẩn đó. | — |
| BR-M09-16 | Sự kiện | Khiếu nại ban được chấp nhận: ban giữ bản ghi, đánh dấu bị lật, thôi hiệu lực, không tính vào số lần đã bị ban; ban còn hiệu lực thì tài khoản về ACTIVE ngay. Người bị ban từng là Mod về ACTIVE với vai trò User; vai trò Mod không được trả lại, Admin muốn thì gửi đề xuất làm Mod (M10). | Lan bị ban lần đầu 30 ngày, khiếu nại được chấp nhận: ACTIVE ngay; lần ban sau của Lan vẫn là 30 ngày. Minh (Mod) bị ban, khiếu nại được chấp nhận: ACTIVE, vai trò User. |
| BR-M09-17 | Sự kiện | Khiếu nại cảnh cáo được chấp nhận: cảnh cáo giữ bản ghi, đánh dấu bị lật; số lần cảnh cáo hiện tại giảm 1 (không xuống dưới 0), mức cảnh cáo tính lại theo số lần còn lại và hạn chế theo mức mới áp dụng ngay; thời điểm kết thúc thời gian thử thách hiện tại không đổi. | Lan 3 lần (MEDIUM, không tạo bài), hết thử thách 20/10 09:00; lật 1 lần → 2 lần, LIGHT: tạo bài lại được ngay; thử thách vẫn hết 20/10 09:00. Minh 6 lần (HEAVY), lật 1 → 5 lần, vẫn HEAVY. |
| BR-M09-18 | Sự kiện | Khiếu nại bài bị gỡ được chấp nhận: bài trở lại trạng thái kiểm duyệt Bình thường; điểm đã trừ vì lần gỡ đó được hoàn (M12); cảnh cáo, ban ra cùng lần gỡ đó được lật theo BR-M09-16, BR-M09-17, trừ trường hợp ở BR-M09-29. | Bài P bị gỡ kèm cảnh cáo C3; khiếu nại P được chấp nhận: P hiện lại, điểm từ upvote của P được hoàn, C3 bị lật. |
| BR-M09-19 | Sự kiện | Khiếu nại bị từ chối: xử lý bị khiếu nại giữ nguyên; với khiếu nại gộp, cả bài và cảnh cáo giữ nguyên. | — |
| BR-M09-20 | Sự kiện | Thông báo kết luận khiếu nại (M07 gửi): khiếu nại ban gửi trong ứng dụng và qua email; khiếu nại cảnh cáo, bài viết chỉ gửi trong ứng dụng. | — |
| BR-M09-21 | Ràng buộc | Người khiếu nại mở xem lại nội dung của mình đã bị xử lý (chỉ đọc) từ khiếu nại của mình; không thấy danh tính người báo cáo, lý do người báo cáo chọn, mô tả, bằng chứng của báo cáo. | — |
| BR-M09-22 | Sự kiện | Khiếu nại không bị xóa; dữ liệu khiếu nại được giữ cả khi tài khoản người khiếu nại bị xóa, để phục vụ an toàn cộng đồng. | — |
| BR-M09-23 | Sự kiện | Hạn khiếu nại và giới hạn bằng chứng là hằng số chính sách: không đổi qua giao diện, chỉ đổi qua triển khai. | — |
| BR-M09-24 | Sự kiện | Bài bị AI tự từ chối kèm một cảnh cáo AI: tác giả nhận một thông báo nêu cả hai (bài bị từ chối, chưa được đăng; bạn bị cảnh cáo), kèm một nút Khiếu nại; bài và cảnh cáo được khiếu nại chung trong một khiếu nại, không khiếu nại riêng cảnh cáo đó. Chấp nhận: bài chuyển sang Đã đăng ngay, không quét lại, và cảnh cáo bị lật; nếu tác giả đã gửi lại bài trước khi kết luận thì chỉ cảnh cáo bị lật. Tác giả vẫn được sửa và gửi lại bài không giới hạn (M03). | An gửi P lúc 01/10 10:00, AI chấm 0,92: P Bị từ chối, An nhận C1. An khiếu nại 03/10, Mod chấp nhận 04/10: P Đã đăng, C1 bị lật. Nếu 03/10 An tự sửa và gửi lại, P đã đăng: chấp nhận ngày 04/10 chỉ lật C1. |
| BR-M09-25 | Sự kiện | Khiếu nại gửi trong hạn vẫn được xét và lật như thường dù xử lý đã kết thúc trước lúc kết luận (ban hết hạn hoặc được gỡ, mức cảnh cáo đã giảm). | Ban 30 ngày lúc 01/10, khiếu nại 05/10, ban hết 31/10, chấp nhận 02/11: ban Bị lật, không tính vào số lần đã bị ban, tài khoản vẫn ACTIVE. C3 lúc 01/10 (MEDIUM), khiếu nại 05/10, 11/10 về LIGHT với 2 lần, chấp nhận 15/10: còn 1 lần, LIGHT. C1 lúc 01/10, khiếu nại 03/10, 08/10 về Sạch, chấp nhận 10/10: số lần giữ 0, C1 bị lật. |
| BR-M09-26 | Sự kiện | Lật một cảnh cáo hay một ban ra cùng lần ẩn một bình luận không làm bình luận hiện lại; bình luận giữ trạng thái Bị ẩn. | Bình luận B của An bị AI ẩn kèm cảnh cáo C1; C1 được lật: B vẫn Bị ẩn. |
| BR-M09-27 | Ràng buộc | Kết luận khiếu nại bắt buộc có lý do ở cả Chấp nhận và Từ chối; người khiếu nại thấy kết luận kèm lý do. Người khiếu nại không rút, không sửa khiếu nại đã gửi. | Mod chọn Từ chối mà lý do trống: từ chối thao tác. |
| BR-M09-28 | Sự kiện | Mọi thông báo về một xử lý khiếu nại được (cảnh cáo, ban, bài bị gỡ, bài bị AI tự từ chối) kèm nút Khiếu nại, bất kể người ra xử lý là AI, Mod hay Admin. Thông báo về bình luận bị ẩn, nhóm bị ẩn hoặc bị khóa không kèm. | AI tự cảnh cáo An: thông báo "Bạn bị cảnh cáo" có nút Khiếu nại, như khi Mod cảnh cáo trong vụ. |
| BR-M09-29 | Suy diễn | Cảnh cáo hay ban ra cùng lần gỡ một bài chỉ bị lật một lần, theo khiếu nại được Chấp nhận trước: khiếu nại riêng của nó hoặc khiếu nại bài. Nó đã có khiếu nại riêng bị Từ chối thì khiếu nại bài được chấp nhận không lật nó. Xử lý đã bị lật thì khiếu nại mới cho nó bị từ chối khi gửi; khiếu nại của nó đang chờ vẫn được xét, chấp nhận thì không đổi gì thêm. | Mod gỡ bài P của An kèm cảnh cáo C3. (1) An khiếu nại C3, bị từ chối; sau đó khiếu nại P, được chấp nhận: P hiện lại, hoàn điểm, C3 giữ nguyên. (2) An khiếu nại P trước, được chấp nhận: P hiện lại, C3 bị lật; An khiếu nại C3 sau đó: bị từ chối. (3) An khiếu nại P và C3 cùng lúc, P được chấp nhận trước: C3 bị lật; khiếu nại C3 vẫn xét, chấp nhận không đổi gì. (4) Cùng vụ bị ban 30 ngày; khiếu nại ban được chấp nhận rồi khiếu nại P được chấp nhận: ban đã lật, không đổi gì thêm. |

### 5.10 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Khiếu nại | Người khiếu nại; loại khiếu nại (ban, cảnh cáo, bài viết); xử lý bị khiếu nại; lời giải thích; bằng chứng (tối đa 3 ảnh); thời điểm gửi; trạng thái (Chờ xét, Đã kết luận); người đang giữ; thời điểm thao tác cuối của người giữ; kết luận (Chấp nhận, Từ chối); lý do kết luận; người kết luận; thời điểm kết luận | Thuộc một Tài khoản (M01); nhắm vào đúng một Cảnh cáo, một Ban (M08) hoặc một Bài viết (M03); khiếu nại gộp nhắm vào một lần từ chối bài cùng cảnh cáo AI ra cùng lần; mỗi xử lý có nhiều nhất một Khiếu nại |
| Cảnh cáo (M08) | Trạng thái Bị lật (M09 đặt) | Khiếu nại được một lần; cảnh cáo ra cùng lần AI từ chối bài chỉ khiếu nại qua khiếu nại gộp |
| Ban (M08) | Trạng thái Bị lật (M09 đặt) | Khiếu nại được một lần |
| Bài viết (M03) | Trạng thái kiểm duyệt Bị ẩn → Bình thường; trạng thái đăng Bị từ chối → Đã đăng, khi khiếu nại được chấp nhận | Khiếu nại được một lần cho mỗi lần bị gỡ hoặc bị AI tự từ chối |

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Khiếu nại | FR-M09-01.01 | FR-M09-02.01, FR-M09-03.01, FR-M09-03.02, FR-M09-06.01; thống kê: M15 | Giữ, nhả: FR-M09-04.01, FR-M09-04.06; kết luận: FR-M09-07.01, FR-M09-07.02; nội dung khiếu nại: Không có (FR-M09-01.22) | Không có (FR-M09-01.16) |
| Cảnh cáo (M08) | M08 | FR-M09-06.02 | Lật: FR-M09-08.04, FR-M09-08.05, FR-M09-08.13 | M08 |
| Ban (M08) | M08 | FR-M09-06.02 | Lật: FR-M09-08.01 | M08 |
| Bài viết (M03) | M03 | FR-M09-06.04, FR-M09-02.03 | Hiện lại: FR-M09-08.08; đăng bài bị AI từ chối: FR-M09-08.12 | M03 |

### 5.11 Chuyển trạng thái

#### Khiếu nại

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người dùng gửi khiếu nại | Xử lý khiếu nại được (BR-M09-01, BR-M09-02), còn hạn (BR-M09-04), chưa từng được khiếu nại (BR-M09-06), tài khoản không bị ban hoặc xử lý là chính lệnh ban (BR-M09-07), nội dung hợp lệ (BR-M09-03) | Chờ xét, chưa ai giữ | FR-M09-01.01 |
| Chờ xét, chưa ai giữ | Mod hoặc Admin chọn "Nhận xử lý" | Với Mod: khiếu nại không về xử lý do chính Mod đó ra, không do một Mod gửi (BR-M09-12) | Chờ xét, đang được giữ | FR-M09-04.01, FR-M09-04.03, FR-M09-04.08 |
| Chờ xét, đang được giữ | Người giữ không thao tác 30 phút | — | Chờ xét, chưa ai giữ | FR-M09-04.06 |
| Chờ xét, đang được giữ | Người giữ chọn Chấp nhận | Có lý do kết luận (BR-M09-27) | Đã kết luận, Chấp nhận | FR-M09-07.01, FR-M09-07.11 |
| Chờ xét, đang được giữ | Người giữ chọn Từ chối | Có lý do kết luận (BR-M09-27) | Đã kết luận, Từ chối | FR-M09-07.02, FR-M09-07.11 |

#### Ban (phần M09)

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Mod hoặc Admin ban người dùng (M08) | — | Đang hiệu lực | M08 |
| Đang hiệu lực | Ban tạm thời hết hạn (M08) | — | Hết hạn | M08 |
| Đang hiệu lực | Mod hoặc Admin gỡ ban (M08) | — | Đã gỡ | M08 |
| Đang hiệu lực | Khiếu nại ban được chấp nhận, hoặc khiếu nại bài bị gỡ được chấp nhận và ban ra cùng lần gỡ đó | Với khiếu nại bài: chưa bị lật, chưa có khiếu nại riêng bị Từ chối (BR-M09-29) | Bị lật | FR-M09-08.01, FR-M09-08.10, FR-M09-08.16 |
| Hết hạn | Khiếu nại ban gửi trong hạn được chấp nhận sau khi ban hết hạn | — | Bị lật | FR-M09-08.01 |
| Đã gỡ | Khiếu nại ban gửi trong hạn được chấp nhận sau khi ban được gỡ | — | Bị lật | FR-M09-08.01 |

#### Cảnh cáo (phần M09)

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | AI, Mod hoặc Admin cảnh cáo người dùng (M08) | — | Đang tính | M08 |
| Đang tính | Khiếu nại cảnh cáo được chấp nhận; khiếu nại bài bị gỡ được chấp nhận và cảnh cáo ra cùng lần gỡ đó; hoặc khiếu nại gộp được chấp nhận | Với khiếu nại bài: chưa bị lật, chưa có khiếu nại riêng bị Từ chối (BR-M09-29) | Bị lật | FR-M09-08.04, FR-M09-08.10, FR-M09-08.13, FR-M09-08.16 |

#### Trạng thái kiểm duyệt của bài viết (phần M09)

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| Bình thường | Mod hoặc Admin gỡ bài vì vi phạm (M08) | — | Bị ẩn | M08 |
| Bị ẩn | Khiếu nại bài bị gỡ được chấp nhận | — | Bình thường | FR-M09-08.08 |

#### Trạng thái đăng của bài viết (phần M09)

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Tác giả gửi bài (M03) | — | Chờ duyệt | M03 |
| Chờ duyệt | AI cho điểm quét từ 0,9 trở lên (M03) | — | Bị từ chối | M03 |
| Bị từ chối | Khiếu nại gộp được chấp nhận | Tác giả chưa gửi lại bài (BR-M09-24) | Đã đăng | FR-M09-08.12, FR-M09-08.14 |

#### Tài khoản (phần M09)

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| ACTIVE | Mod hoặc Admin ban tài khoản (M08) | — | BANNED | M08 |
| BANNED | Khiếu nại một ban đang hiệu lực được chấp nhận | — | ACTIVE | FR-M09-08.02 |

### 5.12 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Cung cấp | M01 | Hạn khiếu nại để màn hình tài khoản bị khóa hiện hoặc ẩn nút khiếu nại; khiếu nại ban được chấp nhận đưa tài khoản về ACTIVE | FR-M09-01.13, FR-M09-08.02 |
| Dùng | M01 | Tài khoản BANNED đăng nhập vào màn hình bị khóa, chỉ khiếu nại được lệnh ban; đặt lại mật khẩu để vào màn hình đó; đăng nhập trước khi tới trang khiếu nại | FR-M09-01.04, FR-M09-01.05, FR-M09-01.18 |
| Cung cấp | M03 | Khiếu nại bài bị gỡ hoặc bị AI tự từ chối; chấp nhận thì bài bị gỡ về Bình thường, bài bị AI từ chối sang Đã đăng không quét lại; thông báo từ chối gộp với cảnh cáo AI kèm nút Khiếu nại | FR-M09-01.03, FR-M09-01.19, FR-M09-08.08, FR-M09-08.12 |
| Dùng | M03 | Bài đã xóa, đã xóa hẳn, tự ẩn được giữ để xem trong khiếu nại; tác giả xem lại bài chỉ đọc từ khiếu nại của mình; tác giả sửa và gửi lại bài bị AI từ chối | FR-M09-06.04, FR-M09-02.03, FR-M09-08.14 |
| Cung cấp | M04 | Khiếu nại cảnh cáo, ban; bình luận không có khiếu nại riêng; lật cảnh cáo, ban không làm bình luận bị ẩn hiện lại | FR-M09-01.15, FR-M09-08.15 |
| Dùng | M04 | Bình luận đã xóa được giữ để xét khiếu nại; chủ bình luận xem lại bình luận chỉ đọc từ khiếu nại của mình | FR-M09-06.04, FR-M09-02.03 |
| Cung cấp | M07 | Sự kiện thông báo kết luận khiếu nại kèm lý do: khiếu nại ban gửi trong ứng dụng và email; khiếu nại cảnh cáo, bài viết chỉ trong ứng dụng; thông báo gộp bài bị AI từ chối và cảnh cáo | FR-M09-07.04, FR-M09-07.05, FR-M09-01.19 |
| Cung cấp | M08 | Lật cảnh cáo (giảm số lần, không dưới 0, tính lại mức), lật ban (không tính vào số lần đã bị ban) | FR-M09-08.01, FR-M09-08.03, FR-M09-08.04, FR-M09-08.05 |
| Dùng | M08 | Cảnh cáo, ban, kết luận vụ là đối tượng khiếu nại; nút Khiếu nại trong mọi thông báo về xử lý khiếu nại được; nhật ký để Mod xem thao tác của Mod khác khi xét khiếu nại | FR-M09-01.06, FR-M09-06.02, FR-M09-06.03 |
| Dùng | M10 | Vai trò Mod, Admin để xem hàng chờ và xét khiếu nại; Mod bị ban mất vai trò Mod, lật ban không trả lại vai trò (Admin gửi đề xuất làm Mod) | FR-M09-03.07, FR-M09-04.04, FR-M09-08.11 |
| Dùng | M11 | Thao tác kiểm duyệt cấp nhóm không khiếu nại được | FR-M09-01.15 |
| Cung cấp | M12 | Hoàn điểm đã trừ khi khiếu nại bài bị gỡ được chấp nhận | FR-M09-08.09 |
| Dùng | M13 | Nhật ký quyết định AI để xét khiếu nại bài bị AI tự từ chối | FR-M09-06.05 |
| Cung cấp | M15 | Khiếu nại theo loại và kết luận cho thống kê kiểm duyệt | FR-M09-01.01, FR-M09-07.01, FR-M09-07.02 |

### 5.13 AI hỗ trợ và hành vi khi tắt AI

- M09 không gọi AI. Khiếu nại chỉ do Mod, Admin kết luận, AI không xét khiếu nại (FR-M09-07.09).
- Xử lý do AI đưa ra khiếu nại được như xử lý của Mod, Admin: cảnh cáo AI tự ra (FR-M09-01.07); bài bị AI tự từ chối,
  gộp với cảnh cáo AI đi kèm (FR-M09-01.19, FR-M09-01.20). Các khiếu nại này hiện với mọi Mod trừ khi người gửi là Mod
  (FR-M09-03.06); người xét xem nhật ký quyết định AI của bài bị AI tự từ chối (FR-M09-06.05). Chấp nhận thì bài được
  đăng mà không quét lại (FR-M09-08.12).
- Công tắc AI tắt không làm đổi hành vi của M09: M09 không có trong bảng hành vi khi tắt AI của module-registry.

### 5.14 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.15 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-16 | Tạo mới | Phạm Văn Đức |
| 1.0 | 2026-10-18 | Chốt. Bổ sung theo DEC-195–202: Admin không bị báo cáo, không có khiếu nại; khiếu nại của Mod chỉ Admin xét; khiếu nại gộp bài bị AI từ chối và cảnh cáo AI; một hàng chờ chung; hạn cảnh cáo cố định; lật cả khi xử lý đã kết thúc; bỏ FR-M09-05; đóng OPEN-012 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M09-01 | DEC-084, DEC-085, DEC-086, DEC-087, DEC-115, DEC-198, DEC-166, DEC-197, DEC-078, DEC-109, DEC-180, DEC-091, DEC-192, QA-019, QA-154, QA-375, MR-M09 | Nói thẳng | — |
| FR-M09-02 | DEC-179, DEC-184, DEC-065, DEC-201 | Suy ra | Nguồn nói chủ nội dung mở xem lại nội dung của mình "từ khiếu nại của mình" và có thông báo về khiếu nại ⇒ người khiếu nại mở được khiếu nại của mình cùng kết luận |
| FR-M09-03 | DEC-088, DEC-115, DEC-200, DEC-090, QA-020, QA-021, DEC-195, DEC-196 | Nói thẳng | — |
| FR-M09-04 | DEC-088, DEC-115, DEC-195 | Nói thẳng | — |
| FR-M09-05 | DEC-196 | Nói thẳng | Đã bỏ ở phiên bản 0.1: chuyển lên Admin là quy tắc lọc (FR-M09-03.09) |
| FR-M09-06 | DEC-081, DEC-133, DEC-168, DEC-179, DEC-184, DEC-185, DEC-198 | Nói thẳng | — |
| FR-M09-07 | DEC-087, DEC-088, DEC-089, DEC-065, QA-019, QA-021, DEC-201 | Nói thẳng | — |
| FR-M09-08 | DEC-089, DEC-115, DEC-113, DEC-187, DEC-188, DEC-198, DEC-199, DEC-201, DEC-202 | Nói thẳng | — |
| FR-M09-01.01 | DEC-084, DEC-087, DEC-088, DEC-115, DEC-198 | Nói thẳng | — |
| FR-M09-01.02 | DEC-088, DEC-200, QA-379 | Nói thẳng | — |
| FR-M09-01.03 | DEC-088, DEC-115, DEC-198, DEC-200 | Nói thẳng | — |
| FR-M09-01.04 | DEC-085, DEC-197, QA-373 | Nói thẳng | — |
| FR-M09-01.05 | DEC-085 | Nói thẳng | — |
| FR-M09-01.06 | DEC-197, QA-374, DEC-192 | Nói thẳng | Nút do M08, M03 kèm vào thông báo |
| FR-M09-01.07 | DEC-078, DEC-197 | Nói thẳng | — |
| FR-M09-01.08 | DEC-085 | Suy ra | Tài khoản bị ban vẫn đăng nhập để khiếu nại, đường dẫn trong email đi qua đăng nhập ⇒ khiếu nại cần đăng nhập |
| FR-M09-01.09 | QA-019, DEC-085 | Suy ra | Khiếu nại là của người bị xử lý (quyền "của mình" ở 4.3) ⇒ người khác bị từ chối |
| FR-M09-01.10 | DEC-084 | Suy ra | Lời giải thích "required" ⇒ trống thì từ chối |
| FR-M09-01.11 | DEC-084 | Suy ra | "max 3 images" ⇒ ảnh thứ tư bị từ chối |
| FR-M09-01.12 | DEC-084, DEC-130 | Suy ra | "5MB/file", chỉ nhận JPEG/PNG/WebP ⇒ vượt thì từ chối |
| FR-M09-01.13 | DEC-086, DEC-115, DEC-198, DEC-199 | Suy ra | Hạn khiếu nại là khoảng được gửi; ban vĩnh viễn "appeal right permanently expires" ⇒ quá hạn thì từ chối |
| FR-M09-01.14 | DEC-087 | Suy ra | "appealed exactly once" ⇒ khiếu nại thứ hai cho cùng xử lý bị từ chối, dù khiếu nại đầu chưa kết luận |
| FR-M09-01.15 | DEC-115, DEC-180, DEC-194, DEC-109, DEC-091 | Suy ra | Nguồn nói các trường hợp này không có khiếu nại ⇒ từ chối |
| FR-M09-01.16 | DEC-154, DEC-129 | Nói thẳng | — |
| FR-M09-01.17 | DEC-090 | Nói thẳng | — |
| FR-M09-01.18 | DEC-197, QA-373 | Nói thẳng | — |
| FR-M09-01.19 | DEC-198, QA-375 | Nói thẳng | Thông báo gửi qua M07; thay cho hai thông báo riêng của M03, M08 |
| FR-M09-01.20 | DEC-198, QA-375 | Nói thẳng | — |
| FR-M09-01.21 | DEC-199, DEC-198 | Nói thẳng | "appealed only through the combined post appeal" |
| FR-M09-01.22 | DEC-201, QA-382 | Nói thẳng | — |
| FR-M09-01.23 | DEC-202, QA-383 | Nói thẳng | — |
| FR-M09-02.01 | DEC-179, DEC-184 | Suy ra | Người khiếu nại mở nội dung của mình "từ khiếu nại của mình" ⇒ mở được chính khiếu nại đó với những gì đã gửi |
| FR-M09-02.02 | DEC-201, QA-382 | Nói thẳng | — |
| FR-M09-02.03 | DEC-179, DEC-184 | Nói thẳng | Hiển thị nội dung do M03, M04 thực hiện (FR-M03-07.08, FR-M04-06.03) |
| FR-M09-02.04 | DEC-179, DEC-184 | Nói thẳng | — |
| FR-M09-02.05 | DEC-179 | Suy ra | Chỉ chủ nội dung xem lại từ "khiếu nại của mình" ⇒ người khác bị từ chối |
| FR-M09-03.01 | DEC-088, DEC-200, QA-379 | Nói thẳng | — |
| FR-M09-03.02 | DEC-200, QA-379 | Nói thẳng | — |
| FR-M09-03.03 | DEC-088, DEC-200 | Nói thẳng | — |
| FR-M09-03.04 | DEC-088, DEC-196 | Nói thẳng | — |
| FR-M09-03.05 | QA-021, DEC-196 | Nói thẳng | — |
| FR-M09-03.06 | DEC-078, DEC-088, DEC-198, DEC-195 | Suy ra | Mod chỉ bị loại khỏi khiếu nại về thao tác của chính mình và khiếu nại do Mod gửi ⇒ xử lý do AI ra không loại Mod nào khác |
| FR-M09-03.07 | DEC-090, QA-020 | Suy ra | Xử lý khiếu nại là việc dùng chung của Mod và Admin ⇒ người khác bị từ chối |
| FR-M09-03.08 | DEC-195, QA-370 | Nói thẳng | — |
| FR-M09-03.09 | DEC-196, QA-372, DEC-088 | Nói thẳng | Thay chức năng FR-M09-05 đã bỏ |
| FR-M09-04.01 | DEC-088, DEC-115 | Nói thẳng | — |
| FR-M09-04.02 | DEC-088 | Suy ra | Nhận xử lý cùng cơ chế với hàng chờ báo cáo, một vụ một người giữ ⇒ người thứ hai bị từ chối |
| FR-M09-04.03 | DEC-088, QA-021 | Nói thẳng | — |
| FR-M09-04.04 | DEC-090 | Suy ra | Chỉ Mod, Admin xử lý khiếu nại ⇒ người khác bị từ chối |
| FR-M09-04.05 | DEC-087 | Suy ra | Khiếu nại đã kết luận là cuối cùng ⇒ không còn gì để nhận |
| FR-M09-04.06 | DEC-088, DEC-115 | Nói thẳng | — |
| FR-M09-04.07 | DEC-088 | Suy ra | Tự nhả sau 30 phút "inactivity" ⇒ mỗi thao tác đặt lại khoảng 30 phút |
| FR-M09-04.08 | DEC-195 | Nói thẳng | — |
| FR-M09-05.01 | DEC-196 | Nói thẳng | Đã bỏ: chuyển lên Admin là quy tắc lọc |
| FR-M09-06.01 | DEC-084 | Nói thẳng | — |
| FR-M09-06.02 | DEC-081 | Nói thẳng | Các trường theo nhật ký kiểm duyệt (M08) |
| FR-M09-06.03 | DEC-081, QA-021 | Nói thẳng | Quyền xem nhật ký thuộc M08 (FR-M08-17.03) |
| FR-M09-06.04 | DEC-179, DEC-184, DEC-185, DEC-168 | Nói thẳng | — |
| FR-M09-06.05 | DEC-133, DEC-198 | Nói thẳng | — |
| FR-M09-06.06 | DEC-090 | Suy ra | Chỉ Mod, Admin xử lý khiếu nại ⇒ người khác bị từ chối |
| FR-M09-06.07 | DEC-088, QA-021 | Suy ra | Khiếu nại về thao tác của chính Mod bị ẩn hoàn toàn khỏi Mod đó ⇒ mở chi tiết cũng bị từ chối |
| FR-M09-06.08 | DEC-195 | Suy ra | Khiếu nại do Mod gửi chỉ Admin thấy và xét ⇒ Mod mở chi tiết bị từ chối |
| FR-M09-07.01 | DEC-089, DEC-088, DEC-201 | Nói thẳng | — |
| FR-M09-07.02 | DEC-087, DEC-088, DEC-201 | Nói thẳng | — |
| FR-M09-07.03 | DEC-087, DEC-198 | Suy ra | Chỉ khiếu nại được chấp nhận mới đảo ngược; từ chối là cuối cùng ⇒ xử lý giữ nguyên |
| FR-M09-07.04 | DEC-065, DEC-201 | Suy ra | Sự kiện "Appeal — ban-related" gửi cả hai kênh; người bị ban cần biết kết luận ⇒ ít nhất kết luận được gửi |
| FR-M09-07.05 | DEC-065, DEC-201 | Suy ra | Sự kiện "Appeal — post/warn-related" chỉ trong ứng dụng ⇒ kết luận gửi trong ứng dụng |
| FR-M09-07.06 | DEC-088 | Suy ra | Cơ chế nhận xử lý: chỉ người đang giữ xử lý ⇒ người khác bị từ chối |
| FR-M09-07.07 | DEC-088, QA-021 | Nói thẳng | — |
| FR-M09-07.08 | DEC-087 | Suy ra | "rejected appeals are final"; mỗi xử lý một khiếu nại ⇒ kết luận không đổi lại được |
| FR-M09-07.09 | QA-019 | Nói thẳng | "Review appeal: ... AI ✗" |
| FR-M09-07.10 | QA-021 | Nói thẳng | — |
| FR-M09-07.11 | DEC-201 | Suy ra | Lý do bắt buộc ở cả hai kết quả ⇒ trống thì từ chối |
| FR-M09-07.12 | DEC-195 | Nói thẳng | — |
| FR-M09-08.01 | DEC-089, DEC-199, QA-378 | Nói thẳng | — |
| FR-M09-08.02 | DEC-089 | Nói thẳng | Trạng thái tài khoản thuộc M01 (FR-M01-05.16) |
| FR-M09-08.03 | DEC-187 | Nói thẳng | Cách đếm thuộc M08 (FR-M08-14.12) |
| FR-M09-08.04 | DEC-188, DEC-089 | Nói thẳng | — |
| FR-M09-08.05 | DEC-089, DEC-188, DEC-199, QA-378 | Nói thẳng | — |
| FR-M09-08.06 | DEC-089, DEC-188 | Nói thẳng | "restriction lifted immediately" đọc theo DEC-188 (C.2) |
| FR-M09-08.07 | DEC-188 | Nói thẳng | — |
| FR-M09-08.08 | DEC-115, DEC-161 | Nói thẳng | "content is restored"; "gỡ" là Bị ẩn (DEC-161) |
| FR-M09-08.09 | DEC-115, DEC-113 | Nói thẳng | Việc cộng điểm thực hiện ở M12 |
| FR-M09-08.10 | DEC-115, DEC-202 | Nói thẳng | — |
| FR-M09-08.11 | DEC-201, QA-380 | Nói thẳng | Đề xuất làm Mod thuộc M10 (DEC-091) |
| FR-M09-08.12 | DEC-198, QA-375 | Nói thẳng | Trạng thái đăng thuộc M03 |
| FR-M09-08.13 | DEC-198 | Nói thẳng | — |
| FR-M09-08.14 | DEC-198 | Nói thẳng | — |
| FR-M09-08.15 | DEC-201, QA-381 | Nói thẳng | Đóng OPEN-012 |
| FR-M09-08.16 | DEC-202, QA-383 | Nói thẳng | — |
| FR-M09-08.17 | DEC-202 | Nói thẳng | — |
| BR-M09-01 | DEC-087, DEC-078, DEC-115, DEC-161, DEC-198, QA-019, DEC-195, QA-371 | Nói thẳng | — |
| BR-M09-02 | DEC-115, DEC-180, DEC-194, DEC-192, DEC-109, DEC-091 | Nói thẳng | — |
| BR-M09-03 | DEC-084, DEC-130 | Nói thẳng | — |
| BR-M09-04 | DEC-086, DEC-079, DEC-080, DEC-115, DEC-127, DEC-188, DEC-198, DEC-199, QA-377, QA-375 | Nói thẳng | — |
| BR-M09-05 | DEC-086, DEC-085, DEC-019 | Nói thẳng | — |
| BR-M09-06 | DEC-087, DEC-198 | Nói thẳng | — |
| BR-M09-07 | DEC-085, DEC-151, DEC-197, QA-373 | Nói thẳng | — |
| BR-M09-08 | DEC-085 | Nói thẳng | — |
| BR-M09-09 | DEC-088, DEC-115, DEC-200, QA-379 | Nói thẳng | — |
| BR-M09-10 | DEC-088, DEC-115, DEC-200 | Nói thẳng | — |
| BR-M09-11 | DEC-088, DEC-115 | Suy ra | Nguồn nói nhận xử lý "cùng cơ chế với hàng chờ báo cáo", tự nhả sau 30 phút không thao tác ⇒ một người giữ tại một thời điểm và thao tác tính như ở hàng chờ báo cáo (mở xem, kết luận) |
| BR-M09-12 | DEC-088, QA-021, QA-019, DEC-195, DEC-196, QA-370 | Nói thẳng | — |
| BR-M09-13 | DEC-088, QA-021, DEC-196, QA-372 | Nói thẳng | — |
| BR-M09-14 | DEC-078, DEC-088, DEC-198, DEC-195 | Suy ra | Mod chỉ bị loại khỏi khiếu nại về thao tác của chính mình và khiếu nại do Mod gửi; cảnh cáo AI, bài bị AI từ chối không do Mod ra ⇒ mọi Mod khác xét được |
| BR-M09-15 | DEC-081, DEC-179, DEC-184, DEC-185, DEC-168, DEC-133, DEC-198 | Nói thẳng | — |
| BR-M09-16 | DEC-089, DEC-187, DEC-201, QA-380 | Nói thẳng | — |
| BR-M09-17 | DEC-089, DEC-188, DEC-199 | Nói thẳng | — |
| BR-M09-18 | DEC-115, DEC-113, DEC-161, DEC-202 | Nói thẳng | — |
| BR-M09-19 | DEC-087, DEC-198 | Suy ra | Khiếu nại bị từ chối là cuối cùng và chỉ khiếu nại được chấp nhận mới đảo ngược ⇒ từ chối thì xử lý giữ nguyên |
| BR-M09-20 | DEC-065 | Nói thẳng | — |
| BR-M09-21 | DEC-179, DEC-184 | Nói thẳng | — |
| BR-M09-22 | DEC-154, DEC-129 | Nói thẳng | — |
| BR-M09-23 | DEC-090 | Nói thẳng | — |
| BR-M09-24 | DEC-198, DEC-199, QA-375, DEC-166 | Nói thẳng | — |
| BR-M09-25 | DEC-199, QA-378 | Nói thẳng | — |
| BR-M09-26 | DEC-201, DEC-180, QA-381 | Nói thẳng | — |
| BR-M09-27 | DEC-201, QA-382 | Nói thẳng | — |
| BR-M09-28 | DEC-197, QA-374, DEC-192 | Nói thẳng | — |
| BR-M09-29 | DEC-202, QA-383, DEC-087, DEC-115 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Thiếu chi tiết | Mod, Admin là người gửi khiếu nại: Admin có khiếu nại được không; người xét có xét khiếu nại do chính mình gửi không? | Admin không bị báo cáo, không có khiếu nại; khiếu nại, vụ liên quan tới Mod chỉ Admin xử lý (vai trò tính theo lúc bị xử lý); bài, bình luận của Admin không duyệt, không quét; nhóm do Admin làm Owner không báo cáo được; bài của Admin trong nhóm vẫn qua cổng nhóm. | ISS-310, ISS-311, QA-370, QA-371, DEC-195 |
| Q-02 | Thiếu chi tiết | Mod có xét khiếu nại về xử lý do Admin ra không? | Có, với người dùng không phải Mod (giữ nguồn); khiếu nại do Mod gửi chỉ Admin xét. | ISS-310, QA-370, DEC-195 |
| Q-03 | Mơ hồ | Hạn khiếu nại cảnh cáo khi thời gian thử thách bị đặt lại hoặc nối tiếp? | A — cố định 7/10/15 ngày từ lúc ra, theo mức của chính cảnh cáo đó. | ISS-317, QA-377, DEC-199 |
| Q-04 | Thiếu chi tiết | Khiếu nại bài bị AI tự từ chối: có cho không, hạn, hàng chờ, kết quả? | Cho khiếu nại, gộp với cảnh cáo AI đi kèm, một thông báo, một nút; hạn theo cảnh cáo, không có cảnh cáo thì 3 ngày; chấp nhận thì bài đăng ngay không quét lại, cảnh cáo bị lật. | ISS-315, QA-375, DEC-198 |
| Q-05 | Mơ hồ | Ưu tiên giữa khiếu nại bài viết (hàng chờ riêng) và khiếu nại cảnh cáo, ban? | B — một danh sách chung ban > cảnh cáo > bài, lọc theo loại. | ISS-319, QA-379, DEC-200 |
| Q-06 | Mơ hồ | "Mod duy nhất có thể xét" và chuyển lên Admin nghĩa là gì? | A — không có bước chuyển riêng, chỉ là quy tắc lọc. FR-M09-05 bỏ. | ISS-312, QA-372, DEC-196 |
| Q-07 | Mơ hồ | Khiếu nại xét sau khi xử lý đã kết thúc? | A — vẫn xét, vẫn lật; số lần cảnh cáo không xuống dưới 0. | ISS-318, QA-378, DEC-199 |
| Q-08 | Thiếu chi tiết | Kết luận khiếu nại có bắt buộc lý do không? | Bắt buộc ở cả hai kết quả; người khiếu nại thấy. | ISS-322, QA-382, DEC-201 |
| Q-09 | Thiếu chi tiết | Rút, sửa khiếu nại đã gửi? | Không. | ISS-322, QA-382, DEC-201 |
| Q-10 | Thiếu chi tiết | Tài khoản đang bị ban có khiếu nại cảnh cáo, bài bị gỡ không? | A — trong lúc bị ban chỉ khiếu nại chính lệnh ban. | ISS-313, QA-373, DEC-197 |
| Q-11 | Thiếu chi tiết | Lật ban của Mod có trả lại vai trò Mod không? | B — không; Admin gửi đề xuất làm Mod nếu muốn. | ISS-320, QA-380, DEC-201 |
| Q-12 | Thiếu chi tiết | Người bị AI tự cảnh cáo vào khiếu nại từ đâu? | Mọi thông báo về xử lý khiếu nại được đều kèm nút Khiếu nại, bất kể ai ra. | ISS-314, QA-374, DEC-197 |
| Q-13 | Cần cân nhắc | Lưu bản chụp nội dung lúc xử lý để xét khiếu nại (mở rộng phạm vi, stakeholder nêu)? | C — không làm ở MS1; ghi B.3 K-01. | ISS-316, QA-376, DEC-198 |
| Q-14 | Thiếu chi tiết | OPEN-012: bình luận bị ẩn có hiện lại khi cảnh cáo, ban liên quan bị lật không? | B — vẫn ẩn. TBD-M09-01 đóng. | ISS-321, QA-381, DEC-201 |
| Q-15 | Mâu thuẫn | Khiếu nại bài bị Mod gỡ (lật cả cảnh cáo, ban đi kèm) và khiếu nại riêng cảnh cáo, ban đó có thể cho kết luận ngược nhau? | B — giữ hai đường; xử lý đi kèm chỉ bị lật một lần, theo khiếu nại được chấp nhận trước; đã bị từ chối riêng thì khiếu nại bài không lật nó. | ISS-323, QA-383, DEC-202 |

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|

<!-- TBD-M09-01 (OPEN-012) đã chốt ở bước 6: Q-14, DEC-201. -->

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|
| K-01 | Bản chụp nội dung tại lúc xử lý để người xét khiếu nại thấy đúng nội dung đã bị xử lý | Bình luận, hồ sơ bị cảnh cáo mà không bị ẩn vẫn sửa được (bình luận không có lịch sử sửa), nên người xét có thể chỉ thấy nội dung đã sửa | Không làm ở MS1 (DEC-198); người xét dựa vào lý do kết luận, bằng chứng, lịch sử sửa bài, nhật ký AI; xem lại sau MS1 |

## Phụ lục C. Sổ nguồn

**Owner keywords:** M09, appeal, appeals, appealed, appealing, Appeal queue, appeal window, appeal right, /appeal, khiếu nại, Gửi khiếu nại, hàng chờ khiếu nại, hạn khiếu nại, Content Deletion Appeal, overturned, overturn, bị lật, reversal, đảo ngược, locked screen, conflict of interest, Auto-revoke, revokes the MOD role
**Dependency keywords:** warning, warn, cảnh cáo, warn count, probation, ban, banned, BANNED, unban, gỡ ban, report, báo cáo, claim, claim-based, queue, hàng chờ, audit log, nhật ký, post, bài viết, comment, bình luận, notification, thông báo, email, evidence, bằng chứng, image, ảnh, point, điểm, reputation, restore, khôi phục, HIDDEN, bị ẩn, account_state, timezone, ai_decision_log, admin, mod
**Mục draft của module:** Không có — draft không có mục riêng cho khiếu nại (DM-10.2, DM-10.3 nói cảnh cáo, ban thuộc M08)
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-118 ("full reversal of that principle" — M12, không nói khiếu nại); DG-5 ("không đảo ngược tùy tiện" — nguyên tắc thiết kế chung); DEC-105, DEC-121, QA-202 (vào nhóm C qua tham chiếu của DEC-113, DEC-114; nói xóa nhóm, tính bảng xếp hạng — M11, M12)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DEC-084 | Sở hữu | Hiện hành | FR-M09-01, FR-M09-01.01, FR-M09-01.10, FR-M09-01.11, FR-M09-01.12, FR-M09-06.01, BR-M09-03 | Nhóm A. Nội dung khiếu nại: lời giải thích bắt buộc, bằng chứng tùy chọn (3 ảnh, 5MB/ảnh) |
| DEC-085 | Sở hữu | Sửa một phần bởi DEC-151, DEC-197 | FR-M09-01, FR-M09-01.04, FR-M09-01.05, FR-M09-01.08, FR-M09-01.09, BR-M09-05, BR-M09-07, BR-M09-08 | Nhóm A. Tài khoản bị ban vẫn đăng nhập, gửi khiếu nại từ màn hình bị khóa; email ban có đường dẫn khiếu nại. DEC-151 thêm ngoại lệ: tài khoản BANNED được đặt lại mật khẩu (sửa không ghi dấu) |
| DEC-086 | Sở hữu | Sửa một phần bởi DEC-199 | FR-M09-01, FR-M09-01.13, BR-M09-04, BR-M09-05 | Nhóm A. Hạn khiếu nại: cảnh cáo = thời gian thử thách; ban tạm thời = thời hạn ban; ban vĩnh viễn = 90 ngày |
| DEC-087 | Sở hữu | Sửa một phần bởi DEC-202 | FR-M09-01, FR-M09-07, FR-M09-01.01, FR-M09-01.14, FR-M09-04.05, FR-M09-07.02, FR-M09-07.03, FR-M09-07.08, BR-M09-01, BR-M09-06, BR-M09-19, BR-M09-29 | Nhóm A. Mỗi xử lý khiếu nại một lần; bị từ chối thì không gửi lại |
| DEC-088 | Sở hữu | Sửa một phần bởi DEC-115, DEC-196, DEC-200 | FR-M09-03, FR-M09-04, FR-M09-07, FR-M09-01.01, FR-M09-01.02, FR-M09-01.03, FR-M09-03.01, FR-M09-03.03, FR-M09-03.04, FR-M09-03.06, FR-M09-03.09, FR-M09-04.01, FR-M09-04.02, FR-M09-04.03, FR-M09-04.06, FR-M09-04.07, FR-M09-06.07, FR-M09-07.01, FR-M09-07.02, FR-M09-07.06, FR-M09-07.07, BR-M09-09, BR-M09-10, BR-M09-11, BR-M09-12, BR-M09-13, BR-M09-14 | Nhóm A. Hàng chờ khiếu nại riêng; ưu tiên; nhận xử lý 30 phút; ẩn khiếu nại về thao tác của chính Mod; chuyển Admin. DEC-115 thêm loại thứ ba có hàng chờ riêng, ưu tiên thấp nhất |
| DEC-089 | Sở hữu | Sửa một phần bởi DEC-188, DEC-199, DEC-201 | FR-M09-07, FR-M09-08, FR-M09-07.01, FR-M09-08.01, FR-M09-08.02, FR-M09-08.04, FR-M09-08.05, FR-M09-08.06, BR-M09-16, BR-M09-17 | Nhóm A. Khiếu nại được chấp nhận: ban → ACTIVE, giữ bản ghi bị lật; cảnh cáo → gỡ hạn chế, giảm số lần. DEC-188 (tiêu đề ghi clarifies DEC-089, tool không bắt): cảnh cáo bị lật thì mức tính lại theo số lần còn lại, thời điểm kết thúc thử thách không đổi |
| DEC-113 | Phụ thuộc | Hiện hành | FR-M09-08, FR-M09-08.09, BR-M09-18 | Nhóm A. M12: trừ điểm khi nội dung bị Mod/Admin gỡ; DEC-115 hoàn lại khi khiếu nại bài bị gỡ thành công. Thay ngoại lệ nhóm của DEC-105 (đã loại) — không chạm M09 |
| DEC-114 | Nhắc tới | Hiện hành | Không áp dụng: M12 huy hiệu, không quy định hành vi M09 | Nhóm A. M12: huy hiệu không thu hồi; nằm trong section chung M09 + M12 |
| DEC-115 | Sở hữu | Sửa một phần bởi DEC-133, DEC-166, DEC-198, DEC-200, DEC-202 | FR-M09-01, FR-M09-03, FR-M09-04, FR-M09-08, FR-M09-01.01, FR-M09-01.03, FR-M09-01.13, FR-M09-01.15, FR-M09-04.01, FR-M09-04.06, FR-M09-08.08, FR-M09-08.09, FR-M09-08.10, BR-M09-01, BR-M09-02, BR-M09-04, BR-M09-09, BR-M09-10, BR-M09-11, BR-M09-18, BR-M09-29 | Nhóm A. Khiếu nại bài bị gỡ (chỉ bài, không bình luận): 30 ngày, hàng chờ riêng, ưu tiên thấp nhất, khôi phục + hoàn điểm + lật cảnh cáo/ban đi kèm. DEC-133, DEC-166 đưa bài bị AI từ chối vào khiếu nại (sửa không ghi dấu) |
| ISS-113 | Sở hữu | Trùng với DEC-084 | — | Nhóm A. Nội dung khiếu nại |
| ISS-114 | Sở hữu | Trùng với DEC-085 | — | Nhóm A. Tài khoản bị ban truy cập khiếu nại |
| ISS-115 | Sở hữu | Trùng với DEC-086 | — | Nhóm A. Hạn khiếu nại |
| ISS-116 | Sở hữu | Trùng với DEC-088 | — | Nhóm A. Hàng chờ khiếu nại |
| ISS-117 | Sở hữu | Trùng với DEC-089 | — | Nhóm A. Đảo ngược khi khiếu nại thành công |
| ISS-118 | Sở hữu | Trùng với DEC-087 | — | Nhóm A. Không khiếu nại lại |
| ISS-144 | Sở hữu | Trùng với DEC-115 | — | Nhóm A. Mở rộng: khiếu nại bài bị gỡ |
| QA-150 | Sở hữu | Trùng với DEC-084 | — | Nhóm A. Nội dung khiếu nại như báo cáo |
| QA-151 | Sở hữu | Trùng với DEC-085 | — | Nhóm A. Tài khoản bị ban vào trang khiếu nại |
| QA-152 | Sở hữu | Trùng với DEC-085 | — | Nhóm A. Email ban dẫn tới trang khiếu nại, qua đăng nhập |
| QA-153 | Sở hữu | Trùng với DEC-086 | — | Nhóm A. Hạn khiếu nại cảnh cáo, ban |
| QA-154 | Sở hữu | Hiện hành | FR-M09-01 | Nhóm A. Lý do giới hạn hạn khiếu nại ban vĩnh viễn |
| QA-155 | Sở hữu | Trùng với DEC-087 | — | Nhóm A. Mỗi xử lý khiếu nại một lần |
| QA-156 | Sở hữu | Trùng với DEC-088 | — | Nhóm A. Hàng chờ khiếu nại tách riêng |
| QA-157 | Sở hữu | Trùng với DEC-088 | — | Nhóm A. Thứ tự ưu tiên ban > cảnh cáo, đến trước xét trước |
| QA-158 | Sở hữu | Trùng với DEC-088 | — | Nhóm A. Mod không thấy khiếu nại về thao tác của mình; Mod duy nhất thì chuyển Admin |
| QA-159 | Sở hữu | Trùng với DEC-089 | — | Nhóm A. Kết quả khi khiếu nại được chấp nhận |
| QA-191 | Phụ thuộc | Trùng với DEC-113 | — | Nhóm A. M12: trừ điểm theo nguyên tắc trực tiếp/gián tiếp |
| QA-192 | Nhắc tới | Trùng với DEC-114 | — | Nhóm A. M12: huy hiệu; nằm trong section chung M09 + M12 |
| QA-193 | Sở hữu | Trùng với DEC-115 | — | Nhóm A. Khiếu nại bài bị gỡ |
| MR-M09 | Sở hữu | Sửa một phần bởi DEC-115, DEC-195 | FR-M09-01 | Nhóm A. Dòng module M09. Dòng registry chưa có khiếu nại bài bị gỡ |
| DEC-019 | Phụ thuộc | Hiện hành | BR-M09-05 | Nhóm B. M01: màn hình BANNED hiện lý do, thời gian khiếu nại, nút khiếu nại (nếu còn hạn). DEC-148, DEC-149, DEC-156 (ngoài bảng nguồn) chỉ sửa phần vô hiệu hóa, xóa tài khoản |
| DEC-032 | Phụ thuộc | Sửa một phần bởi DEC-161 | Chuyển M03 | Nhóm B. M03: bài Bị Mod ẩn, tác giả phải khiếu nại. DEC-190 (ngoài bảng nguồn) chỉ sửa việc báo cáo đổi trạng thái |
| DEC-065 | Phụ thuộc | Sửa một phần bởi DEC-115, DEC-180 | FR-M09-02, FR-M09-07, FR-M09-07.04, FR-M09-07.05, BR-M09-20 | Nhóm B. M07: sự kiện thông báo khiếu nại và kênh (ban: in-app + email; bài/bình luận/cảnh cáo: in-app). Chữ "comment" ở dòng "Appeal — post/comment/warn-related" hết hiệu lực: bình luận không có khiếu nại (DEC-115, DEC-180 mới hơn). DEC-147, DEC-151 chỉ thêm sự kiện tài khoản |
| DEC-074 | Phụ thuộc | Sửa một phần bởi DEC-192 | FR-M09-01.06 | Nhóm B. M08: thông báo cho người bị báo cáo kèm đường dẫn khiếu nại |
| DEC-078 | Phụ thuộc | Hiện hành | FR-M09-01, FR-M09-01.07, FR-M09-03.06, BR-M09-01, BR-M09-14 | Nhóm B. M08: cảnh cáo do AI tự ra khiếu nại được qua M09. DEC-186 (ngoài bảng nguồn) chỉ sửa ngưỡng AI, AI không tự cảnh cáo Mod/Admin; cảnh cáo AI vẫn khiếu nại được |
| DEC-081 | Phụ thuộc | Hiện hành | FR-M09-06, FR-M09-06.02, FR-M09-06.03, BR-M09-15 | Nhóm B. M08: nhật ký; Mod xem thao tác của Mod khác khi xét khiếu nại. DEC-146, DEC-193 (ngoài bảng nguồn) chỉ thêm loại thao tác ghi nhật ký; ngoại lệ xét khiếu nại giữ nguyên |
| DEC-090 | Phụ thuộc | Hiện hành | FR-M09-03, FR-M09-01.17, FR-M09-03.07, FR-M09-04.04, FR-M09-06.06, BR-M09-23 | Nhóm B. M10: xử lý khiếu nại dùng chung Mod/Admin; hằng số chính sách không cấu hình qua giao diện. Cạnh DEC-141 đúng nhưng chỉ sửa phần Topic |
| DEC-091 | Phụ thuộc | Hiện hành | FR-M09-01, FR-M09-01.15, BR-M09-02 | Nhóm B. M10: giáng cấp Mod không có quyền khiếu nại |
| DEC-109 | Sở hữu | Hiện hành | FR-M09-01, FR-M09-01.15, BR-M09-02 | Nhóm B. Thao tác kiểm duyệt cấp nhóm không khiếu nại được |
| DEC-122 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc ban đảo ngược được qua khiếu nại (M12) | Nhóm B. M12: ban đảo ngược được qua khiếu nại; tài khoản bị ban vẫn hiện nội dung. Cạnh lineage ISS-154 bác bỏ: ISS-154 là issue sinh ra DEC-122 |
| DEC-127 | Phụ thuộc | Hiện hành | BR-M09-04 | Nhóm B. Dùng chung: múi giờ Việt Nam cho hạn khiếu nại |
| DEC-133 | Phụ thuộc | Hiện hành | FR-M09-06, FR-M09-06.05, BR-M09-15 | Nhóm B. M13: nhật ký quyết định AI làm căn cứ xét khiếu nại bài bị AI xử lý |
| DEC-151 | Phụ thuộc | Hiện hành | BR-M09-07 | Nhóm B. M01: tài khoản BANNED được đặt lại mật khẩu để vào khiếu nại |
| DEC-152 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: ban tạm thời hết hạn tự về ACTIVE; nút OK màn hình bị khóa đăng xuất |
| DEC-154 | Nhắc tới | Hiện hành | FR-M09-01.16, BR-M09-22 | Nhóm B. M01: trang chính sách có mục khóa tài khoản và khiếu nại |
| DEC-162 | Phụ thuộc | Sửa một phần bởi DEC-179, DEC-184 | Chuyển M03 | Nhóm B. M03: bài Bị Mod ẩn không sửa, không khôi phục được — phải khiếu nại |
| DEC-166 | Sở hữu | Sửa một phần bởi DEC-198 | FR-M09-01, BR-M09-24 | Nhóm B. Bài bị AI tự từ chối: phản đối qua M09; nay là khiếu nại gộp với cảnh cáo AI (DEC-198) |
| DEC-168 | Phụ thuộc | Sửa một phần bởi DEC-185 | FR-M09-06, FR-M09-06.04, BR-M09-15 | Nhóm B. M03: Mod/Admin xem bài Bị gắn cờ, Bị Mod ẩn qua M08/M09 |
| DEC-179 | Phụ thuộc | Hiện hành | FR-M09-02, FR-M09-06, FR-M09-02.01, FR-M09-02.03, FR-M09-02.04, FR-M09-02.05, FR-M09-06.04, BR-M09-15, BR-M09-21 | Nhóm B. M03/M04: Mod/Admin xem nội dung đã xóa trong khiếu nại; chủ nội dung xem lại từ khiếu nại của mình |
| DEC-180 | Phụ thuộc | Sửa một phần bởi DEC-201 | FR-M09-01, FR-M09-01.15, BR-M09-02, BR-M09-26 | Nhóm B. M04: bình luận không có khiếu nại; hiện lại khi lật cảnh cáo/ban: OPEN-012. Cạnh lineage OPEN-012 bác bỏ: OPEN-012 được DEC-201 đóng, không sửa DEC-180 |
| DEC-184 | Phụ thuộc | Hiện hành | FR-M09-02, FR-M09-06, FR-M09-02.01, FR-M09-02.03, FR-M09-02.04, FR-M09-06.04, BR-M09-15, BR-M09-21 | Nhóm B. M03: bài Đã xóa hẳn xem được trong khiếu nại |
| DEC-185 | Phụ thuộc | Hiện hành | FR-M09-06, FR-M09-06.04, BR-M09-15 | Nhóm B. M03: bài Tự ẩn xem được trong khiếu nại |
| DEC-187 | Phụ thuộc | Hiện hành | FR-M09-08, FR-M09-08.03, BR-M09-16 | Nhóm B. M08: ban bị lật do khiếu nại không tính vào số lần đã bị ban |
| DEC-188 | Phụ thuộc | Hiện hành | FR-M09-08, FR-M09-08.04, FR-M09-08.05, FR-M09-08.06, FR-M09-08.07, BR-M09-04, BR-M09-17 | Nhóm B. M08: cảnh cáo bị lật: số lần giảm 1, mức tính lại, bản ghi giữ, thời gian thử thách không đổi |
| DEC-189 | Phụ thuộc | Sửa một phần bởi DEC-195 | Chuyển M08 | Nhóm B. M08: chỉ Admin cảnh cáo, ban Mod; ban Mod thì mất vai trò Mod |
| DEC-192 | Phụ thuộc | Sửa một phần bởi DEC-197 | FR-M09-01, FR-M09-01.06, BR-M09-02, BR-M09-28 | Nhóm B. M08: đường dẫn khiếu nại chỉ kèm cảnh cáo, ban, bài bị ẩn |
| DEC-194 | Phụ thuộc | Hiện hành | FR-M09-01.15, BR-M09-02 | Nhóm B. M08: nhóm bị ẩn/khóa không kèm đường dẫn khiếu nại |
| ISS-038 | Nhắc tới | Hiện hành | Không áp dụng: câu hỏi đã được QA-019–QA-021 trả lời | Nhóm B. Câu hỏi Phase 2 về ban và khiếu nại; trả lời ở QA-019–QA-021 |
| ISS-111 | Phụ thuộc | Trùng với DEC-081 | — | Nhóm B. M08: nhật ký, ngoại lệ khi xét khiếu nại |
| ISS-119 | Phụ thuộc | Trùng với DEC-090 | — | Nhóm B. M10: xử lý khiếu nại dùng chung |
| ISS-120 | Phụ thuộc | Trùng với DEC-091 | — | Nhóm B. M10: giáng cấp không khiếu nại |
| ISS-139 | Sở hữu | Trùng với DEC-109 | — | Nhóm B. Kiểm duyệt cấp nhóm không khiếu nại |
| ISS-181 | Phụ thuộc | Trùng với QA-244 | — | Nhóm B. M15: thống kê khiếu nại theo loại và kết quả |
| ISS-189 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm B. Dùng chung: múi giờ, hạn khiếu nại |
| ISS-195 | Phụ thuộc | Trùng với DEC-133 | — | Nhóm B. M13: nhật ký quyết định AI cho khiếu nại bài bị gỡ |
| ISS-285 | Phụ thuộc | Trùng với DEC-180 | — | Nhóm B. M04: khiếu nại bình luận |
| ISS-289 | Phụ thuộc | Trùng với DEC-179 | — | Nhóm B. M03/M04: xem lại nội dung đã xóa khi khiếu nại |
| OPEN-012 | Sở hữu | Bị thay bởi DEC-201 | — | Nhóm B. Bình luận bị ẩn có hiện lại khi khiếu nại cảnh cáo/ban liên quan thành công — chốt ở FR-M09. Ghi TBD-M09-01. Đóng bởi DEC-201 (Q-14) |
| QA-013 | Phụ thuộc | Hiện hành | Chuyển M10 | Nhóm B. M10: Mod bị ban tự mất vai trò Mod |
| QA-019 | Sở hữu | Sửa một phần bởi QA-020, QA-021, DEC-115, DEC-187, DEC-189 | FR-M09-01, FR-M09-07, FR-M09-01.09, FR-M09-07.09, BR-M09-01, BR-M09-12 | Nhóm B. Phase 2: hệ thống khiếu nại 2 loại (cảnh cáo, ban), người xét; AI không xét khiếu nại; bài/bình luận bị xóa không khiếu nại. Phần khiếu nại: "ban chỉ Admin xét" bị thay bởi QA-020, QA-021; "bài bị xóa không khiếu nại" bị thay bởi DEC-115. DEC-187, DEC-189 sửa phần M08. "AI không xét khiếu nại" còn hiệu lực |
| QA-020 | Sở hữu | Sửa một phần bởi DEC-115, DEC-188 | FR-M09-03, FR-M09-03.07 | Nhóm B. Phần khiếu nại: Mod xét khiếu nại cảnh cáo, ban trừ thao tác của mình; bài/bình luận bị xóa không khiếu nại. Phần cảnh cáo thuộc M08. "Bài bị xóa không khiếu nại" bị thay bởi DEC-115; DEC-188, DEC-186 (ngoài bảng nguồn) sửa phần M08 |
| QA-021 | Sở hữu | Sửa một phần bởi DEC-196 | FR-M09-03, FR-M09-07, FR-M09-03.05, FR-M09-04.03, FR-M09-06.03, FR-M09-06.07, FR-M09-07.07, FR-M09-07.10, BR-M09-12, BR-M09-13 | Nhóm B. Mod không xét khiếu nại về thao tác của mình, chuyển Admin; Admin xét mọi khiếu nại |
| QA-063 | Phụ thuộc | Trùng với DEC-019 | — | Nhóm B. M01: màn hình BANNED hiện thời gian khiếu nại còn lại |
| QA-123 | Phụ thuộc | Trùng với DEC-065 | — | Nhóm B. M07: danh sách sự kiện có khiếu nại |
| QA-124 | Phụ thuộc | Trùng với DEC-065 | — | Nhóm B. M07: email chỉ cho khiếu nại liên quan ban |
| QA-137 | Phụ thuộc | Trùng với DEC-074 | — | Nhóm B. M08: người vi phạm nhận đường dẫn khiếu nại |
| QA-148 | Phụ thuộc | Trùng với DEC-081 | — | Nhóm B. M08: Mod xem nhật ký Mod khác khi xét khiếu nại |
| QA-163 | Phụ thuộc | Trùng với DEC-091 | — | Nhóm B. M10: giáng cấp không khiếu nại |
| QA-187 | Sở hữu | Trùng với DEC-109 | — | Nhóm B. Kiểm duyệt cấp nhóm không khiếu nại |
| QA-204 | Nhắc tới | Trùng với DEC-122 | — | Nhóm B. M12: ban gỡ được qua khiếu nại |
| QA-223 | Nhắc tới | Hiện hành | Không áp dụng: M16, chỉ nhắc kênh email | Nhóm B. M16: email chỉ cho mật khẩu, vô hiệu hóa, ban, khiếu nại |
| QA-244 | Phụ thuộc | Hiện hành | Chuyển M15 | Nhóm B. M15: thống kê khiếu nại theo loại và kết quả |
| QA-248 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm B. Dùng chung: múi giờ, hạn khiếu nại |
| QA-254 | Phụ thuộc | Trùng với DEC-133 | — | Nhóm B. M13: nhật ký quyết định AI cho khiếu nại bài bị gỡ |
| QA-308 | Phụ thuộc | Trùng với DEC-151 | — | Nhóm B. M01: tài khoản BANNED đặt lại mật khẩu để khiếu nại |
| QA-314 | Nhắc tới | Trùng với DEC-154 | — | Nhóm B. M01: trang chính sách có mục khiếu nại |
| QA-328 | Sở hữu | Trùng với DEC-166 | — | Nhóm B. Bài bị AI tự từ chối: khiếu nại qua M09 |
| QA-343 | Phụ thuộc | Trùng với DEC-179 | — | Nhóm B. M03/M04: Mod/Admin xem nội dung đã xóa qua khiếu nại. Phần bài (OPEN-010) đã chốt ở DEC-184 |
| QA-345 | Phụ thuộc | Trùng với DEC-180 | — | Nhóm B. M04: bình luận không khiếu nại |
| QA-349 | Phụ thuộc | Trùng với DEC-179 | — | Nhóm B. M03/M04: chủ nội dung xem lại nội dung đã xóa từ khiếu nại |
| QA-351 | Phụ thuộc | Trùng với DEC-185 | — | Nhóm B. M03: Mod xem bài Tự ẩn trong khiếu nại |
| QA-359 | Phụ thuộc | Trùng với DEC-187 | — | Nhóm B. M08: ban bị lật không tính vào số lần đã bị ban |
| QA-362 | Phụ thuộc | Trùng với DEC-192 | — | Nhóm B. M08: đường dẫn khiếu nại chỉ khi khiếu nại được |
| MR-A03 | Nhắc tới | Hiện hành | Không áp dụng: tóm tắt đợt M15 | Nhóm B. M15: thống kê khiếu nại |
| MR-A04 | Nhắc tới | Hiện hành | Không áp dụng: tóm tắt Phase 6; múi giờ lấy từ DEC-127 | Nhóm B. Phase 6: múi giờ áp dụng cho hạn khiếu nại |
| MR-M08 | Nhắc tới | Hiện hành | Không áp dụng: dòng registry của M08 | Nhóm B. M08: ngoại lệ xem nhật ký khi xét khiếu nại. Dấu sửa DEC-186–194 chỉ chạm M08 |
| DEC-004 | Nhắc tới | Hiện hành | Không áp dụng: chỉ là lý do DEC-115 viện dẫn | Nhóm C. Lý do DEC-115 chỉ cho khiếu nại bài, không cho bình luận |
| DEC-079 | Phụ thuộc | Sửa một phần bởi DEC-122, DEC-188 | BR-M09-04 | Nhóm C. M08: thời gian thử thách 7/10/15 ngày — hạn khiếu nại cảnh cáo. DEC-188 đổi thời gian thử thách thành nối tiếp khi giảm mức. DEC-118 (đã loại), DEC-163 chỉ sửa phần bảng xếp hạng, tạo bài |
| DEC-080 | Phụ thuộc | Sửa một phần bởi DEC-152, DEC-187 | BR-M09-04 | Nhóm C. M08: thời hạn ban 30/90 ngày, vĩnh viễn — hạn khiếu nại ban |
| DEC-161 | Phụ thuộc | Sửa một phần bởi DEC-185 | FR-M09-08.08, BR-M09-01, BR-M09-18 | Nhóm C. M03: "bị Mod/Admin gỡ" là trạng thái Bị ẩn. DEC-185 chỉ thêm quét lại bài tự ẩn; "gỡ" = Bị ẩn giữ nguyên |
| ISS-142 | Phụ thuộc | Trùng với DEC-113 | — | Nhóm C. M12: trừ điểm khi nội dung bị gỡ |
| ISS-143 | Nhắc tới | Trùng với DEC-114 | — | Nhóm C. M12: huy hiệu |
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09 |
| DEC-129 | Phụ thuộc | Hiện hành | FR-M09-01.16, BR-M09-22 | Nhóm D. Dùng chung: nhật ký kiểm duyệt giữ vĩnh viễn; chỉ xóa hẳn khi an toàn. DEC-156 (ngoài bảng nguồn) chỉ sửa phần tài khoản đã xóa |
| DEC-130 | Phụ thuộc | Hiện hành | FR-M09-01.12, BR-M09-03 | Nhóm D. Dùng chung: tải ảnh (ảnh bằng chứng). DEC-160 (ngoài bảng nguồn) chỉ thêm tài liệu đính kèm bài |
| DEC-131 | Nhắc tới | Sửa một phần bởi DEC-154 | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09. DEC-146 (ngoài bảng nguồn) chỉ thêm Topic Suggestion |
| DEC-132 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09. DEC-141, DEC-144 (ngoài bảng nguồn) chỉ sửa phần Topic |
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: công nghệ | Nhóm D. Công nghệ |
| DEC-135 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung: kênh thời gian thực cho thông báo; không quy định hành vi M09 |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: công nghệ | Nhóm D. Công nghệ |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: công nghệ | Nhóm D. Công nghệ |
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09. DEC-155, DEC-157 (ngoài bảng nguồn) chỉ sửa phần đồng ý chính sách |
| ISS-190 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M09 |
| ISS-191 | Phụ thuộc | Trùng với DEC-129 | — | Nhóm D. Dùng chung: giữ dữ liệu |
| ISS-192 | Phụ thuộc | Trùng với DEC-130 | — | Nhóm D. Dùng chung: tải ảnh (ảnh bằng chứng) |
| ISS-193 | Nhắc tới | Trùng với DEC-131 | — | Nhóm D. Dùng chung; không quy định hành vi M09 |
| ISS-194 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M09 |
| ISS-196 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09 |
| ISS-197 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Công nghệ |
| ISS-198 | Nhắc tới | Trùng với DEC-135 | — | Nhóm D. Dùng chung; không quy định hành vi M09 |
| ISS-199 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Công nghệ |
| ISS-200 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09 |
| ISS-201 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09 |
| ISS-202 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09 |
| ISS-203 | Nhắc tới | Trùng với QA-263 | — | Nhóm D. Công nghệ |
| ISS-204 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M09 |
| QA-249 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M09 |
| QA-250 | Phụ thuộc | Trùng với DEC-129 | — | Nhóm D. Dùng chung: giữ dữ liệu |
| QA-251 | Phụ thuộc | Trùng với DEC-130 | — | Nhóm D. Dùng chung: tải ảnh (ảnh bằng chứng) |
| QA-252 | Nhắc tới | Trùng với DEC-131 | — | Nhóm D. Dùng chung; không quy định hành vi M09 |
| QA-253 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M09 |
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09 |
| QA-256 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Công nghệ |
| QA-257 | Nhắc tới | Trùng với DEC-135 | — | Nhóm D. Dùng chung; không quy định hành vi M09 |
| QA-258 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Công nghệ |
| QA-259 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09 |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09 |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09 |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M09 | Nhóm D. Dùng chung; không quy định hành vi M09 |
| QA-263 | Nhắc tới | Hiện hành | Không áp dụng: công nghệ | Nhóm D. Công nghệ |
| QA-264 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M09 |
| MR-A05 | Nhắc tới | Hiện hành | Không áp dụng: công nghệ | Nhóm D. Công nghệ |
| DEC-195 | Sở hữu | Hiện hành | FR-M09-03, FR-M09-04, FR-M09-03.06, FR-M09-03.08, FR-M09-04.08, FR-M09-06.08, FR-M09-07.12, BR-M09-01, BR-M09-12, BR-M09-14 | Nhóm A. Admin không bị báo cáo, không có khiếu nại; vụ, khiếu nại về Mod chỉ Admin; nội dung Admin không duyệt, không quét |
| DEC-196 | Sở hữu | Hiện hành | FR-M09-03, FR-M09-05, FR-M09-03.04, FR-M09-03.05, FR-M09-03.09, FR-M09-05.01, BR-M09-12, BR-M09-13 | Nhóm A. Ai thấy khiếu nại; chuyển lên Admin là quy tắc lọc |
| DEC-197 | Sở hữu | Hiện hành | FR-M09-01, FR-M09-01.04, FR-M09-01.06, FR-M09-01.07, FR-M09-01.18, BR-M09-07, BR-M09-28 | Nhóm A. Trong lúc bị ban chỉ khiếu nại lệnh ban; mọi thông báo xử lý khiếu nại được kèm nút Khiếu nại |
| DEC-198 | Sở hữu | Hiện hành | FR-M09-01, FR-M09-06, FR-M09-08, FR-M09-01.01, FR-M09-01.03, FR-M09-01.13, FR-M09-01.19, FR-M09-01.20, FR-M09-01.21, FR-M09-03.06, FR-M09-06.05, FR-M09-07.03, FR-M09-08.12, FR-M09-08.13, FR-M09-08.14, BR-M09-01, BR-M09-04, BR-M09-06, BR-M09-14, BR-M09-15, BR-M09-19, BR-M09-24 | Nhóm A. Khiếu nại gộp bài bị AI từ chối và cảnh cáo AI; không chụp nội dung |
| DEC-199 | Sở hữu | Hiện hành | FR-M09-08, FR-M09-01.13, FR-M09-01.21, FR-M09-08.01, FR-M09-08.05, BR-M09-04, BR-M09-17, BR-M09-24, BR-M09-25 | Nhóm A. Hạn khiếu nại cảnh cáo cố định; vẫn lật khi xử lý đã kết thúc |
| DEC-200 | Sở hữu | Hiện hành | FR-M09-03, FR-M09-01.02, FR-M09-01.03, FR-M09-03.01, FR-M09-03.02, FR-M09-03.03, BR-M09-09, BR-M09-10 | Nhóm A. Một danh sách khiếu nại chung, lọc theo loại |
| DEC-201 | Sở hữu | Hiện hành | FR-M09-02, FR-M09-07, FR-M09-08, FR-M09-01.22, FR-M09-02.02, FR-M09-07.01, FR-M09-07.02, FR-M09-07.04, FR-M09-07.05, FR-M09-07.11, FR-M09-08.11, FR-M09-08.15, BR-M09-16, BR-M09-26, BR-M09-27 | Nhóm A. Lật ban Mod không trả vai trò; bình luận vẫn ẩn; lý do kết luận bắt buộc; không rút, sửa |
| ISS-310 | Sở hữu | Trùng với DEC-195 | — | Nhóm A. Câu hỏi FR M09 |
| ISS-311 | Sở hữu | Trùng với DEC-195 | — | Nhóm A. Câu hỏi FR M09 |
| ISS-312 | Sở hữu | Trùng với DEC-196 | — | Nhóm A. Câu hỏi FR M09 |
| ISS-313 | Sở hữu | Trùng với DEC-197 | — | Nhóm A. Câu hỏi FR M09 |
| ISS-314 | Sở hữu | Trùng với DEC-197 | — | Nhóm A. Câu hỏi FR M09 |
| ISS-315 | Sở hữu | Trùng với DEC-198 | — | Nhóm A. Câu hỏi FR M09 |
| ISS-316 | Sở hữu | Trùng với DEC-198 | — | Nhóm A. Câu hỏi FR M09 |
| ISS-317 | Sở hữu | Trùng với DEC-199 | — | Nhóm A. Câu hỏi FR M09 |
| ISS-318 | Sở hữu | Trùng với DEC-199 | — | Nhóm A. Câu hỏi FR M09 |
| ISS-319 | Sở hữu | Trùng với DEC-200 | — | Nhóm A. Câu hỏi FR M09 |
| ISS-320 | Sở hữu | Trùng với DEC-201 | — | Nhóm A. Câu hỏi FR M09 |
| ISS-321 | Sở hữu | Trùng với DEC-201 | — | Nhóm A. Câu hỏi FR M09 |
| ISS-322 | Sở hữu | Trùng với DEC-201 | — | Nhóm A. Câu hỏi FR M09 |
| QA-370 | Sở hữu | Hiện hành | FR-M09-03.08, BR-M09-12 | Nhóm A. Câu trả lời FR M09 |
| QA-371 | Sở hữu | Hiện hành | BR-M09-01 | Nhóm A. Câu trả lời FR M09 |
| QA-372 | Sở hữu | Hiện hành | FR-M09-03.09, BR-M09-13 | Nhóm A. Câu trả lời FR M09 |
| QA-373 | Sở hữu | Hiện hành | FR-M09-01.04, FR-M09-01.18, BR-M09-07 | Nhóm A. Câu trả lời FR M09 |
| QA-374 | Sở hữu | Hiện hành | FR-M09-01.06, BR-M09-28 | Nhóm A. Câu trả lời FR M09 |
| QA-375 | Sở hữu | Hiện hành | FR-M09-01, FR-M09-01.19, FR-M09-01.20, FR-M09-08.12, BR-M09-04, BR-M09-24 | Nhóm A. Câu trả lời FR M09 |
| QA-376 | Sở hữu | Hiện hành | Không áp dụng: quyết định không chụp nội dung ở MS1, ghi ở B.3 K-01 | Nhóm A. Câu trả lời FR M09 |
| QA-377 | Sở hữu | Hiện hành | BR-M09-04 | Nhóm A. Câu trả lời FR M09 |
| QA-378 | Sở hữu | Hiện hành | FR-M09-08.01, FR-M09-08.05, BR-M09-25 | Nhóm A. Câu trả lời FR M09 |
| QA-379 | Sở hữu | Hiện hành | FR-M09-01.02, FR-M09-03.01, FR-M09-03.02, BR-M09-09 | Nhóm A. Câu trả lời FR M09 |
| QA-380 | Sở hữu | Hiện hành | FR-M09-08.11, BR-M09-16 | Nhóm A. Câu trả lời FR M09 |
| QA-381 | Sở hữu | Hiện hành | FR-M09-08.15, BR-M09-26 | Nhóm A. Câu trả lời FR M09 |
| QA-382 | Sở hữu | Hiện hành | FR-M09-01.22, FR-M09-02.02, BR-M09-27 | Nhóm A. Câu trả lời FR M09 |
| DEC-013 | Phụ thuộc | Sửa một phần bởi DEC-161, DEC-195 | Chuyển M03 | Nhóm C. M03: quét bài trước khi đăng; bài của Admin không quét |
| DEC-077 | Phụ thuộc | Sửa một phần bởi DEC-180, DEC-186, DEC-195 | Chuyển M08 | Nhóm C. M08: quét bình luận; bình luận của Admin không quét. DEC-190 (ngoài bảng nguồn) chỉ sửa phần vụ chờ xét |
| DEC-186 | Phụ thuộc | Sửa một phần bởi DEC-195 | Chuyển M08 | Nhóm C. M08: ngưỡng AI, cảnh cáo AI; nội dung Admin không quét |
| DEC-191 | Phụ thuộc | Sửa một phần bởi DEC-195 | Chuyển M08 | Nhóm C. M08: gửi báo cáo; không báo cáo được Admin |
| DEC-202 | Sở hữu | Hiện hành | FR-M09-08, FR-M09-01.23, FR-M09-08.10, FR-M09-08.16, FR-M09-08.17, BR-M09-18, BR-M09-29 | Nhóm A. Xử lý đi kèm bài bị gỡ chỉ bị lật một lần; khiếu nại nào được chấp nhận trước thì thắng |
| ISS-323 | Sở hữu | Trùng với DEC-202 | — | Nhóm A. Câu hỏi FR M09 |
| QA-383 | Sở hữu | Hiện hành | FR-M09-01.23, FR-M09-08.16, BR-M09-29 | Nhóm A. Câu trả lời FR M09 |
| GL:Appeal | Sở hữu | Sửa một phần bởi DEC-115, DEC-198 | Không áp dụng: nằm ngoài chỉ mục nên không trích ở Phụ lục A; phần còn hiệu lực (giao diện gọi là "Khiếu nại") ghi ở mục 2.1 | Ngoài chỉ mục: glossary.md dòng 47 viết dạng đoạn in đậm, index_sources.py không đọc. Định nghĩa "chỉ cảnh cáo và ban". Phần "không áp dụng cho bài bị xóa" bị thay |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| QA-019 → QA-020 → QA-021 → DEC-088 → DEC-195, DEC-196 | Người xét: Mod và Admin xét khiếu nại cảnh cáo, ban, bài viết; phần "ban chỉ Admin xét" của QA-019 bị thay. Mod không thấy, không xét khiếu nại về thao tác của chính mình và khiếu nại do một Mod gửi; khiếu nại do Mod gửi chỉ Admin xét, vai trò tính theo lúc bị xử lý. Admin xét mọi khiếu nại, kể cả về thao tác của chính Admin. AI không xét khiếu nại. "Chuyển lên Admin" (DEC-088) là quy tắc lọc: không còn Mod nào khác người ra xử lý thì chỉ Admin thấy; không có bước, dấu hay thông báo riêng. |
| DEC-189, DEC-191, DEC-186, DEC-013, DEC-077 → DEC-195 | Admin không bị báo cáo (kể cả nhóm do Admin làm Owner), không bị cảnh cáo, ban, nên không có khiếu nại. Vụ về nội dung, tài khoản của Mod chỉ Admin xử lý. Bài, bình luận của Admin không duyệt, không bị AI quét; bài của Admin trong nhóm vẫn qua cổng của nhóm. Phần áp dụng ở M03, M04, M08. |
| QA-019, QA-020, GL:Appeal → DEC-115 → DEC-133, DEC-166 → DEC-198; DEC-078; DEC-109; DEC-091; DEC-180 → DEC-201; DEC-192, DEC-194 | Đối tượng khiếu nại được: cảnh cáo (kể cả cảnh cáo do AI ra), ban tạm thời, ban vĩnh viễn, bài bị Mod/Admin gỡ (Bị ẩn, DEC-161), bài bị AI tự từ chối (khiếu nại gộp với cảnh cáo AI ra cùng lần). Không khiếu nại được: bình luận, nhóm bị ẩn hoặc khóa, thao tác kiểm duyệt cấp nhóm, giáng cấp Mod. Phần "bài, bình luận bị xóa không có khiếu nại" (QA-019, QA-020) và "chỉ cảnh cáo, ban" (GL:Appeal) bị thay đối với bài. |
| DEC-166, QA-328 → DEC-198, DEC-199 | Bài bị AI tự từ chối kèm cảnh cáo AI: một thông báo nêu cả hai kèm một nút Khiếu nại; một khiếu nại gộp, không khiếu nại riêng cảnh cáo đó; hạn bằng hạn của cảnh cáo, không có cảnh cáo (tác giả đang HEAVY hoặc là Mod) thì 3 ngày. Chấp nhận: bài Đã đăng ngay, không quét lại, cảnh cáo bị lật; tác giả đã gửi lại thì chỉ lật cảnh cáo. Tác giả vẫn sửa và gửi lại không giới hạn. Người xét xem nhật ký quyết định AI (DEC-133). |
| DEC-065 → DEC-115, DEC-180; DEC-074 → DEC-192 → DEC-197 | Mọi thông báo về một xử lý khiếu nại được kèm nút Khiếu nại, bất kể ai ra xử lý. Thông báo kết luận khiếu nại kèm lý do: khiếu nại ban gửi trong ứng dụng và email; khiếu nại cảnh cáo, bài viết chỉ trong ứng dụng. Chữ "comment" trong dòng sự kiện khiếu nại của DEC-065 hết hiệu lực. |
| DEC-088 → DEC-115 → DEC-200 | Hàng chờ khiếu nại tách khỏi hàng chờ báo cáo, là một danh sách chung: ban, rồi cảnh cáo, rồi bài viết; cùng loại thì gửi trước xét trước; lọc được theo loại. Nhận xử lý, tự nhả sau 30 phút không thao tác. |
| DEC-079 → DEC-188; DEC-080 → DEC-152, DEC-187; DEC-086 → DEC-199; DEC-115, DEC-198; DEC-127 | Hạn khiếu nại: cảnh cáo 7, 10 hoặc 15 ngày theo mức của chính cảnh cáo đó, không đổi khi có cảnh cáo sau hay khi giảm mức; ban tạm thời bằng thời hạn ban (30, 90 ngày); ban vĩnh viễn 90 ngày, quá hạn thì mất quyền khiếu nại; bài bị gỡ 30 ngày; bài bị AI từ chối theo hạn cảnh cáo đi kèm hoặc 3 ngày. "N ngày" là N × 24 giờ, theo giờ Việt Nam. |
| DEC-089 → DEC-187, DEC-188, DEC-199, DEC-201; DEC-115 → DEC-113, DEC-202; DEC-087 → DEC-202 | Khiếu nại được chấp nhận. Ban: bản ghi giữ, đánh dấu bị lật, không tính vào số lần đã bị ban; ban còn hiệu lực thì tài khoản về ACTIVE ngay; người từng là Mod về với vai trò User, không trả vai trò Mod. Cảnh cáo: số lần hiện tại giảm 1 (không dưới 0), mức tính lại, hạn chế theo mức mới, bản ghi giữ đánh dấu bị lật, thời điểm kết thúc thử thách không đổi ("gỡ hạn chế ngay" của DEC-089 được hiểu theo DEC-188). Bài bị gỡ: khôi phục bài, hoàn điểm, lật cảnh cáo, ban ra cùng lần gỡ; mỗi xử lý đi kèm chỉ bị lật một lần, theo khiếu nại được chấp nhận trước, và không bị lật nếu khiếu nại riêng của nó đã bị từ chối (DEC-202). Vẫn lật như vậy khi xử lý đã kết thúc trước lúc kết luận. Bình luận bị ẩn cùng lần không hiện lại. |
| DEC-085 → DEC-151, DEC-152, DEC-197; DEC-019 (QA-063) | Tài khoản bị ban vẫn đăng nhập, chỉ thấy màn hình bị khóa (lý do, thời gian khiếu nại còn lại, nút khiếu nại khi còn hạn, nút OK đăng xuất); chỉ khiếu nại được chính lệnh ban, thêm ngoại lệ đặt lại mật khẩu. Cảnh cáo, bài bị gỡ chỉ khiếu nại khi tài khoản ACTIVE và còn hạn. Email ban có đường dẫn tới trang khiếu nại, đi qua đăng nhập nếu cần. |
| DEC-084; DEC-087; DEC-201 | Nội dung khiếu nại: lời giải thích bắt buộc, bằng chứng tùy chọn tối đa 3 ảnh, mỗi ảnh tối đa 5MB. Mỗi xử lý khiếu nại một lần; bị từ chối là cuối cùng; không rút, không sửa. Kết luận bắt buộc lý do ở cả hai kết quả; người khiếu nại thấy kết luận kèm lý do. |
| DEC-081 (QA-148); DEC-168 → DEC-185; DEC-162 → DEC-179, DEC-184; DEC-133; DEC-198 | Khi xét khiếu nại: Mod xem chi tiết thao tác của Mod khác mà khiếu nại nhắc tới; Mod, Admin xem bài Bị Mod ẩn, bài đã xóa, đã xóa hẳn, tự ẩn và bình luận đã xóa trong ngữ cảnh khiếu nại; xem nhật ký quyết định AI của bài bị AI tự từ chối. Không có bản chụp nội dung lúc xử lý (B.3 K-01). Chủ nội dung xem lại nội dung của mình (chỉ đọc) từ khiếu nại của mình. |
| DEC-129; DEC-131 → DEC-154 | Dữ liệu khiếu nại thuộc nhóm dữ liệu giữ cho an toàn cộng đồng: không xóa, giữ cả khi tài khoản bị xóa. Phần còn lại của DEC-154 (trang chính sách) thuộc M01. |
| QA-013, DEC-189 → DEC-195, DEC-201 | Chỉ Admin cảnh cáo, ban Mod; ban Mod thì Mod mất vai trò; khiếu nại ban đó do Admin xét; chấp nhận thì không trả lại vai trò Mod. |
| DEC-180 → OPEN-012 → DEC-201 | Bình luận bị ẩn không hiện lại khi cảnh cáo, ban ra cùng lần ẩn được lật. OPEN-012 đóng. |
