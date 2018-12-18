---
title: Gerenciando exceções com o depurador | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.exceptions
- vs.debug.exceptions.find
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- run-time errors
- exception handling, during debugging
- errors [debugger]
- debugger, runtime errors
- On Error-style error handlers
- exceptions, Win32
- run-time errors, debugging
- Win32, exceptions
- run time, exceptions
- error handling
- debugging [Visual Studio], exception handling
- common language runtime, exceptions
- native run-time checks
- exceptions, debugging
ms.assetid: 43a77fa8-37d0-4c98-a334-0134dbca4ece
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bdb648e7a29b3ed5d9a444e203ddbdcd6b0e73dc
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51770003"
---
# <a name="managing-exceptions-with-the-debugger"></a>Gerenciando exceções com o depurador
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Uma exceção é uma indicação de um estado de erro que ocorre enquanto um programa está sendo executado. Você pode e deve fornecer manipuladores que respondem às exceções mais importantes, mas é importante saber como configurar o depurador para interromper para as exceções que você deseja ver.  
  
 Quando uma exceção ocorre, o depurador grava uma mensagem de exceção para a janela de saída. Ele pode interromper a execução nos seguintes casos:  
  
-   Quando uma exceção é lançada e não é tratada.  
  
-   Quando o depurador está definido para interromper a execução imediatamente quando uma exceção é lançada, antes que qualquer manipulador seja invocado.  
  
-   Se você tiver definido [Just My Code](../debugger/just-my-code.md), e o depurador está definido como interromper qualquer exceção que não é tratada no código do usuário.  
  
> [!NOTE]
>  O ASP.NET tem um manipulador de exceção de nível superior que mostra páginas de erro em um navegador. Ele não interromper a execução, a menos que **Just My Code** está ativado. Por exemplo, consulte [definindo o depurador para continuar em exceções sem tratamento do usuário](../debugger/managing-exceptions-with-the-debugger.md#BKMK_UserUnhandled) abaixo.  
  
> [!NOTE]
>  Em um aplicativo Visual Basic, o depurador gerencia todos os erros como exceções, mesmo se você usar em manipuladores de erro – estilo de erro.  
  
## <a name="managing-exceptions-with-the-exception-settings-window"></a>Gerenciando exceções com a janela de configurações de exceção  
 Você pode usar o **configurações de exceção** janela para especificar quais exceções (ou conjuntos de exceções) fará com que o depurador seja interrompido e, no ponto em que você deseja que sua interrupção. Você pode adicionar ou excluir exceções ou especificar exceções ao interromper em. Abrir essa janela quando uma solução é aberta clicando **depurar / Windows / configurações de exceção**.  
  
 Você pode encontrar exceções específicas usando o **pesquisa** janela na **configurações de exceção** barra de ferramentas, ou usar Pesquisar para filtrar para namespaces específicos (por exemplo **System.IO**).  
  
### <a name="setting-the-debugger-to-break-when-an-exception-is-thrown"></a>Definir o depurador para interromper quando uma exceção é lançada  
 O depurador pode interromper a execução no ponto em que uma exceção é lançada, dando a você a oportunidade de examinar a exceção antes de um manipulador é invocado.  
  
 No **configurações de exceção** janela, expanda o nó para uma categoria de exceções (por exemplo, **exceções do Common Language Runtime**, que significa que as exceções .NET) e marque a caixa de seleção para um determinado exceção dentro dessa categoria (por exemplo **System. AccessViolationException**). Você também pode selecionar uma categoria inteira de exceções.  
  
 ![Checked AccessViolationException](../debugger/media/exceptionsettingscheckaccess.png "ExceptionSettingsCheckAccess")  
  
 Se você marcar uma determinada exceção, a execução do depurador interromperá sempre que a exceção é lançada, independentemente se ele é tratado ou sem tratamento. Neste ponto, a exceção é chamada uma exceção de primeira chance. Por exemplo, aqui estão alguns cenários:  
  
1. O seguinte c# aplicativo de console, o método Main lança um **AccessViolationException** dentro de um `try/catch` bloco:  
  
   ```csharp  
   static void Main(string[] args)  
   {  
       try  
       {  
           throw new AccessViolationException();  
           Console.WriteLine("here");  
       }  
       catch (Exception e)  
       {  
           Console.WriteLine("caught exception");  
       }  
       Console.WriteLine("goodbye");  
   }  
   ```  
  
    Se você tiver **AccessViolationException** check-in **configurações de exceção**, quando você executa esse código na execução do depurador será interrompido no `throw` linha. Em seguida, você pode continuar a execução. O console deverá exibir as duas linhas:  
  
   ```  
   caught exception  
   goodbye  
   ```  
  
    mas ele não exibe o `here` linha.  
  
2. Um aplicativo de console c# faz referência a uma biblioteca de classes com uma classe que tem dois métodos, um método que lança uma exceção e lida com isso e um segundo método que gera a mesma exceção e não tratá-la:  
  
   ```vb  
   public class Class1  
   {  
       public void ThrowHandledException()  
       {  
           try  
           {  
               throw new AccessViolationException();  
           }  
           catch (AccessViolationException ave)  
           {  
               Console.WriteLine("caught exception" + ave.Message);  
           }  
       }  
  
       public void ThrowUnhandledException()  
       {  
           throw new AccessViolationException();  
       }  
   }  
   ```  
  
    Aqui está o método Main () do aplicativo de console:  
  
   ```csharp  
   static void Main(string[] args)  
   {  
       Class1 class1 = new Class1();  
       class1.ThrowHandledException();  
       class1.ThrowUnhandledException();  
   }  
   ```  
  
    Se você tiver **AccessViolationException** check-in **configurações de exceção**, quando você executa esse código na execução do depurador será interrompido no `throw` linha em ambos os  **ThrowHandledException()** e **ThrowUnhandledException()**.  
  
   Se você quiser restaurar as configurações de exceção para os padrões, você pode clicar na **restaurar** na barra de ferramentas:  
  
   ![Restaurar padrões nas configurações de exceção](../debugger/media/restoredefaultexceptions.png "RestoreDefaultExceptions")  
  
###  <a name="BKMK_UserUnhandled"></a> Definir o depurador para continuar em exceções sem tratamento do usuário  
 Se você estiver depurando código do .NET ou JavaScript com [Just My Code](../debugger/just-my-code.md), você pode instruir o depurador não para interromper as exceções que não são manipuladas no código do usuário, mas são tratadas em outro lugar.  
  
1. No **configurações de exceção** janela, abra o menu de contexto clicando duas vezes na janela e, em seguida, selecionando **Mostrar colunas**. (Se você tiver desativado **Just My Code**, você não verá esse comando.)  
  
2. Você deve ver uma segunda coluna chamada **ações adicionais**. Esta coluna exibe **continuar quando não for tratado pelo código do usuário** sobre exceções específicas, o que significa que o depurador não é interrompido se essa exceção não é tratada no código do usuário, mas é tratada no código externo.  
  
3. Você pode alterar essa configuração para uma determinada exceção (selecione a exceção botão direito do mouse e selecionar/anular seleção **continuar quando não for tratado no código do usuário**) ou para uma categoria inteira de exceções (por exemplo, todas as comuns Exceções de tempo de execução de linguagem).  
  
   Por exemplo, aplicativos web ASP.NET manipulam exceções convertendo-os em um código de status HTTP 500 ([tratamento de exceções em API ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling)), que não podem ajudá-lo a determinar a origem da exceção. No exemplo a seguir, o código do usuário faz uma chamada para `String.Format()` que gera um <xref:System.FormatException>. Execução quebra da seguinte maneira:  
  
   ![quebra no usuário&#45;exceção unhanlded](../debugger/media/exceptionunhandledbyuser.png "ExceptionUnhandledByUser")  
  
### <a name="adding-and-deleting-exceptions"></a>Adicionando e excluindo exceções  
 Você pode adicionar e excluir exceções. Você pode excluir qualquer tipo de exceção de qualquer categoria selecionando a exceção e clicando na **exclua** botão (o sinal de subtração) o **configurações de exceção** barra de ferramentas ou clicando duas vezes a exceção e selecionando **excluir** no menu de contexto. Excluir uma exceção tem o mesmo efeito que ter a exceção não verificada, que é que o depurador não será interrompido quando ela é gerada.  
  
 Para adicionar uma exceção: na **configurações de exceção** janela, selecione uma das categorias de exceção (por exemplo, **Common Language Runtime**) e clique no **Add** botão. Digite o nome da exceção (por exemplo. **System.UriTemplateMatchException**). A exceção é adicionada à lista (em ordem alfabética) e é marcada automaticamente.  
  
 Se você quiser adicionar uma exceção para as exceções de acesso de memória de GPU, exceções de tempo de execução do JavaScript ou categorias de exceções do Win32, você precisa incluir o código de erro, bem como a descrição.  
  
> [!TIP]
>  Verifique a ortografia! O **configurações de exceção** janela não verifica a existência de uma exceção adicionada. Portanto, se você digitar **Sytem.UriTemplateMatchException**, você obterá uma entrada para essa exceção (e não para **System.UriTemplateMatchException**).  
  
 Configurações de exceção são persistidas no arquivo. suo da solução, para que elas se aplicam a uma determinada solução. É possível reutilizar configurações de exceção específicos em soluções. Neste ponto, apenas as exceções adicionadas são persistentes; não são excluídos de exceções. Em outras palavras, você pode adicionar uma exceção, feche e reabra a solução e a exceção ainda estará lá. Mas se você excluir uma exceção e fechar/reabrir a solução, a exceção reaparecerá.  
  
 O **configurações de exceção** janela dá suporte a tipos de exceção genérica em c#, mas não no Visual Basic. Para interromper as exceções, como `MyNamespace.GenericException<T>`, você deve adicionar a exceção como **MyNamespace.GenericException'1**. Ou seja, se você tiver criado uma exceção como este:  
  
```csharp  
public class GenericException<T> : Exception  
{  
    public GenericException() : base("This is a generic exception.")  
    {  
    }  
}  
```  
  
 Você pode adicionar a exceção **configurações de exceção** semelhante a esta:  
  
 ![Adicionar exceção genérica](../debugger/media/addgenericexception.png "AddGenericException")  
  
## <a name="see-also"></a>Consulte também  
 [Continuando a execução após uma exceção](../debugger/continuing-execution-after-an-exception.md)   
 [Como: examinar o código do sistema após uma exceção](../debugger/how-to-examine-system-code-after-an-exception.md)   
 [Como: usar verificações de tempo de execução nativas](../debugger/how-to-use-native-run-time-checks.md)   
 [Usar o tempo de execução verifica sem a biblioteca de tempo de execução C](../debugger/using-run-time-checks-without-the-c-run-time-library.md)   
 [Assistente de exceção](http://msdn.microsoft.com/library/992892ac-9d52-44cc-bf09-b44bfc5befeb)   
 [Noções básicas do depurador](../debugger/debugger-basics.md)





