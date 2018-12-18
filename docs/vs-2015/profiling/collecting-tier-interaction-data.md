---
title: Coletando dados de interação de camada | Microsoft Docs
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
- vs.performance.property.tierinteraction
helpviewer_keywords:
- Profiling Tools,ADO.NET profiling
- tier interaction profiling method
- Profiling Tools,tier-interaction method
- ADO.NET performance profiling
ms.assetid: 47a944c2-3098-497c-8fc7-e1f43d750bbc
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 31e2d46992b48b987966bac7d7dc68787f4016c2
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51761183"
---
# <a name="collecting-tier-interaction-data"></a>Coletando dados de interação entre camadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A criação de perfil de interação de camadas fornece informações adicionais sobre os tempos de execução de funções de aplicativos de várias camadas que se comunicam com os bancos de dados por meio de serviços do ADO.NET. Os dados são coletados apenas para chamadas de função síncronas.  
  
 **Edições do Visual Studio**  
  
 Os dados de criação de perfil de interação de camada podem ser coletados usando o Visual Studio Ultimate, Visual Studio Premium ou Visual Studio Professional. No entanto, os dados de criação de perfil de interação de camada somente podem ser exibidos no VS Ultimate e VS Premium.  
  
 **Windows 8 e Windows Server 2012**  
  
 Para coletar dados de interação de camada em aplicativos da área de trabalho do Windows 8 e os aplicativos do Windows Server 2012, é necessário usar o método de instrumentação. Não é possível coletar dados de interação de camada para aplicativos da Windows Store. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md). É possível incluir dados de interação de camada em todos os métodos de criação de perfil em outra versão com suporte do Windows.  
  
 **Assistente de desempenho**  
  
 Por causa de um bug no Assistente de desempenho, é necessário adicionar a opção de coleta de dados de interação de camada para uma execução de criação de perfil do Gerenciador de Desempenho. Também é necessário adicionar o projeto, o executável ou o site ao nó de Destino do Gerenciador de Desempenho.  
  
### <a name="to-add-tier-interaction-data-to-a-profiling-run-by-using-the-performance-session-property-pages"></a>Para adicionar dados de interação de camada a uma execução de criação de perfil usando as páginas de propriedades da sessão de desempenho  
  
1.  No Gerenciador de Desempenho, escolha **Propriedades** no menu de contexto.  
  
2.  Selecione a página **Interações de Camada** e marque a caixa de seleção **Habilitar Criação de Perfil de Interação de Camada**.  
  
3.  No Gerenciador de Desempenho, selecione o nó **Destinos** e, em seguida, especifique o projeto, o executável ou o site da Web para o qual você deseja criar o perfil.  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de Interações de Camada](../profiling/tier-interactions-view.md)



