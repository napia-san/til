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