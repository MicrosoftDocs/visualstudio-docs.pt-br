---
title: Gerenciar exceções com o depurador | Microsoft Docs
ms.custom: seodec18
ms.date: 10/09/2018
ms.topic: how-to
f1_keywords:
- vs.debug.exceptions
- vs.debug.exceptions.find
dev_langs:
- CSharp
- VB
- FSharp
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ff28944a36d338230a17cd533a4832452e42885b
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348451"
---
# <a name="manage-exceptions-with-the-debugger-in-visual-studio"></a>Gerenciar exceções com o depurador no Visual Studio

Uma exceção é uma indicação de um estado de erro que ocorre enquanto um programa está sendo executado. Você pode informar ao depurador quais exceções ou conjuntos de exceções devem ser interrompidas e em qual ponto você deseja que o depurador quebre (ou seja, PAUSE no depurador). Quando o depurador é interrompido, ele mostra onde a exceção foi lançada. Você também pode adicionar ou excluir exceções. Com uma solução aberta no Visual Studio, use **Debug > as configurações de exceção do Windows >** para abrir a janela de **configurações de exceção** .

Forneça manipuladores que respondem às exceções mais importantes. Se você precisar saber como adicionar manipuladores para exceções, consulte [corrigir bugs escrevendo um código C# melhor](../debugger/write-better-code-with-visual-studio.md). Além disso, saiba como configurar o depurador para sempre interromper a execução de algumas exceções.

Quando ocorre uma exceção, o depurador grava uma mensagem de exceção na janela de **saída** . Ele pode interromper a execução nos seguintes casos quando:

- Uma exceção é lançada e não é tratada.
- O depurador é configurado para interromper a execução antes de qualquer manipulador ser invocado.
- Você definiu [apenas meu código](../debugger/just-my-code.md)e o depurador está configurado para interromper qualquer exceção que não seja tratada no código do usuário.

> [!NOTE]
> ASP.NET tem um manipulador de exceção de nível superior que mostra páginas de erro em um navegador. Ele não interrompe a execução, a menos que **apenas meu código** esteja ativado. Para obter um exemplo, consulte [diga ao depurador para continuar nas exceções sem tratamento do usuário](#BKMK_UserUnhandled) abaixo.

<!-- Two consecutive notes are intentional here...-->

> [!NOTE]
> Em um aplicativo Visual Basic, o depurador gerencia todos os erros como exceções, mesmo se você usar os manipuladores de erro de estilo de erro.

## <a name="tell-the-debugger-to-break-when-an-exception-is-thrown"></a>Instruir o depurador a interromper quando uma exceção for gerada

O depurador pode interromper a execução no ponto em que uma exceção é lançada, para que você possa examinar a exceção antes que um manipulador seja invocado.

Na janela **configurações de exceção** (**depurar > configurações de exceção do Windows >**), expanda o nó de uma categoria de exceções, como **exceções de Common Language Runtime**. Em seguida, marque a caixa de seleção para uma exceção específica dentro dessa categoria, como **System. AccessViolationException**. Você também pode selecionar uma categoria inteira de exceções.

![AccessViolationException verificada](../debugger/media/exceptionsettingscheckaccess.png "ExceptionSettingsCheckAccess")

> [!TIP]
> Você pode encontrar exceções específicas usando a janela **Pesquisar** na barra de ferramentas **configurações de exceção** ou usar Pesquisar para filtrar namespaces específicos (como **System.Io**).

Se você selecionar uma exceção na janela **configurações de exceção** , a execução do depurador será interrompida sempre que a exceção for lançada, não importa se ela é tratada. Agora, a exceção é chamada de exceção de primeira chance. Por exemplo, aqui estão alguns cenários:

- No aplicativo de console C# a seguir, o método Main gera um **AccessViolationException** dentro de um `try/catch` bloco.

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

  Se você tiver o **AccessViolationException** verificado nas **configurações de exceção**, a execução será interrompida na `throw` linha quando você executar esse código no depurador. Em seguida, você pode continuar a execução. O console deve exibir as duas linhas:

  ```cmd
  caught exception
  goodbye
  ```

  Mas não exibe a `here` linha.

- Um aplicativo de console em C# faz referência a uma biblioteca de classes com uma classe que tem dois métodos. Um método gera uma exceção e a manipula, enquanto um segundo método gera a mesma exceção, mas não a trata.

  ```csharp
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

  Se você tiver **AccessViolationException** com check-in **das configurações de exceção**, a execução será interrompida na `throw` linha em **ThrowHandledException ()** e **ThrowUnhandledException ()** quando você executar esse código no depurador.

Para restaurar as configurações de exceção para os padrões, escolha o botão **restaurar a lista para as configurações padrão** :

![Restaurar padrões nas configurações de exceção](../debugger/media/restoredefaultexceptions.png "RestoreDefaultExceptions")

## <a name="tell-the-debugger-to-continue-on-user-unhandled-exceptions"></a><a name="BKMK_UserUnhandled"></a>Instruir o depurador a continuar em exceções não tratadas pelo usuário

Se estiver depurando código .NET ou JavaScript com [apenas meu código](../debugger/just-my-code.md), você poderá dizer ao depurador para evitar a interrupção de exceções que não são tratadas no código do usuário, mas que são tratadas em outro lugar.

1. Na janela **configurações de exceção** , abra o menu de atalho clicando com o botão direito do mouse em um rótulo de coluna e selecione **Mostrar colunas > ações adicionais**. (Se você desativou **apenas meu código**, não verá esse comando.) Uma terceira coluna denominada **ações adicionais** é exibida.

   ![Coluna de ações adicionais](../debugger/media/additionalactionscolumn.png "AdditionalActionsColumn")

   Para uma exceção que mostra **continuar quando não tratado no código do usuário** nesta coluna, o depurador continuará se essa exceção não for tratada no código do usuário, mas for manipulada externamente.

2. Para alterar essa configuração para uma exceção específica, selecione a exceção, clique com o botão direito do mouse para mostrar o menu de atalho e selecione **continuar quando não for tratado no código do usuário**. Você também pode alterar a configuração de uma categoria inteira de exceções, como as exceções de Common Language Runtime completas.

   ![* * Continuar quando não tratado na configuração do código do usuário * *](../debugger/media/continuewhenunhandledinusercodesetting.png "ContinueWhenUnhandledInUserCodeSetting")

Por exemplo, aplicativos Web ASP.NET lidam com exceções convertendo-as em um código de status HTTP 500 ([tratamento de exceção no ASP.NET Web API](/aspnet/web-api/overview/error-handling/exception-handling)), que podem não ajudar a determinar a origem da exceção. No exemplo a seguir, o código do usuário faz uma chamada para `String.Format()` que gera um <xref:System.FormatException> . A execução é interrompida da seguinte maneira:

![Quebras no usuário&#45;exceção sem tratamento](../debugger/media/exceptionunhandledbyuser.png "ExceptionUnhandledByUser")

## <a name="add-and-delete-exceptions"></a>Adicionar e excluir exceções

Você pode adicionar e excluir exceções. Para excluir um tipo de exceção de uma categoria, selecione a exceção e escolha o botão **excluir a exceção selecionada da lista** (o sinal de subtração) na barra de ferramentas **configurações de exceção** . Ou você pode clicar com o botão direito do mouse na exceção e selecionar **excluir** no menu de atalho. Excluir uma exceção tem o mesmo efeito que ter a exceção desmarcada, o que é que o depurador não será interrompido quando for lançado.

Para adicionar uma exceção:

1. Na janela **configurações de exceção** , selecione uma das categorias de exceção (por exemplo, **Common Language Runtime**).

2. Escolha o botão **Adicionar uma exceção à categoria selecionada** (o sinal de adição).

   ![* * Adicionar uma exceção ao botão de categoria selecionado * *](../debugger/media/addanexceptiontotheselectedcategorybutton.png "AddAnExceptionToTheSelectedCategoryButton")

3. Digite o nome da exceção (por exemplo, **System. UriTemplateMatchException**).

   ![Digite o nome da exceção](../debugger/media/typetheexceptionname.png "TypeTheExceptionName")

   A exceção é adicionada à lista (em ordem alfabética) e verificada automaticamente.

Para adicionar uma exceção às categorias exceções de acesso à memória GPU, exceções de tempo de execução do JavaScript ou exceções Win32, inclua o código de erro e a descrição.

> [!TIP]
> Verifique a ortografia. A janela de **configurações de exceção** não verifica a existência de uma exceção adicionada. Portanto, se você digitar System **. UriTemplateMatchException**, receberá uma entrada para essa exceção (e não para o **sistema. UriTemplateMatchException**).

As configurações de exceção são mantidas no arquivo. suo da solução, portanto, elas se aplicam a uma solução específica. Não é possível reutilizar configurações de exceção específicas em soluções. Agora, somente exceções adicionadas são persistidas; exceções excluídas não são. Você pode adicionar uma exceção, fechar e reabrir a solução, e a exceção ainda estará lá. Mas se você excluir uma exceção e fechar/reabrir a solução, a exceção será exibida novamente.

A janela de **configurações de exceção** dá suporte a tipos de exceção genérica em C#, mas não em Visual Basic. Para interromper exceções como `MyNamespace.GenericException<T>` , você deve adicionar a exceção como **MyNamespace. genericException ' 1**. Ou seja, se você tiver criado uma exceção como este código:

```csharp
public class GenericException<T> : Exception
{
    public GenericException() : base("This is a generic exception.")
    {
    }
}
```

Você pode adicionar a exceção às **configurações de exceção** usando o procedimento anterior:

![adicionando exceção genérica](../debugger/media/addgenericexception.png "Addgenéricaexception")

## <a name="add-conditions-to-an-exception"></a>Adicionar condições a uma exceção

Use a janela **configurações de exceção** para definir condições em exceções. Atualmente, as condições com suporte incluem os nomes de módulo a serem incluídos ou excluídos para a exceção. Ao definir nomes de módulo como condições, você pode optar por interromper a exceção somente em determinados módulos de código. Você também pode optar por evitar a quebra de determinados módulos.

> [!NOTE]
> A adição de condições a uma exceção é suportada a partir do [!include[vs_dev15](../misc/includes/vs_dev15_md.md)] .

Para adicionar exceções condicionais:

1. Escolha o botão **Editar condições** na janela configurações de exceção ou clique com o botão direito do mouse na exceção e escolha **Editar condições**.

   ![Condições para uma exceção](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

2. Para adicionar condições adicionais necessárias à exceção, selecione **Adicionar condição** para cada nova condição. Linhas de condição adicionais são exibidas.

   ![Condições adicionais para uma exceção](../debugger/media/extraconditionsforanexception.png "ExtraConditionsForAnException")

3. Para cada linha de condição, digite o nome do módulo e altere a lista operador de comparação para **Equals** ou **not Equals**. Você pode especificar curingas ( **\\\*** ) no nome para especificar mais de um módulo.

4. Se você precisar excluir uma condição, escolha o **X** no final da linha de condição.

## <a name="see-also"></a>Veja também

- [Continuar a execução após uma exceção](../debugger/continuing-execution-after-an-exception.md)<br/>
- [Como examinar um código de sistema após uma exceção](../debugger/how-to-examine-system-code-after-an-exception.md)<br/>
- [Como usar verificações de tempo de execução nativas](../debugger/how-to-use-native-run-time-checks.md)<br/>
- [Usar verificações de tempo de execução sem a biblioteca de tempo de execução C](../debugger/using-run-time-checks-without-the-c-run-time-library.md)<br/>
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)
