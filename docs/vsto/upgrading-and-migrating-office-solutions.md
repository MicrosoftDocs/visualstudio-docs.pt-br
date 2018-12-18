---
title: Atualizar e migrar soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], upgrading
- Office projects [Office development in Visual Studio], upgrading
- upgrading applications [Office development in Visual Studio]
- upgrading Office solutions in Visual Studio
- migrating Office solutions in Visual Studio
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 5b86699f11ab59aaf0ef09f5c7ae52d69e41e96c
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671736"
---
# <a name="upgrade-and-migrate-office-solutions"></a>Atualizar e migrar soluções do Office
  Se você tiver um projeto do Microsoft Office que foi criado em uma versão anterior do Visual Studio, você deve atualizar o projeto para usá-lo nas versões atuais do Visual Studio. Para atualizar um projeto do Microsoft Office, abra-o em uma versão do Visual Studio que inclui o Microsoft Office developer tools. Para obter mais informações sobre as versões do Visual Studio que incluem o Microsoft Office developer tools, consulte [configurar um computador para desenvolver soluções do Office](../vsto/configuring-a-computer-to-develop-office-solutions.md).  
  
> [!NOTE]  
>  Interessado em desenvolver soluções que estendem a experiência do Office em toda [várias plataformas](https://dev.office.com/add-in-availability)? Confira a nova [modelo de suplementos do Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Suplementos do Office têm uma superfície pequena em comparação com soluções e suplementos do VSTO, e você pode criá-los usando quase qualquer tecnologia, como HTML5, JavaScript, CSS3 e XML de programação da web.  
  
> [!NOTE]  
>  Visual Studio não pode atualizar projetos de modelo de formulário do InfoPath que foram criados usando versões anteriores do Visual Studio. Não há suporte para esses tipos de projetos na versão atual do Visual Studio.  
  
## <a name="changes-to-upgraded-projects"></a>Alterações em projetos atualizados  
 Quando você atualiza um projeto do Microsoft Office, o Visual Studio modifica o projeto para direcionar os itens a seguir:  
  
-   O Visual Studio 2010 Tools for Office runtime. Para obter mais informações, consulte [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md).  
  
-   As referências de assembly atual.  
  
-   Uma versão do .NET Framework que é compatível com o tipo de projeto (quando você atualiza para o Visual Studio 2013 apenas).  
  
-   Uma versão do Microsoft Office que é compatível com o tipo de projeto (quando você atualiza para o Visual Studio 2013 apenas).  
  
## <a name="assembly-references"></a>Referências de assembly  
 O Visual Studio atualiza as seguintes referências de assembly no projeto:  
  
-   Microsoft Office assemblies de interoperabilidade primários (PIAs).  
  
-   Assemblies no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]. Para obter mais informações sobre esses assemblies, consulte [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md).  
  
-   Versões novas ou atualizadas de assemblies dependentes.  
  
## <a name="targeted-net-framework"></a>.NET Framework de destino  
 Quando você atualiza um projeto do Visual Studio 2013, Visual Studio modifica o projeto para qualquer um de destino a [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] ou o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]. A versão do .NET framework destinada pelo projeto depende de qual versão do Office está instalada em seu computador. Se [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] é instalado, o Visual Studio modifica o projeto tenha como destino o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]. Caso contrário, o Visual Studio modifica o projeto tenha como destino o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)].  
  
> [!NOTE]  
>  Talvez seja necessário executar algumas etapas adicionais para executar uma solução redirecionada em desenvolvimento e os computadores dos usuários finais, e seu projeto não serão mais compilados se usar determinados recursos. Para obter mais informações, consulte [soluções do Office de migrar para o .NET Framework 4 ou posterior](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md).  
  
 Se você destinar a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior em um projeto do Office, você pode usar alguns recursos que não estão disponíveis quando você tem como alvo o .NET Framework 3.5. Para obter mais informações, consulte [Design e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md).  
  
## <a name="targeted-office-application"></a>Aplicativo do Office de destino  
 Quando você atualiza um projeto do Office para Visual Studio 2013, Visual Studio modifica o projeto para direcionar uma versão do Microsoft Office que é compatível com o tipo de projeto, como um projeto de personalização no nível de documento ou projeto de suplemento do VSTO.  
  
 Projetos do Office no Visual Studio 2013 podem direcionar [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] e [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] aplicativos. Visual Studio modifica o projeto para direcionar para a versão mais recente do office que você instalou. Se nenhuma dessas versões do Office estiver instalada, o Visual Studio não atualiza o projeto.  
  
> [!NOTE]  
>  Se você atualizar um projeto de suplemento do VSTO para destino [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] ou posterior, certifique-se de que o `ThisAddIn_Startup` manipulador de eventos do que o suplemento do VSTO não contém código que acessa um documento no aplicativo. Para obter mais informações, consulte [acessa um documento quando inicia o aplicativo do Office](../vsto/programming-vsto-add-ins.md#AccessingDocuments).  
  
 Para personalizações de nível de documento [!INCLUDE[vs_current_short](../sharepoint/includes/vs-current-short-md.md)] converte os documentos em um projeto que têm um formato binário, como documentos que tenham uma *. xls* ou *. doc* extensão, no formato Office Open XML. Para obter mais informações sobre o Open XML, consulte [Introdução às novas extensões de nome de arquivo e o Open XML formatos](https://support.office.com/en-nz/article/Introduction-to-new-file-name-extensions-eca81dcb-5626-4e5b-8362-524d13ae4ec1).  
  
> [!NOTE]  
>  Marcas inteligentes foram preteridas no Excel 2010 e o Word 2010. Portanto, se sua solução usar marcas inteligentes, você deve removê-los antes de testar e depurá-lo no Visual Studio 2013 ou Visual Studio 2015.  
  
## <a name="upgrade-microsoft-office-2003-projects"></a>Atualizar projetos do Microsoft Office 2003  
 Há algumas considerações adicionais para atualizar personalizações em nível de documento e suplementos do VSTO que se destinam a Microsoft Office 2003.  
  
### <a name="document-level-projects"></a>Projetos de nível de documento  
 Se o documento no projeto contém controles dos Windows Forms, você também deve ter o Visual Studio 2005 Tools para Office Second Edition Runtime instalado antes de atualizar o projeto. Se esta versão do tempo de execução não estiver instalado no computador de desenvolvimento antes de atualizar o projeto, o projeto atualizado pode conter a compilação ou erros de tempo de execução. Depois de concluir a atualização do projeto, você pode desinstalar o Visual Studio 2005 Tools para Office Second Edition Runtime do computador de desenvolvimento, se ele não está sendo usado por outras soluções do Office. Esta versão do tempo de execução está disponível como um pacote redistribuível do Microsoft Download Center em [Microsoft Visual Studio 2005 Tools for Office Second Edition Runtime (VSTO 2005 SE) (x86)](http://go.microsoft.com/fwlink/?linkid=49612).  
  
### <a name="vsto-add-in-projects"></a>Projetos de suplemento do VSTO  
 Se o arquivo de solução para seu projeto original incluído um projeto de instalação ou o InstallShield Limited Edition que foi configurado para instalar o suplemento do VSTO, Visual Studio atualiza o projeto, mas não faz outras alterações ao projeto. Se você quiser continuar usando um arquivo do Windows Installer para implantar seu suplemento do VSTO, você deve modificar o projeto de instalação ou o InstallShield Limited Edition para instalar novos pré-requisitos, como o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)], do Visual Studio 2010 Tools for Office Runtime e, opcionalmente, assemblies de interoperabilidade primários referenciados pelo seu suplemento do VSTO. Para obter mais informações, consulte [implantar uma solução do Office usando o Windows Installer](../vsto/deploying-an-office-solution-by-using-windows-installer.md).  
  
 Se você quiser usar o ClickOnce para implantar seu suplemento do VSTO, você pode excluir o projeto de instalação ou o InstallShield Limited Edition inteiramente. Para obter mais informações sobre como implantar Suplementos do VSTO usando o ClickOnce, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como: soluções de atualização do Office](https://msdn.microsoft.com/a269e539-b717-4680-a568-2152b070347e)   
 [Migrar soluções do Office para o .NET Framework 4 ou posterior](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)   
 [Caixa de diálogo de opções de atualização, projeto](../vsto/project-upgrade-options-dialog-box.md)  
  
  