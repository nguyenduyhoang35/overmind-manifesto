# Overmind — Properties

> Đây không phải rules. Đây là những tính chất tự nhiên emerge khi follow Overmind manifesto.
> Bạn không cần cố đạt chúng — chúng xuất hiện khi principles được áp dụng đúng.
> Nếu bạn không thấy chúng xuất hiện, đó là tín hiệu gì đó trong cách áp dụng cần xem lại.

---

## Self-improving

Hệ thống tự cải thiện qua thời gian mà không cần thay đổi model hay tool. Mỗi execution sinh feedback, feedback trở thành knowledge, knowledge cải thiện execution tiếp theo.

Chất lượng là function của knowledge completeness, không phải model capability. Cùng AI, cùng model — iteration 0 cho 84% chất lượng, iteration 21 cho 100% — khác biệt hoàn toàn đến từ knowledge đã tích lũy.

## Failure-positive

Sai lầm có giá trị dương vì mỗi failure sinh ra knowledge mới. Hệ thống không bao giờ fail cùng cách hai lần. Fail sớm rẻ hơn fail muộn. Iteration đầu rough là tín hiệu tốt — hệ thống đang học nhanh.

Hệ quả: team không cần sợ sai. Cần sợ sai mà không capture lesson.

## Compounding knowledge

Knowledge tích lũy và compound theo thời gian. Constraint từ iteration 0 vẫn có giá trị ở iteration 21. Knowledge không depreciate như code hay tools — nó chỉ accumulate hoặc được refined.

Càng nhiều vòng lặp, knowledge store càng valuable. Returns tăng tốc theo thời gian, không giảm tốc.

## Transferable wisdom

Người mới join đọc knowledge store = nhận được kinh nghiệm tích lũy từ mọi iteration trước mà không cần trải qua. Knowledge tách khỏi cá nhân — không mất khi ai đó rời team.

Onboarding trở thành "đọc knowledge store" thay vì "ngồi cạnh senior 3 tháng."

## Emergent quality

Chất lượng không đến từ process enforcement mà emerge từ knowledge richness. Khi knowledge đủ comprehensive, output tự nhiên đúng mà không cần review nhiều lớp.

Process phức tạp là triệu chứng của knowledge thiếu. Khi thấy mình cần thêm gates và checkpoints, hỏi: "knowledge nào đang thiếu khiến output sai?"

## Knowledge > contributor

Knowledge store thông minh hơn bất kỳ individual contributor nào. Con người cung cấp domain truth, AI cross-reference với knowledge đã có, kết quả refined hơn cả input gốc.

Store tích lũy góc nhìn của mọi người qua thời gian — BA contribute business rules, developer contribute technical constraints, tester contribute failure patterns. Tổng thể lớn hơn tổng các phần.

## Tool-agnostic

Giá trị nằm ở knowledge, không ở tool. Đổi execution engine — knowledge store giữ nguyên giá trị. Tool là replaceable, knowledge là durable.

Hệ quả: đừng invest quá nhiều vào tool-specific optimization. Invest vào knowledge quality — nó portable theo bạn mọi nơi.

## Domain-agnostic

Cùng closed loop hoạt động cho software, marketing, operations, research, bất kỳ domain nào. Chỉ khác: knowledge types nào quan trọng và cách discover chúng.

Software cần business rules và technical constraints. Marketing cần audience insights và brand voice. Operations cần process rules và exception handling. Closed loop giống nhau — knowledge → execute → feedback → knowledge.

## Organic complexity

Complexity chỉ xuất hiện khi pain đòi hỏi, không từ upfront design. Bắt đầu 1 folder, 3 files. Thêm skills khi thấy pattern lặp. Thêm tooling khi scale đòi hỏi. Mỗi bước complexity có justification từ real pain.

Hệ quả: hai team áp dụng Overmind sẽ có tooling khác nhau vì pain points khác nhau. Đó là đúng, không phải inconsistency.

## Diminishing error rate

Error rate giảm asymptotically theo knowledge accumulation. Improvement lớn ở đầu — vài constraints đầu tiên eliminate hàng loạt lỗi phổ biến. Plateau dần khi knowledge đã cover phần lớn cases.

Không bao giờ đạt 0% error — nhưng mỗi error mới trở thành error cuối cùng thuộc loại đó.

## Knowledge decay

Knowledge có hạn sử dụng — đặc biệt knowledge gắn với external systems, third-party APIs, regulatory environments, hoặc thị trường biến động nhanh. Rule đúng 6 tháng trước có thể âm thầm trở nên sai.

Retro là cơ chế detect tự nhiên: khi AI follow rule đúng mà output vẫn sai, rule đã decay. Hệ thống không cần "knowledge review process" riêng — feedback loop đã surface stale knowledge thông qua execution failures.

Hệ quả: knowledge gắn với external systems nên có freshness markers ("verified [date], [version]"). Khi context thay đổi, bạn biết knowledge nào cần recheck trước — không cần audit toàn bộ.

## Portable across projects

Knowledge applicable cho project mới mang theo được. Constraints, conventions, decisions, failure patterns — nhiều thứ transcend project cụ thể.

Project thứ 2 không bắt đầu từ 0. Nó bắt đầu từ subset knowledge đã proven. Head start thay vì cold start.

## Scale-invariant principle

Cùng closed loop hoạt động cho 1 người hay 100 người. Team lớn hơn = nhiều knowledge contributors = store giàu hơn = output tốt hơn.

Không cần thêm management layers khi scale. Cần thêm governance cho knowledge store — nhưng principle không thay đổi.
