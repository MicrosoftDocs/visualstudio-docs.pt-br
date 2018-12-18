---
title: Gerenciar exceções com o depurador | Microsoft Docs
ms.custom: seodec18
ms.date: 10/09/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 02c7fbfca9a63ac736972ebea01a854e24f90188
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53057912"
---
# <a name="manage-exceptions-with-the-debugger-in-visual-studio"></a>Gerenciar exceções com o depurador do Visual Studio

Uma exceção é uma indicação de um estado de erro que ocorre enquanto um programa está sendo executado. Você pode instruir o depurador quais exceções ou conjuntos de exceções para interromper e, no ponto em que você deseja que o depurador seja interrompido. Quando o depurador for interrompido, ele mostra onde a exceção foi lançada. Você também pode adicionar ou excluir exceções. Com uma solução aberta no Visual Studio, use **Depurar > Windows > configurações de exceção** para abrir o **configurações de exceção** janela.

Fornece manipuladores que respondem às exceções mais importantes. Saiba também como configurar o depurador para interromper a execução de algumas exceções sempre.

Quando ocorre uma exceção, o depurador grava uma mensagem de exceção para o **saída** janela. Ele pode interromper a execução a seguir casos quando:

- Uma exceção é gerada que não é manipulada.
- O depurador está configurado para interromper a execução antes que qualquer manipulador seja invocado.
- Você definiu [Just My Code](../debugger/just-my-code.md), e o depurador está configurado para interromper qualquer exceção que não é manipulada no código do usuário.

> [!NOTE]
> O ASP.NET tem um manipulador de exceção de nível superior que mostra páginas de erro em um navegador. Ele não interrompe a execução, a menos que **Just My Code** está ativado. Por exemplo, consulte [instruir o depurador para continuar em exceções sem tratamento do usuário](#BKMK_UserUnhandled) abaixo.

<!-- Two consecutive notes are intentional here...-->

> [!NOTE]
> Em um aplicativo Visual Basic, o depurador gerencia todos os erros como exceções, mesmo se você usar em manipuladores de erro de estilo de erro.

## <a name="tell-the-debugger-to-break-when-an-exception-is-thrown"></a>Instruir o depurador para interromper quando uma exceção é lançada

O depurador pode interromper a execução no ponto em que uma exceção é lançada, portanto, você pode examinar a exceção antes de um manipulador é invocado.

No **configurações de exceção** janela (**Depurar > Windows > configurações de exceção**), expanda o nó para uma categoria de exceções, tais como **exceções Common Language Runtime**. Em seguida, selecione a caixa de seleção para uma exceção específica dentro dessa categoria, como **System. AccessViolationException**. Você também pode selecionar uma categoria inteira de exceções.

![Check-AccessViolationException](../debugger/media/exceptionsettingscheckaccess.png "ExceptionSettingsCheckAccess")

> [!TIP]
> Você pode encontrar exceções específicas usando o **pesquisa** janela na **configurações de exceção** barra de ferramentas, ou usar Pesquisar para filtrar para namespaces específicos (como **System.IO**).

Se você selecionar uma exceção na **configurações de exceção** janela, a execução do depurador interromperá sempre que a exceção é lançada, não importa se ele é manipulado. Agora, a exceção é chamada uma exceção de primeira chance. Por exemplo, aqui estão alguns cenários:

- A seguir C# gera do método Main do aplicativo de console, um **AccessViolationException** dentro de um `try/catch` bloco.

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

  Se você tiver **AccessViolationException** check-in **configurações de exceção**, execução será interrompida no `throw` quando você executa esse código no depurador de linha. Em seguida, você pode continuar a execução. O console deverá exibir as duas linhas:

  ```cmd
  caught exception
  goodbye
  ```

  mas ele não exibe o `here` linha.

- Um C# aplicativo de console faz referência a uma biblioteca de classes com uma classe que tem dois métodos. Um método lança uma exceção e lida com isso, enquanto um segundo método gera a mesma exceção, mas não lida com ele.

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

  Se você tiver **AccessViolationException** check-in **configurações de exceção**, execução será interrompida no `throw` linha em ambos os **ThrowHandledException()** e **ThrowUnhandledException()** quando você executa esse código no depurador.

Para restaurar as configurações de exceção para os padrões, escolha o **restaurar a lista para as configurações padrão** botão:

![Restaurar padrões nas configurações de exceção](../debugger/media/restoredefaultexceptions.png "RestoreDefaultExceptions")

## <a name="BKMK_UserUnhandled"></a>Instruir o depurador para continuar em exceções sem tratamento do usuário

Se você estiver depurando código do .NET ou JavaScript com [Just My Code](../debugger/just-my-code.md), você pode instruir o depurador para evitar a quebra de exceções que não são manipuladas no código do usuário, mas são tratadas em outro lugar.

1. No **configurações de exceção** janela, abra o menu de atalho clicando com o rótulo de coluna e, em seguida, selecione **Mostrar colunas > ações adicionais**. (Se você desativou **Just My Code**, você não verá esse comando.) Uma terceira coluna denominada **ações adicionais** é exibida.

   ![Coluna de ações adicional](../debugger/media/additionalactionscolumn.png "AdditionalActionsColumn")

   Para uma exceção que mostra **continuar quando não for tratado no código do usuário** nesta coluna, o depurador continua se essa exceção não é manipulada no código do usuário, mas é tratada externamente.

2. Para alterar essa configuração para uma exceção específica, selecione a exceção, clique com botão direito para mostrar o menu de atalho e selecione **continuar quando não for tratada no código do usuário**. Você também pode alterar a configuração para uma categoria inteira de exceções, como as inteiras exceções de Common Language Runtime).

   ![* * Continuar quando não for tratado no código * * configuração de usuário](../debugger/media/continuewhenunhandledinusercodesetting.png "ContinueWhenUnhandledInUserCodeSetting")

Por exemplo, aplicativos web ASP.NET manipulam exceções convertendo-os em um código de status HTTP 500 ([tratamento de exceções em API Web ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling)), que pode não ajudar a determinar a origem da exceção. No exemplo a seguir, o código do usuário faz uma chamada para `String.Format()` que gera um <xref:System.FormatException>. Execução quebra da seguinte maneira:

![Quebra no usuário&#45;exceção sem tratamento](../debugger/media/exceptionunhandledbyuser.png "ExceptionUnhandledByUser")

## <a name="add-and-delete-exceptions"></a>Adicionar e excluir exceções

Você pode adicionar e excluir exceções. Para excluir um tipo de exceção de uma categoria, selecione a exceção e escolha o **exclui a exceção selecionada da lista** botão (o sinal de subtração) o **configurações de exceção** barra de ferramentas. Ou você pode a exceção botão direito do mouse e selecione **excluir** no menu de atalho. Excluir uma exceção tem o mesmo efeito que ter a exceção não verificada, que é que o depurador não quebre quando ela é gerada.

Para adicionar uma exceção:

1. No **configurações de exceção** janela, selecione uma das categorias de exceção (por exemplo, **Common Language Runtime**).

2. Escolha o **adicionar uma exceção à categoria selecionada** botão (o sinal de adição).

   ![* * Adicionar uma exceção para o botão selecionado categoria * *](../debugger/media/addanexceptiontotheselectedcategorybutton.png "AddAnExceptionToTheSelectedCategoryButton")

3. Digite o nome da exceção (por exemplo, **System.UriTemplateMatchException**).

   ![Digite o nome da exceção](../debugger/media/typetheexceptionname.png "TypeTheExceptionName")

   A exceção é adicionada à lista (em ordem alfabética) e verificada automaticamente.

Para adicionar uma exceção para as exceções de acesso de memória de GPU, exceções de tempo de execução do JavaScript ou categorias de exceções do Win32, incluem o código de erro e a descrição.

> [!TIP]
> Verifique a ortografia. O **configurações de exceção** janela não verifica a existência de uma exceção adicionada. Portanto, se você digitar **Sytem.UriTemplateMatchException**, você obterá uma entrada para essa exceção (e não para **System.UriTemplateMatchException**).

Configurações de exceção são persistidas no arquivo. suo da solução, para que elas se aplicam a uma determinada solução. É possível reutilizar configurações de exceção específicos em soluções. Agora, somente as exceções adicionadas são persistentes; não são excluídos de exceções. Você pode adicionar uma exceção, feche e reabra a solução e a exceção ainda estará lá. Mas se você excluir uma exceção e fechar/reabrir a solução, a exceção reaparecerá.

O **configurações de exceção** janela dá suporte a tipos de exceção genérica em c#, mas não no Visual Basic. Para interromper as exceções, como `MyNamespace.GenericException<T>`, você deve adicionar a exceção como **MyNamespace.GenericException'1**. Ou seja, se você tiver criado uma exceção com este código:

```csharp
public class GenericException<T> : Exception
{
    public GenericException() : base("This is a generic exception.")
    {
    }
}
```

Você pode adicionar a exceção **configurações de exceção** usando o procedimento anterior:

![Adicionar exceção genérica](../debugger/media/addgenericexception.png "AddGenericException")

## <a name="add-conditions-to-an-exception"></a>Adicionar condições a uma exceção

Use o **configurações de exceção** janela para definir condições em exceções. Condições com suporte no momento incluem os nomes de módulo para incluir ou excluir da exceção. Ao definir nomes de módulo como condições, você pode optar por interromper a exceção apenas em determinados módulos de código. Você também pode optar por evitar a quebra de módulos específicos.

> [!NOTE]
> Adicionar condições a uma exceção é nova no [!include[vs_dev15](../misc/includes/vs_dev15_md.md)].

Para adicionar exceções condicionais:

1. Escolha o **editar condições** botão na janela Configurações de exceção, ou a exceção botão direito do mouse e escolha **editar condições**.

   ![Condições para uma exceção](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

2. Para adicionar as condições adicionais necessárias para a exceção, selecione **Adicionar condição** para cada condição nova. Condição adicional que linhas são exibidas.

   ![As condições adicionais para uma exceção](../debugger/media/extraconditionsforanexception.png "ExtraConditionsForAnException")

3. Para cada linha de condição, digite o nome do módulo e altere a lista de operadores de comparação para **é igual a** ou **não é igual a**. Você pode especificar caracteres curinga (* *\\* * *) no nome para especificar mais de um módulo.

4. Se você precisar excluir uma condição, escolha o **X** no final da linha de condição.

## <a name="see-also"></a>Consulte também

[Continuar a execução depois de uma exceção](../debugger/continuing-execution-after-an-exception.md)<br/>
[Como: Examinar o código do sistema após uma exceção](../debugger/how-to-examine-system-code-after-an-exception.md)<br/>
[Como: Usar verificações de tempo de execução nativas](../debugger/how-to-use-native-run-time-checks.md)<br/>
[Usar verificações de tempo de execução sem a biblioteca em tempo de execução C](../debugger/using-run-time-checks-without-the-c-run-time-library.md)<br/>
[Tutorial: Aprender a depurar usando o Visual Studio](../debugger/getting-started-with-the-debugger.md)
