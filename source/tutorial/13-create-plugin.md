---
type: doc
title: プラグインを作成してみる
order: 13
---

## 概要

ここではGrimoire.jsが提供しているジェネレータを活用して、ユーザーはプラグインを制作することができます。また、npmを通じてプラグインを公開することも可能です。

## 学べること

* プラグインジェネレータを用いたプラグインの作成手順
* プラグインの公開

### プラグインジェネレータを使用してみる

Grimoire.jsではコンポーネントやノードの作成のためにプラグインジェネレータを提供しています。これによりユーザーは簡単にプラグインを作成し、公開することが可能になります。ジェネレータに関する詳細は[プラグインジェネレータ](../guide/addons-generator.html)を参照してください。ここでは、簡単なノードとコンポーネントを制作することを行い、プラグイン制作の方法を学びます。

> Grimoire.jsのプラグインを制作、公開するためには現在(2016/10)Node.js環境が必要です。

Grimoire.jsのプラグインジェネレータはyoemanを使って導入されます。

```
npm install yo generator-grimoire-addons -g
```

```
mkdir grimoirejs-sample-plugin
cd grimoirejs-sample-plugin
yo generator-addons
```

> Grimoire.jsのプラグインには`grimoirejs`のプレフィックスをつけることが推奨されます。

Grimoire.jsが用いる各ノードやコンポーネントなどの名前の識別のために名前空間を用います。自分以外の人が用いるであろうコンポーネントやノードを作成する場合、名称が被って競合するのを防ぐために利用する必要があります。

以上の操作でGrimoire.jsのプラグイン開発環境は整います。

Git管理する場合には`.gitignore`がジェネレータにより生成されています。


### コンポーネントを制作してみる

コンポーネントを制作してみましょう。今回はコンポーネントをつけると、対象のノードが移動するようになるコンポーネントを作ってみます。

```
npm run scaffold -- -t component -n LinaerMotion
```

`src/Components`以下に

### コンバーターを生成してみる

コンバーターを作成してみましょう。


### ノードを作成してみる

ノードを作成してみます。

### 作成したプラグインを公開してみる

作成したコンポーネントを公開するにはnpmを通じでpublishすることにより可能です。

