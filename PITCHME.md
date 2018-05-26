
## How to write test for React

---

### はじめに

+++

Reactを

---


### What is Jest?


+++

+ Facebook製のJavaScriptのテストツール。    
`React`専用ではなく、`Vue.js`や`Angular`でも利用できる。

---

### Jest でできること

* describe, expect のスペックテスト |
* カバレッジの取得 |
* UIの変更を検知できるスナップショットテスト |

---

### スペックテスト


+++

#### Storeのテスト


+++

#### Viewのテスト

---

### カバレッジの取得


---

### スナップショットテスト


+++

#### スナップショットテストって？

+ UI が予期せず変更されていないかを確認するテスト | 

+ 最初に実行したテストのアウトプットが保存され、二回目以降のテストは以前のスナップショットとの比較して一致していれば通過する。 |


+++

#### 例



+++

#### コード

```javascript
it('renders correctly', () => {
  const tree = renderer
    .create(<LinkToHome />)
    .toJSON();
  expect(tree).toMatchSnapshot();
});
```

+++

#### スナップショット

![スナップショット画面](https://facebook.github.io/jest/img/content/failedSnapshotTest.png)

+++

 -> 意図した変更であれば、スナップショットを上書き

+++


* テストコード書くのに時間はかからないので、書きやすい and 捨てやすい
+ 実はUIだけでなく、JavaScriptのobjectのスナップショットテストも可能

---


### デモ

---

### おわり
