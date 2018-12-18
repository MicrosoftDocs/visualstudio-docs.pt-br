---
title: Depurar usando o depurador Just-in | Microsoft Docs
ms.custom: ''
ms.date: 09/24/18
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], Just-In-Time
- Just-In-Time debugging
ms.assetid: ee4d79a5-a1d2-4418-a93f-dd57a53e1836
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f66d3fdcd400be9356776647b0ead118e83d7108
ms.sourcegitcommit: c5e72875206b8c5737c29d5b1ec7b86eec747303
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49382735"
---
# <a name="debug-using-the-just-in-time-debugger-in-visual-studio"></a>Depurar usando o depurador Just-in-no Visual Studio

Depuração Just-In-Time pode iniciar o Visual Studio automaticamente quando um aplicativo em execução fora de erros do Visual Studio ou falhas. Com o Just-In-Time de depuração, você pode testar aplicativos fora do Visual Studio e abra o Visual Studio para iniciar a depuração quando ocorre um problema.

Depuração Just-In-Time funciona para aplicativos de desktop do Windows. Ele não funciona para aplicativos universais do Windows ou para código gerenciado que é hospedado em um aplicativo nativo, como visualizadores.

> [!TIP]
> Se você quiser apenas interromper a caixa de diálogo do depurador Just-in-apareça, mas não tiver instalado o Visual Studio, consulte [desabilita o depurador Just-in-](../debugger/just-in-time-debugging-in-visual-studio.md). Se você tivesse uma vez instalado o Visual Studio, talvez você precise [Just-In-Time de desabilitar a depuração do registro do Windows](#disable-just-in-time-debugging-from-the-windows-registry). 

##  <a name="BKMK_Enabling"></a> Habilitar ou Desabilitar depuração no Visual Studio Just-In-Time

>[!NOTE]
>Para habilitar ou desabilitar a depuração Just-In-Time, você deve estar executando o Visual Studio como administrador. Ativando ou desativando o Just-In-Time depuração define uma chave do registro e podem ser necessários privilégios de administrador para alterar essa chave. Para abrir o Visual Studio como administrador, o aplicativo do Visual Studio com o botão direito e escolha **executar como administrador**. 

Você pode configurar a depuração do Visual Studio Just-In-Time **ferramentas** > **opções** (ou **depurar** > **opções**) caixa de diálogo. 

**Para habilitar ou desabilitar Just-In-Time a depuração:**

1. Sobre o **ferramentas** ou **Debug** menu, selecione **opções** > **depuração**  >   **Just-In-Time**.

   ![Habilitar ou desabilitar a depuração JIT](../debugger/media/dbg-jit-enable-or-disable.png "habilitar ou desabilitar a depuração JIT")

1. No **just-in-habilitar a depuração para esses tipos de código** , selecione os tipos de código de depuração para depuração Just-In-Time: **gerenciado**, **nativo**, e/ou  **Script**.
   
1. Selecione **OK**.

Se você habilitar o Just-In-Time depurador, mas ele não abrir quando um aplicativo falhar ou erros, consulte [just-in-solucionar problemas de depuração](#jit_errors).

## <a name="disable-just-in-time-debugging-from-the-windows-registry"></a>Desabilitar a depuração do registro do Windows Just-In-Time

A depuração Just-In-Time ainda poderá ser habilitada, mesmo que o Visual Studio não esteja mais instalado no seu computador. Se o Visual Studio não estiver instalado, você pode desabilitar a depuração, editando o registro do Windows Just-In-Time.

**Para desativar a edição do registro de depuração Just-In-Time:**

1.  De que o Windows **inicie** menu, execute o **Editor do registro** (*regedit.exe*).

2.  No **Editor do registro** janela, localize e exclua as seguintes entradas do registro:

    -   **HKEY_LOCAL_MACHINE\Software\Microsoft\\. NETFramework\DbgManagedDebugger**

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger**

    ![Chave do registro JIT](../debugger/media/dbg-jit-registry.png "chave do registro JIT")

3.  Se o computador estiver executando um sistema operacional de 64 bits, também exclua as entradas de registro a seguir:

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\. NETFramework\DbgManagedDebugger**

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug\Debugger**

    Certifique-se de não excluir ou alterar outras chaves do registro.

5.  Fechar o **Editor do registro** janela.

## <a name="enable-just-in-time-debugging-of-a-windows-form"></a>Habilitar Just-In-Time de depuração de um formulário do Windows

Por padrão, os aplicativos de formulário do Windows têm um manipulador de exceção de nível superior que permite que o aplicativo continuará em execução se puder recuperar. Se um aplicativo de formulários do Windows gera uma exceção sem tratamento, ele mostra a caixa de diálogo a seguir:

![Exceção sem tratamento do formulário do Windows](../debugger/media/windowsformsunhandledexception.png "exceção sem tratamento do formulário do Windows")

Para habilitar a depuração em vez do padrão de tratamento de erros do Windows Form Just-In-Time, adicione essas configurações:

-  No `system.windows.forms` seção o *Machine. config* ou  *\<nome do aplicativo >. exe* de arquivo, defina o `jitDebugging` valor para `true`:
    
    ```xml
    <configuration>
        <system.windows.forms jitDebugging="true" />
    </configuration>
    ```
    
-  Em um aplicativo de formulário do Windows C++, também definido `DebuggableAttribute` à `true` em um *. config* arquivo ou em seu código. Se você compilar com [/Zi](/cpp/build/reference/z7-zi-zi-debug-information-format) e sem [/Og](/cpp/build/reference/og-global-optimizations), o compilador definirá esse atributo para você. Se você quiser depurar um build de versão não otimizada, no entanto, você deve definir `DebuggableAttribute` adicionando a seguinte linha em seu aplicativo *AssemblyInfo* arquivo:

   ```cpp
   [assembly:System::Diagnostics::DebuggableAttribute(true, true)];
   ```
   
   Para obter mais informações, consulte <xref:System.Diagnostics.DebuggableAttribute>.

## <a name="BKMK_Using_JIT"></a>Usar Just-In-Time de depuração
 Este exemplo explica quando um aplicativo gera um erro de depuração Just-In-Time.

 - Você deve ter o Visual Studio instalado para executar estas etapas. Se você não tiver o Visual Studio, você pode baixar gratuitamente [Visual Studio Community Edition](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).
   
 - Certifique-se de que Just-In-Time a depuração está [habilitada](#BKMK_Enabling) na **ferramentas** > **opções** > **depuração**  >  **Just-In-Time**.

Neste exemplo, você fará uma C# aplicativo de console no Visual Studio que lança uma [NullReferenceException](/dotnet/api/system.nullreferenceexception).

1. No Visual Studio, crie um C# aplicativo de console (**arquivo** > **New** > **projeto** > **C#**  >  **Aplicativo de console**) denominada *ThrowsNullException*. Para obter mais informações sobre como criar projetos no Visual Studio, consulte [instruções passo a passo: criar um aplicativo simples](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md).
   
1. Quando o projeto é aberto no Visual Studio, abra o *Program.cs* arquivo. Substitua o método Main () com o código a seguir, que imprime uma linha para o console e, em seguida, lança uma NullReferenceException:
   
   ```csharp
   static void Main(string[] args)
   {
       Console.WriteLine("we will now throw a NullReferenceException");
       throw new NullReferenceException("this is the exception thrown by the console app");
   }
   ```
   
1. Para criar a solução, escolha o **Debug** (padrão) ou **versão** configuration e, em seguida, selecione **Build** > **recompilar solução** . 
   
   >[!NOTE]
   >- Escolher **depurar** configuração para a experiência de depuração completa. 
   >- Se você selecionar [Release](../debugger/how-to-set-debug-and-release-configurations.md) configuração, você deve desligar [Just My Code](../debugger/just-my-code.md) para este procedimento trabalhar. Sob **ferramentas** > **opções** > **depuração**, cancele a seleção **habilitar apenas meu código**.
   Para obter mais informações sobre configurações de build, consulte [Noções básicas sobre configurações de build](../ide/understanding-build-configurations.md).
   
1. Abra o aplicativo compilado *ThrowsNullException.exe* em seu C# pasta do projeto (*...\ThrowsNullException\ThrowsNullException\bin\Debug* ou *...\ThrowsNullException\ ThrowsNullException\bin\Release*). 
   
   Você deverá ver a janela de comando a seguir:
   
   ![ThrowsNullExceptionConsole](../debugger/media/throwsnullexceptionconsole.png "ThrowsNullExceptionConsole")
   
1. O **escolher just-in-depurador** caixa de diálogo é aberta.
   
   ![JustInTimeDialog](../debugger/media/justintimedialog.png "JustInTimeDialog")
   
   Sob **depuradores disponíveis**, selecione **nova instância da \<a Visual Studio versão/edição preferencial >**, se ainda não estiver selecionado. 
   
1. Selecione **OK**.
   
   O projeto de ThrowsNullException é aberto em uma nova instância do Visual Studio, com a execução interrompida na linha que gerou a exceção:
   
   ![NullReferenceSecondInstance](../debugger/media/nullreferencesecondinstance.png "NullReferenceSecondInstance")

Você pode iniciar a depuração no momento. Se você estivesse depurando um aplicativo real, você precisa descobrir por que o código está lançando a exceção.

> [!CAUTION]
> Se seu aplicativo contém um código não confiável, será exibida uma caixa de diálogo de aviso de segurança, permitindo que você decida se deseja continuar com a depuração. Antes de continuar a depuração, decida se você confia no código. Você mesmo escreveu o código? Se o aplicativo está sendo executado em um computador remoto, você reconhece o nome do processo? Se o aplicativo estiver em execução localmente, considere a possibilidade de código mal-intencionado em execução no seu computador. Se você decidir que o código é confiável, selecione **Okey**. Caso contrário, selecione **Cancelar**.

## <a name="jit_errors"></a> Solucionar problemas de Just-In-Time de depuração 

Se Just-In-Time de depuração não foi iniciada quando um aplicativo falha, mesmo que ele está habilitado no Visual Studio:

- Relatório de erros do Windows poderia ser assumindo o tratamento de erros no seu computador. 
  
  Para corrigir esse problema, use o Editor do registro para adicionar um **valor DWORD** de **desabilitado**, com **dados de valor** de **1**, as seguintes chaves do registro:
  
  

  - **Relatório de erros do HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\Windows**
    
  - (Para computadores de 64 bits): **HKEY_LOCAL_MACHINE\Software\WOW6432Node\Microsoft\Windows\Windows relatório de erros**
  
  Para obter mais informações, consulte [. Configurações WER](https://docs.microsoft.com/windows/desktop/wer/wer-settings).
  
- Um problema conhecido do Windows pode estar causando o Just-In-Time depurador falhe. 
  
  A correção é adicionar um **valor DWORD** de **automática**, com **dados de valor** de **1**, as seguintes chaves do registro:
  
  
  - **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug**
    
  - (Para computadores de 64 bits): **HKEY_LOCAL_MACHINE\Software\WOW6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug**

Você pode ver as seguintes mensagens de erro durante Just-In-Time de depuração:

- **Não é possível anexar ao processo de travamento. O programa especificado não é um programa do Windows ou MS-DOS.**

    O depurador tentou anexar a um processo em execução em outro usuário.

    Para contornar esse problema, no Visual Studio, abra **Debug** > **anexar ao processo**e localize o processo que você deseja depurar no **processos disponíveis** lista. Se você não souber o nome do processo, localizar a ID de processo na **depurador do Visual Studio Just-in-** caixa de diálogo. Selecione o processo na **processos disponíveis** lista e, em seguida, selecione **Attach**. Selecione **não** para ignorar o Just-In-Time caixa de diálogo do depurador.

- **Não foi possível iniciar o depurador porque nenhum usuário está conectado.**

    Não há nenhum usuário conectado ao console, portanto, não há nenhuma sessão de usuário para exibir o Just-In-Time caixa de diálogo de depuração.

    Para corrigir esse problema, conecte-se ao computador.

- **Classe não registrada.**

    O depurador tentou criar uma classe COM que não está registrada, provavelmente devido a um problema de instalação.

    Para corrigir esse problema, use o instalador do Visual Studio para reinstalar ou reparar a instalação do Visual Studio.

## <a name="see-also"></a>Consulte também
- [Segurança do depurador](../debugger/debugger-security.md)
- [Noções básicas do depurador](../debugger/getting-started-with-the-debugger.md)
- [Opções, depuração, Just-In-Time caixa de diálogo](../debugger/just-in-time-debugging-options-dialog-box.md)
- [Aviso de segurança: anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou você não tiver certeza, não anexe a esse processo](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md)
