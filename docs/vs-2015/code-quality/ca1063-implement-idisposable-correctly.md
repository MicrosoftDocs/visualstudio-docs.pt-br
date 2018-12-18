---
title: 'CA1063: Implementar IDisposable corretamente | Microsoft Docs'
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
- ImplementIDisposableCorrectly
- CA1063
helpviewer_keywords:
- CA1063
- ImplementIDisposableCorrectly
ms.assetid: 12afb1ea-3a17-4a3f-a1f0-fcdb853e2359
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 94d13514800bac80723031c6bba7920d28ac83e6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49877290"
---
# <a name="ca1063-implement-idisposable-correctly"></a>CA1063: implementar IDisposable corretamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ImplementIDisposableCorrectly|
|CheckId|CA1063|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 `IDisposable` não foi implementado corretamente. Alguns motivos para esse problema estão listados aqui:

- IDisposable é novamente implementado na classe.

- Finalizar novamente é substituído.

- Dispose é substituído.

- Dispose () não é público, sealed ou chamado Dispose.

- Dispose (bool) não é protegido, virtual ou sem lacre.

- Tipos sem lacre, Dispose () deve chamar Dispose (True).

- Para tipos sem lacre, a implementação de Finalize não chamar Dispose (bool) de um ou ambos os ou o finalizador da classe case.

  Violação de qualquer um desses padrões irá disparar esse aviso.

  Cada raiz sem lacre IDisposable tipo deve fornecer seu próprio método void Dispose (bool) virtual protegido. Dispose () deve chamar Dipose(true) e Finalize deve chamar Dispose (False). Se você estiver criando um tipo de IDisposable raiz sem lacre, você deve definir Dispose (bool) e chamá-lo. Para obter mais informações, consulte [limpeza de recursos não gerenciados](http://msdn.microsoft.com/library/a17b0066-71c2-4ba4-9822-8e19332fc213) na [diretrizes de Design do Framework](http://msdn.microsoft.com/library/5fbcaf4f-ea2a-4d20-b0d6-e61dee202b4b) seção da documentação do .NET Framework.

## <a name="rule-description"></a>Descrição da Regra
 Todos os tipos IDisposable devem implementar o padrão Dispose corretamente.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Examine seu código e determinar qual das seguintes resoluções corrigirá essa violação.

-   Remova IDisposable da lista de interfaces implementadas pelo {0} e substituir a implementação de Dispose da classe base em vez disso.

-   Remova o finalizador do tipo {0}, substitua Dispose (bool disposing) e coloque a lógica de finalização no caminho do código onde "disposing" é false.

-   Remover {0}, substitua Dispose (bool disposing) e colocar a lógica de descarte no caminho do código onde "disposing" é true.

-   Certifique-se de que {0} é declarado como público e selado.

-   Renomear {0} como "Dispose" e certifique-se de que ele é declarado como público e selado.

-   Certifique-se de que {0} é declarado como protegido, virtual e sem lacre.

-   Modificar {0} para que ele chame Dispose (True), em seguida, chama GC. SuppressFinalize na instância do objeto atual ('this' ou 'Me' no [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) e, em seguida, retorna.

-   Modificar {0} para que ele chama Dispose (False) e, em seguida, retorna.

-   Se você estiver escrevendo uma classe de IDisposable raiz sem lacre, certifique-se de que a implementação de IDisposable segue o padrão descrito anteriormente nesta seção.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="pseudo-code-example"></a>Exemplo de pseudocódigo
 O pseudocódigo a seguir fornece um exemplo geral de como Dispose (bool) devem ser implementadas em uma classe que usa gerenciada e recursos nativos.

```
public class Resource : IDisposable
{
    private IntPtr nativeResource = Marshal.AllocHGlobal(100);
    private AnotherResource managedResource = new AnotherResource();

// Dispose() calls Dispose(true)
    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }
    // NOTE: Leave out the finalizer altogether if this class doesn't
    // own unmanaged resources itself, but leave the other methods
    // exactly as they are.
    ~Resource()
    {
        // Finalizer calls Dispose(false)
        Dispose(false);
    }
    // The bulk of the clean-up code is implemented in Dispose(bool)
    protected virtual void Dispose(bool disposing)
    {
        if (disposing)
        {
            // free managed resources
            if (managedResource != null)
            {
                managedResource.Dispose();
                managedResource = null;
            }
        }
        // free native resources if there are any.
        if (nativeResource != IntPtr.Zero)
        {
            Marshal.FreeHGlobal(nativeResource);
            nativeResource = IntPtr.Zero;
        }
    }
}
```



