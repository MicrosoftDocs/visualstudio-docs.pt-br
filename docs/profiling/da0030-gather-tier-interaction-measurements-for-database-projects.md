---
title: DA0030-coletar medidas de interação de camada para projetos de banco de dados | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.DA0030
- vs.performance.rules.DA0030
- vs.performance.30
ms.assetid: 42b2f69d-0cfa-4854-82c4-589c3d8b4557
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 47ac30d4a1df36e72b8b12fa9aefb1b36aed6204
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544593"
---
# <a name="da0030-gather-tier-interaction-measurements-for-database-projects"></a>DA0030: coletar medidas de interação de camada para projetos de banco de dados

|Item|Valor|
|-|-|
|ID de regra|DA0030|
|Categoria|Uso das ferramentas de criação de perfil|
|Método de criação de perfil|amostragem|
|Mensagem|A coleta de medições de interação para aplicativos de várias camadas ajuda você a entender os padrões de uso do banco de dados e atrasos de acesso a dados de chave. Tente criar o perfil do aplicativo novamente com a opção Criação de Perfil de Interação de Camada habilitada.|
|Tipo de regra|Informações|

## <a name="cause"></a>Causa
 Chamadas a métodos <xref:System.Data> são uma proporção significativa dos dados de criação de perfil e não foram coletados dados de interação de camada na execução de criação de perfil. Considere a criação de perfil novamente e a adição de dados de interação de camada.

## <a name="rule-description"></a>Descrição da regra
 Essa regra é acionada sempre que há uma atividade significativa nas funções que residem nos namespaces System.Data, incluindo <xref:System.Data.Linq><xref:System.Data.Linq>.

 Aplicativos de várias camadas usam serviços em camadas para suas camadas de apresentação e de dados. Geralmente, a camada de dados é um processo separado que executa um sistema de gerenciamento de banco de dados como o Microsoft SQL Server. A camada de dados ainda pode estar em execução em um computador separado do restante do aplicativo. Os perfis de amostragem fornecem uma análise mínima das funções e dos serviços executados fora do processo ou remotamente.

 As ferramentas de criação de perfil podem coletar informações de tempo para aplicativos de várias camadas que interagem com uma camada de dados do Microsoft SQL Server usando chamadas assíncronas a serviços do ADO.NET. É necessário habilitar explicitamente a Criação de Perfil de Interação de Camada. Ela não é ativada por padrão.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Essa regra se destina apenas a fins informativos e pode não exigir ação corretiva.

 Para obter informações sobre como adicionar dados de interação de camada a dados de criação de perfil por meio do IDE do Visual Studio, confira [Coletar dados de interação de camada](../profiling/collecting-tier-interaction-data.md). Para obter informações sobre como adicionar dados de interação de camada por meio da linha de comando, confira [Coletar dados de interação de camada](../profiling/adding-tier-interaction-data-from-the-command-line.md).
