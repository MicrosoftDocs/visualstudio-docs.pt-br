---
title: Snippets de código do Visual C# | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snippets [C#], default snippets
- snippets [C#], Code Snippet Inserter
- Code Snippet Inserter [J#]
- Code Snippet Inserter [C#]
- Visual C#, default snippets
ms.assetid: dbea3dd6-e650-4190-b874-c9f097d7de6e
caps.latest.revision: 37
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 9c06243b4f41919c1c51002f0ed805a3fbd67112
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49297408"
---
# <a name="visual-c-code-snippets"></a>Snippets de código do Visual C#
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os snippets de código são snippets de código prontos que você pode inserir rapidamente em seu código. Por exemplo, o snippet de código `for` cria um loop `for` vazio. Alguns snippets de código são snippets de código envolvidos, que permite que você selecione linhas de código e, em seguida, escolha um snippet de código que incorpora as linhas de código selecionadas. Por exemplo, quando você seleciona linhas de código e, em seguida, ativa o snippet de código `for`, ele cria um loop `for` com as linhas de código selecionadas dentro do bloco de loop. Os snippets de código podem fazer com que escrever código de programa seja mais rápido, mais fácil e mais confiável.  
  
 Você pode inserir um snippet de código no local do cursor ou inserir um snippet de código envolvido com o código atualmente selecionado. A Unidade de Inserção de Snippet de Código é invocada por meio dos comandos **Inserir Snippet de Código** ou **Envolver com** no menu do **IntelliSense** ou usando os atalhos de teclado CTRL + K e, em seguida, X ou CTRL + K e, em seguida, S, respectivamente.  
  
 A Unidade de Inserção de Snippet de Código exibe o nome do snippet de código de todos os snippets de código disponíveis. A Unidade de Inserção de Snippet de Código também inclui uma caixa de diálogo de entrada em que você pode digitar o nome ou parte do nome do snippet de código. A Unidade de Inserção de Snippet de Código realça a correspondência mais próxima de um nome de snippet de código. Ao pressionar TAB a qualquer momento, a Unidade de Inserção de Snippet de Código será fechada e o snippet de código atualmente selecionado será inserido. Ao digitar ESC ou clicar com o mouse no Editor de Código a Unidade de Inserção de Snippet de Código será fechada sem inserir um snippet de código.  
  
## <a name="default-code-snippets"></a>Snippets de código padrão  
 Por padrão, os snippets de código a seguir são incluídos no Visual Studio.  
  
|Nome (ou atalho)|Descrição|Locais válidos para inserir o snippet|  
|--------------------------|-----------------|---------------------------------------|  
|#if|Cria uma diretiva [#if](http://msdn.microsoft.com/library/48cabbff-ca82-491f-a56a-eeccd528c7c2) e uma diretiva [#endif](http://msdn.microsoft.com/library/6a5fca55-5aee-441f-86f6-1c99fbe9ec05).|Em qualquer lugar.|  
|#region|Cria uma diretiva [#region](http://msdn.microsoft.com/library/672c87d1-9771-4f64-ab3f-0ad3d4ffb2b4) e uma diretiva [#endregion](http://msdn.microsoft.com/library/16099660-91b2-49e5-9646-77f9ef069526).|Em qualquer lugar.|  
|~|Cria um destruidor de classe que o contém.|Dentro de uma classe.|  
|Atributo|Cria uma declaração para uma classe que deriva de <xref:System.Attribute>.|Dentro de um namespace (incluindo o namespace global), uma classe ou uma estrutura.|  
|checked|Cria um bloco [checked](http://msdn.microsoft.com/library/718a1194-988d-48a3-b089-d6ee8bd1608d).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|classe|Cria uma declaração de classe.|Dentro de um namespace (incluindo o namespace global), uma classe ou uma estrutura.|  
|ctor|Cria um construtor para a classe que o contém.|Dentro de uma classe.|  
|cw|Cria uma chamada para <xref:System.Console.WriteLine%2A>.|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|do|Cria uma [fazer](http://msdn.microsoft.com/library/50725f79-9ba6-4898-aa78-6e331568a1bb) `while` loop.|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|else|Cria um bloco [else](http://msdn.microsoft.com/library/d9a1d562-8cf5-4bd4-9ba7-8ad970cd25b2).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|enum|Cria uma declaração [enum](http://msdn.microsoft.com/library/bbeb9a0f-e9b3-41ab-b0a6-c41b1a08974c).|Dentro de um namespace (incluindo o namespace global), uma classe ou uma estrutura.|  
|é igual a|Cria uma declaração de método que substitui o método <xref:System.Object.Equals%2A> definido na classe <xref:System.Object>.|Dentro de uma classe ou um struct.|  
|exception|Cria uma declaração para uma classe que deriva de uma exceção (<xref:System.Exception> por padrão).|Dentro de um namespace (incluindo o namespace global), uma classe ou uma estrutura.|  
|for|Cria um loop [for](http://msdn.microsoft.com/library/34041a40-2c87-467a-9ffb-a0417d8f67a8).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|foreach|Cria um loop [foreach](http://msdn.microsoft.com/library/5a9c5ddc-5fd3-457a-9bb6-9abffcd874ec).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|forr|Cria um loop [for](http://msdn.microsoft.com/library/34041a40-2c87-467a-9ffb-a0417d8f67a8) que decrementa a variável de loop depois de cada iteração.|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|if|Cria um bloco [if](http://msdn.microsoft.com/library/d9a1d562-8cf5-4bd4-9ba7-8ad970cd25b2).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|indexador|Cria uma declaração do indexador.|Dentro de uma classe ou um struct.|  
|interface|Cria uma declaração [interface](http://msdn.microsoft.com/library/7da38e81-4f99-4bc5-b07d-c986b687eeba).|Dentro de um namespace (incluindo o namespace global), uma classe ou uma estrutura.|  
|invoke|Cria um bloco que invoca um evento com segurança.|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|iterator|Cria um iterador.|Dentro de uma classe ou um struct.|  
|iterindex|Cria um par de iterador e indexador "nomeado" usando uma classe aninhada.|Dentro de uma classe ou um struct.|  
|bloqueio|Cria um bloco [lock](http://msdn.microsoft.com/library/656da1a4-707e-4ef6-9c6e-6d13b646af42).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|mbox|Cria uma chamada para <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName>. Talvez seja necessário adicionar uma referência para System.Windows.Forms.dll.|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|namespace|Cria uma declaração de [namespace](http://msdn.microsoft.com/library/0a788423-9110-42e0-97d9-bda41ca4870f).|Dentro de um namespace (incluindo o namespace global).|  
|prop|Cria uma declaração de [propriedade autoimplementada](http://msdn.microsoft.com/library/aa55fa97-ccec-431f-b5e9-5ac789fd32b7).|Dentro de uma classe ou um struct.|  
|propfull|Cria uma declaração de propriedade com acessadores get e set.|Dentro de uma classe ou um struct.|  
|propg|Cria uma [propriedade autoimplementada](http://msdn.microsoft.com/library/aa55fa97-ccec-431f-b5e9-5ac789fd32b7) somente leitura com um acessador "set" particular.|Dentro de uma classe ou um struct.|  
|sim|Cria uma declaração de método [static](http://msdn.microsoft.com/library/5509e215-2183-4da3-bab4-6b7e607a4fdf)[int](http://msdn.microsoft.com/library/212447b4-5d2a-41aa-88ab-84fe710bdb52) Main.|Dentro de uma classe ou um struct.|  
|struct|Cria uma declaração [struct](http://msdn.microsoft.com/library/ff3dd9b7-dc93-4720-8855-ef5558f65c7c).|Dentro de um namespace (incluindo o namespace global), uma classe ou uma estrutura.|  
|svm|Cria uma declaração de método [static](http://msdn.microsoft.com/library/5509e215-2183-4da3-bab4-6b7e607a4fdf)[void](http://msdn.microsoft.com/library/0d2d8a95-fe20-4fbd-bf5d-c1e54bce71d4) Main.|Dentro de uma classe ou um struct.|  
|switch|Cria um bloco [switch](http://msdn.microsoft.com/library/44bae8b8-8841-4d85-826b-8a94277daecb).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|try|Cria um bloco [try-catch](http://msdn.microsoft.com/library/cb5503c7-bfa1-4610-8fc2-ddcd2e84c438).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|tryf|Cria um bloco [try-finally](http://msdn.microsoft.com/library/c27623fb-7261-4464-862c-7a369d3c8f0a).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|unchecked|Cria um bloco [unchecked](http://msdn.microsoft.com/library/0c021f7c-923f-4b3d-a58f-55336f5ac27e).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|unsafe|Cria um bloco [unsafe](http://msdn.microsoft.com/library/7e818009-1c6e-4b9e-b769-3728a01586a0).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
|using|Cria uma diretiva [using](http://msdn.microsoft.com/library/b42b8e61-5e7e-439c-bb71-370094b44ae8).|Dentro de um namespace (incluindo o namespace global).|  
|while|Cria um loop [while](http://msdn.microsoft.com/library/72a0765c-6852-4aca-b327-4a11cb7f5c59).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|  
  
## <a name="see-also"></a>Consulte também  
 [Funções de snippet de código](../ide/code-snippet-functions.md)   
 [Snippets de código](../ide/code-snippets.md)   
 [Como criar um novo snippet com substituições](http://msdn.microsoft.com/en-us/8d56d43c-097a-475b-aa85-cae1554b6338)   
 [Parâmetros de modelo](../ide/template-parameters.md)   
 [Como: usar trechos de código Surround-with](../ide/how-to-use-surround-with-code-snippets.md)   
 [Como restaurar snippets de refatoração C#](../ide/how-to-restore-csharp-refactoring-snippets.md)



