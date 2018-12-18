---
title: Acessando máquinas virtuais do Azure no Gerenciador de servidores | Microsoft Docs
description: Obtenha uma visão geral de como exibir, criar e gerenciar máquinas virtuais (VMs) do Azure no Gerenciador de servidores no Visual Studio.
author: ghogen
manager: douge
assetId: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 8/31/2017
ms.author: ghogen
ms.openlocfilehash: e1410b3dc60ec9689b6582e794aaf10cd13092aa
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001144"
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>Acessando máquinas virtuais do Azure no Gerenciador de Servidores

Se você tiver máquinas virtuais hospedadas pelo Azure, você pode acessá-los no Gerenciador de servidores. Você primeiro deve entrar em sua assinatura do Azure para exibir os serviços móveis. Para entrar, abra o menu de atalho do nó do Azure no Gerenciador de servidores e escolha **conectar-se ao Microsoft Azure**.

1. No Cloud Explorer, escolha uma máquina virtual e, em seguida, escolha a tecla F4 para mostrar a janela de propriedades.

    A tabela a seguir mostra quais propriedades estão disponíveis, mas eles são todos somente leitura. Para alterá-las, use o [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

   | Propriedade | Descrição |
   | --- | --- |
   | Nome DNS |A URL com o endereço de Internet da máquina virtual. |
   | Ambiente |Para uma máquina virtual, o valor dessa propriedade é sempre produção. |
   | Nome |O nome da máquina virtual. |
   | Tamanho |O tamanho da máquina virtual, que reflete a quantidade de memória e espaço em disco disponível. Para obter mais informações, consulte [tamanhos de máquina Virtual](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs). |
   | Status |Os valores incluem inicial, iniciado, parando, parado e recuperando Status. Se recuperando Status aparecer, o status atual é desconhecido. Os valores para essa propriedade diferem dos valores que são usados na [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). |
   | SubscriptionID |A ID de assinatura para sua conta do Azure. Você pode mostrar essas informações sobre o [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) exibindo as propriedades para uma assinatura. |
2. Escolha um nó do ponto de extremidade e, em seguida, exiba os **propriedades** janela.
3. A tabela a seguir descreve as propriedades disponíveis de pontos de extremidade, mas eles são somente leitura. Para adicionar ou editar os pontos de extremidade para uma máquina virtual, use o [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). 

   | Propriedade | Descrição |
   | --- | --- |
   | Nome |Um identificador para o ponto de extremidade. |
   | Porta privada |A porta para acesso à rede interna ao seu aplicativo. |
   | Protocolo |O protocolo que usa a camada de transporte para esse ponto de extremidade, TCP ou UDP. |
   | Porta pública |A porta que é usada para acesso público ao seu aplicativo. |
