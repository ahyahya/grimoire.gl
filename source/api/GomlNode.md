---
type: doc
title: GomlNode
order: 10
---

## GomlNode
GomlNodeはGrimoireJSが扱うツリー構造のノードとなる重要なオブジェクトです。
GomlNodeは、GrimoireInterfaceにregisterNodeされている情報を参照し、Gomlのパースなどで生成されます。
このオブジェクトから、ノードをツリー上で操作することができます。
また、ノードは複数のコンポーネントを包含して管理するので、それらに対しての操作を行うことができます。

**例**

- nameフィールド
- enabledフィールド
- childrenフィールド
- sendMessageメソッド
- ...etc

### name
  ```typescript
  name: NSIdentity;
  ```
このノードの名前を示します。
### enabled
このノードの有効・無効を切り替えます。
ただし、trueであっても親が無効化されているときはこのノードは無効化された状態になります。
無効の場合、子ノードを含めてisActiveがfalseになります。
**有効か無効かを判定したい場合は、enabledではなくisActiveを使用してください。**

### isActive
このノードが有効か無効かを取得します。
無効になっている場合、メッセージを一切受信しません。
### mounted
このノードがマウントされているかを示します。
マウントとは、所属するツリー構造がGrimoireInterfaceの管理下に置かれている状態を指します。
通常、すべてのノードはマウントされていますが、以下の場合にマウントされていない状態になります。

+ 新しいインスタンスを個別に作成した場合。
+ ツリーからノードをデタッチした場合。
+ Gomlからパースされる際、インスタンスが作成されてからパースが完了するまでの間。

マウントされていない状態では、基本的にノードは機能していない状態となります。
また、ノードからメッセージを発行することもできません。
マウント状態が変更する際には、**mount**,**unmount**メッセージが発行されます。

### tree
このノードの所属するGrimoireInterfaceを返します。
ノードがマウントされていないときは例外を投げます。
### deleted
このノードが削除されていることを示します。
削除されたノードは常に非マウント状態であり、再度マウントすることは一切できません。
### companion
ツリーの中で共有されるオブジェクトです。
つまり、同一goml中のすべてのノードで同じインスタンスを参照します。
### parent
このノードの親ノードを参照します。
ルートノードではnullになります。
ツリーにマウントされていない場合もnullになることがあります。
### hasChildren
このノードが子ノードを持っているかを表します
### getChildrenByClass
class属性を指定して子要素を検索します。
### getChildrenByNodeName
ノード名を指定して子要素を検索します
### delete
このノードと子ノードを再帰的に削除します。
削除されたノードはツリーからデタッチされ、**再利用することはできません**。
削除する際には*dispose*メッセージが送信されます。
### sendMessage
このノードのコンポーネントにメッセージを送信します。
### broadcastMessage
このノードと子要素に再帰的にメッセージを送信します。
### addChildByName
ノード名と属性を指定して子ノードを追加します。
```typescript
  var childNode = node.addChildByName("mesh",{"geometry":"cube"});
```
### addChild
ノードのインスタンスを指定して子ノードに追加します。
必要であればインデックスを指定することができます。
```typescript
node.addChild(childNode);
```
### callRecursively
子ノードに再帰的に関数を呼び出します。
### removeChild
指定したノードのインスタンスが子ノードであれば**削除**します。
### detachChild
指定したノードのインスタンスが子ノードであれば**デタッチ**します。
デタッチとは、ツリー上から取り除かれることです。
マウントが解除されるので、*unmount*メッセージが送信されます。
マウントされた他のノードにaddChildすることで、再度マウントすることができます。
```typescript
node1.detachChild(childNode);
node2.addChild(childNode);
```
### detach
このノードを**デタッチ**します。
### getAttribute
属性名を指定して値を取得します。
取得できるのは、このノードのデフォルトコンポーネントの属性です。
**オプショナルコンポーネントの属性は取得できません**。
オプショナルコンポーネントの属性にアクセスする場合、そのコンポーネントのインスタンスか、そのコンポーネントを
対象とするコンポーネントインタフェースを経由することができます。
### setAttribute
属性名を指定して値を設定します。
詳細については*getAttribute*の項目を参照してください。
### addAttribute
このノードに属性を追加します。
この属性はどのコンポーネントにも属さず、ノード自体の属性として扱われます。
### setMounted
システムで使用されます。**使用しないでください。**
### index
このノードの親ノードの子ノードとしてのインデックスです。
親が存在しないとき、-1を返します。
### removeAttribute
指定した属性を削除します。
### addComponent
このノードにオプショナルコンポーネントを追加します。
### getComponents
このノードのコンポーネントのリストを取得します。
### getComponent
名前を指定してコンポーネントを取得します。
### resolveAttributesValue
システムで使用されます。**使用しないでください。**
### checkTreeConstraints
システムで使用されます。**使用しないでください。**
### notifyActivenessUpdate
システムで使用されます。**使用しないでください。**



