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
    - [Workloads APIs カテゴリ](#workloads-apis-カテゴリ)
    - [Service APIs カテゴリ](#service-apis-カテゴリ)
    - [Config & Storage APIs カテゴリ](#config--storage-apis-カテゴリ)
    - [Cluster APIs カテゴリ](#cluster-apis-カテゴリ)
    - [Metadata APIs カテゴリ](#metadata-apis-カテゴリ)
  - [4.4 Namespace による仮想的なクラスタの分離](#44-namespace-による仮想的なクラスタの分離)
  - [4.5 CLI ツールkubectl](#45-cli-ツールkubectl)
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
  | 種別 | 概要 |
  | --- | --- |
  | Workload APIs カテゴリ | コンテナの実行に関するリソース |
  | Service APIs カテゴリ | コンテナを外部公開するようなエンドポイントを提供するリソース |
  | Config & Storage APIs カテゴリ | 設定 / 機密情報 / 永続化ボリュームに関するリソース |
  | Cluster APIs カテゴリ | セキュリティやクォータなどに関するリソース |
  | Metadata APIs カテゴリ | クラスタ内の他リソースを操作するためのリソース |

### Workloads APIs カテゴリ

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

### Service APIs カテゴリ

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

### Config & Storage APIs カテゴリ

- 設定や機密データをコンテナに埋め込んだり、永続ボリュームを提供するリソース
- リソースの種類
  - Secret
  - ConfigMap
  - PersistentVolumeClaim

### Cluster APIs カテゴリ

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

### Metadata APIs カテゴリ

- クラスタ内の他のリソースの動作を制御するためのリソース
- リソースの種類
  - LimitRange
  - HorizontalPodAutoscaler
  - PodDisruptionBudget
  - CustomResourceDefinition

## 4.4 Namespace による仮想的なクラスタの分離

## 4.5 CLI ツールkubectl

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
