---
title: Acesso negado | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 8a512060-d744-47af-a83e-4ba42ea2c5b2
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 874f7c0e5dcfaf4881c059a77f1c5e930d8c0578
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814831"
---
# <a name="access-is-denied"></a>O acesso foi negado
Um script tentou acessar dados de uma fonte que não é o host da página atual. A Política de Mesma Origem seguida pelo Internet Explorer e outros navegadores permite que scripts acessem dados somente de fontes com o mesmo esquema, host e porta de URL da página atual.  
  
 Por exemplo, se a página atual for `https://employees.mycompany.com` , você não poderá acessar dados das seguintes URLs:  
  
- `http://data.contoso.com`, porque está usando HTTP em vez de HTTPS.  
  
- `https://somedatasource.com`, porque ele é um domínio diferente.  
  
- `https://employees.mycompany.com:8888`, porque ele usa uma porta diferente.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Investigue se a API que você está tentando chamar dá suporte para JSONP ou CORS, que são duas abordagens que permitem o uso de scripts entre origens de forma segura.  
  
- Se você estiver tentando chamar uma API REST, refatore essa chamada para seu código do lado do servidor e exponha um novo ponto de extremidade REST para seus scripts do lado do cliente.  
  
     Para saber mais, procure a documentação online relacionada a Política de Mesma Origem, JSONP e CORS.
