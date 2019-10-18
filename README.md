# api-gateway-settings

## 概要

- API Gateway でログを出力されたい場合には、Region単位でAPI Gatewayの設定が必要になる。
- 各サービス単位のCloudFormationのテンプレートでこれを組み込むと冗長になるため、API Gatewayの設定は切り離して実施するためのテンプレート。

## 使い方

```sh
aws cloudformation create-stack \
    --stack-name api-gateway-settings \
    --capabilities CAPABILITY_IAM \
    --template-body file://template.yaml
```

作成後、以下のコマンドでAPI Gatewayの設定画面のURLが取得可能

```sh
aws cloudformation describe-stacks \
    --stack-name api-gateway-settings \
    --query 'Stacks[].Outputs[?OutputKey==`SettingsUrl`].OutputValue' \
    --output text
  # https://ap-northeast-1.console.aws.amazon.com/apigateway/home?region=ap-northeast-1#/settings
```

**CloudWatch log role ARN** にRoleのARNが設定されていれば、API Gatewayでログ出力は可能です。
