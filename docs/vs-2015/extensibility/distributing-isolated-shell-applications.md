---
title: Distribuição de aplicativos de Shell isolado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c503a985-d67a-4ef8-9123-7744a78f2f17
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 27228131c1e955a394e666ac05f0ddd68c879be0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51758783"
---
# <a name="distributing-isolated-shell-applications"></a>Distribuição de aplicativos de Shell isolado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você deve instalar o Visual Studio e SDK do Visual Studio para criar um aplicativo de shell isolado. Para distribuir o aplicativo para as máquinas de outros usuários ou clientes, você deve incluir um pacote redistribuível especial para o shell isolado.  
  
## <a name="prerequisites-for-distributing-isolated-shell-applications"></a>Pré-requisitos para distribuição de aplicativos de Shell isolado  
  
|Nome|Descrição|  
|----------|-----------------|  
|SDK do Visual Studio|O SDK, você deve ter para desenvolver e testar as extensões de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Você também pode usar o SDK para criar sua própria instância do shell isolado do Visual Studio.<br /><br /> Visual Studio é um pré-requisito para o SDK.|  
|Redistribuível do Shell de isolado do Microsoft Visual Studio|Os pacotes redistribuíveis do que você incluir em seu programa de instalação quando você cria um ambiente de ferramentas no Visual Studio shell isolado. O pacote redistribuível do Shell isolado inclui o .NET Framework 4.5.|  
  
## <a name="creating-an-installation-program-for-the-application"></a>Criando um programa de instalação para o aplicativo  
 Você deve criar um programa de instalação especial para seu aplicativo de shell integrado ou isolado. Para obter mais informações, consulte [instalação de um aplicativo de Shell isolado](../extensibility/installing-an-isolated-shell-application.md).  
  
## <a name="allowing-for-updates-to-your-application"></a>Permitindo que as atualizações do seu aplicativo  
 O programa de instalação deve permitir a possibilidade de que seu aplicativo será atualizado, por atualizações da Microsoft ou por atualizações da sua empresa. Para obter mais informações sobre atualizações, consulte [diretrizes de serviço para aplicativos de Shell isolado](../extensibility/servicing-guidelines-for-isolated-shell-applications.md).

