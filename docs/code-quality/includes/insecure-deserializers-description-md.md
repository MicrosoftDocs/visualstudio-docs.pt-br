---
author: dotpaul
ms.author: paulming
ms.date: 04/05/2019
ms.topic: include
ms.openlocfilehash: 054198eff46c0983a5610b29dee5e29e5ac67a70
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89323515"
---
Desserializadores inseguros são vulneráveis ao desserializar dados não confiáveis. Um invasor pode modificar os dados serializados para incluir tipos inesperados para injetar objetos com efeitos colaterais mal-intencionados. Um ataque contra um desserializador inseguro pode, por exemplo, executar comandos no sistema operacional subjacente, comunicar-se pela rede ou excluir arquivos.