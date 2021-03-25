---
title: 'Área de teste 6: excluir | Microsoft Docs'
description: Essa área de teste do controle do código-fonte abrange ações de exclusão em Gerenciador de Soluções para o plug-in de controle do código-fonte do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], deleting items
- source control plug-ins, deleting items
ms.assetid: 6f2e872c-5ba2-4303-9f50-a90cef9a6225
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e405df704dfbba14413bd3787a9fb9f959c62a46
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078585"
---
# <a name="test-area-6-delete"></a>Área de teste 6: Excluir
Esta área de teste de plug-in de controle de origem abrange ações de exclusão.

 O controle do código-fonte responde às ações de exclusão no **Gerenciador de soluções**.

 A seguir está uma lista de itens que podem ser excluídos:

- Arquivos

- Pastas

- Project

  Dependendo do tipo de projeto, você pode ter a opção de **remover** o projeto (deixa os arquivos em disco) ou **excluir** o projeto (remove os arquivos em disco). Qualquer ação remove o projeto ou item de **Gerenciador de soluções**.

## <a name="expected-behavior"></a>Comportamento esperado
 O comportamento esperado para os casos de teste na área de teste de exclusão é:

- O item excluído não está mais visível no **Gerenciador de soluções**.

- O check-out do projeto ou item excluído é feito conforme necessário (possivelmente com um prompt).

- Depois que você exclui um item com check-out ou adicionado, ele não aparece na janela **check-ins pendentes** .

- O item ainda existe no armazenamento de controle do código-fonte, mesmo após a exclusão, e deve ser limpo manualmente.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Excluir um projeto de cliente|1. criar um projeto de cliente.<br />2. Adicione a solução ao controle do código-fonte.<br />3. remover o projeto inteiro da solução|Comportamento esperado comum.|
|Excluir um arquivo vazio|1. criar um projeto de cliente.<br />2. Adicione um arquivo de byte zero ao projeto.<br />3. Adicione a solução ao controle do código-fonte.<br />4. Selecione o arquivo, exclua-o.|Comportamento esperado comum.|
|Excluir uma pasta com um arquivo|1. criar solução de projeto único.<br />2. Adicione uma pasta.<br />3. Adicione um arquivo à pasta.<br />4. Adicione a solução ao controle do código-fonte.<br />5. Confira o projeto para evitar prompts.<br />6. exclua a pasta.|Comportamento esperado comum.|
|Excluir um projeto Web do sistema de arquivos|1. Crie um projeto Web do sistema de arquivos (use o botão procurar para especificar um caminho UNC).<br />2. Adicione a solução ao controle do código-fonte.<br />3. Remova todo o projeto da solução.<br />4. Repita as etapas de 1 a 3 para um projeto Web local (exercita caminhos diferentes por meio do código, mas tem a mesma interface e comportamento externos).|Comportamento esperado comum.|
|Excluir um arquivo de um projeto Web do sistema de arquivos|1. criar um projeto Web do sistema de arquivos.<br />2. Adicione a solução ao controle do código-fonte.<br />3. exclua um arquivo do projeto.<br />4. Repita as etapas de 1 a 3 para um projeto Web local (exercita caminhos diferentes por meio do código, mas tem a mesma interface e comportamento externos).|Comportamento esperado comum.|

## <a name="see-also"></a>Confira também
- [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
