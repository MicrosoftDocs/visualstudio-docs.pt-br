---
title: As configurações de propriedade para projetos Web | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], Web applications
- project settings [Visual Studio], debug configurations
- debug builds, project settings
- projects [Visual Studio], debug configurations
- debugging Web applications, project settings
- debug configurations, Web projects
ms.assetid: 8ec5160a-6408-4f47-8d41-f0e20e79a3b9
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: fbe5ab8d863cbf77647bde8b8d7da69d9c4823e5
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53064213"
---
# <a name="property-pages-settings-for-web-projects"></a>Configurações das páginas de propriedade para projetos Web
Você pode alterar as configurações de propriedade de uma configuração de depuração do site na caixa de diálogo **Páginas de Propriedades**, conforme discutido em [Configurações de depuração e versão](../debugger/how-to-set-debug-and-release-configurations.md). As tabelas a seguir mostram como localizar configurações relacionadas ao depurador na caixa de diálogo **Páginas de Propriedades**.  
  
### <a name="configuration-properties-folder-start-options-category"></a>A pasta propriedades de configuração (Opções de Inicialização)  
  
| **Configuração** | **Descrição** |
| - | - |
| **Iniciar ação** | Cabeçalho que agrupa as opções relacionadas à inicialização do aplicativo. |
| **Usar página atual** | Especifica a página atual como o ponto de inicialização para depuração. |
| **Página específica:** | Especifica a página da Web onde você deseja iniciar a depuração. |
| **Iniciar programa externo:** | Especifica o comando para iniciar o programa que você deseja depurar. |
| **Argumentos de linha de comando:** | Especifica argumentos para o comando especificado acima. |
| **Diretório de trabalho:** | Especifica o diretório de trabalho do programa que está sendo depurado. No [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)], o diretório de trabalho é o diretório a partir do qual o aplicativo é iniciado de \bin\debug por padrão. |
| **URL inicial** | Especifica o local do aplicativo Web que você deseja depurar. |
| **Não abra a página. Aguardar solicitação de um aplicativo externo** | Diz para aguardar solicitação de um aplicativo externo. Essa opção não inicia o Internet Explorer ou outro aplicativo. Ela apenas prepara para depuração quando for chamada por um aplicativo. |
| **Servidor** | Cabeçalho que agrupa as opções relacionadas ao servidor a ser usado. |
| **Usar servidor Web padrão** | Informa para usar o servidor Web padrão. |
| **Usar servidor personalizado** | Permite inserir uma URL base para usar como o servidor. |
| **Depuradores** | Cabeçalho que agrupa as opções relacionadas ao tipo de depuração a ser feito. |
| **Depuração do ASP.NET** | Permite a depuração das páginas do servidor escritas para a plataforma de desenvolvimento do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]. Você precisa especificar uma URL em **URL inicial**. |
| **Depuração de código nativo** | Permite depurar chamadas para código Win32 nativo (não gerenciado) a partir do seu aplicativo gerenciado. |
| **Depuração do SQL Server** | Permite depuração de objetos de banco de dados do SQL Server. |
| **Depuração do Silverlight** | Permite depuração de componentes do Silverlight. |
  
## <a name="see-also"></a>Consulte também  
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)