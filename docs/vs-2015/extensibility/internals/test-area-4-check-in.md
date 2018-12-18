---
title: 'Área de teste 4: Fazer Check-In | Microsoft Docs'
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
- source control [Visual Studio SDK], checking items in
- source control plug-ins, checking items in
ms.assetid: d0329fa8-7a8d-4d30-b67b-6f2a97b75a30
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 97a610325a5165a1de2cc50fede5bbabf182ef5e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51783293"
---
# <a name="test-area-4-check-in"></a>Área de teste 4: fazer check-in
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Essa área de plug-in de teste de controle de origem aborda enviar itens atualizados para o armazenamento de versão por meio de **Fazer Check-In** comando.  
  
## <a name="command-menu-access"></a>Acesso ao Menu de comando  
 O seguinte [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] caminhos de menu de ambiente de desenvolvimento integrado são usados nos casos de teste.  
  
##### <a name="check-in"></a>Fazer Check-in:  
 **Arquivo**, **controle de origem**, **Fazer Check-In**.  
  
 **Arquivo**, **Check-In**.  
  
 Menu de atalho **Fazer Check-In**.  
  
## <a name="common-expected-behavior"></a>Comportamento esperado comuns  
  
-   Projetos e arquivos adicionados a uma solução ou projeto sob controle do código-fonte aparecem na **Fazer Check-In** caixa de diálogo e o **check-ins pendentes** janela.  
  
-   Após o check-in, os itens adicionados são exibidos no controle de origem.  
  
-   Após o check-in, itens atualizados estão corretamente com controle de versão no repositório.  
  
## <a name="test-cases"></a>Casos de teste  
 Estes são os casos de teste específicos para a área de teste de check-in.  
  
### <a name="case-4a-modified-items"></a>Caso 4a: modificou itens  
 Descreve como usar a verificação em ação para atualizar um arquivo sob controle do código-fonte que tenha sido modificado.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Modificar um arquivo de texto que foi feito check-out, check-in somente o arquivo (**Fazer Check-In** caixa de diálogo)|1.  Crie um novo projeto com um arquivo de texto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Fazer check-out e modificar o arquivo de texto.<br />4.  Fazer check-in por meio da caixa de diálogo Fazer Check-In (**arquivo**, **controle do código-fonte**, **Fazer Check-In**).|Comportamento esperado comuns.|  
|Modificar um arquivo de texto que foi feito check-out, Check-in somente o arquivo (**check-ins pendentes** janela)|1.  Crie um novo projeto com um arquivo de texto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Fazer check-out e modificar o arquivo de texto.<br />4.  Fazer check-in por meio de **check-ins pendentes** janela.|Comportamento esperado comuns.|  
  
### <a name="case-4b-adding-files"></a>Caso 4b: adição de arquivos  
 Ao adicionar um arquivo a um projeto ou um item a uma solução, o projeto ou solução deve alterar também. Assim, o arquivo pai também check-out e deve ser verificado para concluir a adição.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Adicione um arquivo de texto e fazer check-in de tudo (**Fazer Check-In** caixa de diálogo)|1.  Crie um novo projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Adicione um arquivo de texto ao projeto.<br />4.  Se solicitado, aceite check-out do projeto.<br />5.  Selecione a solução no **Gerenciador de soluções**.<br />6.  Fazer check-in do **Fazer Check-In** caixa de diálogo.|Comportamento esperado comuns.|  
|Adicione um arquivo de texto e fazer check-in de tudo (**check-ins pendentes** janela)|1.  Crie um novo projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Adicione um arquivo de texto ao projeto.<br />4.  Se solicitado, aceite check-out do projeto.<br />5.  Fazer check-in da solução a partir **check-ins pendentes** janela.|Comportamento esperado comuns|  
  
### <a name="case-4c-adding-projects"></a>Caso c 4: Adicionando projetos  
 Ao adicionar um projeto a uma solução, a solução deve alterar também. Assim, o arquivo de solução também check-out e deve ser verificado para concluir a adição.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Adicionar um projeto a uma solução em branco sob controle do código-fonte (**Fazer Check-In** caixa de diálogo)|1.  Crie uma solução em branco.<br />2.  Adicione a solução ao controle de origem.<br />3.  Adicione um novo projeto.<br />4.  Aceite check-out da solução, se solicitado.<br />5.  Fazer check-in do **Fazer Check-In** caixa de diálogo.|Comportamento esperado comuns.|  
|Adicionar um projeto a uma solução em branco sob controle do código-fonte (**check-ins pendentes** janela)|1.  Crie uma solução em branco.<br />2.  Adicione a solução ao controle de origem.<br />3.  Adicione um novo projeto.<br />4.  Aceite check-out da solução, se solicitado.<br />5.  Fazer check-in da solução a partir **check-ins pendentes** janela.|Comportamento esperado comuns.|  
  
## <a name="see-also"></a>Consulte também  
 [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)

