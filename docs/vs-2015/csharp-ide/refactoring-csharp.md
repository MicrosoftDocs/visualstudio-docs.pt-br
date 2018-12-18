---
title: Refatoração (c#) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.csharp.refactoring.preview
- vs.csharp.refactoring.issues
- vs.csharp.refactoring.buildwarning
- VS.PreviewChanges
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#]
ms.assetid: a39e656a-f81f-4c87-b484-a23168ff1dfc
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: b4f74017a067d4681eb14ba4eb826df504497430
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49262308"
---
# <a name="refactoring-c"></a>Refatoração (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Refatoração é o processo de aperfeiçoar seu código após ele ter sido gravado, alterando a estrutura interna do código sem alterar o comportamento externo do código.  
  
 Visual c# fornece os seguintes comandos de refatoração sobre o **refatoração** menu:  
  
-   [Refatoração Extrair método (C#)](../csharp-ide/extract-method-refactoring-csharp.md)  
  
-   [Refatoração Renomear (C#)](../csharp-ide/rename-refactoring-csharp.md)  
  
-   [Refatoração Encapsular campo (C#)](../csharp-ide/encapsulate-field-refactoring-csharp.md)  
  
-   [Refatoração Extrair Interface (C#)](../csharp-ide/extract-interface-refactoring-csharp.md)  
  
-   [Refatoração Remover parâmetros (C#)](../csharp-ide/remove-parameters-refactoring-csharp.md)  
  
-   [Refatoração Reordenar parâmetros (C#)](../csharp-ide/reorder-parameters-refactoring-csharp.md)  
  
## <a name="multi-project-refactoring"></a>Refatoração de multiprojeto  
 Visual Studio dá suporte a vários projetos de refatoração para projetos que estão na mesma solução. Todas as operações de refatoração que corrigir referências em arquivos corrigir essas referências a todos os projetos do mesmo idioma. Isso funciona para todas as referências de projeto a projeto. Por exemplo, se você tiver um aplicativo de console que faz referência a uma biblioteca de classes, quando você renomeia um tipo de biblioteca de classe (usando o `Rename` operação de refatoração), as referências ao tipo de biblioteca de classe no aplicativo de console também são atualizadas.  
  
## <a name="changes-preview"></a>Visualização de alterações  
 Muitas operações de refatoração oferecem uma oportunidade para você examinar todas as alterações de referência que executa uma operação de refatoração no seu código, antes de confirmar essas alterações. Essas opções de refatoração, um **visualizar alterações de referência** opção aparecerá na caixa de diálogo refatoração. Depois de selecionar essa opção e aceitar a operação de refatoração, o **caixa de diálogo Preview Changes** será exibida. Observe que o **visualizar alterações** caixa de diálogo tem dois modos de exibição. O modo de exibição inferior exibirá o seu código com todas as atualizações de referência devido à operação de refatoração. Pressionar **Cancelar** sobre o **visualizar alterações** caixa de diálogo irá parar a operação de refatoração e nenhuma alteração será feita ao seu código.  
  
## <a name="refactoring-warnings"></a>Avisos de refatoração  
 Se o compilador não tem uma compreensão completa de seu programa, e é possível que o mecanismo de refatoração não pode atualizar todas as referências apropriadas, a caixa de diálogo de aviso é exibida. Essa caixa de diálogo de aviso também fornece uma oportunidade para que você possa visualizar seu código na **visualizar alterações** caixa de diálogo antes de confirmar as alterações.  
  
> [!NOTE]
>  Se um método contém um erro de sintaxe (que indica o IDE com um sublinhado ondulado vermelho), o mecanismo de refatoração não atualizará todas as referências a um elemento dentro do método. O exemplo a seguir ilustra esse comportamento.  
  
 Por padrão, se você executar uma operação de refatoração sem referência a visualização é alterado é detectado um erro de compilação em seu programa e o ambiente de desenvolvimento exibe essa caixa de diálogo de aviso.  
  
 Se você executar uma operação de refatoração que tenha **visualizar alterações de referência** habilitado e um erro de compilação é detectado em seu programa, o ambiente de desenvolvimento exibirá a seguinte mensagem de aviso na parte inferior das **Visualizar alterações** caixa de diálogo, em vez de exibir o **aviso refatoração** caixa de diálogo:  
  
 **Seu projeto ou uma de suas dependências não compila no momento. Referências não podem ser atualizadas.**  
  
 Esse aviso refatoração está disponível somente para operações de refatoração que fornecem a **visualizar alterações de referência** opção.  
  
## <a name="error-tolerant-refactoring-and-verification-results"></a>Refatoração tolerante a erros e resultados de verificação  
 Refatoração é tolerante a falhas de erro. Em outras palavras, você pode executar uma refatoração em um projeto que não é possível compilar. Entretanto, nesses casos o processo de refatoração poderá não atualizar referências ambíguas corretamente.  
  
 O **resultados da verificação** caixa de diálogo pode notificá-lo se o mecanismo de refatoração detecta erros de compilação ou detecta que uma operação de refatoração inadvertidamente faz com que uma referência de código para associar a algo diferente do que era originalmente associada a (problema de religação).  
  
 Para ativar os resultados da verificação de recursos, diante a **ferramentas** menu, clique em **opções**. No **opções** diálogo caixa, expanda **Editor de texto**e, em seguida, expanda **c#**. Clique em **Advanced** e selecione o **verificar os resultados da refatoração** caixa de seleção.  
  
 O **resultados da verificação** caixa de diálogo distingue a diferença entre dois tipos de problemas de reassociação.  
  
### <a name="references-whose-definition-will-no-longer-be-the-renamed-symbol"></a>Referências cuja definição deixarão de ser o símbolo renomeado  
 Esse tipo de problema revinculação ocorre quando uma referência não mais se refere a um símbolo renomeado. Por exemplo, considere o seguinte código:  
  
```csharp  
class Example  
{  
    private int a;  
    public Example(int b)  
    {  
        a = b;  
    }  
}  
```  
  
 Se você usar a refatoração Renomear `a` para `b`, essa caixa de diálogo é exibida. A referência à variável renomeada `a` agora está associado ao parâmetro que é passado para o construtor, em vez de associação para o campo.  
  
### <a name="references-whose-definition-will-now-become-the-renamed-symbol"></a>Referências cuja definição se tornará agora o símbolo renomeado  
 Esse tipo de problema revinculação ocorre quando uma referência que anteriormente não se referia ao símbolo renomeado agora faz referência ao símbolo renomeado. Por exemplo, considere o seguinte código:  
  
```csharp  
class Example  
{  
    private static void Method(object a) { }  
    private static void OtherMethod(int a) { }  
    static void Main(string[] args)  
    {  
        Method(5);  
    }  
}  
```  
  
 Se você usar a refatoração Renomear `OtherMethod` para `Method`, essa caixa de diálogo é exibida. A referência na `Main` refere-se agora para o método sobrecarregado que aceita um `int` parâmetro em vez do método sobrecarregado que aceita um `object` parâmetro.  
  
## <a name="see-also"></a>Consulte também  
 [Usando o ambiente de desenvolvimento do Visual Studio para c#](../csharp-ide/using-the-visual-studio-development-environment-for-csharp.md)   
 [Como restaurar snippets de refatoração C#](../ide/how-to-restore-csharp-refactoring-snippets.md)