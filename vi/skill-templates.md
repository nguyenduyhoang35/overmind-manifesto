# Overmind — Skill Templates

> Đây là starter templates cho 2 skills tạo ra nhiều knowledge nhất: Discover và Retro.
> Chúng không phải scripts cứng nhắc. Điều chỉnh flow theo context của bạn. Cấu trúc tồn tại để ngăn bạn skip bước — không phải để làm chậm bạn.
> Thêm skill templates sẽ emerge khi bạn thực hành. Khi nhận ra mình lặp lại cùng pattern 3+ lần — đó là skill mới đang chờ được viết.

---

## Discover

### Trigger

Dùng Discover khi:
- Bắt đầu project hoặc feature mới và domain knowledge chưa rõ
- AI liên tục assume sai về một area cụ thể
- Bạn sắp build thứ gì đó nhưng không thể mô tả business rules một cách tự tin
- Domain expert mới tham gia và knowledge của họ cần được externalize
- Bạn kế thừa legacy code/process và cần extract các rules ngầm

Không dùng Discover khi:
- Bạn đã hiểu domain đủ rõ để tự viết rules — viết thẳng đi
- Task là quick prototype mà sai assumption cũng rẻ để fix

### Input

Trước khi bắt đầu Discover session, chuẩn bị:
- **Scope** — area nào của knowledge bạn đang explore? ("flow cancel đơn hàng", "pricing rules cho enterprise clients", "authentication requirements")
- **Known unknowns** — bạn đã biết mình chưa biết gì? ("tôi không biết chuyện gì xảy ra khi partial refund được yêu cầu")
- **Existing knowledge** — trỏ AI đến relevant files trong knowledge store để nó không hỏi lại thứ đã capture

### Flow

**Bước 1: AI hỏi, người trả lời**

Vai trò AI là facilitator, không phải teacher. AI hỏi open-ended questions về scoped area. Một câu hỏi một lúc. Mỗi câu hỏi nên probe vào specifics, edge cases, và exceptions.

Ví dụ:
```
AI: "Khi customer cancel đơn sau khi đã ship, chuyện gì xảy ra?"
Human: "Mình gửi return label. Refund sau khi nhận lại hàng."
AI: "Nếu hàng bị hỏng khi trả về thì sao?"
Human: "Partial refund dựa trên đánh giá tình trạng hàng."
AI: "Ai đánh giá tình trạng? Có thời hạn không?"
Human: "Team kho, trong 3 ngày làm việc kể từ khi nhận. Nếu miss deadline, full refund mặc định."
```

Session kết thúc khi:
- Câu hỏi bắt đầu được trả lời bằng "giống cái đã nói rồi"
- Bạn đã cover scope đã define ở Input
- Câu hỏi mới là về edge cases quá hiếm để cần quan tâm lúc này

**Bước 2: AI cấu trúc câu trả lời**

AI lấy raw answers và cấu trúc thành knowledge format:
- Business rules dưới dạng statements rõ ràng, testable
- Decisions kèm lý do
- Constraints dưới dạng must/must-not rules
- Open questions đánh dấu là "unvalidated assumptions"

**Bước 3: Người review và confirm**

Người đọc structured output. Sửa bất kỳ thứ gì AI hiểu sai. Confirm accuracy. Bước này critical — AI sẽ hiểu sai một số câu trả lời. Đừng skip.

### Output Format

Knowledge vào store theo cấu trúc:

```markdown
## [Area]: [Topic]
Source: Discover session, [date]
Participants: [ai đã contribute]

### Business Rules
- Đơn cancel sau khi ship → gửi return label, refund sau khi nhận hàng
- Hàng trả hỏng → partial refund dựa trên đánh giá tình trạng từ team kho
- Deadline đánh giá: 3 ngày làm việc. Miss deadline → full refund mặc định

### Decisions
- [quyết định]: [lý do]

### Constraints
- [must/must-not rule]

### Open Questions
- Chuyện gì xảy ra khi customer dispute đánh giá tình trạng? (unvalidated — cần input từ legal)
```

---

## Retro

### Trigger

Dùng Retro khi:
- Một iteration/sprint/task hoàn thành
- AI produce output cần sửa đáng kể
- Bug hoặc failure xảy ra mà knowledge store hiện tại không catch được
- Bạn nhận ra cùng loại sai lầm lặp lại hơn 1 lần
- Trước khi bắt đầu iteration tiếp theo — để capture lessons khi còn tươi

Không dùng Retro khi:
- Sai lầm quá trivial và đã hiển nhiên (typo, syntax error)
- Fix tốn ít effort hơn capture lesson

### Input

Trước khi bắt đầu Retro session, chuẩn bị:
- **Đã execute gì** — task, iteration, hoặc feature vừa hoàn thành
- **Gì sai** — failures cụ thể, assumptions sai, rework đã xảy ra
- **Gì đúng** — approaches đã hoạt động tốt (đây cũng là knowledge đáng encode)
- **Constraints hiện tại** — trỏ AI đến existing constraints để rules mới không duplicate hoặc contradict

### Flow

**Bước 1: Xác định chuyện gì đã xảy ra**

Walk through execution. AI hỏi targeted questions:

```
AI: "Gì sai trong iteration này?"
Human: "Agent implement payment module nhưng assume mọi currency dùng 2 decimal places."
AI: "Yêu cầu thực tế là gì?"
Human: "JPY dùng 0 decimals, BHD dùng 3. Cần per-currency decimal config."
AI: "Có knowledge nào đã tồn tại mà lẽ ra phải prevent được lỗi này?"
Human: "Không, mình chưa capture currency rules."
```

**Bước 2: Root cause → knowledge thiếu**

Với mỗi failure, AI giúp trace về missing knowledge:

- Có rule lẽ ra phải tồn tại nhưng không có? → **Cần rule mới**
- Có rule tồn tại nhưng sai/lỗi thời? → **Rule cần update**
- Có rule tồn tại nhưng AI không nhận được làm context? → **Vấn đề process, không phải knowledge**
- Có rule tồn tại, AI nhận được, nhưng vẫn vi phạm? → **Rule cần rõ hơn/cụ thể hơn**

**Bước 3: Encode rules mới**

Mỗi failure tạo ra đúng 1 rule mới (hoặc 1 rule được update). AI draft rule. Người confirm.

**Bước 4: Capture cái đã hoạt động tốt**

Đừng chỉ học từ failure. Nếu approach nào hoạt động tốt, encode luôn:
- "Cung cấp full entity relationship diagram làm context đã loại bỏ toàn bộ FK mistakes" → convention: "luôn include ERD trong context cho data model tasks"

### Output Format

```markdown
## Retro: [Tên Iteration/Task]
Date: [date]
Participants: [ai đã tham gia]

### Gì sai
| Issue | Root cause | Knowledge thiếu | Rule mới |
|-------|-----------|-----------------|----------|
| Currency decimal error | Không có currency config rules | Per-currency decimal rules chưa capture | "Mọi tính toán tiền tệ phải dùng decimal precision theo currency. JPY=0, BHD=3, default=2." |
| ... | ... | ... | ... |

### Gì đúng
| Cái hoạt động | Tại sao | Encode thành |
|---------------|---------|-------------|
| ERD trong context | AI có full relationship picture | Convention: include ERD cho data model tasks |

### Knowledge store đã update
- Thêm: [list rules mới kèm file locations]
- Update: [list rules đã update kèm thay đổi gì]
- Cần review: [rules có thể đã outdated dựa trên retro này]
```

---

## Tạo Skills Mới

Khi nhận ra mình lặp lại structured interaction pattern 3+ lần, extract thành skill theo template:

```markdown
## [Tên Skill]

### Trigger
Khi nào dùng / khi nào không

### Input
Chuẩn bị gì trước khi bắt đầu

### Flow
Từng bước tương tác giữa người và AI

### Output Format
Kết quả vào knowledge store dưới dạng nào
```

Giữ template nhẹ nhàng. Skill mà follow tốn nhiều thời gian hơn ad-hoc là skill thất bại. Cấu trúc nên tiết kiệm thời gian, không phải thêm ceremony.
