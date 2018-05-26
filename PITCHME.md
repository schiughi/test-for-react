
## How to write test for React

---

### はじめに

+++

早速ですが、ソフトウェア開発において不具合とどのように向き合えばいいでしょうか。

+ 設計で安全性を高める？ |
   + 契約プログラミング , Flux(Redux) , MVW ...   
+ 静的検証でつぶす？ |
  + TypeScript , Flow
+ 自動テストでつぶす？ |
  + Jest, Enzyme, Mocha, Chai

+++

#### これら全て実践すれば、超高品質なプロダクトができる！！　

 開発スピードを犠牲にすれば、ね…… |

+++


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


```javascript
const add = require('./add');

describe('#add', () => {
  it('knows that 2 and 2 make 4', () => {
    expect(add(2,2)).toBe(4);
  });
});
```

+++

```
PASS  __tests__/state-functions.test.js
  #add
    ✓ knows that 2 and 2 make 4 (5ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 passed, 0 total
Time:        3.11s
```

+++

#### Viewのテスト

+++


#### Tips

+++

##### Testコードどこに書くの？

+++

##### 画像ファイルとかどうすんの？

---

### スナップショットテスト


+++

#### スナップショットテストって？

+ UI が予期せず変更されていないかを確認するテスト | 

+ 最初に実行したテストのアウトプットが保存され、二回目以降のテストは以前のスナップショットとの比較して一致していれば通過する。 |


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

 レビュアー「OK!」    
    
 -> スナップショットを上書き
 
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

```
npm test -- --coverage
```


+++

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
