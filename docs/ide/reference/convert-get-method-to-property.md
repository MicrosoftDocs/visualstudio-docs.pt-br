---
title: Converter o método Get para propriedade e converter uma propriedade para um método Get no Visual Studio
ms.date: 01/26/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
ms.devlang: csharp
author: gewarren
ms.author: gewarren
manager: douge
f1_keywords:
- vs.csharp.refactoring.convertmethodtoproperty
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 35836e18e9cf8ffa33056b6bd93959d8debcc43a
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896011"
---
# <a name="convert-get-method-to-property--convert-property-to-get-method-refactorings"></a>Refatorações para converter o método Get em propriedade/converter uma propriedade no método Get

Essas refatorações aplicam-se a:

- C#

## <a name="convert-get-method-to-property"></a>Converter o método Get em propriedade

**O quê:** permite converter um método Get em uma propriedade (e opcionalmente seu método Set).

**Quando:** você tem um método Get que não contêm nenhuma lógica.

### <a name="how-to"></a>Como fazer

1. coloque o cursor no nome do seu método Get.

1. Depois, siga um destes procedimentos:

   - **Teclado**
      - Pressione **Ctrl**+**.** para disparar o menu **Ações Rápidas e Refatorações** e selecionar **Substituir método por propriedade** no pop-up da janela Visualização.
   - **Mouse**
      - Clique com o botão direito do mouse no código, selecione o menu **Ações Rápidas e Refatorações** e selecione **Substituir método por propriedade** no pop-up da janela Visualização.

1. (Opcional) Se houver um método Set, você também poderá convertê-lo neste momento selecionando **Substituir método Get e método Set por propriedade**.

1. Se você estiver satisfeito com a alteração na visualização do código, pressione **Enter** ou clique na correção no menu e as alterações serão confirmadas.

Exemplo:

```csharp
private int MyValue;

// Before
public int GetMyValue()
{
    return MyValue;
}

// Replace 'GetMyValue' with property

// After
public int MyValue
{
    get { return MyValue; }
}
```

## <a name="convert-property-to-get-method"></a>Converter propriedade em método Get

**O quê:** permite converter uma propriedade em um método Get

**Quando:** você tem uma propriedade que envolve mais do que imediatamente configurar e obter um valor

### <a name="how-to"></a>Como fazer

1. coloque o cursor no nome do seu método Get.

1. Depois, siga um destes procedimentos:

   - **Teclado**
      - Pressione **Ctrl**+**.** para disparar o menu **Ações Rápidas e Refatorações** e selecionar **Substituir propriedade por métodos** no pop-up da janela Visualização.
   - **Mouse**
      - Clique com o botão direito do mouse no código, selecione o menu **Ações Rápidas e Refatorações** e selecione **Substituir propriedade por métodos** no pop-up da janela Visualização.

1. Se você estiver satisfeito com a alteração na visualização do código, pressione **Enter** ou clique na correção no menu e as alterações serão confirmadas.

## <a name="see-also"></a>Consulte também

- [Refatoração](../refactoring-in-visual-studio.md)
- [Visualizar alterações](../../ide/preview-changes.md)