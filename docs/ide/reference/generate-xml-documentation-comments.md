---
title: Inserir comentários da documentação XML no Visual Studio
ms.date: 01/26/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: e3c38e46a5c73d1f8018f56f76b971939ba8c316
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31945422"
---
# <a name="how-to-insert-xml-comments-for-documentation-generation"></a>Como inserir comentários XML para geração de documentação

O Visual Studio pode ajudá-lo a documentar os elementos de código, como classes e métodos, gerando automaticamente a estrutura padrão de comentários da documentação XML. No tempo de compilação, você pode gerar um arquivo XML contendo os comentários da documentação. O arquivo XML gerado pelo compilador pode ser distribuído em conjunto com o assembly do .NET para que o Visual Studio e outros IDEs possam usar o IntelliSense para mostrar informações rápidas sobre os tipos e membros. Além disso, o arquivo XML pode ser executado por ferramentas como [DocFX](https://dotnet.github.io/docfx/) e [Sandcastle](https://www.microsoft.com/download/details.aspx?id=10526) para gerar sites de referência de API.

> [!NOTE]
> O comando **Inserir Comentário**, que insere comentários da documentação XML automaticamente está disponível em [C#](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments) e em [Visual Basic](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation). No entanto, você pode inserir arquivos de [comentários da documentação XML em C++](/cpp/ide/xml-documentation-visual-cpp) manualmente e ainda gerar arquivos da documentação XML no tempo de compilação.

## <a name="to-insert-xml-comments-for-a-code-element"></a>Para inserir comentários XML para um elemento de código

1. coloque o cursor de texto acima do elemento que você deseja documentar, por exemplo, um método.

1. Realize um dos seguintes procedimentos:

   - Digite `///` em C# ou `'''` em Visual Basic

   - No menu **Editar**, escolha **IntelliSense** > **Inserir Comentário**

   - No menu acionado com o botão direito do mouse ou menu de contexto, no elemento de código ou logo acima dele, escolha **Trecho de Código** > **Inserir Comentário**

   O modelo XML é gerado imediatamente acima do elemento de código. Por exemplo, quando um método é comentado, ele gera o elemento **\<summary\>**, um elemento **\<param\>** para cada parâmetro e um elemento **\<returns\>** para documentar o valor retornado.

   ![Modelo de comentário XML – C#](media/doc-preview-cs.png)

   ![Modelo de comentário XML – Visual Basic](media/doc-preview-vb.png)

1. Insira descrições para cada elemento XML para documentar totalmente o elemento de código.

   ![Comentário concluído](media/doc-result-cs.png)

> [!NOTE]
> Há um [opção](../../ide/reference/options-text-editor-csharp-advanced.md) para ativar/desativar os comentários da documentação XML depois de digitar `///` em C# ou `'''` em Visual Basic. Na barra de menus, escolha **Ferramentas** > **Opções** para abrir a caixa de diálogo **Opções**. Em seguida, navegue até **Editor de Texto** > **C#** ou **Básico** > **Avançado**. Na seção **Ajuda do Editor**, procure a opção **Gerar comentários da documentação XML**.

## <a name="see-also"></a>Consulte também

- [Comentários da documentação XML (Guia de Programação em C#)](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)
- [Documentando seu código com comentários em XML (Guia do C#)](/dotnet/csharp/codedoc)
- [Como criar documentação XML (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation)
- [Comentários C++](/cpp/cpp/comments-cpp)
- [Documentação XML (C++)](/cpp/ide/xml-documentation-visual-cpp)
- [Geração de código](../code-generation-in-visual-studio.md)