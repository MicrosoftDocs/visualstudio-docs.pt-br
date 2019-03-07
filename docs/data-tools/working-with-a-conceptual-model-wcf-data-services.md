---
title: Trabalhando com um modelo conceitual (WCF Data Services)
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data [Visual Studio], querying a service
- data [Visual Studio], LINQ to Entities
- data [Visual Studio], querying an EDM
ms.assetid: 2cd873cf-b010-49f2-a278-bb1277aaa934
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 135985d7e6ed13555db73f35fef31e6da4b85071
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55910019"
---
# <a name="work-with-a-conceptual-model-wcf-data-services"></a>Trabalhar com um modelo conceitual (WCF Data Services)

Quando você usa um modelo conceitual para descrever os dados em um banco de dados, você pode consultar os dados por meio de seus objetos em vez de precisar converter de e para trás entre um esquema de banco de dados e um modelo de objeto.

 Você pode usar modelos conceituais com aplicativos do WCF Data Services. Os tópicos a seguir mostram como consultar dados por meio de um modelo conceitual.


| Tópico | Descrição |
| - | - |
| [How to: Execute Data Service Queries](/dotnet/framework/data/wcf/how-to-execute-data-service-queries-wcf-data-services) (Como executar consultas de serviço de dados) | Mostra como consultar um serviço de dados de um [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] aplicativo. |
| [Como projetar resultados da consulta](/dotnet/framework/data/wcf/how-to-project-query-results-wcf-data-services) | Mostra como reduzir a quantidade de dados retornados por meio de uma consulta de serviço de dados. |

 Quando você usa um modelo conceitual, você pode definir o tipo de dados é válido no idioma que corresponde a seu domínio. Você pode definir dados válidos no modelo, ou você pode adicionar validação para operações que podem ser executadas em um serviço de dados ou de entidade.

 Os tópicos a seguir mostram como adicionar validação para aplicativos do WCF Data Services.

|Tópico|Descrição|
|-----------|-----------------|
|[Como interceptar mensagens de serviço de dados](/dotnet/framework/data/wcf/how-to-intercept-data-service-messages-wcf-data-services)|Mostra como adicionar validação a uma operação de serviço de dados.|

 Os tópicos a seguir mostram como criar, atualizar e excluir dados, executando operações em entidades.

|Tópico|Descrição|
|-----------|-----------------|
|[Como adicionar, modificar e excluir entidades](/dotnet/framework/data/wcf/how-to-add-modify-and-delete-entities-wcf-data-services)|Mostra como criar, atualizar e excluir dados de entidade em um serviço de dados.|
|[Como definir relacionamentos entre entidades](/dotnet/framework/data/wcf/how-to-define-entity-relationships-wcf-data-services)|Mostra como criar ou alterar as relações em um serviço de dados.|

## <a name="see-also"></a>Consulte também

- [Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
- [Querying the Data Service](/dotnet/framework/data/wcf/querying-the-data-service-wcf-data-services) (Consultando o serviço de dados)