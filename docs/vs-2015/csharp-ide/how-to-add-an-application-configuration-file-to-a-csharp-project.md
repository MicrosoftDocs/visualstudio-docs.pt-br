---
title: 'Como: adicionar um arquivo de configuração de aplicativo para um projeto c# | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- app.config files, adding to C# projects
ms.assetid: 9caf6bb0-c2fc-4ab6-ba69-bed3b880fbf8
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 43245704a2393b298f0f1d948d8a8829a4ef9bc4
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49204783"
---
# <a name="how-to-add-an-application-configuration-file-to-a-c-project"></a>Como adicionar um Arquivo de Configuração do Aplicativo a um projeto C#
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao adicionar um arquivo de configuração de aplicativo (arquivo app.config) a um projeto C#, você pode personalizar o modo como o Common Language Runtime localiza e carrega arquivos do assembly. Para obter mais informações sobre arquivos de configuração de aplicativo, consulte [como o tempo de execução Localiza Assemblies](http://msdn.microsoft.com/library/772ac6f4-64d2-4cfb-92fd-58096dcd6c34).  
  
> [!NOTE]
>  A Windows Store não dá suporte à <xref:System.Configuration>. Como resultado, os aplicativos da Store não contém um modelo de App. config.  
  
 Quando você compila seu projeto, o ambiente de desenvolvimento copia automaticamente o arquivo App. config, altera o nome do arquivo da cópia para corresponder ao executável e, em seguida, move a cópia para o diretório bin.  
  
### <a name="to-add-an-application-configuration-file-to-your-c-project"></a>Para adicionar um arquivo de configuração do aplicativo ao projeto C#  
  
1.  Na barra de menus, escolha **Project**, **Adicionar Novo Item**.  
  
     A caixa de diálogo **Adicionar Novo Item** é exibida.  
  
2.  Expandir **Installed**, expanda **itens do Visual c#** e, em seguida, escolha o **arquivo de configuração de aplicativo** modelo.  
  
3.  Na caixa e texto **Nome**, insira um nome e escolha o botão **Adicionar**.  
  
     Um arquivo chamado App. config é adicionado ao seu projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando configurações de aplicativo (.NET)](../ide/managing-application-settings-dotnet.md)   
 [Esquema de arquivo de configuração](http://msdn.microsoft.com/library/69003d39-dc8a-460c-a6be-e6d93e690b38)   
 [Configuração de aplicativos](http://msdn.microsoft.com/library/86bd26d3-737e-4484-9782-19b17f34cd1f)   
 [Como: configurar um aplicativo para direcionar uma versão do .NET Framework](http://msdn.microsoft.com/en-us/5247b307-89ca-417b-8dd0-e8f9bd2f4717)   
 [Usando o Ambiente de Desenvolvimento do Visual Studio para C#](../csharp-ide/using-the-visual-studio-development-environment-for-csharp.md)