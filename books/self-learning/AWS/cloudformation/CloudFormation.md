# AWS CloudFormation

## AWS CloudFormation とは？

[AWS CloudFormation ](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/Welcome.html) :
とはテンプレートから AWS リソース（EC2 RDS S3 VPC Subnet など）を自動構築するためのサービスである。

## 概要

<img src='https://wakuwakubank.imgix.net/S3Doc/dc/c2/1f/dc3cd8d6311c1ca2b8761ef291db54c815e263eb0aa7f72ddfe8129bb3' width='50%'>

`テンプレート` : どの AWS リソースをどのような設定で起動するかコードで記述したもの。

`スタック` : テンプレートから生成される AWS リソースの集合です。スタック を消すと、紐づくリソースも全て消えます。

## UI から設定

1. stack 作成ボタンを押し、テンプレートファイルを選択

<img src='../img/CloudFormation01.png' width='50%'>

2. stack 名を追記

<img src='../img/CloudFormation02.png' width='50%'>

3. Stack オプションを設定（基本残す）

- タグをつける ex) name -> stack01
- ロールバック・・・slack 作成時に失敗してしまったときに途中まで作成した個所をロールバックする
- スタックの作成オプション・・・ロールバックは基本残す

4. 確認画面から作成を選択する

## 参考

- https://www.wakuwakubank.com/posts/489-aws-cloudformation/
- https://www.itc109.com/knowledge/aws/get-aws-vpc
