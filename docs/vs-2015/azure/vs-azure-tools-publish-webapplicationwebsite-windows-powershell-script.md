---
title: Publish-WebApplicationWebSite (script do Windows PowerShell) | Microsoft Docs
description: Saiba como publicar um projeto da web em um site do Azure. Esse script cria os recursos necessários em sua assinatura do Azure se não existirem.
author: ghogen
manager: douge
assetId: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/11/2016
ms.author: ghogen
ms.openlocfilehash: 175181d5d866e9d7fab51eaf7c3262e47d0ed6a8
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001303"
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Publish-WebApplicationWebSite (script do Windows PowerShell)
## <a name="syntax"></a>Sintaxe
Publica um projeto da web em um site do Azure. Se não existirem, o script cria os recursos necessários em sua assinatura do Azure.

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>Configuração
O caminho para o arquivo de configuração JSON que descreve os detalhes da implantação.

| Parâmetro | Valor padrão |
| --- | --- |
| Aliases |nenhum |
| Necessário? |true |
| Posição |nomeados |
| Valor padrão |nenhum |
| Aceitar entrada de pipeline? |false |
| Aceitar caracteres curinga? |false |

## <a name="subscriptionname"></a>SubscriptionName
O nome da assinatura do Azure que você deseja criar o site.

| Parâmetro | Valor padrão |
| --- | --- |
| Aliases |nenhum |
| Necessário? |false |
| Posição |nomeados |
| Valor padrão |nenhum |
| Aceitar entrada de pipeline? |false |
| Aceitar caracteres curinga? |false |

## <a name="webdeploypackage"></a>WebDeployPackage
O caminho para o pacote de implantação da web para publicar o site. Você pode criar este pacote usando o Assistente de publicação na Web no Visual Studio. Para obter mais informações, consulte [Introdução aos serviços de nuvem do Azure e ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).

| Parâmetro | Valor padrão |
| --- | --- |
| Aliases |nenhum |
| Necessário? |false |
| Posição |nomeados |
| Valor padrão |nenhum |
| Aceitar entrada de pipeline? |false |
| Aceitar caracteres curinga? |false |

## <a name="databaseserverpassword"></a>DatabaseServerPassword
O nome de usuário e senha para o banco de dados SQL no Azure.

| Parâmetro | Valor padrão |
| --- | --- |
| Aliases |nenhum |
| Necessário? |false |
| Posição |nomeados |
| Valor padrão |nenhum |
| Aceitar entrada de pipeline? |false |
| Aceitar caracteres curinga? |false |

## <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Se for true, imprimir mensagens do script no fluxo de saída.

| Parâmetro | Valor padrão |
| --- | --- |
| Aliases |nenhum |
| Necessário? |false |
| Posição |nomeados |
| Valor padrão |false |
| Aceitar entrada de pipeline? |false |
| Aceitar caracteres curinga? |false |

## <a name="remarks"></a>Comentários
Para obter uma explicação completa de como usar o script para criar ambientes de desenvolvimento e teste, consulte [usando Scripts do Windows PowerShell para publicar para ambientes de desenvolvimento e teste](vs-azure-tools-publishing-using-powershell-scripts.md).

O arquivo de configuração JSON Especifica os detalhes do que está para ser implantado. Ele inclui as informações que você especificou quando criou o projeto, como o nome e o nome de usuário para o site. Ele também inclui o banco de dados para provisionar, se houver. O código a seguir mostra um exemplo de um arquivo de configuração JSON:

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

Você pode editar o arquivo de configuração JSON para alterar o que é implantado. Uma seção do site é necessária, mas a seção de banco de dados é opcional.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte [Publish-WebApplicationVM (script do Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)

