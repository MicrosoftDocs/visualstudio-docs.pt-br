---
title: Depurar usando o depurador just-in-time | Microsoft Docs
description: Depurar usando o depurador just-in-time no Visual Studio. A depuração Just-in-time pode iniciar o Visual Studio automaticamente quando um aplicativo ocorre ou falha.
ms.custom: SEO-VS-2020
ms.date: 09/24/2018
ms.topic: how-to
helpviewer_keywords:
- debugging [Visual Studio], Just-In-Time
- Just-In-Time debugging
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3bdd35056706491ace6e5e6b2f7c3f6a45464d2e
ms.sourcegitcommit: a0f5e7188838c5989c9cc78d99fb29bb2813501e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2021
ms.locfileid: "109729241"
---
# <a name="debug-using-the-just-in-time-debugger-in-visual-studio"></a>Depurar usando o depurador just-in-time no Visual Studio

A depuração Just-in-time pode iniciar o Visual Studio automaticamente quando um aplicativo está em execução fora dos erros ou falhas do Visual Studio. Com a depuração Just-in-time, você pode testar aplicativos fora do Visual Studio e abrir o Visual Studio para iniciar a depuração quando ocorrer um problema.

A depuração Just-in-time funciona para aplicativos da área de trabalho do Windows. Ele não funciona para aplicativos universais do Windows ou para código gerenciado hospedado em um aplicativo nativo, como visualizadores.

> [!TIP]
> Se você quiser apenas interromper a exibição da caixa de diálogo do depurador just-in-time, mas não tiver o Visual Studio instalado, consulte [desabilitar o depurador just-in-time](../debugger/just-in-time-debugging-in-visual-studio.md). Se você tiver instalado o Visual Studio, talvez seja necessário [desabilitar a depuração Just-in-time do registro do Windows](#disable-just-in-time-debugging-from-the-windows-registry).

## <a name="enable-or-disable-just-in-time-debugging-in-visual-studio"></a><a name="BKMK_Enabling"></a> Habilitar ou desabilitar a depuração Just-in-time no Visual Studio

>[!NOTE]
>Para habilitar ou desabilitar a depuração Just-in-time, você deve estar executando o Visual Studio como administrador. Habilitar ou desabilitar a depuração Just-in-time define uma chave do registro e privilégios de administrador podem ser necessários para alterar essa chave. Para abrir o Visual Studio como administrador, clique com o botão direito do mouse no aplicativo do Visual Studio e escolha **Executar como administrador**.

Você pode configurar a depuração Just-in-time na caixa de diálogo opções de **ferramentas** do Visual Studio  >   (ou opções de **depuração**  >  ).

**Para habilitar ou desabilitar a depuração Just-in-time:**

1. No menu **ferramentas** ou **depurar** , selecione **Opções**  >  **depuração**  >  **just-in-time**.

   ![Habilitar ou desabilitar a depuração JIT](../debugger/media/dbg-jit-enable-or-disable.png "Habilitar ou desabilitar a depuração JIT")

1. Na caixa de seleção **Habilitar depuração Just-in-time para esses tipos de código** , selecione os tipos de código que você deseja depuração Just-in-time para depurar: **gerenciado**, **nativo** e/ou **script**.

1. Selecione **OK**.

Se você habilitar o depurador Just-In-Time, mas ele não for aberto quando um aplicativo falhar ou erros, consulte Solucionar problemas de [depuração Just-In-Time.](#jit_errors)

## <a name="disable-just-in-time-debugging-from-the-windows-registry"></a>Desabilitar a depuração Just-In-Time do Registro do Windows

A depuração Just-In-Time ainda poderá ser habilitada, mesmo que o Visual Studio não esteja mais instalado no seu computador. Se Visual Studio estiver instalado, você poderá desabilitar a depuração Just-In-Time editando o Registro do Windows.

**Para desabilitar a depuração Just-In-Time editando o Registro:**

1. No menu **Iniciar do** Windows, execute o Editor do **Registro** (*regedit.exe*).

2. Na janela **Editor do Registro,** localize e exclua as seguintes entradas do Registro:

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\DbgManagedDebugger**

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger**

    ![Chave do Registro JIT](../debugger/media/dbg-jit-registry.png "Chave do Registro JIT")

3. Se o computador estiver executando um sistema operacional de 64 bits, exclua também as seguintes entradas do Registro:

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\DbgManagedDebugger**

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger**

    Não exclua nem altere nenhuma outra chave do Registro.

5. Feche a janela **Editor do Registro**.

## <a name="enable-just-in-time-debugging-of-a-windows-form"></a>Habilitar a depuração Just-In-Time de um Windows Form

Por padrão, os aplicativos do Windows Form têm um manipulador de exceção de nível superior que permite que o aplicativo continue em execução se puder se recuperar. Se um Windows Forms de dados lançar uma exceção sem tratativas, ele mostrará a seguinte caixa de diálogo:

![Exceção sem suporte do Windows Form](../debugger/media/windowsformsunhandledexception.png "Exceção sem suporte do Windows Form")

Para habilitar a depuração Just-In-Time em vez do tratamento de erro padrão do Windows Form, adicione estas configurações:

- Na seção `system.windows.forms` do arquivo *machine.config* ou *\<app name>.exe.config,* de definido `jitDebugging` o valor como `true` :

    ```xml
    <configuration>
        <system.windows.forms jitDebugging="true" />
    </configuration>
    ```

- Em um aplicativo C++ do Windows Form, também de definido `DebuggableAttribute` como em um arquivo `true` *.config* ou em seu código. Se você compilar com [/Zi](/cpp/build/reference/z7-zi-zi-debug-information-format) e sem [/Og](/cpp/build/reference/og-global-optimizations), o compilador definirá esse atributo para você. No entanto, se você quiser depurar um build de versão não otimizado, deverá definir adicionando a seguinte linha ao arquivo `DebuggableAttribute` *AssemblyInfo.cpp* do aplicativo:

   ```cpp
   [assembly:System::Diagnostics::DebuggableAttribute(true, true)];
   ```

   Para obter mais informações, consulte <xref:System.Diagnostics.DebuggableAttribute>.

## <a name="use-just-in-time-debugging"></a><a name="BKMK_Using_JIT"></a>Usar a depuração Just-In-Time
Este exemplo orienta você pela depuração Just-In-Time quando um aplicativo lança um erro.

- Você deve ter Visual Studio instalado para seguir estas etapas. Se você não tiver o Visual Studio, poderá baixar o [Visual Studio Community Edition](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)gratuito.

- Verifique se a depuração Just-in-time está [habilitada](#BKMK_Enabling) em **ferramentas**  >  **Opções** de  >  **depuração**  >  **just-in-time**.

Para este exemplo, você criará um aplicativo de console em C# no Visual Studio que gera uma [NullReferenceException](/dotnet/api/system.nullreferenceexception).

1. No Visual Studio, crie um aplicativo de console em C# (**arquivo**  >  **novo**  >  **projeto** de console do  >  **Visual C#**  >  ) chamado *ThrowsNullException*. Para obter mais informações sobre como criar projetos no Visual Studio, consulte [instruções passo a passo: criar um aplicativo simples](../get-started/csharp/tutorial-wpf.md).

1. Quando o projeto for aberto no Visual Studio, abra o arquivo *Program. cs* . Substitua o método Main () pelo código a seguir, que imprime uma linha no console e, em seguida, gera uma NullReferenceException:

   ```csharp
   static void Main(string[] args)
   {
       Console.WriteLine("we will now throw a NullReferenceException");
       throw new NullReferenceException("this is the exception thrown by the console app");
   }
   ```

1. Para criar a solução, escolha a configuração de **depuração** (padrão) ou de **versão** e, em seguida, selecione **criar**  >  **solução de recompilação**.

   > [!NOTE]
   > - Escolha **depurar** configuração para a experiência de depuração completa.
   > - Se você selecionar a configuração de [versão](../debugger/how-to-set-debug-and-release-configurations.md) , deverá desligar [apenas meu código](../debugger/just-my-code.md) para que esse procedimento funcione. Em **ferramentas**  >  **Opções**  >  **depuração**, desmarque **habilitar apenas meu código**.

   Para saber mais sobre configurações de build, veja [Noções básicas sobre configurações de build](../ide/understanding-build-configurations.md).

1. Abra o aplicativo *ThrowsNullException.exe* criado em sua pasta de projeto do C# (*. ..\ThrowsNullException\ThrowsNullException\bin\Debug* ou *. ..\ThrowsNullException\ThrowsNullException\bin\Release*).

   Você deverá ver a seguinte janela de comando:

   ![Captura de tela do console do para ThrowsNullException.exe, que gera uma exceção de referência nula sem tratamento (System. NullReferenceException).](../debugger/media/throwsnullexceptionconsole.png)

1. A caixa de diálogo **escolher depurador just-in-time** é aberta.

   ![Captura de tela da caixa de diálogo escolher depurador just-in-time, que aparece depois que a exceção é exibida na janela do console do ThrowsNullException.exe.](../debugger/media/justintimedialog.png)

   Em **depuradores disponíveis**, selecione **nova instância \<your preferred Visual Studio version/edition> do**, se ainda não tiver selecionado.

1. Selecione **OK**.

   O projeto ThrowsNullException é aberto em uma nova instância do Visual Studio, com a execução interrompida na linha que gerou a exceção:

   ![Captura de tela do projeto ThrowsNullException Visual Studio, com realce da linha de código-fonte que lançou a exceção.](../debugger/media/nullreferencesecondinstance.png)

Você pode iniciar a depuração neste ponto. Se você estivesse depurando um aplicativo real, precisaria descobrir por que o código está lançando a exceção.

> [!CAUTION]
> Se seu aplicativo contiver código não falso, uma caixa de diálogo de aviso de segurança será exibida, permitindo que você decida se deve continuar com a depuração. Antes de continuar a depuração, decida se confia no código. Você mesmo escreveu o código? Se o aplicativo está sendo executado em um computador remoto, você reconhece o nome do processo? Se o aplicativo estiver em execução localmente, considere a possibilidade de código mal-intencionado em execução no computador. Se você decidir que o código é confiável, selecione **OK.** Caso contrário, selecione **Cancelar**.

## <a name="troubleshoot-just-in-time-debugging"></a><a name="jit_errors"></a> Solucionar problemas de depuração Just-In-Time

Se a depuração Just-In-Time não iniciar quando um aplicativo falhar, mesmo que ele seja habilitado no Visual Studio:

- Relatório de Erros do Windows pode estar assumindo o tratamento de erro no computador.

  Para corrigir esse problema, use o Editor do Registro  para adicionar um Valor **DWORD** de **Desabilitado**, com dados de valor **de 1**, às seguintes chaves do Registro:

  - **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\Windows Error Reporting**

  - (Para máquinas de 64 bits): **HKEY_LOCAL_MACHINE\Software\WOW6432Node\Microsoft\Windows\Windows Error Reporting**

  Para obter mais informações, consulte [. Configurações de WER](/windows/desktop/wer/wer-settings).

- Um problema conhecido do Windows pode estar causando falha no depurador Just-In-Time.

  A correção é adicionar um **valor DWORD** de **Auto**, com **dados de** valor **de 1**, às seguintes chaves do Registro:

  - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug**

  - (Para máquinas de 64 bits): **HKEY_LOCAL_MACHINE\Software\WOW6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug**

Você pode ver as seguintes mensagens de erro durante a depuração Just-In-Time:

- **Não é possível anexar ao processo de falha. O programa especificado não é um programa Windows ou MS-DOS.**

    O depurador tentou anexar a um processo em execução em outro usuário.

    Para resolver esse problema, no Visual Studio, abra **Anexar** de depuração ao processo (ou pressione  >   **Ctrl** Alt P ) e encontre o processo que você deseja  +    +  depurar na lista Processos **Disponíveis.** Se você não sabe o nome do processo, localizou a ID do processo na caixa Visual Studio caixa de **diálogo Depurador Just-In-Time.** Selecione o processo na **lista Processos Disponíveis** e selecione **Anexar**. Selecione **Não** para descartar a caixa de diálogo do depurador Just-In-Time.

- **Não foi possível iniciar o depurador porque não há usuário conectado.**

    Não há nenhum usuário conectado ao console, portanto, não há nenhuma sessão de usuário para exibir a caixa de diálogo de depuração Just-In-Time.

    Para corrigir esse problema, conecte-se ao computador.

- **Classe não registrada.**

    O depurador tentou criar uma classe COM que não está registrada, provavelmente devido a um problema de instalação.

    Para corrigir esse problema, use o Instalador do Visual Studio para reinstalar ou reparar sua Visual Studio instalação.

## <a name="see-also"></a>Consulte também

- [Segurança do depurador](../debugger/debugger-security.md)
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)
- [Caixa de diálogo Opções, Depuração, Just-In-Time](../debugger/just-in-time-debugging-options-dialog-box.md)
- [Aviso de segurança Anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou você não tiver certeza, não anexe a esse processo](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md)
