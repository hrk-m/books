# js es6

- forEach

  - 返り値は undifind
  - ex) フォームでチェックボックスで true なものを削除する等

- map

  - 返り値は配列
  - ex) 投稿に紐づけられたコメント一覧を取得するする時に

- filter

  - 返り値は配列
  - true になったものをすべて返す

- find

  - 返り値は配列
  - 一番初めに条件に引っかかったものを返す(rails でいう find_by)

- every

  - 返り値は boolean
  - rails でいう all?メソッド
  - すべて true の場合 true

- some

  - 返り値は boolean
  - rails でいう any?メソッド
  - ひとつでも true が有れば true

- reduce
  - 返り値は適宜きめられる(以下の場合は 0 数字)
  - rails でいう inject

```
[1, 2, 3].reduce((sum, number) => {
  return sum + number;
}, 0);
```

- テンプレートリテラル(式の展開)

  - `${xxxx}`

- アロー関数
  - const xxx = function() {} → const xxxx = () => {}
  - return を削除可能, const add = (a, b) => a + b;
  - 引数が一つだと, const double = a => a \* 2;

```js
const team = {
  members: ["太朗", "花子"],
  teamName: "スーパーチーム",
  teamSummary: function () {
    return this.members.map((member) => {
      return `${member}は${this.teamName}の所属です。`;
    });
  },
};
team.teamSummary();
```

- オブジェクトリテラル

```js
function createBook(name) {
  return {
    name,       #=> key とvalue が同じ場合に省略
    test: 'bbb',
    value() {   #=> value: function() { を省略
      return xxxxxx
    }
  }
}
new createBook('test');
```

- 関数のデフォルト引数

```js
function makeAjaxRequest(url, method = 'GET') {}

makeAjaxRequest('google.com', null) #=> nullの場合はnull の値がはいる, undifind は値が無い場合と一緒
```

- ## rest 演算子 (...値数の変わる値)

```js
function addNumbers(...numbers) {
  return numbers.reduce((sum, number) => {
    return sum + number;
  }, 0);
}
addNumbers(1, 2, 3, 4, 5);
```

- spread 演算子
  - まとまったものを分解してくれる

```js
function validateShoppingList(...items) {
  if (items.indexOf("牛乳") < 0) {
    return ["牛乳", ...items];
  }
}
validateShoppingList("オレンジ", "パン");
```

- 分割代入(Destructuring)　 hash の場合

```js
var expense = {
  type: '交通費',
  amount: '4500'
}
const { type: myType, amount } = expense;
myType;
amount;

function fileSummary({type, amount}) {  #=> 分割代入は関数でも利用できる
  return `${type}は${amount}`
}
```

- 分割代入(Destructuring)　配列の場合

```js
var expense = [
  '交通費',
  '4500',
  'test'
]
const [ myType, ...rest ] = expense;
myType; # 交通費
rest;   # ['4500','test']
```

- class

- generator
  - 基本的に ( for (let = color of colors) {})で使用する
  - ＊generator の中では map, forEach ... 等は使えない -> for of を使う
  - ex) 家からやることリストを(商品を買い、コインランドリーで洗濯して)して家に戻る

```js
function* shopping() {
  // 歩道
  // 歩道を歩いてお店に行く
  // お店に到着したのでお金を持ってお店に入る
  const stuffFromStore = yield "お金";

  // コインランドリーに到着したので服を持って入る
  const cleanClothes = yield "汚れた服";
  // 家に歩いて帰る
  return [stuffFromStore, cleanClothes];
}
// お店関連の世界
const gen = shopping();
console.log(gen.next()); // 家から歩道に出る
// { value: "お金", done: false }
console.log(gen.next("商品")); // お店で買い物をして日用品を持って歩道に出る
// { value: "汚れた服", done: true }
console.log(gen.next("綺麗な服"));
// { value: Array ["商品", "綺麗な服"], done: true }
```

- generator と for of を使って便利に使う

```js
const engineeringTeam = {
  size: 3,
  department: "開発部",
  lead: "太朗",
  manager: "花子",
  engineer: "二郎",
};

function* TeamIterator(team) {
  yield team.lead;
  yield team.manager;
  yield team.engineer;
}

const names = [];
for (let name of TeamIterator(engineeringTeam)) {
  names.push(name);
}

console.log(names); // > Array ["太朗", "花子", "二郎"]
```

- generator デリゲーション
  ![スクリーンショット 2020-03-29 19.04.18.png](:storage/4f6d03c4-0320-4654-838d-4f2ba4dec09f/2409a591.png)

```js
const testingTeam = {
  lead: "恭子",
  testor: "隆",
};

const engineeringTeam = {
  testingTeam,
  size: 3,
  department: "開発部",
  lead: "太朗",
  manager: "花子",
  engineer: "二郎",
};

function* TestingTeamIterator(team) {
  yield team.lead;
  yield team.testor;
}

function* TeamIterator(team) {
  yield team.lead;
  yield team.manager;
  yield team.engineer;
  const testingTeamGenerator = TestingTeamIterator(team.testingTeam);
  yield* testingTeamGenerator;
}

const names = [];
for (let name of TeamIterator(engineeringTeam)) {
  names.push(name);
}

console.log(names); // > Array ["太朗", "花子", "二郎", "恭子", "隆"]
```

- symbol.iterator (for of がきたら Symbol.iterator を見に行くと覚える)

```js
const testingTeam = {
  lead: "恭子",
  testor: "隆",
  [Symbol.iterator]: function* () {
    yield this.lead;
    yield this.testor;
  },
};

const engineeringTeam = {
  testingTeam,
  size: 3,
  department: "開発部",
  lead: "太朗",
  manager: "花子",
  engineer: "二郎",
  [Symbol.iterator]: function* () {
    yield this.lead;
    yield this.manager;
    yield this.engineer;
    yield* this.testingTeam;
  },
};

const names = [];
for (let name of engineeringTeam) {
  names.push(name);
}

console.log(names); // > Array ["太朗", "花子", "二郎", "恭子", "隆"]
```

- generator と再帰処理
  ![スクリーンショット 2020-03-29 22.01.33.png](:storage/4f6d03c4-0320-4654-838d-4f2ba4dec09f/ca65fd0d.png)

```js
class Comment {
  constructor(content, children) {
    this.content = content;
    this.children = children;
  }

  *[Symbol.iterator]() {
    yield this.content;
    for (let child of this.children) {
      yield* child;
    }
  }
}

const children = [
  new Comment("賛成", []),
  new Comment("反対", []),
  new Comment("うん。。。", []),
];

const tree = new Comment("最高の記事", children);

const values = [];
for (let value of tree) {
  values.push(value);
}

console.log(values); // > Array ["最高の記事", "賛成", "反対", "うん。。。"]
```

- promis

  - js には sleep のような実装はない

- const
  - 再代入不可
- let
  - 再代入可
