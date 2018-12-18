---
title: Adicionando dados de interação de camadas da linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- tier interaction profiling method
- profiling tools,tier interaction method
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bbb950947b3f97a4f6d6e9c1461dd2023595058c
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2018
ms.locfileid: "43775027"
---
# <a name="add-tier-interaction-data-from-the-command-line"></a>Adicionar dados de interação de camada por meio da linha de comando

A criação de perfil de interação de camadas fornece informações adicionais sobre os tempos de execução síncronos que o [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] chama em funções de aplicativos de várias camadas que se comunicam com um ou mais bancos de dados.

**Windows 8 e Windows Server 2012**

Para coletar dados de interação de camadas em aplicativos da área de trabalho do Windows 8 e do Windows Server 2012, você deve usar o método de instrumentação. Não há suporte para a coleta de dados de interação de camadas nos aplicativos UWP.

**Edições do Visual Studio**

A criação de perfil de interação de camadas pode ser coletada usando qualquer edição do Visual Studio. No entanto, os dados de criação de perfil de interação de camadas só podem ser exibidos no Visual Studio Enterprise.

**Coletar dados TIP em um computador remoto**

Para coletar os dados de interação de camadas em um computador remoto, você precisa copiar o arquivo **vs_profiler\_**_\<Platform>_**\_**_\<Language>_**.exe** da pasta _%VSInstallDir%_**\Team Tools\Performance Tools\Setups** de um computador com o Visual Studio para o computador remoto e instalá-lo. Não é possível usar as ferramentas de criação de perfil no pacote de download da [Depuração Remota](../debugger/remote-debugging.md).

**Relatórios TIP**

Os dados de interação entre camadas só podem ser exibidos no Microsoft Visual Studio Enterprise. Os relatórios de interação de camadas baseados em arquivo por meio de [VSPerfReport](../profiling/vsperfreport.md) não estão disponíveis.

## <a name="add-tier-interaction-data-with-vsperfcmd"></a>Adicionar dados de interação de camadas com VSPerfCmd

A ferramenta de linha de comando VSPerfASPNETCmd permite acessar toda a funcionalidade disponível nas Ferramentas de Criação de Perfil. Para adicionar interação de camadas a dados de criação de perfil coletados usando VSPerfCmd, você deve usar o utilitário **VSPerfCLREnv** para definir e remover as variáveis de ambiente que permitem dados de interação de camadas. As opções que você especificar e os procedimentos necessários para coletar dados dependem do tipo de aplicativo cujo perfil está sendo criado.

## <a name="profile-stand-alone-applications"></a>Criar perfil de aplicativos autônomos

Para adicionar dados de interação de camadas a um aplicativo que não é executado por outro processo, como um aplicativo da área de trabalho do Windows que faz chamadas do [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] síncronas para um banco de dados do SQL Server, use a opção **VSPerfClrEnv /InteractionOn** para definir as variáveis de ambiente e a opção **VSPerfClrEnv /InteractionOff** para removê-las.

No exemplo a seguir, um aplicativo de área de trabalho do Windows tem o perfil criado usando o método de instrumentação e dados de interação de camadas são coletados.

### <a name="profile-a-windows-desktop-application-example"></a>Criar perfil de um exemplo de aplicativo da área de trabalho do Windows

1. Abra uma janela de prompt de comando com privilégios de administrador. Clique em **Iniciar**, aponte para **Todos os Programas** e, em seguida, aponte para **Acessórios**. Clique com o botão direito do mouse em **Prompt de Comando** e, em seguida, clique em **Executar Como Administrador**.

2. Inicialize a criação de perfil do .NET e as variáveis de ambiente TIP. Digite os seguintes comandos:

    ```cmd
    vsperfclrenv /traceon
    vsperfclrenv /interactionon
    ```

3. Inicie o criador de perfil. Digite o seguinte comando:

    ```cmd
    vsperfcmd /start:trace /output:Desktop_tip.vsp 
    ```

4. Inicie o aplicativo com VSPerfCmd. Digite o seguinte comando:

    ```cmd
    vsperfcmd /launch:DesktopApp.exe
    ```

5. Utilize o aplicativo para coletar dados de criação de perfil e, em seguida, feche o aplicativo da maneira normal.

6. Limpe as variáveis de ambiente TIP. Digite o seguinte comando:

    ```cmd
    vsperfclrenv /off
    ```

Para obter mais informações, confira [Profile stand-alone applications](../profiling/command-line-profiling-of-stand-alone-applications.md) (Criação de perfil de aplicativos autônomos).

## <a name="profile-services"></a>Serviços de perfil

Para criar perfil de serviços, incluindo aplicativos [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], use a opção **VSPerfClrEnv /GlobalInteractionOn** para definir as variáveis de ambiente e a opção **VSPerfClrEnv /GlobalInteractionOff** para removê-las.

Para criar perfil de serviços, incluindo aplicativos Web do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], geralmente é necessário reiniciar o computador para habilitar a criação de perfil.

No exemplo a seguir, um serviço do Windows tem o perfil criado usando o método de instrumentação e dados de interação de camadas são coletados.

### <a name="profile-a-windows-service-example"></a>Criação de perfil de um serviço do Windows

1. Se necessário, instale o serviço.

2. Abra uma janela de prompt de comando com privilégios de administrador. Clique em **Iniciar**, aponte para **Todos os Programas** e, em seguida, aponte para **Acessórios**. Clique com o botão direito do mouse em **Prompt de Comando** e, em seguida, clique em **Executar Como Administrador**.

3. Inicialize as variáveis de ambiente de criação de perfil do .NET. Digite o seguinte comando:

    ```cmd
    vsperfclrenv /globaltraceon
    ```

4. Inicialize as variáveis de ambiente TIP. Digite o seguinte comando:

    ```cmd
    vsperfclrenv /globalinteractionon
    ```

5. Reinicie o computador para registrar as variáveis de ambiente.

6. Abra uma janela de prompt de comando com privilégios de administrador.

7. Inicie o criador de perfil. Digite o seguinte comando:

    ```cmd
    vsperfcmd /start:trace /output:MiddleTier_tip.vsp /user:SYSTEM /crosssession 
    ```

8. Se necessário, inicie o serviço.

9. Anexe o criador de perfil ao serviço. Digite o seguinte comando:

    ```cmd
    vsperfcmd /attach:MiddleTier.exe /output:MyService_tip.vsp /user:SYSTEM /crosssession 
    ```

10. Utilize o serviço e colete dados de criação de perfil.

11. Pare o criador de perfil. Digite o seguinte comando:

     `vsperfcmd /detach`

12. Limpe as variáveis de ambiente de criação de perfil do .NET e TIP. Digite o seguinte comando:

    ```cmd
    vsperfclrenv /globaloff
    ```

13. Reinicie o computador para registrar as variáveis de ambiente limpas.

Para obter mais informações, consulte um dos seguintes tópicos:

[Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)

[Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)

## <a name="add-tier-interaction-data-with-vsperfaspnetcmd"></a>Adicionar dados de interação de camadas com VSPerfASPNETCmd

A ferramenta de linha de comando VSPerfASPNETCmd permite criar facilmente o perfil de aplicativos Web do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]. Em comparação com a ferramenta de linha de comando **VSPerfCmd**, as opções são reduzidas, nenhuma variável de ambiente precisa ser definida e não é necessário reinicializar o computador. Esses recursos do VSPerfASPNETCmd deixam extremamente fácil a coleta de dados de interação de camadas.

Para adicionar interação de camadas a dados de criação de perfil coletados usando o VSPerfASPNETCmd, adicione a opção **/TIP** na linha de comando. Por exemplo, use a linha de comando a seguir para coletar dados de interação de um aplicativo Web do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], usando o método de instrumentação:

```cmd
vsperfaspnetcmd /tip /trace http://localhost/MyWebApp
```

Para saber mais sobre o VSPerfASPNETCmd, confira [Criação de perfil do site rápida com VSPerfASPNETCmd](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md).