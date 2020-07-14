---
title: Como identificar símbolos em uma biblioteca | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Call Browser tool, identifying symbols in the library
- Call Browser tool
ms.assetid: 8fb0de61-71e7-42d1-8b41-2ad915474384
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fd091f003909110c696c2e42ad80d6c6ea4859d2
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905395"
---
# <a name="how-to-identify-symbols-in-a-library"></a>Como identificar símbolos em uma biblioteca
As ferramentas de navegação de símbolos exibem exibições hierárquicas de símbolos. Os símbolos representam namespaces, objetos, classes, membros de classe e outros elementos de linguagem.

 Cada símbolo na hierarquia pode ser identificado pelas informações de navegação passadas pela biblioteca de símbolos para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objetos por meio das seguintes interfaces:

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfoNode>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes>.

 O local do símbolo na hierarquia distingue um símbolo. Ele permite que as ferramentas de navegação de símbolos naveguem para um símbolo específico. O caminho exclusivo e totalmente qualificado para o símbolo determina o local. Cada elemento no caminho é um nó. O caminho começa com o nó de nível superior e termina com o símbolo específico. Por exemplo, se o método M1 for um membro da classe C1 e C1 estiver no namespace N1, o caminho completo do método M1 será N1. C1. M1. Esse caminho contém três nós: N1, C1 e M1.

 As informações de navegação permitem que o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objetos localize, selecione e mantenha selecionado os símbolos na hierarquia. Ele permite navegar de uma ferramenta de navegação para outra. Ao usar o **pesquisador de objetos** para procurar símbolos em um [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] projeto, você pode clicar com o botão direito do mouse em um método e iniciar a ferramenta de **pesquisador de chamadas** para exibir o método em um grafo de chamada.

 Dois formulários descrevem o local do símbolo. O formulário canônico é baseado no caminho totalmente qualificado do símbolo. Representa uma posição exclusiva do símbolo na hierarquia. Ele é independente da ferramenta de navegação de símbolos. Para obter as informações de formulário canônico, o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objetos chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> método. O formulário de apresentação descreve o local do símbolo dentro de uma ferramenta de navegação de símbolos específica. A posição do símbolo é relativa à posição de outros símbolos na hierarquia. Um determinado símbolo pode ter vários caminhos de apresentação, mas apenas um caminho canônico. Por exemplo, se a classe C1 for herdada da classe C2 e ambas as classes estiverem no namespace N1, o **pesquisador de objetos** exibirá a seguinte árvore hierárquica:

```
N1
    C1
        Bases and Interfaces
            C2
    C2
        Bases and Interfaces
. . . . . . . . . . .

```

 O caminho canônico da classe C2, neste exemplo, é N1 + C2. O caminho de apresentação do C2 inclui os nós C1 e "bases e interfaces": N1 + C1 + "bases e interfaces" + C2.

 Para obter as informações do formulário de apresentação, o Gerenciador de objetos chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A> método.

## <a name="to-obtain-canonical-and-presentation-forms-information"></a>Para obter informações de formas canônicas e de apresentação

1. Implementar o método de <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> .

     O Gerenciador de objetos chama esse método para obter a lista de nós contidos no caminho canônico do símbolo.

    ```vb
    Public Function EnumCanonicalNodes(ByRef ppEnum As Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes) As Integer
        Dim EnumNavInfoNodes As CallBrowserEnumNavInfoNodes = _New CallBrowserEnumNavInfoNodes(m_strMethod)
        ppEnum = CType(EnumNavInfoNodes, IVsEnumNavInfoNodes)
        Return 0
    End Function
    ```

    ```csharp
    public int EnumCanonicalNodes(out Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes ppEnum)
    {
        CallBrowserEnumNavInfoNodes EnumNavInfoNodes =
            new CallBrowserEnumNavInfoNodes(m_strMethod);
        ppEnum = (IVsEnumNavInfoNodes)(EnumNavInfoNodes);
        return 0;
    }

    ```

2. Implementar o método de <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A> .

     O Gerenciador de objetos chama esse método para obter a lista de nós contidos no caminho de apresentação do símbolo.

## <a name="see-also"></a>Confira também
- [Símbolo de suporte – ferramentas de navegação](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [Como registrar uma biblioteca com o Gerenciador de objetos](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [Como: expor listas de símbolos fornecidos pela biblioteca para o Gerenciador de objetos](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
