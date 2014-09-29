AWS CloudFormation 入門
===
# 目的
AWS CloudFormationの[公式ガイド](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)入門部分を日本語解説する。

# 前提
| ソフトウェア     | バージョン    | 備考         |
|:---------------|:-------------|:------------|
| OS X           |10.8.5        |             |
|           　　　|        |             |

# 構成
+ [AWS CloudFormationとは](#1)
+ [はじめに](#2)
+ [IAMによるアクセスコントロール](#3)

# 詳細
## <a name="1">AWS CloudFormationとは</a>
What is AWS CloudFormation?

AWS CloudFormation is a service that helps you model and set up your Amazon Web Services resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and AWS CloudFormation takes care of provisioning and configuring those resources for you. You don't need to individually create and configure AWS resources and figure out what's dependent on what; AWS CloudFormation handles all of that. The following scenarios demonstrate how AWS CloudFormation help.

### AWS CloudFormationとは

AWS CloudFormationとはAWS内のリソース管理の手間を減らし自分のアプリケーションにより集中することを手助けするサービスです。必要な全てのAWSリソース(EC2インスタンスやRDS DBインスタンス)をテンプレート内に記述できます。そしてCloudFormationはプロビジュニングから設定まで面倒を見てくれます。個別にAWSリソースを作ったり依存関係を明記する必要はありません、CloudFormationが全てやってくれます。以下のシナリオでどのようにCloudFormationを使うかを解説します。

Simplify Infrastructure Management

For a scalable web application that also includes a back-end database, you might use an Auto Scaling group, an Elastic Load Balancing load balancer, and an Amazon Relational Database Service database instance. Normally, you might use each individual service to provision these resources. And after you create the resources, you would have to configure them to work together. All these tasks can add complexity and time before you even get your application up and running.

Instead, you can create or modify an existing AWS CloudFormation template. Templates describes all of your resources and their properties. When you use that template to create an AWS CloudFormation stack, AWS CloudFormation provisions the Auto Scaling group, load balancer, and database for you. After the stack has been successfully created, your AWS resources are up and running. You can delete the stack just as easily, which deletes all the resources in the stack. By using AWS CloudFormation, you easily manage a collection of resources as a single unit.

#### 簡単にインフラ管理

バックエンドにデータベースを稼働させている拡張性のあるwebアプリケーションではElastic Load BalancingやRDSサービスインスタンスを使う必要があります。通常は個別に各リソースを設定します。リソースを作成した後それらのサービスがうまく共同で動くように設定する必要が有ります。これらの作業は複雑で時間がかかります。

代わりにAWS CloudFormationテンプレートを作ったり既存のテンプレートを編集することができます。テンプレートにはあなたが必要な全てのリソースとプロパティが記述されています。AWS CloudFormationスタックのテンプレートを作成したならオートスケールグループ、ロードバランサーそしてデータベースの構成をプロビジョニングしてくれます。スタックが無事に作成されたならばあなたのAWSリソースは稼働しています。簡単にスタックを削除できます。AWS CloudFormationを使うことでリソースの集合をひとつの単位として簡単に管理できます。

Quickly Replicate Your Infrastructure

If your application requires additional availability, you might replicate it in multiple regions so that if one region becomes unavailable, your users can still use your application in other regions. The challenge in replicating your application is that it also requires you to replicate your resources. Not only do you need to record all the resources that your application requires, but you must also provision and configure those resources in each region.

When you use AWS CloudFormation, you can reuse your template to set up your resources consistently and repeatedly. Just describe your resources once and then provision the same resources over and over in multiple regions.

#### インフラの素早い切り替え

もしアプリケーションに追加の可用性が必要になったなら複数のリージョンで変更する必要がある。アプリケーションの変更にはリソースの変更も必要になる。アプリケーションに必要な全てのリソースを記録する以外に複数のリージョンで繰り返し同じリソースのプロビジョニングをしなければならない。

AWS CloudFormationを使えば安定的に繰り返しテンプレートを再利用できる。一回リソースを記述すれば同じリソースを複数のリージョンで繰り返し使えます。

Easily Control and Track Changes to Your Infrastructure

In some cases, you might have underlying resources that you want to upgrade incrementally. For example, you might change to a higher performing instance type in your Auto Scaling launch configuration so that you can reduce the maximum number of instances in your Auto Scaling group. If problems occur after you complete the update, you might need to roll back your infrastructure to the original settings. To do this manually, you not only have to remember which resources were changed, you also have to know what the original settings were.

When you provision your infrastructure with AWS CloudFormation, the AWS CloudFormation template describes exactly what resources are provisioned and their settings. Because these templates are text files, you simply track differences in your templates to track changes to your infrastructure, similar to the way developers control revisions to source code. For example, you can use a version control system with your templates so that you know exactly what changes were made, who made them, and when. If at any point you need to reverse changes to your infrastructure, you can use a previous version of your template.

#### 簡単に管理できインフラの変更を追跡できる

いくつかのケースではリソースを継続的にアップグレードしたいでしょう。例えばオートスケールグループのインスタンスの最大数を減らすためより高いパフォーマンスのインスタンス変更する場合。もし、変更が完了した後に問題が発生したならオリジナルのセッテイングにロールバックする必要があります。手動だとリソースのどこが変わったかを覚えておく他にオリジナルのセッテイングがどうだったかも知っておく必要があります。

AWS CloudFormationでインフラをプロビジョニングした時、AWS CloudFormationはプロビジョニングされたリソースとセッテイングを正確に記録しています。なぜならテンプレートはテキストファイルだからです。ソース管理システムを使った開発と同じようにテンプレート内から簡単にインフラの変更を追跡できます。例えば、何が作られ、誰が作りそしていつなのかをバージョンコントロールシステムをテンプレートに適用することで正確に知ることができます。

Related Information

For more information about AWS CloudFormation stacks and templates, see AWS CloudFormation Concepts.

For an overview about how to use AWS CloudFormation, see How Does AWS CloudFormation Work?.

For pricing information, see AWS CloudFormation Pricing.

#### 関連情報

+ AWS CloudFormationのスタックとテンプレートに関しては[ここ](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-whatis-concepts.html)

+ AWS CloudFormationの概要に関しては[ここ](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-whatis-howdoesitwork.html)

+ 価格に関しては[ここ](http://aws.amazon.com/jp/cloudformation/pricing/)

### AWS CloudFormation Concepts

When you use AWS CloudFormation, you work with templates and stacks. You create templates to describe your AWS resources and their properties. Whenever you create a stack, AWS CloudFormation provisions the resources that are described in your template.

### AWS CloudFormationコンセプト

AWS CloudFormationを使う時、テンプレートとスタックを使います。AWSリソースとプロパティを記述したテンプレートを作る。スタックを作った時はいつでもAWS CloudFormationはテンプレートに書かれ内容をプロビジョニングします。

Templates

An AWS CloudFormation template is a text file whose format complies with the JSON standard. You can save these files with any extension, such as .json, .template, or .txt. AWS CloudFormation uses these templates as blueprints for building your AWS resources. For example, in a template, you can describe an Amazon EC2 instance, such as the instance type, the AMI ID, block device mappings, and its Amazon EC2 key pair name. Whenever you create a stack, you also specify a template that AWS CloudFormation uses to create whatever you described in the template.

テンプレート

AWS CloudFormationテンプレートはJSON形式でコンパイルされたテキストファイルです。.json、.templateまたは.txtといった拡張子のいずれでも使えます。AWS CloudFormationはテンプレートをAWSリソースを構築するブループリントとして使います。例えば、テンプレート内にAmazon EC2インスタンスのインスタンスタイプやAMI ID、ブロックデバイスそしてAmazon EC2キーペアを記述できます。スタックを作った時はいつでもAWS CloudFormationで使うテンプレートを特定できます。

Stacks

When you use AWS CloudFormation, you manage related resources as a single unit called a stack. In other words, you create, update, and delete a collection of resources by creating, updating, and deleting stacks. All the resources in a stack are defined by the stack's AWS CloudFormation template. Suppose you created a template that includes an Auto Scaling group, Elastic Load Balancing load balancer, and an Amazon RDS database instance. To create those resources, you create a stack by submitting the template that you created, and AWS CloudFormation provisions all those resources for you. To update resources, you first modify the original stack template and then update your stack by submitting the modified template. You can work with stacks by using the AWS CloudFormation console, API, or AWS CLI.

For more information about creating, updating, or deleting stacks, see Working with Stacks.

スタック

AWS CloudFormationを使っている時、関連するリソースをスタックと呼ばれる単一の単位で管理します。言い換えればスタックを作成、更新、削除することでリソースの集合を作成、更新、削除します。スタック内の全てのリソースはAWS CloudFormationテンプレートの集まりで定義されています。オートスケールグループ、ロードバランサー、RDSデータベースインスタンスを含んだテンプレートを作る手助けをしてくれます。これらのリソースを作るため、作成したテンプレートを組み合わせてスタックを作りAWS CloudFormationでそれら全てをプロビジョニングします。リソースをアップデートするためオリジナルのスタックテンプレートを編集して編集したテンプレートをスタックに反映することで更新します。AWS CloudFormationコンソール、APIまたはCLIからスタックを操作することができます。

スタックの作成、更新、削除に関する詳細は[ここ](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacks.html)



## <a name="2">はじめに</a>


## <a name="3">IAMによるアクセスコントロール</a>

# 参照

+ [AWS CloudFormation](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
