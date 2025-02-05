# public-qiita-hardcoding

Qiita記事用ハードコーディングは避けるべきというコンテンツのコードリポジトリになります。

## コード全容

```typescript
// スプレッドシートのセルから値を取得してGASのスクリプトプロパティに保存する
function setIdData(){
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  const targetSheet = ss.getActiveSheet();
  
  const tokenData = targetSheet.getRange(2,3).getValue();
  PropertiesService.getScriptProperties().setProperty("token", tokenData);
  return
}

// GASのスクリプトプロパティから値を取得して利用する：一つの値
function getIdData(){
  const property = PropertiesService.getScriptProperties().getProperty("token");
  console.log(`property：${property}`)
}

// GASのスクリプトプロパティから値を取得して利用する：複数の値を配列として取得
function getIdDatas(){
  const keys = PropertiesService.getScriptProperties().getKeys() // これは配列として取得する
  const properties = PropertiesService.getScriptProperties().getProperties()  //これはキー・値のオブジェクトとして取得する

  // 値だけの配列にする
  const propertiesArray = keys.map((key) => properties[key]);

  // キー・値ごとの配列にする
  const formattedProperties = keys.map( (key) => ({
    "Key": key,
    "Value": properties[key]
  }))

  console.log(`keys：\n${JSON.stringify(keys, null, 2)}`)
  console.log(`properties：\n${JSON.stringify(properties, null, 2)}`)
  console.log(`propertiesArray：\n${JSON.stringify(propertiesArray, null, 2)}`)
  console.log(`formattedProperties：\n${JSON.stringify(formattedProperties, null, 2)}`)
}
```
