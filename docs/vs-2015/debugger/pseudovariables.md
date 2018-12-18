---
title: As pseudovariáveis | Microsoft Docs
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
- Watch window, pseudovariables
- debugging [Visual Studio], pseudovariables
- pseudovariables
ms.assetid: fae84f68-2138-4144-9bd4-c9e271b6182a
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 79d2f47acfbd5a4b6adf6d5f679fb3b514679dab
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51789493"
---
# <a name="pseudovariables"></a>Pseudovariáveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As pseudovariáveis são termos usados para exibir determinadas informações em uma janela variável ou o **QuickWatch** caixa de diálogo. Você pode inserir um pseudovariável da mesma maneira que incorporaria uma variável normal. As pseudovariáveis não são variáveis, no entanto, e não correspondem aos nomes de variáveis em seu programa.  
  
## <a name="example"></a>Exemplo  
 Suponha que você está escrevendo um aplicativo de código nativo e quer consultar o número de identificadores alocados em seu aplicativo. No **Watch** janela, você pode inserir a seguinte pseudovariável na **nome** coluna e, em seguida, pressionar Return para avaliá-lo:  
  
```  
$handles  
```  
  
 em código nativo, você pode usar as pseudovariáveis mostradas na tabela:  
  
|Pseudovariável|Função|  
|--------------------|--------------|  
|`$err`|Exibe o último conjunto de valores de erro com a função SetLastError. O valor que é exibido representa o que seria retornado pela função GetLastError.<br /><br /> Use `$err,hr` para ver o formulário decodificado deste valor. Por exemplo, se o erro mais recente fosse 3, `$err,hr` exibiria `ERROR_PATH_NOT_FOUND : The system cannot find the path specified.`|  
|`$handles`|Exibe o número de manipuladores alocados em seu aplicativo.|  
|`$vframe`|Exibe o endereço do quadro de pilha atual.|  
|`$tid`|Exibe a ID do thread para o thread atual.|  
|`$env`|Exibe o bloco de ambiente no visualizador de cadeia de caracteres.|  
|`$cmdline`|Exibe a cadeia de caracteres de linha de comando que iniciou o programa.|  
|`$pid`|Exibe a identificação do processo.|  
|`$` *RegisterName*<br /><br /> ou<br /><br /> `@` *RegisterName*|Exibe o conteúdo do registro *registername*.<br /><br /> Normalmente, você pode exibir conteúdo do registro simplesmente inserindo o nome do registro. A única vez que você precisa usar essa sintaxe é quando o nome do registro sobrecarrega um nome de variável. Se o nome do registro for igual ao nome da variável no escopo atual, o depurador interpretará o nome como um nome de variável. Ou seja, quando `$` *registername* ou `@` *registername* se torna útil.|  
|`$clk`|Exibe a hora em ciclos de relógio.|  
|`$user`|Exibe uma estrutura com informações de conta para a conta que executa o aplicativo. Por motivo de segurança, as informações de senha não são exibidas.|  
|`$exceptionstack`|Exibe o rastreamento de pilha da exceção atual de Tempo de Execução do Windows. O `$ exceptionstack` funciona apenas em aplicativos da Store que estão em execução no Windows 8.1 ou posterior. `$ exceptionstack` não tem suporte para exceções de C++ e SHE|  
|`$ReturnValue`|Mostra o valor retornado de um método .NET Framework. Consulte [examinar valores de retorno de chamadas de método](http://msdn.microsoft.com/library/e3245b37-8e2e-4200-ba84-133726e95f1f)|  
  
 No C# e no Visual Basic, você pode usar as pseudovariáveis mostradas na tabela:  
  
|Pseudovariável|Função|  
|--------------------|--------------|  
|`$exception`|Exibe informações sobre a última exceção. Se nenhuma exceção tiver ocorrido, a avaliação `$exception` exibirá uma mensagem de erro.<br /><br /> No Visual c#, quando o Assistente de exceção está desabilitado, `$exception` é adicionado automaticamente para o **Locals** janela quando ocorre uma exceção.|  
|`$user`|Exibe uma estrutura com informações de conta para a conta que executa o aplicativo. Por motivo de segurança, as informações de senha não são exibidas.|  
  
 No Visual Basic, você pode usar as pseudovariáveis mostradas na seguinte tabela:  
  
|Pseudovariável|Função|  
|--------------------|--------------|  
|`$delete` ou `$$delete`|Exclui uma variável implícita que foi criada na **imediato** janela. A sintaxe é `$delete,` *variável* ou`$delete,` *variável*`.`|  
|`$objectids` ou `$listobjectids`|Exibe todas as IDs de objetos como filhos da expressão especificada. A sintaxe é `$objectid,` *expressão* ou`$listobjectids,` *expressão*`.`|  
|`$` *N* `#`|Exibe o objeto com a ID de objeto igual a *N*.|  
|`$dynamic`|Exibe o especial **modo de exibição dinâmico** nó para um objeto que implementa o `IDynamicMetaObjectProvider`. Interface. A sintaxe é `$dynamic,` *objeto*. Esse recurso se aplica somente ao código que usa o .NET Framework versão 4. Ver [modo de exibição dinâmico](http://msdn.microsoft.com/library/4c851b17-2c12-46a0-9828-eb6ea6f5c563).|  
  
## <a name="see-also"></a>Consulte também  
 [Inspeção e QuickWatch Windows](../debugger/watch-and-quickwatch-windows.md)   
 [Windows variável](http://msdn.microsoft.com/library/ce0a67f6-2502-4b7a-ba45-cc32f8aeba3e)





