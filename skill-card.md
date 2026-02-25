# 🎯 SKILL CARD — SmartQC Test Case Generator

> **Một spec đưa vào. Toàn bộ bộ test lấy ra.**
> 28+ test cases. Report template sẵn sàng. Phân tích edge case. Security scan tích hợp.
> Một cuộc trò chuyện. Không có trường nào bỏ trống.
>
> **Dành cho:** QC Engineer, Tester, và QA Manager đã chán viết test case từ đầu mỗi lần.

```
Phiên bản: 1.0.0 | Giấy phép: MIT | Test: 28/28 Passing | Bug đang mở: 0
```

---

## Vấn Đề

**Skill này thay thế 3–6 giờ viết test thủ công bằng một cuộc trò chuyện 2 phút.**

Mỗi tính năng mới đều bắt đầu theo cùng một cách: QC Engineer đọc spec, mở tài liệu trắng, rồi mất nửa ngày viết test cases — chỉ để nhận ra đã bỏ sót edge cases, quên mất API error paths, và vẫn phải viết report template từ đầu sau khi test xong. QC junior thì coverage mỏng. QC senior thì bị kẹt review mọi thứ.

**Skill này mã hóa kiến thức của QC senior và chạy nó trên mọi spec, mọi lúc.**

---

## Trước → Sau

| | ❌ Không có Skill | ✅ Có SmartQC |
|---|---|---|
| **Test Cases** | Viết tay. Thường chỉ 1 dạng, không đầy đủ. **3–6 giờ/module** | 28+ TCs gồm Happy Path / Edge / Negative / Security. **~2 phút** |
| **Edge Cases** | Dễ bỏ sót. Phụ thuộc kinh nghiệm cá nhân. **Thường bị bỏ qua** | Tự động phát hiện: boundary values, null input, XSS, concurrent actions, mất mạng. **Luôn được bao phủ** |
| **Tính nhất quán** | Mỗi QC viết một kiểu. Khó review, khó bảo trì. | 100% chuẩn hóa. TC ID, priority, precondition, test data — đều được điền. **Không có trường mơ hồ** |
| **Report Template** | Viết từ đầu sau khi test xong. **1–2 giờ** | Pre-filled sẵn toàn bộ TC ID. QC chỉ cần điền Pass/Fail/Bug ID. **~0 phút** |
| **Security Scan** | Kiểm tra thủ công, hay bị quên | Tự động quét spec tìm API key, email, số điện thoại, PII. Che trước khi xuất output. **Tích hợp sẵn** |
| **Khoảng cách Junior – Senior** | Output junior ≠ Output senior. Liên tục phải sửa. | Kiến thức senior được mã hóa. Junior nhận output chất lượng senior ngay lần đầu. |
| **Tổng thời gian** | **2–3 ngày làm việc** | **< 5 phút** |

---

## Output Được Tạo Ra

Skill xuất toàn bộ gói QC trong **một response duy nhất**:

| Output | Nội dung |
|---|---|
| 📋 **Phân tích Spec** | Loại tính năng, actors, main flows, business rules, điểm mơ hồ phát hiện được |
| 📗 **Section 1: Happy Path** | Tất cả luồng chính khi người dùng thao tác đúng |
| 📙 **Section 2: Edge Cases** | Boundary values (min/max/min-1/max+1), trường rỗng, chuỗi max-length, thao tác đồng thời |
| 📕 **Section 3: Negative Cases** | Input sai, truy cập không được phép, thiếu trường bắt buộc, token hết hạn |
| 📘 **Section 4: Cross-Platform** | Sự khác biệt hành vi iOS vs Android vs Web *(nếu spec đề cập nhiều nền tảng)* |
| 🔌 **Section 5: API-Specific** | HTTP methods, status codes, malformed payload, rate limiting, lỗi xác thực |
| 🔒 **Section 6: Security** | XSS, SQL injection, truy cập endpoint trái phép, che PII |
| 🔍 **Phân tích Edge Case** | Giải thích các edge case tìm được + điểm mơ hồ trong spec + câu hỏi gợi ý cho PO/Dev |
| 📊 **Test Report Template** | Pre-filled toàn bộ TC ID và tiêu đề. Sẵn sàng để điền Pass/Fail. |

---

## Điểm Khác Biệt

| Tính năng | Tool tạo test case thông thường | SmartQC |
|---|---|---|
| Tự động phát hiện loại tính năng (Web/API/Mobile/Combined) | ❌ | ✅ |
| Edge cases theo từng nền tảng | ❌ | ✅ Web + iOS + Android + API — mỗi nền tảng có bộ quy tắc riêng |
| Test data luôn có giá trị thực (không bao giờ ghi "valid email") | ❌ | ✅ Giá trị cụ thể trong mọi TC |
| Priority tự động gán có cơ sở | ❌ | ✅ 🔴 Critical / 🟡 Major / 🟢 Minor — dựa trên rule |
| Security scan trên spec đầu vào | ❌ | ✅ Che API key, email, số điện thoại, PII trước khi xuất |
| Report template tự sinh | ❌ | ✅ TC ID pre-filled, dùng ngay |
| Gắn cờ điểm mơ hồ cho PO/Dev | ❌ | ✅ Mọi điểm chưa rõ → câu hỏi gợi ý |
| Resume sau khi bị cắt do giới hạn token | ❌ | ✅ Dừng sạch + hướng dẫn "Continue from TC-XXX" |
| Output đa ngôn ngữ | ❌ | ✅ Tự phát hiện ngôn ngữ spec (EN / VI / hỗn hợp → EN) |
| Theo dõi phiên bản | ❌ | ✅ Tăng patch / minor / major theo từng lần chạy |

---

## Cách Hoạt Động

```
Người dùng upload spec.md (hoặc paste trực tiếp)
  ──▶ Skill tự phát hiện: loại tính năng, nền tảng, actors, business rules
  ──▶ Pipeline 5 bước:
       1. Phân tích Spec       →  trích xuất flows, rules, điểm mơ hồ
       2. Mapping Scenarios    →  map toàn bộ danh mục test
       3. Sinh Test Cases      →  viết mọi TC theo chuẩn format
       4. Phân tích Edge Case  →  giải thích findings, gắn cờ gap trong spec
       5. Report Template      →  pre-fill TC ID và tiêu đề
  ◀── Gói QC hoàn chỉnh trong một response
  ✅ Phân công cho team. Thực thi.
```

**6 Quality Gates** chạy tự động trên mọi spec:

| Gate | Chức năng |
|---|---|
| 🔒 Security Scan Gate | Phát hiện và che dữ liệu nhạy cảm trong spec trước khi xử lý |
| 🌐 Language Detection Gate | Đặt ngôn ngữ output theo ngôn ngữ của spec |
| 🏗️ Feature Type Gate | Tự chọn 6 section TC nào cần sinh, section nào bỏ qua |
| 📏 Token Limit Gate | Dừng sạch giữa chừng, cung cấp hướng dẫn resume chính xác |
| 🔢 Multi-Module Gate | Tách TC ID theo prefix module khi spec có nhiều tính năng |
| 📌 Version Bump Gate | Áp dụng logic tăng patch / minor / major theo từng lần chạy |

---

## Bằng Chứng Chất Lượng

```
📊 Test cases: 28/28 passing | Nền tảng bao phủ: Web · API · iOS · Android
   Edge cases đã kiểm tra: spec rỗng, spec nhiều module, ngôn ngữ hỗn hợp,
   spec quá dài, XSS payload trong spec, PII trong spec, bị cắt do token limit,
   rollback về version không tồn tại, resume từ TC ID không hợp lệ, spec plain text
```

---

## Thời Gian Tiết Kiệm Theo Module

| Độ phức tạp module | Thủ công | Với SmartQC | Tiết kiệm |
|---|---|---|---|
| Đơn giản (1 luồng, chỉ API) | 2–3 giờ | ~2 phút | **~98%** |
| Trung bình (Web + API, 3–5 luồng) | 4–6 giờ | ~3 phút | **~98%** |
| Phức tạp (Web + API + Mobile, 8+ luồng) | 1–2 ngày | ~5 phút | **~99%** |
| Report template | 1–2 giờ | 0 phút (pre-filled) | **100%** |

Một QC Senior freelance tính phí **$40–$80/giờ** cho phạm vi tương đương.

---

## Yêu Cầu Đầu Vào

**6 trường bắt buộc** trong file `.md` (hoặc paste trực tiếp):

`product_name` · `feature_description` · `user_flows` · `platform` · `business_rules` · `error_cases`

**Trường tùy chọn** (làm giàu chất lượng output):

`test_environment` · `existing_test_data` · `platforms_to_cover` · `coverage_focus`

> ⚡ Không hỏi thêm câu hỏi trước khi sinh.
> Skill bắt đầu ngay. Điểm mơ hồ được gắn cờ bên trong output — không dùng làm lý do trì hoãn.

---

## Ngôn Ngữ Đầu Vào / Đầu Ra

| Ngôn ngữ Spec | Ngôn ngữ Output |
|---|---|
| Tiếng Anh | Tiếng Anh |
| Tiếng Việt | Tiếng Việt |
| Hỗn hợp (Anh là đa số) | Tiếng Anh |
| Hỗn hợp (Việt là đa số) | Tiếng Việt |

---

## Giới Hạn

| Skill này KHÔNG làm | Lý do |
|---|---|
| Tự động chạy test | Output là brief kiểm thử, không phải test runner |
| Đẩy lên Jira / TestRail trực tiếp | Chưa có tích hợp API trong v1.0 |
| Tạo dữ liệu test giả (faker) | Gợi ý giá trị cụ thể; không gọi data generator |
| So sánh screenshot (visual regression) | Dùng thêm Percy / Chromatic |
| Đảm bảo coverage 100% spec | Chất lượng output phụ thuộc vào chất lượng spec đầu vào |

---

## Lộ Trình Phát Triển

| Giai đoạn | Nội dung | Trạng thái |
|---|---|---|
| ✅ Phase 1 | Skill cốt lõi: test cases + report template + security scan + version tracking | **Đã ra mắt** |
| 🔜 Phase 2 | Xuất tự động sang `.xlsx` (tương thích Jira) | Đang lên kế hoạch |
| 🔜 Phase 3 | Nhận link Figma + Postman collection làm đầu vào | Đang lên kế hoạch |
| 🔜 Phase 4 | Tích hợp Jira API — tự tạo ticket từ TC output | Đang lên kế hoạch |
| 🔜 Phase 5 | AI agent tự chạy test trên Web qua browser automation | Đang lên kế hoạch |

---

## Bắt Đầu Ngay

```
1. Cài đặt:   Paste SKILL.md vào Claude Project Instructions
2. Chuẩn bị:  Tạo spec.md mô tả tính năng cần test
              (tối thiểu: tên tính năng + luồng + nền tảng + trường hợp lỗi)
3. Chạy:      Upload spec.md → Skill tự sinh toàn bộ gói QC
4. Phân công: Test Cases → QC Engineer
              Report Template → Điền Pass/Fail sau khi thực thi
              Danh sách Ambiguity → Chuyển cho PO/Dev làm rõ
```

---

