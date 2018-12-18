---
title: 'Área de teste 4: Check-In | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], checking items in
- source control plug-ins, checking items in
ms.assetid: d0329fa8-7a8d-4d30-b67b-6f2a97b75a30
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e7f3e8a343823016f391735aae59e58dfefe1a5f
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31133097"
---
# <a name="test-area-4-check-in"></a>Área de teste 4: Check-In
Essa área de plug-in de teste de controle de origem abrange enviar itens atualizados para o armazenamento de versão por meio de **Check-In** comando.  
  
## <a name="command-menu-access"></a>Acesso de Menu de comando  
 O seguinte [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caminhos de menu do ambiente de desenvolvimento integrado são usados nos casos de teste.  
  
##### <a name="check-in"></a>Fazer Check-in:  
 **Arquivo**, **controle de origem**, **Check-In**.  
  
 **Arquivo**, **Check-In**.  
  
 Menu de atalho, **Check-In**.  
  
## <a name="common-expected-behavior"></a>Comportamento esperado comuns  
  
-   Projetos e arquivos adicionados a uma solução ou projeto sob controle de origem são exibidos no **Check-In** caixa de diálogo e o **check-ins pendentes** janela.  
  
-   Após o check-in, os itens adicionados aparecem no controle de origem.  
  
-   Após o check-in, itens atualizados estão corretamente com controle de versão no repositório.  
  
## <a name="test-cases"></a>Casos de teste  
 Estes são os casos de teste específicos para a área de teste de check-in.  
  
### <a name="case-4a-modified-items"></a>Caso 4a: modificado itens  
 Descreve como usar a verificação em ação para atualizar um arquivo sob controle de origem que foi modificado.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Modificar um arquivo de texto que foi feito check-out, verifique no arquivo somente (**Check-In** caixa de diálogo)|1.  Crie um novo projeto com um arquivo de texto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Check-out e modificar o arquivo de texto.<br />4.  Check-in por meio da caixa de diálogo Fazer Check-In (**arquivo**, **controle de origem**, **Check-In**).|Comportamento esperado comuns.|  
|Modificar um arquivo de texto que foi feito check-out, verifique no arquivo somente (**check-ins pendentes** janela)|1.  Crie um novo projeto com um arquivo de texto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Check-out e modificar o arquivo de texto.<br />4.  Check-in por meio de **check-ins pendentes** janela.|Comportamento esperado comuns.|  
  
### <a name="case-4b-adding-files"></a>Caso 4b: adicionando arquivos  
 Ao adicionar um arquivo a um projeto ou um item a uma solução, o projeto ou solução deve alterar também. Assim, o arquivo pai também farão check-out e deve ser verificado para concluir a adição.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Adicionar um arquivo de texto e check-in de tudo (**Check-In** caixa de diálogo)|1.  Crie um novo projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Adicione um arquivo de texto para o projeto.<br />4.  Aceite check-out do projeto, se solicitado.<br />5.  Selecione a solução em **Gerenciador de soluções**.<br />6.  Check-in do **Check-In** caixa de diálogo.|Comportamento esperado comuns.|  
|Adicionar um arquivo de texto e check-in de tudo (**check-ins pendentes** janela)|1.  Crie um novo projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Adicione um arquivo de texto para o projeto.<br />4.  Aceite check-out do projeto, se solicitado.<br />5.  Check-in de solução de **check-ins pendentes** janela.|Comportamento esperado comuns|  
  
### <a name="case-4c-adding-projects"></a>Caso 4c: adicionando a projetos  
 Ao adicionar um projeto a uma solução, a solução deve também serão alteradas. Portanto, o arquivo de solução também farão check-out e deve ser verificado para concluir a adição.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Adicionar um projeto a uma solução em branco sob controle do código-fonte (**Check-In** caixa de diálogo)|1.  Crie uma solução em branco.<br />2.  Adicione a solução ao controle de origem.<br />3.  Adicione um novo projeto.<br />4.  Aceite check-out da solução, se solicitado.<br />5.  Check-in do **Check-In** caixa de diálogo.|Comportamento esperado comuns.|  
|Adicionar um projeto a uma solução em branco sob controle do código-fonte (**check-ins pendentes** janela)|1.  Crie uma solução em branco.<br />2.  Adicione a solução ao controle de origem.<br />3.  Adicione um novo projeto.<br />4.  Aceite check-out da solução, se solicitado.<br />5.  Check-in de solução de **check-ins pendentes** janela.|Comportamento esperado comuns.|  
  
## <a name="see-also"></a>Consulte também  
 [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)