---
title: Análise de código para visão geral do código gerenciado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.projectpropertypages.codeanalysis
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
ms.assetid: 12ec0dab-46a4-43d8-984a-440730ef37a9
caps.latest.revision: 37
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: b2d84ba17fb3fd866dcd73cd2821289c40153b6d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49872662"
---
# <a name="code-analysis-for-managed-code-overview"></a>Visão geral da análise de código para código gerenciado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Análise de código para código gerenciado analisa os assemblies gerenciados e relata informações sobre assemblies, como violações de programação e regras de design estabelecidas nas diretrizes de Design do Microsoft .NET Framework.  
  
 A ferramenta de análise representa as verificações que executa durante uma análise como mensagens de aviso. Mensagens de aviso identificam quaisquer problemas de programação e design relevantes e, quando é possíveis, forneça informações sobre como corrigir o problema.  
  
## <a name="ide-integrated-development-environment-integration"></a>Integração de IDE (ambiente de desenvolvimento integrado)  
 Como desenvolvedor, você pode executar a análise de código em seu projeto automaticamente ou você pode executá-lo manualmente.  
  
 Para executar a análise de código sempre que você compila um projeto, você seleciona **habilitar análise de código na compilação (define a constante CODE_ANALYSIS)** na página de propriedades do projeto. Para obter mais informações, consulte [como: habilitar e desabilitar análise de código automática](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md).  
  
 Para executar análise de código manualmente em um projeto na **Analyze** menu, clique em **executar análise de código na**_ProjectName_. Para obter mais informações, consulte [como: habilitar e desabilitar análise de código automática](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md).  
  
## <a name="rule-sets"></a>Conjuntos de regras  
 Regras de análise de código para código gerenciado são agrupadas em *conjuntos de regra*. Você pode usar um dos conjuntos de regra padrão Microsoft, ou você pode criar uma regra personalizada definida para atender a uma necessidade específica. Para obter mais informações, consulte [usando os conjuntos de regras para agrupar regras de análise de código](../code-quality/using-rule-sets-to-group-code-analysis-rules.md).  
  
## <a name="in-source-suppression"></a>Exclusão de origem  
 Com frequência, é útil indicar que um aviso é não aplicáveis. Isso informa o desenvolvedor e outras pessoas que podem examinar o código mais tarde, que um aviso foi investigado e então suprimido ou ignorado.  
  
 Exclusão de origem dos avisos é implementada por meio de atributos personalizados. Para suprimir um aviso, adicione o atributo `SuppressMessage` no código-fonte, conforme mostrado no exemplo a seguir:  
  
 `[System.Diagnosis.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`  
  
 `Public class MyClass`  
  
 `{`  
  
 `// code`  
  
 `}`  
  
 Para obter mais informações, consulte [suprimir avisos usando o atributo SuppressMessage](../code-quality/suppress-warnings-by-using-the-suppressmessage-attribute.md).  
  
## <a name="run-code-analysis-as-part-of-check-in-policy"></a>Executar análise de código como parte da política de check-in  
 Como uma organização, você talvez queira exigem que todos os check-ins satisfaçam determinadas políticas. Em particular, você deseja certificar-se de que você siga essas políticas:  
  
- Não havia nenhum erro de compilação no check-in do código.  
  
- Análise de código foi executada como parte da compilação mais recente.  
  
  Você pode fazer isso com a especificação de políticas de check-in. Para obter mais informações, consulte [aprimorando a qualidade do código com políticas de Check-in do projeto de equipe](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md).  
  
## <a name="team-build-integration"></a>Integração do Team Build  
 Você pode usar os recursos integrados do sistema de compilação para executar a ferramenta de análise como parte do processo de compilação. Para obter mais informações, consulte [Compilar o aplicativo](http://msdn.microsoft.com/library/a971b0f9-7c28-479d-a37b-8fd7e27ef692).  
  
## <a name="see-also"></a>Consulte também  
 [Usando conjuntos de regras para agrupar regras de análise de código](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)   
 [Como habilitar e desabilitar a análise de código automática](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)



