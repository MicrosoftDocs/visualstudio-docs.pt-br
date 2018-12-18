---
title: Instalar o SDK do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2018
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: c730edb6-5099-4c16-85a8-08def09f1455
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8dceab38f543c58997092559bf9a840806e9b013
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39498581"
---
# <a name="install-the-visual-studio-sdk"></a>Instalar o SDK do Visual Studio

O Visual Studio SDK (Software Development Kit) é um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde.  
  
## <a name="install-the-visual-studio-sdk-as-part-of-a-visual-studio-installation"></a>Instalar o SDK do Visual Studio como parte de uma instalação do Visual Studio

Para incluir o SDK do VS em sua instalação do Visual Studio, instale o **desenvolvimento de extensões do Visual Studio** carga de trabalho sob **outros conjuntos de ferramentas**. Essa carga de trabalho vai instalar o SDK do Visual Studio e os pré-requisitos necessários. Você pode ajustar a instalação selecionando ou desmarcando componentes a partir de **resumo** modo de exibição.
  
## <a name="install-the-visual-studio-sdk-after-installing-visual-studio"></a>Instalar o SDK do Visual Studio depois de instalar o Visual Studio

Para instalar o SDK do Visual Studio depois de concluir a instalação do Visual Studio, execute novamente o instalador do Visual Studio e selecione o **desenvolvimento de extensões do Visual Studio** carga de trabalho.  
  
## <a name="install-the-visual-studio-sdk-from-a-solution"></a>Instalar o SDK do Visual Studio de uma solução

Se você abrir uma solução com um projeto de extensibilidade sem primeiro instalar o SDK do VS, você será solicitado por um **instalar o recurso ausente** caixa de diálogo para instalar o **desenvolvimento de extensões do Visual Studio** carga de trabalho:

![Instalar o desenvolvimento de extensão](../extensibility/media/install-extension-development.png "instalar o desenvolvimento de extensão")  
  
## <a name="install-the-visual-studio-sdk-from-the-command-line"></a>Instalar o SDK do Visual Studio na linha de comando

Como com qualquer componente ou carga de trabalho do Visual Studio, você também pode instalar o **desenvolvimento de extensões do Visual Studio** carga de trabalho (ID: Microsoft.VisualStudio.Workload.VisualStudioExtension) na linha de comando. Ver [usar parâmetros de linha de comando para instalar o Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md) para obter detalhes sobre as opções de linha de comando apropriadas e instruções gerais sobre como determinar os identificadores de componente ou carga de trabalho.
  
Observe que você deve usar o instalador do Visual Studio que corresponde à sua versão instalada do Visual Studio. Por exemplo, se você tiver o Visual Studio Enterprise instalado em seu computador, você deve executar o instalador do Visual Studio Enterprise (*vs_enterprise.exe*).