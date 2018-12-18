---
title: Manutenção diretrizes para aplicativos de Shell de isolados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Studio Shell integrated mode, serviceability
- Shell integrated mode [Visual Studio], serviceability
ms.assetid: 747d1a47-b8b3-4e8b-93c0-768724be48f2
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: a795e5dc71183550e660f8ce7d67f1a41bddbcf4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51726784"
---
# <a name="servicing-guidelines-for-isolated-shell-applications"></a>Diretrizes de serviço para aplicativos de Shell isolado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você distribui um aplicativo de shell isolado do Visual Studio, você deve ser capaz de fornecer atualizações de software para seu aplicativo após a instalação. Para fazer isso, você deve instalar o aplicativo usando um arquivo do Microsoft Installer (MSI). Esse tipo de instalação permite que as atualizações de software fornecidas pela Microsoft para ser redistribuído através da Web, baixar e consumida por seus clientes sem intervenção personalizada.  
  
## <a name="servicing-requirements"></a>Requisitos de serviço  
 Você pode garantir que sua instalação do shell isolado pode permitir que as atualizações, certificando-se de que seu programa de instalação atende aos critérios de três a seguir.  
  
### <a name="redistribute-by-using-an-msi"></a>Redistribuir usando um MSI  
 Você deve usar um MSI para redistribuir o seu aplicativo, porque um MSI preserva a identidade do produto e garante que o aplicativo tem um local físico no computador cliente. Módulos de mesclagem (arquivos. msm) não fornecem essas garantias e não devem ser usados.  
  
### <a name="accounting-for-custom-actions"></a>Estatísticas para ações personalizadas  
 Ações personalizadas são diretivas de instalação não padrão em um programa de instalação. Ações personalizadas alteram parâmetros, como locais de arquivos, configurações do registro, as configurações do usuário ou outros itens de instalação. Ações personalizadas podem manipular os dados no momento da instalação.  
  
 Quando você usa ações personalizadas em um programa de instalação, você deve garantir que todas as ações personalizadas durante a instalação devem ter uma ação personalizada correspondente para desfazer a ação quando o usuário desinstala o aplicativo. Se seu programa de instalação falha para fornecer correspondente desinstalar ação personalizada, removendo o aplicativo sairá parcialmente instalado.  
  
-   Uma ação personalizada que se baseia em uma versão específica de um arquivo ou hash valores falhará quando as atualizações de software, alterar essas versões ou valores de hash. Nesse caso, a ação personalizada deve atualizar manualmente esses valores. Um problema adicional ocorrerá se as versões de um arquivo ou hash valores são compartilhadas entre versões do produto. Evite esta dependência sempre que possível.  
  
### <a name="accounting-for-shared-files"></a>Estatísticas para arquivos compartilhados  
 Arquivos compartilhados têm os mesmos nomes e são instalados no mesmo local por vários produtos. Esses produtos podem diferir em versão, unidade de manter de estoque (SKU) ou ambos, e os produtos podem coexistir em um determinado computador. No entanto, os arquivos compartilhados criar problemas de manutenção por vários motivos:  
  
-   Atualizar arquivos compartilhados pode causar problemas de compatibilidade de aplicativos, porque uma atualização para um aplicativo pode alterar a versão de um arquivo usado por um segundo aplicativo que não foi atualizado. Instaladores para produtos que compartilham arquivos de contagem de referências para os arquivos compartilhados. Portanto, a desinstalação de um produto não afeta arquivos compartilhados, além de diminuir a contagem de instâncias instaladas.  
  
-   O instalador de Quick Fix Engineering (QFE) será revertido para versões de arquivos para as versões dos produtos que o instalador QFE atendido. Esse processo potencialmente interrompe um aplicativo que tinha entregue a um arquivo compartilhado atualizado.

