---
title: Suporte para alterações de código (c# e Visual Basic) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [C#], supported code changes
- Edit and Continue [Visual Basic], supported code changes
ms.assetid: c7a48ea9-5a7f-4328-a9d7-f0e76fac399d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 855e8111721480b98c1395811090a54dd6e3ab2a
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31480528"
---
# <a name="supported-code-changes-c-and-visual-basic"></a>Alterações de código suportadas (c# e Visual Basic)
Editar e Continuar trata a maioria dos tipos de alterações de código dentro dos corpos do método. A maioria das alterações fora dos corpos do método e algumas alterações dentro dos corpos do método, no entanto, não podem ser aplicadas durante a depuração. Para aplicar essas alterações sem suporte, você deverá parar a depuração e reinicializar com uma versão atualizada do código.

## <a name="supported-changes-to-code"></a>Alterações suportadas em código

A tabela a seguir mostra as alterações que podem ser feitas para c# e o código do Visual Basic durante uma sessão de depuração sem reiniciar a sessão.

|Elemento de linguagem/recurso|Operação de edição com suporte|Limitações|
|-|-|-|
|Tipos|Adicionar métodos, campos, construtores, et al|[Sim](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|
|Iterators|Adicionar ou modificar|Não|
|expressões async/await|Adicionar ou modificar|[Sim](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|
|Objetos dinâmicos|Adicionar ou modificar|Não|
|expressões lambda|Adicionar ou modificar|[Sim](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|
|Expressões LINQ|Adicionar ou modificar|[Mesmo que as expressões lambda](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits)|

> [!NOTE]
> Novos recursos de idioma como interpolação de cadeia de caracteres e operadores condicionais nulos geralmente têm suporte por Edit e Continue. Para obter as informações mais atuais, consulte o [Enc suporte edita](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits) página.

## <a name="unsupported-changes-to-code"></a>Não há suporte para alterações no código
 As alterações a seguir não podem ser aplicadas ao código c# e Visual Basic durante uma sessão de depuração:  
  
-   As alterações na instrução atual ou qualquer outra instrução ativa.  
  
     As instruções ativas incluem todas as instruções, em funções na pilha de chamadas, que foram chamadas para acessar a instrução atual.  
  
     A instrução atual é marcada por um plano de fundo amarelo na janela de origem. Outras instruções ativas são marcadas por um plano de fundo sombreado e são somente leitura. Essas cores padrão podem ser alterados no **opções** caixa de diálogo.

- A tabela a seguir mostra as alterações não suportadas para o código por elemento de linguagem.

|Elemento de linguagem/recurso|Operação de edição sem suporte|
|-|-|
|Todos os elementos de código|Renomear|
|Namespaces|Adicionar|
|Namespaces, tipos, membros|Excluir|
|Genéricos|Adicionar ou modificar|
|Interfaces|Modificar|
|Tipos|Adicionar membro abstract ou virtual, adicione substituição (consulte [detalhes](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits))|
|Tipos|Adicionar destruidor|
|Membros|Modificar um membro fazendo referência a um tipo de interoperabilidade inserido|
|Membros (Visual Basic)|Modificar um membro com a instrução On Error ou Resume|
|Membros (Visual Basic)|Modificar um membro que contém uma cláusula de consulta de agregação, Group By, Join simples ou grupo ingressar LINQ|
|Métodos|Modificar assinaturas|
|Métodos|Fazer um método abstrato que se tornam não-abstrato, adicionando um corpo de método|
|Métodos|Excluir um corpo de método|
|Atributos|Adicionar ou modificar|
|Propriedades ou eventos|Modificar um parâmetro de tipo, o tipo base, tipo de representante ou tipo de retorno |
|Operadores ou indexadores|Modificar um parâmetro de tipo, o tipo base, tipo de representante ou tipo de retorno |
|blocos catch|Modificar quando ela contém uma instrução ativa|
|blocos try-catch-finally|Modificar quando ela contém uma instrução ativa|
|usando instruções|Adicionar|
|métodos/lambdas assíncrono|Modificar um método/lambda assíncrona em um projeto de destino do .NET Framework 4 e diminuir (consulte [detalhes](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits))|
|Iterators|Modificar um iterador em um projeto de destino do .NET Framework 4 e diminuir (consulte [detalhes](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits))|
  
## <a name="unsafe-code"></a>Código não seguro  
 Alterações em código não seguro têm as mesmas limitações que as alterações para o código de segurança, com uma restrição adicional: editar e continuar não dá suporte a alterações de código não seguro que sai dentro de um método que contém o `stackalloc` operador.  

## <a name="unsupported-app-scenarios"></a>Cenários de aplicativos sem suporte

Plataformas e aplicativos sem suporte incluem ASP.NET 5, Silverlight 5 e Windows 8.1.

> [!NOTE]
> Aplicativos com suporte incluem UWP do Windows 10 em x86 e x64 aplicativos para o .NET Framework 4.6 desktop ou versões posteriores (.NET Framework é apenas uma versão de área de trabalho).
  
## <a name="unsupported-scenarios"></a>Cenários sem suporte  
 Editar e Continuar não está disponível nos seguintes cenários de depuração:  
  
-   Depuração de modo misto (nativo/gerenciado).  
  
-   Depuração de SQL.  
  
-   Depurando um despejo do Dr. Watson.  
  
-   Depurando um aplicativo inserido de tempo de execução.  
  
-   Depurando um aplicativo usando anexar ao processo (**Depurar > Anexar ao processo**) em vez de executar o aplicativo escolhendo **iniciar** do **depurar** menu.  
  
-   Depurando código otimizado.  
  
-   Depurando uma versão antiga do código depois que uma nova versão não é compilada devido a erros de compilação.
  
## <a name="see-also"></a>Consulte também  
 [Editar e continuar (Visual c#)](../debugger/edit-and-continue-visual-csharp.md)   
 [Como usar Editar e Continuar (C#)](../debugger/how-to-use-edit-and-continue-csharp.md)