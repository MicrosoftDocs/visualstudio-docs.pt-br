---
title: Coletando dados de interação de camada | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.property.tierinteraction
helpviewer_keywords:
- Profiling Tools,ADO.NET profiling
- tier interaction profiling method
- Profiling Tools,tier-interaction method
- ADO.NET performance profiling
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 4f7b2a2bb5efd86d052247825a29a06c7f5ad109
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331600"
---
# <a name="collect-tier-interaction-data"></a>Coletar dados de interação de camadas

A criação de perfil de interação de camadas fornece informações adicionais sobre os tempos de execução de funções de aplicativos de várias camadas que se comunicam com os bancos de dados por meio de serviços do ADO.NET. Os dados são coletados apenas para chamadas de função síncronas.

**Edições do Visual Studio**

Os dados de criação de perfil de interação de camadas podem ser coletados usando qualquer edição do Visual Studio. No entanto, os dados de criação de perfil de interação de camadas só podem ser exibidos no Visual Studio Enterprise.

**Windows 8 e Windows Server 2012**

Para coletar dados de interação de camada em aplicativos da área de trabalho do Windows 8 e os aplicativos do Windows Server 2012, é necessário usar o método de instrumentação. Não é possível coletar dados de interação de camada de aplicativos UWP. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md). É possível incluir dados de interação de camada em todos os métodos de criação de perfil em outra versão com suporte do Windows.

**Assistente de Desempenho**

Por causa de um bug no Assistente de desempenho, é necessário adicionar a opção de coleta de dados de interação de camada para uma execução de criação de perfil do Gerenciador de Desempenho. Também é necessário adicionar o projeto, o executável ou o site ao nó de Destino do Gerenciador de Desempenho.

## <a name="to-add-tier-interaction-data-to-a-profiling-run-by-using-the-performance-session-property-pages"></a>Para adicionar dados de interação de camada a uma execução de criação de perfil usando as páginas de propriedades da sessão de desempenho

1. No Gerenciador de Desempenho, escolha **Propriedades** no menu de contexto.

2. Selecione a página **Interações de Camada** e marque a caixa de seleção **Habilitar Criação de Perfil de Interação de Camada**.

3. No Gerenciador de Desempenho, selecione o nó **Destinos** e, em seguida, especifique o projeto, o executável ou o site da Web para o qual você deseja criar o perfil.

## <a name="see-also"></a>Veja também

[Exibição de interações de camada](../profiling/tier-interactions-view.md)
