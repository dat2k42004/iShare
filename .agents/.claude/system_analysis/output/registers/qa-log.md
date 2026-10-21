# QA Log Register

> Every question asked and its recorded answer.
> This is the primary traceability source for functional requirements.
> Format: structured entries below — one block per QA pair.

---

### QA-001
- **Issue ref:** ISS-021
- **Phase:** 1 — Business Context
- **Question:** Timeline và deadline cho toàn bộ dự án, cụ thể là MS1 là khi nào?
- **Answer (stakeholder):** Còn khoảng 3 tháng — deadline MS1 là giữa/cuối tháng 12 năm 2026. Thời gian này được đánh giá là đủ để hoàn thành toàn bộ project.
- **Implication:** MS1 = mid/late December 2026. Đây là mốc cứng duy nhất tính đến thời điểm BA. Kế hoạch phát triển các phase tiếp theo cần fit trong ~3 tháng còn lại.
- **Traceability note:** Timeline 3 tháng cho 11 module + AI layer là áp lực cao. Cần phân tích MoSCoW kỹ ở phase Requirements để đảm bảo P0 deliverable đúng hạn.

---

### QA-002
- **Issue ref:** ISS-022
- **Phase:** 1 — Business Context
- **Question:** Definition of Done cho MS1 là gì? Tiêu chí chấp nhận được (acceptance) và tiêu chí lý tưởng (nice-to-have)?
- **Answer (stakeholder):** Chấp nhận được: hoàn thành giai đoạn dev, có sản phẩm demo, đầy đủ full chức năng. Nice-to-have/khuyến khích: hoàn thành thêm giai đoạn testing, có output test hoặc test cho một số chức năng core (chức năng/module nào được test sẽ quyết định khi dev xong). Deploy không bắt buộc cho MS1.
- **Implication:** DoD MS1 = dev complete + demo-ready + full feature. Testing là bonus. No deployment required. Điều này cho phép team tập trung vào feature completeness thay vì infra/devops cho MS1.
- **Traceability note:** "Full feature" ở đây bao gồm cả AI layer hoạt động live (confirmed QA-007). Demo sẽ dùng seeded data nhưng AI phải xử lý real-time khi có action mới.

---

### QA-003
- **Issue ref:** ISS-023
- **Phase:** 1 — Business Context
- **Question:** Success metric cho MS1 là gì và đo bằng cách nào?
- **Answer (stakeholder):** Chọn mô hình A — đủ tài liệu, demo, sản phẩm hoàn thiện. Vì demo cần data, có thể cần product metric — dự tính sẽ dump/seed data để tạo số liệu demo. Product metric thực tế sẽ không đo được ở MS1 vì chưa deploy.
- **Implication:** Success metric của MS1 là qualitative (feature completeness, demo quality) chứ không phải quantitative (DAU, post count thực tế). Seeded data phục vụ mục đích demo trực quan.
- **Traceability note:** Cần thiết kế seeder script đủ mạnh để tạo data demo phong phú (users, posts, comments, interactions, badges) — đây là deliverable phụ nhưng quan trọng cho ngày demo.

---

### QA-004
- **Issue ref:** ISS-024
- **Phase:** 1 — Business Context
- **Question:** Landscape cạnh tranh hiện tại — HS đang dùng gì để trao đổi học thuật?
- **Answer (stakeholder):** Hiện tại chủ yếu là Facebook (group/chat) và Zalo (chat/group chat). Forum học thuật chính thức hầu như không có. Quora tồn tại nhưng chỉ ở dạng Q&A thông thường, ít được dùng. Đáng chú ý: HS hiện ít có tinh thần chia sẻ — xu hướng là tự tìm lời giải hoặc hỏi AI (ChatGPT, etc.) thay vì chia sẻ cộng đồng.
- **Implication:** iShare không có competitor trực tiếp trong phân khúc HS Việt Nam. Thách thức lớn nhất không phải cạnh tranh mà là thay đổi hành vi (behavior change): từ "hỏi AI cá nhân" sang "chia sẻ cộng đồng". Gamification (BG-03) trở nên đặc biệt quan trọng để tạo động lực ban đầu.
- **Traceability note:** Insight "HS hay hỏi AI thay vì share cộng đồng" là cơ sở để thiết kế AI layer không phải thay thế mà là hỗ trợ và kéo user vào tương tác cộng đồng. AI gợi ý → user xem post → user tham gia thảo luận.

---

### QA-005
- **Issue ref:** ISS-025 (phần 1)
- **Phase:** 1 — Business Context
- **Question:** Business goals của hệ thống là gì? Đâu là mục tiêu ưu tiên nhất?
- **Answer (stakeholder — phần 1):** Quan trọng nhất là tạo văn hóa học tập cộng đồng. HS cần có nơi trao đổi về học thuật, tâm tư, tâm lý. Đề nghị BA gợi ý bổ sung thêm.
- **BA proposed (pending confirm):** Đề xuất 6 goals (A–F): A) Cộng đồng học tập; B) Peer review chất lượng; C) Safe space cho chủ đề nhạy cảm; D) Gamification/phần thưởng; E) Peer learning "học thầy không tày học bạn"; F) AI tăng hiệu quả vận hành.
- **Implication (partial):** Xem QA-006 cho kết quả cuối.

---

### QA-006
- **Issue ref:** ISS-025 (phần 2 — confirm goals)
- **Phase:** 1 — Business Context
- **Question (follow-up):** Confirm và tinh chỉnh danh sách business goals từ QA-005.
- **Answer (stakeholder):** Bỏ ý F (AI goal). Tinh chỉnh: D (gamification/phần thưởng) rất hay — cơ sở lý thuyết là Expectancy Theory (Vroom, 1964): con người hành động hiệu quả hơn khi biết sẽ có phần thưởng/kết quả rõ ràng khi đạt mục tiêu. E (peer learning) chính là tinh thần "học thầy không tày học bạn" — một trong số tinh thần cốt lõi của hệ thống. C mở rộng hơn safe space cho nhạy cảm — không gian thảo luận đa chiều cho HS. Cấu trúc cuối: A+E = 1 goal, D = 1 goal, C = 1 goal riêng (mở rộng), E = 1 goal riêng.
- **Confirmed Business Goals:**
  - **BG-01:** Xây dựng văn hóa học tập cộng đồng — tạo không gian chia sẻ học thuật và tâm tư cho HS (A)
  - **BG-02:** Phát huy tinh thần peer learning — "học thầy không tày học bạn"; tôn vinh giá trị tri thức từ bạn bè đồng trang lứa (E)
  - **BG-03:** Thúc đẩy đóng góp tích cực qua gamification — dựa trên Expectancy Theory (Vroom, 1964): người dùng hành động hiệu quả hơn khi thấy phần thưởng/kết quả rõ ràng từ đóng góp của mình (D)
  - **BG-04:** Tạo không gian thảo luận đa chiều cho HS — không chỉ học thuật mà cả tâm tư, đời sống, các chủ đề đa dạng phù hợp lứa tuổi (C mở rộng)
- **Implication:** 4 business goals này là nền tảng cho toàn bộ feature set. Gamification (BG-03) phải được thiết kế có chiều sâu lý thuyết. Peer learning spirit (BG-02) ảnh hưởng đến UX — cần tôn vinh người đóng góp rõ ràng.
- **Traceability note:** BG-03 có thể dùng trực tiếp trong phần "cơ sở lý thuyết" của báo cáo luận văn — Expectancy Theory là framework học thuật được công nhận rộng rãi (Vroom, V.H. 1964. Work and Motivation. New York: Wiley). BG-02 gắn với tục ngữ dân gian Việt Nam — có thể dùng làm trích dẫn văn hóa trong phần giới thiệu đề tài.

---

### QA-007
- **Issue ref:** ISS-026
- **Phase:** 1 — Business Context
- **Question:** AI budget hợp lý cho MS1 là bao nhiêu? Tính toán chi phí thực tế cho 5 AI features bắt buộc ở scale demo.
- **Answer (stakeholder):** Phạm vi demo: ~20–30 users, tổng 50–70 posts (không phải per day). Summarization chỉ áp dụng cho Post (không phải Comment thread). AI phải hoạt động live khi có action mới (không phải dummy/seeded AI response).
- **BA calculation (confirmed):**
  - Scale: 70 posts × embedding + 70 classifications + 70 moderations + 70 summarizations + ~200 semantic searches
  - AI Moderation: OpenAI Moderation API → **$0.00** (free dedicated endpoint)
  - AI Classification: gpt-4o-mini → ~$0.002
  - Semantic Search: text-embedding-3-small → ~$0.001
  - Summarization (Post only): gpt-4o-mini → ~$0.003
  - Feedback/Eval Loop: minimal overhead → ~$0.001
  - **Total: < $0.01** — khuyến nghị nạp $5 OpenAI credit để có buffer thoải mái
  - **Provider stack đề xuất:** OpenAI (Moderation API free + gpt-4o-mini + text-embedding-3-small)
- **Status:** OPEN — budget chưa chốt chính thức, $5 credit là estimate an toàn.
- **Traceability note:** AI cost ở đây là cho MS1 demo only. Production scale sẽ cần recalculate khi có số liệu thực. OpenAI Moderation API miễn phí là lợi thế lớn — loại bỏ cost cho feature quan trọng nhất (content safety).

**[Amended 2026-10-19 — DEC-206: tóm tắt theo yêu cầu, giữ tạm 24 giờ, không tóm tắt mọi bài]**

---

### QA-008
- **Issue ref:** ISS-027
- **Phase:** 1 — Business Context
- **Question:** Kỳ vọng về production-readiness — hệ thống có cần sẵn sàng scale lên production sau MS1 không?
- **Answer (stakeholder):** MS1 là demo only. Nhưng hệ thống vẫn cần được xây đúng chuẩn production ngay từ đầu — sau deploy đỡ phải sửa nhiều. Tư duy: build for production, demo ở MS1.
- **Decision triggered:** Ngầm định production-ready architecture — không workaround, không hack for demo.
- **Implication:** Toàn bộ design decisions (DB schema, API design, auth, AI integration) phải theo production standard. Không được phép dùng shortcut "chỉ để demo" trừ khi được ghi rõ là technical debt.
- **Traceability note:** Điều này ảnh hưởng đến lựa chọn tech stack (stability > novelty), DB design (normalized, indexed đúng chuẩn), và AI integration (proper error handling, fallback khi AI unavailable).

---

### QA-009
- **Issue ref:** ISS-028
- **Phase:** 1 — Business Context
- **Question:** Sau khi bàn giao, ai giữ role ADMIN? Dev team, giáo viên/client, hay cả hai?
- **Context:** Câu hỏi ảnh hưởng trực tiếp đến thiết kế hệ thống: nếu chỉ dev team thì ADMIN là role kỹ thuật thuần túy, không cần flow bàn giao trong UI. Nếu cả hai thì cần "super admin pattern" — ADMIN có thể promote user khác lên ADMIN thông qua giao diện.
- **Answer (stakeholder):** Chọn C — cả hai. Dev team giữ quyền root ở cấp DB (không qua UI), đồng thời trong hệ thống có cơ chế ADMIN promote account khác thành ADMIN để bàn giao quyền vận hành (operation handover). Mục đích: sau MS1 có thể bàn giao operational admin cho giáo viên hoặc người được chỉ định mà không cần dev team can thiệp trực tiếp vào DB.
- **Decision triggered:** DEC-007 (Super Admin pattern — ADMIN có thể cấp quyền ADMIN cho user khác qua UI)
- **Implication:** Module ADMN cần thiết kế flow promote/demote ADMIN trong giao diện quản trị; dev team seed 1 root admin account từ DB khi khởi tạo hệ thống (via migration/seeder script).
- **Traceability note:** Pattern này phổ biến trong các hệ thống SaaS và forum (Discourse, Stack Overflow for Teams). Root admin được tạo qua migration/seeder, không expose qua UI đăng ký. Phù hợp với mô hình bàn giao học thuật: dev bàn giao credential root, client tự quản lý admin operation về sau.

---

### QA-010
- **Issue ref:** ISS-029
- **Phase:** 1 — Business Context
- **Question:** Có ràng buộc học thuật nào từ hội đồng/nhà trường về nội dung, scope, tài liệu, hoặc công nghệ không?
- **Answer (stakeholder — partial):** Không có ràng buộc đặc biệt về nội dung, scope hay tài liệu bắt buộc. Tech stack chưa được quyết định tại thời điểm này — sẽ xác nhận ở phase sau.
- **Status:** PARTIAL — ISS-029 giữ OPEN, chờ tech stack được chốt.
- **Traceability note:** Đây là điểm cần trace lại khi vào phase Architecture/Tech Stack — ràng buộc học thuật (nếu có) sẽ ảnh hưởng đến lựa chọn công nghệ và cấu trúc tài liệu nộp hội đồng.

---

### QA-011
- **Issue ref:** ISS-030
- **Phase:** 2 — Actors, Roles & Permissions
- **Question:** Guest (chưa đăng nhập) có quyền gì trên iShare?
- **Answer (stakeholder — confirmed):**
  - USR: Đăng ký, Đăng nhập
  - POST: Xem/đọc post (public + nội dung public group)
  - COMT: Xem comment
  - CLAS: Xem danh sách Topic / Tag / Khối lớp
  - GRP: Xem danh sách + mô tả + nội dung Group công khai; Private group ẩn hoàn toàn
  - REWD: Xem Leaderboard, Badges, Reputation score của user
  - AI: Xem AI Summary + AI Classification trên post
  - Report (POST/COMT): Không
  - Semantic Search: Không
  - INTR / MSG / ADMN: Không
- **Decision triggered:** Group có phân loại Public / Private. Guest chỉ tiếp cận Public group content.
- **New issue spawned:** ISS-GRP-01 (Phase 4 backlog) — deep dive Public vs Private group: ai tạo được private group, ai thấy private group tồn tại, cơ chế join private group, v.v.
- **Traceability note:** Cho Guest xem post + comment là quyết định quan trọng về SEO và discoverability — content iShare sẽ được index bởi search engine, tạo organic traffic. Không cho Guest dùng Semantic Search bảo vệ AI cost budget (ISS-026). Report yêu cầu auth để đảm bảo accountability và chống spam.

**[Amended 2026-10-13 — DEC-171: Guest xem được trang hồ sơ, chỉ đọc]**

**[Amended 2026-10-19 — DEC-206: tóm tắt AI chỉ cho người đã đăng nhập; Guest bấm thì được nhắc đăng nhập]**

**[Clarified 2026-10-20 — DEC-208: Guest tìm bài bằng full-text; "Tìm kiếm thông minh" nhắc đăng nhập]**

---

### QA-012
- **Issue ref:** ISS-031
- **Phase:** 2 — Actors, Roles & Permissions
- **Question:** USER trở thành MODERATOR bằng cách nào? Ai phong? Điều kiện gì?
- **Answer (stakeholder):** Do ADMIN chỉ định thủ công. Không có điều kiện bắt buộc (reputation, thâm niên, v.v.) — ADMIN toàn quyền quyết định.
- **Implication:** Module ADMN cần flow: ADMIN chọn user → promote thành MODERATOR. Không cần automated suggestion hay eligibility check.
- **Traceability note:** Mô hình đơn giản, phù hợp giai đoạn đầu của platform khi cộng đồng còn nhỏ. Nếu platform scale lên, có thể bổ sung reputation threshold sau — nhưng không thuộc scope MS1.

---

### QA-013
- **Issue ref:** ISS-032
- **Phase:** 2 — Actors, Roles & Permissions
- **Question:** MODERATOR mất role bằng cách nào?
- **Answer (stakeholder):** Chọn B + C — ba cơ chế:
  1. ADMIN revoke thủ công
  2. Auto-revoke khi MODERATOR bị ban (business rule bắt buộc — tránh lỗi logic role/state)
  3. MODERATOR tự từ chức (self-resign) — trigger flow tương tự ADMIN revoke nhưng do chính MODERATOR thực hiện
- **Implication:** Module ADMN cần 2 flow: (1) ADMIN revoke; (2) MODERATOR self-resign. Auto-revoke on ban là side-effect của ban action — cần ghi vào spec của feature Ban User.
- **Traceability note:** Self-resign có chi phí implement thấp nhưng giá trị UX cao — phù hợp với đối tượng HS có lịch học biến động. Auto-revoke on ban là business rule không thể thiếu để đảm bảo data consistency giữa role và account status.

**[Clarified 2026-10-21 — DEC-223: giữ tự từ chức, áp cả Admin không phải gốc]**

---

### QA-014
- **Issue ref:** ISS-033
- **Phase:** 2 — Actors, Roles & Permissions
- **Question:** Một user có thể vừa là MODERATOR vừa là ADMIN không?
- **Answer (stakeholder):** Không cần — ADMIN đã có full quyền. Role là hierarchy đơn: USER < MODERATOR < ADMIN. ADMIN kế thừa toàn bộ quyền MODERATOR.
- **Decision triggered:** Role model = single-value hierarchy, không phải multi-role set.
- **Implication:** DB column `role` là enum đơn (USER/MODERATOR/ADMIN). Permission check: if role >= MODERATOR → có quyền mod; if role == ADMIN → có full quyền. Không cần role array hay junction table.
- **Traceability note:** Mô hình này (role hierarchy) phổ biến trong forum platforms (Discourse, phpBB). Đơn giản hơn RBAC thuần túy, phù hợp với scope 3 role cố định của iShare.

---

### QA-015
- **Issue ref:** ISS-034
- **Phase:** 2 — Actors, Roles & Permissions
- **Question:** Anonymous Post — danh tính ẩn với ai?
- **Answer (stakeholder):** Ẩn với USER thường. MODERATOR và ADMIN đều thấy danh tính thật — vì MOD có quyền ban/warn account, cần biết ai đăng để xử lý vi phạm.
- **Implication:** DB vẫn lưu `author_id` đầy đủ cho mọi post kể cả anonymous. UI hiển thị "Ẩn danh" với USER; MODERATOR/ADMIN thấy tên thật + link profile. API cần filter field `author` theo role người gọi.
- **Traceability note:** Quyết định này đảm bảo anonymous post không trở thành lỗ hổng kiểm duyệt. Pattern phổ biến: lưu đủ ở DB, ẩn ở presentation layer theo permission.

---

### QA-016
- **Issue ref:** ISS-035 + ISS-039
- **Phase:** 2 — Actors, Roles & Permissions
- **Question:** GroupMember có role riêng trong Group không? Group có toggle kiểm duyệt và quan hệ với system moderation như thế nào?
- **Answer (stakeholder):** 3 level trong Group: Owner / Group Moderator / Member. Group có toggle pre-moderation (Owner bật/tắt). Luồng moderation chọn Luồng 1: Submit → AI Moderation (auto, real-time) → nếu AI pass → vào queue Group Mod (nếu toggle ON) → Group Mod approve → Live. System MODERATOR và ADMIN vẫn có quyền can thiệp vào content trong group bất kỳ lúc nào — group không phải vùng tự trị.
- **Implication:** GRP module cần: (1) role field riêng trong GroupMember table (owner/moderator/member); (2) setting `pre_moderation: boolean` trên Group; (3) post trong group có thêm trạng thái `pending_group_approval` trong state machine; (4) Group Mod queue UI.
- **New issues spawned (Phase 4 GRP backlog):** ISS-GRP-01 (Public vs Private), ISS-GRP-02 (chi tiết flow post trong group — nhiều sub-issues).
- **Traceability note:** AI làm bộ lọc vi phạm nghiêm trọng (tự động, real-time); Group Mod tập trung vào curation chất lượng nội dung của group. Hai tầng có vai trò khác nhau, không chồng chéo. System MOD/ADMIN là tầng override cuối cùng — đảm bảo platform không có "vùng cấm" với kiểm duyệt hệ thống.

---

### QA-017
- **Issue ref:** ISS-036
- **Phase:** 2 — Actors, Roles & Permissions
- **Question:** Có actor hệ thống (background/automated) nào? Scope AI Moderation có bao gồm Comment không? AI Classification hoạt động theo cơ chế nào?
- **Answer (stakeholder — confirmed):**
  - AI Moderation scan cả Post lẫn Comment (OpenAI Moderation API free → không có lý do cost để giới hạn)
  - AI Classification: gợi ý Topic (không auto-gán) — user review và chọn lại nếu cần. Kết quả cuối cùng (user chọn gì) là feedback cho AI → đây chính là cơ chế Feedback/Evaluation Loop cho classification feature
  - Tag: user tự quyết định hoàn toàn, AI không can thiệp
- **Confirmed system actors:**
  1. **AI Moderation Worker** — scan Post + Comment mới, real-time
  2. **AI Classification Worker** — gợi ý Topic khi user tạo Post; nhận feedback từ lựa chọn cuối của user
  3. **Notification Worker** — gửi notification theo event (reply, vote, badge, mention, v.v.)
  4. **Badge/Reputation Engine** — tính điểm và trao badge tự động khi đủ điều kiện
- **Key insight:** Feedback/Evaluation Loop (AI feature thứ 5) được hiện thực hóa tự nhiên trong classification flow — không cần UI riêng. User chọn/sửa topic sau AI suggestion → system log delta → training signal.
- **Implication:** 4 system actors trên cần được document trong architecture. Notification Worker và Badge Engine là background jobs (queue-based hoặc event-driven). AI workers gọi OpenAI API sync hoặc async tùy latency requirement (cần clarify Phase 6).
- **Traceability note:** Feedback loop từ user behavior (implicit feedback) là pattern phổ biến trong recommender systems — không cần user "rate AI" explicitly. Delta giữa AI suggestion và user final choice là signal chất lượng tự nhiên nhất.

**[Clarified 2026-10-19 — DEC-203: vòng phản hồi chỉ đánh giá gợi ý Topic]**

---

### QA-018
- **Issue ref:** ISS-037
- **Phase:** 2 — Actors, Roles & Permissions
- **Question:** User tự xóa tài khoản — data xử lý thế nào?
- **Answer (stakeholder — confirmed):**
  - Xóa tài khoản = soft delete, không hard delete
  - Account state machine:
    - ACTIVE → [user request delete] → DEACTIVATED (grace period: 14 ngày)
    - DEACTIVATED → [trong 14 ngày: vào trang kích hoạt + confirm email OTP] → ACTIVE
    - DEACTIVATED → [sau 14 ngày không kích hoạt] → DELETED (auto, vĩnh viễn)
    - ACTIVE → [mod warn] → ACTIVE (có flag cảnh báo)
    - ACTIVE → [admin/mod ban] → BANNED
    - BANNED → [admin unban] → ACTIVE
  - Login khi DEACTIVATED không tự kích hoạt lại — phải vào trang kích hoạt riêng + confirm email OTP
  - Profile của DEACTIVATED/DELETED user → hiển thị "người dùng không tồn tại"
  - Post của deleted account: vẫn hiển thị nội dung, author → "[Người dùng đã xóa tài khoản]"
  - Comment của deleted account: tombstone "[Bình luận từ tài khoản đã xóa]", giữ vị trí trong thread
  - Leaderboard: kỳ hiện tại giữ nhưng grayed out + nhãn "[Tài khoản đã xóa]"; kỳ tiếp loại khỏi tính toán
  - Badge: orphaned trong DB, không hiển thị khi account deleted
  - Admin/Mod không có quyền "xóa tài khoản" — chỉ warn hoặc ban
- **Implication:** USR module cần: (1) status enum trên account (ACTIVE/DEACTIVATED/DELETED/BANNED/WARNED); (2) scheduled job auto-delete sau 14 ngày DEACTIVATED; (3) reactivation flow với email OTP; (4) API filter author display theo account status.
- **Traceability note:** Grace period 14 ngày cân bằng giữa UX (cho phép đổi ý) và data hygiene (không giữ zombie accounts mãi). Email OTP để kích hoạt lại là bước xác thực quan trọng — tránh kích hoạt vô tình và đảm bảo chỉ owner tài khoản mới restore được.

**[Amended 2026-10-11 — DEC-149: bình luận của tài khoản đã xóa giữ nội dung, tác giả "[Người dùng đã xóa]"]**

---

### QA-019
- **Issue ref:** ISS-038
- **Phase:** 2 — Actors, Roles & Permissions
- **Question:** Ban user — ai có quyền, phạm vi, thời hạn, warn, AI authority, và appeal system?
- **Answer (stakeholder — confirmed):**
  - Ban/Unban: cả MOD và ADMIN, phạm vi toàn hệ thống
  - Ban có thời hạn (temporary) và vĩnh viễn (permanent) — period appeal thay đổi theo loại
  - Ban notification: email + link appeal; banned user vẫn login được, thấy màn hình thông báo + nút khiếu nại
  - AI authority: AI CÓ quyền warn trực tiếp (auto, cho borderline content); AI KHÔNG auto-ban; khi account đạt ngưỡng warn → AI escalate tạo ticket cho MOD/ADMIN review
  - Ngưỡng warn để escalate: TBD → Phase 4 ADMN backlog (ISS-ADMN-01)
  - Appeal system: build trang riêng trong hệ thống, 2 loại:
    1. Warn appeal → MOD hoặc ADMIN review
    2. Ban appeal → chỉ ADMIN review (MOD không tự review appeal của ban mình đã thực hiện)
  - Post/comment bị xóa: KHÔNG có appeal — nếu user thấy sai thì report MOD lên ADMIN
- **AI authority table confirmed:**
  - Flag content (internal): AI ✓
  - Warn account: AI ✓ (auto), MOD ✓, ADMIN ✓
  - Escalate warn threshold → ticket: AI ✓ (auto)
  - Ban/Unban: MOD ✓, ADMIN ✓; AI ✗
  - Review appeal: MOD ✓ (warn), ADMIN ✓ (warn + ban); AI ✗
  - Override AI warn: MOD ✓, ADMIN ✓
- **Implication:** ADMN module cần: appeal page (2 forms: warn/ban); ticket system cho AI escalation; ban notification email; banned user redirect flow; logic "MOD không review appeal của chính mình".
- **Traceability note:** Không cho appeal post/comment xóa giúp giữ moderation đơn giản và có thẩm quyền. Pattern "AI warns, human bans" là best practice trong content moderation — giữ human-in-the-loop cho quyết định nghiêm trọng, đồng thời tận dụng AI cho scale. Tham khảo: Discord auto-mod warns, human mod bans.

**[Amended 2026-10-15 — DEC-187, DEC-189: lần vi phạm thứ 7 thành yêu cầu ban trong hàng chờ; chỉ Admin cảnh cáo, ban Mod]**

---

### QA-020
- **Issue ref:** ISS-038 (bổ sung) + ISS-AI-01 (sketch)
- **Phase:** 2 — Actors, Roles & Permissions
- **Question:** Warn system — levels, thresholds, probation, AI confidence threshold theo warn status?
- **Answer (stakeholder — confirmed):**
  - 3 warn levels: LIGHT (count 1–2) / MEDIUM (count 3–4) / HEAVY (count 5–6)
  - Warn mới không tăng level → chỉ reset probation timer
  - Probation auto-reduce level (không cần confirm): HEAVY 14 ngày → MEDIUM; MEDIUM 10 ngày → LIGHT; LIGHT 5 ngày → Clean
  - Account bị warn vẫn hoạt động bình thường — có indicator hiển thị theo level cho người khác thấy
  - Warn level ảnh hưởng đến AI confidence threshold (user warn nhiều → AI nhạy hơn, ngưỡng thấp hơn)
  - AI threshold sketch (số cụ thể negotiate Phase 6): Clean ~85% / LIGHT ~75% / MEDIUM ~65% / HEAVY ~55%
  - Threshold phụ thuộc vào LEVEL (không phải số lần warn active)
  - MOD có thể review appeal (warn + ban), trừ action của chính mình
  - Post/comment bị xóa: không có appeal
- **Issues spawned:**
  - ISS-AI-01 (Phase 6): AI confidence threshold calibration theo OpenAI Moderation API score range
  - ISS-REWD-02 (Phase 4): Warn level ảnh hưởng đến trust/reputation display — penalty % và recovery
- **Traceability note:** Dynamic confidence threshold theo user history là pattern phổ biến trong content moderation (trust & safety systems). "Repeat offender penalty" — người đã vi phạm nhiều lần được AI giám sát chặt hơn — cân bằng giữa fairness (first-time có lợi ích nghi ngờ) và safety (repeat offender ít khoan nhượng hơn). Số cụ thể phụ thuộc vào OpenAI Moderation API score distribution — cần empirical calibration ở Phase 6.

**[Amended 2026-10-15 — DEC-186, DEC-188: một cặp ngưỡng 0,9/0,5 cho mọi người; giảm mức về số lần cao nhất của mức dưới, thử thách nối tiếp]**

---

### QA-021
- **Issue ref:** ISS-038 (correction)
- **Phase:** 2 — Actors, Roles & Permissions
- **Correction:** Appeal review permissions — MOD không review được appeal từ action của chính mình (conflict of interest → escalate lên ADMIN). ADMIN review được TẤT CẢ appeal kể cả action ADMIN tự thực hiện — vì ADMIN là cấp cao nhất, không có cấp trên để escalate.
- **Implication:** Appeal routing logic: if appeal.issued_by == current_mod → redirect to ADMIN queue. ADMIN queue nhận tất cả không lọc.

**[Clarified 2026-10-18 — DEC-196: "redirect to ADMIN queue" là quy tắc lọc, không có bước chuyển riêng]**

---

## Phase 3 — Scope Decomposition

### QA-022
- **Issue:** ISS-040
- **Phase:** 3
- **Question:** Search nên dùng semantic hay full-text? Và search được entity nào?
- **Context:** Cần xác định loại search engine và phạm vi entity cho M06.
- **Answer:** Semantic search (embedding) cho Post body/title; exact/prefix match cho User và Tag. Comment không đưa vào search (quá nhiều, ít giá trị). Fallback full-text keyword khi AI off.
- **Decision triggered:** DEC-008 (AI Feature Flag covers M06 fallback)
- **Implication:** M06 depends on M13 (AI Layer); cần vector storage — flag vào OPEN-002 để resolve ở Phase 8.

---

### QA-023
- **Issue:** ISS-041
- **Phase:** 3
- **Question:** Chat scope: chỉ DM (1-1) hay bao gồm Group Chat?
- **Context:** Real-time chat chưa được đề cập trước Phase 3.
- **Answer:** Cả hai — DM giữa 2 user và Group Chat trong Group đều in scope. → M16 Chat & Messaging (Should).
- **Decision triggered:** M16 thêm vào module registry.
- **Implication:** M16 depends on M01 (auth) và M11 (group). Real-time infrastructure sẽ được flag ở Phase 7 (NFR).
- **AMENDED Phase 5 (M16 deep dive, 2026-09-30):** "Group Chat trong Group" là scoping sai — Group Chat là conversation multi-party độc lập hoàn toàn, không liên quan Group/M11. Dependency M16→M11 đã được gỡ bỏ. Xem ISS-163 / QA-221.

---

### QA-024
- **Issue:** ISS-042
- **Phase:** 3
- **Question:** AI Layer (M13) nên là Should hay Must? Vì M06/M08/M05 đều phụ thuộc vào nó.
- **Context:** M06 cần embedding, M08 cần OpenAI Moderation API, M05 cần topic suggestion — tất cả là Must.
- **Answer:** M13 AI Layer → **Must**. Nhưng vẫn là layer riêng biệt. Global feature flag (DEC-008) đảm bảo graceful degradation khi AI off.
- **Decision triggered:** DEC-008
- **Implication:** M13 là shared infrastructure cho M05, M06, M08. Cần thiết kế AI Layer như một service độc lập từ đầu.

---

### QA-025
- **Issue:** ISS-044 (partial)
- **Phase:** 4
- **Question:** Post content: inline image hay chỉ attachment?
- **Answer:** Không hỗ trợ inline image. Tất cả media phải là attachment (file đính kèm). Inline image làm phức tạp storage và scan.
- **Decision triggered:** F-POST-06 (attachment only, no inline image)
- **Implication:** Editor không có "insert image" inline. Upload → file list bên dưới bài viết.

---

### QA-026
- **Issue:** ISS-043
- **Phase:** 4
- **Question:** OAuth provider nào? Account linking strategy?
- **Answer:** Google OAuth (Sign in with Google). Auto-link by verified email khi email Google khớp email đăng ký. Gửi notification sau link. Không manual confirmation.
- **Decision triggered:** DEC-010
- **Implication:** M01 cần Google OAuth flow + email-match auto-link logic + notification trigger.

---

### QA-027
- **Issue:** ISS-044
- **Phase:** 4
- **Question:** Soft delete — window bao lâu?
- **Answer:** 7 ngày. `deleted_at` timestamp. Cron hard-delete sau 7 ngày. User tự khôi phục trong window nếu mod chưa removed.
- **Decision triggered:** DEC-011
- **Implication:** Cần cron job + recovery endpoint + UI "Bài viết đã xóa" trong profile.

---

### QA-028
- **Issue:** ISS-044
- **Phase:** 4
- **Question:** Post status model — ai quyết định trạng thái nào?
- **Answer:** 3 trường độc lập: `publish_state` (user), `mod_state` (system/mod), `lock_level` (author hoặc mod). Author lock comments của bài mình; Mod có thể lock thêm. User "xóa" = set publish_state=deleted; Mod "gỡ" = set mod_state=removed.
- **Decision triggered:** DEC-012
- **Implication:** Schema post cần 3 field + audit trail cho mod actions.

---

### QA-029
- **Issue:** ISS-044
- **Phase:** 4
- **Question:** mod_state: 'hide' vs 'remove' khác gì?
- **Answer:** Chỉ dùng `under_review` (tạm ẩn, AI/mod đang xét) và `removed` (đã gỡ vĩnh viễn bởi mod). Không có 'hide' riêng — under_review là trạng thái ẩn tạm thời.
- **Decision triggered:** DEC-012
- **Implication:** `mod_state` enum = pending / active / under_review / removed.

---

### QA-030
- **Issue:** ISS-044
- **Phase:** 4
- **Question:** Scan policy: pre-scan hay post-scan cho bài mới?
- **Answer:** Pre-scan cho post mới (ẩn với public, `mod_state=pending`, cho đến khi AI scan xong → active hoặc under_review). Background re-scan cho edit (không ẩn, nếu flagged → under_review).
- **Decision triggered:** DEC-013
- **Implication:** New post flow: save → mod_state=pending → hidden → AI scan → active/under_review. Cần pending state visible cho author.

---

### QA-031
- **Issue:** ISS-044
- **Phase:** 4
- **Question:** Khi AI được re-enable, có retroactive scan không?
- **Answer:** Không (Option C). Chỉ scan post mới từ thời điểm AI re-enable. Không scan lại existing posts.
- **Decision triggered:** DEC-013
- **Implication:** Đơn giản hóa re-enable flow. Admin cần được thông báo rõ khi re-enable: "posts created while AI was off won't be rescanned."

---

### QA-032
- **Issue:** ISS-045
- **Phase:** 4
- **Question:** Comment nesting — bao nhiêu cấp?
- **Answer:** 1 cấp duy nhất (reply to comment). Không có reply to reply. Tiktok pattern.
- **Decision triggered:** —
- **Implication:** M04 Comment: parent_comment_id nullable; depth check = 1 level max.

---

### QA-033
- **Issue:** ISS-046
- **Phase:** 4
- **Question:** Classification — 1 hay 2 tầng? Grade level tích hợp thế nào?
- **Answer:** 2 tầng: Category → Topic. `grade_level` là field độc lập trên Post (optional, user chọn). Không cross-validate grade với Category/Topic. **[Amended 2026-10-07 — DEC-140: Topic phẳng, không 2 tầng]**
- **Decision triggered:** —
- **Implication:** Post schema: `category_id`, `topic_id`, `grade_level` (3 field riêng). AI gợi ý topic_id, user confirm. grade_level = user's explicit choice.

---

### QA-034
- **Issue:** ISS-046
- **Phase:** 4
- **Question:** grade_level trên User Profile — có tự động tăng theo năm không?
- **Answer:** Không tự động. User tự update. Hệ thống có thể gửi notification nhắc nhở đầu năm học. `grade_level` trên User và trên Post là 2 field độc lập, đều optional.
- **Decision triggered:** —
- **Implication:** User profile schema: `grade_level` ENUM('10','11','12') NULL. Notification template cho school-year reminder.

**[Amended 2026-10-13 — DEC-176: không nhắc cập nhật Lớp/Khối ở MS1]**

---

### QA-035
- **Issue:** ISS-047
- **Phase:** 4
- **Question:** Search scope — entity nào support search type nào?
- **Answer:** Post: semantic (pgvector) + FTS (tsvector). User: pg_trgm (display name substring). Group: FTS (name + description). Comment: không được search.
- **Decision triggered:** —
- **Implication:** M06 cần 3 search strategies: embedding, tsvector, pg_trgm. Không cần Elasticsearch.

---

### QA-036
- **Issue:** ISS-047
- **Phase:** 4
- **Question:** Tại sao dùng pg_trgm cho User thay vì prefix hay semantic?
- **Answer:** Vietnamese names: "Nam" không match prefix cho "Nguyễn Văn Nam". Semantic overkill cho name matching. pg_trgm handles substring match natively trong PostgreSQL.
- **Decision triggered:** —
- **Implication:** `CREATE EXTENSION pg_trgm;` trong DB schema. Index `gin(display_name gin_trgm_ops)`.

**[Clarified 2026-10-20 — DEC-209: khớp ở bất kỳ vị trí được giữ, áp cho cả Tag, Topic, Group]**

---

### QA-037
- **Issue:** ISS-047
- **Phase:** 4
- **Question:** Comment có search không? Accepted answer có embed không?
- **Answer:** Comment: FTS only (tsvector). Không semantic embed vì: upvote-based system (không có clean "accepted answer" entity đủ ổn định để embed); overhead dynamic top-N embedding không worth it. FTS đủ cho thesis scale.
- **Decision triggered:** —
- **Implication:** Comment tsvector index. Không cần comment embedding pipeline.

---

### QA-038
- **Issue:** ISS-048
- **Phase:** 4
- **Question:** Leaderboard — chu kỳ và filter như thế nào?
- **Answer:** Time windows: Weekly / Monthly / All-time (không reset score, chỉ sum upvotes trong window). Grade filter: 10 / 11 / 12 / all (all bao gồm cả users không có grade). Scope: global only (không per-group).
- **Decision triggered:** —
- **Implication:** Leaderboard query: `SUM(upvotes_received) WHERE created_at IN [window]`, optional grade filter.

---

### QA-039
- **Issue:** ISS-048
- **Phase:** 4
- **Question:** Leaderboard có per-group không?
- **Answer:** Không. Chỉ global.
- **Decision triggered:** —
- **Implication:** M12 không cần group-scoped leaderboard logic.

---

### QA-040
- **Issue:** ISS-049
- **Phase:** 4
- **Question:** Points tính theo gì? Badge loại nào?
- **Answer:** Points = tổng upvotes nhận được (thuần túy). Badges: threshold-based (ví dụ: 10 upvotes → "Người mới nổi") + periodic top-N title (ví dụ: "Ngôi sao tuần" cho top N người trong weekly leaderboard). Danh hiệu periodic reset mỗi chu kỳ.
- **Decision triggered:** —
- **Implication:** M12: `user_points` = cumulative upvotes. Badge engine: periodic cron check top-N + threshold check on each upvote event.

---

### QA-041
- **Issue:** ISS-049
- **Phase:** 4
- **Question:** "Người phát sao" là cá nhân top 1 hay top N?
- **Answer:** Top N (không chỉ 1 người). Số N chính xác sẽ được xác định khi design M12.
- **Decision triggered:** —
- **Implication:** Periodic title = top-N set, không phải winner-takes-all.

---

### QA-042
- **Issue:** ISS-050
- **Phase:** 4
- **Question:** Report categories — những loại nào?
- **Answer:** 5 categories + Khác: Spam / Nội dung không phù hợp / Sai lệch thông tin / Quấy rối / Bản quyền / Khác (free text).
- **Decision triggered:** —
- **Implication:** `report_category` ENUM với 6 values. Khác → `report_note` text field.

---

### QA-043
- **Issue:** ISS-051
- **Phase:** 4
- **Question:** Follow scope — user/topic/post/group?
- **Answer:** Follow: User (nhận noti khi họ post), Topic (nhận noti khi có post mới trong topic), Post (nhận noti mọi update/comment của post đó). Không follow Group (join/leave đã đủ semantics).
- **Decision triggered:** —
- **Implication:** `follows` table: `follower_id`, `target_type` ENUM('user','topic','post'), `target_id`. M07 Notification cần filter theo follow type.

**[Amended 2026-10-20 — DEC-215: chỉ theo dõi người dùng, Topic; bỏ theo dõi bài; chỉ theo dõi người dùng có thông báo bài mới]**

---

### QA-044
- **Issue:** ISS-052
- **Phase:** 4
- **Question:** Private group có visible khi search không? Join flow như thế nào?
- **Answer:** Visible-but-gated: user tìm thấy group, thấy tên/description, nhưng không thấy nội dung cho đến khi join. Có thể join qua invite link (direct approve) hoặc request join (cần approval từ Owner/Moderator).
- **Decision triggered:** —
- **Implication:** Group listing cần `privacy` field. Content query phải check membership. Invite link có token.

**[Amended 2026-10-20 — DEC-210: nhóm Private không hiện khi người ngoài nhóm tìm kiếm]**

---

### QA-045
- **Issue:** ISS-052
- **Phase:** 4
- **Question:** Private group có câu hỏi khi request join không?
- **Answer:** Có 1 field `join_question` (TEXT NULL) trong Group. Owner tự custom câu hỏi hoặc để null (không cần trả lời). User request join điền `answer` TEXT NULL trong join request.
- **Decision triggered:** —
- **Implication:** `groups.join_question TEXT NULL`. `group_join_requests.answer TEXT NULL`. Simple 1-field approach.

---

### QA-046
- **Issue:** ISS-053
- **Phase:** 4
- **Question:** Chat transport: WebSocket hay SSE? Pub/sub model?
- **Answer:** POST để gửi tin (đảm bảo delivery), SSE để nhận tin (server push, auto-reconnect, simpler infra). Pub/sub: in-memory `Map<chatId, Set<SSEConnection>>` (thesis scale). Không cần Redis pub/sub.
- **Decision triggered:** —
- **Implication:** M16: REST POST endpoint để gửi + SSE endpoint `/chat/:id/stream` để receive. In-memory pub/sub đủ cho 1 server instance.

---

### QA-047
- **Issue:** ISS-049 (follow-up)
- **Phase:** 4
- **Question:** Points có nên giảm theo thời gian (decay) không?
- **Answer:** Không. Points = cumulative upvotes, không decay. Time-window leaderboard (weekly/monthly) đã giải quyết bài toán freshness. Decay thêm complexity không cần thiết và counter-intuitive với user.
- **Decision triggered:** —
- **Implication:** Không cần cron job tính lại điểm. All-time score = tổng đóng góp suốt đời, dùng cho badge threshold. Leaderboard ranking dựa trên sum trong window, không phải total score.

---

## Phase 5 — M01: Authentication & Account

### QA-048
- **Issue:** ISS-054 | **Phase:** 5
- **Question:** Registration fields bắt buộc lúc đăng ký?
- **Answer:** email + password (Step 1 only). display_name + username required nhưng ở Step 3 sau verify.
- **Decision triggered:** DEC-014

### QA-049
- **Issue:** ISS-054 | **Phase:** 5
- **Question:** Email verification có bắt buộc không? Chưa verify làm được gì?
- **Answer:** Mandatory. Chưa verify → redirect Step 2 khi login. Google OAuth = đã verify, bỏ qua step này.
- **Decision triggered:** DEC-014, DEC-018

### QA-050
- **Issue:** ISS-054 | **Phase:** 5
- **Question:** Display name — nickname hay full name?
- **Answer:** Free-form. User tự chọn style — nickname, tên thật, sáng tạo tùy ý. Không unique.
- **Decision triggered:** DEC-015

### QA-051
- **Issue:** ISS-054 | **Phase:** 5
- **Question:** Có cần @username riêng ngoài display_name không?
- **Answer:** Có. Community platform cần mention, mention cần unique handle không có space. username: unique, min 3 max 20, alphanumeric+underscore.
- **Decision triggered:** DEC-015

### QA-052
- **Issue:** ISS-054 | **Phase:** 5
- **Question:** Display_name có unique không?
- **Answer:** Không. Username mới unique.
- **Decision triggered:** DEC-015

### QA-053
- **Issue:** ISS-054 | **Phase:** 5
- **Question:** Google OAuth — user có cần đặt username không?
- **Answer:** Có — Google không có username concept. display_name auto-fill từ Google (đổi được), username user tự đặt ở Step 3.
- **Decision triggered:** DEC-014

### QA-054
- **Issue:** ISS-054 | **Phase:** 5
- **Question:** Mention search — username hay display_name hay cả 2? Có support khoảng trắng trong query không?
- **Answer:** Cả 2 (pg_trgm). Spaces cho phép trong query. Trigger sau 1 char, debounce 300ms. Priority tiers theo context (Group vs Post).
- **Decision triggered:** DEC-020

**[Amended 2026-10-20 — DEC-214: khớp tên theo DEC-209 (bất kỳ vị trí, bỏ dấu, gần đúng)]**

### QA-055
- **Issue:** ISS-054 | **Phase:** 5
- **Question:** Mention render — hiện @ không? Stored như nào?
- **Answer:** Không hiện @. Chỉ display_name + brand highlight. Stored bằng user_id → auto-update nếu display_name thay đổi.
- **Decision triggered:** DEC-020

### QA-056
- **Issue:** ISS-054 | **Phase:** 5
- **Question:** Cho phép trim/edit label mention sau khi chọn không?
- **Answer:** Không. Node atomic — backspace xóa cả node. Tránh misrepresentation và complexity.
- **Decision triggered:** DEC-020

### QA-057
- **Issue:** ISS-055 | **Phase:** 5
- **Question:** Token strategy? Duration?
- **Answer:** JWT. Access token 1 giờ. Refresh token 30 ngày, rotating. refresh_tokens table trong PostgreSQL.
- **Decision triggered:** DEC-017

### QA-058
- **Issue:** ISS-055 | **Phase:** 5
- **Question:** Multi-device có làm SSE phức tạp hơn không?
- **Answer:** Không. Mỗi device = 1 SSEConnection độc lập trong Set<SSEConnection>. Pub/sub tự nhiên handle multi-device.
- **Decision triggered:** DEC-017

### QA-059
- **Issue:** ISS-056 | **Phase:** 5
- **Question:** Change password flow (biết pass cũ)?
- **Answer:** Old pass + new pass + confirm (trong Settings). Không revoke session khác — bình thường, không phải security event.
- **Decision triggered:** DEC-016

### QA-060
- **Issue:** ISS-056 | **Phase:** 5
- **Question:** Forgot password flow?
- **Answer:** Email → magic link 15 phút → nhập pass mới + confirm → revoke all other sessions → auto-login session mới.
- **Decision triggered:** DEC-016

### QA-061
- **Issue:** ISS-056 | **Phase:** 5
- **Question:** Google OAuth user nhấn "Quên mật khẩu"?
- **Answer:** Hiện thông báo "Tài khoản này đăng nhập qua Google, vui lòng dùng Google để đăng nhập".
- **Decision triggered:** DEC-016

### QA-062
- **Issue:** ISS-057 | **Phase:** 5
- **Question:** Account states đầy đủ là gì? Có state cho onboarding không?
- **Answer:** 2 fields: account_state ENUM(ACTIVE/DEACTIVATED/DELETED/BANNED) + verify_level ENUM(NONE/EMAIL_VERIFIED/SETUP_COMPLETED). Login gate check account_state trước, rồi verify_level.
- **Decision triggered:** DEC-018

### QA-063
- **Issue:** ISS-057 | **Phase:** 5
- **Question:** BANNED screen hiện gì?
- **Answer:** Lý do ban + thời gian khiếu nại còn lại (nếu còn) + nút khiếu nại (nếu còn) + nút OK.
- **Decision triggered:** DEC-019

### QA-064
- **Issue:** ISS-057 | **Phase:** 5
- **Question:** Deactivation window bao lâu? User có thể xóa thẳng không?
- **Answer:** 14 ngày window → auto-DELETED. Không có nút xóa trực tiếp — bắt buộc qua deactivate trước.
- **Decision triggered:** DEC-019

### QA-065
- **Issue:** ISS-057 | **Phase:** 5
- **Question:** Post/comment của user deactivated hiển thị như nào?
- **Answer:** Post → ẩn ("Nội dung không tồn tại"). Comment → content giữ nguyên, author name → "Tài khoản tạm thời vô hiệu hoá", avatar → placeholder.
- **Decision triggered:** DEC-019

### QA-066
- **Issue:** ISS-057 | **Phase:** 5
- **Question:** Sau khi hết 14 ngày auto-DELETED, comment hiển thị như nào?
- **Answer:** Tombstone đổi → "[Người dùng đã xóa]", PII bị wipe. Post vẫn ẩn như cũ.
- **Decision triggered:** DEC-019

---
## Phase 5 — M02: User Profile

| ID | Question | Answer |
|----|----------|--------|
| QA-067 | Profile page info? | Avatar, display_name, username, bio, points, badges, followers/following count+list, content tabs **[Amended 2026-10-13 — DEC-173: thêm Lớp/Khối, ngày tham gia]** |
| QA-068 | Content tabs owner vs visitor? | Owner: Posts+Bookmarks; Visitor: Posts only |
| QA-069 | Followers/following list hidden? | No — fully public |
| QA-070 | Username change history on profile? | No — dropped, extra table not worth v1 |
| QA-071 | Avatar CDN + types? | Cloudinary; JPEG/PNG/WebP; max 10MB; old deleted on update |
| QA-072 | Animated GIF avatar? | No — complex CDN config, not worth it |
| QA-073 | Bio char limit? | UI 155 chars, DB VARCHAR(255) |
| QA-074 | Why 155 not 255? | Product UX decision; 155 ≈ meta description sweet spot |
| QA-075 | /u/{username} — one route or two? | One route, dual-context conditional rendering |
| QA-076 | Social links? | Dropped v1 — malicious link risk + off-platform pull |
| QA-077 | Points+badges on profile? | Display only; M12 handles logic |

---
## Phase 5 — M03: Post & Content

| ID | Question | Answer |
|----|----------|--------|
| QA-078 | LaTeX support + visual editor? | LaTeX/KaTeX raw input only; visual editor future extension |
| QA-079 | Inline image in editor? | No — all media as attachments below post |
| QA-080 | Post types needed? | 1 type only; poll as optional separate table |
| QA-081 | Poll: open or closed? | Closed poll — owner defines options, users vote only |
| QA-082 | publish_state values? | DRAFT/PENDING/PUBLISHED/HIDDEN/REJECTED/DELETED |
| QA-083 | mod_state values? | NORMAL/FLAGGED/HIDDEN |
| QA-084 | lock_level — who can set? | COMMENT_LOCKED: author or mod; FULLY_LOCKED: mod only; locked_by tracks who |
| QA-085 | Pre-scan: block or flag? | Block publish — stays PENDING until mod approves |
| QA-086 | Attachment types + limits? | Images 5MB×10; Docs 20MB×3 |
| QA-087 | Avatar size updated? | Yes — 5MB (down from 10MB) for consistency with attachment images |
| QA-088 | Poll expiry required? | Yes — expires_at NOT NULL; can extend or force-close with is_closed |
| QA-089 | Poll reopen after close? | No — permanent |
| QA-090 | Edit history for comments? | edited_at only; no full history UI |
| QA-091 | Soft delete recovery? | 7-day window; author sees "Đã xóa" tab on profile; restore → PUBLISHED |

---
## Phase 5 — M04: Comment

| ID | Question | Answer |
|----|----------|--------|
| QA-092 | Comment editor scope? | Minimal: bold/italic/inline-code/LaTeX/link/@mention/blockquote |
| QA-093 | Threading depth? | 2 levels only; reply-to-child stays in same thread |
| QA-094 | Downvote on comment? | No — upvote only; report for bad content |
| QA-095 | Comment sort options? | Top/Mới nhất/Cũ nhất; child always chronological |
| QA-096 | Comment edit time limit? | No limit |
| QA-097 | Comment delete behavior? | Permanent; root tombstoned if has replies; child hard deleted |
| QA-098 | Comment attachments? | Not supported |
| QA-099 | @Mention in comment triggers notification? | Yes, always |
| QA-100 | Quote-reply support? | Yes — blockquote auto-inserted on Reply click |

---
## Phase 5 — M05: Topic & Tag

| ID | Question | Answer |
|----|----------|--------|
| QA-101 | Topic vs Tag format? | Topic = structured category; Tag = free #hashtag, no spaces |
| QA-102 | Topic taxonomy structure? | Flat, 11 topics (grouped per 2018 curriculum + non-academic) |
| QA-103 | AI suggest topic limit? | Max 3 (matches max 3 topics/post cap) |
| QA-104 | Content changed after AI suggest? | Flag is_stale, soft warning, feedback only recorded when not stale |
| QA-105 | Tag max count/length? | Max 5 tags/post, 30 chars/tag |
| QA-106 | Trending calculation? | Rolling 7-day window, score = Σ(1+upvotes×2+comments×1), recalc every 15-30min **[Amended 2026-10-07 — DEC-145]** |
| QA-107 | Topic/tag edit/delete by mod? | Topic: edit+merge, no delete. Tag: fully free, soft-delete only for crisis (name becomes reserved, non-tagifiable) **[Amended 2026-10-07 — DEC-141, DEC-143]** |
| QA-108 | Comment tags? | Not needed — comments inherit parent post's topic/tag context |

---
## Phase 5 — M06: Search

| ID | Question | Answer |
|----|----------|--------|
| QA-109 | Search scope reconfirm — does it include Topic/Group? | Yes, expanded: Post+User+Tag+Topic+Group. Original Phase 3 (QA-022) only covered Post+User+Tag |
| QA-110 | User search — pgvector or pg_trgm? | pg_trgm on display_name+username, shared with M01 @mention. pgvector reserved for Post semantic search only **[Clarified 2026-10-20 — DEC-209: kết quả tìm người dùng chỉ gồm tài khoản ACTIVE đã xong Bước 3]** |
| QA-111 | Post search trigger timing? | Submit-only (no debounce, too expensive) |
| QA-112 | Engagement weighting in ranking? | Upvotes weighted 2x vs comments 1x, consistent with trending formula |
| QA-113 | Search result filters? | Topic, Tag, date range, Following-only, Sort |
| QA-114 | Full-text fallback tech? | Postgres tsvector/tsquery + unaccent + pg_trgm |
| QA-115 | Autocomplete dropdown content? | User/Tag/Topic/Group prefix matches; no Post titles |
| QA-116 | Search history storage? | localStorage, not DB — max 10 entries |
| QA-117 | Results page layout? | Mixed single page, Post primary, others supplementary |
| QA-118 | Snippet highlighting complexity? | Semantic search has no literal keyword match to highlight reliably — skip highlighting entirely for simplicity |
| QA-119 | Guest search access? | Same as public browse **[Amended 2026-10-20 — DEC-208: Guest tìm bài bằng full-text]** |
| QA-120 | Private group in search? | Group entity (name) visible-but-gated always; group content (posts) only visible to members **[Amended 2026-10-20 — DEC-210: nhóm Private ẩn khỏi tìm kiếm với người ngoài nhóm]** |
| QA-121 | Rate limit guest vs user? | Guest stricter (30/10) than logged-in user (45/20) — accountability difference |
| QA-122 | Pagination style? | Infinite scroll preferred over page numbers; capped at 120 total results |

---
## Phase 5 — M07: Notification

| ID | Question | Answer |
|----|----------|--------|
| QA-123 | Full notification event list? | Password/deactivation/follow/post lifecycle/upvote/comment/mention/report/warning/ban/appeal/group/gamification/chat — see DEC-065 table |
| QA-124 | Which events get email? | Only: password changed, deactivation warning, ban/unban, ban-related appeal. Rest in-app only |
| QA-125 | Digest email needed? | No |
| QA-126 | Upvote notify per-vote or milestone? | Per-vote, but batched within 5-min window to avoid spam |
| QA-127 | Follow-post (subscribe/watch) feature? | Not added — bookmark stays save-only, no notify subscription **[Clarified 2026-10-20 — DEC-215: bỏ hẳn theo dõi bài viết]** |
| QA-128 | Bell UI structure? | Dropdown (recent) + dedicated /notifications page |
| QA-129 | Chat notification UI? | Separate Message icon in navbar, not mixed with bell |
| QA-130 | Email delivery timing? | Async via queue table + cron every 1 min (not blocking, not real synchronous send) |
| QA-131 | In-app delivery mechanism? | DB write (source of truth) + best-effort WebSocket push; no retry cron needed (client fetch-on-load covers gaps) [Amended: thông báo dùng SSE thay WebSocket — DEC-135/QA-257] |
| QA-132 | Granular notification preferences? | Skipped for v1 — replaced by per-post mute + chat mute (global + per-conversation) |
| QA-133 | Notification retention policy? | None — kept indefinitely, matches Facebook/Twitter/Discord/GitHub practice |

---
## Phase 5 — M08: Moderation

| ID | Question | Answer |
|----|----------|--------|
| QA-134 | Report reasons same across entities? | No — tailored per entity (Post 8, Comment 7, User 2, Group 4) |
| QA-135 | Can guest report? | No, login required |
| QA-136 | Evidence upload for report? | Max 3 images, 5MB each; description optional except for "Khác" |
| QA-137 | Report outcome — who sees what? | Reporter: vague outcome only. Offender: detailed reason + punishment + appeal link |
| QA-138 | Multiple mods — how to divide report queue? | Claim-based lock system, 30-min auto-release on inactivity |
| QA-139 | Priority calc when case has mixed reasons? | MAX severity among reasons in case, not sum |
| QA-140 | Duplicate reports on same content? | Grouped into 1 case while open; each report keeps own data; resolved case's new reports open fresh case |
| QA-141 | Does comment need AI scan like post? | Yes but different mechanism — post-scan triggered by reply velocity, not pre-scan block |
| QA-142 | Scan scope on velocity trigger? | Whole thread (root+replies) not yet scanned with current content |
| QA-143 | Does edit alone re-trigger comment scan? | No — needs both edit AND next velocity trigger together |
| QA-144 | Can AI auto-issue warnings? | Yes, when confidence high; low confidence escalates to mod. AI never bans |
| QA-145 | LIGHT warning restrictions? | None — just a tracking/probation window |
| QA-146 | Warning status visibility? | Fully private — user + mod only, never public |
| QA-147 | Ban duration determination? | Escalation formula: 30d→90d→permanent based on ban count, or manual permanent override |
| QA-148 | Who can view moderation logs? | Admin: all. Mod: own actions, plus cross-mod visibility only when reviewing appeals |
| QA-149 | How to detect malicious/false reporting? | target_concentration metric (same-target dismissed report ratio) over rolling 90-day window, mod judgment only |

---
## Phase 5 — M09: Appeal

| ID | Question | Answer |
|----|----------|--------|
| QA-150 | What does an appeal submission contain? | Required message + optional evidence (max 3 images/5MB), same as report system |
| QA-151 | How does a banned user reach the appeal page? | Still logs in normally; sees locked "banned" screen with appeal button; all other endpoints blocked |
| QA-152 | Does ban email link directly to appeal? | Yes, protected route /appeal, redirects through login if needed |
| QA-153 | Appeal deadline for warning vs ban? | Warning: full probation period. Temp ban: full ban duration. Permanent ban: 90 days flat |
| QA-154 | Why not unlimited appeal window for permanent ban? | Practical concern — old cases years later lose context, mod turnover, no clean resolution path |
| QA-155 | Can the same action be appealed multiple times? | No — exactly once, rejected appeals are final for that action |
| QA-156 | Appeal queue shared with report queue? | No, separate — different assignment rule (exclude mod's own actions) |
| QA-157 | Appeal priority ordering? | Ban appeals prioritized over warning appeals, FIFO within tier |
| QA-158 | What happens when mod's own action is up for appeal? | Automatically hidden from their queue; if sole mod, escalates to admin |
| QA-159 | What happens on appeal approval? | Ban: immediate ACTIVE + log marked overturned. Warning: restriction lifted + warn count decremented |

---
## Phase 5 — M10: Admin Panel

| ID | Question | Answer |
|----|----------|--------|
| QA-160 | What's admin-exclusive vs shared with mod? | Admin: role mgmt/config/full-audit/mod-mgmt. Shared: moderation actions, topic/tag mgmt **[Amended 2026-10-07 — DEC-141: quản lý Topic chỉ Admin]** |
| QA-161 | Should policy constants be admin-configurable? | No — hardcoded, changed via deployment |
| QA-162 | Can admin promote any user to mod freely? | Yes, no eligibility conditions, but user can decline the proposal |
| QA-163 | Does demote need mod's consent? | No — direct, immediate, no appeal (not a punishment) |
| QA-164 | What system configs does admin panel need? | AI toggle, maintenance mode, registration toggle, feature flags, announcement banner |
| QA-165 | AI toggle — single switch or per-module? | Both — master toggle + granular per-module (search/moderation/topic) |
| QA-166 | Are admin's own actions logged? | Yes, append-only, viewable but not editable even by admin |

---
## Phase 5 — M13: AI Layer

| ID | Question | Answer |
|----|----------|--------|
| QA-167 | Which embedding model? | text-embedding-3-small (OpenAI, cheap, multilingual) |
| QA-168 | Where are embeddings stored? | pgvector, posts.embedding vector(1536), HNSW index |
| QA-169 | Which model for topic suggestion? | GPT-4o-mini |
| QA-170 | Does Moderation API cover all report reasons? | No — only harassment/hate/sexual/violence; spam/plagiarism/misinformation are manual-report-only |
| QA-171 | Does AI auto-reject content, not just flag? | Yes — score≥0.9 triggers auto-reject (post)/auto-hide (comment), skipping mod entirely |
| QA-172 | Same threshold for content gate and warning? | Yes, symmetric — both use 0.9/0.5 thresholds |
| QA-173 | Are thresholds final? | No — placeholder, needs tuning with real usage data |
| QA-174 | Admin-off vs transient AI failure — same handling? | No — admin-off uses defined module fallbacks; transient failure is per-request degradation with retry |
| QA-175 | Timeout duration for AI calls? | Fast APIs (moderation/embedding) 5s; LLM generation (topic) 10s |
| QA-176 | Retry behavior on AI failure? | Exactly 1 retry, sequential, 2s delay before retry |
| QA-177 | Failed pre-scan — auto-publish or hold? | Hold for mod review (safer than auto-publish) |
| QA-178 | Is there a dedicated AI rate limit system? | No — reuses existing search limits; only new limit is 10/min/user for Topic Suggest button |

---
## Phase 5 — M11: Group

| ID | Question | Answer |
|----|----------|--------|
| QA-179 | ISS-130: Group creation — ai tạo được, giới hạn gì? | Mọi user đã login tạo group tự do; rate limit 5 group/ngày/user (chống spam); không giới hạn tổng số group sở hữu |
| QA-180 | ISS-131: Role permissions matrix (Owner/Group Mod/Member)? | Owner full quyền (kick Mod/Member, promote/demote Mod, đổi setting, xóa group); Group Mod duyệt pre-mod queue, ẩn/xóa post-comment, kick Member (KHÔNG kick Mod khác/không promote); Member chỉ đăng bài/comment/vote |
| QA-181 | ISS-132: Join flow — public/private, join question xử lý sao? | Public+no-question=join ngay; mọi case khác (có question, hoặc private)=cần duyệt Owner/Mod theo câu trả lời. Reject xong cho gửi lại ngay (không cooldown, theo pattern Facebook/LinkedIn/Discord); Owner/Mod dùng block riêng cho case spam request |
| QA-182 | ISS-133: Group content moderation quan hệ với M08 system-wide thế nào? | System Mod/Admin vẫn giám sát toàn bộ qua Report (M08) + can intervene anytime (không bypass); AI scan/Group Mod queue chỉ là publishing gate bổ sung. Score≥0.9→auto-reject; 0.5-0.9→bắt buộc Group Mod/Owner xử lý (dù pre-mod ON/OFF); <0.5→theo toggle pre-mod. Group có queue "chờ duyệt publish" riêng, tách Report queue, cùng cơ chế claim-based 30 phút |
| QA-183 | ISS-134: Group deletion (Owner xóa) và member rời group: nội dung xử lý sao? | Xóa group: soft-delete (nội dung ẩn khỏi mọi user kể cả ex-member, không hard-delete DB); reputation tổng giữ nguyên; NGOẠI LỆ: point từ upvote content đã mất theo group bị trừ. Member rời/bị kick: post cũ giữ nguyên (tài sản group), tác giả hiện tên thật, point không đổi; kick = rời tự nguyện |
| QA-184 | ISS-136: Group size limit — số group tối đa 1 user tham gia/sở hữu? | Không giới hạn — join bao nhiêu group cũng được, làm Owner bao nhiêu group cũng được |
| QA-185 | ISS-137: Owner rời/mất khả năng thao tác: group chuyển quyền sở hữu thế nào? | Owner rời tự nguyện: bắt buộc chỉ định successor trước (blocking action); group chỉ còn 1 member (chính Owner) rời → group bị xóa. Owner bị block/deactivate/xóa (involuntary): tự động promote Group Mod active senior nhất → nếu không có Mod thì Member senior nhất → nếu chỉ còn Owner thì xóa group |
| QA-186 | ISS-138: Đổi visibility Public↔Private: post cũ trên main feed xử lý sao? | Đổi visibility bất kỳ lúc nào (Owner). Post đã hiện với user nào rồi thì giữ hiện (không rút lại) nhưng khóa tương tác nếu chuyển Private; feed/search query MỚI loại post này khỏi kết quả cho user không phải member |
| QA-187 | ISS-139: Group Mod/Owner xóa post (pre-mod) có qua Appeal (M09) không? | Không — hành động moderation cấp group không có cơ chế appeal, quyết định Group Mod/Owner là cuối cùng (khác hành động system Mod/Admin, vẫn qua M09 bình thường) |
| QA-188 | ISS-140: Private group: có hiện trong search/discovery không? Ai được invite? | Ẩn hoàn toàn khỏi search/discovery, chỉ vào được qua invite/link. Bất kỳ member nào (Member/Mod/Owner) đều invite được, không giới hạn riêng cho Mod/Owner. Join flow dùng lại cơ chế đã chốt ở ISS-132 (không có entity Invitation riêng) |
| QA-189 | ISS-141: Post trong group có cross-post ra main feed không? | Post luôn hiện trong feed của member group (Public/Private). Riêng Public group: post CÒN hiện như post thường trên main feed (visible non-member). Private group: không bao giờ lộ ra main feed |
| QA-190 | ISS-135: Anonymous posting trong group — cơ chế cụ thể? | Khi toggle bật: user tự chọn ẩn danh hoặc không cho từng post (opt-in per-post, không bắt buộc toàn bộ). Khi Owner tắt toggle: post đã đăng ẩn danh trước đó VẪN giữ ẩn danh (không bị de-anonymize retroactively). Group Mod/Owner thấy được real identity của anonymous author (giống pattern system-wide MOD/ADMIN, DEC-004/005) |

---
## Phase 5 — M09 Amendment + M12: Gamification (QA-191 → QA-193)

| ID | Question | Answer |
|----|----------|--------|
| QA-191 | ISS-142: Content-tied point deduction — trường hợp nào trừ, thời điểm nào? | Nguyên tắc trực tiếp/gián tiếp: trừ điểm CHỈ khi content mất đi do hành động trực tiếp của chính chủ (tự xóa post/comment của mình) hoặc do chính content đó bị Mod/Admin xóa vì vi phạm. KHÔNG trừ nếu content mất đi gián tiếp do hành động của người khác (group bị Owner xóa dù mình chỉ là Member; comment bị cascade-ẩn vì post cha bị xóa — dù post cha bị xóa vì lý do gì). Thời điểm trừ: tự xóa → trừ SAU KHI hết cửa sổ soft-delete 7 ngày (hard-delete xong) — nếu khôi phục trong 7 ngày thì chưa từng bị trừ, không cần cơ chế hoàn riêng; Mod/Admin xóa do vi phạm → trừ NGAY lập tức. Quyết định này thay thế ngoại lệ group trong DEC-105 (group deletion trước đây có trừ điểm, nay bỏ ngoại lệ đó — điểm được bảo toàn hoàn toàn khi group bị xóa) |
| QA-192 | ISS-143: Badge nên permanent hay revocable? Audit trail ra sao? | Permanent — không thu hồi badge dù điểm sau đó giảm xuống dưới ngưỡng (kể cả do case trừ điểm hợp lệ ở QA-191). Lý do: badge là cột mốc lịch sử đã đạt được (giống Stack Overflow/Duolingo), không phải chỉ số theo dõi liên tục; tránh phạt user vì lý do ngoài tầm kiểm soát; đơn giản hơn khi build (không cần logic recheck-revoke). Badge UI hiển thị kèm ngày đạt được thay vì chỉ số ngưỡng, tránh gây hiểu lầm khi điểm hiện tại thấp hơn ngưỡng. Audit: badge theo ngưỡng (permanent, 1 lần đạt) → 1 bản ghi audit (ngày đạt đầu tiên); danh hiệu periodic top-N (VD "Ngôi sao tuần", reset mỗi chu kỳ) → nhiều bản ghi audit (mỗi chu kỳ thắng là 1 sự kiện riêng) |
| QA-193 | ISS-144: Có nên mở appeal cho content bị xóa do vi phạm không? Phạm vi, deadline, cơ chế, outcome thế nào? | Có — amend lại quyết định Phase 2 (trước đây Appeal chỉ có Warning+Ban, KHÔNG có content deletion). Tiền lệ tham khảo: Reddit phân biệt admin-removal (có appeal chính thức, cửa sổ 6 tháng) vs subreddit-mod-removal (không có appeal chính thức cấp platform — khớp với DEC-109 Group-level moderation không đổi); YouTube: content removal appeal trong 1 năm, strike 6 tháng. Vì iShare quy mô nhỏ hơn nhiều, chọn deadline ngắn hơn: 30 ngày cố định. Phạm vi: CHỈ Post, KHÔNG áp dụng Comment (post là tài sản quan trọng hơn; comment volume cao dễ quá tải queue; nhất quán với Post Star ≠ Comment Star DEC-004 coi post có giá trị cao hơn). Cơ chế: queue riêng "Content Deletion Appeal" (tách khỏi Report và Warning/Ban Appeal), nhưng tái dùng cơ chế claim-based 30 phút đã có. Priority: thấp nhất trong 3 loại appeal (Ban > Warning > Content Deletion). Outcome khi thành công: (1) khôi phục content, (2) hoàn point đã trừ, (3) đảo ngược warn/ban đi kèm lần xóa đó nếu có — tái dùng đúng cơ chế outcome reversal đã có ở ISS-117 (warn: gỡ restriction + giảm warn_count; ban: unban ngay, log giữ overturned flag). Comment bị xóa do vi phạm: point bị trừ vẫn vĩnh viễn, không có đường khiếu nại |

## Phase 5 — M12: Gamification Deep Dive (QA-194 → QA-207)

| ID | Question | Answer |
|----|----------|--------|
| QA-194 | ISS-REWD-01: Badge dựa trên tiêu chí gì — chỉ điểm, hay thêm số bài/chủ đề? | Chỉ dựa trên tổng điểm (points). Không có badge theo số bài đăng hay theo chủ đề ở v1 |
| QA-195 | ISS-REWD-01: Danh sách badge cụ thể — bao nhiêu mốc, ngưỡng, tên gọi? | 5 mốc: Người mới nổi (25đ) / Cây bút triển vọng (100đ) / Cây bút tích cực (300đ) / Chuyên gia cộng đồng (600đ) / Huyền thoại iShare (1000đ). Ngưỡng đầu chỉnh khó hơn theo yêu cầu stakeholder (từ đề xuất ban đầu 10/50/150/400/1000) |
| QA-196 | ISS-145: Post Star vs Comment Star — trọng số cụ thể? | Post Star = 2, Comment Star = 1 |
| QA-197 | ISS-146: Periodic top-N title gắn chu kỳ nào, N bao nhiêu? | Chỉ Weekly ("Ngôi sao tuần"), N=3 |
| QA-198 | ISS-152: Hòa điểm ở đúng hạng cắt N=3 thì xử lý sao? | Cho tất cả user hòa ở hạng cắt đều nhận title (N là số tối thiểu, có thể vượt lên nếu hòa), không cần tie-break riêng |
| QA-199 | ISS-REWD-02: Warn level có ảnh hưởng hiển thị leaderboard/reputation không? | Có — nhưng chỉ HEAVY: ẩn hoàn toàn khỏi leaderboard công khai trong suốt thời gian probation. Đây là exception có chủ đích, amend DEC-079 (private scope gốc chỉ nói posts/comments/profile, nay thêm leaderboard eligibility là ngoại lệ công khai duy nhất). MEDIUM/LIGHT không bị ảnh hưởng |
| QA-200 | ISS-147: Upvote rút lại được không? Điểm xử lý ra sao? | Có — vote là toggle (bấm lại để hủy). Điểm người nhận trừ ngay lập tức khi rút, đối xứng với lúc cộng |
| QA-201 | ISS-148: Tự vote nội dung của chính mình có được phép không? | Không — hệ thống ẩn/disable nút vote trên chính content của tác giả, chặn gian lận từ gốc |
| QA-202 | ISS-153: Có cho xem lại leaderboard đầy đủ của các chu kỳ trước không? | Không — chỉ hiển thị trạng thái hiện tại của Weekly/Monthly/All-time (không lưu snapshot lịch sử). Lịch sử "từng đạt danh hiệu gì" vẫn giữ qua title/badge audit trail (DEC-114) |
| QA-203 | ISS-149: Leaderboard ranking tính real-time hay batch/cache định kỳ? | Batch — gộp thành 1 cron job duy nhất, chạy mỗi 60 phút. Job này vừa refresh ranking hiển thị (cho xem tạm), vừa kiểm tra "có chu kỳ nào vừa đóng chưa" — nếu có, tính lại ranking cuối cùng bằng query chính xác theo đúng mốc thời gian chu kỳ (không dùng số liệu cache), rồi award title + gửi notification. Trễ tối đa 60 phút so với giờ đóng chu kỳ thực, nhưng người thắng luôn đúng |
| QA-204 | ISS-154: Tài khoản bị BAN — có ẩn khỏi leaderboard không? Profile/post/comment còn hiển thị cho người khác không? | Ẩn khỏi leaderboard trong suốt thời gian bị ban (nhất quán với HEAVY warn, mở rộng DEC-118). Nhưng profile/post/comment vẫn hiển thị bình thường cho người khác (không tombstone, không ẩn) — vì Ban khác Delete: có thể unban qua appeal, và nội dung vi phạm cụ thể đã được xử lý riêng qua M08 Report/Moderation, không liên quan đến việc khóa tài khoản |
| QA-205 | ISS-154 (bổ sung): Nhãn "tài khoản bị khóa" hiển thị ở đâu? | Ở MỌI nơi tên tác giả xuất hiện — trang profile, và cạnh tên tác giả trên từng bài post/comment họ từng đăng. Nhãn: "Tài khoản đã bị khóa" (khác với "Tài khoản tạm thời vô hiệu hoá" dùng cho Deactivate — DEC-019). Khác nguyên tắc private tuyệt đối của Warn (DEC-079) — Ban là mức phạt nặng hơn, mang tính công khai |
| QA-206 | ISS-150: Hai user bằng điểm nhau trên leaderboard thì xếp hạng thế nào? | Đồng hạng — cả hai cùng hiển thị chung 1 thứ hạng, người tiếp theo nhảy số hạng (giống xếp hạng thể thao/Olympic). Không cần tie-break riêng, nhất quán với nguyên tắc đã chốt ở ISS-152 |
| QA-207 | ISS-151: Badge chưa đạt có hiển thị tiến độ (VD "150/300 điểm") không? | Không — chỉ hiện badge sau khi đã đạt được, không hiện thanh tiến độ trước đó |

---

## Phase 5 — M16: Chat & Messaging (QA-208 → QA-224)

| ID | Question | Answer |
|----|----------|--------|
| QA-208 | ISS-155: Trạng thái tin nhắn có cần lưu field/enum riêng trên message không? | Không — "đã xem" không phải thuộc tính của riêng tin nhắn mà là quan hệ giữa tin nhắn và người đọc, suy ra bằng cách so `id`/`created_at` của tin với mốc đọc gần nhất của người nhận. 2 trạng thái hiển thị ở tầng UI (computed, không lưu DB): "Đã gửi" (mặc định) và "Đã xem" (chỉ hiện ở tin nhắn cuối cùng trong conversation, không rải theo từng tin lịch sử) |
| QA-209 | ISS-155: Mốc đọc ("last read") lưu ở đâu, dùng timestamp hay message id? | Lưu `last_read_message_id` (FK tới `messages.id`, không dùng timestamp để tránh lệch đồng hồ client/server) trên bảng `conversation_members` (1 dòng/user/conversation) — dùng chung cho cả DM và Group chat. Update qua `UPDATE ... SET last_read_message_id = GREATEST(last_read_message_id, :new_id)` để chống trường hợp request đến lệch thứ tự làm lùi mốc đã đọc. Không cần bảng riêng lưu "đã đọc tin nào" theo từng dòng tin/user (sẽ phình theo N tin × M thành viên) |
| QA-210 | ISS-155: Trigger nào cập nhật mốc đã đọc khi có tin nhắn mới tới lúc đang mở sẵn conversation? | Kết hợp 2 điều kiện qua client: (1) tab/window đang focus — dùng Page Visibility API (`document.hidden`), nếu tab ẩn thì đợi tới khi `visibilitychange` bắn lại mới tính; (2) đang ở đáy danh sách tin nhắn — dùng `IntersectionObserver` trên 1 sentinel ở cuối danh sách, nếu đang cuộn đọc tin cũ thì tin mới KHÔNG tự cuộn xuống, chỉ hiện badge "tin nhắn mới", đợi user tự cuộn xuống chạm đáy mới mark-as-read. Khi cả 2 điều kiện đúng, debounce ~500ms–1s trước khi gọi API mark-as-read (tránh gọi dồn dập khi tin đến liên tục) |
| QA-211 | ISS-155: Group chat "đã xem" hiển thị kiểu nào — avatar từng người (Messenger) hay ẩn hoàn toàn chỉ dùng nội bộ (Slack)? | Chọn kiểu Messenger — hiện avatar của (các) thành viên đã đọc kịp **tin nhắn mới nhất** ngay dưới tin đó (nhiều người cùng mốc thì gộp avatar). Thành viên nào chưa đọc kịp tin mới nhất thì không hiện avatar ở đâu cả (không rải theo lịch sử, chỉ áp dụng cho tin cuối cùng — nhất quán với QA-208). Cách này loại bỏ luôn nhu cầu xử lý case "mốc đọc trỏ tới tin chưa được load/phân trang", vì tin mới nhất luôn có sẵn ngay khi mở conversation. DM dùng chung 1 cơ chế (chỉ là trường hợp đặc biệt 1 avatar duy nhất) |
| QA-212 | ISS-155: Khi 1 người bấm đã đọc, những người còn lại trong conversation có cần được báo real-time không? Cơ chế nào? | Có, bắt buộc — nếu không thì avatar "đã xem" phía người khác không tự cập nhật (phải F5 mới thấy). Tái dùng hạ tầng SSE + pub/sub `Map<chatId, Set<SSEConnection>>` đã có sẵn cho tin nhắn (QA-046) — không mở kết nối riêng. Server sau khi update `last_read_message_id` thành công sẽ broadcast 1 event kiểu mới (`event: read_receipt`, data `{user_id, last_read_message_id}`) tới các connection khác đang subscribe conversation đó; không cần debounce thêm ở server vì tần suất đã được kiểm soát từ debounce phía client (QA-210) |
| QA-213 | ISS-158: Tin nhắn có cho phép sửa nội dung sau khi gửi không? | Không — không cho sửa tin nhắn dưới bất kỳ hình thức nào sau khi đã gửi |
| QA-214 | ISS-158: Tin nhắn có cho xóa không? Nếu có, soft-delete (tombstone) hay hard-delete? | Cho xóa — chọn soft-delete kiểu tombstone: nội dung gốc bị xóa hẳn (không giữ lại kể cả cho mod xem lại, vì chat là kênh riêng tư, không thuộc phạm vi moderation như Post/Comment), thay bằng placeholder "Tin nhắn đã bị thu hồi" giữ nguyên vị trí trong luồng chat — nhất quán UX với Messenger/Zalo mà học sinh đã quen dùng, tránh hụt ngữ cảnh hội thoại so với hard-delete không dấu vết |
| QA-215 | ISS-158: Thu hồi tin nhắn áp dụng cho 1 phía hay cả 2 phía? Có cần thêm kiểu "xóa chỉ mình tôi thấy" riêng không? | Chỉ 1 kiểu xóa duy nhất — thu hồi luôn cho CẢ 2 phía cùng lúc. Không có thêm tùy chọn "xóa chỉ ở phía tôi" tách biệt, giữ scope đơn giản cho MS1 |
| QA-216 | ISS-158: Giới hạn thời gian cho phép thu hồi tin nhắn là bao lâu? | 5 phút kể từ lúc gửi (`now() - created_at <= 5 minutes`) — đủ để xử lý tình huống phổ biến nhất (gửi nhầm người/nội dung, phát hiện gần như ngay lập tức), đồng thời đủ ngắn để tránh phá vỡ mạch hội thoại khi tin đã được đọc/phản hồi. Sau 5 phút, tin nhắn không còn cách nào xóa/ẩn được nữa — vĩnh viễn |
| QA-217 | ISS-159: Tin nhắn hỗ trợ nội dung gì — text only, hay thêm emoji/đính kèm ảnh-file? | Text + emoji cho MS1. Đính kèm ảnh/file: ngoài phạm vi MS1, để mở rộng ở phase sau. Không có AI Moderation quét nội dung chat (khác Post/Comment) vì chat là kênh riêng tư |
| QA-218 | ISS-160: Không có AI Moderation, chat cũng không nằm trong Report system (M08) — vậy harassment/quấy rối qua DM xử lý thế nào? | Sau khi cân nhắc trade-off giữa Report-only (chỉ xử lý được sau, không ngăn tin nhắn tiếp tục trong lúc chờ mod) và Block (kiểm soát tức thời nhưng phát sinh câu hỏi scope: level nào, ảnh hưởng content/leaderboard/group chat hay không) — quyết định: KHÔNG làm Block, KHÔNG làm Report cho tin nhắn ở MS1. Đánh dấu OPEN-003, để lại xử lý ở phase sau |
| QA-219 | ISS-161: Rate limiting cho chat — có cần không, mức nào? | Có — 30 tin nhắn/phút theo từng cặp (người gửi, conversation). Mục đích khác Search (không phải giới hạn chi phí AI — chat không gọi AI) mà để chặn spam/bot flood, bảo vệ server, và là lớp chặn kỹ thuật tối thiểu bù cho việc chưa có Block/Report (OPEN-003). Chọn per-conversation (không phải global) để chặn đúng trọng tâm (1 người spam 1 target cụ thể) mà không cản trở họ nhắn ở chat khác. 30 tin/phút nhanh hơn tốc độ gõ người thật, không ảnh hưởng use case hợp lệ |
| QA-220 | ISS-162: Ai nhắn tin (DM) được cho ai — mở hoàn toàn, cần mutual follow, hay message request kiểu Messenger? | Mở hoàn toàn — bất kỳ user nào cũng nhắn DM được cho bất kỳ user nào khác, không cần follow, không có cơ chế message request riêng. Làm rộng thêm bề mặt rủi ro đã ghi ở OPEN-003, nhưng đã có rate limit (QA-219) làm lớp chặn tối thiểu |
| QA-221 | ISS-163: Group Chat có phải kênh gắn liền với Group (M11) không? | Không — correction so với QA-023 (Phase 3 scoping ban đầu ghi nhầm "Group Chat within Group"). Group Chat là loại conversation multi-party (3+ người) hoàn toàn độc lập, ai cũng tạo được, không liên quan gì tới việc có chung Group/cộng đồng nào hay không. Đã cập nhật module-registry.md: bỏ dependency M16→M11 |
| QA-222 | ISS-164: Group Chat — quản trị ra sao (role, add/remove, kiểm duyệt, đổi tên, rời nhóm, kế nhiệm Admin, giới hạn size)? | Follow: mở, giống DM (QA-220). Role: Admin (người tạo) + Member. Add: cả 2 role đều add được. Remove: chỉ Admin xóa được thành viên, Member không xóa được ai. Kiểm duyệt: Admin bật/tắt toggle; bật thì thêm thành viên mới cần Admin duyệt (không phải Member). Đổi tên nhóm: mọi thành viên. Rời nhóm: tự do, tách biệt hoàn toàn với bị Admin xóa. Admin rời: bắt buộc chủ động chuyển quyền cho người khác trước (không có auto-promote hệ thống như Owner ở Group M11/QA-185). Giới hạn: 100 thành viên/Group Chat — đủ cho use case thực tế (nhóm lớp, CLB, nhóm ôn thi) mà không biến Group Chat thành kênh broadcast giả |
| QA-223 | ISS-165: Tin nhắn mới có gửi email notification không? | Không — chỉ in-app, khớp mặc định đã chốt ở QA-124 (email chỉ dành cho password/deactivation/ban/appeal), không thêm ngoại lệ riêng cho chat |
| QA-224 | ISS-165: Pagination lịch sử chat — cơ chế và số lượng/lần load? | Infinite scroll (cuộn lên trên để load tin cũ hơn), 20 tin/lần, cursor-based theo `message_id` (nhất quán pattern Search QA-097). Khác Search: KHÔNG có giới hạn tổng số tin tối đa — user phải cuộn được tới tận tin nhắn đầu tiên của conversation, không có khái niệm "hết mức độ liên quan" như kết quả search |

## Phase 5 — M14: Feed & Discovery (QA-225 → QA-240)

| ID | Question | Answer |
|----|----------|--------|
| QA-225 | ISS-168: M14 Feed có những tab/view nào? | 3 tab ban đầu: Trending (sub Post/Topic/Tag) + Following (chronological, theo Follow M07) + Newest (chronological toàn site). Không có tab "For You" thuật toán cá nhân hóa riêng. (Sau đó mở rộng thành 4 tab — xem QA-229) |
| QA-226 | ISS-185: Trending Post dùng công thức/decay nào? | Trending Topic/Tag giữ nguyên DEC-052 (rolling 7-day hard window, không decay). Trending Post dùng công thức mới — DEC-124: exponential half-life decay, `weight=0.5^(age_days/7)`, cắt hẳn về 0 sau 28 ngày (4 tuần). Lý do chọn 4 tuần: bội số sạch của half-life 7 ngày (4 nửa chu kỳ → còn 6.25%, gần như không đáng kể), nhất quán thuật ngữ "theo tuần" dùng xuyên suốt hệ thống, tránh số lẻ như 1 tháng (30/7≈4.29) |
| QA-227 | ISS-166: Guest (chưa đăng nhập) xem được gì trong Feed? | Guest xem đầy đủ Newest + Trending (cả 3 sub, không giới hạn riêng sub nào vì Trending Topic/Tag còn công khai hơn cả Post). Tab Following/Group vẫn hiện nhưng bấm vào yêu cầu đăng nhập. Mọi tương tác (upvote, report, bookmark, follow...) đều cần login — nhất quán QA-011 (permission matrix Guest, Phase 2: INTR=Không, Report=Không). Mặc định guest vào tab Trending |
| QA-228 | ISS-169: Tab Following rỗng (user chưa follow ai/gì) hiện gì? | Empty state + CTA dẫn sang trang Search (tìm theo User/Topic/Post) — Search đúng phạm vi 3 loại follow target (M07), trong khi Trending có cả sub Tag (không phải đối tượng follow được) nên dẫn sang đó sẽ lạc đề |
| QA-229 | ISS-187: Có nên thêm tab Group (feed tổng hợp từ group đã join) không? | Có — thêm tab thứ 4 "Group", tổng hợp bài từ mọi group (Public+Private) mà user đã join, hiển thị chronological (khác với việc vào từng group riêng lẻ đã có sẵn ở M11/DEC-111) |
| QA-230 | ISS-188: Tab Group hiện/ẩn theo điều kiện nào? | Luôn hiện cho user đã login (nhất quán cách xử lý Following, QA-228); Guest thấy tab nhưng gate giống Following (QA-227). Chưa join group nào → empty state + CTA "Khám phá Group" (dẫn sang trang danh sách/tìm Group) |
| QA-231 | ISS-172: Trending Post có cần filter theo Topic không? | Không — chỉ 1 danh sách global duy nhất. Đã có Trending Topic riêng (1 trong 3 sub) để xem theo chủ đề, filter thêm trong Trending Post sẽ dư thừa |
| QA-232 | ISS-173: Bài Group Public cross-post (DEC-111) có tính vào Newest/Trending Post không? | Ban đầu: Có, tính vào cả 2. **AMENDED ngay trong cùng phiên — xem QA-233**: loại khỏi Newest, vẫn giữ trong Trending Post |
| QA-233 | ISS-173 (amend QA-232): phạm vi chính xác? | Group Public cross-post vẫn tính vào Trending Post (và tất nhiên vào tab Group) nhưng **loại khỏi Newest** — lý do: Trending xếp hạng theo độ hot nên gộp mọi nguồn hợp lý, còn Newest là "dòng thời gian nội dung chung của site" nên giữ thuần không-thuộc-group |
| QA-234 | ISS-174: Cơ chế phân trang cho cả 4 tab? | Infinite scroll, cursor-based (theo post_id/created_at tùy tab), 20 bài/lần load — nhất quán pattern đã dùng cho Chat (QA-224). Note kỹ thuật: cần SSR cho batch đầu để đảm bảo SEO crawlability cho nội dung Guest xem được (Newest/Trending) — lý do Guest được xem post/comment từ đầu là vì SEO/discoverability (QA-011) **[Amended: phần SSR hoãn ở MS1 — xem QA-256/DEC-134, OPEN-006]** |
| QA-235 | ISS-175: Có ngưỡng tối thiểu (min upvote/comment) để vào Trending không? | Không đặt ngưỡng cho MS1 — dataset demo nhỏ (~70 bài, 30 user), đặt ngưỡng dễ khiến Trending trống/gần trống lúc demo. Provisional — có thể bổ sung ngưỡng sau khi dataset đủ lớn, cần revisit |
| QA-236 | ISS-176: Trending có loại bài của user BANNED/HEAVY warn không? | Không loại, không chỉnh score. Theo đúng precedent đã chốt ở DEC-118/DEC-122 (M12): ngoại lệ ẩn khỏi khu vực công khai CHỈ áp dụng riêng cho Leaderboard, còn lại (profile/post/comment, và nay thêm Trending) vẫn hiển thị bình thường. BANNED tự có label công khai "Tài khoản đã bị khóa" (QA-205) hiện cả trên Trending nếu bài lọt vào — đủ giải quyết vấn đề minh bạch mà không cần rule loại trừ riêng. HEAVY warn giữ private tuyệt đối (DEC-079), không hiện gì đặc biệt, nhất quán khắp nơi khác |
| QA-237 | ISS-177: Feed có tự cập nhật real-time khi có bài mới không? | Không auto-insert nội dung. Newest/Following/Group dùng banner "có bài mới" (polling định kỳ ~30-60s), bấm vào chỉ fetch phần mới rồi prepend lên đầu — giữ nguyên vị trí cuộn hiện tại, không reload toàn bộ. Trending không cần banner — tự refresh theo đúng chu kỳ tính lại decay (15-30 phút, DEC-052/124) |
| QA-238 | ISS-177 (bổ sung): banner reload có mất vị trí cuộn không? | Không — bấm banner chỉ fetch đúng phần bài mới (so với cursor cuối cùng) rồi chèn thêm vào đầu, không reload lại toàn bộ, không ép về đầu trang. Vị trí đang đọc ở dưới (nếu có) giữ nguyên |
| QA-239 | ISS-177 (amend): banner nên polling hay real-time (SSE)? | Giữ polling, không chuyển sang real-time cho MS1. Lý do: khác Chat (pub/sub theo đúng 1 chatId, biết chính xác ai cần nhận), Following/Group cần lọc cá nhân hóa theo từng connection (follow/membership của từng user) mới biết có nên đẩy tín hiệu không — phức tạp hơn hẳn broadcast đơn thuần, chưa đáng effort cho module Could-priority ở MS1 |
| QA-240 | ISS-186: M14 có còn phụ thuộc M13 (AI Layer) không? | Bỏ dependency M13 khỏi M14 cho scope hiện tại — chỉ còn phụ thuộc M03 (Post), M05 (Topic/Tag). Lý do: dependency gốc đặt ra từ lúc còn tab "For You" cá nhân hóa AI, nay đã bỏ (xem QA-225). Không bỏ vĩnh viễn — có thể tái thêm M13 nếu mở rộng tính năng cá nhân hóa AI sau MS1 |

## Phase 5 — M15: Analytics & Stats (QA-241 → QA-247)

| ID | Question | Answer |
|----|----------|--------|
| QA-241 | ISS-178: M15 Analytics & Stats — ai truy cập được, ADMIN-only hay có mở cho MOD? | Chỉ ADMIN truy cập được cả 3 dashboard. Đã cân nhắc phương án mở thêm cho MOD xem Moderation Stats (lọc riêng theo hoạt động của MOD đó) kèm ý tưởng bổ sung bảng xếp hạng Top-N MOD xử lý nhiều report nhất — nhưng việc lọc số liệu cá nhân hóa theo từng MOD làm tăng độ phức tạp đáng kể so với query tổng toàn hệ thống, trong khi đây là module Could-priority. Quyết định cuối: giữ đơn giản, chỉ ADMIN xem, bỏ hẳn ý tưởng Top-N MOD |
| QA-242 | ISS-179: User Stats dashboard gồm những chỉ số nào? | Tổng user theo trạng thái tài khoản (ACTIVE/DEACTIVATED/BANNED) · trend đăng ký mới theo thời gian (biểu đồ) · phân bố theo vai trò (USER/MOD/ADMIN) · phân bố theo Lớp/Khối (grade_level, F-POST-09) · phân bố theo mức warn (Clean/LIGHT/MEDIUM/HEAVY/BANNED). Tất cả derive từ dữ liệu sẵn có (bảng user + warn level), không cần tracking infra mới như DAU/WAU/MAU (yêu cầu activity-log riêng — bị loại vì tốn thêm effort không cần thiết cho MS1, trong khi tổng user theo mốc thời gian đã đủ thông tin cho mục đích demo/báo cáo) |
| QA-243 | ISS-180: Content Stats dashboard gồm những chỉ số nào? | Tổng Post theo publish_state · breakdown theo mod_state (pending/active/under_review/removed) · trend bài đăng mới theo thời gian · phân bố Post theo Topic · trend Comment mới theo thời gian. Đã cân nhắc thêm tỉ lệ Group-post/độc lập và tỉ lệ bài ẩn danh nhưng loại bỏ — không cần thiết, thêm nhiễu cho dashboard mà không phục vụ mục đích vận hành rõ ràng **[Amended 2026-10-19 — DEC-203: thêm "tỷ lệ Topic gợi ý được giữ lại"]** |
| QA-244 | ISS-181: Moderation Stats dashboard gồm những chỉ số nào? | Tổng Report theo trạng thái (pending/resolved/dismissed...) + theo category (5 category + Khác, ISS-050) · Warn issued theo level theo thời gian · Ban/Unban theo thời gian · Appeal theo loại + outcome. Chọn phương án "thêm được nhiều thì càng tốt" (mọi chỉ số đều derive free từ dữ liệu Report/Warn/Ban/Appeal đã có ở M08/M09) thay vì phương án tối giản chỉ đếm tổng Report |
| QA-245 | ISS-182: Filter thời gian cho cả 3 dashboard — custom range hay preset? | Preset cố định: Hôm nay / 7 ngày / 30 ngày / Toàn thời gian (all-time). Không có custom date range picker cho MS1 — đơn giản hóa UI và truy vấn |
| QA-246 | ISS-183: Cách tính toán — real-time query hay batch/cache? | Real-time — query trực tiếp mỗi lần admin load dashboard (COUNT/GROUP BY đơn giản theo preset thời gian), không cache/batch. Khác Leaderboard (M12, cần batch vì ranking + tie-break phức tạp, DEC-123), lượng truy cập admin vào Analytics thấp hơn nhiều so với traffic user thông thường nên real-time query không tạo áp lực đáng kể lên hệ thống |
| QA-247 | ISS-184: Có export dữ liệu (CSV) không? | Không làm cho MS1. Đánh dấu **OPEN-004** (để ngỏ xem xét lại sau khi các module core hoàn thiện), theo đúng pattern đã dùng cho OPEN-003 — đây là quyết định defer có chủ đích, không phải unknown bỏ sót |

## Phase 6 — Cross-cutting Concerns (QA-248 → QA-255)

| ID | Question | Answer |
|----|----------|--------|
| QA-248 | ISS-189: Timezone & date handling — lưu trữ/tính toán theo múi giờ nào? | Lưu timestamp dạng UTC trong DB (chuẩn phổ biến). Mọi tính toán ranh giới ngày/tuần (reset leaderboard weekly M12, deadline appeal 30 ngày M09, probation warn 5/10/15 ngày M08, preset Hôm nay/7 ngày/30 ngày M15, soft-delete window 7 ngày M03...) và hiển thị trên UI đều quy về **Asia/Ho_Chi_Minh (UTC+7)** — cố định, không có DST vì Việt Nam không đổi giờ mùa hè. Lý do chọn: 100% target user là học sinh VN, không cần multi-timezone, và việc cố định offset +7 không phát sinh edge case kỹ thuật nào |
| QA-249 | ISS-190: i18n/localisation — site có cần hỗ trợ ngôn ngữ nào ngoài tiếng Việt không? | Vietnamese-only ở MS1 (không có language switcher), nhưng tổ chức theo kiến trúc i18n-ready — string UI externalize qua i18n key (thư viện kiểu i18next), chỉ có 1 locale `vi` active. Lý do: dễ mở rộng sau mà không cần refactor lại toàn bộ UI string. Lưu ý quan trọng: i18n UI chỉ dịch được phần "chrome" (nhãn, nút, thông báo hệ thống) — KHÔNG dịch được nội dung do user tạo ra (post/comment vẫn mãi ở ngôn ngữ writer viết). Việc hỗ trợ nội dung đa ngôn ngữ (dịch/tag content theo ngôn ngữ) là 1 tính năng hoàn toàn khác, ngoài scope draft gốc — ghi nhận là ý tưởng mở, không build ở MS1 |
| QA-250 | ISS-191: Data retention tổng quát — audit log và chat message có cần policy xóa/lưu trữ gì không? | Giữ vĩnh viễn, không hard-delete/archive — nhất quán với Notification (DEC-071: "no retention policy"). Research xác nhận: log/audit data thường không bị xóa trong thực tế (vì mục đích compliance/minh bạch/trace), khác bản chất với content user có thể chủ động xóa. Thêm lý do kỹ thuật: nhiều bảng khác tham chiếu tới audit log/message (FK — report trỏ message_id, warn trỏ report...), hard-delete dễ phá referential integrity. Nguyên tắc tổng quát rút ra áp dụng cho mọi quyết định hard-delete từ đây về sau: **chỉ hard-delete khi thật sự an toàn** (có lý do rõ ràng — privacy/PII cần xóa, hoặc dọn rác content do chính user chủ động xóa có UX hợp lý — VÀ không phá referential integrity với bảng khác tham chiếu). Các quyết định hard-delete đã chốt trước đó (Post 7 ngày DEC-011, Comment permanent DEC-038, Account PII wipe DEC-019) đều thỏa nguyên tắc này nên không đổi gì |
| QA-251 | ISS-192: File/media upload — có cần cơ chế scan virus/malware không? | Không — chỉ giữ whitelist type/size đã có (ảnh JPEG/PNG/WebP, giới hạn size theo từng feature: avatar 5MB, report evidence 5MB/file). Dựa vào CDN (Cloudinary) tự re-encode/transcode ảnh khi upload — quá trình này tự nhiên loại bỏ payload độc hại ẩn trong file ảnh, đủ an toàn cho scope chỉ-cho-upload-ảnh (không file thực thi) ở MS1 |
| QA-252 | ISS-193: AI — nội dung user gửi ra OpenAI (3rd party) có cần xử lý gì về privacy không? | Có — thêm 1 trang Privacy Policy/ToS công khai, nêu rõ nội dung đăng công khai (post/comment) được xử lý bởi dịch vụ AI bên thứ 3 (OpenAI Moderation API + Embedding) cho mục đích kiểm duyệt và tìm kiếm ngữ nghĩa. Link hiện ở footer và/hoặc registration flow. Lý do: chi phí gần như bằng 0 (chỉ 1 trang nội dung tĩnh) nhưng tăng minh bạch đáng kể, đặc biệt quan trọng vì đối tượng user là học sinh (có thể vị thành niên) |
| QA-253 | ISS-194: AI — Topic Suggestion (GPT-4o-mini) trả về ngoài danh sách 11 topic hợp lệ thì xử lý sao? | Validate output theo whitelist 11 topic cố định của hệ thống; nếu AI trả về topic không khớp → coi như suggestion fail, hiển thị non-blocking error ("Không thể gợi ý chủ đề lúc này, vui lòng chọn thủ công") và để user tự chọn thủ công. Dùng CHUNG đúng 1 UX pattern với case AI transient-failure đã chốt ở DEC-099 (timeout/retry hết hạn) — dù nguyên nhân kỹ thuật khác nhau (timeout vs hallucination), người dùng không cần phân biệt, trải nghiệm giống hệt nhau |
| QA-254 | ISS-195: AI — có cần lưu log raw output (score Moderation, Topic suggestion) để audit/debug không? | Có — mỗi lần gọi AI (Moderation API, Embedding, Topic Suggestion) lưu raw response vào bảng `ai_decision_log` riêng, gắn với post/comment liên quan (khác với audit log hành động admin/mod đã có ở DEC-081/094 — đây là log quyết định do chính AI đưa ra). Phục vụ 2 mục đích: (1) debug/tinh chỉnh threshold 0.9/0.5 hiện là placeholder (DEC-098) bằng dữ liệu thật thay vì đoán, (2) làm cơ sở xử lý Content Deletion Appeal (M09/DEC-115) khi user khiếu nại bị AI xử oan — mod/admin cần xem lại được "tại sao AI quyết định vậy" |
| QA-255 | ISS-196: Analytics events — có cần hạ tầng event-tracking chung (ngoài 3 dashboard M15) không? | Không xây cho MS1 — formalize lại quyết định đã ngầm chọn lúc deep-dive M15 (QA-242: từ chối DAU/WAU/MAU vì cần activity-log/event-tracking riêng), áp dụng thành nguyên tắc chung cho toàn hệ thống thay vì chỉ riêng M15, tránh việc module khác sau này tự ý thêm event-tracking rải rác không nhất quán. Đánh dấu **OPEN-005** — để ngỏ xem xét lại sau khi các module core hoàn thiện, theo đúng pattern của OPEN-003/OPEN-004 (quyết định defer có chủ đích, không phải unknown bỏ sót) |

## Phase 7 prep — Tech Stack (OPEN-002)

| ID | Question | Answer |
|----|----------|--------|
| QA-256 | ISS-197: Tech stack — Backend/Frontend framework, và có cần SSR/SEO ở MS1 không? | Backend: Java + Spring Boot. Frontend: ReactJS. Stakeholder làm rõ: "chỉ cần đảm bảo core, MS1 chưa cần SEO, SSR gì cả". Đã giải thích: SSR (server dựng sẵn HTML, khác SSE = server đẩy realtime); Next.js là React framework có SSR sẵn nhưng team chưa dùng; React thuần + thư viện không có SSR sẵn. Kết luận: React + Vite chạy phía trình duyệt, không SSR ở MS1; SEO/SSR ghi thành OPEN-006 (xem lại trước deploy thật). Hệ quả đã nêu: Google index kém tin cậy hơn, preview khi dán link vào Zalo/Facebook không có. Để dễ chuyển Next.js về sau: tách lớp gọi API, giữ component thiên về hiển thị (hướng làm, không cam kết chi phí). UI Kit dùng chung cho toàn app, làm sau khi có design: stakeholder xác nhận chỉ dùng trong application (nội bộ, không phải sản phẩm nộp riêng, không thêm module/scope); phải tuân thủ i18n key (DEC-128) và timezone hiển thị (DEC-127). Yêu cầu cốt lõi: có một bộ common UI thống nhất dùng trong app; được phép xây trên thư viện nền có sẵn (stakeholder: tự viết hay dùng nền đều được, quan trọng là có bộ common UI). Chọn thư viện nền: chắc chắn đợi có design; hiện stakeholder nghiêng về MUI (xu hướng, chưa chốt) → ghi **OPEN-007**. |
| QA-257 | ISS-198: Kênh realtime — thống nhất SSE hay giữ WebSocket cho thông báo? | Stakeholder nghiêng về SSE và hỏi app có cần giao tiếp hai chiều không. Đã rà register: chat = POST gửi + SSE nhận (đã xem cũng qua POST + SSE, QA-212); thông báo chỉ server→client; feed banner = polling (QA-239); AI = request/response; leaderboard = cron (QA-203); không có typing indicator/presence/collab. Stakeholder đề xuất online/offline bằng FE ping định kỳ (heartbeat) rồi quyết định bỏ qua — không đưa vào yêu cầu. Kết luận: dùng SSE cho cả chat và thông báo, bỏ WebSocket; QA-131 và các ghi chú WebSocket liên quan được amend. Lưu ý: pub/sub in-memory (không Redis) chỉ chạy 1 instance — đã chấp nhận ở scale demo (ghi lại ở Phase 7). |
| QA-258 | ISS-199: Email — thư viện và nguồn SMTP gửi mail? | Stakeholder đề xuất Spring Mail. Đã giải thích SMTP (giao thức gửi mail; app giao thư cho máy chủ SMTP) và tách 2 lớp: code gửi (Spring Mail) vs nguồn SMTP phía sau (chỉ là host/port/user/password trong config). Chọn phương án A: Spring Mail + SMTP của nhà cung cấp có gói miễn phí; nhà cụ thể chọn khi triển khai, không ảnh hưởng spec. Gmail SMTP chỉ dùng ở dev. Xác thực tên miền gửi (SPF/DKIM) cần khi chạy thật, chưa cần cho demo 20–30 người. |
| QA-259 | ISS-200: Cờ `AI_ENABLED` lưu ở đâu? | Assistant đưa phương án A (env var) / B (DB + admin UI) / C — nhưng stakeholder chỉ ra đã chốt từ đầu có màn hình admin cấu hình các mục này. Kiểm tra lại: đúng — DEC-092 (System config list: AI toggle, maintenance, registration, feature flags, banner) và DEC-093 (AI master + per-module) đã chốt trong M10. Phân biệt: QA-161 chỉ nói *hằng số chính sách* (ngưỡng, thời hạn) không chỉnh được qua UI, khác với *system config toggle*. Kết luận: không có quyết định mới, cờ AI nằm trong Admin Panel (lưu bền trong DB). |
| QA-260 | ISS-201: Hosting / deployment ở MS1? | Stakeholder xác nhận: "ở MS1 ta chưa cần deploy gì cả". Nhất quán QA-002 (DoD: dev complete + demo-ready, deploy không bắt buộc). Hosting = N/A ở MS1; nhà cung cấp và cách đóng gói (Docker chỉ là ý tưởng, chưa chốt) để khi cần deploy thật. Không có quyết định mới. |
| QA-261 | ISS-202 (đóng ISS-029): Có ràng buộc học thuật nào về công nghệ không? | Stakeholder: không có yêu cầu gì, tự do khi implement code. Bổ sung: đồ án rất nặng về "design system" (hiểu là thiết kế hệ thống — chưa xác nhận, không phải UI Kit) — từ thiết kế DB, models tới luồng đi qua từng class, phản hồi như thế nào..., nặng nghiệp vụ nên phần đó cần làm cực kỳ kỹ. Cập nhật QA-010: không có ràng buộc công nghệ; kỳ vọng chiều sâu thiết kế/nghiệp vụ cao. Không có quyết định mới về công nghệ. |
| QA-262 | Phase 8 (Data model) — cách tiếp cận và độ sâu? | Stakeholder chọn đi từng module (không gộp một lượt), sau đó tổng hợp thành hệ thống. Quy trình: (1) trích xuất danh từ → đối tượng (entity) và thuộc tính cho từng module; (2) tổng hợp thành sơ đồ thực thể (ERD) toàn hệ thống; (3) tiếp theo là thiết kế database (giai đoạn thiết kế, sau BA), rồi các bước sau. Lý do: đồ án nặng về thiết kế hệ thống/nghiệp vụ nên cần kỹ (QA-261). Áp dụng khi vào Phase 8. |
| QA-263 | ISS-203: Xác nhận nhóm công nghệ ngầm định? | Stakeholder: "xác nhận tất, và sau này có cần thêm gì ta sẽ bàn sau". Xác nhận PostgreSQL + pgvector, Cloudinary, OpenAI (Moderation / text-embedding-3-small / GPT-4o-mini), Tiptap/ProseMirror (JSON), JWT. Đóng OPEN-002. |

## System Requirement prep — Privacy & Consent

| ID | Question | Answer |
|----|----------|--------|
| QA-264 | ISS-204: Có yêu cầu đồng ý Privacy Policy/ToS khi đăng ký không, và privacy xây dựng thế nào? | Stakeholder: "yêu cầu đồng ý chắc chắn phải có mới register được"; "ta sẽ xây dựng privacy sau nhưng chắc chắn phải có privacy". Assistant nêu các chỗ chưa có trong register: danh mục dữ liệu cá nhân, quyền của người dùng (xem/tải/xóa dữ liệu), xử lý học sinh dưới 18 tuổi, cơ sở pháp lý, và câu hỏi DEC-129 (giữ chat và log vĩnh viễn) so với việc xóa sạch PII khi xóa tài khoản. Tất cả để sau, ghi OPEN-008. |

## System Requirement prep — Documentation approach

| ID | Question | Answer |
|----|----------|--------|
| QA-265 | ISS-205: Cách viết tài liệu SR theo module? | Stakeholder cung cấp tài liệu mẫu (cấu trúc mục 1–6, mỗi chức năng gồm yêu cầu cấp trên / lý do / yêu cầu cấp dưới) và chốt: mỗi module một tài liệu, tự chứa thuật ngữ và quyền; tiếng Việt (giữ tiếng Anh cho thuật ngữ bắt buộc); văn phong chuyên nghiệp dễ hiểu; viết SR ngay ở phase này, Phase 7/8 làm sau; một hành vi chỉ ở một module sở hữu, module khác tham chiếu bằng ID (điểm 4A); Nguồn/Basis ở phụ lục truy vết, thân tài liệu sạch (điểm 6B); milestone/ưu tiên ghi một lần ở mục 5.1, chỉ gắn nhãn ngoại lệ, bỏ bảng áp dụng kiểu automotive (điểm 10B); mục 4.1 chỉ ghi luật/tiêu chuẩn do stakeholder nêu, nếu không có thì 'Không có'; phần đầu có mã tài liệu, dự án, module, trạng thái, phiên bản, ngày, tác giả Phạm Văn Đức, bỏ mục người duyệt; lưu ở .agents/.claude/system_analysis/output/specs/ (báo cáo audit ở specs/audit/); hai agent Author (viết) và Auditor (chỉ kiểm tra, không sửa; kiểm độ bao quát bằng ma trận nguồn–yêu cầu và checklist quy tắc), Author sửa theo báo cáo, tối đa 2 vòng rồi đưa stakeholder quyết; mọi GAP/mơ hồ/đề xuất raise cho stakeholder từng việc; câu trả lời ghi vào register (QA/DEC) và Author phải sửa/bổ sung vào SR; chạy thử một module trước (đề xuất M05); HMI Requirements và Screen Transitions để placeholder đến khi có design. Ghi nhận: quyết định này khác hai quy tắc trong BA-INTERVIEW-RULES (output tiếng Anh; chỉ sinh spec sau Phase 9). |
| QA-266 | ISS-206: Quy ước ID cho tài liệu SR? | Stakeholder chốt tạm: tiền tố dự án `ISH`; tài liệu `ISH-SR-Mxx`; yêu cầu cấp trên `ISH-Mxx-nnn`, cấp dưới `ISH-Mxx-nnn.k`; điểm mở `OP-Mxx-nn` (tạm thời, chỉ ở Phụ lục B); phát hiện audit `AUD-Mxx-nn`; mục nguồn dùng lại ID ISS/QA/DEC/OPEN; ID vĩnh viễn (không đánh số lại/dùng lại, cho phép khoảng trống); số mục 5.x không phải ID. Kèm yêu cầu: xây skill Author và sửa các file trong .agent-instructions liên quan, sau đó stakeholder review |

---

## Functional Requirement — M05: Topic & Tag (QA-267 → QA-291)

| ID | Question | Answer |
|----|----------|--------|
| QA-267 | ISS-207: AI Classification có gợi ý Tag không? | Xác nhận: AI không gợi ý Tag, chỉ gợi ý Topic (giữ QA-017) |
| QA-268 | ISS-208: Có bước Mod duyệt kết quả gợi ý Topic không? | Xác nhận: không có bước Mod duyệt; tác giả tự chỉnh rồi đăng (giữ DEC-050) |
| QA-269 | ISS-209: Topic phẳng hay 2 tầng? | Xác nhận: Topic phẳng, không chia 2 tầng (giữ DEC-047, thay QA-033) |
| QA-270 | ISS-210: Cho thêm Topic mới? | Chỉ Admin được thêm; tên Topic không được trùng; AI phải gợi ý dựa trên toàn bộ danh mục Topic hiện tại; bài cũ không tự gán Topic mới; không đặt giới hạn số Topic. Gộp Topic cũng chỉ Admin. Admin được xóa Topic khi Topic chưa có bài nào. Xóa mềm Tag khi khủng hoảng vẫn cho cả Mod và Admin |
| QA-271 | ISS-211: Đổi công thức Trending Topic/Tag thế nào? | Xét dữ liệu tương tác trên cửa sổ 7 ngày, không chỉ bài đăng trong cửa sổ; giữ 7 ngày, không decay; thêm bookmark trọng số 1 (bài mới 1, upvote 2, comment 1); tương tác đã rút lại không tính; bài nhiều Topic/Tag góp cho tất cả; chưa thêm lượt xem ở MS1. Trending Post có thêm bookmark không: để review ở M14, tạo OPEN, hướng đang chấp nhận là thêm |
| QA-272 | ISS-212: Có giữ quyền đổi tên Topic không? | "confirm không hỗ trợ đổi tên!" — sửa tên bằng cách thêm Topic mới rồi gộp Topic cũ vào |
| QA-273 | ISS-213: Tác giả có đổi Topic, Tag khi sửa bài đã gửi không? | "có, tác giả, mod và admin đều có thể đổi" |
| QA-274 | ISS-214: Mod/Admin có đổi Topic, Tag trên bài người khác không? | Có (trả lời cùng QA-273) |
| QA-275 | ISS-215: "Browse" có gồm trang bài theo Topic/Tag không? | Không: M05 chỉ có danh sách Topic/Tag; xem bài theo Topic/Tag qua bộ lọc của M06 |
| QA-276 | ISS-216: Có kích hoạt lại Tag đã vô hiệu hóa không? | "hoàn toàn mod/admin có thể active lại tag này" |
| QA-277 | ISS-217: Bài nháp có bắt buộc 1–3 Topic không? | A: chỉ bắt buộc khi gửi; nháp được có 0 Topic (vẫn tối đa 3 Topic, 5 Tag) |
| QA-278 | ISS-218: So trùng tên Topic thế nào? | Đồng ý: không phân biệt hoa/thường, bỏ khoảng trắng thừa (đầu, cuối, giữa); khác dấu là khác tên |
| QA-279 | ISS-219: "Topic chưa có bài" đếm những bài nào? | "có lẽ chỉ cần bỏ qua bài nháp" — đếm mọi bài không phải nháp (kể cả đã xóa còn trong 7 ngày khôi phục); bài nháp mất Topic đó khi Topic bị xóa |
| QA-280 | ISS-220: Sau khi gộp, Topic nguồn và người follow ra sao? | Topic nguồn tự bị xóa; người follow Topic nguồn tự chuyển sang Topic đích. Kèm: khi xóa Topic, các lượt follow Topic đó bị bỏ |
| QA-281 | ISS-221: Ngưỡng 20 từ đếm thế nào? | A: giữ 20 từ, đếm trên tiêu đề cộng nội dung chữ; mỗi cụm ký tự cách nhau bởi khoảng trắng là một từ |
| QA-282 | ISS-222: AI trả về một phần Topic ngoài danh mục? | Đồng ý: bỏ Topic sai, giữ Topic hợp lệ; chỉ thất bại khi không còn Topic hợp lệ |
| QA-283 | ISS-223: 10 lần/phút tính theo cửa sổ nào? | Đồng ý: 60 giây gần nhất |
| QA-284 | ISS-224: Tag gồm ký tự nào, hiển thị thế nào, "#" có tính không? | Chữ cái (kể cả có dấu), chữ số, "_"; có ít nhất một chữ cái (#12 không hợp lệ); không thêm ký tự khác. Hiển thị chung theo tên chuẩn hóa chữ thường. "#" không tính vào 30 ký tự, chỉ để hiển thị |
| QA-285 | ISS-225: Trending tính trên bài và tương tác nào? | A: chỉ bài đang hiển thị trên feed chính (đã đăng, không bị Mod ẩn; gồm nhóm Public, không gồm nhóm Private); upvote chỉ cho bài; comment gồm reply; bài không còn hiển thị không đóng góp |
| QA-286 | ISS-226: Mốc kiểm chứng cho chu kỳ 15–30 phút? | A: mọi tương tác có mặt trong điểm Trending chậm nhất 30 phút; không hạ mốc |
| QA-287 | ISS-227: Mục điểm 0 và thứ tự khi bằng điểm? | Chỉ hiện mục có điểm > 0. Bằng điểm → số bài mới (đăng trong cửa sổ 7 ngày) nhiều hơn xếp trước → tên A–Z. "vì tên không trùng nên chắc chắn không thể cùng hạng" |
| QA-288 | ISS-228: Dùng gợi ý Topic khi sửa bài? | A: tác giả dùng được, cùng quy tắc và có ghi phản hồi; Mod/Admin sửa bài người khác không dùng gợi ý |
| QA-289 | ISS-229: Mod/Admin đổi Topic, Tag bài người khác có thông báo, có ghi lịch sử sửa không? | "không thông báo, cũng không cần ghi vào lịch sử sửa bài" |
| QA-290 | ISS-230: Ghi nhật ký thao tác Tag/Topic của Mod? | A: "ghi log là được" — ghi vào nhật ký kiểm duyệt |
| QA-291 | ISS-231: Công bố việc gửi nội dung cho AI gợi ý Topic? | "Có" — bổ sung vào trang Chính sách quyền riêng tư |

---

## Functional Requirement — M01: Authentication & Account (QA-292 → QA-308)

| ID | Question | Answer |
|----|----------|--------|
| QA-292 | ISS-232: Có thông báo sau khi tự liên kết Google không, qua kênh nào? | A: giữ thông báo, gửi trong ứng dụng và email, cùng nhóm bảo mật với đổi mật khẩu |
| QA-293 | ISS-233: Bình luận của tài khoản DELETED hiển thị thế nào? | A: giữ nội dung, tên tác giả "[Người dùng đã xóa]", avatar mặc định |
| QA-294 | ISS-234: Mod/Admin có xem được bài bị ẩn và danh tính thật của tác giả đã vô hiệu hóa không? | A: có, trong khi tài khoản ở DEACTIVATED (theo lý do của QA-015); người dùng thường thấy như cũ |
| QA-295 | ISS-235: Quy tắc mật khẩu? | Tối thiểu 8, tối đa 64 ký tự; không bắt buộc loại ký tự; nhận mọi ký tự kể cả khoảng trắng, chữ có dấu, không tự cắt khoảng trắng; "rõ ràng khi đổi/đặt lại mật khẩu, nó phải khác với mật khẩu hiện tại". Không chặn mật khẩu phổ biến, không so với email/username |
| QA-296 | ISS-236: username có dấu? phân biệt hoa thường? giới hạn display_name? | username "chỉ alphabet (a-z, A-Z, 0-9 và _)", không dấu; so trùng không phân biệt hoa thường, hiển thị giữ nguyên chữ hoa thường người dùng gõ. display_name 1–50 ký tự, "không nhận emoji, chỉ text", chấp nhận dấu; gồm chữ cái, chữ số, khoảng trắng và . , - _ ' ( ) |
| QA-297 | ISS-237: Email Google trùng tài khoản email chưa xác minh thì sao? | "hành động y hệt như vậy đi, gộp và chuyển email thành đã xác minh" (chấp nhận rủi ro người khác đăng ký trước bằng email của mình) |
| QA-298 | ISS-238: Hạn 30 ngày của phiên làm mới? | Tính lại 30 ngày từ mỗi lần làm mới (ok cả nhóm) |
| QA-299 | ISS-239: 14 ngày tính thế nào? | Đủ 14 × 24 giờ từ lúc vô hiệu hóa (ok cả nhóm) |
| QA-300 | ISS-240: Mã kích hoạt lại? | Trang kích hoạt chỉ nhập email; mã 6 chữ số, hạn 15 phút, sai tối đa 5 lần thì mã mất hiệu lực, xin lại cách ít nhất 60 giây; kích hoạt xong "tự động đăng nhập luôn" |
| QA-301 | ISS-241: Danh sách gợi ý và thông báo nhắc tên? | Trong cùng tầng xếp theo mức khớp; bình luận dùng ngữ cảnh bài chứa nó; không hiện DEACTIVATED, DELETED, chưa xong bước 3, và "BANNED cũng sẽ không xuất hiện trong mention"; lượt nhắc cũ tới DEACTIVATED/DELETED hiện tên thay thế "và click vào sẽ không dẫn hướng sang trang cá nhân đó"; thông báo gửi khi nội dung hiển thị công khai, sửa nội dung chỉ báo người mới được nhắc |
| QA-302 | ISS-242: Email cảnh báo xóa; thông báo khi đặt lại mật khẩu? | Email cảnh báo gửi một lần, 24 giờ trước khi tự xóa; đặt lại mật khẩu cũng gửi "mật khẩu đã đổi" trong ứng dụng và email (ok cả nhóm) |
| QA-303 | ISS-243: Công tắc tạm dừng đăng ký, chế độ bảo trì? | Tạm dừng đăng ký chặn cả tạo tài khoản Google lần đầu, liên kết Google vào tài khoản có sẵn vẫn được; tài khoản đã qua bước 1 làm tiếp bước 2, 3; bảo trì: chỉ ADMIN đăng nhập, phiên của người khác không dùng được (ok cả nhóm) |
| QA-304 | ISS-244: Ban tạm thời hết hạn? | Tự về ACTIVE ngay lúc hết hạn (ok cả nhóm) |
| QA-305 | ISS-245: Đổi tên; dùng lại email, username của tài khoản DELETED? | Đổi được cả hai ở trang sửa hồ sơ, không giới hạn số lần; username cũ được giải phóng khi đổi. Tài khoản DELETED: "email cho dùng lại, và username sẽ bị khoá vĩnh viễn" |
| QA-306 | ISS-246: Magic link dùng mấy lần? | Một lần; gửi link mới thì link cũ mất hiệu lực (ok cả nhóm) |
| QA-307 | ISS-247: Nút OK trên màn hình bị khóa? | Đăng xuất (ok cả nhóm) |
| QA-308 | ISS-248: "Quên mật khẩu" với email lạ, tài khoản không ACTIVE? | Mọi yêu cầu (kể cả email không thuộc tài khoản nào) hiện cùng một câu: "Liên kết đã được gửi, vui lòng kiểm tra email của bạn". DEACTIVATED: không gửi link, hướng tới trang kích hoạt. Đổi mật khẩu, đổi thông tin chỉ khi tài khoản ACTIVE; riêng BANNED: "BAN thì cho đặt mật khẩu nhé, vì cần khiếu nại mà!" — đặt lại chỉ để đăng nhập vào màn hình tài khoản bị khóa và gửi khiếu nại |
| QA-309 | ISS-249: Danh mục dữ liệu cá nhân? Trình bày trên trang thế nào? | Stakeholder giao assistant đề xuất ("phải nhờ bạn vì tôi chẳng rõ"). Trang không liệt kê chi tiết; gộp tài khoản và hồ sơ thành một nhóm; không nêu phiên đăng nhập. Bốn nhóm: thông tin tài khoản và hồ sơ (kể cả dữ liệu nhận từ Google khi đăng nhập Google); nội dung bạn tạo; dữ liệu giữ an toàn cộng đồng; dữ liệu được xử lý bởi AI. Danh mục chi tiết giữ trong tài liệu nội bộ (FR) |
| QA-310 | ISS-250: Có lưu việc đồng ý không? Khi nào phải đồng ý lại? | Lưu thời điểm và phiên bản đã đồng ý; "chỉ khi thay đổi policy mới cần đồng ý thêm" — hỏi lại ở lần đăng nhập kế tiếp sau khi chính sách đổi phiên bản |
| QA-311 | ISS-251: Khi DELETED xóa gì, giữ gì? | "bạn cứ đề xuất sao cho hệ thống hoạt động được" — chấp nhận đề xuất: xóa email, mật khẩu, liên kết Google, display_name, avatar, bio, Lớp/Khối, phiên đăng nhập, bookmark, quan hệ theo dõi, bản ghi đồng ý; giữ username (khóa vĩnh viễn), trạng thái, vai trò, bài viết ở trạng thái ẩn, bình luận với tên "[Người dùng đã xóa]", upvote đã cho (không còn biết ai cho) |
| QA-312 | ISS-252: Tin nhắn và nhật ký của người đã xóa tài khoản? | "okey" — A: giữ nội dung, người gửi hiện "[Người dùng đã xóa]"; nhật ký kiểm duyệt và nhật ký AI vẫn gắn với tài khoản đã xóa qua username để Mod, Admin tra cứu; trang chính sách nêu việc giữ lại vì an toàn cộng đồng |
| QA-313 | ISS-253: Nêu xử lý bởi AI thế nào? | "không nên nói xử lý bởi AI bên thứ ba" → "write theo kiểu xử lý bởi nhà cung cấp dịch vụ AI" (không nêu tên nhà cung cấp). Các dịch vụ bên ngoài khác (đăng nhập, lưu ảnh, gửi email) nêu chung một mục, không liệt kê tên; cam kết không bán dữ liệu |
| QA-314 | ISS-254: Cơ sở xử lý và các mục của trang? | Chấp nhận đề xuất: cơ sở là sự đồng ý khi đăng ký và khi chính sách đổi; dữ liệu giữ lại sau khi xóa tài khoản dựa trên mục đích an toàn cộng đồng. Trang gồm: dữ liệu thu thập, mục đích, dịch vụ bên ngoài, thời gian lưu, quyền của bạn, người dùng dưới 16 tuổi, thay đổi chính sách, liên hệ; phần Điều khoản gồm quy tắc cộng đồng, kiểm duyệt và cảnh báo, khóa tài khoản và khiếu nại, quyền với nội dung đăng. Liên hệ: "tạm chưa cần, có thể chốt khi triển khai" |
| QA-315 | ISS-255: Nhận bản sao dữ liệu? Rút lại đồng ý? | Bản sao dữ liệu: "khá phức tạp" → không làm chức năng ở MS1, trang nêu quyền này và cách yêu cầu công bố khi triển khai. Rút lại đồng ý = vô hiệu hóa tài khoản; không đồng ý phiên bản chính sách mới thì chỉ chọn được đăng xuất hoặc vô hiệu hóa ("okey chốt") |
| QA-316 | ISS-256: Người dùng dưới 16 tuổi? | "chọn A" — không hỏi tuổi; ô đồng ý ở bước 1 kèm cam kết "nếu dưới 16 tuổi, tôi đã được cha mẹ hoặc người giám hộ đồng ý"; trang có mục riêng cho người dưới 16 tuổi |
| QA-317 | ISS-257: Người đang giữ phiên đăng nhập có được hỏi đồng ý lại ngay khi mở ứng dụng không? | A — hỏi ở lần mở ứng dụng kế tiếp, kể cả khi đang giữ phiên đăng nhập |
| QA-318 | ISS-258: Ai phát hành phiên bản chính sách mới? | A — đội phát triển, khi triển khai bản mới; nội dung trang và số phiên bản nằm trong mã nguồn, không có màn hình Admin |
| QA-319 | ISS-259: Lượt theo dõi Topic, bài viết của tài khoản đã xóa? | Theo đề xuất — xóa cùng các quan hệ theo dõi khác |
| QA-320 | ISS-260: Phản hồi gợi ý Topic của tài khoản đã xóa? | Theo đề xuất — giữ lại như nhật ký AI; bản ghi chỉ gồm Topic gợi ý và Topic được chọn, không còn gắn danh tính |

---
## Functional Requirement — M03: Post & Content (QA-321 → QA-333, QA-350 → QA-351)

| ID | Question | Answer |
|----|----------|--------|
| QA-321 | ISS-261: Bài viết có được đính kèm tài liệu (PDF/DOCX/XLSX/PPTX) không? | A — giữ theo DEC-035. "kệ đi, nó là vấn đề security, ta có thể sửa sau này. Hiện tại sẽ focus vào việc cho upload là được" |
| QA-322 | ISS-262: Bài mới tạo mang trạng thái kiểm duyệt nào; "gỡ" bài là gì? | "Bài vừa tạo, ta cứ cho trạng thái bình thường đi"; "gỡ chính là ẩn đó!" |
| QA-323 | ISS-263: Sửa bài đã đăng, quét lại: xử lý theo điểm và khi AI lỗi? | "với bài sửa, ta chỉ hoạt động dựa trên mức nghi ngờ thôi, ẩn và chờ mod xét!"; "khi AI lỗi, ta hoạt động theo đề xuất" (để nguyên, bài vẫn hiện) |
| QA-324 | ISS-264: Sửa, xóa, khôi phục theo trạng thái bài? | "okey theo đề xuất" — bảng sửa/xóa/khôi phục theo trạng thái (DEC-162) |
| QA-325 | ISS-265: MEDIUM, HEAVY chặn những thao tác nào? | A — chặn mọi thao tác đưa bài chưa từng công khai ra công khai; vẫn cho sửa, khôi phục bài cũ và bình chọn |
| QA-326 | ISS-266: Phần bắt buộc, giới hạn độ dài? | Gửi: bắt buộc tiêu đề và nội dung, "pool có thể tính như content và thay thế content"; tệp đính kèm không thay nội dung. Nháp: chỉ cần "không trắng tinh". Tiêu đề 150 ký tự; nội dung "tầm 5000 từ (hoặc lớn hơn chút)" → chốt 6.000 từ, chỉ xét chữ người đọc thấy. Nháp áp dụng như bình thường và "có cảnh báo ngay khi soạn thảo" |
| QA-327 | ISS-267: Chi tiết poll? | Đổi phiếu luôn được khi còn hạn (bỏ tùy chọn); có tùy chọn chọn một/chọn nhiều, "chọn nhiều luôn là mặc định"; khóa cấu hình sau khi gửi; chỉ chủ bài thêm lựa chọn, sau khi gửi chỉ thêm lựa chọn và sửa hạn, tối đa 10; hạn ≥ hiện tại, đổi được khi còn mở, kết thúc ngay = hạn bằng hiện tại; "cho phép bỏ chọn bình thường"; thêm/bỏ poll chỉ khi chưa gửi; % "tính trên tổng lượt chọn", làm tròn số nguyên (A); tác giả được bình chọn poll của mình |
| QA-328 | ISS-268: Bài bị AI tự từ chối? | "đúng vậy" — thấy nhóm vi phạm, gửi lại không giới hạn, khiếu nại qua M09 **[Clarified 2026-10-18 — DEC-198: khiếu nại gộp với cảnh cáo AI; hạn theo cảnh cáo hoặc 3 ngày]** |
| QA-329 | ISS-269: Khóa toàn bộ chặn gì? | Chặn bình luận mới, upvote và "khoá cả pool"; bookmark, báo cáo vẫn được |
| QA-330 | ISS-270: Đếm 7 ngày khôi phục thế nào? | "7 ngày tính từ lúc bắt đầu chọn xoá" (7 × 24 giờ) |
| QA-331 | ISS-271: Mod xem bài chưa công khai của người khác? | "không mở nháp nhé, vì tinh thần nháp chưa public thì ai duyệt? ta hiểu duyệt là bài mà để cho người khác đọc được!" — áp dụng cả bài tự ẩn, bài bị từ chối |
| QA-332 | ISS-272: Accepted Answer có trong MS1? | "MS1 không hỗ trợ chức năng accepted answer!" |
| QA-333 | ISS-273: Ảnh bìa bài viết? | "không có ảnh bìa, nếu có ảnh đính kèm thì dùng thôi!" |
| QA-350 | ISS-290: Bài hết 7 ngày khôi phục xử lý thế nào; ai xem lại bài đã xóa hẳn? | Đồng ý 4 đề xuất (giữ toàn bộ dữ liệu, Mod/Admin và tác giả xem lại như DEC-179, bookmark và trừ điểm tính tại lúc chuyển cờ); "thêm note định nghĩa đã xoá hẳn trong trường hợp này là như nào nhé, chứ không phải là xoá hết dữ liệu đâu" |
| QA-351 | ISS-291: Bài tự ẩn có né được kiểm duyệt không (Mod không xem được; sửa trong lúc ẩn rồi hiện lại không bị quét)? | Mod xem bài Tự ẩn trong báo cáo, lịch sử báo cáo, khiếu nại: "Đồng ý với bạn nói"; quét lại: "Chọn cách 2 nhé!" — quét khi tác giả hiện lại bài Tự ẩn đã được sửa trong lúc ẩn |

---

## Functional Requirement — M02: User Profile (QA-334 → QA-341)

| ID | Question | Answer |
|----|----------|--------|
| QA-334 | ISS-274: Chủ hồ sơ có ba tab (Bài viết, Bookmark, Đã xóa) hay "Đã xóa" nằm chỗ khác? | "bổ sung tab đã xoá nhé!" — ba tab, mặc định Bài viết; người xem chỉ Bài viết |
| QA-335 | ISS-275: Guest xem trang hồ sơ, danh sách theo dõi? | "guest xem được trang hồ sơ, chỉ đọc. xem danh sách theo dõi yêu cầu đăng nhập" |
| QA-336 | ISS-276: "Đang theo dõi" gồm gì; DEACTIVATED, BANNED? | "chỉ tính người dùng thôi nhé. các tài khoản deactive, ban sẽ không xuất hiện (nếu tài khoản trở lại trạng thái kích hoạt thì hiện lại)" |
| QA-337 | ISS-277: Hiện Lớp/Khối, ngày tham gia, stars nhận/cho? | "Chọn A đi, không cần hiện số star đã nhận / cho nữa" — hiện Lớp/Khối (khi đã đặt) và ngày tham gia |
| QA-338 | ISS-278: Bài đã lưu không còn xem được? | Chọn B: "chỉ cần hiển thị 'Nội dung không hiển thị' (hoặc câu gì đó tương đương)"; chốt dùng câu "Nội dung không tồn tại", giữ vị trí, bỏ lưu được; bài xóa hẳn hoặc tác giả DELETED thì bookmark bị xóa — "okey đó!" |
| QA-339 | ISS-279: Tab Bài viết hiện bài nào? | "chọn A đi, đồng ý!" — người xem: bài đã đăng công khai, không ẩn danh, bài nhóm Private chỉ với thành viên; chủ hồ sơ thêm nháp, chờ duyệt, bị từ chối, tự ẩn và bài ẩn danh của mình (có dấu "ẩn danh") |
| QA-340 | ISS-280: Danh sách xác nhận chi tiết hồ sơ | Nhắc Lớp/Khối: "cái này không làm ở ms1"; thứ tự: "cứ mới nhất là ưu tiên"; avatar: "hiện avatar mặc định, hoặc avatar là chữ cái đầu tiên của displayname or smth else"; bio: "không xét khoảng trắng đầu/cuối", Lớp/Khối optional; địa chỉ /u/: "ok" |
| QA-341 | ISS-281: Mod gỡ avatar, bio vi phạm? | "không cần quản lý cái đó đâu" |

---

## Functional Requirement — M04: Comment (QA-342 → QA-349)

| ID | Question | Answer |
|----|----------|--------|
| QA-342 | ISS-282: Sửa, xóa bình luận khi bài khóa / mức HEAVY / bình luận bị ẩn? | Khóa bình luận/khóa toàn bộ: "không sửa", cho xóa (đồng ý đề xuất); HEAVY: "vậy ok" — vẫn sửa, xóa bình luận cũ; bị ẩn: "không sửa/xoá là đúng rồi" |
| QA-343 | ISS-283: Xóa bình luận vĩnh viễn hay xóa mềm? | "post, comment và những thứ có thể report ta chỉ cho xoá mềm thôi, gắn cờ vào là được"; bài viết: "vẫn giữ tính năng 7 ngày để khôi phục, sau đó thay vì xoá hẳn ta có thể chuyển cờ" (mở OPEN-010); M11, M16: "tạo gì đó để ta sẽ trao đổi thêm khi làm các module đó" (OPEN-011); Mod/Admin xem nội dung đã xóa qua báo cáo, lịch sử báo cáo, khiếu nại (đồng ý đề xuất) |
| QA-344 | ISS-284: Bài bị xóa hẳn thì bình luận ra sao? | "bài bị xoá thì đâu ai xem được bình luận đâu mà phải lo xoá. cứ giữ cùng bài đi" |
| QA-345 | ISS-285: Bình luận bị ẩn: chủ bình luận thấy ở đâu; Mod xóa là gì; quét AI; khiếu nại? | "Làm giống bài nhé" — chủ bình luận chỉ xem khi mở từ thông báo; Mod chỉ có thao tác Ẩn (đồng ý đề xuất); quét AI: "ta giữ kiểm duyệt như vậy đi"; khiếu nại: "không khiếu nại!" |
| QA-346 | ISS-286: Gốc bị ẩn còn trả lời; dấu khi hết trả lời; trả lời vào luồng có dấu? | Gốc bị ẩn: "chọn C" — dùng chung dấu "[Bình luận đã bị xóa]"; dấu khi hết trả lời, trả lời vào luồng có dấu: "ok" theo đề xuất |
| QA-347 | ISS-287: Số bình luận; thứ tự Top khi cùng upvote? | Số bình luận: "chọn A" — đếm gốc và trả lời đang hiển thị bình thường; Top: "ok" — đăng trước đứng trước |
| QA-348 | ISS-288: Giới hạn độ dài; trích dẫn có tính không? | "cho 1000 từ"; "không tính trích dẫn nhé, trích dẫn chỉ là phần hiển thị, và cũng chỉ hiển thị 1 phần nếu quá dài"; "cho trích dẫn chỉ hiển thị 1 dòng" |
| QA-349 | ISS-289: Người bị xử lý có xem lại nội dung đã xóa khi khiếu nại hoặc xem mình bị báo cáo vì gì? | "chọn A" — chỉ chủ nội dung, chỉ đọc, mở từ thông báo xử lý hoặc khiếu nại; không thấy thông tin người báo cáo |

---

## Functional Requirement — M08: Moderation (QA-352 → QA-369)

| ID | Question | Answer |
|----|----------|--------|
| QA-352 | ISS-292: Ngưỡng AI có thay đổi theo mức cảnh cáo của tác giả không? | "ok chọn A đi" — một cặp 0,9/0,5 cho mọi người |
| QA-353 | ISS-293: "Suspend", "Disable account" có là thao tác riêng không? | "A nhé" — suspend chính là ban tạm thời; không có suspend, disable riêng |
| QA-354 | ISS-294: Vi phạm lần thứ 7 chuyển sang ban thế nào? | "okey, chọn A" — không ghi cảnh cáo thứ 7; hệ thống tạo yêu cầu ban trong hàng chờ, Mod/Admin bấm "Ban"; Mod phát hiện khi xử lý vụ thì chọn Ban thay vì cảnh cáo |
| QA-355 | ISS-295: Ai cảnh cáo, ban được tài khoản Mod, Admin; Mod xử lý vụ nhắm vào chính mình? | "ok 4 điểm" — (1) chỉ Admin cảnh cáo, ban Mod; Mod xử lý vụ nhắm vào Mod khác chỉ được ẩn nội dung; (2) Admin không bị cảnh cáo, ban; (3) AI không tự cảnh cáo Mod (≥ 0,9 để Admin quyết) và Admin; (4) Mod không thấy, không nhận vụ nhắm vào chính mình |
| QA-356 | ISS-296: Mod, Admin có ẩn, cảnh cáo, ban ngoài một vụ không? | Hỏi lại "chọn B có phức tạp hơn không", sau khi được giải thích: "chọn A đi" — mọi xử lý qua vụ; Mod tự phát hiện vi phạm thì tự báo cáo rồi nhận xử lý |
| QA-357 | ISS-297: Mức nặng của lý do, số lý do mỗi báo cáo, thứ tự khi bằng điểm? | "ừ, đồng ý đề xuất" — Nặng 10 (Bạo lực/Đe dọa, Người lớn/Không phù hợp, Thù ghét/Phân biệt, Quấy rối/Bắt nạt kể cả "có hệ thống", Group giả mạo), Trung bình 5 (Nội dung sai/hiểu nhầm, Đạo văn/Vi phạm bản quyền), Nhẹ 2 (Spam/Quảng cáo, Khác); mỗi báo cáo một lý do; bằng điểm thì vụ mở trước đứng trước |
| QA-358 | ISS-298: Hết thời gian thử thách thì giảm mức thế nào; "N ngày" tính sao? | "ừm chọn A và i" — về số lần cao nhất của mức dưới (HEAVY → 4, MEDIUM → 2, LIGHT → 0), mức mới có thời gian thử thách riêng nối tiếp; N ngày = đủ N × 24 giờ |
| QA-359 | ISS-299: Ban nào tính vào số lần đã bị ban? | "ok chọn A" — mọi ban từng có hiệu lực, kể cả ban được gỡ sớm và ban vĩnh viễn thủ công; không tính ban bị lật do khiếu nại |
| QA-360 | ISS-300: Báo cáo có làm bài bị tạm ẩn không? | "A nhé, báo cáo không ẩn" — chỉ AI quét lại mới làm bài Bị gắn cờ |
| QA-361 | ISS-301: Nội dung AI gắn cờ, yêu cầu ban nằm ở hàng chờ nào? | "okey nếu A hợp lí" — chung hàng chờ báo cáo, mỗi việc là một vụ, người báo cáo "Hệ thống (AI)"; gộp vào vụ đang mở của cùng đối tượng; mức nặng theo nhóm vi phạm AI phát hiện, số báo cáo tính 1; vụ yêu cầu ban có đánh dấu |
| QA-362 | ISS-302: Kết luận vụ — lý do, thông báo khi Bác bỏ, kết quả chung cho người báo cáo? | "A nhé" — lý do kết luận bắt buộc ở cả hai kết quả; người bị báo cáo không nhận thông báo khi Bác bỏ; người báo cáo nhận "đã có biện pháp xử lý" hoặc "không phát hiện vi phạm", câu chữ chốt khi thiết kế; vụ do AI tạo không có thông báo cho người báo cáo; đường dẫn khiếu nại chỉ kèm khi xử lý khiếu nại được |
| QA-363 | ISS-303: Báo cáo đối tượng không còn hiển thị với người báo cáo? | "01.12: okey, chọn A" — từ chối báo cáo |
| QA-364 | ISS-304: Báo cáo chính mình, báo cáo trùng, người ở HEAVY? | "nhóm 1-4: ok" — không báo cáo được nội dung, tài khoản của chính mình; cùng người báo cáo lại cùng đối tượng khi vụ còn mở thì từ chối; người ở HEAVY vẫn báo cáo được |
| QA-365 | ISS-305: "30 phút không thao tác", chỉ số tập trung, Admin xử lý vụ nhắm vào chính mình? | "nhóm 1-4: ok" — 30 phút tính từ thao tác cuối của người giữ (mở xem vụ, ẩn, cảnh cáo, ban, kết luận); chỉ số tập trung tính cho đối tượng của vụ đang xem, trong 90 × 24 giờ gần nhất; Admin cũng không thấy, không nhận vụ nhắm vào chính mình |
| QA-366 | ISS-306: Ngưỡng tốc độ, điểm quét, nhiều nội dung một lần quét, bỏ hoặc lật cảnh cáo? | "nhóm 1-4: ok" — kích hoạt khi số trả lời trong luồng đạt ngưỡng trở lên; điểm quét = điểm cao nhất trong 4 nhóm, nhóm đó là lý do của vụ; mỗi nội dung ≥ 0,9 một cảnh cáo; bỏ hoặc lật cảnh cáo: số lần giảm 1, mức tính lại, bản ghi giữ có đánh dấu, thời điểm kết thúc thử thách không đổi |
| QA-367 | ISS-307: Ban chồng; nhật ký? | "nhóm 1-4: ok" — không ban chồng (gỡ rồi Ban vĩnh viễn); nhật ký ghi thêm gỡ ban, bỏ cảnh cáo AI; không ghi nhận, nhả vụ; dòng nhật ký không sửa, không xóa |
| QA-368 | ISS-308: Người báo cáo có rút, sửa báo cáo không? | "q15b: không rút/sửa" |
| QA-369 | ISS-309: Báo cáo nhóm xử lý thế nào? | "có thể ẩn/khoá nhóm nhé", rồi "hỗ trợ cả ẩn và khoá đi", sau đó "ok" với hành vi chi tiết — Ẩn nhóm (không bỏ ẩn) và Khóa nhóm (Mod/Admin mở khóa trực tiếp); người bị báo cáo là Owner |

---

## Functional Requirement — M09: Appeal (QA-370 → QA-383)

| ID | Question | Answer |
|----|----------|--------|
| QA-370 | ISS-310: Ai xét khiếu nại khi người khiếu nại hoặc người ra xử lý là Mod, Admin? | Hỏi lại "có thật sự cần trường hợp mod, admin khiếu nại nhau không?"; sau khi làm rõ: "report/khiếu nại của mod sẽ do admin xử lý, và không thể report admin nhé, vì vậy không cần khiếu nại!" — Admin không bị báo cáo, không có khiếu nại; vụ và khiếu nại liên quan Mod chỉ Admin xử lý; phần còn lại giữ nguồn (Mod xét khiếu nại của người dùng thường, kể cả về xử lý do Admin ra, trừ thao tác của mình). Mod bị ban rồi khiếu nại: tính theo vai trò lúc bị xử lý — "được." |
| QA-371 | ISS-311: Bài, bình luận của Admin có qua duyệt, quét AI không? | "bài của admin không cần duyệt!"; "comment của admin tương tự". Ba điểm biên đề xuất — E1 nhóm do Admin làm Owner không báo cáo được; E2 bài của Admin trong nhóm vẫn qua cổng duyệt của nhóm (M11), chỉ bỏ quét AI và duyệt của hệ thống; E3 nội dung Admin không có kiểm duyệt nào — "ok" |
| QA-372 | ISS-312: "Mod duy nhất có thể xét" và chuyển lên Admin nghĩa là gì? | "A nhé!" — không có cơ chế chuyển riêng; chỉ là quy tắc lọc người thấy khiếu nại |
| QA-373 | ISS-313: Tài khoản đang bị ban có khiếu nại cảnh cáo, bài bị gỡ được không? | "chỉ khiếu nại được ban chứ?" → "ok" — trong lúc bị ban chỉ khiếu nại chính lệnh ban; xử lý khác khiếu nại khi tài khoản ACTIVE và còn hạn |
| QA-374 | ISS-314: Người bị AI tự cảnh cáo vào trang khiếu nại từ đâu? | "tại sao không khiếu nại như bị mod khiếu nại nhỉ?"; "vậy tại sao phải phân biệt do ai khiếu nại, chỉ cần thông báo bạn bị cảnh cáo ... + kèm option khiếu nại là được mà?" → "ok" — mọi thông báo về một xử lý khiếu nại được đều kèm nút Khiếu nại, bất kể ai ra |
| QA-375 | ISS-315: Khiếu nại bài bị AI tự từ chối: có cho khiếu nại không, hạn, kết quả? Cảnh cáo AI đi kèm? | Lúc đầu: "thôi, không cho khiếu nại nhé, như fb tôi thấy từ chối là từ chối thì phải?"; cảnh cáo AI đi kèm: "Cảnh cáo đó khiếu nại được mà?". Sau khi xem ví dụ Mod lật cảnh cáo mà bài vẫn bị từ chối, stakeholder hỏi lại "ta nên cho phép khiếu nại không ta?" → "đúng, phải theo hướng B, hạn 3 ngày được không (nhưng còn vướng cái cảnh cáo nếu để hạn này)" → "nếu có cảnh cáo -> hạn = hạn khiếu nại của cảnh cáo. nếu không -> hạn 3 ngày. OK không? và cảnh cáo cũng phải nêu là bài sẽ bị ẩn vì ta gộp" → "ok" (thông báo ghi "bị từ chối", không phải "bị ẩn") |
| QA-376 | ISS-316: Có lưu bản chụp nội dung lúc xử lý để xét khiếu nại không (stakeholder nêu)? | "ta đang có khá nhiều loại khiếu nại đó, nên việc lưu snapshot khá phức tạp" → "chọn C đi" — không chụp ở MS1; người xét dựa vào lý do kết luận, bằng chứng, lịch sử sửa bài, nhật ký AI; chỗ hở còn lại ghi "Cần cân nhắc" để xem sau MS1 |
| QA-377 | ISS-317: Hạn khiếu nại cảnh cáo khi thời gian thử thách bị đặt lại hoặc nối tiếp? | "ừ chọn A đi" — hạn cố định cho từng cảnh cáo: 7/10/15 ngày từ lúc ra, theo mức mà cảnh cáo đó đưa người dùng tới |
| QA-378 | ISS-318: Khiếu nại xét sau khi xử lý đã kết thúc? | "A" — vẫn xét, vẫn lật; số lần cảnh cáo hiện tại giảm 1, không dưới 0 |
| QA-379 | ISS-319: Ưu tiên giữa hàng chờ bài viết và cảnh cáo, ban? | "ừ chọn B đi" — một danh sách chung: ban > cảnh cáo > bài bị gỡ, cùng loại đến trước xét trước; lọc theo loại |
| QA-380 | ISS-320: Lật ban của Mod có trả lại vai trò Mod không? | "B đi nhé!" — không; Admin muốn thì gửi đề xuất làm Mod (DEC-091) |
| QA-381 | ISS-321: Bình luận bị ẩn có hiện lại khi cảnh cáo, ban liên quan bị lật không (OPEN-012)? | Hỏi lại "bài viết ta đang không cho hiện lại, vậy bình luận có cho hiện lại không?"; sau khi đính chính (bài bị Mod gỡ vẫn hiện lại, bài bị AI từ chối thì không): "ừ chọn B" — bình luận vẫn ẩn |
| QA-382 | ISS-322: Danh sách xác nhận — L1 lý do kết luận khiếu nại; L2 rút, sửa khiếu nại | "ok" — L1: lý do bắt buộc ở cả Chấp nhận và Từ chối, người khiếu nại thấy kết luận kèm lý do; L2: không rút, không sửa |
| QA-383 | ISS-323: Khiếu nại bài bị gỡ và khiếu nại riêng cảnh cáo, ban đi kèm cho kết luận ngược nhau thì sao? | "chọn B đi" — giữ hai đường riêng; xử lý đi kèm chỉ bị lật một lần, theo khiếu nại được chấp nhận trước; đã có khiếu nại riêng bị từ chối thì khiếu nại bài không lật nó; xử lý đã bị lật thì khiếu nại riêng mới bị từ chối, khiếu nại đang chờ vẫn xét, chấp nhận không đổi gì thêm |

---

## Functional Requirement — M13: AI Layer (QA-384 → QA-392)

| ID | Question | Answer |
|----|----------|--------|
| QA-384 | ISS-324: Vòng phản hồi đánh giá AI đo những gì: chỉ gợi ý Topic, hay cả AI kiểm duyệt? | Lúc đầu: "tôi nghĩ sẽ bỏ qua phản hồi AI này"; sau khi làm rõ chức năng không gửi phản hồi ngược cho AI mà chỉ đo nội bộ, và nêu hệ quả bỏ hẳn (sửa DEC-006, dữ liệu M05 mất mục đích): "ừ vậy giữ cho phần phản hồi topic nhé!" — chỉ đánh giá gợi ý Topic từ phản hồi gợi ý của M05; không đánh giá AI kiểm duyệt, không có thao tác đánh dấu đúng/sai |
| QA-385 | ISS-325: Ai xem chỉ số, ở đâu; tính thế nào? | Hỏi "tại sao ta phải làm cái này", "nhưng ở đâu dùng tới cái này"; sau khi giải thích: "vậy bổ sung nó vào trang thống kê nhé" — Admin xem ở trang thống kê M15. Cách tính chốt ở danh sách xác nhận (QA-392 mục 6) |
| QA-386 | ISS-326: Phần nào của bài được gửi cho AI kiểm duyệt? | "ừ thế chọn B đi!" — tiêu đề, nội dung chữ, bình chọn (câu hỏi, lựa chọn) và ảnh đính kèm; không gửi tài liệu đính kèm |
| QA-387 | ISS-327: Embedding tạo ở mốc nào; "sửa nhiều" là thế nào? | "chọn A nhé, tạo embedding sau khi bài chuyển qua đã đăng." — tạo khi bài chuyển sang Đã đăng (mọi đường); tạo lại mỗi lần tiêu đề hoặc nội dung chữ thay đổi |
| QA-388 | ISS-328: Embedding khi AI tắt hoặc lỗi; công tắc nào? | "chọn B đi, thêm bài đó vào queue để embedd lại." — embedding bài theo công tắc tổng và công tắc Search; bài thiếu embedding (do tắt hoặc lỗi) vào hàng chờ tạo bù khi công tắc bật lại hoặc AI hết lỗi. (Phần tóm tắt trong câu này không còn áp dụng sau QA-389: tóm tắt không lưu) |
| QA-389 | ISS-329: Tóm tắt tự động hay theo yêu cầu, có lưu không, ai dùng, ngưỡng, giới hạn? | "không cần lưu tóm tắt đâu ý, mỗi lần có yêu cầu thì nhận kết quả từ AI và hiện tóm tắt cho người dùng"; ngưỡng "mình chưa biết nên là bao nhiêu"; "logged in rồi mới có thể sử dụng chức năng tóm tắt, guest ấn nút xem tóm tắt -> thông báo đăng nhập để sử dụng tính năng"; giới hạn: "ta không cần giới hạn, ta lưu cache tóm tắt khi có yêu cầu, cache này tồn tại trong 1 khoảng thời gian … vừa giảm tải khi nhiều user yêu cầu, vừa hạn chế 1 người spam tóm tắt" → "chốt cách (ii)", "bạn đề xuất ngưỡng T sao cho hợp lí đi"; xác nhận cache dùng chung cả hệ thống; "bài dài chút mới nên tóm tắt chứ" → đề xuất 300 từ, giữ tạm 24 giờ → "ok" |
| QA-390 | ISS-330: Tóm tắt — thời gian chờ, khi lỗi, khi AI tắt, nội dung gửi AI? | "10s có đủ cho 1 lần tóm tắt không" → giữ 10 giây, là hằng số chỉnh qua triển khai; lỗi: "thông báo hệ thống bận/lỗi"; AI tắt: "xử lý như 2, nhưng thông báo ngay"; "phải thêm note là tóm tắt chưa bao gồm nội dung đính kèm"; không gửi bình chọn → "ok" |
| QA-391 | ISS-331: Mod, Admin có tra cứu nhật ký AI ngoài lúc xét khiếu nại không (mở rộng phạm vi)? | "chọn A đi" — không; chỉ xem khi xét khiếu nại bài bị AI tự từ chối; chỉnh ngưỡng do đội phát triển đọc dữ liệu, đổi qua triển khai |
| QA-392 | ISS-332: Danh sách xác nhận 1–6 | "ok" — (1) hai nhóm cùng điểm cao nhất: lấy nhóm đứng trước theo thứ tự Quấy rối → Thù ghét → Người lớn → Bạo lực; (2) nhật ký ghi chấm điểm kiểm duyệt, embedding bài, gợi ý Topic; không ghi tóm tắt, embedding truy vấn; (3) mỗi lời gọi một bản ghi, kể cả thất bại — là chỗ "ghi lỗi cho Admin"; (4) quét luồng bình luận: mỗi bình luận một bản ghi; (5) bản ghi không sửa, không xóa; (6) chỉ số ở M15 bản tối thiểu "tỷ lệ Topic gợi ý được giữ lại" |

---

## Functional Requirement — M06: Search (QA-393 → QA-404)

| ID | Question | Answer |
|----|----------|--------|
| QA-393 | ISS-333: Guest tìm bài theo ngữ nghĩa như User, hay chỉ full-text? | "ừm chọn B, nếu guest chọn tìm kiếm thông minh -> hiện notify yêu cầu đăng nhập"; "là tìm theo ngữ nghĩa ấy, chứ ai đặt tên thô là 'tìm theo ngữ nghĩa'"; xác nhận phương án A của câu bổ sung: "đúng nhé" — Guest tìm bài bằng full-text; chỉ Guest thấy lựa chọn "Tìm kiếm thông minh" (tên hiển thị của tìm kiếm ngữ nghĩa), bấm thì nhắc đăng nhập, kể cả khi AI tắt; người đã đăng nhập luôn tìm ngữ nghĩa khi AI bật, không có công tắc |
| QA-394 | ISS-334: Người dùng, Tag, Topic, Group khớp thế nào; thứ tự trong mỗi loại? | "A nhé" — khớp ở bất kỳ vị trí trong tên, không phân biệt hoa thường, bỏ dấu, cho khớp gần đúng; chỉ khớp tên (người dùng: display_name, username; Group không khớp mô tả); trong mỗi loại kết quả giống chuỗi gõ hơn đứng trước |
| QA-395 | ISS-335: Nhóm Private có hiện khi tìm Group không? | "B nhé" — ẩn hoàn toàn khỏi tìm kiếm và gợi ý khi gõ với người không là thành viên (kể cả Guest); thành viên vẫn tìm thấy nhóm của mình |
| QA-396 | ISS-336: Full-text khớp truy vấn nhiều từ thế nào, xếp hạng ra sao? | "ok chọn B" — bài chứa ít nhất một từ của truy vấn là khớp; Điểm liên quan = số từ của truy vấn có trong bài ÷ số từ của truy vấn; vẫn dùng công thức 0,8/0,2 |
| QA-397 | ISS-337: Chi tiết công thức xếp hạng? | "ừm" (hiểu là đồng ý phương án A) — tập ứng viên 120 bài; điểm liên quan ngữ nghĩa đổi về 0–1 theo thang cố định; điểm tương tác chuẩn hóa trong tập ứng viên, cùng điểm thô thì bằng 0; bằng điểm cuối → điểm liên quan cao hơn, rồi bài mới hơn; HEAVY: điểm cuối × 0,5 ở cả hai chế độ; thông báo khi đã tải đủ 120 mà cuộn tiếp |
| QA-398 | ISS-338: Sắp xếp Mới nhất, Nhiều upvote nhất áp trên tập nào? | "A nhé" — sắp lại chính tập ứng viên; bằng nhau thì bài mới hơn trước; không giảm hạng HEAVY ở hai cách này |
| QA-399 | ISS-339: Xem bài theo Topic/Tag khi không có truy vấn? | "A" — liệt kê mọi bài khớp bộ lọc; mặc định Mới nhất, đổi được sang Nhiều upvote nhất, không có Liên quan; không giới hạn 120; không gọi AI; ô trống không có bộ lọc thì không tìm |
| QA-400 | ISS-340: Bộ lọc kết hợp thế nào, "Following-only" gồm gì? | "ok chọn A" — mỗi loại bộ lọc một giá trị; nhiều bộ lọc thì bài phải thỏa tất cả; "đang theo dõi" gồm bài của người đang theo dõi, bài thuộc Topic đang theo dõi, bài đang theo dõi (như tab Following M14); bộ lọc chỉ áp cho kết quả bài |
| QA-401 | ISS-341: Kết quả tìm người dùng có hiện tài khoản không ACTIVE không? | "chỉ active thôi" — chỉ hiện tài khoản ACTIVE; ẩn BANNED, DEACTIVATED, DELETED |
| QA-402 | ISS-342: Danh sách xác nhận X1–X7 | "x1-x7 ok" — (X1) tài khoản chưa xong Bước 3 không hiện trong tìm người dùng; (X2) Guest thấy bộ lọc theo dõi, bấm thì nhắc đăng nhập; (X3) gợi ý từ ký tự đầu tiên, mỗi loại tối đa 3; (X4) Hôm nay/Tuần này/Tháng này theo lịch, giờ Việt Nam, theo thời điểm đăng; (X5) đoạn trích 150 ký tự đầu, cắt trước từ bị chia đôi và thêm "…", không quá 150 ký tự thì hiện nguyên, không có nội dung chữ thì không có đoạn trích; (X6) lịch sử chỉ thêm khi gửi truy vấn có chữ, gửi lại thì đưa lên đầu, hiện mới nhất trước, chọn mục thì gửi luôn, không xóa từng mục; (X7) "mỗi phút" = 60 giây gần nhất, tải thêm không tính, đổi bộ lọc/sắp xếp, mở trang Topic/Tag, chọn mục lịch sử tính một lượt gửi |
| QA-403 | ISS-343: Có xóa lịch sử tìm kiếm khi đăng xuất không (mở rộng phạm vi)? | "B di" — khi đăng xuất, xóa toàn bộ lịch sử tìm kiếm trên trình duyệt đó |
| QA-404 | ISS-344: Gợi ý @mention có khớp tên theo DEC-209 (bất kỳ vị trí, bỏ dấu, gần đúng) không? | "ok chọn A đi!" — có: @mention khớp tên như DEC-209; thứ tự theo tầng của @mention giữ nguyên |

---

## Functional Requirement — M07: Notification (QA-405 → QA-411)

| ID | Question | Answer |
|----|----------|--------|
| QA-405 | ISS-345: Theo dõi có sinh thông báo nội dung mới không, cho đối tượng nào; có giữ theo dõi bài viết không? | "following user: có thể thông báo user có bài đăng mới; following post: có lẽ không nên để following post hay sao nhỉ" → theo dõi Topic có thông báo bài mới không: "KHÔNG"; theo dõi bài viết: "bỏ theo dõi bài viết nhé!". Chi tiết thông báo bài mới theo đề xuất, xác nhận khi duyệt bản nháp: "ok được" — gửi khi bài công khai lần đầu; không gửi với bài ẩn danh, bài nhóm Private với người ngoài nhóm, bài bị từ chối, khi sửa hoặc khôi phục bài |
| QA-406 | ISS-346: Có cho bỏ theo dõi không (mở rộng phạm vi)? | "A, cho phép bỏ theo dõi nhé!" — cho bỏ theo dõi người dùng, Topic; mỗi cặp người theo dõi – người được theo dõi chỉ sinh một thông báo "đã theo dõi bạn" |
| QA-407 | ISS-347: Gộp upvote hoạt động thế nào? | "W2" — báo ngay lượt đầu; cửa sổ 5 phút tính từ lượt đầu; lượt sau trong cửa sổ cập nhật cùng thông báo; gộp riêng từng bài, từng bình luận; "A" là người upvote mới nhất, N là số người khác nhau còn lại; bỏ upvote không đổi thông báo |
| QA-408 | ISS-348: Chuông và trang Thông báo hiện thế nào? | "ok, theo đề xuất đi" — chuông 10 thông báo gần nhất, mới nhất trước (theo lần cập nhật cuối); số chưa đọc riêng; mở chuông không tự đánh dấu đã đọc; trang Thông báo tải 20 mỗi lần, cuộn được tới cuối |
| QA-409 | ISS-349: Ai nhận thông báo; tên người gây sự kiện hiện thế nào? | "ok, như đề xuất." — không báo cho chính người gây sự kiện; vẫn tạo cho người nhận BANNED, DEACTIVATED; không tạo cho DELETED; tên người gây sự kiện theo DEC-149, DEC-156 |
| QA-410 | ISS-350: Tắt toàn bộ Chat và tắt từng cuộc tác động lên nhau thế nào? | "Ừm, chọn A" — tắt toàn bộ là tắt hết, không bật riêng được; bỏ tắt toàn bộ thì cuộc đã tắt riêng vẫn tắt. Sửa phần "bị tắt nghĩa là gì": "Với tin nhắn, có thể mỗi tin nhắn mới, ta sẽ có 1 cái popup nhỏ thông báo. tắt thông báo chỉ là không hiện popup, còn số count vẫn phải đúng số thông báo chưa đọc". Popup không hiện khi đang mở đúng cuộc trò chuyện đó: "đúng rồi!"; số trên biểu tượng Tin nhắn là số cuộc trò chuyện có tin chưa đọc: "đúng rồi, là số cuộc trò chuyện ấy!" |
| QA-411 | ISS-351: Danh sách xác nhận X1–X6 | "OK cả nhóm" — (X1) không theo dõi chính mình, không theo dõi mới tài khoản BANNED, lượt theo dõi đã có được giữ; (X2) đề xuất làm Mod chọn một lần, không hết hạn, đề xuất lại là thông báo mới; (X3) email lỗi gửi lại ở lần quét kế tiếp, tối đa 3 lần; (X4) nội dung không còn: bấm thì thành đã đọc, hiện "Nội dung không tồn tại"; (X5) biểu tượng Tin nhắn đếm số cuộc trò chuyện có tin chưa đọc; (X6) công tắc tắt thông báo hiện trên mọi bài, tắt cả upvote bài và upvote bình luận của mình trong bài |

---

## Functional Requirement — M10: Admin Panel (QA-412 → QA-420)

| ID | Question | Answer |
|----|----------|--------|
| QA-412 | ISS-352: Cấp, thu hồi vai trò Admin thế nào? | "nên có 1 ADMIN_ROOT, và chỉ admin này được thăng/giáng cấp admin khác. flow giống mod cho đồng nhất" — cấp qua đề xuất + chấp nhận; thu hồi trực tiếp, về USER; ADMIN gốc không bị thu hồi |
| QA-413 | ISS-353: Đề xuất có hạn không; nhiều đề xuất thì sao? | "đề xuất chỉ có hiệu lực trong 7 ngày (hoặc ít hơn) thôi nhé, kể cả mod"; sau khi bàn lý do: "ok vậy 7 ngày" — phương án A: 7 × 24 giờ từ lúc gửi; hết hạn thì không bấm được; mỗi người một đề xuất cùng loại còn hiệu lực; chấp nhận chỉ có tác dụng khi còn đúng vai trò |
| QA-414 | ISS-354: Giữ tự từ chức không? | "ừm chọn A" — giữ cho Mod và Admin (trừ ADMIN gốc), có bước xác nhận, ghi nhật ký |
| QA-415 | ISS-355: "Performance" trong quản lý tài khoản Mod là gì? | "A nhé" — không có màn hình riêng; Admin xem nhật ký kiểm duyệt lọc theo Mod; "revoke" là giáng cấp |
| QA-416 | ISS-356: Cờ tính năng chỉ cho Auth? | "ủa tưởng áp dụng cho module auth (register ...) thôi mà nhỉ" — đã làm rõ: tạm dừng đăng ký là mục riêng; cờ tính năng là mục khác của DEC-092. Stakeholder: "khi tắt thì một số thứ vẫn nên chạy ngầm, chỉ từ chối request của user và hiện thông báo hệ thống đang bận khi truy cập module đó" |
| QA-417 | ISS-356: Xét toàn bộ module, module nào nên có cờ? | "ừ được" — chỉ Group, Chat, Gamification (giữ DEC-092); các module khác không có cờ, kèm lý do theo từng module |
| QA-418 | ISS-357: Banner thế nào? | "ừ theo đề xuất đi" — một banner, văn bản thuần, tối đa 200 ký tự, người xem đóng được, nội dung mới thì hiện lại |
| QA-419 | ISS-358: Nhật ký thao tác Admin ghi gì? | "ừm chọn A" — mọi thao tác làm đổi dữ liệu Admin làm với vai trò Admin, và mọi thay đổi vai trò kể cả khi người làm không phải Admin; không ghi việc xem, nhận/nhả vụ, việc làm như người dùng thường |
| QA-420 | ISS-359: Danh sách xác nhận L1–L5 | "ok full" — chấp nhận toàn bộ đề xuất L1.1–L5.4 (xem người dùng, đối tượng đề xuất, độ dài banner, lý do và thứ tự, lọc nhật ký, giá trị khởi tạo cấu hình) |
