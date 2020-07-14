---
title: Depurar usando o depurador just-in-time | Microsoft Docs
ms.date: 09/24/2018
ms.topic: how-to
helpviewer_keywords:
- debugging [Visual Studio], Just-In-Time
- Just-In-Time debugging
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 40b6a0e43a8d0980615087c946e5dd14deef1b0b
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350570"
---
# <a name="debug-using-the-just-in-time-debugger-in-visual-studio"></a>Depurar usando o depurador just-in-time no Visual Studio

A depuração Just-in-time pode iniciar o Visual Studio automaticamente quando um aplicativo está em execução fora dos erros ou falhas do Visual Studio. Com a depuração Just-in-time, você pode testar aplicativos fora do Visual Studio e abrir o Visual Studio para iniciar a depuração quando ocorrer um problema.

A depuração Just-in-time funciona para aplicativos da área de trabalho do Windows. Ele não funciona para aplicativos universais do Windows ou para código gerenciado hospedado em um aplicativo nativo, como visualizadores.

> [!TIP]
> Se você quiser apenas interromper a exibição da caixa de diálogo do depurador just-in-time, mas não tiver o Visual Studio instalado, consulte [desabilitar o depurador just-in-time](../debugger/just-in-time-debugging-in-visual-studio.md). Se você tiver instalado o Visual Studio, talvez seja necessário [desabilitar a depuração Just-in-time do registro do Windows](#disable-just-in-time-debugging-from-the-windows-registry).

## <a name="enable-or-disable-just-in-time-debugging-in-visual-studio"></a><a name="BKMK_Enabling"></a>Habilitar ou desabilitar a depuração Just-in-time no Visual Studio

>[!NOTE]
>Para habilitar ou desabilitar a depuração Just-in-time, você deve estar executando o Visual Studio como administrador. Habilitar ou desabilitar a depuração Just-in-time define uma chave do registro e privilégios de administrador podem ser necessários para alterar essa chave. Para abrir o Visual Studio como administrador, clique com o botão direito do mouse no aplicativo do Visual Studio e escolha **Executar como administrador**.

Você pode configurar a depuração Just-in-time na caixa de diálogo opções de **ferramentas**do Visual Studio  >  **Options** (ou opções de **depuração**  >  **Options**).

**Para habilitar ou desabilitar a depuração Just-in-time:**

1. No menu **ferramentas** ou **depurar** , selecione **Opções**  >  **depuração**  >  **just-in-time**.

   ![Habilitar ou desabilitar a depuração JIT](../debugger/media/dbg-jit-enable-or-disable.png "Habilitar ou desabilitar a depuração JIT")

1. Na caixa de seleção **Habilitar depuração Just-in-time para esses tipos de código** , selecione os tipos de código que você deseja depuração Just-in-time para depurar: **gerenciado**, **nativo**e/ou **script**.

1. Selecione **OK**.

Se você habilitar o depurador just-in-time, mas ele não abrir quando um aplicativo falhar ou erros, consulte [solucionar problemas de depuração Just-in-time](#jit_errors).

## <a name="disable-just-in-time-debugging-from-the-windows-registry"></a>Desabilitar a depuração Just-in-time do registro do Windows

A depuração Just-In-Time ainda poderá ser habilitada, mesmo que o Visual Studio não esteja mais instalado no seu computador. Se o Visual Studio não estiver mais instalado, você poderá desabilitar a depuração Just-in-time editando o registro do Windows.

**Para desabilitar a depuração Just-in-time editando o registro:**

1. No menu **Iniciar** do Windows, execute o **Editor do registro** (*regedit.exe*).

2. Na janela **Editor do registro** , localize e exclua as seguintes entradas do registro:

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\DbgManagedDebugger**

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger**

    ![Chave do registro JIT](../debugger/media/dbg-jit-registry.png "Chave do registro JIT")

3. Se o computador estiver executando um sistema operacional de 64 bits, exclua também as seguintes entradas do registro:

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\DbgManagedDebugger**

    - **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger**

    Certifique-se de não excluir nem alterar nenhuma outra chave do registro.

5. Feche a janela **Editor do Registro**.

## <a name="enable-just-in-time-debugging-of-a-windows-form"></a>Habilitar a depuração Just-in-time de um formulário do Windows

Por padrão, os aplicativos do Windows Form têm um manipulador de exceção de nível superior que permite que o aplicativo continue em execução se ele puder ser recuperado. Se um aplicativo Windows Forms lançar uma exceção sem tratamento, ele mostrará a seguinte caixa de diálogo:

![Exceção sem tratamento do Windows Form](../debugger/media/windowsformsunhandledexception.png "Exceção sem tratamento do Windows Form")

Para habilitar a depuração Just-in-time em vez da manipulação de erros padrão do Windows Form, adicione estas configurações:

- Na `system.windows.forms` seção do arquivo *machine.config* ou * \<app name>.exe.config* , defina o `jitDebugging` valor como `true` :

    ```xml
    <configuration>
        <system.windows.forms jitDebugging="true" />
    </configuration>
    ```

- Em um aplicativo do Windows Form do C++, também defina `DebuggableAttribute` como `true` em um arquivo *. config* ou em seu código. Se você compilar com [/Zi](/cpp/build/reference/z7-zi-zi-debug-information-format) e sem [/Og](/cpp/build/reference/og-global-optimizations), o compilador definirá esse atributo para você. No entanto, se você quiser depurar uma compilação de versão não otimizada, deverá definir `DebuggableAttribute` a seguinte linha no arquivo *AssemblyInfo. cpp* do seu aplicativo:

   ```cpp
   [assembly:System::Diagnostics::DebuggableAttribute(true, true)];
   ```

   Para obter mais informações, consulte <xref:System.Diagnostics.DebuggableAttribute>.

## <a name="use-just-in-time-debugging"></a><a name="BKMK_Using_JIT"></a>Usar depuração Just-in-time
Este exemplo o orienta na depuração Just-in-time quando um aplicativo gera um erro.

- Você deve ter o Visual Studio instalado para seguir estas etapas. Se você não tiver o Visual Studio, poderá baixar o [Visual Studio Community Edition](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)gratuito.

- Verifique se a depuração Just-in-time está [habilitada](#BKMK_Enabling) em **ferramentas**  >  **Opções**de  >  **depuração**  >  **just-in-time**.

Para este exemplo, você criará um aplicativo de console em C# no Visual Studio que gera uma [NullReferenceException](/dotnet/api/system.nullreferenceexception).

1. No Visual Studio, crie um aplicativo de console em C# (**arquivo**  >  **novo**  >  **projeto**de console do  >  **Visual C#**  >  **Console Application**) chamado *ThrowsNullException*. Para obter mais informações sobre como criar projetos no Visual Studio, consulte [instruções passo a passo: criar um aplicativo simples](../get-started/csharp/tutorial-wpf.md).

1. Quando o projeto for aberto no Visual Studio, abra o arquivo *Program.cs* . Substitua o método Main () pelo código a seguir, que imprime uma linha no console e, em seguida, gera uma NullReferenceException:

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

   ![ThrowsNullExceptionConsole](../debugger/media/throwsnullexceptionconsole.png "ThrowsNullExceptionConsole")

1. A caixa de diálogo **escolher depurador just-in-time** é aberta.

   ![JustInTimeDialog](../debugger/media/justintimedialog.png "JustInTimeDialog")

   Em **depuradores disponíveis**, selecione **nova instância \<your preferred Visual Studio version/edition> do **, se ainda não tiver selecionado.

1. Selecione **OK**.

   O projeto ThrowsNullException é aberto em uma nova instância do Visual Studio, com a execução interrompida na linha que gerou a exceção:

   ![NullReferenceSecondInstance](../debugger/media/nullreferencesecondinstance.png "NullReferenceSecondInstance")

Você pode iniciar a depuração neste ponto. Se você estivesse Depurando um aplicativo real, precisaria descobrir por que o código está lançando a exceção.

> [!CAUTION]
> Se seu aplicativo contiver um código não confiável, uma caixa de diálogo de aviso de segurança será exibida, permitindo que você decida se deseja continuar com a depuração. Antes de continuar a depuração, decida se você confia no código. Você mesmo escreveu o código? Se o aplicativo está sendo executado em um computador remoto, você reconhece o nome do processo? Se o aplicativo estiver em execução localmente, considere a possibilidade de código mal-intencionado em execução no seu computador. Se você decidir que o código é confiável, selecione **OK**. Caso contrário, selecione **Cancelar**.

## <a name="troubleshoot-just-in-time-debugging"></a><a name="jit_errors"></a>Solucionar problemas de depuração Just-in-time

Se a depuração Just-in-time não iniciar quando um aplicativo falhar, mesmo que ele esteja habilitado no Visual Studio:

- Relatório de Erros do Windows pode estar assumindo o tratamento de erros em seu computador.

  Para corrigir esse problema, use o editor do registro para adicionar um **valor DWORD** **desabilitado**, com **dados de valor** de **1**, às seguintes chaves do registro:

  - **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\Windows Error Reporting**

  - (Para computadores de 64 bits): **HKEY_LOCAL_MACHINE relatório de erros \software\wow6432node\microsoft\windows\windows**

  Para obter mais informações, consulte [. Configurações do WER](/windows/desktop/wer/wer-settings).

- Um problema conhecido do Windows pode estar fazendo com que o depurador just-in-time falhe.

  A correção é adicionar um **valor DWORD** de **auto**, com **dados de valor** de **1**, às seguintes chaves do registro:

  - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug**

  - (Para computadores de 64 bits): **HKEY_LOCAL_MACHINE \Software\wow6432node\microsoft\windows NT\CurrentVersion\AeDebug**

Você poderá ver as seguintes mensagens de erro durante a depuração Just-in-time:

- **Não é possível anexar ao processo de falha. O programa especificado não é um programa do Windows ou MS-DOS.**

    O depurador tentou anexar a um processo em execução em outro usuário.

    Para contornar esse problema, no Visual Studio, abra **Debug**a  >  **anexação de depuração a ser processada**e localize o processo que você deseja depurar na lista de **processos disponíveis** . Se você não souber o nome do processo, localize a ID do processo na caixa de diálogo do **depurador just-in-time do Visual Studio** . Selecione o processo na lista **processos disponíveis** e selecione **anexar**. Selecione **não** para ignorar a caixa de diálogo do depurador just-in-time.

- **Não foi possível iniciar o depurador porque não há usuário conectado.**

    Não há nenhum usuário conectado ao console, portanto, não há nenhuma sessão de usuário para exibir a caixa de diálogo de depuração Just-in-time.

    Para corrigir esse problema, conecte-se ao computador.

- **Classe não registrada.**

    O depurador tentou criar uma classe COM que não está registrada, provavelmente devido a um problema de instalação.

    Para corrigir esse problema, use o Instalador do Visual Studio para reinstalar ou reparar a instalação do Visual Studio.

## <a name="see-also"></a>Veja também

- [Segurança do depurador](../debugger/debugger-security.md)
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)
- [Opções, depuração, caixa de diálogo just-in-time](../debugger/just-in-time-debugging-options-dialog-box.md)
- [Aviso de segurança Anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou você não tiver certeza, não anexe a esse processo](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md)
