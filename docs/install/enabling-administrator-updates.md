---
title: Habilitando atualizações do administrador para o Visual Studio com o Microsoft Endpoint Configuration Manager
titleSuffix: ''
description: Saiba mais sobre como implantar atualizações do administrador no Visual Studio.
ms.date: 04/06/2021
ms.custom: ''
ms.topic: overview
ms.assetid: 546fbad6-f12b-49cf-bccc-f2e63e051a18
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: affb5a0c78c1ad1e230c571485385d9f55fc2bec
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307447"
---
# <a name="enabling-administrator-updates-to-visual-studio-with-microsoft-endpoint-configuration-manager"></a>Habilitando atualizações do administrador para o Visual Studio com o Microsoft Endpoint Configuration Manager

O Microsoft Endpoint Configuration Manager (SCCM) pode gerenciar as atualizações de administrador do Visual Studio 2017 e do Visual Studio 2019 usando o fluxo de trabalho do gerenciamento de atualizações de software.

> [!NOTE]
> Para simplificar a documentação, o conteúdo a seguir fará referência aos produtos Visual Studio 2017, Visual Studio 2019 e Visual Studio 2022 coletivamente como "Visual Studio".

Quando a Microsoft publica uma nova atualização do Visual Studio para a CDN (rede de distribuição de conteúdo), a Microsoft publicará simultaneamente um pacote de atualização de administrador correspondente nos servidores de Microsoft Update. Isso permitirá que um administrador distribua a atualização do Visual Studio por meio do muc ( [Catálogo de Microsoft Update](https://www.catalog.update.microsoft.com/Home.aspx) ) ou do [Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus) (WSUS). Configuration Manager pode ser configurado para sincronizar as atualizações do administrador do Visual Studio do catálogo do WSUS no servidor do site e, em seguida, ele pode baixar a atualização e distribuí-la para computadores cliente do Visual Studio em toda a organização. Para obter mais informações sobre quais correções estão presentes em cada versão do Visual Studio, consulte as [notas de versão](/visualstudio/releases/2019/release-notes).

Para distribuir as atualizações do administrador do Visual Studio por meio do Configuration Manager, você precisará executar estas duas etapas iniciais de preparação:
1. Habilite Configuration Manager para receber notificações de atualização do administrador do Visual Studio. 
2. Habilite (ou desabilite) computadores cliente para receber as atualizações do administrador do Visual Studio de Configuration Manager.

Depois de executar essas etapas, você pode usar os recursos de gerenciamento de atualização de software do Configuration Manager para implantar as atualizações do administrador do Visual Studio. Os diferentes tipos e características das atualizações do Visual Studio Administrator são descritos em [aplicando atualizações do administrador](../install/applying-administrator-updates.md), que fornece orientação sobre como e quando elas devem ser distribuídas em toda a sua organização. Para obter mais informações sobre Configuration Manager funcionalidade e opções, consulte [implantar atualizações de software no Microsoft Endpoint Configuration Manager](/mem/configmgr/sum/deploy-use/deploy-software-updates).

## <a name="enable-configuration-manager-to-receive-visual-studio-administrator-update-notifications"></a>Habilitar Configuration Manager para receber notificações de atualização do administrador do Visual Studio

Para habilitar a Configuration Manager para gerenciar as atualizações do administrador do Visual Studio, você precisará de:

* Uma versão licenciada atual do Windows Server que executa o Microsoft Endpoint Configuration Manager (Branch atual) e o Windows Server Update Services (WSUS). Você não pode usar o próprio WSUS para implantar essas atualizações; Ele deve ser usado em conjunto com Configuration Manager.

* O servidor WSUS de nível superior da hierarquia e o servidor do site Configuration Manager de nível superior devem ter acesso às URLs e às portas do Visual Studio listadas aqui: [instalar e usar o Visual Studio e os serviços do Azure atrás de um firewall ou servidor proxy](../install/install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md).  

* O Microsoft Endpoint Configuration Manager deve ser configurado para receber notificações quando os pacotes de atualização do Visual Studio Administrator estiverem disponíveis.  Para fazer isso, use as etapas a seguir e para obter mais informações, consulte [Introduction to software updates in Microsoft Endpoint Configuration Manager](/mem/configmgr/sum/understand/software-updates-introduction).

  1. No console do Configuration Manager, selecione **Administração** (inferior esquerda), selecione configuração do **site** (meio esquerdo), **sites** e selecione o servidor do site.

  2. Na faixa de opções da guia **início** na parte superior, no botão grupo de **configurações** , selecione **configurar componentes do site** e selecione ponto de **atualização de software**.

  3. Na caixa de diálogo **Propriedades do componente de ponto de atualização de software** :

        * Na guia **produtos** , na hierarquia **ferramentas para desenvolvedores, tempos de execução e redistribuíveis** , escolha as versões do Visual Studio que você deseja sincronizar.

        * Na guia **classificações** , certifique-se de que "atualizações de segurança", "pacotes de recursos" e "Atualizações" estão selecionadas.

  4. Em seguida, sincronize as atualizações de software com o servidor do WSUS escolhendo **biblioteca de software** (inferior esquerda) e, em seguida, na faixa de opções da guia **página inicial** na parte superior, selecione o botão **sincronizar atualizações de software** . A sincronização de atualizações de software disponibilizará as atualizações do administrador do Visual Studio visíveis no, e poderá ser implantada a partir do console do Configuration Manager.

## <a name="enable-or-disable-client-machines-ability-to-receive-visual-studio-administrator-updates-from-configuration-manager"></a>Habilitar (ou desabilitar) a capacidade dos computadores cliente de receber atualizações do administrador do Visual Studio do Configuration Manager

Para permitir que um computador cliente aceite atualizações de administrador do Visual Studio, você precisará garantir que o utilitário detector de cliente do Visual Studio esteja instalado corretamente e será necessário definir uma chave do registro para permitir que o cliente Receba atualizações do administrador.  

### <a name="visual-studio-client-detector-utility"></a>Utilitário de detector de cliente do Visual Studio

O [utilitário detector de cliente do Visual Studio](https://support.microsoft.com/help/5001148) deve ser instalado nos computadores cliente para que as atualizações do administrador sejam corretamente reconhecidas e recebidas. Esse utilitário foi incluído com todas as atualizações de produto do Visual Studio 2017 e do Visual Studio 2019 lançadas no ou após 12 de maio de 2020, ela é incluída como um pré-requisito com todas as atualizações de administrador do Visual Studio e também está disponível no [Catálogo de Microsoft Update](https://catalog.update.microsoft.com) para ser instalado de forma independente.

### <a name="encoding-administrator-intent-on-the-client-machines"></a>Codificação da intenção de administrador nos computadores cliente

Os computadores cliente devem ser habilitados para receber atualizações do administrador. Essa etapa é necessária para garantir que as atualizações não sejam desintencionalmente ou desativadas acidentalmente para desconfiar em computadores cliente.

A chave **AdministratorUpdatesEnabled**   foi projetada para o administrador codificar a intenção do administrador. Essa chave pode estar em qualquer um dos locais padrão do Visual Studio, conforme descrito na documentação [definir padrões para implantações corporativas do Visual Studio](/visualstudio/install/set-defaults-for-enterprise-deployments) . O acesso de administrador no computador cliente é necessário para criar e definir o valor dessa chave.

* Para configurar o computador cliente para aceitar atualizações do administrador, defina a chave de REG_DWORD **AdministratorUpdatesEnabled**   como **1**.
* Se a  ****   chave de REG_DWORD AdministratorUpdatesEnabled estiver **ausente ou estiver definida como 0**, as atualizações do administrador serão impedidas de serem aplicadas ao computador cliente.

## <a name="feedback-and-support"></a>Comentários e suporte

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

Você pode usar os seguintes métodos para fornecer comentários sobre as atualizações do administrador do Visual Studio ou os problemas de relatório que afetam as atualizações:

* Consulte as diretrizes [solução de problemas de instalação e atualização do Visual Studio](../install/troubleshooting-installation-issues.md) .
* Faça perguntas à Comunidade na instalação do [Visual Studio Q&um fórum](/answers/topics/vs-setup.html).
* Vá para a [página de suporte do Visual Studio](https://visualstudio.microsoft.com/vs/support/)e verifique se o problema está listado nas perguntas frequentes.  Você também pode selecionar o botão [link de suporte](https://visualstudio.microsoft.com/vs/support/#talktous) para a ajuda do chat.
* [Forneça comentários sobre recursos ou relate um problema](https://aka.ms/vs/wsus/feedback) à equipe do Visual Studio sobre essa experiência de habilitar atualizações do administrador.
* Entre em contato com o gerente técnico de conta da sua organização para a Microsoft.

## <a name="see-also"></a>Confira também

* [Aplicando atualizações do administrador](../install/applying-administrator-updates.md)
* [Guia do administrador do Visual Studio](../install/visual-studio-administrator-guide.md)
* [Ciclo de vida e manutenção do produto Visual Studio](/visualstudio/productinfo/vs-servicing-vs)
* [Notas sobre a versão do Visual Studio 2019](/visualstudio/releases/2019/release-notes)
* [Notas de versão do Visual Studio 2017](/visualstudio/releasenotes/vs2017-relnotes)
* [Instalar o Visual Studio](../install/install-visual-studio.md)
* [Perguntas frequentes do catálogo de Microsoft Update](https://www.catalog.update.microsoft.com/faq.aspx)
* [Documentação do Microsoft Endpoint Configuration Manager (SCCM)](/mem/configmgr)
* [Importar atualizações do catálogo da Microsoft para o Configuration Manager](/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)
* [Documentação do Windows Server Update Services (WSUS)](/windows-server/administration/windows-server-update-services/get-started-windows-server-update-services-wsus)
