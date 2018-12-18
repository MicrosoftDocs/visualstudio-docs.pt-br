---
title: Publicar WebApplicationVM | Microsoft Docs
description: Saiba como implantar um aplicativo web para uma máquina virtual. Esse script cria os recursos necessários em sua assinatura do Azure se não existirem.
author: ghogen
manager: douge
assetId: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/11/2016
ms.author: ghogen
ms.openlocfilehash: c2383e6d7b14d801a391a725f0482736fb926cd1
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001325"
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Publish-WebApplicationVM (script do Windows PowerShell)
Implanta um aplicativo web para uma máquina virtual. Se não existirem, o script cria os recursos necessários em sua assinatura do Azure.

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a>Configuração
O caminho para o arquivo de configuração JSON que descreve os detalhes da implantação.

| Aliases | nenhum |
| --- | --- |
| Necessário? |true |
| Posição |nomeados |
| Valor padrão |nenhum |
| Aceitar entrada de pipeline? |false |
| Aceitar caracteres curinga? |false |

### <a name="subscriptionname"></a>SubscriptionName
O nome da assinatura do Azure no qual você deseja criar a máquina virtual.

| Aliases | nenhum |
| --- | --- |
| Necessário? |false |
| Posição |nomeados |
| Valor padrão |Usa a primeira assinatura no arquivo de assinatura |
| Aceitar entrada de pipeline? |false |
| Aceitar caracteres curinga? |false |

### <a name="webdeploypackage"></a>WebDeployPackage
O caminho para o pacote de implantação da web para publicar para a máquina virtual. Você pode criar este pacote usando o Assistente de publicação na Web no Visual Studio. Ver [como: criar um pacote de implantação da Web no Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).

| Aliases | nenhum |
| --- | --- |
| Necessário? |false |
| Posição |nomeados |
| Valor padrão |nenhum |
| Aceitar entrada de pipeline? |false |
| Aceitar caracteres curinga? |false |

### <a name="allowuntrusted"></a>AllowUntrusted
Se verdadeiro, permita o uso de certificados que não está assinado por uma autoridade raiz confiável.

| Aliases | nenhum |
| --- | --- |
| Necessário? |false |
| Posição |nomeados |
| Valor padrão |false |
| Aceitar entrada de pipeline? |false |
| Aceitar caracteres curinga? |false |

### <a name="vmpassword"></a>VMPassword
As credenciais para a conta de máquina virtual. Exemplo: - VMPassword @{nome = "admin"; Senha = "password"}

| Aliases | nenhum |
| --- | --- |
| Necessário? |false |
| Posição |nomeados |
| Valor padrão |nenhum |
| Aceitar entrada de pipeline? |false |
| Aceitar caracteres curinga? |false |

### <a name="databaseserverpassword"></a>DatabaseServerPassword
As credenciais de banco de dados SQL do Azure. Exemplo: - DatabaseServerPassword @{nome = "admin"; Senha = "password"}

| Aliases | nenhum |
| --- | --- |
| Necessário? |false |
| Posição |nomeados |
| Valor padrão |nenhum |
| Aceitar entrada de pipeline? |false |
| Aceitar caracteres curinga? |false |

### <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Se for true, imprimir mensagens do script no fluxo de saída.

| Aliases | nenhum |
| --- | --- |
| Necessário? |false |
| Posição |nomeados |
| Valor padrão |false |
| Aceitar entrada de pipeline? |false |
| Aceitar caracteres curinga? |false |

## <a name="remarks"></a>Comentários
Para obter uma explicação completa de como usar o script para criar ambientes de desenvolvimento e teste, consulte [usando Scripts do Windows PowerShell para publicar para ambientes de desenvolvimento e teste](vs-azure-tools-publishing-using-powershell-scripts.md).

O arquivo de configuração JSON Especifica os detalhes do que está para ser implantado. Ele inclui as informações que você especificou quando criou o projeto, como o nome, o grupo de afinidade, a imagem de VHD e o tamanho da máquina virtual. Ele também inclui os pontos de extremidade na máquina virtual, os bancos de dados para provisionar, se houver e os parâmetros de implantação web. O código a seguir mostra um exemplo de um arquivo de configuração JSON:

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Você pode editar o arquivo de configuração JSON para alterar o que é provisionado. Uma máquina virtual e um serviço de nuvem são necessários, mas a seção de banco de dados é opcional.

