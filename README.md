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

How Does AWS CloudFormation Work?

Whenever you create a stack, AWS CloudFormation makes underlying service calls to AWS to provision and configure your resources. Note that AWS CloudFormation can only perform actions that you have permission to do. For example, to create Amazon EC2 instances by using AWS CloudFormation, you need permissions to create instances. You'll need similar permissions to terminate instances when you delete stacks with instances. You use AWS Identity and Access Management to manage permissions.

The calls that AWS CloudFormation makes are all declared by your template. For example, suppose you have a template that describes an Amazon EC2 instance with a t1.micro instance type. When you use that template to create a stack, AWS CloudFormation calls the Amazon EC2 create instance API and specifies the instance type as t1.micro. The following diagram summarizes the AWS CloudFormation create stack workflow:

### AWS CloudFormationはどのように動くのか

スタックを作った時はいつでも、AWS CloudFormationはリソースのプロビジョニングと設定をするためのサービスを実行する。AWS CloudFormationは許可されたことしか実行できないことに注意してください。例えばAWS CloudFormationを使ってEC2インスタンスを作った場合インスタンスを作成する許可が必要になります。インスタンスと一緒にスタックを削除する場合も同様に許可が必要になります。許可を管理するには AWS Identity and Access Managementを使ってください。

AWS CloudFormationから呼び出されるものは全てテンプレート内にあります。例えばt1.microインスタンスタイプのEC2インスタンスをテンプレートで利用する場合。スタックを作るためにテンプレートを使った時AWS CloudFormationはEC2インスタンス作成APIを呼び出しインスタンスタイプをt1.microに指定します。以下がAWS CloudFormationがスタックを作る流れです。

1. テンプレートを作るまたは再利用する

1. ローカルまたはS3バケットに保存する

1. AWS CloudFormationを使ってテンプレートを元にスタックのベースを作る

1. AWS CloudFormationが指定されたスタックリソースを構築・設定する

Update Stack Workflow

When you update a stack, you modify the original stack template. AWS CloudFormation compares the modified template with the original stack template and updates only the resources that you modified. The following diagram summarizes the update stack workflow:

スタック更新の流れ

スタックを更新した時、オリジナルスタックテンプレートを更新します。AWS CloudFormationはオリジナルスタックテンプレートと編集したテンプレートを比較して編集された部分だけリソースを更新します。以下がスタック更新の流れです。

1. テンプレート編集

1. ローカルまたはS3バケットに保存する

1. AWS CloudFormationを使ってテンプレートを元にスタックのベースを作る

1. AWS CloudFormationがオリジナルテンプレートと比較して適宜にスタックリソースを更新する

Delete Stack Workflow

When you delete a stack, you specify the stack to delete, and AWS CloudFormation deletes the stack and all the resources in that stack. You can delete stacks by using the AWS CloudFormation console, API, or AWS CLI.

If you want to delete a stack but want to retain some resources in that stack, you can use a deletion policy to retain those resources.

After all the resources have been deleted, AWS CloudFormation signals that your stack has been successfully deleted. If AWS CloudFormation cannot delete a resource, the stack will not be deleted. Any resources that haven't been deleted will remain until you can successfully delete the stack.

スタック削除の流れ

スタックを削除した時、どのスタックを削除するか特定すればAWS CloudFormationはスタックとスタック内の全てのリソースを削除します。AWS CloudFormationコンソール、APIまたはAWS CLIを使って削除もできます。

Additional Resources

For more information about creating AWS CloudFormation templates, see Template Anatomy.

For more information about creating, updating, or deleting stacks, see Working with Stacks.

追加リソース

AWS CloudFormationテンプレートを作成の詳細は[ここ](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html)

スタックの作成、更新または削除にかんする詳細は[ここ](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacks.html)

## <a name="2">はじめに</a>

### Signing Up for an AWS Account

### AWSアカウントを登録

### Get Started

Step 1: Sign up for the Service

#### Step 1: サインイン

[AWSコンソール](http://aws.amazon.com/cloudformation)

Step 2: Pick a template

#### Step 2: テンプレートを選択

 https://s3.amazonaws.com/cloudformation-templates-us-east-1/WordPress_Single_Instance_With_RDS.template.

![002](https://farm3.staticflickr.com/2941/15373625736_1af0f9306e.jpg)

![001](https://farm3.staticflickr.com/2949/15396323962_d90b809b5c.jpg)

![003](https://farm3.staticflickr.com/2945/15373625656_5f1084596b.jpg)

Step 3: Make sure you have prepared any required items for the stack

#### Step 3: スタックに必要なアイテムが準備出来たか確認する

![004](https://farm4.staticflickr.com/3919/15373625766_dbe2c44da9.jpg)

Step 4: Create the stack

#### Step 4: スタックを作る

![008](https://farm4.staticflickr.com/3914/15210147087_aa3bda6826.jpg)

Step 5: Monitor the progress of stack creation

#### Step 5: スタック作成の進捗をモニターする

![009](https://farm4.staticflickr.com/3919/15393475391_ec050c0370.jpg)

![007](https://farm3.staticflickr.com/2942/15210146897_09c19b7db6.jpg)

作成が完了したらWebWebsiteURLのリンク先をクリックしてWordPressのインストールを実行する。

### Learn Template Basics

### テンプレート基本

#### AWS CloudFormationテンプレートとは

JSON形式のテキストファイル。

#### Resources

Resourcesオブジェクトは複数のResourceオブジェクトで構成されています。Resourceオブジェクトは_Type_アトリビュートを持たなければならない。_Type_アトリビュートのフォーマットは`AWS::ProductIdentifier::ResourceType`


```json
{
    "Resources" : {
        "HelloBucket" : {
            "Type" : "AWS::S3::Bucket"
        }
    }
}
```

#### Resourcesを一緒に使ったResourceプロパティ

```json
{
    "Resources" : {
        "HelloBucket" : {
            "Type" : "AWS::S3::Bucket",
            "Properties" : {
               "AccessControl" : "PublicRead"
            }
        }
    }
}
```

複数プロパティ

```json
{
    "Resources" : {
        "HelloBucket" : {
            "Type" : "AWS::S3::Bucket",
            "Properties" : {
               "AccessControl" : "PublicRead",
               "WebsiteConfiguration" : {
                    "IndexDocument" : "index.html",
                    "ErrorDocument" : "error.html"
               }
            }
        }
    }
}
```

[Ref関数](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html)を使った場合

```json
{
  "Resources" : {
    "Ec2Instance" : {
      "Type" : "AWS::EC2::Instance",
      "Properties" : {
        "SecurityGroups" : [ { "Ref" : "InstanceSecurityGroup" } ],
        "KeyName" : "mykey",
        "ImageId" : ""
      }
    },

    "InstanceSecurityGroup" : {
      "Type" : "AWS::EC2::SecurityGroup",
      "Properties" : {
        "GroupDescription" : "Enable SSH access via port 22",
        "SecurityGroupIngress" : [ {
          "IpProtocol" : "tcp",
          "FromPort" : "22",
          "ToPort" : "22",
          "CidrIp" : "0.0.0.0/0"
        } ]
      }
    }
  }
}
```

テンプレートで宣言されていないセキュリティグループを使う

```json
{
  "Resources" : {
    "Ec2Instance" : {
      "Type" : "AWS::EC2::Instance",
      "Properties" : {
        "SecurityGroups" : [ { "Ref" : "InstanceSecurityGroup" }, "MyExistingSecurityGroup" ],
        "KeyName" : "mykey",
        "ImageId" : "ami-7a11e213"
      }
    },

    "InstanceSecurityGroup" : {
      "Type" : "AWS::EC2::SecurityGroup",
      "Properties" : {
        "GroupDescription" : "Enable SSH access via port 22",
        "SecurityGroupIngress" : [ {
          "IpProtocol" : "tcp",
          "FromPort" : "22",
          "ToPort" : "22",
          "CidrIp" : "0.0.0.0/0"
        } ]
      }
    }
  }
}
```

キーペアを入力パラメータにする

```json
{
  "Parameters" : {
    "KeyName" : {
      "Description" : "The EC2 Key Pair to allow SSH access to the instance",
      "Type" : "String"
    }
  },
  "Resources" : {
    "Ec2Instance" : {
      "Type" : "AWS::EC2::Instance",
      "Properties" : {
        "SecurityGroups" : [ { "Ref" : "InstanceSecurityGroup" }, "MyExistingSecurityGroup" ],
        "KeyName" : { "Ref" : "KeyName"},
        "ImageId" : "ami-7a11e213"
      }
    },

    "InstanceSecurityGroup" : {
      "Type" : "AWS::EC2::SecurityGroup",
      "Properties" : {
        "GroupDescription" : "Enable SSH access via port 22",
        "SecurityGroupIngress" : [ {
          "IpProtocol" : "tcp",
          "FromPort" : "22",
          "ToPort" : "22",
          "CidrIp" : "0.0.0.0/0"
        } ]
      }
    }
  }
}
```

[GetAtt関数](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html)を使う

```json
{
    "Resources" : {
        "myBucket" : {
            "Type" : "AWS::S3::Bucket"
        },
        "myDistribution" : {
           "Type" : "AWS::CloudFront::Distribution",
           "Properties" : {
              "DistributionConfig" : {
                   "S3Origin" : {
                       "DNSName": {"Fn::GetAtt" : ["myBucket", "DomainName"]}
                   }
               }
            }
        }
    }
}
```

#### インプットパラメータを使ったユーザーからの入力受け取り

```json
  "Parameters": {
    "KeyName": {
      "Description" : "Name of an existing EC2 KeyPair to enable SSH access into the WordPress web server",
      "Type": "String"
    },
    "WordPressUser": {
      "Default": "admin",
      "NoEcho": "true",
      "Description" : "The WordPress database admin account user name",
      "Type": "String",
      "MinLength": "1",
      "MaxLength": "16",
      "AllowedPattern" : "[a-zA-Z][a-zA-Z0-9]*"
    },
    "WebServerPort": {
      "Default": "8888",
      "Description" : "TCP/IP port for the WordPress web server",
      "Type": "Number",
      "MinValue": "1",
      "MaxValue": "65535"
    }
  },
```

#### Mapping使った特定条件に該当する値の取得

```json
{
  "Parameters" : {
    "KeyName" : {
      "Description" : "Name of an existing EC2 KeyPair to enable SSH access to the instance",
      "Type" : "String"
    }
  },

  "Mappings" : {
    "RegionMap" : {
      "us-east-1" : {
          "AMI" : "ami-76f0061f"
      },
      "us-west-1" : {
          "AMI" : "ami-655a0a20"
      },
      "eu-west-1" : {
          "AMI" : "ami-7fd4e10b"
      },
      "ap-southeast-1" : {
          "AMI" : "ami-72621c20"
      },
      "ap-northeast-1" : {
          "AMI" : "ami-8e08a38f"
      }
    }
  },

  "Resources" : {
    "Ec2Instance" : {
      "Type" : "AWS::EC2::Instance",
      "Properties" : {
        "KeyName" : { "Ref" : "KeyName" },
        "ImageId" : { "Fn::FindInMap" : [ "RegionMap", { "Ref" : "AWS::Region" }, "AMI" ]},
        "UserData" : { "Fn::Base64" : "80" }
      }
    }
  }
}
```

#### 値構築と出力値


```json
  "Resources" : {
    "ElasticLoadBalancer" : {
      "Type" : "AWS::ElasticLoadBalancing::LoadBalancer",
      "Properties" : {
        "AvailabilityZones" : { "Fn::GetAZs" : "" },
        "Instances" : [ { "Ref" : "Ec2Instance1" },{ "Ref" : "Ec2Instance2" } ],
        "Listeners" : [ {
          "LoadBalancerPort" : "80",
          "InstancePort" : { "Ref" : "WebServerPort" },
          "Protocol" : "HTTP"
        } ],
        "HealthCheck" : {
          "Target" : { "Fn::Join" : [ "", ["HTTP:", { "Ref" : "WebServerPort" }, "/"]]},
          "HealthyThreshold" : "3",
          "UnhealthyThreshold" : "5",
          "Interval" : "30",
          "Timeout" : "5"
        }
      }
    },
```

Targetプロパティの出力

```
HTTP:8888/
```

AWSコンソールCloudFormationのOutputsタグに表示される値

```json
  "Outputs": {
    "InstallURL": {
      "Value": {
        "Fn::Join": [
          "",
          [
            "http://",
            {
              "Fn::GetAtt": [
                "ElasticLoadBalancer",
                "DNSName"
              ]
            },
            "/wp-admin/install.php"
          ]
        ]
      },
      "Description" : "Installation URL of the WordPress website"
    },
    "WebsiteURL": {
      "Value": {
        "Fn::Join": [
          "",
          [
            "http://",
            {
              "Fn::GetAtt": [
                "ElasticLoadBalancer",
                "DNSName" ]
            }
          ]
        ]
      }
    }
  }
```

出力値

```
http://mywptests-elasticl-1gb51l6sl8y5v-206169572.us-east-1.elb.amazonaws.com/wp-admin/install.php
```


### Walkthrough: Updating a Stack

### Walkthrough: Custom Resources

### Using CloudFormer to Create Templates

### AWS CloudFormation Endpoints

## <a name="3">IAMによるアクセスコントロール</a>

# 参照

+ [AWS CloudFormation](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
