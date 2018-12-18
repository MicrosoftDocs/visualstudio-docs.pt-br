---
title: Como o ClickOnce executa atualizações de aplicativos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- updates, ClickOnce
- ClickOnce deployment, updates
- deploying applications [ClickOnce], application updates
ms.assetid: d54313c2-cf0c-420d-b151-99953a95f0bb
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 5c2e135a2b872ecd389149626ac09caf02734f40
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49298019"
---
# <a name="how-clickonce-performs-application-updates"></a>Como o ClickOnce executa atualizações de aplicativos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ClickOnce usa as informações de versão do arquivo especificadas no manifesto de implantação do aplicativo para decidir se deseja atualizar os arquivos do aplicativo. Depois que uma atualização começa, o ClickOnce usa uma técnica chamada *aplicação de patch de arquivo* para evitar o download redundante dos arquivos de aplicativo.  
  
## <a name="file-patching"></a>Aplicação de patch de arquivo  
 Ao atualizar um aplicativo, ClickOnce não baixa todos os arquivos para a nova versão do aplicativo, a menos que os arquivos foram alterados. Em vez disso, ele compara as assinaturas de hash dos arquivos especificados no manifesto do aplicativo para o aplicativo atual em relação as assinaturas no manifesto para a nova versão. Se as assinaturas de um arquivo forem diferentes, o ClickOnce baixa a nova versão. Se as assinaturas forem correspondentes, o arquivo não foi alterado de uma versão para a próxima. Nesse caso, o ClickOnce copia o arquivo existente e usa-o na nova versão do aplicativo. Essa abordagem impede que o ClickOnce precisar baixar todo o aplicativo novamente, mesmo que apenas um ou dois arquivos foram alterados.  
  
 Aplicação de patch de arquivo também funciona para assemblies que são baixados sob demanda usando o <xref:System.Deployment.Application.ApplicationDeployment.DownloadFileGroup%2A> e <xref:System.Deployment.Application.ApplicationDeployment.DownloadFileGroupAsync%2A> métodos.  
  
 Se você usar o Visual Studio para compilar seu aplicativo, ele irá gerar novas assinaturas de hash para todos os arquivos sempre que você recompile o projeto inteiro. Nesse caso, todos os assemblies serão baixados para o cliente, embora apenas alguns assemblies podem ter sido alterado.  
  
 Aplicação de patch de arquivo não funciona para arquivos que são marcados como dados e armazenados no diretório de dados. Eles são sempre baixados independentemente da assinatura de hash do arquivo. Para obter mais informações sobre o diretório de dados, consulte [acessando dados locais e remotos em aplicativos ClickOnce](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md).  
  
## <a name="see-also"></a>Consulte também  
 [Escolhendo uma estratégia de atualização do ClickOnce](../deployment/choosing-a-clickonce-update-strategy.md)   
 [Escolhendo uma estratégia de implantação do ClickOnce](../deployment/choosing-a-clickonce-deployment-strategy.md)



