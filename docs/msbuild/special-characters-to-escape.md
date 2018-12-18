---
title: Caracteres especiais para escape| Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- special characters to escape
- msbuild, special characters to escape
ms.assetid: 5b5172c3-41e4-4f38-a16f-2aeac831a5fc
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a57316904aa1075484a4d33c6e2259586c88fe78
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39151374"
---
# <a name="special-characters-to-escape"></a>Caracteres especiais para escape
Caracteres especiais devem ser de escape somente se tiverem um significado especial no contexto em que eles estiverem sendo usados. Por exemplo, o asterisco (*) é um caractere especial somente nos atributos "Incluir" e "Excluir" de uma definição de item ou em uma chamada para <xref:Microsoft.Build.Tasks.CreateItem>. Em outros casos, o asterisco é tratado como um asterisco literal. Embora você não precise que os asteriscos sejam de escape em todos os arquivos de projeto, fazer isso não é prejudicial.  
  
 Use a notação %\<xx> no lugar do caractere especial, em que \<xx> representa o valor hexadecimal do caractere ASCII. Por exemplo, para usar um asterisco (*) como um caractere literal, use o valor `%2A`.  
  
 Veja a seguir a lista completa de caracteres especiais de escape:  
  
|Caractere|Descrição|  
|---------------|-----------------|  
|%|Sinal de porcentagem, usado para fazer referência a metadados.|  
|$|Cifrão, usado para fazer referência a propriedades.|  
|@|Sinal de arroba, usado para fazer referência a listas de itens.|  
|(|Parênteses de abertura, usado em listas.|  
|)|Parênteses de fechamento, usado em listas.|  
|`|Apóstrofe (ou marca de escala) usado em condições e outras expressões.|  
|;|Ponto e vírgula, separador de lista.|  
|?|Ponto de interrogação, um caractere curinga ao descrever uma especificação de arquivo na seção Incluir/Excluir de um item.|  
|*|Asterisco, um caractere curinga ao descrever uma especificação de arquivo na seção Incluir/Excluir de um item.|  
  
## <a name="see-also"></a>Consulte também  
 [Como fazer o escape de caracteres especiais no MSBuild](../msbuild/how-to-escape-special-characters-in-msbuild.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)