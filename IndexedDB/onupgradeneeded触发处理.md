# onupgradeneeded 触发处理

## 起因

封装 IndexedDB 时遇到这个事件

## 分析

> https://www.bookstack.cn/read/javascript-tutorial/spilt.3.docs-bom-indexeddb.md

如果指定的版本号，大于数据库的实际版本号，就会发生数据库的升级事件 `upgradeneeded`

## 解决方案

新建数据库

新建数据库与打开数据库是同一个操作。如果指定的数据库不存在，就会新建。不同之处在于，后续的操作主要在 `upgradeneeded`事件监听下完成，因为这时版本从无到有，所以会触发这个事件。

通常，新建数据库以后，第一件事是新建对象仓库（即新建表）。

```js
request.onupgradeneeded = function(event) {
  const db = event.target.result;

  // 判断一下这张表是否存在再新建
  if (!db.objectStoreNames.contains('person')) {
    const objectStore = db.createObjectStore('person', { keyPath: 'id' });
  }
}
```

主键（key）是默认建立索引的属性。比如，数据记录是`{ id: 1, name: '张三' }`，那么id属性可以作为主键。主键也可以指定为下一层对象的属性，比如`{ foo: { bar: 'baz' } }`的`foo.bar`也可以指定为主键。

如果数据记录里面没有合适作为主键的属性，那么可以让 IndexedDB 自动生成主键。

```js
// 指定主键为一个递增的整数。
const objectStore = db.createObjectStore('person',  { autoIncrement: true })
```

新建仓库后，下一步可以新建索引。

```js
request.onupgradeneeded = function(event) {
  const db = event.target.result
  const objectStore = db.createObjectStore('person', { keyPath: 'id' })
  // IDBObject.createIndex()的三个参数分别为索引名称、索引所在的属性、配置对象（说明该属性是否包含重复的值）。
  objectStore.createIndex('name', 'name', { unique: false })
  objectStore.createIndex('email', 'email', { unique: true })
}
```
