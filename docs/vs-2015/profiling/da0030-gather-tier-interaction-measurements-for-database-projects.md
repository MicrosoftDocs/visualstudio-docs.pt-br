---
title: 'DA0030: coletar medições de interação de camada para projetos de banco de dados | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.performance.DA0030
- vs.performance.rules.DA0030
- vs.performance.30
ms.assetid: 42b2f69d-0cfa-4854-82c4-589c3d8b4557
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 16d6275074b3cae6b186fe9bb113e32c33e284af
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51796747"
---
# <a name="da0030-gather-tier-interaction-measurements-for-database-projects"></a>DA0030: coletar medições de interação de camada para projetos de banco de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Id da regra | DA0030 |  
| Categoria | Uso das ferramentas de criação de perfil |  
| Método de criação de perfil | Amostragem |  
| Mensagem | Coleta de medições de interação para aplicativos de várias camadas ajudam você a compreender os padrões de uso de banco de dados e os dados importantes acessará atrasos. Tente criar o perfil de aplicativo novamente com a opção de criação de perfil de interação de camadas habilitada. |  
| Tipo de regra | Informações |  
  
## <a name="cause"></a>Causa  
 Chamadas a métodos <xref:System.Data> são uma proporção significativa dos dados de criação de perfil e não foram coletados dados de interação de camada na execução de criação de perfil. Considere a criação de perfil novamente e a adição de dados de interação de camada.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Essa regra é acionada sempre que há uma atividade significativa nas funções que residem nos namespaces System.Data, incluindo <xref:System.Data.Linq><xref:System.Data.Linq>.  
  
 Aplicativos de várias camadas usam serviços em camadas para suas camadas de apresentação e de dados. Geralmente, a camada de dados é um processo separado que executa um sistema de gerenciamento de banco de dados como o Microsoft SQL Server. A camada de dados ainda pode estar em execução em um computador separado do restante do aplicativo. Os perfis de amostragem fornecem uma análise mínima das funções e dos serviços executados fora do processo ou remotamente.  
  
 As ferramentas de criação de perfil podem coletar informações de tempo para aplicativos de várias camadas que interagem com uma camada de dados do Microsoft SQL Server usando chamadas assíncronas a serviços do ADO.NET. É necessário habilitar explicitamente a Criação de Perfil de Interação de Camada. Ela não é ativada por padrão.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Essa regra se destina apenas a fins informativos e pode não exigir ação corretiva.  
  
 Para obter informações sobre como adicionar dados de interação de camada a dados de criação de perfil por meio da IDE do Visual Studio, consulte [Coletando dados de interação de camada](../profiling/collecting-tier-interaction-data.md). Para obter informações sobre como adicionar dados de interação de camada por meio da linha de comando, consulte [Coletando dados de interação de camada](../profiling/adding-tier-interaction-data-from-the-command-line.md).



