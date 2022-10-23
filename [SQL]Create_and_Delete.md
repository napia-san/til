# [SQL]データの追加削除更新[Oct.23.2022]

## レコードの挿入
`INSERT`を使用すれば，レコードの挿入が行える<br>
【Usage】
```
INSERT INTO <テーブル名>(<カラム名1>, <カラム名2>, ...)
VALUES(<カラム名1に対応する値>, <カラム名2に対応する値>, ...)
```
＊`AUTO INCREMENT`のカラムはについては，記述しない<br><br>
[Sample1] テーブルへレコードの挿入を行う
```
INSERT INTO students(id, name, course)
VALUES(4, "Yamada", "International");
```
<br>

## データの更新
`UPDATE`を使用すれば，データの更新がおこなえる<br>
【Usage】
```
UPDATE <テーブル名>
SET <変更先カラム名> = <新しい値>
WHERE <変更先でないカラム名(変更先レコードの指定)> = <値>
```
＊`WHERE`で変更先の指定を行わないと，全てのレコードに反映されてしまうので注意．<br><br>
[Sample2] レコードに変更を加える
```
UPDATE students
SET name = "Tanaka"
WHERE id = 4;
```
<br>

## レコードの削除
`DELETE`を使う．<br>
[Sample3]レコードの削除
```
DELETE FROM students
WHERE id = 4;
```
＊こちらも，`WHERE`で条件の指定がないと，全て削除されてしまうので注意．