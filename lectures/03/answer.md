# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：
- `--trace` で見えたツール呼び出し（ツール名と引数）：search\_glossary({'query': 'LoRA'}) と search\_glossary({'query': 'QLoRA'})
- 1つの質問での LLM 呼び出し回数（`requests`）：2回
- ## 追加したツールと、docstring に書いた説明：
  ```
  make\_quiz(lecture: int)
  
  「指定した回の確認問題を1問出してほしいときに使う。問題と答えを返す。」
  
  第2回の確認問題を頼むと make\_quiz({'lecture': 2}) が呼ばれ、
  
  「学習率」の問題が出た。requests=2、tool\_calls=1。
  
  テストは11件すべて合格。
  ```

## 宿題

- - 取り組んだレベル：基礎
- やったこと：

  INSTRUCTIONS の「回答の最後に、関係する回（第N回）を示す」を

  「回答の最後に、理解を確かめる確認問題を1問出す」に変更し、

  同じ「LoRAとQLoRAの違いは？」を --trace 付きで実行した。
- 結果：

  変更前後とも、LoRAとQLoRAを search\_glossary で個別に検索した。

  変更後は make\_quiz({'lecture': 2}) が追加で呼ばれ、

  「事前学習」の確認問題が出た。

  tool\_calls は2回から3回、requests も2回から3回に増えた。
- 気づき・疑問：

  指示を1か所変えると、回答だけでなく使うツールも変わった。

  make\_quiz は指定した回からランダムに選ぶため、

  質問した用語に直接関係する問題が出るとは限らない。



### 追加：発展（a）

- やったこと：

  同じ INSTRUCTIONS と3つのツールを使い、Google ADK版を作成した。

  「LoRAとQLoRAの違いは？」と質問し、Pydantic AI版と比較した。

- 結果：

  ADK版でも両者の違いを説明し、最後に確認問題を出した。

  Pydantic AIは instructions と tool_plain、

  ADKは instruction と tools リストで指示・ツールを渡した。

- 気づき・疑問：

  同じ指示と関数を別のフレームワークでも利用できた。

  ADKの通常出力ではツール呼び出し履歴が見えなかったため、

  回答だけでは実際の呼び出しを確認できなかった。

