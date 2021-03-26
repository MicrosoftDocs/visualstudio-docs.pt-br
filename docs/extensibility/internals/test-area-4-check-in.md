---
title: 'Área de teste 4: fazer check-in | Microsoft Docs'
description: Esta área de teste de plug-in de controle de origem aborda o envio de itens atualizados para o repositório de versão usando o comando check in.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], checking items in
- source control plug-ins, checking items in
ms.assetid: d0329fa8-7a8d-4d30-b67b-6f2a97b75a30
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b8de88b75b7013b75a35c9e92dc662598185e92b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080535"
---
# <a name="test-area-4-check-in"></a>Área de teste 4: Fazer check-in
Esta área de teste de plug-in de controle de origem aborda o envio de itens atualizados para o repositório de versão por meio do comando **check-in** .

## <a name="command-menu-access"></a>Acesso ao menu de comando
 Os seguintes [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caminhos de menu do ambiente de desenvolvimento integrado são usados nos casos de teste.

##### <a name="check-in"></a>Check-in:
 **Arquivo**, **controle do código-fonte**, **check-in**.

 **Arquivo**, **faça check-in**.

 Menu de atalho, **faça check-in**.

## <a name="common-expected-behavior"></a>Comportamento comum esperado

- Projetos e arquivos adicionados a uma solução ou projeto sob controle do código-fonte aparecem na caixa de diálogo **check-in** e na janela **check-ins pendentes** .

- Após o check-in, os itens adicionados aparecem no controle do código-fonte.

- Após o check-in, os itens atualizados têm controle de versão correto na loja.

## <a name="test-cases"></a>Casos de teste
 Veja a seguir os casos de teste específicos para a área de teste de check-in.

### <a name="case-4a-modified-items"></a>Caso 4a: itens modificados
 Descreve como usar a ação de check-in para atualizar um arquivo sob controle do código-fonte que foi modificado.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Modificar um arquivo de texto cujo check-out foi feito, faça check-in somente do arquivo (caixa **de diálogo check-in** )|1. Crie um novo projeto com um arquivo de texto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. fazer check-out e modificar o arquivo de texto.<br />4. faça check-in por meio da caixa de diálogo check-in (**arquivo**, **controle do código-fonte**, **check-in**).|Comportamento esperado comum.|
|Modificar um arquivo de texto cujo check-out foi feito, faça check-in somente do arquivo (janela **check-ins pendentes** )|1. Crie um novo projeto com um arquivo de texto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. fazer check-out e modificar o arquivo de texto.<br />4. faça check-in por meio da janela **check-ins pendentes** .|Comportamento esperado comum.|

### <a name="case-4b-adding-files"></a>4B de caso: Adicionando arquivos
 Ao adicionar um arquivo a um projeto ou a um item a uma solução, o projeto ou a solução também deve ser alterada. Portanto, o check-out do arquivo pai também é necessário e deve ser feito o check-in para concluir a adição.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Adicionar um arquivo de texto e fazer check-in de tudo (caixa **de diálogo check-in** )|1. Crie um novo projeto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Adicione um arquivo de texto ao projeto.<br />4. aceitar check-out do projeto, se solicitado.<br />5. Selecione a solução em **Gerenciador de soluções**.<br />6. faça check-in na caixa de diálogo **check-in** .|Comportamento esperado comum.|
|Adicionar um arquivo de texto e fazer check-in de tudo (janela **check-ins pendentes** )|1. Crie um novo projeto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Adicione um arquivo de texto ao projeto.<br />4. aceitar check-out do projeto, se solicitado.<br />5. fazer check-in da solução na janela **check-ins pendentes** .|Comportamento comum esperado|

### <a name="case-4c-adding-projects"></a>4C de caso: Adicionando projetos
 Ao adicionar um projeto a uma solução, a solução também deve ser alterada. Portanto, o arquivo de solução também é submetido a check-out e deve ser verificado para concluir a adição.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Adicionar um projeto a uma solução em branco no controle do código-fonte (caixa **de diálogo check-in** )|1. Crie uma solução em branco.<br />2. Adicione a solução ao controle do código-fonte.<br />3. adicionar um novo projeto.<br />4. aceitar check-out da solução se solicitado.<br />5. faça check-in na caixa de diálogo **check-in** .|Comportamento esperado comum.|
|Adicionar um projeto a uma solução em branco sob controle do código-fonte (janela **check-ins pendentes** )|1. Crie uma solução em branco.<br />2. Adicione a solução ao controle do código-fonte.<br />3. adicionar um novo projeto.<br />4. aceitar check-out da solução se solicitado.<br />5. fazer check-in da solução na janela **check-ins pendentes** .|Comportamento esperado comum.|

## <a name="see-also"></a>Confira também
- [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
