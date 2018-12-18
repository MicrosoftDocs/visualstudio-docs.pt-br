---
title: Como exibir uma lista de itens separada por vírgula | Microsoft Docs
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
- MSBuild, separating items with semicolons
- MSBuild, formatting item collections
ms.assetid: 3cae844c-7c6d-4144-82dc-efad10ba458f
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c9de7655335d2937a31cc2d63f5220fbf5415745
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49195865"
---
# <a name="how-to-display-an-item-list-separated-with-commas"></a>Como exibir uma lista de itens separada por vírgulas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Quando você trabalha com listas de itens no [!INCLUDE[vstecmsbuildengine](../includes/vstecmsbuildengine-md.md)] ([!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]), às vezes, é útil exibir o conteúdo dessas listas de itens de uma maneira que seja fácil de ler. Ou, você pode ter uma tarefa que utiliza uma lista de itens separados por uma cadeia de caracteres do separador especial. Em ambos os casos, você pode especificar uma cadeia de caracteres do separador para uma lista de itens.  
  
## <a name="separating-items-in-a-list-with-commas"></a>Separando itens em uma lista com vírgulas  
 Por padrão, o [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] usa o ponto e vírgula para separar itens em uma lista. Por exemplo, considere um elemento `Message` com o seguinte valor:  
  
 `<Message Text="This is my list of TXT files: @(TXTFile)"/>`  
  
 Quando a lista de itens de `@(TXTFile)` contém os itens App1.txt, App2.txt e App3.txt, a mensagem é:  
  
 `This is my list of TXT files: App1.txt;App2.txt;App3.txt`  
  
 Se você quiser alterar o comportamento padrão, especifique seu próprio separador. A sintaxe para especificar um separador de lista de itens é:  
  
 `@(ItemListName, '<separator>')`  
  
 O separador pode ser um único caractere ou uma cadeia de caracteres e deve ser colocado entre aspas.  
  
#### <a name="to-insert-a-comma-and-a-space-between-items"></a>Para inserir uma vírgula e um espaço entre itens  
  
-   Use a notação de item semelhante ao seguinte:  
  
     `@(TXTFile, ', ')`  
  
## <a name="example"></a>Exemplo  
 Neste exemplo, a tarefa [Exec](../msbuild/exec-task.md) executa a ferramenta findstr para localizar as cadeias de caracteres de texto especificadas no arquivo, Phrases.txt. No comando findstr, cadeias de caracteres de pesquisa literais são indicadas pela opção **/c:**, portanto, o separador de item, `/c:` é inserido entre os itens na lista de itens de `@(Phrase)`.  
  
 Neste exemplo, a linha de comando equivalente é:  
  
 `findstr /i /c:hello /c:world /c:msbuild phrases.txt`  
  
```  
<Project DefaultTargets = "Find"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
  
    <ItemGroup>  
        <Phrase Include="hello"/>  
        <Phrase Include="world"/>  
        <Phrase Include="msbuild"/>  
    </ItemGroup>  
  
    <Target Name = "Find">  
        <!-- Find some strings in a file -->  
        <Exec Command="findstr /i /c:@(Phrase, ' /c:') phrases.txt"/>  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Itens](../msbuild/msbuild-items.md)



