# 書籍編集画面

## 概要

書籍の編集を行う。

## 画面イメージ

![編集画面](images/screen/edit.png)

## 画面項目

| 項目名       | タイプ         | 取得元/保存先                              | フォーマット |
| :----------- | :------------- | :----------------------------------------- | :--- |
| 書籍ID       | ラベル         | 書籍情報.書籍ID                         | -    |
| タイトル     | テキスト       | 書籍情報.タイトル                       | -    |
| 著者         | テキスト       | 書籍情報.著者                           |      |
| 出版社       | テキスト       | 書籍情報.出版社ID<br>=>出版社マスタ.名称         | -    |
| 価格         | テキスト       | 書籍情報.価格                           | -    |
| 購入日       | テキスト       | 書籍情報.購入日                         | yyyy/MM/dd    |
| 書籍管理部署 | ドロップダウン | 書籍情報.書籍管理部署ID<br>=>部署マスタ.部署名 | -    |
| 更新日       | ラベル         | 当日日付                                   | yyyy/MM/dd    |
| 更新者       | ラベル         | ログイン情報.ユーザ名                      | -    |
| 更新者部署   | ラベル         | ログイン情報.ユーザ部署名                  | -    |
| 戻る         | ボタン         | -                                          | -    |
| 登録         | ボタン         | -                                          | -    |

## アクション

### 初期表示時

1. リクエストパラメータより取得した書籍IDを用いて、書籍情報を取得し、画面に表示する。
1. 出版社マスタより出版社の全件を取得し、出版社ドロップダウンに表示する。
1. 部署マスタより部署の全件を取得し、書籍管理部署ドロップダウンに表示する。
1. セッションからログインユーザ情報を取得し、画面の各項目に表示する。

### 戻るボタン押下時

1. [書籍一覧画面](list.md)に遷移する。

### 登録ボタン押下時

1. 入力チェックを実施する
2. 【入力エラーがある場合】
    1. エラーの内容を画面に表示し、以降のアクション内処理を中断する。
3. 確認ダイアログを表示する。「登録します。よろしいですか？」
4. 【「はい」以外が選択された場合】
    1. 以降のアクション内処理を中断する。
5. 画面の入力項目及び、以下の情報から書籍情報の登録処理を行う。
    - 更新者：ログイン情報.ユーザID
    - 更新日：本処理の実行時間
    - 更新者部署ID：ログイン情報.部署ID
6. 【登録に失敗した場合】
    1. メッセージ「サーバにてエラーが発生しました。」を表示し、以降のアクション内処理を中断する。
2. メッセージ「登録に成功しました。」を表示し、[書籍詳細画面](detail.md)に遷移する。[※1]

#### ※1・・・処理順序について

- メッセージの表示タイミングと表示方式は問わない
- 画面遷移とメッセージ表示の順序は前後しても構わない
- ただし、利用者がメッセージを見失わないように留意すること


## 入力チェック

| 項目名 | 必須 | 最小桁数 | 最大桁数 | フォーマット |　備考 |
|:-|:-:|:-:|:-:|:-|:-|
| タイトル | 〇 | 1 | 20| - | |
| 著者 | 〇 | 1 | 20 | -|  |
| 出版社 | 〇 | - | - | -| |
| 価格 | 〇 | 2 | - | 数値のみ | |
| 購入日 | 〇 | - | - | yyyy/MM/dd | |
| 書籍管理部署 | 〇 | - | - | -| |
