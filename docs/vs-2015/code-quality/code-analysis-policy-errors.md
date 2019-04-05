---
title: Erros de política de análise de código | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.policyfailures
helpviewer_keywords:
- policy errors, code analysis
ms.assetid: d1f221cd-68c0-4277-9397-b76ad0dbae77
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 9b61d7d9718e9557ef153474718542f889ad7629
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58925715"
---
# <a name="code-analysis-policy-errors"></a>Erros da política de análise do código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os seguintes erros ocorrem se a política de análise de código não for atendida no check-in:  
  
 **As configurações de análise de código para um ou mais projetos não são compatíveis com a política de análise de código.**  
  
 Os requisitos de análise de código fazer check-in para o controle de fonte do projeto de equipe não foi atendida para um ou mais projetos de código. Esse erro pode ser causado por uma ou mais das seguintes condições:  
  
1. Análise de código não está habilitada na compilação para todos os projetos na solução.  
  
2. A regra local definida para o projeto no Visual Studio tem menos restritivo **ação** configuração do que a regra de projeto de equipe, por exemplo, definir uma regra que é definida como **ação**=**erro**  no servidor tem sua **ação** definido como **aviso** ou **nenhum** na regra definida que está sendo executado no Visual Studio).  
  
3. A regra no conjunto especificada no Visual Studio não contém todas as regras que são especificadas na regra de conjunto especificada na análise de código check-in política de projeto de equipe.  
  
   **A política de análise de código falha. Há erros no projeto {0} ou a compilação não está atualizada.**  
  
   O build contiver erros ou os erros foram corrigidos, mas a análise de código não foi executada após a correção.  
  
   **Falha de check-in. A política de análise de código requer que você verifique meio do Visual Studio com uma solução aberta.**  
  
   A política de análise de código requer que todos os arquivos em check-in devem ser na solução atualmente aberta. Para corrigir esse erro, abra a solução que contém o arquivo de check-in.  
  
   **Nem todos os arquivos em check-in pendente estão dentro da solução aberta no momento.**  
  
   A política de análise de código requer que todos os arquivos em check-in devem ser na solução atualmente aberta. Esse erro é gerado quando há uma solução aberta, mas alguns arquivos na exibição de "verificação pendente em" não fazem parte da solução atualmente aberta. Para corrigir esse erro, abra a solução que contém o arquivo de check-in.  
  
   **A versão do '{0}' não está correto. É o nome forte especificado na política '{1}'.**  
  
   Esse erro se aplica a projetos do .NET. Um arquivo de regra. dll exigido pela política de análise de código existe no computador local, mas a chave pública/versão não coincide. Para corrigir esse erro, os criadores de diretiva devem atualizar os. DLLs no *C:\Program Files\Microsoft Visual Studio 8\Team Tools\Static análise Tools\FxCop\Rules\\*  diretório em seu computador.  
  
   **'{0}' especificado na diretiva de assembly não existe.**  
  
   Esse erro se aplica a projetos do .NET. Uma regra exigida pela política de análise de código não tem a dll correspondente instalada no computador cliente. Para corrigir esse erro, os criadores de diretiva devem atualizar a dll no *C:\Program Files\Microsoft Visual Studio 8\Team Tools\Static análise Tools\FxCop\Rules\\*  diretório em seu computador.  
  
   **Projeto {0} configurações de regra não estão em conformidade com a política de análise de código.**  
  
   Esse erro se aplica a projetos do .NET. As configurações de regras de código gerenciado não são tão estritas quanto a política exige. Para corrigir esse erro, a configuração do cliente deve ser o mesmo ou mais rígidas do que o requisito de política no servidor.  
  
   **Análise de código não está habilitada na configuração ativa. Alterne para a configuração {0} e compile o projeto {1} antes de fazer check-in.**  
  
   No [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], a configuração do Active Directory não tem code analysis habilitado, mas há pelo menos um code analysis habilitado.  
  
   **Você deve habilitar a análise de código para binários gerenciados no projeto {0} propriedades e compilação antes de fazer check-in.**  
  
   Esse erro se aplica a [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] aplicativos .NET. A política exige a análise de código gerenciado a ser executada, mas ele não está habilitado no projeto atual no cliente.  
  
   **Você deve habilitar a análise de código no projeto {0} propriedades e compilação antes de fazer check-in.**  
  
   Esse erro aplicado a [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projetos e projetos Web. A política exige a análise de código gerenciado a ser executada, mas ele não está habilitado no projeto atual no cliente.  
  
   **Você deve habilitar a análise de código C/C++ em projeto {0} propriedades e compilação antes de fazer check-in.**  
  
   Esse erro se aplicam a projetos não gerenciados. A política de análise de código requer a análise de código para C/C++, mas ele não está habilitado no projeto atual no cliente.  
  
## <a name="see-also"></a>Consulte também  
 [Erros de aplicativo de análise de código](../code-quality/code-analysis-application-errors.md)
