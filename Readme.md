### 名称
mbed_compile_database_creator

### 概要
mbedで生成したmakefileプロジェクトから, VSCodeなどで使用できる, <br>
compile_commands.jsonを生成する, pythonスクリプト

### 前提
python3.7以降 <br>
mbedプロジェクトは, makeが通ること前提 <br>
mbedプロジェクトは, cleanされている前提 <br>

### 使い方
mbedから, GNU-GCC-MAKEでプロジェクトをエクスポートし, 展開後, <br>
プロジェクト配下に, 本リポジトリのpythonスクリプトを置く. <br>
その後, makefileのうち, <br>
@$(AS) -c $(ASM_FLAGS) -o $@ $< <br>
@$(CC) $(C_FLAGS) $(INCLUDE_PATHS) -o $@ $< <br>
@$(CCP) $(CXX_FLAGS) $(INCLUDE_PATHS) -o $@ $< <br>
の行頭の@を削除する. <br>
make >Make.logを実行し, Make.logを生成する. <br>
最後に, pythonスクリプトを走らせれば, compile_commands.jsonが生成される. <br>
生成されたjsonは, directoryの設定が間違っているので, ここを手動で調整する. <br>

### 残存問題
1 makefileによる移動先ディレクトリを認識していない <br>
  makefile内での, ディレクトリ移動を認識していないため, <br>
  生成後にjsonファイル内の, directoryを手動で調整する必要がある <br>
<br>
2 makefileのログファイルを生成しなければならない <br>
  makefileのログファイルとして, Make.logを読む構造のため, <br>
  毎回ログファイルを作成しなければならない <br>
<br>
3 makefileのメッセージ抑制の@を手動で消さなければならない <br>
  mbedが生成するmakefileは, コマンド実行内容の出力を@で抑制しているので, <br>
  外部からログが見えない. そのため, makefileを手動で@を削除する必要がある. <br>

