---
title: Construindo cadeias de caracteres de filtro para o designer de tabela | Microsoft Docs
description: Construindo cadeias de caracteres de filtro para o designer de tabela
author: ghogen
manager: douge
assetId: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/18/2016
ms.author: ghogen
ms.openlocfilehash: ff8c3dd927e81b9e131242a9a6631a8297046a6e
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001299"
---
# <a name="constructing-filter-strings-for-the-table-designer"></a>Construindo cadeias de caracteres de filtro para o Designer de Tabela
## <a name="overview"></a>Visão geral
Para filtrar dados em uma tabela do Azure que é exibido no Visual Studio **Designer de tabela**, construir uma cadeia de caracteres de filtro e insira-o no campo de filtro. A sintaxe de cadeia de caracteres de filtro é definida pelo WCF Data Services e é semelhante a uma cláusula SQL WHERE, mas é enviada para o serviço de tabela por meio de uma solicitação HTTP. O **Designer de tabela** lida com a codificação correta para você, portanto, para filtrar um valor da propriedade desejada, você só precisa digitar o nome da propriedade, operador de comparação, valor de critérios e, opcionalmente, booliano operador no campo de filtro. Você não precisa incluir a opção de consulta $filter como você faria se estivesse criando uma URL para consultar a tabela por meio de [referência de API de REST de serviços de armazenamento](http://go.microsoft.com/fwlink/p/?LinkId=400447).

O WCF Data Services se baseiam os [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData). Para obter detalhes sobre a opção de consulta de sistema filter (**$filter**), consulte o [especificação de convenções de URI OData](http://go.microsoft.com/fwlink/p/?LinkId=214806).

## <a name="comparison-operators"></a>Operadores de comparação
Os seguintes operadores lógicos têm suporte para todos os tipos de propriedade:

| operador lógico | Descrição | Cadeia de caracteres de filtro de exemplo |
| --- | --- | --- |
| EQ |Igual |City eq 'Redmond' |
| gt |Maior que |Preço gt 20 |
| GE |Maior ou igual a |Preço ge 10 |
| lt |Menor que |Preço lt 20 |
| Le |Menor que ou igual a |Preço le 100 |
| ne |Não é igual a |Cidade ne 'London' |
| e |And |Preço le 200 e preço gt 3,5 |
| ou |Ou |Preço le 3,5 ou preço gt 200 |
| not |não |não isAvailable |

Ao construir uma cadeia de caracteres de filtro, as regras a seguir são importantes:

* Use os operadores lógicos para comparar uma propriedade com um valor. Observe que não é possível comparar uma propriedade com um valor dinâmico; um dos lados da expressão deve ser uma constante.
* Todas as partes da cadeia de caracteres de filtro diferenciam maiusculas de minúsculas.
* O valor da constante deve ser do mesmo tipo de dados como a propriedade para que o filtro retorne resultados válidos. Para obter mais informações sobre os tipos de propriedade com suporte, consulte [Noções básicas sobre o modelo de dados do serviço de tabela](http://go.microsoft.com/fwlink/p/?LinkId=400448).

## <a name="filtering-on-string-properties"></a>Filtrando em Propriedades de cadeia de caracteres
Ao filtrar nas propriedades de cadeia de caracteres, coloque a constante de cadeia de caracteres entre aspas simples.

O exemplo a seguir filtra a **PartitionKey** e **RowKey** propriedades; adicionais não chave propriedades também podem ser adicionadas à cadeia de caracteres de filtro:

    PartitionKey eq 'Partition1' and RowKey eq '00001'

Você pode colocar cada expressão de filtro entre parênteses, embora não seja necessário:

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

Observe que o serviço de tabela não oferece suporte a consultas de curingas e eles não têm suporte no Designer de tabela ou. No entanto, você pode executar usando os operadores de comparação no prefixo desejado de correspondência de prefixo. O exemplo a seguir retorna entidades com a propriedade LastName começando com a letra 'A':

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a>Filtrando em propriedades numéricas
Para filtrar em um inteiro ou um número de ponto flutuante, especifique o número sem aspas.

Este exemplo retorna todas as entidades com uma propriedade idade cujo valor é maior que 30:

    Age gt 30

Este exemplo retorna todas as entidades com uma propriedade AmountDue cujo valor é menor ou igual a 100,25:

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a>Filtrando em Propriedades Boolianas
Para filtrar um valor booliano, especifique **verdadeira** ou **falso** sem aspas.

O exemplo a seguir retorna todas as entidades em que a propriedade IsActive é definida como **verdadeira**:

    IsActive eq true

Você também pode escrever essa expressão de filtro sem o operador lógico. No exemplo a seguir, o serviço tabela também retornará todas as entidades nas quais IsActive for **verdadeira**:

    IsActive

Para retornar todas as entidades nas quais IsActive for false, você pode usar o não operador:

    not IsActive

## <a name="filtering-on-datetime-properties"></a>Filtrando em Propriedades DateTime
Para filtrar um valor DateTime, especifique o **datetime** palavra-chave, seguido pela constante de data/hora entre aspas. A constante de data/hora deve estar no formato UTC combinado, conforme descrito em [formatação de valores de propriedade DateTime](http://go.microsoft.com/fwlink/p/?LinkId=400449).

O exemplo a seguir retorna entidades em que a propriedade CustomerSince é igual a 10 de julho de 2008:

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
