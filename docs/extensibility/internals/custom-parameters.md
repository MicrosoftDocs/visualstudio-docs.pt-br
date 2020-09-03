---
title: Parâmetros personalizados | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- wizards, custom parameters
- custom parameters
ms.assetid: ba5c364b-66e6-47ea-9760-a0b70de8f0a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cd52a49daa7d57a21d8cb0896f7108efa09e32b2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708943"
---
# <a name="custom-parameters"></a>Parâmetros personalizados
Parâmetros personalizados controlam a operação de um assistente após o início de um assistente. Um arquivo *. vsz* relacionado fornece uma matriz de parâmetros definidos pelo usuário que são empacotados pelo IDE (ambiente de desenvolvimento integrado) e passados para o assistente como uma matriz de cadeias de caracteres quando o assistente é iniciado. Em seguida, o assistente analisa a matriz de cadeias de caracteres e usa as informações para controlar a operação real do assistente. Dessa maneira, um assistente pode personalizar a funcionalidade dependendo do conteúdo do arquivo *. vsz* .

 Os parâmetros de contexto, por outro lado, definem o estado do projeto quando o assistente é iniciado. Para obter mais informações, consulte [parâmetros de contexto](../../extensibility/internals/context-parameters.md).

 Veja a seguir um exemplo de um arquivo *. vsz* que tem parâmetros personalizados:

```
VSWIZARD 8.0
Wizard=VsWizard.VsWizard_Engine
Param="WIZARD_NAME = Sample Wizard"
Param="WIZARD_UI = FALSE"
Param="RELATIVE_PATH = VSWizards\Classwiz\ATL"
Param="PREPROCESS_FUNCTION = CanAddATLSupport"
Param="PROJECT_TYPE = CSPROJ"
```

 O autor do arquivo *. vsz* adiciona os valores dos parâmetros. Quando um usuário seleciona **novo projeto** ou **adiciona novo item** no menu **arquivo** ou clicando com o botão direito do mouse em um projeto no **Gerenciador de soluções**, o IDE coleta esses valores em uma matriz de cadeias de caracteres. Em seguida, o IDE chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A> método do projeto com o <xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION> sinalizador definido, e o projeto chama o <xref:EnvDTE.IVsExtensibility.RunWizardFile%2A> método que é responsável por executar o assistente e retornar o resultado.

 O assistente é responsável por analisar a matriz de cadeias de caracteres e agir adequadamente nas cadeias de caracteres. Dessa maneira, implementando parâmetros personalizados, você pode criar um assistente que executa uma variedade de funções. Em outras palavras, um assistente pode ter três arquivos *. vsz* diferentes. Cada arquivo passa conjuntos diferentes de parâmetros personalizados para controlar o comportamento do assistente em várias situações.

 Para obter mais informações, consulte o [arquivo Wizard (. vsz)](../../extensibility/internals/wizard-dot-vsz-file.md).

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- [Parâmetros de contexto](../../extensibility/internals/context-parameters.md)
- [Assistentes](../../extensibility/internals/wizards.md)
- [Arquivo do assistente (. vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)
