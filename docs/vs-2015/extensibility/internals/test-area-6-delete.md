---
title: 'Área de teste 6: Excluir | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- source control [Visual Studio SDK], deleting items
- source control plug-ins, deleting items
ms.assetid: 6f2e872c-5ba2-4303-9f50-a90cef9a6225
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1498566e1afeaf1517b7ae3bd62297444c828888
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51766303"
---
# <a name="test-area-6-delete"></a>Área de teste 6: excluir
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Essa área de plug-in de teste de controle de origem aborda as ações de exclusão.  
  
 Controle de origem responde para excluir ações na **Gerenciador de soluções**.  
  
 A seguir está uma lista de itens que podem ser excluídos:  
  
- Arquivos  
  
- Pastas  
  
- Projeto  
  
  Dependendo do tipo de projeto, você terá a opção de **remova** o projeto (deixa os arquivos no disco) ou **excluir** o projeto (remove os arquivos no disco). Qualquer ação remove o projeto ou item de **Gerenciador de soluções**.  
  
## <a name="expected-behavior"></a>Comportamento esperado  
 O comportamento esperado para os casos de teste na área de teste delete é:  
  
-   Item excluído não está mais visível dentro **Gerenciador de soluções**.  
  
-   O pai do item ou projeto excluído foi extraído, conforme necessário (possivelmente com um prompt.)  
  
-   Depois de excluir um check-out ou foi adicionado um item, ele não aparece na **check-ins pendentes** janela.  
  
-   O item ainda existe dentro do armazenamento de controle de origem, mesmo após a exclusão e deve ser removido manualmente.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Excluir um projeto de cliente|1.  Crie um projeto de cliente.<br />2.  Adicione a solução ao controle de origem.<br />3.  Remova todo o projeto de solução|Comportamento esperado comuns.|  
|Excluir um arquivo vazio|1.  Crie um projeto de cliente.<br />2.  Adicione um arquivo de zero byte ao projeto.<br />3.  Adicione a solução ao controle de origem.<br />4.  Selecione o arquivo, excluí-lo.|Comportamento esperado comuns.|  
|Excluir uma pasta com um arquivo|1.  Crie a solução de projeto único.<br />2.  Adicione uma pasta.<br />3.  Adicione um arquivo para a pasta.<br />4.  Adicione a solução ao controle de origem.<br />5.  Check-out do projeto para evitar prompts.<br />6.  Exclua a pasta.|Comportamento esperado comuns.|  
|Excluir um projeto Web do sistema de arquivos|1.  Crie um projeto Web do sistema de arquivos (use o botão Procurar para especificar um caminho UNC).<br />2.  Adicione a solução ao controle de origem.<br />3.  Remova todo o projeto da solução.<br />4.  Repita as etapas 1 a 3 para um projeto da Web local (exercita caminhos diferentes por meio do código, mas tem a mesma interface externa e o comportamento).|Comportamento esperado comuns.|  
|Excluir um arquivo de um projeto Web do sistema de arquivos|1.  Crie um projeto Web do sistema de arquivos.<br />2.  Adicione a solução ao controle de origem.<br />3.  Exclua um arquivo de projeto.<br />4.  Repita as etapas 1 a 3 para um projeto da Web local (exercita caminhos diferentes por meio do código, mas tem a mesma interface externa e o comportamento).|Comportamento esperado comuns.|  
  
## <a name="see-also"></a>Consulte também  
 [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)

