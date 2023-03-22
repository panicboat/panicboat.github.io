# Kubernetes 公式ドキュメントの学習環境を EKS on Fargate でやってみた

## 事前準備

### ツールのインストール

1. [kubectl のインストールまたは更新](https://docs.aws.amazon.com/ja_jp/eks/latest/userguide/install-kubectl.html)
1. [eksctl のインストールまたは更新](https://docs.aws.amazon.com/ja_jp/eks/latest/userguide/eksctl.html)


### Cloudリソースの構築

[cdk](https://github.com/panicboat/infrastructures)を利用して以下を構築

1. VPC
1. EKS on Fargate

```
make build TARGET=sandbox
make plan TARGET=sandbox ENV=development
make deploy TARGET=sandbox ENV=development
```

### aws eks update-kubeconfig

1. aws sso login --profile sandbox
1. AWS_ACCOUNT_ID=\`aws sts get-caller-identity --query Account --output text\`
1. aws eks update-kubeconfig --name sandbox --region ap-northeast-1 --role-arn arn:aws:iam::${AWS_ACCOUNT_ID}:role/sandboxEksRole
1. kubectl get namespaces
