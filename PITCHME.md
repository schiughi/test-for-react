
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

+ 最初に実行したテストのアウトプットが保存され、二回目以降のテストは以前のスナップショットとの比較して一致していれば通過する。


+++

```javascript
// Updated test case with a Link to a different address
it('renders correctly', () => {
  const tree = renderer
    .create(<Link page="http://www.instagram.com">Instagram</Link>)
    .toJSON();
  expect(tree).toMatchSnapshot();
});
```



+++

![スナップショット画面](https://facebook.github.io/jest/img/content/failedSnapshotTest.png)

---


### デモ

---

### おわり
