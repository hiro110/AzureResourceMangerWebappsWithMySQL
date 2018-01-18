

# What's this?
WebApps(on Windows) AzureDatabase for MySQLテンプレート
* App Service PlanはStandard
* インスタンスタイプは S1(1GB CPU, 1.75GB MEM, 50GB Storage)
* アラート設定は以下の通り
    * HTTP 401 エラー
    * HTTP 404 エラー
    * 内部 エラー(5xx, 6xx)
    * 平均メモリ使用量　（閾値80%）
    * 平均応答時間

* Azure Database for MySQL
    * パスワードは英数字、記号を含めた8桁以上にすること
    * SKUはBasic 50DTU

# How to Deploy
* parameters.jsonを適宜更新
* デプロイ手順（Azure CLI）

```:Bash
# Azure ログイン
$ az login

To sign in, use a web browser to open the page https://aka.ms/devicelogin and enter the code xxxxx to authenticate.

https://aka.ms/devicelogin へアクセスし、xxxxxを入力し、認証する。

# Azure サブスクリプション　確認
$ az account list --output table

#  Azure サブスクリプション アクティベート（切替）
$ az account set --subscription "<SubscrioptionName>"

# Azure リソース　確認
$ az resource list --output table

# リソースグループ作成
$ az group create -n <resourceGroupName> -l "japaneast"
※既存のリソースグループにデプロイする場合は、不要

# デプロイテスト  
$ az group deployment validate --resource-group <resourceGroupName> --template-file deploy.json --parameters parameters.json
※必須ではないが、自信がない時はやってみること

# デプロイ  
$ az group deployment create --resource-group <resourceGroupName> --template-file deploy.json --parameters parameters.json

```


* デプロイ手順（PowerShell）

```
# Azure ログイン
> Login-AzureRmAccount

To sign in, use a web browser to open the page https://aka.ms/devicelogin and enter the code xxxxx to authenticate.

https://aka.ms/devicelogin へアクセスし、xxxxxを入力し、認証する。

# Azure サブスクリプション　確認
> Get-AzureRmSubscription

#  Azure サブスクリプション アクティベート（切替）
> Set-AzureRmContext -SubscriptionName "<SubscrioptionName>"

# Azure リソース　確認
> Get-AzureRmResourceGroup

# リソースグループ作成
> New-AzureRmResourceGroup -Name <resourceGroupName> -Location "japaneast"
※既存のリソースグループにデプロイする場合は、不要

# デプロイテスト  
> Test-AzureRmResourceGroupDeployment -ResourceGroupName <resourceGroupName> -TemplateFile deploy.json -TemplateParameterFile parameters.json
※必須ではないが、自信がない時はやってみること

# デプロイ  
> New-AzureRmResourceGroupDeployment -ResourceGroupName <resourceGroupName> -TemplateFile deploy.json -TemplateParameterFile parameters.json
```



* FYI  
[初めての Azure Resource Manager テンプレートを作成およびデプロイする](https://docs.microsoft.com/ja-jp/azure/azure-resource-manager/resource-manager-create-first-template)  
[Azure Resource Manager テンプレートの構造と構文の詳細](https://docs.microsoft.com/ja-jp/azure/azure-resource-manager/resource-group-authoring-templates)  
[az group deployment](https://docs.microsoft.com/en-us/cli/azure/group/deployment?view=azure-cli-latest#az_group_deployment_create)
[Define resources in Azure Resource Manager templates](https://docs.microsoft.com/ja-jp/azure/templates/)