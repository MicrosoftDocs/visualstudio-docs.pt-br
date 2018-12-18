---
title: Solução de problemas de instalação com o Visual Studio 2017
description: Às vezes, as coisas podem dar errado. Se a instalação ou atualização do Visual Studio falhar, esta página poderá ajudar.
ms.date: 08/01/2018
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: troubleshooting
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 556EDD3F-E365-43EE-B3DD-03AA4353F75B
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: db85353830e1d86773a870a410797bfb5c60ccd7
ms.sourcegitcommit: 4708f0ba09b540424efcc344f8438f25432e3d51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2018
ms.locfileid: "44384117"
---
# <a name="troubleshoot-visual-studio-2017-installation-and-upgrade-issues"></a>Solução de problemas de instalação e atualização do Visual Studio 2017

> [!IMPORTANT]
> Está com problema para instalar? Podemos ajudá-lo. Oferecemos um [**chat ao vivo**](https://visualstudio.microsoft.com/vs/support/#talktous) a opção de suporte (apenas em inglês).

Este guia de solução de problemas apresenta instruções passo a passo que resolvem a maioria dos problemas de instalação.

## <a name="how-to-troubleshoot-an-online-installation"></a>Como solucionar problemas de uma instalação offline

As etapas a seguir são otimizadas para uma instalação online típica. Para um problema que afeta uma instalação offline, confira [Como solucionar problemas de uma instalação offline](#how-to-troubleshoot-an-offline-installation).

### <a name="step-1---check-whether-this-problem-is-a-known-issue"></a>Etapa 1: verificar se esse é um problema conhecido

Existem alguns problemas conhecidos com o instalador do Visual Studio que a Microsoft está trabalhando para corrigir. Para saber se há uma solução para o problema, consulte [a seção Problemas Conhecidos das nossas notas de versão](/visualstudio/releasenotes/vs2017-relnotes#-known-issues).

### <a name="step-2---check-with-the-developer-community"></a>Etapa 2: conferir com a comunidade de desenvolvedores

Pesquise em sua mensagem de erro com a [Comunidade de Desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/spaces/8/index.html). Outros membros da comunidade podem ter documentado uma solução para o seu problema.

### <a name="step-3---delete-the-visual-studio-installer-directory-to-fix-upgrade-problems"></a>Etapa 3 - excluir o diretório de instalação do Visual Studio para corrigir problemas de atualização

O bootstrapper de instalação do Visual Studio é um executável leve mínimo que instala o restante do instalador do Visual Studio. A exclusão de arquivos de instalação do Visual Studio e a nova execução do bootstrapper podem resolver algumas falhas de atualização.

> [!NOTE]
> Executar as seguintes ações reinstalará os arquivos do Instalador do Visual Studio e redefinirá os metadados de instalação.

1. Fechar o instalador do Visual Studio.
2. Exclua o diretório de instalação do Visual Studio. Normalmente, o diretório é `C:\Program Files (x86)\Microsoft Visual Studio\Installer`.
3. Execute o bootstrapper de instalação do Visual Studio. Você pode encontrar o bootstrapper na pasta Downloads com um nome de arquivo que segue um padrão `vs_[Visual Studio edition]__*.exe`. Se não encontrar esse aplicativo, você poderá baixar o bootstrapper indo para a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/) e clicando em **Baixar** para sua edição do Visual Studio. Em seguida, execute o arquivo executável para redefinir os metadados de instalação.
4. Tente instalar ou atualizar o Visual Studio. Se o Instalador continuar a falhar, vá para a próxima etapa.

### <a name="step-4---report-a-problem"></a>Etapa 4 - relatar um problema

Em algumas situações, como aquelas relacionadas a arquivos corrompidos, os problemas talvez precisem ser resolvidos caso a caso. Para que possamos ajudá-lo, faça o seguinte:

1. Colete os logs de configuração. Para saber mais detalhes, consulte [Como obter os logs de instalação do Visual Studio](#how-to-get-visual-studio-installation-logs).
2. Abra o instalador do Visual Studio e clique em **Relatar um problema** para abrir a ferramenta de comentários do Visual Studio.
![Você pode pressionar Tab até acessar o botão Fornecer Comentários para abrir a ferramenta de comentários](media/report-a-problem.png)
3. Dê um título ao relatório de problemas e forneça detalhes relevantes. Clique em **Avançar** para ir até a seção **Anexos** e anexar o arquivo de log gerado (normalmente, o arquivo está em `%TEMP%\vslogs.zip`).
4. Clique em **Avançar** para examinar o relatório de problemas e clique em **Enviar**.

### <a name="step-5---run-installcleanupexe-to-remove-installation-files"></a>Etapa 5 – Executar InstallCleanup.exe para remover os arquivos de instalação

Como último recurso, você pode [remover o Visual Studio](remove-visual-studio.md) para remover todos os arquivos de instalação e informações do produto.

1. Siga as instruções em [Remover o Visual Studio](remove-visual-studio.md).
2. Execute novamente o bootstrapper descrito na [Etapa 3 - excluir o diretório do Instalador do Visual Studio para corrigir problemas de atualização](#step-3---delete-the-visual-studio-installer-directory-to-fix-upgrade-problems).
3. Tente instalar ou atualizar o Visual Studio.

### <a name="step-6---contact-us-optional"></a>Etapa 6 – Entrar em contato conosco (opcional)

Se nenhuma das etapas anteriores ajudá-lo a instalar ou a atualizar o Visual Studio, entre em contato conosco usando a nossa opção de suporte por [**chat ao vivo**](https://visualstudio.microsoft.com/vs/support/#talktous) (somente em inglês) para obter mais assistência.

## <a name="how-to-troubleshoot-an-offline-installation"></a>Como solucionar problemas de uma instalação offline

Vejamos uma tabela de problemas conhecidos e algumas soluções alternativas que podem ajudar durante a instalação a partir de um layout local.

| Problema       | Item                   | Solução |
| ----------- | ---------------------- | -------- |
| Os usuários não têm acesso aos arquivos. | permissões (ACLs) | Lembre-se de ajustar as permissões (ACLs) para que elas concedam acesso de Leitura aos outros usuários *antes* de você compartilhar a instalação offline. |
| Falha na instalação de novas cargas de trabalho, novos componentes ou idiomas.  | `--layout`  | Verifique se você tem acesso à Internet se estiver instalando com base em um layout parcial e selecione as cargas de trabalho, os componentes ou idiomas que não foram baixado anteriormente nesse layout parcial. |

## <a name="how-to-get-visual-studio-installation-logs"></a>Como obter os logs de instalação do Visual Studio

Os logs de instalação são necessários para solucionar a maioria dos problemas de instalação. Quando você enviar um problema usando [Relatar um Problema](../ide/how-to-report-a-problem-with-visual-studio-2017.md) no Instalador do Visual Studio, esses logs serão incluídos automaticamente no relatório.

Caso contate o Suporte da Microsoft, talvez você precise fornecer esses logs de configuração usando a [Ferramenta de Coleta de Log do .NET Framework e o Microsoft Visual Studio](https://aka.ms/vscollect). A ferramenta de coleta de log coleta os logs de configuração de todos os componentes instalados pelo Visual Studio 2017, incluindo .NET Framework, SDK do Windows e SQL Server. Ela também coleta informações do computador, um inventário do Windows Installer e as informações de log de eventos do Instalador do Visual Studio, Windows Installer e Restauração do Sistema.

Para coletar os logs:

1. [Baixe a ferramenta](https://aka.ms/vscollect).
2. Abra um prompt de comando administrativo.
3. Execute `Collect.exe` no diretório em que você salvou a ferramenta.
4. Localize o arquivo `vslogs.zip` resultante no diretório `%TEMP%`, por exemplo, `C:\Users\YourName\AppData\Local\Temp\vslogs.zip`.

> [!NOTE]
> A ferramenta deve ser executada na mesma conta de usuário em que a instalação com falha foi executada. Se estiver executando a ferramenta em uma conta de usuário diferente, defina a opção `–user:<name>` para especificar a conta de usuário na qual a instalação com falha foi executada. Execute `Collect.exe -?` em um prompt de comando do administrador para obter informações adicionais de uso e opções.

## <a name="get-live-help"></a>Obter ajuda ao vivo

Se as soluções listadas neste guia de solução de problemas não ajudarem a instalar ou atualizar o Visual Studio, use a nossa opção de suporte por [**chat ao vivo**](https://visualstudio.microsoft.com/vs/support/#talktous) (somente em inglês) para obter mais assistência.

## <a name="see-also"></a>Consulte também

* [Remover o Visual Studio 2017](remove-visual-studio.md)
* [Instalar e usar o Visual Studio e os Serviços do Azure atrás de um firewall ou servidor proxy](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)
* [Ferramentas para detectar e gerenciar instâncias do Visual Studio](tools-for-managing-visual-studio-instances.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
