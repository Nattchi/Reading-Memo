# AWSコンテナ設計・構築［本格］入門

## 2-1 AWS が提供するコンテナサービス

コントロールプレーン: コンテナを管理する機能

AWSでは…
### Amazon Elastic Container Service (ECS)

コンテナのオーケストレーションサービス

### Amazon Elastic Kubernetes Service (EKS)

Kubernetes コントロールプレーンの管理をAWSに移譲できる

データプレーン: コンテナが実際に稼働するリソース環境

AWSでは…
### Amazon Elastic Compute Cloud (EC2)

AWS上で仮想マシンを稼働できるサービス

ECSやEKSで動かすデータプレーンとして利用されることも

### AWS Fargate (Fargate)

ECS, EKS の両者で動作するコンテナ向けサービス

メリット: ホストの管理が不要
デメリット: OSに直接介入できない

リポジトリ: コンテナイメージを管理するリポジトリ
AWSでは…
### Amazon Elastic Container Resistry (ECR)
レジストリ: リポジトリを管理・格納する場所(サーバーやサービス)

簡単にコンテナイメージを保存・管理

### AWS Lambda (Lambda)
コードをアップロードするだけで実行ができるサービス

### AWS App Runner (App Runner)
プロダクションレベルでスケール可能なWebアプリケーションを展開するためのマネージドサービス

デプロイ方法: GitHub, ECRビルド済みコンテナイメージ

## 2.2 アーキテクチャの構成例



