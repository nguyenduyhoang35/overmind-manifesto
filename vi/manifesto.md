# Overmind

### A Knowledge-Driven Development Manifesto

> Bạn không cần AI thực thi nhanh hơn.
> Bạn cần AI thực thi **đúng** hơn.
> Và "đúng" phụ thuộc hoàn toàn vào chất lượng kiến thức bạn cho nó.

---

## Vấn đề thực sự

Hãy nhìn lại những lần AI cho output tệ. Không phải vì model dở. Không phải vì prompt sai. Mà vì bạn chưa biết rõ thứ mình muốn — hoặc biết rõ nhưng chưa diễn tả được.

Bạn nói "build tính năng quản lý đơn hàng." AI build ra thứ gì đó. Trông hợp lý. Nhưng nó assume 1 đơn hàng = 1 seller, trong khi business của bạn cho phép 1 đơn hàng nhiều seller. Nó assume cancel = refund ngay, trong khi flow thực tế cần approval. Mỗi assumption sai = rework. Rework nhiều hơn build từ đầu.

Bạn nói "viết chiến lược marketing cho sản phẩm mới." AI viết ra thứ trông chuyên nghiệp. Nhưng nó assume target audience là B2C, trong khi sản phẩm bạn bán B2B. Nó assume budget lớn cho paid ads, trong khi bạn bootstrap. Cùng một vấn đề: AI không có knowledge về context cụ thể của bạn.

Đây không phải lỗi AI. Đây là lỗi của việc **cho AI execute mà không cho nó đủ knowledge.**

Vấn đề này không giới hạn ở phát triển phần mềm. Bất kỳ lĩnh vực nào bạn dùng AI để thực thi — viết content, phân tích dữ liệu, thiết kế quy trình, nghiên cứu thị trường, vận hành hệ thống — đều gặp cùng bottleneck: AI execute dựa trên knowledge bạn cung cấp. Knowledge tốt → output tốt. Knowledge thiếu → AI tự assume → output sai.

Prompt engineering, context engineering, harness engineering — tất cả đều giải quyết "làm sao AI thực thi tốt hơn." Nhưng chúng đều có chung một assumption ngầm: **bạn đã biết rõ mình muốn gì.** Nếu bạn chưa clear, pipeline đẹp mấy cũng chạy sai hướng.

Overmind giải quyết ở tầng sâu hơn: **trước khi bàn đến execution, hãy chắc chắn knowledge đã đúng.** Nguyên lý này áp dụng cho bất kỳ lĩnh vực nào — phát triển phần mềm chỉ là nơi ta nhìn thấy nó rõ nhất vì feedback loop nhanh (code chạy hoặc không chạy), nhưng cách nghĩ này chuyển được sang mọi domain mà AI đóng vai trò thực thi.

---

## Ý tưởng cốt lõi

### Knowledge là gì?

Knowledge không phải document. Không phải data. Không phải information.

**Knowledge là bất kỳ thứ gì mà nếu AI không biết, nó sẽ phải tự assume — và assumption đó có thể sai.**

"Đơn hàng dưới 500K không cần approval" — đó là knowledge. Nếu AI không biết, nó sẽ assume mọi đơn cần approval, hoặc không đơn nào cần. Cả hai đều sai.

"Dùng PostgreSQL vì cần JSONB + full-text search" — đó là knowledge. Không chỉ quyết định mà cả lý do. Khi 6 tháng sau ai đó hỏi "tại sao không dùng MongoDB?" — lý do đã nằm sẵn.

"Lần trước agent hay tạo lại file đã tồn tại trong worktree" — đó cũng là knowledge. Bài học từ sai lầm, encode để không lặp lại.

Knowledge có nhiều dạng: business rules, quyết định kỹ thuật, ràng buộc, thuật ngữ, bài học từ sai lầm, hành vi của hệ thống bên ngoài, assumptions đã validate, assumptions chưa validate. Dạng nào quan trọng nhất phụ thuộc vào project và thay đổi theo thời gian. Không có danh sách cố định — bạn sẽ nhận ra knowledge nào cần capture khi thấy AI assume sai vì thiếu nó.

### Knowledge quyết định chất lượng output

Output là hạ nguồn của knowledge. Khi knowledge đúng, AI execution chính xác đến mức đáng ngạc nhiên. Khi knowledge sai hoặc thiếu, không tool nào cứu được output. Điều này đúng cho code, cho content, cho phân tích, cho bất kỳ output nào AI tạo ra.

Đây không phải lý thuyết. Một dự án thực tế đã chạy 21 iteration với AI agents. Iteration đầu tiên, agents vi phạm 7 guidelines vì không có knowledge đầy đủ — chất lượng đạt 84%. Đến iteration thứ 21, cùng AI đó, cùng model đó, nhưng knowledge đã tích lũy qua 21 lần học — chất lượng đạt 100%, toàn bộ 106 bài test pass, không bỏ sót bài nào.

Khác biệt 84% → 100% đến **hoàn toàn** từ knowledge, không từ model hay prompt.

### Knowledge-first: đầu tư vào knowledge trước khi execute

Tỷ lệ đầu tư giữa knowledge và execution không cố định — nó phụ thuộc vào mức độ bạn đã biết về domain, complexity của task, và cost of getting it wrong.

Dự án mới trong domain lạ? Phần lớn effort ban đầu sẽ dồn vào discovery và capture knowledge. Dự án đã chạy 20 iterations với knowledge store đầy đủ? Effort chủ yếu ở execution vì knowledge đã sẵn sàng. PoC cần validate idea trong 1 ngày? Gần như toàn bộ effort ở execution, capture vài ghi chú nếu cần.

Nguyên tắc không phải "luôn dành X% cho knowledge" mà là: **đừng execute cho đến khi bạn tin rằng knowledge đủ cho AI không phải assume những thứ quan trọng.** Đôi khi đủ nghĩa là 10 phút ghi 3 quyết định. Đôi khi đủ nghĩa là 1 tuần phỏng vấn domain expert. Bạn cảm nhận được — và qua thời gian, bạn cảm nhận chính xác hơn.

### Con người nhận ra pattern, AI thực thi pattern

Đây là phân công lao động đúng nhất giữa người và AI trong mọi lĩnh vực. Con người giỏi nhận ra "à, mỗi lần AI viết proposal cho client enterprise, nó luôn quên đề cập compliance requirements." AI giỏi tuân thủ rule "khi viết proposal cho enterprise client, luôn include compliance section." Con người phát hiện pattern, encode thành rule, AI tuân thủ rule mãi mãi.

Trong phần mềm: "mỗi lần agents implement cross-context feature, chúng luôn quên check event contract" → rule: "kiểm tra event contract trước khi implement."

Trong content: "mỗi lần AI viết blog post, nó dùng giọng quá formal cho audience của mình" → rule: "giọng conversational, không dùng jargon, viết như đang nói chuyện."

Pattern giống nhau ở mọi nơi. Đây cũng là lý do tại sao người 2 năm kinh nghiệm nhưng biết nhận ra pattern có giá trị hơn người 5 năm kinh nghiệm nhưng chỉ biết follow checklist. Checklist ai cũng follow được, AI follow còn tốt hơn người. Nhận ra khi nào cần checklist mới — đó là việc của con người.

### Knowledge tốt hơn bất kỳ contributor đơn lẻ nào

Một tính chất tự nhiên của approach này: khi AI có access vào knowledge store trong quá trình tương tác với con người, knowledge được tạo ra chính xác hơn cả input gốc. Con người cung cấp domain truth, AI cross-reference với knowledge đã có — kết quả là refined knowledge mà không bên nào tự tạo được riêng lẻ. Knowledge store trở thành thứ thông minh hơn bất kỳ individual contributor nào, vì nó tích lũy và kết nối góc nhìn của mọi người qua thời gian.

---

## Ba thứ bạn cần

Không phải framework phức tạp. Không phải hệ thống enterprise. Ba thứ:

### 1. Một chỗ ghi knowledge

Gọi là knowledge store, knowledge base, hay thậm chí chỉ là folder có cấu trúc — không quan trọng. Quan trọng là:

**Mọi knowledge quan trọng phải nằm ở một chỗ mà cả người và AI agent đều đọc được.** Không nằm trong đầu bạn. Không nằm trong Slack message tuần trước. Không nằm trong meeting notes mà không ai đọc lại.

Knowledge bao gồm gì? Tùy project. Có thể là:
- Business rules ("đơn hàng dưới 500K không cần approval")
- Quyết định kỹ thuật ("dùng PostgreSQL vì cần JSONB + full-text search")
- Ràng buộc ("không import trực tiếp giữa các module")
- Bài học từ sai lầm ("agent hay tạo lại file đã có trong worktree — phải ghi rõ 'file ĐÃ TỒN TẠI, KHÔNG tạo mới'")
- Thuật ngữ ("PO = Purchase Order, không phải Post Office")
- API behaviors ("Shopee webhook delay 5-30 giây, không phải realtime")
- Bất kỳ thứ gì mà nếu AI không biết, nó sẽ assume sai

Bắt đầu đơn giản. Một folder với markdown files có cấu trúc là đủ. Phức tạp hóa khi và chỉ khi đơn giản không đủ.

### 2. Skills để tương tác với knowledge

Skill là structured interaction giữa người và AI. Thay vì prompt ad-hoc ("viết cho tôi API quản lý user"), skill guide bạn qua quá trình có cấu trúc.

Bạn chỉ cần 5 skills cơ bản:

**Discover** — AI đóng vai facilitator, giúp bạn extract knowledge từ trong đầu ra ngoài. Không phải AI dạy bạn — AI hỏi đúng câu hỏi để bạn tự trả lời. "Khi customer cancel đơn sau khi đã ship, chuyện gì xảy ra?" Bạn trả lời, AI ghi lại có cấu trúc, bạn confirm, knowledge vào store.

**Decide** — Ghi lại quyết định kèm lý do. Không chỉ "dùng Redis" mà "dùng Redis vì cần cache với TTL, đã cân nhắc Memcached nhưng thiếu data structures, cân nhắc local cache nhưng cần shared across instances." Khi 6 tháng sau ai đó hỏi "tại sao dùng Redis?" — câu trả lời nằm sẵn trong knowledge store.

**Plan** — Lấy knowledge từ store, lắp ráp thành context cho AI execution. "Iteration này build tính năng payment. Knowledge liên quan: business rules về refund, quyết định dùng Stripe, ràng buộc về PCI compliance, bài học từ lần trước implement payment ở project khác."

**Retro** — Sau mỗi iteration, hỏi: "cái gì sai? tại sao? encode rule gì để không sai lại?" Output đi thẳng vào knowledge store dưới dạng constraints hoặc failure patterns.

**Query** — Hỏi bất kỳ thứ gì về knowledge store. "Những ràng buộc nào liên quan đến module payment?" "Quyết định nào đã được đưa ra về authentication?" "Những sai lầm nào đã xảy ra với frontend testing?"

Năm skills này đủ cho mọi loại project. Khi bạn nhận ra pattern mới ("mỗi lần reverse-engineer legacy code cần extract business rules"), bạn tạo skill mới (`/reverse-discover`). Framework không predict skills cho bạn — framework cho bạn mechanism tạo skill khi cần.

### 3. Feedback loop: execution → knowledge

Đây là thứ biến hệ thống từ tĩnh thành sống. Mỗi lần AI execute, kết quả phải feedback về knowledge store:

- Test fail → tại sao? → knowledge thiếu gì? → bổ sung
- Agent assume sai → assumption nào? → ghi explicit vào knowledge
- Code review phát hiện pattern xấu → tạo constraint mới
- Project hoàn thành → retro → bài học → knowledge cho project sau

Hệ thống không thông minh hơn vì model mới hơn. Hệ thống thông minh hơn vì **mỗi sai lầm được encode thành knowledge** cho lần sau.

### Knowledge Decay: khi rules trở nên lỗi thời

Knowledge tích lũy — nhưng cũng decay. API behavior ghi 6 tháng trước có thể đã thay đổi. Business rule encode ở iteration 3 có thể đã bị supersede bởi regulation mới. Knowledge gắn với external systems đặc biệt dễ vỡ.

Không cần hệ thống phức tạp để xử lý. Ba practices đơn giản:

**Retro là decay detector tự nhiên.** Khi AI follow rule đúng nhưng output vẫn sai — đó là signal. Rule đã lỗi thời, không phải AI. Retro nên luôn hỏi: "có rule nào đã có đang dẫn mình đi sai?"

**Đánh dấu external knowledge với freshness.** Knowledge phụ thuộc vào external systems (API behaviors, third-party tool versions, regulatory requirements) nên ghi rõ lần cuối verify: "Shopee webhook delay: 5-30 giây (verified 2025-01-15, API v2.3)." Khi context thay đổi — API version mới, regulation mới — bạn biết knowledge nào cần recheck trước.

**Nguyên tắc đơn giản:** nếu AI follow rule đúng mà output vẫn sai → rule cần update, không phải AI cần fix.

---

## Vòng lặp

Chỉ có 1 vòng lặp duy nhất:

```
Knowledge → Execute → Feedback → Knowledge (updated)
```

Mọi thứ trong approach này đều là manifestation của vòng lặp đó.

Bạn discover domain knowledge → AI execute → test fail → bạn nhận ra spec thiếu edge case → update knowledge → AI execute lại → pass. Đó là vòng lặp với execution = AI generate code, feedback = test result.

Bạn đọc lại 2 constraints đã có → nhận ra chúng imply thêm 1 rule mới → thêm vào knowledge store. Đó là vòng lặp với execution = suy nghĩ, feedback = insight. Không cần AI agent chạy.

Hai người làm song song, cả hai update knowledge → conflict → resolve → knowledge nhất quán. Đó là vòng lặp với feedback = conflict signal.

Project mới, knowledge store trống → discover intensive → knowledge đầu tiên vào store → plan iteration đầu tiên. Đó là vòng lặp lần đầu tiên chạy.

Không cần nhớ "có bao nhiêu loại loop." Chỉ cần nhớ: **mọi execution đều kết thúc bằng knowledge được update.** Nếu bạn execute mà knowledge store không thay đổi — bạn đang mất thông tin. Nếu knowledge store thay đổi sau mỗi execution — hệ thống đang học.

Iteration đầu tiên luôn rough — vì knowledge store gần như trống. Mỗi vòng lặp, knowledge giàu hơn, output chính xác hơn. Một dự án thực tế: iteration 0 chất lượng 84%, iteration 21 chất lượng 100% — cùng AI, cùng model, chỉ khác knowledge đã tích lũy qua 21 vòng lặp.

---

## Áp dụng cho bất kỳ lĩnh vực nào

### Bước 1: Hỏi "knowledge gì quan trọng nhất cho việc này?"

Mỗi lĩnh vực có loại knowledge khác nhau:

**Phát triển phần mềm:** business rules, domain models, technical constraints, API behaviors, architectural decisions, failure patterns.

**Content & Marketing:** brand voice, target audience behaviors, competitive positioning, channel-specific constraints, performance data từ campaigns trước.

**Operations & Process:** workflow rules, exception handling procedures, compliance requirements, supplier behaviors, SLA commitments.

**Research & Analysis:** methodology standards, data source characteristics, bias patterns, terminology definitions, previous findings.

**Product Development:** user pain points, market assumptions (validated/unvalidated), technical feasibility findings, competitor behaviors.

Không cần biết hết từ đầu. Hỏi: **"nếu AI không biết thứ gì, nó sẽ assume sai nhất?"** Đó là knowledge cần capture đầu tiên.

### Bước 2: Tạo skill phù hợp cho cách discover knowledge đó

Knowledge khác nhau cần cách discover khác nhau:

- Business rules → **phỏng vấn domain expert** (AI hỏi, expert trả lời)
- API behaviors → **thử nghiệm và ghi log** (thử call API, observe behavior, ghi lại)
- Legacy business logic → **đọc code và extract** (AI đọc code, propose rules, human verify)
- User experience → **observation** (xem user dùng, ghi lại pain points)
- Technical feasibility → **spike/prototype** (build nhỏ, đo performance, ghi kết luận)
- Market knowledge → **research và validate** (AI tổng hợp data, human validate assumptions)
- Process knowledge → **walk through với người vận hành** (AI hỏi từng bước, ghi lại exceptions)

Mỗi cách discover có thể trở thành 1 skill khi bạn nhận ra mình lặp lại cách đó nhiều lần. Tạo skill khi bạn thấy pattern — không cần tạo trước.

### Bước 3: Thiết lập feedback loop

Hỏi: "khi execution xảy ra, kết quả feedback về knowledge store bằng cách nào?"

Đơn giản nhất: sau mỗi iteration, chạy retro, ghi bài học. Phức tạp hơn: automated monitoring detect khi knowledge outdated (API behavior thay đổi, schema drift).

Không cần hoàn hảo từ đầu. Bắt đầu bằng manual retro. Automate khi nhận ra pattern lặp lại.

### Bước 4: Cho AI execute với knowledge đã có

Đây là bước mà phần lớn người bắt đầu — và đó là sai. Nó phải là bước cuối. Khi knowledge đã đủ, execution gần như tự động. Khi knowledge thiếu, execution tốn gấp nhiều lần.

Execution có thể dùng bất kỳ tool nào phù hợp với công việc — Claude Code, Cursor, hay bất kỳ AI tool nào đọc được context từ knowledge store. Framework không ràng buộc vào tool cụ thể.

### Bước 5: Mỗi sai lầm = 1 rule mới

Đây là bước quan trọng nhất và cũng là bước dễ skip nhất.

Khi execution fail: đừng chỉ fix code. Hỏi: "tại sao fail? knowledge nào thiếu? rule nào cần thêm để không fail lại?"

Encode câu trả lời thành constraint hoặc convention trong knowledge store. Agent tiếp theo đọc rule → không mắc lỗi tương tự. Hệ thống tích lũy wisdom qua thời gian.

Một dự án bắt đầu với 0 constraints. Sau 21 iterations: 33 constraints, mỗi cái có ghi rõ "rule này ra đời từ sai lầm nào ở iteration nào." Người mới join đọc 33 constraints = nhận được kinh nghiệm tích lũy từ 21 iterations mà không cần trải qua.

---

## Thay đổi vai trò

### Người thực thi → Người own knowledge

Dù bạn là developer, marketer, analyst, hay operations manager — vai trò thay đổi cùng pattern: bạn không phải người **làm** output nữa. AI làm output. Bạn là người **đảm bảo AI có đủ knowledge để làm đúng**, và **verify output đúng với knowledge đã define.**

Trong phát triển phần mềm: developer không viết code — developer own knowledge quality, điều phối AI execution, review output. Viết code? AI lo. Hiểu business logic để biết "đúng" trông như thế nào? Developer lo. Nhận ra pattern để tạo rule mới? Developer lo.

Trong marketing: marketer không viết content — marketer own brand knowledge, audience insights, campaign learnings. AI viết draft, marketer verify nó đúng tone, đúng audience, đúng facts.

Pattern giống nhau ở mọi lĩnh vực: **con người chuyển từ executor sang knowledge owner + quality gatekeeper.**

### Mọi người đều là knowledge contributor

Sự khác biệt giữa team dùng AI tệ và team dùng AI tốt: team tệ để 1 người prompt AI. Team tốt để **mọi người contribute knowledge** vào cùng knowledge store — business analyst contribute business rules, developer contribute technical constraints, tester contribute failure patterns, domain expert contribute nghiệp vụ, operations contribute real-world behaviors.

AI dùng toàn bộ knowledge đó để execute. Càng nhiều góc nhìn, knowledge càng comprehensive, output càng chính xác. Knowledge không phải trách nhiệm của 1 người — nó là tài sản chung của team.

---

## Knowledge Governance

Khi chỉ 1 người contribute knowledge, governance không cần bàn. Khi 10 người contribute, conflict sẽ xuất hiện. Hai người encode rules mâu thuẫn. Ai đó update decision mà không ghi lý do. Knowledge tích lũy nhưng không ai biết phần nào còn đáng tin.

Section này không phải governance framework — mà là 3 principles nhẹ nhàng ngăn chặn những vấn đề phổ biến nhất mà không thêm bureaucracy.

### Ownership

Mỗi knowledge area có 1 owner. Business rules → BA hoặc product owner. Technical constraints → tech lead. Failure patterns → người chạy retro.

Owner không approve mọi entry — đó sẽ là bottleneck. Owner là **người cuối cùng khi conflict xảy ra.** Phần lớn knowledge vào store không có conflict. Owner chỉ activate khi hai rules mâu thuẫn hoặc khi ai đó challenge rule hiện tại.

### Conflict Resolution

Khi hai rules mâu thuẫn:

1. Rule nào có **context rõ hơn thắng** — context nghĩa là: lý do được ghi, evidence đính kèm, source được xác định. "Dùng Redis vì cần TTL + shared cache across instances" thắng "dùng Memcached" không có lý do.
2. Nếu context quality ngang nhau → **escalate lên area owner.** Owner quyết định, ghi reasoning, update rule thua.
3. Conflict đã resolve cũng trở thành knowledge — ghi lại cái gì mâu thuẫn và tại sao rule nào thắng. Điều này ngăn cùng conflict tái xuất hiện.

### Truy vết thay đổi

Khi knowledge thay đổi, ghi rõ nó thay thế cái gì:

```
"Mọi tính toán tiền tệ phải dùng decimal precision theo currency."
Thay thế: "Dùng 2 decimal places cho mọi giá trị tiền tệ" (iteration 14)
Lý do: JPY dùng 0 decimals, BHD dùng 3. Phát hiện khi implement payment module.
```

Không phải thay đổi nào cũng cần chi tiết đến vậy. Dùng khi rule trước **đang được follow tích cực** — để người đã học rule cũ hiểu tại sao nó thay đổi.

---

## Khi nào KHÔNG dùng cách này

Transparent: approach này có overhead. Nếu overhead lớn hơn giá trị, đừng dùng.

**Quick prototype cần validate trong 1 ngày** — just prompt AI, xem kết quả, decide. Capture vài ghi chú nếu prototype thành công và cần build thật.

**Task quá đơn giản** — "viết email xác nhận đơn hàng" hay "tạo endpoint CRUD cho 1 entity" không cần knowledge ceremony. Prompt đủ rõ, AI tạo đúng.

**Bạn đã expert hoàn toàn trong domain** — knowledge đã ở trong đầu bạn, và task đủ nhỏ để bạn describe đầy đủ trong 1 prompt. Không cần external knowledge store cho cái bạn đã biết rõ và diễn tả được.

**Output sai dễ sửa** — nếu sai rồi fix 5 phút, đừng dành 30 phút capture knowledge.

Nguyên tắc: **dùng khi cost of getting it wrong > cost of knowledge ceremony.** Nếu sai rồi rework 2 tuần, dành 2 ngày capture knowledge là đầu tư xứng đáng. Ranh giới này bạn tự cảm nhận — và cảm nhận chính xác hơn qua kinh nghiệm.

---

## Bắt đầu từ đâu

### Ngày 1

Tạo 1 folder `knowledge/` trong project. Tạo 3 files:

- `decisions.md` — mỗi quyết định kỹ thuật quan trọng, kèm lý do
- `constraints.md` — rules mà mọi người (và AI) phải follow
- `glossary.md` — thuật ngữ project, nghĩa thống nhất

Đó là knowledge store v1. Đủ để bắt đầu.

### Tuần 1

Khi dùng AI thực hiện task, trước mỗi task: đọc `constraints.md`, cung cấp relevant rules làm context cho AI. Sau mỗi task: nếu AI sai gì, thêm 1 rule vào `constraints.md`.

Cuối tuần: bạn sẽ có 5-10 constraints tích lũy. AI bắt đầu sai ít hơn.

### Tháng 1

Pattern sẽ emerge:
- Bạn thấy mình lặp đi lặp lại cùng prompt template khi discover → tạo skill
- Bạn thấy constraints file dài → tổ chức lại thành categories
- Bạn thấy nhiều người cần đọc cùng knowledge → cần shared access
- Bạn thấy AI cần programmatic access → cần MCP

Thêm complexity chỉ khi pain thực sự xuất hiện. Đừng build infrastructure trước khi cần.

### Tháng 3

Knowledge store đã có 30+ constraints, hàng chục decisions, multiple team members contribute. Bạn bắt đầu thấy: new team member join, đọc knowledge store 1 ngày, productive ngay ngày thứ 2 vì knowledge đã externalized. AI produce output chất lượng cao hơn hẳn so với tháng 1. Khi bắt đầu project mới, bạn mang theo applicable knowledge (constraints, conventions, decisions) → head start thay vì bắt đầu từ 0.

Đó là Overmind hoạt động.

---

## Tóm lại

Không phải tool. Không phải process. Là cách nghĩ.

**Trước khi hỏi "AI execute thế nào?" → hỏi "AI biết gì?"**

**Trước khi fix output sai → hỏi "knowledge nào thiếu?"**

**Trước khi tạo process phức tạp → hỏi "pattern gì đang lặp lại?"**

Mỗi sai lầm là cơ hội encode 1 rule mới. Mỗi rule mới là 1 lần hệ thống thông minh hơn. Sau đủ vòng lặp, hệ thống biết gần hết những gì cần biết — và AI produce output đúng gần như mặc định.

Bắt đầu đơn giản. 1 folder, 3 files. Phức tạp hóa khi pain đòi hỏi. Tin vào quá trình: iteration đầu rough, iteration thứ 10 smooth, iteration thứ 20 gần như tự động.

Knowledge-first. Execution-last. Humans recognize patterns. AI follows rules. Mỗi vòng lặp, cả hai tốt hơn.
