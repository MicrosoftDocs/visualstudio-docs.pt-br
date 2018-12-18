---
title: Página Publicar, Designer de Projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.Dialog.PropertyPage
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Project Designer, Publish page
- Publish page in Project Designer
ms.assetid: 153527c6-8b95-4003-8e8e-03a489d0a629
caps.latest.revision: 37
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 1dcd6660ff431bee76fb7f595ed243104136684d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49277952"
---
# <a name="publish-page-project-designer"></a>Página de Publicação, Designer de Projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
A página **Publicar** do **Designer de Projeto** é usada para configurar as propriedades de implantação do ClickOnce.  
  
 Para acessar a página **Publicar**, selecione um nó do projeto no **Gerenciador de Soluções** e, em seguida, no menu **Projeto**, clique em **Propriedades**. Quando o **Designer de Projeto** for exibido, clique na guia **Publicar**.  
  
> [!NOTE]
>  Algumas das propriedades do ClickOnce descritas aqui também podem ser definidas no **PublishWizard**, disponível no menu **Build** ou clicando no botão **PublishWizard** nesta página.  
  
## <a name="uielement-list"></a>Lista UIElement  
 **Local da Pasta de Publicação**  
 Especifica o local em que o aplicativo é publicado. Pode ser um caminho de unidade (`C:\deploy\myapplication`), um compartilhamento de arquivos (`\\server\myapplication`), um servidor FTP (`ftp://ftp.microsoft.com/myapplication`) ou um site da Web (`http://www.microsoft.com/myapplication`). Observe que o texto deve estar presente na caixa **Local de Publicação** para o botão de procurar (**...** ) funcionar.  
  
 Por padrão, o local de publicação será `http://localhost/<projectname>/` se você tiver o IIS instalado, ou o diretório `publish\` se você não tiver o IIS instalado. Se o computador estiver executando o Windows Vista, o padrão será sempre o diretório `publish\`, independentemente de você ter o IIS instalado.  
  
 **URL da Pasta de Instalação**  
 Opcional. Especifica um site que os usuários acessam para instalar o aplicativo. Isso é necessário apenas quando ele difere do **Local de Publicação**, por exemplo, quando o aplicativo for publicado em um servidor de preparo.  
  
 **Configurações e Modo de Instalação**  
 Determina se o aplicativo é executado diretamente do **Local de Publicação** (quando **O aplicativo está disponível somente online** está selecionado) ou é instalado e adicionado ao menu **Iniciar** e ao item **Adicionar ou Remover Programas** no **Painel de Controle** (quando **O aplicativo está disponível também offline** é selecionado).  
  
 Para Aplicativos do Navegador da Web WPF, a opção **O aplicativo está disponível também offline** está desabilitada, pois esses aplicativos estão disponíveis somente online.  
  
 **Arquivos de Aplicativo**  
 Abre a [Caixa de Diálogo de Arquivos do Aplicativo](http://msdn.microsoft.com/en-us/b06dff3a-b87a-4caf-996b-7a4acf8137a8), que é usada para especificar como e o local em que os arquivos individuais são instalados.  
  
 **Pré-requisitos**  
 Abre a [Caixa de Diálogo de Pré-Requisitos](../../ide/reference/prerequisites-dialog-box.md), que é usada para especificar os componentes de pré-requisito, como o .NET Framework, a serem instalados junto com o aplicativo.  
  
 **Atualizações**  
 Abre a [Caixa de Diálogo de Atualizações do Aplicativo](http://msdn.microsoft.com/en-us/8eca8743-8e68-4d04-bfd5-4dc0a9b2934f), que é usada para especificar o comportamento da atualização para o aplicativo. Não disponível quando **O aplicativo está disponível apenas online** está selecionado.  
  
 **Opções**  
 Abre a [Caixa de Diálogo Opções de Publicação](http://msdn.microsoft.com/en-us/fd9baa1b-7311-4f9e-8ffb-ae50cf110592), que é usada para especificar mais opções de publicação avançadas.  
  
 **Versão da Publicação**  
 Define o número de versão da publicação para o aplicativo; quando o número de versão é alterado, o aplicativo é publicado como uma atualização. Cada parte da versão de publicação (**Principal**, **Secundária**, **Build**, **Revisão**) pode ter um valor máximo de 65355 (<xref:System.UInt16.MaxValue>), o máximo permitido pelo <xref:System.Version>.  
  
 Ao instalar mais de uma versão de um aplicativo usando o ClickOnce, a instalação moverá as versões anteriores do aplicativo para uma pasta chamada Arquivo, no local de publicação especificado. O arquivamento de versões anteriores dessa maneira mantém o diretório de instalação livre de pastas da versão anterior.  
  
 **Incrementar revisão automaticamente a cada publicação**  
 Opcional. Quando essa opção é selecionada (padrão), a parte de **Revisão** do número de versão de publicação é incrementada em uma unidade toda vez que o aplicativo é publicado. Isso faz o aplicativo ser publicado como uma atualização.  
  
 **Assistente de Publicação**  
 Abre o [Assistente de Publicação](http://msdn.microsoft.com/en-us/fc6abebd-13d6-48e4-a567-fbc52dad0872). Concluir o Assistente de Publicação tem o mesmo efeito que executar o comando **Publicar** no menu **Build**.  
  
 **Publicar Agora**  
 Publica o aplicativo usando as configurações atuais. Equivalente ao botão **Concluir** no **PublishWizard**.  
  
## <a name="see-also"></a>Consulte também  
 [Publicando aplicativos ClickOnce](../../deployment/publishing-clickonce-applications.md)   
 [Como publicar um Aplicativo ClickOnce usando o Assistente de Publicação](../../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)   
 [Como especificar o local em que o Visual Studio copiará os arquivos](../../deployment/how-to-specify-where-visual-studio-copies-the-files.md)   
 [Como especificar o local do qual os usuários finais instalarão](../../deployment/how-to-specify-the-location-where-end-users-will-install-from.md)   
 [Como especificar um link para suporte técnico](../../deployment/how-to-specify-a-link-for-technical-support.md)   
 [Como especificar o modo de instalação offline ou online do ClickOnce](../../deployment/how-to-specify-the-clickonce-offline-or-online-install-mode.md)   
 [Como habilitar o AutoStart para instalações por CD](../../deployment/how-to-enable-autostart-for-cd-installations.md)   
 [Como definir a versão da publicação do ClickOnce](../../deployment/how-to-set-the-clickonce-publish-version.md)   
 [Como incrementar automaticamente a versão de publicação do ClickOnce](../../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)   
 [Como especificar os arquivos a serem publicados pelo ClickOnce](../../deployment/how-to-specify-which-files-are-published-by-clickonce.md)   
 [Como instalar pré-requisitos com um aplicativo ClickOnce](../../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)   
 [Como gerenciar atualizações para um aplicativo ClickOnce](../../deployment/how-to-manage-updates-for-a-clickonce-application.md)   
 [Como alterar o idioma de publicação para um aplicativo ClickOnce](../../deployment/how-to-change-the-publish-language-for-a-clickonce-application.md)   
 [Como especificar um nome no menu Iniciar para um aplicativo ClickOnce](../../deployment/how-to-specify-a-start-menu-name-for-a-clickonce-application.md)   
 [Como especificar uma página de publicação para um aplicativo ClickOnce](../../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)   
 [Segurança e implantação do ClickOnce](../../deployment/clickonce-security-and-deployment.md)



