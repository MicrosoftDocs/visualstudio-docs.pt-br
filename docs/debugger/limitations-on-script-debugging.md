---
title: Limitações na depuração de Script | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- ASPX breakpoint mapping, limitations
- script debugging, limitations
- breakpoint mapping, limitations
ms.assetid: 280eead5-693c-47af-967f-dfe9d23f84db
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9c85f990d08a41bd4b4ee25190d0c5b6bd99d340
ms.sourcegitcommit: 0bf2aff6abe485e3fe940f5344a62a885ad7f44e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37058016"
---
# <a name="limitations-on-script-debugging"></a>Limitações na depuração de script
O [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] suporta a depuração de script do lado do cliente, sujeito às restrições neste tópico.  
  
## <a name="limitations-on-breakpoint-mapping-with-client-side-script"></a>Limitações do mapeamento de pontos de interrupção com script do lado do cliente  
 O [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] permite definir um ponto de interrupção em um ASPX de servidor ou arquivo HTML que seja transformado em um arquivo do lado do cliente em tempo de execução. O [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] mapeia o ponto de interrupção do arquivo do servidor a um ponto de interrupção correspondente no arquivo do lado do cliente, sujeito às seguintes restrições:  
  
-   Os pontos de interrupção devem ser definidos dentro dos blocos de `<script>`. Não é possível mapear pontos de interrupção em scripts embutidos ou em blocos de `<% %>`.  
  
-   A URL do navegador da página deve conter o nome da página. Por exemplo, http://microsoft.com/default.apsx. Mapeamento de ponto de interrupção não é possível reconhecer um redirecionamento de um endereço como http://microsoft.com para a página padrão.  
  
-   O ponto de interrupção deve ser definido na página especificada na URL do navegador, não em um arquivo de controle ASPX (ascx), uma página mestre ou outro arquivo incluído por essa página. Não é possível mapear pontos de interrupção definidos em páginas incluídas.  
  
-   Não é possível mapear pontos de interrupção definidos em blocos de `<script defer=true>`.  
  
-   Para os pontos de interrupção definidos em blocos de `<script id="">`, o mapeamento de pontos de interrupção ignora o atributo `id`.  
  
## <a name="breakpoint-mapping-and-duplicate-lines"></a>Mapeamento de pontos de interrupção e linhas duplicadas  
 Para encontrar o local correspondente no script do servidor e do lado do cliente, o algoritmo de mapeamento de pontos de interrupção examina o código em cada linha. O algoritmo supõe que cada linha é única. Se duas ou mais linhas contêm o mesmo código e você definiu um ponto de interrupção em uma dessas linhas duplicadas, o algoritmo de mapeamento de pontos de interrupção pode selecionar a duplicata incorreta no arquivo do lado do cliente. Para evitar isso, adicione um comentário à linha na qual você definiu o ponto de interrupção. Por exemplo:  
  
```csharp
i++ ;  
i ++; // I added a comment, so this line is now unique  
i ++;  
```
