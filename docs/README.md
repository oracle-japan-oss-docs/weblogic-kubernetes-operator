# WebLogic Kubernetes Operator

WebLogic Kubernetes Operator (オペレータ)は、業界標準のクラウド・ニュートラル・デプロイメント・プラットフォームであるKubernetesでのWebLogic ServerおよびFusion Middleware Infrastructureドメインの実行をサポートしています。これにより、WebLogic Serverインストール全体および階層化されたアプリケーションを、移植可能なクラウド・ニュートラル・イメージおよび単純なリソース記述ファイルのセットにカプセル化できます。オペレータをデプロイしたKubernetesをサポートするオンプレミスまたはパブリック・クラウドで実行できます。

さらに、このオペレータはCI/CDプロセスに適しています。テストから本番への移行など、環境間を移動する際に変更を簡単に挿入できます。たとえば、デプロイ時にデータベースURLおよび資格証明を外部で注入したり、ほとんどのWebLogic構成に任意の変更を注入できます。

オペレータは[「Kubernetesオペレータ・パターン」](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/)を利用します。つまり、Kubernetes APIを使用して次のような操作をサポート: プロビジョニング、ライフサイクル管理、アプリケーションのバージョニング、製品のパッチ適用、スケーリングおよびセキュリティ。オペレータは、モニタリング、ロギング、トレースおよびセキュリティのために、このインフラストラクチャに固有のツールを使用することもできます。

次のことができます:
* Kubernetesクラスタ内のすべての名前空間内のすべてのWebLogicドメインを管理するオペレータ、名前空間の特定のサブセット内のドメインのみを管理するオペレータ、またはオペレータと同じ名前空間内のドメインのみを管理するオペレータをデプロイします。名前空間は、最大で1つのオペレータで管理できます。
* 次を使用してWebLogicドメイン構成を指定します:
   * _PVのドメイン_: WebLogicドメイン・ホームをKubernetes PersistentVolume (PV)に配置します。このPVは、NFSファイルシステムまたはその他のKubernetesボリューム・タイプに存在できます。
   * _イメージ内のドメイン_: WebLogicドメイン・ホームをコンテナ・イメージに含めます。
   * _イメージ内のモデル_: [WebLogic Deploy Tooling](https://github.com/oracle/weblogic-deploy-tooling)モデルおよびアーカイブをコンテナ・イメージに含めます。
* (Kubernetesカスタム・リソース定義を使用して) WebLogicドメインのデプロイメントをKubernetesリソースとして構成します。
* WebLogicドメイン構成の特定の側面をオーバーライドします。たとえば、デプロイメントごとに異なるデータベース・パスワードを使用します。
* 宣言的な起動パラメータおよび必要な状態に基づいて、ドメイン内のサーバーおよびクラスタを起動および停止します。
* 管理対象サーバーをオンデマンドで起動および停止するか、REST APIと統合してWebLogic Diagnostics Framework (WLDF)、Prometheus、Grafanaまたはその他のルールに基づいてスケーリングを開始することで、WebLogicドメインをスケーリングします。
* 必要に応じて、WebLogic Server管理コンソールをKubernetesクラスタの外部に公開します。
* 必要に応じて、Kubernetesドメインの外部でT3チャネルを公開します。
* ロード・バランシングを使用してKubernetesドメイン外のWebLogicドメインでHTTPパスを公開し、WebLogicドメイン内の管理対象サーバーが起動または停止されたときにロード・バランサを自動的に更新します。
* オペレータおよびWebLogic ServerのログをElasticsearchに公開し、Kibanaで対話します。


オペレータを最も速く体験するには、[「クイックスタート・ガイド」](https://oracle.github.io/weblogic-kubernetes-operator/quickstart/)をフォローするか、[ドキュメンテーション](https://oracle.github.io/weblogic-kubernetes-operator)を使用するか、[「ブログ」](https://blogs.oracle.com/weblogicserver/how-to-weblogic-server-on-kubernetes)を読むか、[例](https://oracle.github.io/weblogic-kubernetes-operator/samples/simple/)を試します。

***
[「オペレータの現在のリリース」](https://github.com/oracle/weblogic-kubernetes-operator/releases)は3.2.2です。このリリースは2021年4月27日に公開されました。
***

# ドキュメンテーション

オペレータのドキュメントは、[「こちらから入手可能」](https://oracle.github.io/weblogic-kubernetes-operator)です。

このドキュメントには、ユーザーおよび開発者向けの情報が含まれています。すぐに起動して実行する場合は、サンプル、参照資料、セキュリティ情報および[「クイック・スタート」](https://oracle.github.io/weblogic-kubernetes-operator/quickstart/)ガイドを提供します。

オペレータの以前のリリースのドキュメント: [2.5.0](https://oracle.github.io/weblogic-kubernetes-operator/2.5/)、[2.6.0](https://oracle.github.io/weblogic-kubernetes-operator/2.6/)、[3.0.x](https://oracle.github.io/weblogic-kubernetes-operator/3.0/)および[3.1.x](https://oracle.github.io/weblogic-kubernetes-operator/3.1/)。

# 下位互換性ガイドライン

2.0リリースでは、変更が中断され、以前のリリースとの互換性が維持されていませんでした。

2.0.1リリース以降、オペレータ・リリースは、domainresourceスキーマ、オペレータHelmチャート入力値、構成オーバーライド・テンプレート、Kubernetesリソース(オペレータHelmチャートを作成)、オペレータによって作成されたKubernetesリソースおよびオペレータRESTインタフェースに関して下位互換性を持つことを目的としています。3つのリリースでは、明確に伝達された非推奨の機能が使用可能になった後も1つのリリースで維持される場合を除いて、互換性が保たれる予定です。

# さらにサポートが必要ですか? 提案がありますか?

**「パブリックSlackチャネル」**では、オペレータの使用について質問したり、表示する機能や改善点に関するフィードバックを提供することができます。私たちはあなたから便りがあるのが好きです。チャネルに参加するには、[招待を取得するには、このサイトにアクセスしてください](https://weblogic-slack-inviter.herokuapp.com/)。招待メールには、Slackワークスペースへのアクセス方法の詳細が含まれます。ログイン後、`#operator`に移動して「こんにちは。」と言ってください

# オペレータへの貢献

Oracleは、誰からでもこのプロジェクトに貢献します。貢献者がオペレータに問題を報告しているか、プル・リクエストを発行している可能性があります。大量のプル・リクエストを引き起こす可能性のある重要な開発を開始する前に、まず問題を作成し、提案された変更について既存の開発者と話し合うことをお薦めします。

プル・リクエストを送信してバグを修正したり、既存の機能を強化する場合は、まず問題を開き、プル・リクエストを送信するときにその問題にリンクしてください。

送信の可能性について質問がある場合は、問題を自由に開くことができます。

## WebLogic Kubernetes Operatorリポジトリへのコントリビュート

プル・リクエストは、[https://www.oracle.com/technetwork/community/oca-486395.html](https://www.oracle.com/technetwork/community/oca-486395.html)で入手可能なOracle Contributor Agreement (OCA)で行うことができます。

プル・リクエストを受け入れるには、OCA署名者リストに表示されるコントリビュータ名と電子メール・アドレスを使用して、コミット・メッセージの下部に次の行が必要です。

```
Signed-off-by: Your Name <you@example.org>
```

これは、次のものを使用してコミットすることで、プル・リクエストに自動的に追加できます:

```
git commit --signoff
```

OCAに署名したことを確認できるコミット者からのプル・リクエストのみを受け入れることができます。

## プル・リクエスト・プロセス

* リポジトリをフォークします。
* forkにブランチを作成して変更を実装します。`1234-fixes`などのブランチ名の一部として問題番号を使用することをお薦めします。
* 修正に必要な変更でドキュメントが更新されていることを確認します。
* ベース・イメージが変更された場合は、すべてのサンプルが更新されていることを確認します。
* プル・リクエストを送信します。プル・リクエストは空白のままにしないでください。変更の目的を正確に説明し、変更の検証方法に関する簡単なステップを示します。作成した問題も参照していることを確認します。プル・リクエストをマージする前に、レビューのために2-3人に割り当てます。

## 新しい依存関係の導入

新しい依存関係を導入しようとするプル・リクエストは、追加のレビューの対象となることに注意してください。通常、コントリビュータは互換性のないライセンスとの依存関係を回避し、最新バージョンの依存関係の使用を試みる必要があります。新しい依存関係を受け入れる前に、標準のセキュリティ脆弱性チェックリストが参照されます。WebLogic Serverを含むクローズド・ソース・コードへの依存性は、ほとんどの場合拒否されます。
