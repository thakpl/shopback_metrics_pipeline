# AI Usage Reflection

Throughout this assignment, I utilized AI (Google Gemini) as a collaborative pair-programmer. Instead of generating the entire codebase at once, I used it to brainstorm data modeling logic, debug execution errors, and refine my documentation.

Below are the key instances where AI assisted in my development process:

| Task | Prompt or Question Used | Outcome / What You Learned |
| --- | --- | --- |
| **Designing SQL logic for `avg_order_revenue**` | "How to calculate average revenue per order by customer in DuckDB when raw data is split between `orders` and `order_items` tables?" | Realized the risk of data duplication when joining tables with one-to-many relationships. Learned to use `COUNT(DISTINCT o.order_id)` instead of a basic `COUNT()` to ensure accurate averages. |
| **Handling edge cases in YAML validation** | "My Python script crashes with `TypeError: 'NoneType' object is not subscriptable` when iterating through the `/metrics` folder. How do I fix this?" | Discovered that `yaml.safe_load()` returns `None` for empty files rather than an empty dictionary. Implemented `if metric is None:` and used `.get()` to safely handle missing files/keys, making the pipeline crash-proof. |
| **Debugging DuckDB execution errors** | "DuckDB throws `Catalog Error: Table does not exist` when trying to query the table at the end of the script, even though the code looks correct. What went wrong?" | Learned that running scripts using absolute paths from outside the project root causes relative path resolution failures (the script couldn't find the `/metrics` folder). Added a strict "Setup Instructions" section in the README to enforce the correct Current Working Directory (CWD). |
| **Structuring professional documentation** | "What is the standard structure for a data engineering project's README.md to ensure another analyst can easily use it?" | Improved my technical writing skills by organizing the README into clear, actionable sections (Prerequisites, Setup, Step-by-Step Metric Addition, and Guidelines), prioritizing a smooth handover process. |
