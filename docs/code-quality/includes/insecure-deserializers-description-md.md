---
author: dotpaul
ms.author: paulming
ms.date: 04/05/2019
ms.topic: include
ms.openlocfilehash: 054198eff46c0983a5610b29dee5e29e5ac67a70
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68147086"
---
Desserializadores inseguros são vulneráveis ao desserializar dados não confiáveis. Um invasor pode modificar os dados serializados para incluir tipos inesperados para injetar objetos com efeitos colaterais mal-intencionados. Um ataque contra um desserializador inseguro pode, por exemplo, executar comandos no sistema operacional subjacente, comunicar-se pela rede ou excluir arquivos.