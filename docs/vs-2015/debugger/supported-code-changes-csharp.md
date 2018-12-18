---
title: Suporte para alterações de código (c#) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Edit and Continue [C#], supported code changes
ms.assetid: c7a48ea9-5a7f-4328-a9d7-f0e76fac399d
caps.latest.revision: 30
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1d028c35ea5d0f00dd8206fbfe0b086c9dbed067
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51724668"
---
# <a name="supported-code-changes-c"></a>Alterações de código suportadas (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Editar e Continuar trata a maioria dos tipos de alterações de código dentro dos corpos do método. A maioria das alterações fora dos corpos do método e algumas alterações dentro dos corpos do método, no entanto, não podem ser aplicadas durante a depuração. Para aplicar essas alterações sem suporte, você deverá parar a depuração e reinicializar com uma versão atualizada do código.  
  
 As seguintes alterações não podem ser aplicadas ao código C# durante uma sessão de depuração:  
  
-   As alterações na instrução atual ou qualquer outra instrução ativa.  
  
     As instruções ativas incluem todas as instruções, em funções na pilha de chamadas, que foram chamadas para acessar a instrução atual.  
  
     A instrução atual é marcada por um plano de fundo amarelo na janela de origem. Outras instruções ativas são marcadas por um plano de fundo sombreado e são somente leitura. Essas cores padrão podem ser alteradas na **opções** caixa de diálogo.  
  
-   Alterando a assinatura de um tipo.  
  
-   Adicionando um método anônimo que captura uma variável que não havia sido capturada antes.  
  
-   Alterando, removendo ou alterando atributos.  
  
-   Adicionando, removendo ou alterando políticas `using`.  
  
-   Adicionando `foreach`, `using`, ou `lock` em torno da instrução ativa.  
  
## <a name="unsafe-code"></a>Código não seguro  
 Alterações no código não seguro têm as mesmas limitações que as alterações no código seguro, com uma restrição adicional: editar e continuar não dá suporte a alterações no código não seguro que saem de um método que contém o `stackalloc` operador.  
  
## <a name="exceptions"></a>Exceções  
 Editar e continuar dá suporte a alterações `catch` e `finally` bloqueia, exceto que a adição de uma `catch` ou `finally` bloco em torno da instrução ativa não é permitido.  
  
## <a name="unsupported-scenarios"></a>Cenários sem suporte  
 Editar e Continuar não está disponível nos seguintes cenários de depuração:  
  
-   Depurando código LINQ em determinadas circunstâncias. Para obter mais informações, consulte [Depurando LINQ](../debugger/debugging-linq.md).  
  
    -   Capturando uma variável que não havia sido capturada antes.  
  
    -   Alterando o tipo de expressão de consulta (por exemplo, selecione um = > selecione Novo {um = um};)  
  
    -   Removendo um `where` que contém uma instrução ativa.  
  
    -   Removendo um `let` que contém uma instrução ativa.  
  
    -   Removendo um `join` que contém uma instrução ativa.  
  
    -   Removendo um `orderby` que contém uma instrução ativa.  
  
-   Depuração de modo misto (nativo/gerenciado).  
  
-   Depuração de SQL.  
  
-   Depurando um despejo do Dr. Watson.  
  
-   Editando o código após uma exceção sem tratamento, quando o "**desenrolar a pilha de chamadas em exceções não tratadas**" opção não estiver selecionada.  
  
-   Depurando um aplicativo inserido de tempo de execução.  
  
-   Depurando um aplicativo que tem **anexar** em vez de executar o aplicativo escolhendo **iniciar** do **depurar** menu.  
  
-   Depurando código otimizado.  
  
-   Depurando uma versão antiga do código depois que uma nova versão não é compilada devido a erros de compilação.  
  
## <a name="see-also"></a>Consulte também  
 [Editar e continuar (Visual c#)](../debugger/edit-and-continue-visual-csharp.md)   
 [Como usar Editar e Continuar (C#)](../debugger/how-to-use-edit-and-continue-csharp.md)



