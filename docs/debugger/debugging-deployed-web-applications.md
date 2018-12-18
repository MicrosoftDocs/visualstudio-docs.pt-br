---
title: Depurando aplicativos ASP.NET implantado | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- ASP.NET Web applications
- Web services, debugging
- XML, debugging Web services
- debugging Web services
- ASP.NET, debugging Web applications
- XML Web services, debugging
ms.assetid: b938a91b-be96-416f-83bc-4177e7f3929a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: b8c7c9ea2f280eaf60f4592f149ed2989d862b9b
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31472430"
---
# <a name="debugging-deployed-aspnet-applications"></a>Depurando aplicativos ASP.NET implantado
Para usar o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para depurar um aplicativo implantado, você deverá anexar ao processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] e verificar se o depurador tem acesso aos símbolos para o aplicativo. Você também deve localizar e abrir os arquivos de origem para o aplicativo. Para obter mais informações, consulte [especificar símbolo (. PDB) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md), [como: localizar o nome do processo do ASP.NET](../debugger/how-to-find-the-name-of-the-aspnet-process.md), e [requisitos de sistema](../debugger/aspnet-debugging-system-requirements.md).  

> [!WARNING]
> Se você anexar ao [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] processo de trabalho para depuração e a ocorrência de um ponto de interrupção, todo código gerenciado no processo de trabalho for interrompida. Interromper todo o código gerenciado no processo de trabalho pode causar uma parada de trabalho para todos os usuários no servidor. Antes de depurar em um servidor de produção, considere o impacto potencial no trabalho de produção. 
  
O processo para anexar ao processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] é o mesmo que anexar a qualquer outro processo remoto. Quando você está conectado, se você não tiver o projeto correto aberto, uma caixa de diálogo é exibida quando o aplicativo for interrompido. Essa caixa de diálogo solicita o local dos arquivos de origem para o aplicativo. O nome do arquivo que você especifica na caixa de diálogo deve corresponder ao nome de arquivo especificado nos símbolos de depuração no servidor Web. Para obter mais informações, consulte [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md). Para configurar a depuração remota no IIS, consulte [ASP.NET de depuração remota em um computador remoto do IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md).
 
> [!NOTE]
>  Muitos aplicativos Web do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] fazem referência às DLLs que contêm a lógica de negócios ou outro código útil. Tal referência copia a DLL do computador local para a pasta \bin do diretório virtual do aplicativo da Web quando você implantar seu aplicativo. Quando você estiver depurando, lembre-se de que o aplicativo Web está referenciando essa cópia da DLL e não a cópia em seu computador local. 
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos ASP.NET](../debugger/how-to-enable-debugging-for-aspnet-applications.md)   
 [Como: habilitar a depuração para aplicativos ASP.NET](../debugger/how-to-enable-debugging-for-aspnet-applications.md)   
 [Como: localizar o nome do processo do ASP.NET](../debugger/how-to-find-the-name-of-the-aspnet-process.md)   
 [Especifique o símbolo (. PDB) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)