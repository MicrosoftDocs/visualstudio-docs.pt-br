---
title: Classificação, filtragem e agrupamento em XML Schema Explorer
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 4a914de0-9ffc-4526-9603-92e460e52513
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2a3e281f8e3995cf22100d328089f1993110f756
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34693663"
---
# <a name="sorting-filtering-and-grouping-xml-schema-explorer"></a>Classificação, filtragem e agrupamento (XML Schema Explorer)

Este tópico descreve as opções que estão disponíveis por meio de **opções de agrupamento, filtragem e classificação** menu o **XML Schema Explorer** barra de ferramentas.

## <a name="filter-options"></a>Opções de filtro

 As seguintes opções de filtro estão disponíveis. Por padrão, o **Mostrar Namespaces** e **Mostrar arquivos de esquema** são selecionadas.

-   **Mostrar Namespaces**.

-   **Mostrar os arquivos de esquema**.

-   **Exibir compositores (sequência/escolha/tudo)**.

## <a name="sorting-options"></a>Opções de classificação

 As seguintes opções de classificação estão disponíveis. O padrão é **classificar por tipo**. **Classificar por** opções não se aplicam a arquivos e namespaces.

-   **Classificar por tipo**.

-   **Classificar por nome**.

-   **Ordem de documento**.

### <a name="sort-by-type"></a>Classificar por Tipo

 Quando o **classificar por tipo** opção é selecionada, nós globais são classificados na seguinte ordem. Nós são classificados em ordem alfabética dentro de cada grupo.

1.  nós de`import` .

2.  nós de`include` .

3.  nós de`redefine` .

4.  nós de`attribute` .

5.  nós de`attributeGroup` .

6.  nós de`complexType` .

7.  nós de`simpleType` .

8.  nós de`element` .

9. nós de`group` .

### <a name="sort-by-name"></a>Classificar por Nome

 Quando o **classificar por nome** opção é selecionada, nós globais são classificados na seguinte ordem:

1.  nós de`import` (em ordem alfabética namespaces).

2.  nós de`include` (em ordem alfabética de atributos de `schemaLocation` ).

3.  nós de`redefine` (em ordem alfabética de atributos de `schemaLocation` ).

4.  Outros nós globais em ordem alfabética.

### <a name="document-order"></a>Ordem de documento

 O **ordem do documento** opção está disponível quando o **Mostrar arquivos de esquema** opção é selecionada. Quando **ordem do documento** for selecionada, nós globais são exibidos na ordem em que aparecem no arquivo de esquema.

## <a name="persisting-sortfilter-options"></a>Opções de classificação/filtro persistentes

 A classificação, filtragem, e opções de agrupamento são salvas no Registro para cada usuário, não importa qual a solução ou arquivos estavam aberta quando as configurações foram alteradas.