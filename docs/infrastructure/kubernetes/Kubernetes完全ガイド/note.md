# 概要<!-- omit in toc -->

- 書籍名
  - Kubernetes完全ガイド

# 学習目的<!-- omit in toc -->

- [ ] Kubernetesの基礎知識やキーワードを理解しつつ、おおよその全体像を把握できるようになること

# 学習アウトプット<!-- omit in toc -->

- [ ] Kubernetesの基礎知識やキーワードを整理してリポジトリに反映する
- [ ] 「Rails + Nginx」をminikube上で実行する
- [ ] 上記の構築手順を技術記事にして公開する

# 目次<!-- omit in toc -->

- [第1章 Docker の復習と「Hello, Kubernetes」](#第1章-docker-の復習とhello-kubernetes)
  - [1.1 Docker の復習](#11-docker-の復習)
  - [1.2 さあ、Kubernetes の世界へ](#12-さあkubernetes-の世界へ)
- [第2章 なぜKubernetes が必要なのか？](#第2章-なぜkubernetes-が必要なのか)
  - [2.1 Kubernetes とは](#21-kubernetes-とは)
  - [2.2 Kubernetes の歴史](#22-kubernetes-の歴史)
  - [2.3 Kubernetes を使うと何ができるのか](#23-kubernetes-を使うと何ができるのか)
    - [2.3.1 宣言的なコードによる管理(IaC)](#231-宣言的なコードによる管理iac)
    - [2.3.2 スケーリング/オートスケール](#232-スケーリングオートスケール)
    - [2.3.3 スケジューリング](#233-スケジューリング)
    - [2.3.4 リソース管理](#234-リソース管理)
    - [2.3.5 セルフヒーリングƒ](#235-セルフヒーリングƒ)
    - [2.3.6 ロードバランシングとサービスディスカバリ](#236-ロードバランシングとサービスディスカバリ)
    - [2.3.7 データの管理](#237-データの管理)
  - [2.4 まとめ](#24-まとめ)
- [第3章 Kubernetes 環境の選択肢](#第3章-kubernetes-環境の選択肢)
  - [3.1 Kubernetes 環境の種別](#31-kubernetes-環境の種別)
  - [3.2 ローカルKubernetes](#32-ローカルkubernetes)
    - [3.2.1 Minikube](#321-minikube)
    - [3.2.2 Docker Desktop for Mac](#322-docker-desktop-for-mac)
    - [3.2.3 kind (Kubernetes in Docker)](#323-kind-kubernetes-in-docker)
  - [3.3 Kubernetes 構築ツール](#33-kubernetes-構築ツール)
    - [3.3.1 Kubernetesのサービスレベル目標(SLO)](#331-kubernetesのサービスレベル目標slo)
    - [3.3.2 kubeadm](#332-kubeadm)
    - [3.3.3 Flannel](#333-flannel)
    - [3.3.4 Rancher](#334-rancher)
  - [3.4 パブリッククラウド上のマネージドKubernetes サービス](#34-パブリッククラウド上のマネージドkubernetes-サービス)
    - [3.4.1 GKE (Google Kubernetes Engine)](#341-gke-google-kubernetes-engine)
    - [3.4.2 AKS (Azure Kubernetes Service)](#342-aks-azure-kubernetes-service)
    - [3.4.3 EKS (Elastic Kubernetes Service)](#343-eks-elastic-kubernetes-service)
  - [3.5 Kubernetes プレイグラウンド](#35-kubernetes-プレイグラウンド)
  - [3.6 まとめ](#36-まとめ)
- [第4章 API リソースとkubectl](#第4章-api-リソースとkubectl)
  - [4.1 本章以降を読み進めるための準備](#41-本章以降を読み進めるための準備)
  - [4.2 Kubernetes の基礎](#42-kubernetes-の基礎)
  - [4.3 Kubernetes とリソース](#43-kubernetes-とリソース)
    - [4.3.1 Workloads APIs カテゴリ](#431-workloads-apis-カテゴリ)
    - [4.3.2 Service APIs カテゴリ](#432-service-apis-カテゴリ)
    - [4.3.3 Config & Storage APIs カテゴリ](#433-config--storage-apis-カテゴリ)
    - [4.3.4 Cluster APIs カテゴリ](#434-cluster-apis-カテゴリ)
    - [4.3.5 Metadata APIs カテゴリ](#435-metadata-apis-カテゴリ)
  - [4.4 Namespace による仮想的なクラスタの分離](#44-namespace-による仮想的なクラスタの分離)
  - [4.5 CLI ツールkubectl](#45-cli-ツールkubectl)
    - [4.5.1 認証情報とContext (config)](#451-認証情報とcontext-config)
    - [4.5.2 Kubectx / kubensによる切り替え](#452-kubectx--kubensによる切り替え)
    - [4.5.3 マニフェストとリソースの作成 / 削除 / 更新 (create / delete / apply)](#453-マニフェストとリソースの作成--削除--更新-create--delete--apply)
    - [4.5.4 リソース作成にも kubectl apply を使うべき理由](#454-リソース作成にも-kubectl-apply-を使うべき理由)
    - [4.5.5 Server-side apply](#455-server-side-apply)
    - [4.5.6 Pod の再起動 (rollout restart)](#456-pod-の再起動-rollout-restart)
    - [4.5.7 generateNameによるランダムな名前のリソースの作成](#457-generatenameによるランダムな名前のリソースの作成)
    - [4.5.8 リソースの状態のチェックと待機(wait)](#458-リソースの状態のチェックと待機wait)
    - [4.5.9 マニフェストファイルの設計](#459-マニフェストファイルの設計)
      - [1つのマニフェストファイルの中に複数のリソースを記述する](#1つのマニフェストファイルの中に複数のリソースを記述する)
      - [複数のマニフェストファイルを同時に適用する](#複数のマニフェストファイルを同時に適用する)
      - [マニフェストファイルの設計指針](#マニフェストファイルの設計指針)
    - [4.5.10 アノテーションとラベル (annotate / label)](#4510-アノテーションとラベル-annotate--label)
      - [アノテーション (annotate)](#アノテーション-annotate)
        - [システムコンポーネントのためにデータを保存する](#システムコンポーネントのためにデータを保存する)
        - [すべての環境では利用できない設定を行う](#すべての環境では利用できない設定を行う)
        - [正式に組み込まれる前の機能の設定を行う](#正式に組み込まれる前の機能の設定を行う)
      - [ラベル (label)](#ラベル-label)
        - [システムが利用するラベル](#システムが利用するラベル)
        - [システムが利用するラベル](#システムが利用するラベル-1)
    - [4.5.11 Pruneによるリソースの削除 (--pruneオプション)](#4511-pruneによるリソースの削除---pruneオプション)
    - [4.5.12 エディターによる編集j (edit)](#4512-エディターによる編集j-edit)
    - [4.5.13 リソースの一部情報の更新 (set)](#4513-リソースの一部情報の更新-set)
    - [4.5.14 ローカルマニフェストとKubernetes上の登録情報の差分取得 (diff)](#4514-ローカルマニフェストとkubernetes上の登録情報の差分取得-diff)
    - [4.5.15 利用可能なリソース種別の一覧取得 (api-resources)](#4515-利用可能なリソース種別の一覧取得-api-resources)
    - [4.5.16 リソースの情報取得 (get)](#4516-リソースの情報取得-get)
    - [4.5.17 リソースの詳細情報の取得 (describe)](#4517-リソースの詳細情報の取得-describe)
    - [4.5.18 実際のリソースの使用量の確認 (top)](#4518-実際のリソースの使用量の確認-top)
    - [4.5.19 コンテナ上でのコマンドの実行 (exec)](#4519-コンテナ上でのコマンドの実行-exec)
    - [4.5.20 Pod上にデバッグ用の一時的なコンテナの追加 (debug)](#4520-pod上にデバッグ用の一時的なコンテナの追加-debug)
    - [4.5.21 ローカルマシンからPodへのポートフォワーディング (port-forward)](#4521-ローカルマシンからpodへのポートフォワーディング-port-forward)
    - [4.5.22 コンテナのログ確認](#4522-コンテナのログ確認)
    - [4.5.23 Sternによる高度なログ確認](#4523-sternによる高度なログ確認)
    - [4.5.24 コンテナとローカルマシン間でのファイルのコピー (cp)](#4524-コンテナとローカルマシン間でのファイルのコピー-cp)
    - [4.5.25 kubectl pluginとパッケージマネージャ (plugin / krew)](#4525-kubectl-pluginとパッケージマネージャ-plugin--krew)
  - [4.6 まとめ](#46-まとめ)
- [第5章 Workloads APIs カテゴリ](#第5章-workloads-apis-カテゴリ)
  - [5.1 Workloads APIs カテゴリの概要](#51-workloads-apis-カテゴリの概要)
  - [5.2 Pod](#52-pod)
  - [5.3 ReplicaSet ／ ReplicationController](#53-replicaset--replicationcontroller)
  - [5.4 Deployment](#54-deployment)
  - [5.5 DaemonSet](#55-daemonset)
  - [5.6 StatefulSet](#56-statefulset)
  - [5.7 Job](#57-job)
  - [5.8 CronJob](#58-cronjob)
  - [5.9 まとめ](#59-まとめ)
- [第6章 Service APIs カテゴリ](#第6章-service-apis-カテゴリ)
  - [6.1 Service APIs カテゴリの概要](#61-service-apis-カテゴリの概要)
  - [6.2 Kubernetes クラスタのネットワークとService](#62-kubernetes-クラスタのネットワークとservice)
  - [6.3 ClusterIP Service](#63-clusterip-service)
  - [6.4 ExternalIP Service](#64-externalip-service)
  - [6.5 NodePort Service](#65-nodeport-service)
  - [6.6 LoadBalancer Service](#66-loadbalancer-service)
  - [6.7 Service のその他の機能](#67-service-のその他の機能)
  - [6.8 Headless Service（None）](#68-headless-servicenone)
  - [6.9 ExternalName Service](#69-externalname-service)
  - [6.10 None-Selector Service](#610-none-selector-service)
  - [6.11 Ingress](#611-ingress)
  - [6.12 まとめ](#612-まとめ)
- [第7章 Config ＆ Storage APIs カテゴリ](#第7章-config--storage-apis-カテゴリ)
  - [7.1 Config ＆ Storage APIs カテゴリの概要](#71-config--storage-apis-カテゴリの概要)
  - [7.2 環境変数の利用](#72-環境変数の利用)
  - [7.3 Secret](#73-secret)
  - [7.4 ConfigMap](#74-configmap)
  - [7.5 PersistentVolumeClaim](#75-persistentvolumeclaim)
  - [7.6 Volume](#76-volume)
  - [7.7 PersistentVolume（PV）](#77-persistentvolumepv)
  - [7.8 PersistentVolumeClaim (PVC)](#78-persistentvolumeclaim-pvc)
  - [7.9 volumeMounts で利用可能なオプション](#79-volumemounts-で利用可能なオプション)
  - [7.10 まとめ](#710-まとめ)
- [第8章 Cluster APIs カテゴリとMetadata APIs カテゴリ](#第8章-cluster-apis-カテゴリとmetadata-apis-カテゴリ)
  - [8.1 Cluster APIs カテゴリとMetadata APIs カテゴリの概要](#81-cluster-apis-カテゴリとmetadata-apis-カテゴリの概要)
  - [8.2 Node](#82-node)
  - [8.3 Namespace](#83-namespace)
  - [8.4 まとめ](#84-まとめ)
- [第9章 リソース管理とオートスケーリング](#第9章-リソース管理とオートスケーリング)
  - [9.1 リソースの制限](#91-リソースの制限)
  - [9.2 Cluster Autoscaler とリソース不足](#92-cluster-autoscaler-とリソース不足)
  - [9.3 LimitRange によるリソース制限](#93-limitrange-によるリソース制限)
  - [9.4 QoS Class](#94-qos-class)
  - [9.5 ResourceQuota によるNamespace のリソースクォータ制限](#95-resourcequota-によるnamespace-のリソースクォータ制限)
  - [9.6 HorizontalPodAutoscaler（HPA）](#96-horizontalpodautoscalerhpa)
  - [9.7 VerticalPodAutoscaler（VPA）](#97-verticalpodautoscalervpa)
  - [9.8 まとめ](#98-まとめ)
- [第10章 ヘルスチェックとコンテナのライフサイクル](#第10章-ヘルスチェックとコンテナのライフサイクル)
  - [10.1 ヘルスチェック](#101-ヘルスチェック)
  - [10.2 コンテナのライフサイクルと再始動（restartPolicy）](#102-コンテナのライフサイクルと再始動restartpolicy)
  - [10.3 Init Containers](#103-init-containers)
  - [10.4 起動直後と終了直前に任意のコマンドを実行する（postStart ／ preStop）](#104-起動直後と終了直前に任意のコマンドを実行するpoststart--prestop)
  - [10.5 Pod の安全な停止とタイミング](#105-pod-の安全な停止とタイミング)
  - [10.6 リソースを削除した時の挙動](#106-リソースを削除した時の挙動)
  - [10.7 まとめ](#107-まとめ)
- [第11章 メンテナンスとノードの停止](#第11章-メンテナンスとノードの停止)
  - [11.1 ノードの停止とPod の停止](#111-ノードの停止とpod-の停止)
  - [11.2 スケジューリング対象からの除外と復帰（cordon ／ uncordon）](#112-スケジューリング対象からの除外と復帰cordon--uncordon)
  - [11.3 ノードの排出処理によるPod の退避（drain）](#113-ノードの排出処理によるpod-の退避drain)
  - [11.4 PodDisruptionBudget（PDB）による安全な退避](#114-poddisruptionbudgetpdbによる安全な退避)
  - [11.5 まとめ](#115-まとめ)
- [第12章 高度で柔軟なスケジューリング](#第12章-高度で柔軟なスケジューリング)
  - [12.1 フィルタリングとスコアリング](#121-フィルタリングとスコアリング)
  - [12.2 マニフェストで指定するスケジューリング](#122-マニフェストで指定するスケジューリング)
  - [12.3 ビルトインノードラベルとラベルの追加](#123-ビルトインノードラベルとラベルの追加)
  - [12.4 nodeSelector（Simple Node Affinity）](#124-nodeselectorsimple-node-affinity)
  - [12.5 Node Affinity](#125-node-affinity)
  - [12.6 matchExpressions のオペレータとset-based 条件](#126-matchexpressions-のオペレータとset-based-条件)
  - [12.7 Node Anti-Affinity](#127-node-anti-affinity)
  - [12.8 Inter-Pod Affinity](#128-inter-pod-affinity)
  - [12.9 Inter-Pod Anti-Affinity](#129-inter-pod-anti-affinity)
  - [12.10 複数の条件を組み合わせたPod のスケジューリング](#1210-複数の条件を組み合わせたpod-のスケジューリング)
  - [12.11 1.18 Beta TopologySpreadConstraints によるトポロジ均衡](#1211-118-beta-topologyspreadconstraints-によるトポロジ均衡)
  - [12.12 Taints とTolerations](#1212-taints-とtolerations)
  - [12.13 PriorityClass によるPod の優先度と退避](#1213-priorityclass-によるpod-の優先度と退避)
  - [12.14 その他のスケジューリング](#1214-その他のスケジューリング)
  - [12.15 まとめ](#1215-まとめ)
- [第13章 セキュリティ](#第13章-セキュリティ)
  - [13.1 ServiceAccount](#131-serviceaccount)
  - [13.2 RBAC（Role Based Access Control）](#132-rbacrole-based-access-control)
  - [13.3 SecurityContext](#133-securitycontext)
  - [13.4 PodSecurityContext](#134-podsecuritycontext)
  - [13.5 1.18 Beta PodSecurityPolicy](#135-118-beta-podsecuritypolicy)
  - [13.6 NetworkPolicy](#136-networkpolicy)
  - [13.7 認証／認可とAdmission Control](#137-認証認可とadmission-control)

# 第1章 Docker の復習と「Hello, Kubernetes」

## 1.1 Docker の復習

## 1.2 さあ、Kubernetes の世界へ

# 第2章 なぜKubernetes が必要なのか？

## 2.1 Kubernetes とは

- Kubernetes Node
  - 実際にコンテナが動作するノード（物理マシン, 仮想マシン）
- Kubernetes Master
  - Kubernetes Nodeを管理するノード

## 2.2 Kubernetes の歴史

## 2.3 Kubernetes を使うと何ができるのか

- コンテナ運用の課題
  - 複数のKubernetes Nodeの管理
  - コンテナのスケジューリング
  - ローリングアップデート
  - スケーリング・オートスケーリング
  - コンテナの死活監視
  - 障害時のセルフヒーリング
  - ロードバランシング
  - データの管理
  - ワークロードの管理
  - ログの管理
  - IaC
  - その他エコシステムとの連携や拡張
- ワークロード
  - Kubernetes上で実行中のアプリケーションのこと

### 2.3.1 宣言的なコードによる管理(IaC)

- マニフェストファイルで宣言的にリソースを管理できる(IaC)
  - .yaml形式で管理することが多い

### 2.3.2 スケーリング/オートスケール

- コンテナのレプリカを自動増減（オートスケール）することで、負荷分散や耐障害性を確保できる

### 2.3.3 スケジューリング

- どのKubernetes Nodeにコンテナを配置するのか判断するステップのこと
- Affinity, Anti-Affinity機能

### 2.3.4 リソース管理

- Kubernetes NodeのCPUやメモリの空リソースをみて、Kubernetesが自動的に判断して実行する（ユーザーが管理する必要なし）
- クラスタオートスケール機能では、Kubernetes Node自体の増減も自動的に行える

### 2.3.5 セルフヒーリングƒ

- Kubernetesがコンテナのプロセス監視を行う
- プロセス停止を検知するとコンテナを再デプロイする
- Kubernetes Nodeに障害が発生しても、アプリケーションを自動復旧するようなつくり

### 2.3.6 ロードバランシングとサービスディスカバリ

- ロードバランシング機能
  - Service, Ingressなどの機能が存在する
  - アプリケーションのコンテナ群に対してルーティングを行うエンドポイントを払い出す
  - オートスケールや障害発生時には、Kubernetesが自動的に切り替える
- Service
  - サービスディスカバリが可能
  - マイクロサービスアーキテクチャに効果的
  - 各サービスのマニフェストファイルを元に、システム全体を簡単に連携できる

### 2.3.7 データの管理

- データストアにetcdを採用している(KVS)
  - マニフェストファイルやServiceなどを保持する
  - 認証情報や設定ファイルなどを保持できる仕組みもあるため、Kubernetes上で集中管理できる
- サードパーティ連携
  - Ansible
    - Kubernetesへのコンテナのデプロイ
  - Apache Ignite
    - Kubernetesのサービスディスカバリを利用したクラスタ形成とスケーリング
  - Fluentd
    - Kubernetes上のコンテナのログを転送
  - GitLab
    - CI/CDを実現するための一連の様々なツールとKubernetesの統合
  - Jenkins
    - ジョブ実行時にジョブワーカー用のコンテナをKubernetesにデプロイ
  - Prometheus
    - Kubernetesのモニタリング
  - Spark
    - ジョブをKubernetes上でネイティブ実行（YARN代替）
  - Spinnaker
    - Kubernetesへのコンテナのデプロイ
  - Kubeflow
    - Kubernetes上にML Platformをデプロイ
  - Rook
    - Kubernetes上に分散ファイルシステムをデプロイ
  - Vitess
    - Kubernetes上にMySQLクラスタをデプロイ

## 2.4 まとめ

# 第3章 Kubernetes 環境の選択肢

## 3.1 Kubernetes 環境の種別

- ローカルKubernetes
  - Minikube
  - Docker Desktop
  - kind (Kubernetes in Docker)
- Kubernetes構築ツール
  - kubeadm
  - Rancher
- パブリッククラウド
  - GKE
  - AKS
  - EKAS

## 3.2 ローカルKubernetes

### 3.2.1 Minikube

- シングルノード構成
- 複数台構成が必要なKubernetesの機能は使用できない

### 3.2.2 Docker Desktop for Mac

### 3.2.3 kind (Kubernetes in Docker)

- ローカル環境でマルチノードクラスタを構築できる
- kindで使用するDockerイメージはDockerHubのkindest Organizationで管理されている

## 3.3 Kubernetes 構築ツール

### 3.3.1 Kubernetesのサービスレベル目標(SLO)

### 3.3.2 kubeadm

- Kubernetes公式の構築ツール

### 3.3.3 Flannel

- Kubernetesクラスタ内のPod同士の通信（Podネットワーク）を実現するもの

### 3.3.4 Rancher

- Kubernetesの構築・運用をサポートする機能を持つ
  - 複数クラスタの統合管理
  - Kubernetesクラスタのデプロイ（AWS, OpenStack, VMware, ...etc）
  - 既存のKubernetesクラスタをRancherで管理（クラスタのインポート機能）
  - 複数クラスタに対するアプリケーションデプロイ機能
  - WebUIの提供（認証・モニタリングなど可能）

## 3.4 パブリッククラウド上のマネージドKubernetes サービス

### 3.4.1 GKE (Google Kubernetes Engine)

- GCE (Google Compute Engine)
  - 24時間で自動停止するインスタンス
  - 安い
- Preemptible-killer
  - ランダムにノードを入れ替えることができる
- Cloud Logging
  - GKEのログを集約する
- NodePool

  - GKE特有の機能
  - Nodeにラベリングしてグルーピングができる

  ```mermaid
  graph

  subgraph Kubernetes Cluster
    subgraph "NodePool A (High CPU)"
      A["NodePoor: A"]
      B["NodePoor: A"]
      C["NodePoor: A"]
    end

    subgraph "NodePool B (High Memory)"
      E["NodePoor: B"]
      F["NodePoor: B"]
    end
  end
  ```

- GCPのコマンドラインツールで操作する

### 3.4.2 AKS (Azure Kubernetes Service)

### 3.4.3 EKS (Elastic Kubernetes Service)

- IAMとKubernetesユーザーを紐づけられる
- EC2インスタンスをKubernetes Nodeとして利用する
- EKS on Fargateというのもある
  - FargateをKubernetes Nodeとして利用する
  - 一部のKubernetesコンポーネントがまだマネージドでない可能性あり
- eksctlで操作する

## 3.5 Kubernetes プレイグラウンド

## 3.6 まとめ

# 第4章 API リソースとkubectl

## 4.1 本章以降を読み進めるための準備

- kindでcluster構築

  ```shell
  # クラスタ作成
  ## kindという名前のクラスタを作成
  kind create cluster
  ## k8sという名前のクラスタを作成
  kind create cluster --name=k8s

  # クラスタ削除
  ## kindという名前のクラスタを削除
  kind delete cluster
  ## k8sという名前のクラスタを削除
  kind delete cluster --name=k8s
  ```

## 4.2 Kubernetes の基礎

- Kubernetesの各ノード
  - Kubernetes Master
    - APIエンドポイントの提供
    - コンテナのスケジューリング、スケーリング
  - Kubernetes Node
    - コンテナを起動
- Kubernetes Masterへのリソースの登録
  - kubectlとマニフェストファイルで行う
  - kubectlがマニフェストファイルの内容に基づいて、Kubernetes MasterのAPIにリクエストを送信してKubernetesを操作する

## 4.3 Kubernetes とリソース

- Kubernetesのリソース

  | 種別                           | 概要                                                         |
  | ------------------------------ | ------------------------------------------------------------ |
  | Workload APIs カテゴリ         | コンテナの実行に関するリソース                               |
  | Service APIs カテゴリ          | コンテナを外部公開するようなエンドポイントを提供するリソース |
  | Config & Storage APIs カテゴリ | 設定 / 機密情報 / 永続化ボリュームに関するリソース           |
  | Cluster APIs カテゴリ          | セキュリティやクォータなどに関するリソース                   |
  | Metadata APIs カテゴリ         | クラスタ内の他リソースを操作するためのリソース               |

### 4.3.1 Workloads APIs カテゴリ

- クラスタ上にコンテナを起動させるためのリソース
- リソースの種類
  - Pod
  - ReplicationController
  - ReplicaSet
  - Deployment
  - DaemonSet
  - StatefulSet
  - Job
  - CronJob

### 4.3.2 Service APIs カテゴリ

- コンテナのサービスディスカバリや、クラスタの外部からアクセス可能なエンドポイントを提供するリソース
- リソースの種類
  - Service
    - ClusterIP
    - ExternalIP (ClusterIPの一種)
    - NodePort
    - LoadBalancer
    - Headless (None)
    - ExternalName
    - None-Selector
  - Ingress

### 4.3.3 Config & Storage APIs カテゴリ

- 設定や機密データをコンテナに埋め込んだり、永続ボリュームを提供するリソース
- リソースの種類
  - Secret
  - ConfigMap
  - PersistentVolumeClaim

### 4.3.4 Cluster APIs カテゴリ

- クラスタ自体の振る舞いを定義するリソース
- リソースの種類
  - Node
  - Namespace
  - PersistentVolume
  - ResourceQuota
  - ServiceAccount
  - Role
  - ClusterRole
  - RoleBinding
  - ClusterRoleBinding
  - NetworkPolicy

### 4.3.5 Metadata APIs カテゴリ

- クラスタ内の他のリソースの動作を制御するためのリソース
- リソースの種類
  - LimitRange
  - HorizontalPodAutoscaler
  - PodDisruptionBudget
  - CustomResourceDefinition

## 4.4 Namespace による仮想的なクラスタの分離

- Namespace
  - 仮想的なKubernetesクラスタの分離機能のこと
- Namespaceでできること
  - 本番環境、ステージング環境、開発環境のように、環境ごとに分割すること
  - 同じKubernetesクラスタを複数チームでの利用すること
- Namespaceの慣習
  - kube-system
    - Kubernetes Dashboardなどのシステムコンポーネントやアドオンをデプロイする
  - kube-public
    - 全ユーザーが共通して利用する設定値などを保存する
  - kube-node-lease
    - Kubernetes Nodeのハードビート情報を保存するためのLeaseリソースを保存する
  - default
    - ユーザーが任意のリソースを登録する
- Namespace、RBAC (RoleBased Access Control)、Network Policyを組み合わせることで分離性を高められる
- Namespaceの分割粒度
  - マイクロサービス単位（開発チーム単位）での分割が好ましい。（権限分離性の観点で）
- クラスタの分離粒度
  - 本番環境、ステージング環境、開発環境の環境単位でクラスタごと分離するのが好ましい
  - 理由
    - すべての環境で同時に障害が発生するリスクがあるため
    - マニフェストの再利用性が著しく低下するため
    - 環境名を考慮した命名が必要で煩雑になるため

## 4.5 CLI ツールkubectl

- クラスタの操作方法
  - Kubernetes MasterのAPI
  - クライアントライブラリ
  - CLIツール「kubectl」 => 最も一般的

### 4.5.1 認証情報とContext (config)

- kubeconfig

  - Kubernetes Masterとの通信に必要な認証情報などを記述する

    ```yaml
    # ~/.kube/config

    apiVersion: v1
    kind: Config
    preferences: {}
    clusters: # 接続先クラスタ
      - name: sample-cluster
        cluster:
          server: https://localhost:6443
    users: # 認証情報
      - name: sample-user
        user:
          client-certificate-data: LS0tLS1CRUdJTi...
          client-key-data: LS0tLS1CRUdJTi...
    contexts: # 接続先と認証情報の組み合わせ
      - name: sample-context
        context:
          cluster: sample-cluster
          namespace: default
          user: sample-user
    current-context: sample-context
    ```

- kubeconfigの設定変更の方法
  - kubeconfigを直接編集する
  - kubectlコマンドで設定変更（kubeconfigファイルも自動的に更新される）

### 4.5.2 Kubectx / kubensによる切り替え

- ContextやNamespaceを簡単に切り替えられるOSS

### 4.5.3 マニフェストとリソースの作成 / 削除 / 更新 (create / delete / apply)

- リソース操作
  - 作成
    - `kubectl create -f hoge.yaml`
  - 削除
    - `kubectl delete -f hoge.yaml`
    - オプション
      - `--wait`：削除完了するまで待機する
      - `--force`：強制削除
  - 更新
    - `kubectl apply -f hoge.yaml`
    - applyできないフィールドも存在する
- Podのイメージの詳細確認
  - `kubectl get pod Pod名 -o jsonpath={}`
  - `kubectl get pod Pod名 -o jsonpath={.spec.containers}`

### 4.5.4 リソース作成にも kubectl apply を使うべき理由

- 常に`kubectl apply`を使用するべき
- 理由：差分検知が想定通りに動作しないケースがあるため

### 4.5.5 Server-side apply

- Client-side apply
  - コマンド: `kubectl apply -f hoge.yaml`
  - 手元のマニフェストファイルで更新してしまうため、サーバ側の情報を直接書き換えたりしていると内容を破棄してしまうケースがある
- Server-side apply
  - コマンド: `kubectl apply -f hoge.yaml --server-side`
  - サーバ側の実態とマニフェストを比較し、コンフリクトがある場合は処理を中断する
  - `--force-conflicts`で、コンフリクトを無視してマニフェストファイルの内容で更新する

### 4.5.6 Pod の再起動 (rollout restart)

- リソースに紐づくPodを再起動する
  - `kubectl rollout restart リソースの種類 リソース名`
- 注意点: Podに対して直接実行することはできない
  - `kubectl rollout restart pod Pod名`はエラーで動作しない

### 4.5.7 generateNameによるランダムな名前のリソースの作成

- マニフェストファイルでランダムな名前のリソースを定義可能
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    generateName: hoge- # hoge-cglj9 のようなランダムなリソース名にできる
  spec:
    containers:
      - name: nginx-container
        image: nginx:1.16
  ```
- 注意点
  - createでのみ利用可能
  - applyでは不可能

### 4.5.8 リソースの状態のチェックと待機(wait)

- 構文
  - `kubectl wait --for=条件 リソースを指定`
- 例
  - Podの起動を待機する場合
    - `kubectl wait --for=condition=Ready pod/Pod名`
  - Podの削除を待機する場合
    - `kubectl wait --for=delete pod --all --timeout=5s`
  - マニフェストファイルでPodの起動を待機する場合
    - `kubectl wait --for=condition=Ready -f マニフェストファイルのPath`

### 4.5.9 マニフェストファイルの設計

#### 1つのマニフェストファイルの中に複数のリソースを記述する

- マニフェストファイルのユースケース
  - 1つのマニフェストファイルにまとめるケース
    - 「Podを起動するWorkloads APIsカテゴリのリソース」と「外部公開するService APIsカテゴリのリソース」をまとめることで、1つのマニフェストファイルでサービスを公開できるようにしたいケース
  - マニフェストファイルを分割するケース
    - 設定ファイル（ConfigMapリソース）やパスワード（Secretリソース）を共通化したいケース
- 複数リソースの記述方法
  - `---`で区切る

#### 複数のマニフェストファイルを同時に適用する

- ディレクトリ構成が以下の場合
  ```
  ./
  ├── sample-pod1.yaml
  ├── sample-pod2.yaml
  └── innerdir
      └── sample-pod3.yaml
  ```
- ディレクトリ内のマニフェストファイルを適用
  - `kubectl apply -f ./`
- ディレクトリ内のマニフェストファイルを再帰的に適用（サブディレクトリ内のマニフェストも適用）
  - `kubectl apply -f ./ -R`

#### マニフェストファイルの設計指針

- マイクロサービス単位でマニフェストファイルを分割するパターン
  ```
  ./whole-system
  ├── microservice-A.yaml (Deployment + Service)
  ├── microservice-B.yaml (Deployment + Service)
  ├── microservice-C.yaml (Deployment + Service)
  └── microservice-D.yaml (Deployment + Service)
  ```
  - メリット
    - マイクロサービス単位で適用できること
- マイクロサービス単位でディレクトリを分割するパターン

  ```
  ./microservice-A/
  ├── deployment.yaml
  └── service.yaml

  ./microservice-B/
  ├── deployment.yaml
  └── service.yaml

  ./microservice-C/
  ├── deployment.yaml
  └── service.yaml

  ./microservice-D/
  ├── deployment.yaml
  └── service.yaml
  ```

  - メリット
    - 可読性が高まること
  - デメリット
    - 適用の順序制御が難しい

### 4.5.10 アノテーションとラベル (annotate / label)

- アノテーション
  - システムコンポーネントが利用するメタデータ
- ラベル
  - リソース管理に利用するメタデータ

#### アノテーション (annotate)

- マニフェストファイルの`metadata.annotations`で設定できるメタデータ
- アノテーションのデータ構造
  - Key-Value形式
- アノテーションの用途
  - システムコンポーネントのためにデータを保存する
  - すべての環境では利用できない設定を行う
  - 正式に組み込まれる前の機能の設定を行う

##### システムコンポーネントのためにデータを保存する

##### すべての環境では利用できない設定を行う

- 「GKE / AKS / EKS」それぞれに独自の拡張機能があり、その設定にアノテーションを使うケースが多い

##### 正式に組み込まれる前の機能の設定を行う

#### ラベル (label)

- マニフェストファイルの`metadata.labels`で設定できるメタデータ
- ラベルの用途
  - 開発者が利用するラベル
  - システムが利用するラベル

##### システムが利用するラベル

- ラベルをもとにリソースをフィルタリングしたり指定できる
  - `kubectl get pods -l label1=val1,label2`

##### システムが利用するラベル

- ラベルが衝突することによる副作用が発生するケースが考えられる
  - Podの数を維持するリソース(ReplicaSet)にて、停止させるべきでないPodを停止させてしまうケース
  - ロードバランサからPodにリクエストを転送するリソース(LoadBalancer)にて、転送するべきでないPodに転送してしまうケース
- 推奨されるラベル

  | ラベルのキー名               | 概要                                               |
  | ---------------------------- | -------------------------------------------------- |
  | app.kubernetes.io/name       | アプリケーションの名前                             |
  | app.kubernetes.io/version    | アプリケーションのバージョン                       |
  | app.kubernetes.io/component  | アプリケーションの役割                             |
  | app.kubernetes.io/part-of    | アプリケーションが全体として構成するシステムの名前 |
  | app.kubernetes.io/instance   | アプリケーションやシステムを識別するインスタンス名 |
  | app.kubernetes.io/managed-by | アプリケーションが管理されているツール             |

### 4.5.11 Pruneによるリソースの削除 (--pruneオプション)

- Kubernetesを実運用する場合

  - マニフェストファイルをGit管理
  - マニフェストファイルをスクリプトで自動実行

  ```mermaid
  flowchart LR
    A[(マニフェスト<br>Git リポジトリ)]
    B["スクリプト"]
    C["Kubernetesクラスタ"]
    D["開発者"]

    A--git clone-->B
    B--kubectl apply -f-->C
    D--NG: kubectl apply -f<br>実運用では自動化する-->C
    D--マニフェストの追加/変更-->A
  ```

- `apply`だけだと、マニフェストから削除されたリソースを削除できない
- 「`--prune`オプション」を付与することで、削除されたリソースを検知して自動削除できる
- `--prune`の仕組み
  - ラベルに一致する全リソースのうち、マニフェストファイルに含まれないリソースを削除する挙動をとる

### 4.5.12 エディターによる編集j (edit)

### 4.5.13 リソースの一部情報の更新 (set)

- マニフェストファイルを更新せずにリソースを更新する方法
  - env
  - image
  - resource
  - selector
  - serviceaccount
  - subject
- 注意点
  - リソースを更新しても、マニフェストファイルは更新されないため乱用すべきでない

### 4.5.14 ローカルマニフェストとKubernetes上の登録情報の差分取得 (diff)

- マニフェストファイルとリソースの差分を表示できる
  - `kubectl diff -f hoge.yaml`

### 4.5.15 利用可能なリソース種別の一覧取得 (api-resources)

### 4.5.16 リソースの情報取得 (get)

- Pod一覧
  - `kubectl get pods`
- 特定のPod
  - `kubectl get pod hoge-pod`
- 特定のラベルを持つPod
  - `kubectl get pod -l label1=val1`
- 詳細情報を表示
  - `kubectl get pods -o wide`
  - `kubectl get pods -o yaml`
  - `kubectl get pods -o json`
  - `kubectl get pods -o json hoge-pod`
- Node一覧
  - `kubectl get nodes`
- ほぼすべての種類のリソースを表示
  - `kubectl get all`
- すべての種類のリソースを表示
  - `kubectl get $(kubectl api-resources --namespeced=true --verbs=list -o name | tr '\n' ',' | sed -e 's|,$||g')`
- リソースの状態変化を表示
  - `kubectl get pods --watch`
  - `kubectl get pods --watch --output-watch-events`

### 4.5.17 リソースの詳細情報の取得 (describe)

- リソースの詳細情報を表示
  - `kubectl describe pod hoge-pod`
- 確認できる情報
  - Event配下で、リソースの状態遷移などのライフサイクル情報が確認できる
  - など

### 4.5.18 実際のリソースの使用量の確認 (top)

- リソースの使用量を確認
  - `kubectl top node`
  - `kubectl top pod`

### 4.5.19 コンテナ上でのコマンドの実行 (exec)

- Pod内のコンテナでbash
  - `kubectl exec -it hoge-pod -- /bin/bash`
- Pod内の特定のコンテナでbash
  - `kubectl exec -it hoge-pod -c hoge-container -- /bin/bash`

### 4.5.20 Pod上にデバッグ用の一時的なコンテナの追加 (debug)

- 課題
  - 最小限のコンテナイメージで`kubectl exec`しても、ツールが揃っておらずデバッグが困難である
- 解決策
  - 一時的なコンテナを起動して、そのコンテナのツールを利用してデバッグできるようにする
  - `kubectl debug sample-pod --image=amsy810/tools:v2.0 -it -- bash`

### 4.5.21 ローカルマシンからPodへのポートフォワーディング (port-forward)

- ホストの8888ポートへのリクエストをPodの80番ポートに転送する
  - `kubectl port-forward hoge-pod 8888:80`

### 4.5.22 コンテナのログ確認

- Kubernetesでのロギングのベストプラクティス
  - 標準出力、標準エラー出力にログを出力すること
- Kubernetesでのログの確認方法
  - `kubectl logs hoge-pod`
  - `kubectl logs hoge-pod -c hoge-container`
- １つのPodのログを監視し続けたい場合
  - `kubectl logs -f hoge-pod`
- 複数のPodのログを監視し続けたい場合（該当するラベルのログ）
  - `kubectl logs --selector app=hoge-app`

### 4.5.23 Sternによる高度なログ確認

- Stern
  - 高機能なログ出力をサポートするOSS
- できること
  - Pod名のサフィックスなどで絞り込んで複数Podのログ出力
  - Podごとに色分けしてログ出力

### 4.5.24 コンテナとローカルマシン間でのファイルのコピー (cp)

- hoge-pod内の/etc/hostnameファイルをローカルマシンにコピー
  - `kubectl cp hoge-pod:/etc/hostname ./hostname`
- ローカルマシンのhostnameファイルをhoge-pod内の/etc/hostnameにコピー
  - `kubectl cp ./hostname hoge-pod:/etc/hostname`

### 4.5.25 kubectl pluginとパッケージマネージャ (plugin / krew)

- krewをセットアップ

  - 手順(https://krew.sigs.k8s.io/docs/user-guide/setup/install/)
  - gitインストール

    ```shell
    sudo apt install -y git
    ```

  - パッケージ取得

    ```shell
    (
      set -x; cd "$(mktemp -d)" &&
      OS="$(uname | tr '[:upper:]' '[:lower:]')" &&
      ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" &&
      KREW="krew-${OS}_${ARCH}" &&
      curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&
      tar zxvf "${KREW}.tar.gz" &&
      ./"${KREW}" install krew
    )
    ```

  - bashにPATHを追加

    ```shell
    # ~/.bashrc
    export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
    ```

- plugin一覧

  ```shell
  kubectl pluglin list
  #=> The following compatible plugins are available:
  #=> /home/user/.krew/bin/kubectl-krew
  ```

- plugin追加

  ```shell
  kubectl krew install plugin名
  ```

## 4.6 まとめ

# 第5章 Workloads APIs カテゴリ

## 5.1 Workloads APIs カテゴリの概要

## 5.2 Pod

## 5.3 ReplicaSet ／ ReplicationController

## 5.4 Deployment

## 5.5 DaemonSet

## 5.6 StatefulSet

## 5.7 Job

## 5.8 CronJob

## 5.9 まとめ

# 第6章 Service APIs カテゴリ

## 6.1 Service APIs カテゴリの概要

## 6.2 Kubernetes クラスタのネットワークとService

## 6.3 ClusterIP Service

## 6.4 ExternalIP Service

## 6.5 NodePort Service

## 6.6 LoadBalancer Service

## 6.7 Service のその他の機能

## 6.8 Headless Service（None）

## 6.9 ExternalName Service

## 6.10 None-Selector Service

## 6.11 Ingress

## 6.12 まとめ

# 第7章 Config ＆ Storage APIs カテゴリ

## 7.1 Config ＆ Storage APIs カテゴリの概要

## 7.2 環境変数の利用

## 7.3 Secret

## 7.4 ConfigMap

## 7.5 PersistentVolumeClaim

## 7.6 Volume

## 7.7 PersistentVolume（PV）

## 7.8 PersistentVolumeClaim (PVC)

## 7.9 volumeMounts で利用可能なオプション

## 7.10 まとめ

# 第8章 Cluster APIs カテゴリとMetadata APIs カテゴリ

## 8.1 Cluster APIs カテゴリとMetadata APIs カテゴリの概要

## 8.2 Node

## 8.3 Namespace

## 8.4 まとめ

# 第9章 リソース管理とオートスケーリング

## 9.1 リソースの制限

## 9.2 Cluster Autoscaler とリソース不足

## 9.3 LimitRange によるリソース制限

## 9.4 QoS Class

## 9.5 ResourceQuota によるNamespace のリソースクォータ制限

## 9.6 HorizontalPodAutoscaler（HPA）

## 9.7 VerticalPodAutoscaler（VPA）

## 9.8 まとめ

# 第10章 ヘルスチェックとコンテナのライフサイクル

## 10.1 ヘルスチェック

## 10.2 コンテナのライフサイクルと再始動（restartPolicy）

## 10.3 Init Containers

## 10.4 起動直後と終了直前に任意のコマンドを実行する（postStart ／ preStop）

## 10.5 Pod の安全な停止とタイミング

## 10.6 リソースを削除した時の挙動

## 10.7 まとめ

# 第11章 メンテナンスとノードの停止

## 11.1 ノードの停止とPod の停止

## 11.2 スケジューリング対象からの除外と復帰（cordon ／ uncordon）

## 11.3 ノードの排出処理によるPod の退避（drain）

## 11.4 PodDisruptionBudget（PDB）による安全な退避

## 11.5 まとめ

# 第12章 高度で柔軟なスケジューリング

## 12.1 フィルタリングとスコアリング

## 12.2 マニフェストで指定するスケジューリング

## 12.3 ビルトインノードラベルとラベルの追加

## 12.4 nodeSelector（Simple Node Affinity）

## 12.5 Node Affinity

## 12.6 matchExpressions のオペレータとset-based 条件

## 12.7 Node Anti-Affinity

## 12.8 Inter-Pod Affinity

## 12.9 Inter-Pod Anti-Affinity

## 12.10 複数の条件を組み合わせたPod のスケジューリング

## 12.11 1.18 Beta TopologySpreadConstraints によるトポロジ均衡

## 12.12 Taints とTolerations

## 12.13 PriorityClass によるPod の優先度と退避

## 12.14 その他のスケジューリング

## 12.15 まとめ

# 第13章 セキュリティ

## 13.1 ServiceAccount

## 13.2 RBAC（Role Based Access Control）

## 13.3 SecurityContext

## 13.4 PodSecurityContext

## 13.5 1.18 Beta PodSecurityPolicy

## 13.6 NetworkPolicy

## 13.7 認証／認可とAdmission Control
