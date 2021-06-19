---
title: Gerenciar exceções com o depurador | Microsoft Docs
description: Saiba como especificar em quais exceções o depurador interrompe, em que ponto você deseja que o depurador se quebre e como as quebras são tratadas.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 89795df3a4c6b87c6a878cd07a072027f880e660
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390418"
---
# <a name="manage-exceptions-with-the-debugger-in-visual-studio"></a>Gerenciar exceções com o depurador no Visual Studio

Uma exceção é uma indicação de um estado de erro que ocorre enquanto um programa está sendo executado. Você pode dizer ao depurador quais exceções ou conjuntos de exceções interromper e em qual ponto você deseja que o depurador seja interromper (ou seja, pausar no depurador). Quando o depurador é descartado, ele mostra onde a exceção foi lançada. Você também pode adicionar ou excluir exceções. Com uma solução aberta no Visual Studio, use **Depurar** > Windows > Configurações de Exceção para abrir a janela **Configurações de** Exceção.

Forneça manipuladores que respondem às exceções mais importantes. Se você precisar saber como adicionar manipuladores para exceções, confira Corrigir bugs escrevendo [um código C# melhor.](../debugger/write-better-code-with-visual-studio.md) Além disso, saiba como configurar o depurador para sempre quebrar a execução de algumas exceções.

Quando ocorre uma exceção, o depurador grava uma mensagem de exceção na **janela Saída.** Ele pode quebrar a execução nos seguintes casos quando:

- Uma exceção é lançada que não é tratada.
- O depurador é configurado para quebrar a execução antes que qualquer manipulador seja invocado.
- Você definiu [Apenas Meu Código](../debugger/just-my-code.md)e o depurador está configurado para quebrar qualquer exceção que não seja tratada no código do usuário.

> [!NOTE]
> ASP.NET tem um manipulador de exceção de nível superior que mostra páginas de erro em um navegador. Ele não quebra a execução, **a menos que Apenas Meu Código** esteja ligado. Para ver um exemplo, consulte [Diga ao depurador para continuar em exceções sem-manuseio do usuário](#BKMK_UserUnhandled) abaixo.

<!-- Two consecutive notes are intentional here...-->

> [!NOTE]
> Em um Visual Basic, o depurador gerencia todos os erros como exceções, mesmo se você usar manipuladores de erro no estilo De erro.

## <a name="tell-the-debugger-to-break-when-an-exception-is-thrown"></a>Diga ao depurador para quebrar quando uma exceção for lançada

O depurador pode quebrar a execução no ponto em que uma exceção é lançada, portanto, você pode examinar a exceção antes que um manipulador seja invocado.

Na janela **Configurações de** Exceção (**Depurar > Configurações** de Exceção do Windows > ), expanda o nó para uma categoria de exceções, como Exceções do **Common Language Runtime.** Em seguida, marque a caixa de seleção para uma exceção específica dentro dessa categoria, **como System.AccessViolationException.** Você também pode selecionar uma categoria inteira de exceções.

![Acesso VerificadoViolationException](../debugger/media/exceptionsettingscheckaccess.png "ExceptionSettingsCheckAccess")

> [!TIP]
> Você pode encontrar exceções específicas usando  a janela Pesquisar na barra de ferramentas Configurações de Exceção ou usar a pesquisa para filtrar namespaces específicos **(como System.IO**). 

Se você selecionar uma  exceção na janela Configurações de Exceção, a execução do depurador será quebrada sempre que a exceção for lançada, independentemente de ela ser tratada. Agora, a exceção é chamada de exceção de primeira chance. Por exemplo, aqui estão alguns cenários:

- No aplicativo de console C# a seguir, o método Main lança **um AccessViolationException** dentro de um `try/catch` bloco.

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

  Se Você tiver **AccessViolationException** marcado em Configurações de **Exceção,** a execução será desaixado na linha quando você executar esse código no `throw` depurador. Em seguida, você pode continuar a execução. O console deve exibir as duas linhas:

  ```cmd
  caught exception
  goodbye
  ```

  mas não exibe a `here` linha.

- Um aplicativo de console C# faz referência a uma biblioteca de classes com uma classe que tem dois métodos. Um método lança uma exceção e a trata, enquanto um segundo método lança a mesma exceção, mas não a trata.

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

  Este é o método Main() do aplicativo de console:

  ```csharp
  static void Main(string[] args)
  {
      Class1 class1 = new Class1();
      class1.ThrowHandledException();
      class1.ThrowUnhandledException();
  }
  ```

  Se Você tiver **AccessViolationException** marcado em Configurações de **Exceção,** a execução será desaixada na linha em `throw` **ThrowHandledException()** e **ThrowUnhandledException()** quando você executar esse código no depurador.

Para restaurar as configurações de exceção para os padrões, escolha o botão Restaurar **a lista para as configurações** padrão:

![Restaurar padrões em Configurações de Exceção](../debugger/media/restoredefaultexceptions.png "RestoreDefaultExceptions")

## <a name="tell-the-debugger-to-continue-on-user-unhandled-exceptions"></a><a name="BKMK_UserUnhandled"></a>Diga ao depurador para continuar com exceções sem-manuseio do usuário

Se você estiver depurando código .NET ou JavaScript com [Apenas Meu Código](../debugger/just-my-code.md), poderá dizer ao depurador para evitar a quebra de exceções que não são tratadas no código do usuário, mas que são tratadas em outro lugar.

1. Na janela **Configurações de** Exceção, abra o menu de atalho clicando com o botão direito do mouse em um rótulo de coluna e selecione Mostrar **Colunas > Ações Adicionais**. (Se você tiver desligado **Apenas Meu Código**, não verá esse comando.) Uma terceira coluna chamada **Ações Adicionais é** exibida.

   ![Coluna Ações Adicionais](../debugger/media/additionalactionscolumn.png "AdditionalActionsColumn")

   Para uma exceção que mostra **Continuar** quando não tratada no código do usuário nesta coluna, o depurador continuará se essa exceção não for tratada no código do usuário, mas for tratada externamente.

2. Para alterar essa configuração para uma exceção específica, selecione a exceção, clique com o botão direito do mouse para mostrar o menu de atalho e selecione Continuar quando não for utilizado **no código do usuário.** Você também pode alterar a configuração de uma categoria inteira de exceções, como as exceções inteiras do Common Language Runtime).

   ![**Continuar quando não for utilizado na configuração de código do usuário**](../debugger/media/continuewhenunhandledinusercodesetting.png "ContinueWhenUnhandledInUserCodeSetting")

Por exemplo, ASP.NET aplicativos Web lidam com exceções convertendo-as em um código de status HTTP 500 ( tratamento de exceção na[API Web do ASP.NET](/aspnet/web-api/overview/error-handling/exception-handling)), o que pode não ajudar a determinar a origem da exceção. No exemplo a seguir, o código do usuário faz uma chamada para `String.Format()` que lança um <xref:System.FormatException> . Quebras de execução da seguinte forma:

![Quebras no usuário&#45;exceção sem-uso](../debugger/media/exceptionunhandledbyuser.png "ExceptionUnhandledByUser")

## <a name="add-and-delete-exceptions"></a>Adicionar e excluir exceções

Você pode adicionar e excluir exceções. Para excluir um tipo de exceção de uma  categoria, selecione a exceção e escolha o botão Excluir a exceção selecionada no botão de lista (o sinal de subtração) na barra de ferramentas Configurações **de** Exceção. Ou você pode clicar com o botão direito do mouse na exceção e **selecionar Excluir** no menu de atalho. A exclusão de uma exceção tem o mesmo efeito de ter a exceção desmarcada, que é que o depurador não será desmarcado quando ela for lançada.

Para adicionar uma exceção:

1. Na janela **Configurações de Exceção,** selecione uma das categorias de exceção (por exemplo, **Common Language Runtime**).

2. Escolha o **botão Adicionar uma exceção à categoria** selecionada (o sinal de a mais).

   ![Botão **Adicionar uma exceção à categoria selecionada**](../debugger/media/addanexceptiontotheselectedcategorybutton.png "AddAnExceptionToTheSelectedCategoryButton")

3. Digite o nome da exceção (por exemplo, **System.UriTemplateMatchException**).

   ![Digite o nome da exceção](../debugger/media/typetheexceptionname.png "TypeTheExceptionName")

   A exceção é adicionada à lista (em ordem alfabética) e marcada automaticamente.

Para adicionar uma exceção às categorias Exceções de Acesso à Memória de GPU, Exceções de Runtime do JavaScript ou Exceções win32, inclua o código de erro e a descrição.

> [!TIP]
> Verifique a ortografia. A **janela Configurações de** Exceção não verifica a existência de uma exceção adicionada. Portanto, se você digitar **Sytem.UriTemplateMatchException,** obterá uma entrada para essa exceção (e não para **System.UriTemplateMatchException**).

As configurações de exceção são persistentes no arquivo .suo da solução, portanto, elas se aplicam a uma solução específica. Não é possível reutilizar configurações de exceção específicas entre soluções. Agora, apenas as exceções adicionadas são persistentes; exceções excluídas não são. Você pode adicionar uma exceção, fechar e reabrir a solução, e a exceção ainda estará lá. Mas se você excluir uma exceção e fechar/reabrir a solução, a exceção reaparecerá.

A **janela Configurações de Exceção** dá suporte a tipos de exceção genéricos em C#, mas não em Visual Basic. Para quebrar exceções como , você deve adicionar a exceção `MyNamespace.GenericException<T>` como **MyNamespace.GenericException'1**. Ou seja, se você tiver criado uma exceção como este código:

```csharp
public class GenericException<T> : Exception
{
    public GenericException() : base("This is a generic exception.")
    {
    }
}
```

Você pode adicionar a exceção às **Configurações de Exceção** usando o procedimento anterior:

![adicionando exceção genérica](../debugger/media/addgenericexception.png "Addgenéricaexception")

## <a name="add-conditions-to-an-exception"></a>Adicionar condições a uma exceção

Use a **janela Configurações de** Exceção para definir condições em exceções. As condições com suporte no momento incluem os nomes do módulo a incluir ou excluir para a exceção. Ao definir nomes de módulo como condições, você pode optar por quebrar para a exceção somente em determinados módulos de código. Você também pode optar por evitar a quebra em módulos específicos.

> [!NOTE]
> A adição de condições a uma exceção tem suporte a partir do [!include[vs_dev15](../misc/includes/vs_dev15_md.md)] .

Para adicionar exceções condicionais:

1. Escolha o **botão Editar condições** na janela Configurações de Exceção ou clique com o botão direito do mouse na exceção e escolha Editar **Condições**.

   ![Condições para uma exceção](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

2. Para adicionar condições adicionais necessárias à exceção, selecione **Adicionar Condição** para cada nova condição. Linhas de condição adicionais são exibidas.

   ![Condições extras para uma exceção](../debugger/media/extraconditionsforanexception.png "ExtraConditionsForAnException")

3. Para cada linha de condição, digite o nome do módulo e altere a lista de operadores de comparação **para Igual ou** Não é Igual **a**. Você pode especificar curingas ( **\\\*** ) no nome para especificar mais de um módulo.

4. Se você precisar excluir uma condição, escolha **o X** no final da linha de condição.

## <a name="see-also"></a>Confira também

- [Continuar a execução após uma exceção](../debugger/continuing-execution-after-an-exception.md)<br/>
- [Como examinar um código de sistema após uma exceção](../debugger/how-to-examine-system-code-after-an-exception.md)<br/>
- [Como usar verificações de tempo de execução nativas](../debugger/how-to-use-native-run-time-checks.md)<br/>
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)
