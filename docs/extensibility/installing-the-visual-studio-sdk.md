---
title: Instalando o SDK do Visual Studio | Microsoft Docs
ms.date: 07/12/2018
ms.topic: overview
ms.assetid: c730edb6-5099-4c16-85a8-08def09f1455
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 31df92b011336320d759461ed16ce2a3c8f61017
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905548"
---
# <a name="install-the-visual-studio-sdk"></a>Instalar o SDK do Visual Studio

O SDK do Visual Studio (Software Development Kit) é um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde.

## <a name="install-the-visual-studio-sdk-as-part-of-a-visual-studio-installation"></a>Instalar o SDK do Visual Studio como parte de uma instalação do Visual Studio

Para incluir o SDK do VS em sua instalação do Visual Studio, instale a carga de trabalho de **desenvolvimento da extensão do Visual Studio** em **outros conjuntos de ferramentas**. Essa carga de trabalho instalará o SDK do Visual Studio e os pré-requisitos necessários. Você pode ajustar a instalação selecionando ou desmarcando componentes da exibição de **Resumo** .

## <a name="install-the-visual-studio-sdk-after-installing-visual-studio"></a>Instalar o SDK do Visual Studio depois de instalar o Visual Studio

Para instalar o SDK do Visual Studio após concluir a instalação do Visual Studio, execute novamente o instalador do Visual Studio e selecione a carga de trabalho de **desenvolvimento da extensão do Visual Studio** .

## <a name="install-the-visual-studio-sdk-from-a-solution"></a>Instalar o SDK do Visual Studio de uma solução

Se você abrir uma solução com um projeto de extensibilidade sem primeiro instalar o SDK do VS, será solicitada uma caixa de diálogo **instalar recurso ausente** para instalar a carga de trabalho de **desenvolvimento da extensão do Visual Studio** :

![Instalar o desenvolvimento da extensão](../extensibility/media/install-extension-development.png "Instalar o desenvolvimento da extensão")

## <a name="install-the-visual-studio-sdk-from-the-command-line"></a>Instalar o SDK do Visual Studio a partir da linha de comando

Como com qualquer carga de trabalho ou componente do Visual Studio, você também pode instalar a carga de trabalho de **desenvolvimento de extensão do Visual Studio** (ID: Microsoft. VisualStudio. Workload. VisualStudioExtension) na linha de comando. Consulte [usar parâmetros de linha de comando para instalar o Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md) para obter detalhes sobre as opções de linha de comando apropriadas e instruções gerais sobre como determinar a carga de trabalho ou os identificadores de componente.

Observe que você deve usar o instalador do Visual Studio que corresponde à sua versão instalada do Visual Studio. Por exemplo, se você tiver Visual Studio Enterprise instalado em seu computador, deverá executar o instalador do Visual Studio Enterprise (*vs_enterprise.exe*).
