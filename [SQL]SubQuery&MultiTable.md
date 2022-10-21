# [SQL]Sub Query & Multi Table[Oct.19.2022]

## サブクエリ
クエリの中にクエリを入れることを言う．
サブクエリはその外側のクエリより先に実行される．<br><br>

以下のテーブルに対するクエリを例示することとする<br>
[Table] players
| id | name | score | age |
| :-: | :-: | :-: | :-: |
| 1 | Andy | 190 | 23 |
| 2 | Buzz | 890 | 38 |
| 3 | Duffy | 140 | 4 |
| 4 | Daisy | 280 | 28 |
| 5 | Belle | 630 | 34 |
| 6 | Chris | 390 | 10 |
| 7 | Ben | 870 | 25 |
| 8 | Mike | 500 | 31 |

[Sample1] `score`が`Mike`より高い人の`name`と`id`を出力する
```
SELECT id, name
FROM players
WHERE score > (
  SELECT score
  FROM players
  WHERE name = "Mike" //サブクエリの末尾にはセミコロン不要
);
```

[Sample2] `score`が平均以上の人のデータを表示する．
```
SELECT *
FROM players
WHERE score > (
  SELECT AVG(score)
  FROM players
);
```

## Responseの可読性向上
`AS`:カラム名の書き換え<br>
さまざまな条件で絞り込んだとき，カラム名がデフォルトのままだと，何が何だかわからなくなる．わかりやすくするためにカラム名を書き換えて出力することがある．

[Sample3] `score`が平均以上の人のidを表示する．
```
SELECT id AS "平均点を超えた人のid"
FROM players
WHERE score > (
  SELECT AVG(score)
  FROM players
);
```
<br>

## テーブル同士の結合
テーブルが2つあるとする．
[Table1] players
| id | name | score | age | ex_class_id |
| :-: | :-: | :-: | :-: | :-: |
| 1 | Andy | 190 | 23 | 1 |
| 2 | Buzz | 890 | 38 | 3 |
| 3 | Duffy | 140 | 4 |   |
| 4 | Daisy | 280 | 28 |   |
| 5 | Belle | 630 | 34 | 1 |
| 6 | Chris | 390 | 10 | 2 |
| 7 | Ben | 870 | 25 |   |
| 8 | Mike | 500 | 31 | 2 |
<br>

[Table2] classes
| id | name |
| :-: | :-: |
| 1 | A |
| 2 | B |
| 3 | C |
<br>

テーブルを分けておけば，変更が生じたときの手間が省ける．<br>
`players`の`ex_class_id`カラムの値は，`classes`の`id`と関連付けされている．
このとき，前者を`外部キー`，後者を`主キー`と呼ぶ．<br>

[Sample4] 二つのテーブルを結合して出力
```
SELECT *
FROM players
JOIN classes
ON players.ex_class_id = classes.id;
```
[Response]
| id | name | score | age | ex_class_id | id | name |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 1 | Andy | 190 | 23 | 1 | 1 | A |
| 2 | Buzz | 890 | 38 | 3 | 3 | C |
| 5 | Belle | 630 | 34 | 1 | 1 | A |
| 6 | Chris | 390 | 10 | 2 | 2 | B |
| 8 | Mike | 500 | 31 | 2 | 2 | B |
<br>

このように`ex_class_id`が`NULL`となっているレコードは除外して出力される．<br>
[Sample5] `NULL`でも出力させる(`LEFT JOIN`を使う)
```
SELECT *
FROM players
LEFT JOIN classes
ON players.ex_class_id = classes.id;
```
[Response]
| id | name | score | age | ex_class_id | id | name |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 1 | Andy | 190 | 23 | 1 | 1 | A |
| 2 | Buzz | 890 | 38 | 3 | 3 | C |
| 3 | Duffy | 140 | 4 |   |   |   |
| 4 | Daisy | 280 | 28 |   |   |   |
| 5 | Belle | 630 | 34 | 1 | 1 | A |
| 6 | Chris | 390 | 10 | 2 | 2 | B |
| 7 | Ben | 870 | 25 |   |   |   |
| 8 | Mike | 500 | 31 | 2 | 2 | B |
<br>

## 複数のテーブルの結合
テーブルが3つあるとする．<br>
[Table1] players
| id | name | score | age | ex_class_id | nationality_id |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 1 | Andy | 190 | 23 | 1 | 1 |
| 2 | Buzz | 890 | 38 | 3 | 1 |
| 3 | Duffy | 140 | 4 |   | 4 |
| 4 | Daisy | 280 | 28 |   | 1 |
| 5 | Belle | 630 | 34 | 1 | 3 |
| 6 | Chris | 390 | 10 | 2 | 2 |
| 7 | Ben | 870 | 25 |   | 2 |
| 8 | Mike | 500 | 31 | 2 | 3 |
<br>

[Table2] classes
| id | name |
| :-: | :-: |
| 1 | A |
| 2 | B |
| 3 | C |
<br>

[Table3] nationalities
| id | name |
| :-: | :-: |
| 1 | The USA |
| 2 | Canada |
| 3 | France |
| 4 | Japan |
<br>

[Sample6] 3つとも結合する<br>
`JOIN` or `LEFT JOIN`を複数回使用する．
```
SELECT players.name, score, classes.name AS "前のクラス", nationalities.name AS "国籍"
FROM players
LEFT JOIN classes
ON players.ex_class_id = classes.id
JOIN nationalities
ON players.nationality_id = nationalities.id;
```
[Response]
| id | name | score | 前のクラス | 国籍 |
| :-: | :-: | :-: | :-: | :-: |
| 1 | Andy | 190 | A | The USA |
| 2 | Buzz | 890 | C | The USA |
| 3 | Duffy | 140 |   | Japan |
| 4 | Daisy | 280 |   | The USA |
| 5 | Belle | 630 | A | France |
| 6 | Chris | 390 | B | Canada |
| 7 | Ben | 870 |   | Canada |
| 8 | Mike | 500 | B | France |
<br>