---
title: 'DA0506: máximo de bytes privados alocados para o processo do qual o perfil está sendo criado | Microsoft Docs'
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
- vs.performance.rules.DA0506
- vs.performance.DA0506
- vs.performance.506
ms.assetid: e9c43554-9a85-4d98-9fa4-3b19986e7b62
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bdd7d63ad7dd0261394d3333cdd35ec5f5a330f1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810384"
---
# <a name="da0506-maximum-private-bytes-allocated-for-the-process-being-profiled"></a>DA0506: máximo de bytes particulares alocados para o processo com criação de perfil
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Id da regra | DA0506 |  
| Categoria | Monitoramento de recursos |  
| Método de criação de perfil | Todos os |  
| Mensagem | Estas informações foram coletadas apenas para fins informativos. O contador Bytes privados do processo mede a memória virtual alocada pelo processo do qual o perfil está sendo criado. O valor relatado é o máximo observado em todos os intervalos de medição. |  
| Tipo de regra | Informações |  
  
 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Essa mensagem relata a quantidade máxima de memória virtual que o processo alocou em bytes (Bytes privados). Os bytes privados representam os locais de memória virtual que foram alocados pelo processo que podem ser acessados somente por threads em execução no processo.  
  
 Para processos de 32 bits em execução em um computador de 32 bits, o limite superior da parte privada do espaço de endereço do processo é de 2 GB. Ao usar a opção [/3 GB](http://go.microsoft.com/fwlink/?LinkId=177831) Boot.ini, os processos de 3 bits podem adquirir até 32 GB de memória virtual. Um processo de 32 bits em execução em um computador de 64 bits pode adquirir até 4 GB de memória virtual privada.  
  
 Um processo de 64 bits em execução em um computador de 64 bits pode adquirir até 8 TB de memória virtual privada.  
  
 O valor relatado é o máximo de todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo.  
  
 Para obter mais informações sobre espaços de endereço do processo, consulte [Espaço de endereço virtual](http://go.microsoft.com/fwlink/?LinkId=177832) na documentação do Gerenciamento de memória do Windows.  
  
## <a name="how-to-use-rule-data"></a>Como usar dados de regra  
 Use o valor relatado para comparar o desempenho de diferentes versões ou compilações do programa ou para entender o desempenho do aplicativo em diferentes cenários de criação de perfil.  
  
 Um valor máximo de bytes privados do processo que está se aproximando do limite arquitetônico do crescimento máximo de um espaço de endereço do processo pode levar a exceções de memória insuficiente. Para obter mais informações, consulte [Investigando problemas de memória](http://go.microsoft.com/fwlink/?LinkID=177833) na Revista do MSDN.



