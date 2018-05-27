
## How to write test for React


---

### はじめに

+++

#### フロントエンド開発は常に副作用との戦い

+ サーバサイドよりもModelのライフサイクルが長い |
+ 複数のイベントを捌かなければならない |
   + (ユーザーアクション、非同期通信、プッシュ配信)


+++

#### どうやって副作用に立ち向かうか？

+++

#### Flux?

+ 副作用を全てactionと捉え、状態管理を徹底する |

+++

#### Test?

+ 今日話すこと |

---


### What is Jest?


+++

+ Facebook製のJavaScriptのテストツール。    
`React`専用ではなく、`Vue.js`や`Angular`でも利用できる。

---

### Jest でできること

* describe, expect のスペックテスト |
* UIの変更を検知できるスナップショットテスト |
* カバレッジの取得 |

---

### スペックテスト


+++

#### ロジックのテスト

+++

##### テストコード

BDD風。自然言語を併記しながらテストコードを記述する

```javascript
const plus = require('./plus');

describe('#plus', () => {
  it('knows that 2 and 2 make 4', () => {
    expect(plus(2,2)).toBe(4);
  });
});
```
@[1](テスト対象のfunctionをimportする)
@[3](テスト対象の説明)
@[4](期待する結果の説明)
@[5](アサーション)


+++

```
PASS  __tests__/state-functions.test.js
  #plus
    ✓ knows that 2 and 2 make 4 (5ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 passed, 0 total
Time:        3.11s
```
@[2-3](関数の仕様と適切に動いていることが分かる )

+++

#### Viewのテスト

+++

* Jestは自動的にリソースをMock化する

+++


#### テストコードはコストが高い？

* 常にメンテナンス |
* 危なそうなとこだけ書く |
* 男は黙って手動テスト  |


---

### スナップショットテスト


+++

#### スナップショットテストって？

+ UI が予期せず変更されていないかを確認するテスト | 

+ 前回のアウトプットとの比較するテストコードを書くだけ |


+++

#### 例

+ 開発者「`<LinkToHome />`というコンポーネントのURLを変更しました!」

+++

#### コード

```javascript
it('renders correctly', () => {
  const tree = renderer
    .create(<LinktoHome />)
    .toJSON();
  expect(tree).toMatchSnapshot();
});
```

+++

#### スナップショット

![スナップショット画面](https://facebook.github.io/jest/img/content/failedSnapshotTest.png)

+++
    
 -> 意図したとおりなら、スナップショットを上書き
 
```
jest --updateSnapshot
```

+++


+ テストコード書くのに時間はかからないので、書きやすい and 捨てやすい
+ 実はUIだけでなく、JavaScriptのobjectのスナップショットテストも可能
+ スナップショットもGit管理する必要があるので、コンフリクトは心配かも？


---

### カバレッジの取得

+++

テスト実行時に `--coverage`オプションを付けるだけ
```
npm test -- --coverage
```


+++

レポートがhtml形式で出力される

![カバレッジ一覧](https://camo.qiitausercontent.com/00a690cecc7ce975c0ca17712de1953191a49513/68747470733a2f2f71696974612d696d6167652d73746f72652e73332e616d617a6f6e6177732e636f6d2f302f3132383634352f35666366353033392d326264382d386632322d346263382d6133373733626331643861662e706e67)


+++

![ファイル単位](https://camo.qiitausercontent.com/bb03701306124e5da41eedb6ff5691e6975bc5fe/68747470733a2f2f71696974612d696d6167652d73746f72652e73332e616d617a6f6e6177732e636f6d2f302f3132383634352f31623736353038642d633262652d373137642d313061302d6666323932643266353266662e706e67)


+++

_(カバレッジは)書かれているコードに対するカバレッジであって、仕様に対するカバレッジではありません。不具合というものは、多くの場合、仕様の不理解に対して発生するものです。仕様を把握していない結果「書かれなかった」コードに対して、カバレッジ測定は無力です。ですから「カバレッジ 100% だから絶対にバグは無いし安心」などということは言えないのです。_   
@t-wada

---

### デモ

---


### 参考

* [Testing with Jest Snapshots: First Impressions](https://benmccormick.org/2016/09/19/testing-with-jest-snapshots-first-impressions/)

* [jestでテストカバレッジを見る](https://qiita.com/monisoi/items/44931e36c5f7b1f4e683)

* [右手に感情、左手に数値 - カバレッジを味方にしよう](http://d.hatena.ne.jp/t-wada/20111207/coverage_is_your_friend)

---


### おわり
