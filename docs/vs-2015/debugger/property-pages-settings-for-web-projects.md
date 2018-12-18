---
title: As configurações para projetos da Web de páginas de propriedade | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], Web applications
- project settings [Visual Studio], debug configurations
- debug builds, project settings
- projects [Visual Studio], debug configurations
- debugging Web applications, project settings
- debug configurations, Web projects
ms.assetid: 8ec5160a-6408-4f47-8d41-f0e20e79a3b9
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4aef37bb7f6ac6b5b11c1d5a1ea80f12fae288ec
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51777858"
---
# <a name="property-pages-settings-for-web-projects"></a>Configurações das páginas de propriedade para projetos Web
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode alterar as configurações de propriedade para uma configuração de depuração no site da web do **páginas de propriedades** caixa de diálogo, conforme discutido na [Debug and Release Configurations](../debugger/how-to-set-debug-and-release-configurations.md). As tabelas a seguir mostram onde localizar configurações relacionadas ao depurador na **páginas de propriedade** caixa de diálogo.  
  
### <a name="configuration-properties-folder-start-options-category"></a>A pasta propriedades de configuração (Opções de Inicialização)  
  
|**Configuração**|**Descrição**|  
|-----------------|---------------------|  
|**Iniciar ação**|Cabeçalho que agrupa as opções relacionadas à inicialização do aplicativo.|  
|**Use a página atual**|Especifica a página atual como o ponto de inicialização para depuração.|  
|**Página específica:**|Especifica a página da Web onde você deseja iniciar a depuração.|  
|**Inicie programa externo:**|Especifica o comando para iniciar o programa que você deseja depurar.|  
|**Argumentos de linha de comando:**|Especifica argumentos para o comando especificado acima.|  
|**Diretório de trabalho:**|Especifica o diretório de trabalho do programa que está sendo depurado. No [!INCLUDE[csprcs](../includes/csprcs-md.md)], o diretório de trabalho é o diretório a partir do qual o aplicativo é iniciado de \bin\debug por padrão.|  
|**Iniciar URL**|Especifica o local do aplicativo Web que você deseja depurar.|  
|**Não abra a página. Aguarde até que uma solicitação de um aplicativo externo**|Diz para aguardar solicitação de um aplicativo externo. Essa opção não inicia o Internet Explorer ou outro aplicativo. Ela apenas prepara para depuração quando for chamada por um aplicativo.|  
|**Servidor**|Cabeçalho que agrupa as opções relacionadas ao servidor a ser usado.|  
|**Usar servidor Web padrão**|Informa para usar o servidor Web padrão.|  
|**Usar servidor personalizado**|Permite inserir uma URL base para usar como o servidor.|  
|**Depuradores**|Cabeçalho que agrupa as opções relacionadas ao tipo de depuração a ser feito.|  
|**Depuração do ASP.NET**|Permite a depuração das páginas do servidor escritas para a plataforma de desenvolvimento do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]. Você deve especificar uma URL no **iniciar URL**.|  
|**Depuração de código nativo**|Permite depurar chamadas para código Win32 nativo (não gerenciado) a partir do seu aplicativo gerenciado.|  
|**Depuração do SQL Server**|Permite depuração de objetos de banco de dados do SQL Server.|  
|**Depuração do Silverlight**|Permite depuração de componentes do Silverlight.|  
  
## <a name="see-also"></a>Consulte também  
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)



