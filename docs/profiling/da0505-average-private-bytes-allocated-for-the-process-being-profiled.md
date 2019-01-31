---
title: 'DA0505: Média de bytes privados alocados para o processo do qual o perfil está sendo criado | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.DA0505
- vs.performance.rules.DA0505
- vs.performance.505
ms.assetid: 32c612ea-d077-44ba-8e6f-3a96333bad00
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 26a3678bb47a27152daa46488d756fe7d51abfa8
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54929959"
---
# <a name="da0505-average-private-bytes-allocated-for-the-process-being-profiled"></a>DA0505: Média de Bytes Privados alocados para o Processo cujo perfil está sendo criado

|||  
|-|-|  
|ID de regra|DA0505|  
|Categoria|Gerenciamento de recursos|  
|Método de criação de perfil|Todos|  
|Mensagem|Essas informações foram coletadas apenas para fins informativos. O contador Bytes privados do processo mede a memória virtual alocada pelo processo do qual o perfil está sendo criado. O valor relatado é a média calculada de todos os intervalos de medição.|  
|Tipo de regra|Informações|  

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.  

## <a name="rule-description"></a>Descrição da regra  
 Essa mensagem relata a quantidade média de memória virtual que o processo alocou em bytes (Bytes privados). Os bytes privados representam os locais de memória virtual que foram alocados pelo processo que podem ser acessados somente por threads em execução no processo.  

 Para processos de 32 bits em execução em um computador de 32 bits, o limite superior da parte privada do espaço de endereço do processo é de 2 GB. Ao usar a opção [/3GB](http://go.microsoft.com/fwlink/?LinkId=177831) Boot.ini, os processos de 32 bits podem adquirir até 3 GB de memória virtual. Um processo de 32 bits em execução em um computador de 64 bits pode adquirir até 4 GB de memória virtual privada.  

 Um processo de 64 bits em execução em um computador de 64 bits pode adquirir até 8 TB de memória virtual privada.  

 O valor relatado é a média de todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo.  

 Para obter mais informações sobre espaços de endereço do processo, consulte [Espaço de endereço virtual](http://go.microsoft.com/fwlink/?LinkId=177832) na documentação do Gerenciamento de memória do Windows.  

## <a name="how-to-use-rule-data"></a>Como usar dados de regra  
 Use o valor relatado para comparar o desempenho de diferentes versões ou compilações do programa ou para entender o desempenho do aplicativo em diferentes cenários de criação de perfil.