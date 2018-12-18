---
title: Alterações necessárias para executar projetos do Office migrados para o .NET Framework 4 ou o .NET Framework 4.5
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], migrating to .NET Framework 4
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 78a46fbffdbf849ab9f9584b72c520d5aa1d3624
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50670787"
---
# <a name="required-changes-to-run-office-projects-that-you-migrate-to-the-net-framework-4-or-the-net-framework-45"></a>Alterações necessárias para executar projetos do Office migrados para o .NET Framework 4 ou o .NET Framework 4.5
  Se a estrutura de destino de um projeto do Office será alterada para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior de uma versão anterior do .NET Framework, você deve executar as seguintes tarefas para garantir que a solução pode ser executado no computador de desenvolvimento e nos computadores dos usuários finais:  
  
- Remover o <xref:System.Security.SecurityTransparentAttribute> do projeto se tiver atualizado do Visual Studio 2008.  
  
- Executar uma **Clean** comando no Visual Studio para poder executar ou depurar o projeto no computador de desenvolvimento.  
  
- Atualize o pré-requisito para o projeto do .NET Framework.  
  
- Os usuários finais também deverá reinstalar a solução se tiver implantado usando o ClickOnce antes de alterar a estrutura de destino.  
  
  Para obter mais informações sobre cada uma dessas tarefas, consulte as seções correspondentes abaixo.  
  
## <a name="remove-the-securitytransparent-attribute-from-projects-that-you-upgrade-from-visual-studio-2008"></a>Remova o atributo de SecurityTransparent dos projetos que você atualizar do Visual Studio 2008  
 Se você atualizar um projeto do Office do Visual Studio 2008 e a estrutura de destino do projeto muda posteriormente para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, você deve remover o <xref:System.Security.SecurityTransparentAttribute> do projeto. Visual Studio não remove automaticamente esse atributo para você. Se você não remover esse atributo, você receberá uma mensagem de erro quando você compila o projeto.  
  
 Para obter mais informações sobre as condições em que o Visual Studio pode alterar a estrutura de destino de um projeto atualizado para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)], consulte [atualizar e migrar soluções do Office](../vsto/upgrading-and-migrating-office-solutions.md).  
  
#### <a name="to-remove-the-securitytransparentattribute"></a>Para remover o SecurityTransparentAttribute  
  
1.  Com o projeto aberto no Visual Studio, abra **Gerenciador de soluções**.  
  
2.  Sob o **propriedades** nó (para c#) ou o **My Project** nó (para Visual Basic), clique duas vezes no arquivo AssemblyInfo código para abri-lo no editor de códigos.  
  
    > [!NOTE]  
    >  Em projetos do Visual Basic, você deve clicar o **Show All Files** botão na **Gerenciador de soluções** para ver o arquivo de código de AssemblyInfo.  
  
3.  Localize o <xref:System.Security.SecurityTransparentAttribute> e removê-lo a partir do arquivo ou comentá-lo.  
  
    ```vb  
    <Assembly: SecurityTransparent()>  
    ```  
  
    ```csharp  
    [assembly: SecurityTransparent()]  
    ```  
  
## <a name="perform-the-clean-command-to-debug-or-run-a-project-on-the-development-computer"></a>Execute o comando limpo para depurar ou executar um projeto no computador de desenvolvimento  
 Se um projeto do Office foi criado antes que a estrutura de destino do projeto é alterada para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, você deve executar um **Clean** de comando e, em seguida, recompile o projeto depois que a estrutura de destino for alterada. Se não executar uma **Clean** de comando, você receberá um <xref:System.Runtime.InteropServices.COMException> quando você tenta depurar ou executar o projeto redirecionado.  
  
 Para obter mais informações sobre o **Clean** de comando, consulte [soluções do Office compilar](../vsto/building-office-solutions.md).  
  
## <a name="update-the-prerequisites-for-deployment"></a>Atualizar os pré-requisitos para implantação  
 Quando você redirecionar um projeto do Office [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, você também deve atualizar o pré-requisito do .NET Framework correspondente na **pré-requisitos** caixa de diálogo. Caso contrário, a implantação do ClickOnce ou o projeto do InstallShield Limited Edition verifica e instala uma versão anterior do .NET Framework.  
  
 Para obter mais informações sobre como atualizar os pré-requisitos para implantação para computadores de usuários finais, consulte [como: instalar pré-requisitos em computadores de usuário final para executar soluções do Office](https://msdn.microsoft.com/74dd2c52-838f-4abf-b2b4-4d7b0c2a0a98).  
  
## <a name="reinstall-solutions-on-end-user-computers"></a>Reinstalar as soluções em computadores de usuário final  
 Se você usa o ClickOnce para implantar uma solução do Office que tem como alvo o .NET Framework 3.5 e, em seguida, redirecionar o projeto para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, os usuários finais deve desinstalar a solução e, em seguida, reinstalar a solução depois que você publicar novamente. Se você publicar novamente a solução redirecionada e a solução é atualizada nos computadores dos usuários finais, os usuários finais receberão um <xref:System.Runtime.InteropServices.COMException> quando executarem a solução atualizada.  
  
## <a name="see-also"></a>Consulte também  
 [Migrar soluções do Office para o .NET Framework 4 ou posterior](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)  
  
  