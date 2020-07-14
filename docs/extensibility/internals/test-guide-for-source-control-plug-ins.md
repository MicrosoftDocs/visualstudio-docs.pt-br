---
title: Guia de teste para plug-ins de controle do código-fonte | Microsoft Docs
ms.date: 11/04/2016
ms.topic: overview
helpviewer_keywords:
- plug-ins, source control
- source control [Visual Studio SDK], testing plug-ins
- tests, source control plug-ins
- testing, source control plug-ins
- source control plug-ins, test guide
ms.assetid: 13b74765-0b7c-418e-8cd9-5f2e8db51ae5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 321d61175068f135aae87bff73f13ac800f4793c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905158"
---
# <a name="test-guide-for-source-control-plug-ins"></a>Guia de teste para plug-ins de controle do código-fonte
Esta seção fornece diretrizes para testar seu plug-in de controle do código-fonte com o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Uma visão geral abrangente das áreas de teste mais comuns, bem como algumas das áreas mais complexas que podem ser problemáticas é fornecida. Esta visão geral não deve ser uma lista completa de casos de teste.

> [!NOTE]
> Algumas correções de bugs e melhorias no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE mais recente podem revelar problemas com plug-ins de controle do código-fonte existentes que não foram encontrados anteriormente durante o uso de versões anteriores do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . É altamente recomendável que você teste seu plug-in de controle do código-fonte existente para as áreas enumeradas nesta seção, mesmo que nenhuma alteração tenha sido feita no plug-in desde a versão anterior do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

## <a name="common-preparation"></a>Preparação comum
 É necessário um computador com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o e o plug-in de controle do código-fonte de destino instalado. Uma segunda máquina configurada de forma semelhante pode ser usada para alguns dos testes de controle do código-fonte abertos.

## <a name="definition-of-terms"></a>Definição de termos
 Para fins deste guia de teste, use as seguintes definições de termo:

 Projeto de cliente qualquer tipo de projeto disponível no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] que dê suporte à integração de controle do código-fonte (por exemplo,, [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] ou [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] ).

 Projeto Web há quatro tipos de projetos da Web: sistema de arquivos, IIS local, sites remotos e FTP.

- Os projetos do sistema de arquivos são criados em um caminho local, mas eles não exigem que o Serviços de Informações da Internet (IIS) seja instalado, pois eles são acessados internamente por meio de um caminho UNC e podem ser colocados sob o controle do código-fonte de dentro do IDE, bem como projetos cliente.

- Os projetos locais do IIS funcionam com o IIS instalado no mesmo computador e são acessados com uma URL apontando para o computador local.

- Os projetos de sites remotos também são criados em um serviço IIS, mas eles são colocados sob controle do código-fonte no computador do servidor IIS e não de dentro do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.

- Os projetos de FTP são acessados por meio de um servidor FTP remoto, mas não podem ser colocados sob controle do código-fonte.

  Inscrição em outro termo para a solução ou o projeto sob controle do código-fonte.

  Armazenamento de versão o banco de dados de controle do código-fonte que está sendo acessado através da API de plug-in de controle do código

## <a name="test-areas-covered-in-this-section"></a>Áreas de teste abordadas nesta seção

- [Área de teste 1: adicionar a/abrir do controle do código-fonte](../../extensibility/internals/test-area-1-add-to-open-from-source-control.md)

  - Caso 1a: Adicionar solução ao controle do código-fonte

  - Caso 1b: Abrir solução do controle do código-fonte

  - Caso 1C: Adicionar solução do controle do código-fonte

- [Área de teste 2: obter do controle do código-fonte](../../extensibility/internals/test-area-2-get-from-source-control.md)

- [Área de teste 3: fazer check-out/desfazer checkout](../../extensibility/internals/test-area-3-check-out-undo-checkout.md)

  - Caso 3: fazer check-out/desfazer check-out

  - Caso 3A: check-out

  - Caso 3B: desconectado do check-out

  - Caso 3C: Query Edit/consulta Save (QEQS)

  - Caso 3D: check-out silencioso

  - O caso 3E: desfazer check-out

- [Área de teste 4: fazer check-in](../../extensibility/internals/test-area-4-check-in.md)

  - Caso 4a: itens modificados

  - 4B de caso: Adicionando arquivos

  - 4C de caso: Adicionando projetos

- [Área de teste 5: alterar o controle do código-fonte](../../extensibility/internals/test-area-5-change-source-control.md)

  - Caso 5a: associar

  - Caso 5b: desassociar

  - 5C de caso: reassociar

- [Área de teste 6: excluir](../../extensibility/internals/test-area-6-delete.md)

- [Testar área 7: compartilhar](../../extensibility/internals/test-area-7-share.md)

- [Área de teste 8: alternância de plug-in](../../extensibility/internals/test-area-8-plug-in-switching.md)

  - 8a de caso: alteração automática

  - Cenário 8B: alteração baseada em solução

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../../extensibility/source-control-plug-ins.md)
