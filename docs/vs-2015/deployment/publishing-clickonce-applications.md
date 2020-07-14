---
title: Publicando aplicativos ClickOnce | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.Dialog.Options
- Microsoft.VisualStudio.Publish.ClickOnceProvider.PublishWizard.Help
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, publishing
- ClickOnce applications, publishing
- applications [Visual Studio], ClickOnce deployment
- deploying applications [ClickOnce], publishing ClickOnce applications
ms.assetid: eb6dfe79-f54c-4331-8e36-073688e70973
caps.latest.revision: 24
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 209aac56f4648554ce619cbe31cef19a8ab1fed7
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531788"
---
# <a name="publishing-clickonce-applications"></a>Publicando aplicativos ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao publicar um aplicativo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] pela primeira vez, as propriedades de publicação podem ser definidas usando o Assistente de Publicação. Apenas algumas das propriedades estão disponíveis no assistente; todas as outras propriedades são definidas como seus valores padrão.  
  
 Alterações subsequentes na publicação de propriedades são feitas na página **Publicação** no **Designer de Projeto**.  
  
## <a name="publish-wizard"></a>Assistente de Publicação  
 Você pode usar o Assistente de Publicação para definir as configurações básicas para publicar o aplicativo. Isso inclui as seguintes propriedades de publicação:  
  
- Local da Pasta de Publicação - onde o Visual Studio copiará os arquivos (computador local, compartilhamento de arquivos de rede, servidor FTP ou site)  
  
- Local da Pasta de Instalação - por meio do qual os usuários finais instalarão (compartilhamento de arquivos de rede, servidor FTP, site, CD/DVD)  
  
- Disponibilidade Offline ou Online - se os usuários finais podem acessar o aplicativo com ou sem uma conexão de rede  
  
- Frequência de atualização - com que frequência o aplicativo verifica se há novas atualizações.  
  
  Para obter mais informações, consulte [como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).  
  
## <a name="publish-page"></a>Página Publicação  
 A página **Publicar** do **Designer de Projeto** é usada para configurar as propriedades de implantação do ClickOnce. A tabela a seguir relaciona tópicos  
  
|Title|Descrição|  
|-----------|-----------------|  
|[Como especificar onde o Visual Studio copia os arquivos](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)|Descreve como definir onde o Visual Studio coloca os arquivos de aplicativo e os manifestos.|  
|[Como especificar o local para onde os usuários finais serão instalados](../deployment/how-to-specify-the-location-where-end-users-will-install-from.md)|Descreve como definir o local onde os usuários irão baixar e instalar o aplicativo.|  
|[Como especificar o modo de instalação do ClickOnce offline ou online](../deployment/how-to-specify-the-clickonce-offline-or-online-install-mode.md)|Descreve como definir se o aplicativo estará disponível offline ou online.|  
|[Como: definir a versão de publicação do ClickOnce](../deployment/how-to-set-the-clickonce-publish-version.md)|Descreve como configurar a propriedade **Publicar Versão do ClickOnce**, que determina se o aplicativo que você está publicando será ou não tratado como uma atualização.|  
|[Como incrementar a versão da publicação do ClickOnce automaticamente](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)|Descreve como incrementar automaticamente o número de revisão de **PublishVersion** toda vez que você publicar o aplicativo.|  
  
 Para obter mais informações, consulte [Publicar página, designer de projeto](../ide/reference/publish-page-project-designer.md)  
  
### <a name="application-files-dialog-box"></a>Caixa de diálogo Arquivos do Aplicativo  
 Essa caixa de diálogo permite que você especifique como os arquivos em seu projeto são categorizados para publicação, download dinâmico e atualização. Ela contém uma grade que lista os arquivos de projeto que não são excluídos por padrão, ou que têm um grupo de download.  
  
 Para excluir arquivos, marcar arquivos como arquivos de dados ou pré-requisitos e criar grupos de arquivos para instalação condicional na interface do usuário do Visual Studio, consulte [como especificar quais arquivos são publicados pelo ClickOnce](../deployment/how-to-specify-which-files-are-published-by-clickonce.md). Você também pode marcar os arquivos de dados usando o Mage.exe. Para obter mais informações, consulte [como: incluir um arquivo de dados em um aplicativo ClickOnce](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md).  
  
### <a name="prerequisites-dialog-box"></a>Caixa de diálogo Pré-requisitos  
 Essa caixa de diálogo especifica quais componentes de pré-requisito estão instalados e também como eles estão instalados. Para obter mais informações, consulte [como: instalar pré-requisitos com um aplicativo ClickOnce](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md) e uma [caixa de diálogo de pré-requisitos](../ide/reference/prerequisites-dialog-box.md).  
  
### <a name="application-updates-dialog-box"></a>Caixa de diálogo Atualizações do Aplicativo  
 Essa caixa de diálogo especifica como a instalação do aplicativo deve verificar se há atualizações. Para obter mais informações, consulte [como: gerenciar atualizações para um aplicativo ClickOnce](../deployment/how-to-manage-updates-for-a-clickonce-application.md).  
  
### <a name="publish-options-dialog-box"></a>Caixa de diálogo Opções de Publicação  
 A caixa de diálogo Opções de Publicação especifica as opções de implantação do aplicativo.  
  
|Title|Descrição|
|-|-|  
|[Como: alterar o idioma de publicação para um aplicativo ClickOnce](../deployment/how-to-change-the-publish-language-for-a-clickonce-application.md)|Descreve como especificar um idioma e uma cultura para coincidir com a versão localizada.|  
|[Como especificar um nome do menu Iniciar para um aplicativo ClickOnce](../deployment/how-to-specify-a-start-menu-name-for-a-clickonce-application.md)|Descreve como alterar o nome de exibição de um aplicativo ClickOnce.|  
|[Como especificar um link para suporte técnico](../deployment/how-to-specify-a-link-for-technical-support.md)|Descreve como configurar a propriedade **URL de Suporte**, que identifica uma página da Web ou um compartilhamento de arquivos que os usuários podem acessar para obter informações sobre o aplicativo.|  
|[Como especificar uma URL de suporte para pré-requisitos individuais em uma implantação do ClickOnce](../deployment/how-to-specify-a-support-url-for-individual-prerequisites-in-a-clickonce-deployment.md)|Demonstração de como alterar manualmente um manifesto de aplicativo para incluir URLs de suporte individual para cada pré-requisito.|  
|[Como especificar uma página de publicação para um aplicativo ClickOnce](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)|Descreve como gerar e publicar uma página da Web padrão (publish.htm) junto com o aplicativo|  
|[Como: personalizar a página da Web padrão do ClickOnce](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)|Descreve como personalizar a página da Web que é gerada automaticamente e publicada com o aplicativo.|  
|[Como habilitar o AutoStart para instalações por CD](../deployment/how-to-enable-autostart-for-cd-installations.md)|Descreve como habilitar a Autoinicialização para que o aplicativo ClickOnce seja iniciado automaticamente quando a mídia for inserida.|  
  
## <a name="related-topics"></a>Tópicos Relacionados  
  
|Title|Descrição|  
|-----------|-----------------|  
|[Como: criar associações de arquivo para um aplicativo ClickOnce](../deployment/how-to-create-file-associations-for-a-clickonce-application.md)|Descreve como adicionar suporte à extensão de nome de arquivo para um aplicativo ClickOnce.|  
|[Como recuperar informações de cadeia de caracteres de consulta em um aplicativo ClickOnce online](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)|Demonstra como recuperar os parâmetros passados na URL usada para executar um aplicativo ClickOnce.|  
|[Como: desabilitar a ativação de URL de aplicativos ClickOnce usando o designer](../deployment/how-to-disable-url-activation-of-clickonce-applications-by-using-the-designer.md)|Descreve como forçar os usuários a iniciar o aplicativo por meio do menu **Iniciar** usando o designer.|  
|[Como desabilitar a ativação de URL de aplicativos ClickOnce](../deployment/how-to-disable-url-activation-of-clickonce-applications.md)|Descreve como forçar usuários a iniciarem o aplicativo do menu **Iniciar**.|  
|[Walkthrough: baixando assemblies sob demanda com a API de implantação do ClickOnce usando o designer](../deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer.md)|Explica como baixar assemblies do aplicativo somente quando eles forem usados pela primeira vez pelo aplicativo usando o designer.|  
|[Passo a passo: baixando assemblies sob demanda com a API de implantação do ClickOnce](../deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api.md)|Explica como baixar assemblies do aplicativo somente quando eles forem usados pela primeira vez pelo aplicativo.|  
|[Instruções passo a passo: baixando assemblies satélite por demanda com a API de implantação do ClickOnce](../deployment/walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api.md)|Descreve como marcar seus assemblies satélites como opcionais e baixar somente o assembly que o computador cliente precisa para suas configurações de cultura.|  
|[Walkthrough: Implantando manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)|Explica como usar os utilitários do .NET Framework para implantar seu aplicativo ClickOnce.|  
|[Walkthrough: Implantando manualmente um aplicativo ClickOnce que não requer nova assinatura e que preserva informações de identidade visual](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required?view=vs-2015)|Explica como usar os utilitários do .NET Framework para implantar seu aplicativo ClickOnce sem assinar novamente os manifestos.|  
|[NIB: como otimizar um aplicativo para um tipo de CPU específico](https://msdn.microsoft.com/294a75d2-4279-4b72-8298-2bea05be907a)|Explica como publicar um processador de 64 bits alterando a propriedade **CPU de destino** ou **Destino de plataforma** no projeto.|  
|[Walkthrough: habilitando um aplicativo ClickOnce para ser executado em várias versões de .NET Framework](https://msdn.microsoft.com/7f4383af-ed87-4853-b4d4-02a3967a5fd9)|Explica como habilitar um aplicativo ClickOnce para instalar e executar em várias versões do .NET Framework.|  
|[Instruções passo a passo: criando um instalador personalizado para um aplicativo ClickOnce](../deployment/walkthrough-creating-a-custom-installer-for-a-clickonce-application.md)|Explica como criar um instalador personalizado para instalar um aplicativo ClickOnce.|  
|[Como: publicar um aplicativo WPF com estilos visuais habilitados](../deployment/how-to-publish-a-wpf-application-with-visual-styles-enabled.md)|Fornece instruções passo a passo para resolver um erro que aparece quando você tentar publicar um aplicativo WPF com estilos visuais habilitados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)   
 [Referência de ClickOnce](../deployment/clickonce-reference.md)
