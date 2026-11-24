# 第6回 解答

## 演習

<!-- [tool call] の行は、表示された行をそのまま貼り付けてください。終わらなかった STEP は、空欄のままでかまいません。 -->

- STEP 1 のツールの名前：glossary_search_glossary
- STEP 2 の [tool call]：[tool call] glossary_search_glossary ({'query': '3レベル'})
- STEP 3 の [tool call]：[tool call] fetch_fetch({'url': 'https://modelcontextprotocol.io/'})
- STEP 4 の [tool call]：[tool call] aws_aws_search_documentation({'topics': ['general'], 'search_phrase': 'Amazon S3 versioning overview'})
- 気づき・疑問：MCPサーバーを経由すると、ローカル実行（command）と外部接続（url）のどちらのツールもモデルには「サーバー名_ツール名」の形式で同じように認識され、エージェント本体のコードを変更せずに機能を拡張できると分かった。

## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎
- やったこと：`app/mcp_server.py` の TODO コメントの下に `server.tool()(tools.get_lecture_summary)` を1行追加し、ツール一覧の確認、第2回の講義内容に関する質問実行（`--trace` 付き）、および `uv run pytest -q` によるテストを実施した。
- 結果：`--list-tools` で認識されるツール数が7個から8個に増え、`glossary_get_lecture_summary` が追加された。質問に対して `[tool call] glossary_get_lecture_summary({'lecture': 2})` が正しく呼ばれ、第2回（ファインチューニングとLoRA）の要点を回答できた。`pytest` も `21 passed` で全件通過した。
- 気づき・疑問：エージェント側（`app/mcp_agent.py` や `app/mcp_servers.json`）を一切変更しなくても、起動時にMCPサーバーから最新のツール一覧を自動取得するため、サーバー側の修正だけで新ツールが即座に利用できる点が便利だと感じた。