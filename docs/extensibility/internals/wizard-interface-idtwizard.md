---
title: Interface do assistente (IDTWizard) | Microsoft Docs
description: O IDE usa a interface IDTWizard para se comunicar com assistentes. Os assistentes devem implementar essa interface para serem instalados no IDE.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDTWizard interface
- wizards, interface
ms.assetid: 09618d9d-d115-45b6-bccc-de328994b39c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 930996de7fa5366463ec2d60f7cf96d941f6c243
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898611"
---
# <a name="wizard-interface-idtwizard"></a>Interface do assistente (IDTWizard)
O IDE (ambiente de desenvolvimento integrado) usa a <xref:EnvDTE.IDTWizard> interface para se comunicar com assistentes. Os assistentes devem implementar essa interface para serem instalados no IDE.

 O <xref:EnvDTE.IDTWizard.Execute%2A> método é o único método associado à interface <xref:EnvDTE.IDTWizard> . Os assistentes implementam esse método e o IDE chama o método na interface . O exemplo a seguir mostra a assinatura do método .

```
/* IDTWizard Method */
STDMETHOD(Execute)(THIS_
   /* [in] */ IDispatch *Application,
   /* [in] */ long hwndOwner,
   /* [in] */ SAFEARRAY * *ContextParams,
   /* [in] */ SAFEARRAY * *CustomParams,
   /* [out] [in] */ wizardResult *RetVal
   );
```

 O mecanismo de início é semelhante para os **assistentes Novo Projeto** **e Adicionar Novo Item.** Para iniciar um dos dois, chame <xref:EnvDTE.IDTWizard> a interface definida em Dteinternal.h. A única diferença é o conjunto de contexto e parâmetros personalizados que são passados para a interface quando a interface é chamada.

 As informações a seguir descrevem a <xref:EnvDTE.IDTWizard> interface que os assistentes devem implementar para funcionar no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE. O IDE chama <xref:EnvDTE.IDTWizard.Execute%2A> o método no assistente, passando-o da seguinte forma:

- O objeto DTE

     O objeto DTE é a raiz do modelo de Automação.

- O handle para a caixa de diálogo da janela, conforme mostrado no segmento de código, `hwndOwner ([in] long)` .

     O assistente usa isso `hwndOwner` como o pai da caixa de diálogo do assistente.

- Parâmetros de contexto passados para a interface como variante para SAFEARRAY, conforme mostrado no segmento de código, `[in] SAFEARRAY (VARIANT)* ContextParams` .

     Os parâmetros de contexto contêm uma matriz de valores específicos para o tipo de assistente que está sendo iniciado e o estado atual do projeto. O IDE passa os parâmetros de contexto para o assistente. Para obter mais informações, consulte [Parâmetros de contexto](../../extensibility/internals/context-parameters.md).

- Parâmetros personalizados passados para a interface como uma variante para SAFEARRAY, conforme mostrado no segmento de código, `[in] SAFEARRAY (VARIANT)* CustomParams` .

     Parâmetros personalizados contêm uma matriz de parâmetros definidos pelo usuário. Um arquivo .vsz passa parâmetros personalizados para o IDE. Os valores são determinados pelas `Param=` instruções . Para obter mais informações, consulte [Parâmetros personalizados.](../../extensibility/internals/custom-parameters.md)

- Os valores de retorno para a interface são

    ```
    wizardResultSuccess = -1,
    wizardResultFailure = 0
    wizardResultCancel = 1
    wizardResultBackout = 2
    ```

## <a name="see-also"></a>Confira também
- [Parâmetros de contexto](../../extensibility/internals/context-parameters.md)
- [Parâmetros personalizados](../../extensibility/internals/custom-parameters.md)
- [Assistentes](../../extensibility/internals/wizards.md)
- [Arquivo do assistente (.Vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)
