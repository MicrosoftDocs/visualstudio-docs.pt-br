---
title: 'DA0001: usar StringBuilder para concatenações | Microsoft Docs'
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
- vs.performance.DA0001
- vs.performance.rules.DAUseStringBuilder
- vs.performance.1
- vs.performance.rules.DA0001
ms.assetid: a7cc7613-ad5f-48c8-bd2b-56372cc12dfc
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4cbfbabc96273f6a39a69888025b80d12103dd4b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51803312"
---
# <a name="da0001-use-stringbuilder-for-concatenations"></a>DA0001: usar StringBuilder para concatenações
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente do Visual Studio 2017, consulte [DA0001: usar StringBuilder para concatenações](https://docs.microsoft.com/visualstudio/profiling/da0001-use-stringbuilder-for-concatenations) em docs.microsoft.com.  
  
|||  
|-|-|  
|ID de regra|DA0001|  
|Categoria|Uso do .NET Framework|  
|Métodos de criação de perfil|Amostragem<br /><br /> Instrumentação|  
|Mensagem|Considere o uso de StringBuilder para concatenações de cadeias de caracteres|  
|Tipo de mensagem|Aviso|  
  
## <a name="cause"></a>Causa  
 Chamadas a System.String.Concat são uma proporção significativa dos dados de criação de perfil. Considere o uso da classe <xref:System.Text.StringBuilder> para construir cadeias de caracteres com base em vários segmentos.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Um objeto <xref:System.String> é imutável. Portanto, qualquer modificação na cadeia de caracteres cria um novo objeto de cadeia de caracteres e a coleta de lixo do original. Esse comportamento será o mesmo que chamar String.Concat explicitamente ou usar os operadores de concatenação de cadeia de caracteres, como + ou +=. O desempenho do programa poderá ser diminuído se esses métodos forem chamados com frequência, como ocorre quando os caracteres são adicionados a uma cadeia de caracteres em um loop estreito.  
  
 A classe StringBuilder é um objeto mutável e, ao contrário de System.String, a maioria dos métodos em StringBuilder que modifica uma instância dessa classe retorna uma referência a essa mesma instância. É possível inserir caracteres ou acrescentar texto a uma instância StringBuilder, além de remover ou substituir caracteres na instância sem a necessidade de alocar uma nova instância e excluir a instância original.  
  
## <a name="how-to-investigate-a-warning"></a>Como investigar um aviso  
 Clique duas vezes na mensagem da janela Lista de Erros para navegar para a [Exibição de Detalhes da Função](../profiling/function-details-view.md) dos dados de perfil de amostragem. Encontre as seções do programa que fazem o uso mais frequente da concatenação de cadeia de caracteres. Use a classe StringBuilder para manipulações de cadeias de caracteres complexas, incluindo operações de concatenação de cadeia de caracteres frequentes.  
  
 Para obter mais informações sobre como trabalhar com cadeias de caracteres, consulte a seção [String Operations](http://go.microsoft.com/fwlink/?LinkId=177816) (Operações de cadeia de caracteres) de [Chapter 5 — Improving Managed Code Performance](http://go.microsoft.com/fwlink/?LinkId=177817) (Capítulo 5 – Melhorando o desempenho de código gerenciado) na biblioteca Microsoft Patterns and Practices (Padrões e Práticas da Microsoft).

