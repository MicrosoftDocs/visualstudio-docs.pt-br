---
title: Parâmetros personalizados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- wizards, custom parameters
- custom parameters
ms.assetid: ba5c364b-66e6-47ea-9760-a0b70de8f0a0
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8bb8a1861d6162e73906d74250f738ff96b9a505
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51757904"
---
# <a name="custom-parameters"></a>Parâmetros personalizados
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Parâmetros personalizados controlam a operação de um assistente depois de um assistente foi iniciado. Um arquivo. vsz relacionados fornece uma matriz de parâmetros definidos pelo usuário que são empacotados pelo ambiente de desenvolvimento integrado (IDE) e passado para o assistente como uma matriz de cadeias de caracteres quando o assistente for iniciado. Em seguida, o assistente analisa a matriz de cadeias de caracteres e usa as informações para controlar a operação real do assistente. Dessa forma, um assistente pode personalizar a funcionalidade dependendo do conteúdo do arquivo. vsz.  
  
 Parâmetros de contexto, por outro lado, definem o estado do projeto quando o assistente for iniciado. Para obter mais informações, consulte [parâmetros de contexto](../../extensibility/internals/context-parameters.md).  
  
 A seguir está um exemplo de um arquivo. vsz que tem parâmetros personalizados:  
  
```  
VSWIZARD 8.0  
Wizard=VsWizard.VsWizard_Engine  
Param="WIZARD_NAME = Sample Wizard"  
Param="WIZARD_UI = FALSE"  
Param="RELATIVE_PATH = VSWizards\Classwiz\ATL"  
Param="PREPROCESS_FUNCTION = CanAddATLSupport"  
Param="PROJECT_TYPE = CSPROJ"  
```  
  
 O autor do arquivo. vsz adiciona os valores dos parâmetros. Quando um usuário escolhe **novo projeto** ou **Adicionar Novo Item** no menu arquivo ou clicando em um projeto no **Gerenciador de soluções**, o IDE coleta esses valores em uma matriz de cadeias de caracteres. O IDE, em seguida, chama o projeto <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A> método com o <xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION> sinalizador conjunto e as chamadas de projeto a <xref:EnvDTE.IVsExtensibility.RunWizardFile%2A> método que é responsável por executar o assistente e retornar o resultado.  
  
 O assistente é responsável por analisar a matriz de cadeias de caracteres e agir sobre as cadeias de caracteres corretamente. Dessa forma, com a implementação de parâmetros personalizados, você pode criar um assistente que executa uma variedade de funções. Em outras palavras, um assistente poderia ter três arquivos. vsz diferentes. Cada arquivo passa a diferentes conjuntos de parâmetros personalizados para controlar o comportamento do assistente em várias situações.  
  
 Para obter mais informações, consulte [Assistente (. Arquivo vsz)](../../extensibility/internals/wizard-dot-vsz-file.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>   
 [Parâmetros de contexto](../../extensibility/internals/context-parameters.md)   
 [Assistentes](../../extensibility/internals/wizards.md)   
 [Arquivo do assistente (.Vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)

