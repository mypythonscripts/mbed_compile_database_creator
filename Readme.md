### 名称
mbed_compile_database_creator

### 概要
mbedで生成したmakefileプロジェクトから, VSCodeなどで使用できる, 
compile_commands.jsonを生成する, pythonスクリプト

### 前提
python3.7以降
mbedプロジェクトは, makeが通ること前提
mbedプロジェクトは, cleanされている前提

### 使い方
mbedから, GNU-GCC-MAKEでプロジェクトをエクスポートし, 展開後, 
プロジェクト配下に, 本リポジトリのpythonスクリプトを置く. 
その後, makefileのうち, 
@$(AS) -c $(ASM_FLAGS) -o $@ $<
@$(CC) $(C_FLAGS) $(INCLUDE_PATHS) -o $@ $<
@$(CCP) $(CXX_FLAGS) $(INCLUDE_PATHS) -o $@ $<
の行頭の@を削除する. 
make >Make.logを実行し, Make.logを生成する. 
最後に, pythonスクリプトを走らせれば, compile_commands.jsonが生成される. 
生成されたjsonは, directoryの設定が間違っているので, ここを手動で調整する. 

### 残存問題
1 makefileによる移動先ディレクトリを認識していない
  makefile内での, ディレクトリ移動を認識していないため, 
  生成後にjsonファイル内の, directoryを手動で調整する必要がある

2 makefileのログファイルを生成しなければならない
  makefileのログファイルとして, Make.logを読む構造のため, 
  毎回ログファイルを作成しなければならない

3 makefileのメッセージ抑制の@を手動で消さなければならない
  mbedが生成するmakefileは, コマンド実行内容の出力を@で抑制しているので, 
  外部からログが見えない. そのため, makefileを手動で@を削除する必要がある. 

