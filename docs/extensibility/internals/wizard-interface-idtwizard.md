---
title: Interface do assistente (IDTWizard) | Microsoft Docs
description: O IDE usa a interface IDTWizard para se comunicar com os assistentes. Os assistentes devem implementar essa interface para ser instalada no IDE.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDTWizard interface
- wizards, interface
ms.assetid: 09618d9d-d115-45b6-bccc-de328994b39c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b8dc88341bc72755ae0f5011d18182c5b78bb483
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074191"
---
# <a name="wizard-interface-idtwizard"></a>Interface do assistente (IDTWizard)
O IDE (ambiente de desenvolvimento integrado) usa a <xref:EnvDTE.IDTWizard> interface para se comunicar com os assistentes. Os assistentes devem implementar essa interface para serem instalados no IDE.

 O <xref:EnvDTE.IDTWizard.Execute%2A> método é o único método associado à <xref:EnvDTE.IDTWizard> interface. Os assistentes implementam esse método e o IDE chama o método na interface. O exemplo a seguir mostra a assinatura do método.

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

 O mecanismo de início é semelhante para os assistentes **novo projeto** e **Adicionar novo item** . Para iniciar o, você chama a <xref:EnvDTE.IDTWizard> interface definida em Dteinternal. h. A única diferença é o conjunto de contexto e parâmetros personalizados que são passados para a interface quando a interface é chamada.

 As informações a seguir descrevem a <xref:EnvDTE.IDTWizard> interface que os assistentes devem implementar para funcionar no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE. O IDE chama o <xref:EnvDTE.IDTWizard.Execute%2A> método no assistente, passando o seguinte:

- O objeto DTE

     O objeto DTE é a raiz do modelo de automação.

- O identificador para a caixa de diálogo de janela, conforme mostrado no segmento de código, `hwndOwner ([in] long)` .

     O assistente usa isso `hwndOwner` como o pai da caixa de diálogo do assistente.

- Parâmetros de contexto passados para a interface como Variant para SAFEARRAY, conforme mostrado no segmento de código, `[in] SAFEARRAY (VARIANT)* ContextParams` .

     Os parâmetros de contexto contêm uma matriz de valores que são específicos do tipo de assistente que está sendo iniciado e do estado atual do projeto. O IDE passa os parâmetros de contexto para o assistente. Para obter mais informações, consulte [parâmetros de contexto](../../extensibility/internals/context-parameters.md).

- Parâmetros personalizados passados para a interface como uma variante para SAFEARRAY, conforme mostrado no segmento de código, `[in] SAFEARRAY (VARIANT)* CustomParams` .

     Parâmetros personalizados contêm uma matriz de parâmetros definidos pelo usuário. Um arquivo. vsz passa parâmetros personalizados para o IDE. Os valores são determinados pelas `Param=` instruções. Para obter mais informações, consulte [Custom Parameters](../../extensibility/internals/custom-parameters.md).

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
