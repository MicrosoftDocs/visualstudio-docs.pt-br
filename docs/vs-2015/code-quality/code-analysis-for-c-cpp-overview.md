---
title: Análise de código para visão geral do C / C++ | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- annotations, code analysis
- build integration, code analysis
- C/C++ code analysis
- IDE, code analysis
- pragma directive, code analysis
- code analysis, C/C++
- code analysis tool
- command line, code analysis
- C++, code analysis
- check-in policies, code analysis
- '#pragma directives, code analysis'
- C, code analysis
ms.assetid: 81f0c9e8-f471-4de5-aac4-99db336a8809
caps.latest.revision: 27
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: f7261b0bab423aa851b44ec725ca1c2818da9319
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51763573"
---
# <a name="code-analysis-for-cc-overview"></a>Análise de código para visão geral do C/C++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A ferramenta de análise de código C/C++ fornece informações para desenvolvedores sobre possíveis defeitos no código-fonte C/C++. Erros de codificação comuns relatados pela ferramenta incluem saturações de buffer, memória não inicializada, desreferências de ponteiro nulo e vazamentos de memória e recursos.  
  
## <a name="ide-integrated-development-environment-integration"></a>Integração de IDE (ambiente de desenvolvimento integrado)  
 Para torná-lo natural para os desenvolvedores a usar a ferramenta de análise, ele é totalmente integrado dentro de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE. Durante o processo de compilação, todos os avisos gerados para o código-fonte aparecem na lista de erros. Você pode navegar para o código-fonte que causou o aviso, e você pode exibir informações adicionais sobre a causa e possíveis soluções do problema.  
  
## <a name="pragma-support"></a>#pragma suporte  
 Os desenvolvedores podem usar o `#pragma` diretiva para tratar avisos como erros; ativar ou desativar avisos e suprimir avisos para linhas individuais de código. Para obter mais informações, consulte [como: habilitar e desabilitar análise de código para avisos específicos de C/C++](http://msdn.microsoft.com/en-us/910b8518-71f1-4b2e-b012-70647795642a).  
  
## <a name="annotation-support"></a>Suporte de anotação  
 Anotações de melhorar a precisão da análise de código. Anotações fornecem informações adicionais sobre condições pré e pós-nos parâmetros de função e tipos de retorno. Para obter mais informações, consulte [como: especificar informações de código adicionais usando analysis_assume](../code-quality/how-to-specify-additional-code-information-by-using-analysis-assume.md)  
  
## <a name="run-analysis-tool-as-part-of-check-in-policy"></a>Execute a ferramenta de análise como parte da política de check-in  
 Talvez você queira exigem que o código de origem todos os check-ins satisfaçam determinadas políticas. Em particular, convém certificar-se de que a análise foi executada como uma etapa de compilação local mais recente. Para obter mais informações sobre como habilitar uma política de check-in do análise código, consulte [criando e usando análise de código de Check-In políticas](../code-quality/creating-and-using-code-analysis-check-in-policies.md)  
  
## <a name="team-build-integration"></a>Integração do Team Build  
 Você pode usar os recursos integrados do sistema de compilação para executar a ferramenta de análise de código como uma etapa do [!INCLUDE[esprtfs](../includes/esprtfs-md.md)] processo de compilação. Para obter mais informações, consulte [Compilar o aplicativo](http://msdn.microsoft.com/library/a971b0f9-7c28-479d-a37b-8fd7e27ef692).  
  
## <a name="command-line-support"></a>Suporte de linha de comando  
 Além da integração completa dentro do ambiente de desenvolvimento, os desenvolvedores também podem usar a ferramenta de análise da linha de comando, conforme mostrado no exemplo a seguir:  
  
 `C:\>cl /analyze Sample.cpp`



