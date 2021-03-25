---
title: 'Área de teste 8: alternância de plug-in | Microsoft Docs'
description: Essa área de teste do controle do código-fonte fornece casos de teste para o processo de escolher qual plug-in usar para o controle de origem da solução no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], switching plug-ins
- source control plug-ins, switching
ms.assetid: 01370792-b5da-4e46-9ce2-7dd326587141
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2dbc6b9646bcdec8cbdfae9d262397eb0ff74bdc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090766"
---
# <a name="test-area-8-plug-in-switching"></a>Área de teste 8: Alternância de plug-in
O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE (ambiente de desenvolvimento integrado) tem a interface do usuário para alterar o plug-in atual de controle do código-fonte. Essa área de teste fornece casos de teste para o processo de escolher qual plug-in usar para o controle de origem da solução.

## <a name="command-menu-access"></a>Acesso ao menu de comando
 Os seguintes [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caminhos de menu do ambiente de desenvolvimento integrado são usados nos casos de teste.

- Plug-in de controle do código-fonte atual: **ferram**  ->  **Opções**  ->  seleção de plug-in de **controle do código-fonte**  ->  .

- Alterar Associação de controle do código-fonte: controle de origem de **arquivo**  ->    ->  **alterar controle** de origem...

## <a name="common-expected-behavior"></a>Comportamento comum esperado
 A alteração do plug-in de controle do código-fonte para uma solução é possível sem sair do Visual Studio ou recarregar a solução. Além disso, o plug-in de controle do código-fonte atual muda automaticamente para aquele usado por uma solução quando essa solução é carregada.

## <a name="test-cases"></a>Casos de teste
 Veja a seguir os casos de teste específicos para a área de teste de comutação de plug-in.

### <a name="case-8a-automatic-change"></a>8a de caso: alteração automática

#### <a name="expected-behavior"></a>Comportamento esperado
 Quando um usuário carrega uma solução que está sob controle do código-fonte, a solução é carregada automaticamente e o plug-in apropriado do controle do código-fonte é selecionado como atual.

| Ação | Etapas de teste | Resultados esperados para verificar |
| - | - | - |
| Alteração automática de plug-in de controle do código-fonte | 1. Selecione plug-in em testar como atual (**ferramentas**  ->  **Opções**  ->  seleção de plug-in de **controle do código-fonte**  ->  .)<br />2. Crie um novo projeto.<br />3. Adicione a solução ao controle do código-fonte.<br />4. Selecione outro plug-in (por exemplo, [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] ).<br />5. aceitar o aviso de solução de descarregamento.<br />6. reabra a solução do disco. | A solução está aberta.<br /><br /> O plug-in em teste é o plug-in atual de controle do código-fonte. |

### <a name="case-8b-solution-based-change"></a>Cenário 8B: alteração baseada em solução

#### <a name="expected-behavior"></a>Comportamento esperado
 A solução pode ter seu plug-in de controle do código-fonte associado alterado.

| Ação | Etapas de teste | Resultados esperados para verificar |
|----------------------------------| - | - |
| Alteração de plug-in para uma solução | 1. Selecione plug-in em testar como atual (**ferramentas**  ->  **Opções**  ->  seleção de plug-in de **controle do código-fonte**  ->  ).<br />2. Crie um novo projeto e solução.<br />3. Adicione a solução ao controle do código-fonte.<br />4. desassociar a solução do controle do código-fonte (usando a caixa de diálogo **alterar controle do código-fonte** ).<br />5. Selecione outro plug-in (por exemplo, [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] ).<br />6. recarregue a solução do disco, se descarregada.<br />7. Adicione a solução ao controle do código-fonte.<br />8. desassociar a solução do controle do código-fonte (usando a caixa de diálogo **alterar controle do código-fonte** ).<br />9. Selecione plug-in em teste novamente.<br />10. recarregue a solução do disco, se descarregada.<br />11. associe a solução ao local original (usando a caixa de diálogo **alterar controle do código-fonte** ). | A solução é adicionada ao controle do código-fonte usando o plug-in selecionado. |

## <a name="see-also"></a>Confira também
- [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
