# [JS]JavaScriptの基本文法[Oct.26.2022]

## 変数の定義
### 変数
`let box;` : 変数(`box`)の定義<br>
型の定義は必要無い．<br>
`box = 'A';` : 変数への代入<br>
＊`let box = 'A';`こんな感じで定義と代入を同時に行うこともできる．
<br>

### 配列
以下で定義可能．
```
let box = [
	'Apple',
	'Bagle',
	'Canon',
	'Drive',
];
```
<br>

### 定数
`const box;` : で定義できる．
<br><br>

***
## 出力
`console.log(box);` : コンソール上に出力される．末尾には改行あり．<br>
`alert(box);` : ダイアログボックスに表示．<br>
`console.log(box[2]);` : 配列の2番目の要素を出力．<br>
`box.forEach(word => console.log(word));` : 配列内の要素全てを一行ずつ出力．<br>
`box.forEach(word => console.table(word));` : 配列内の要素全てを表の形で出力．<br><br>

***
## オブジェクト
オブジェクトとは：Cで言う構造体みたいなもの．<br>
### 定義
```
const user = {
	id: 2,
	name: {
		first_name: 'masatoshi',
		last_name: 'suzuki'
	},
	age: 28
};
```
### 出力
`console.log(user.age);` : `age`の出力<br>
`console.log('id:' + user.id + ', name:' + user.name.first_name);` : `id`と`first_name`の出力<br>

***
## 関数
### 定義
[Sample] BMIを計算する関数
```
function calc_bmi(height, weight) {
	return weight / (height ** 2);
}
```
### 呼び出し
`console.log(calc_bmi(1.67, 63));`