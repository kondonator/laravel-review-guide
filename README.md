# laravel-review-guide

Laravelを長年使用してきた経験から、コードレビューする際にチェックするポイントをまとめます。

## FatControllerからSlimControllerへ
FatControllerはテストを難しくします。

処理を別クラスに切り出して、SlimController化することで、切り出したクラスごとにテストを作成することができるようになります。

### ValidationはFormRequestを継承したクラスへ
Controller内のValidation処理をFormRequestを継承したRequestクラスへ移行します。

これにより、ControllerをSlim化することができるようになります。

Requestクラスのテストを作成しましょう。

また、dataProviderを使用することで、パターンを網羅したテストを行うことができるようになります。

### 認可処理をPolicyクラスへ
複数Roleがあるサービスの場合、Controller内の認可処理をPolicyクラスに移行します。

これにより、ControllerをSlim化することができるようになります。

Policyクラスのテストを作成しましょう。

### Controller内の処理をServiceクラスやUseCaseクラスへ
Controller内の処理をServiceクラスやUseCaseクラスに移行します。
必要に応じて、Repositoryクラスを作成して、モデルの処理をそちらに移行することで、さらに再利用しやすくなります。

以上のアプローチにより、Controller内の処理を$requestの処理と画面遷移の処理に集中させることができるようになります。

## その他

### 変数の初期化
ループ内で変数が定義されている場合、ループの外で定義するように移動する。
