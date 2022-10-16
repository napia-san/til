# [SQL]Data processing
以下のテーブルに対するクエリを例示する<br>
[Table] users
| id | class | level | name | age | sex | last_update |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 1 | A | 48 | Edwin | 28 | M | 2022-10-08 |
| 2 | C | 13 | Nancy | 21 | W | 2022-09-18 |
| 3 | B | 41 | Napia | 24 | M | 2022-10-16 |
| 4 | A | 87 | Kiana | 38 | W | 2022-06-23 |
| 5 | B | 38 | Phill | 41 | M | 2022-09-03 |
<br>

## 重複を除去して取得する
SELECT DISTINCT(カラム名):重複したカラムを除外して昇順に取得<br>
[Sample]
```
SELECT DISTINCT(class)
FROM users
ORDER BY class ASC;
```
<br>

## データの計算
 - `SELECT <カラム名>` `[+` `-` `*` `/]` `<任意の数>`:四則計算してデータ取得
 - `SELECT SUM(<カラム名>)`:特定のカラムの総和を出力
 - `SELECT AVG(<カラム名>)`:特定のカラムの平均を出力
 - `SELECT MAX(<カラム名>)`/`MIN(<カラム名>)`:特定のカラムの最大値/最小値を出力
 - `SELECT COUNT(<カラム名>)`:特定のカラムのデータ数を出力(NULLはカウントしない)
 - `SELECT COUNT(*)`:テーブルのレコード数を出力<br>

[Query]
```
SELECT AVG(age), MAX(level), COUNT(*)
FROM users
WHERE class = "A"; //計算対象を絞り込める
```
[Responce]
| AVG(age) | MAX(level) | COUNT(*) |
| :-: | :-: | :-: |
| 33 | 87 | 2 |
<br>

## グループごとに集計する
`GROUP BY`を使えば，特定のカラムをグループ化して集計できる．<br>
[Query]
```
SELECT COUNT(*), sex
FROM users
//この行にWHEREを使えば，絞り込みも行える
GROUP BY sex; //複数指定すれば全ての組み合わせにおける結果が出力される
```
＊このときSELECTできるのは，集計結果と絞り込みに使ったカラムのみ<br><br>
[Response]
| COUNT(*) | sex |
| :-: | :-: |
| 3 | M |
| 2 | W |
<br>

`HAVING <条件式>`:グループ化した後に絞り込みしたいときに使う