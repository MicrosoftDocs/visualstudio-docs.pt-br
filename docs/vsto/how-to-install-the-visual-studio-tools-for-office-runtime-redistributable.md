---
title: 'Como: instalar o Visual Studio Tools for Office runtime redistribuível'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office runtime [Office development in Visual Studio]
- installing Office development tools in Visual Studio
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 15e3c1b25d4834808fb17e596fcc7babe7dd969f
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35255844"
---
# <a name="how-to-install-the-visual-studio-tools-for-office-runtime-redistributable"></a>Como: instalar o Visual Studio Tools for Office runtime redistribuível
  O Visual Studio 2010 Tools for Office runtime deve ser instalado em cada computador que executa soluções que são criadas usando as ferramentas de desenvolvedor do Microsoft Office em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. O tempo de execução é instalado automaticamente quando você instala o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]e o Microsoft Office. Para obter mais informações, consulte [ferramentas do Visual Studio para cenários de instalação do Office em tempo de execução](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md).  
  
 Talvez seja necessário que você siga as instruções de instalação manual abaixo nas seguintes situações:  
  
-   Você precisa instalar o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] em um servidor. Por exemplo, você deseja usar o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe para gerenciar soluções de nível de documento em um servidor.  
  
-   Você precisa instalar o tempo de execução em um computador que já tem todos os outros pré-requisitos para soluções do Office instalados.  
  
    > [!NOTE]  
    >  Você deve ser um administrador no computador de desenvolvimento para instalar o .NET Framework e o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)].  
  
## <a name="to-install-the-visual-studio-tools-for-office-runtime"></a>Para instalar o Visual Studio Tools for Office runtime  
  
1.  Instalar o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior.  
  
    -   Para baixar o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)], consulte [Microsoft .NET Framework 4 (instalador da Web)](http://go.microsoft.com/fwlink/?LinkId=178957).  
  
    -   Para baixar o [!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)], consulte [(instalador da Web) do Microsoft .NET Framework 4 Client Profile](http://go.microsoft.com/fwlink/?LinkId=178958).  
  
    -   Para baixar o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)], consulte [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).  
  
2.  Execute *vstor_redist.exe* para instalar o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)].  
  
     Você pode baixar esses arquivos de instalação do [Visual Studio 2010 Tools for Office runtime](http://go.microsoft.com/fwlink/?LinkId=140384). Os pré-requisitos para o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] corresponder os pré-requisitos para o .NET Framework.  
  
     O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]inclui pacotes de idiomas. Se a instalação do Windows é definida como um idioma diferente do inglês, você pode exibir mensagens de tempo de execução no mesmo idioma que você usa para Windows. Da mesma forma, se os usuários finais instalam o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] e, em seguida, executar suas soluções em instalações do Windows que são definidos para um idioma diferente do inglês, mensagens de tempo de execução serão exibidas no mesmo idioma do Windows. Em alguns casos, talvez seja necessário pacotes de idiomas adicionais. Por exemplo, talvez seja necessário pacotes de idiomas adicionais se sua cópia do Windows usa mais de uma configuração de idioma, ou se você alternar para outro idioma depois que você já tiver instalado o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]. Você pode encontrar os pacotes de idiomas em [Microsoft Visual Studio 2010 Tools para o pacote de idiomas do Microsoft Office system (runtime versão 4.0)](http://go.microsoft.com/fwlink/?LinkId=140386).  
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)   
 [Configurar um computador para desenvolver soluções do Office](../vsto/configuring-a-computer-to-develop-office-solutions.md)   
 [Como: configurar um computador para desenvolver soluções do Office](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)   
 [Como: assemblies de interoperabilidade primários do Office de instalação](../vsto/how-to-install-office-primary-interop-assemblies.md)   
 [Gerenciar documentos em um servidor usando a classe ServerDocument](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)  
  
  