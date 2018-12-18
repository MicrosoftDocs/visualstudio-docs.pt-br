---
title: 'Área de teste 2: Obter do controle de origem | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting items from source control
- source control [Visual Studio SDK], getting items from
ms.assetid: cbd345c5-ca43-4630-b7a4-85564f4e2090
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 27f2a535b2e08d3632dfd46031823919477fca3e
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31133239"
---
# <a name="test-area-2-get-from-source-control"></a>Área de teste 2: Obter do controle de origem
Essa área de teste abrange os casos de teste para recuperar itens do repositório de versão por meio do comando Get. Nesses casos de teste podem ser aplicados para ambos os locais e projetos da Web.  
  
## <a name="command-menu-access"></a>Acesso de Menu de comando  
 O seguinte [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caminhos de menu do ambiente de desenvolvimento integrado são usados nos casos de teste.  
  
##### <a name="get-latest-version"></a>Obter a versão mais recente:  
  
-   **Arquivo**, **controle de origem**, **obter versão mais recente**.  
  
-   **Arquivo**, **obter versão mais recente**.  
  
-   Menu de atalho, **obter versão mais recente**.  
  
-   Get: **arquivo**, **controle de origem**, **obter**.  
  
## <a name="expected-behavior"></a>Comportamento esperado  
  
##### <a name="get-latest-version"></a>Obter a versão mais recente:  
 Executa uma recuperação de modo silencioso (nenhuma interface do usuário) da versão mais recente do item do armazenamento de versão.  
  
##### <a name="get"></a>Obter:  
 Exibe o **obter** caixa de diálogo e permite que o usuário fizer alterações no conjunto de arquivos que será recuperado, bem como modificar as opções que afetam como os arquivos são recuperados.  
  
## <a name="test-cases"></a>Casos de teste  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Obter a versão mais recente de um arquivo que não existe localmente|1.  Criar um projeto.<br />2.  Adicione um item ao projeto.<br />3.  Coloque o projeto sob controle do código-fonte.<br />4.  Exclua a cópia local do item.<br />5.  Obter a versão mais recente do item (Menu de atalho, **obter versão mais recente**).|Arquivo do item é recuperado localmente.|  
|Obter um arquivo que não existe localmente|1.  Criar um projeto.<br />2.  Adicione um item ao projeto.<br />3.  Coloque o projeto sob controle do código-fonte.<br />4.  Exclua a cópia local do item.<br />5.  Obter o item (**arquivo**, **controle de origem**, **obter** \<item >).|Arquivo do item é recuperado localmente.|  
|Obter um arquivo que foi feito check-out exclusivamente e modificado localmente|1.  Criar um projeto.<br />2.  Adicione um item ao projeto.<br />3.  Coloque o projeto sob controle do código-fonte.<br />4.  O check-out do item de projeto exclusivamente.<br />5.  Modificar a cópia local.<br />6.  Obter a versão mais recente do item (**arquivo**, **obter versão mais recente do** \<item >). Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />7.  Clique em **substituir** botão na caixa de diálogo de aviso.|**ReResult da etapa 6** `:`<br /><br /> Caixa de diálogo de aviso indica que esse arquivo está checked-out.<br /><br /> **ReResult da etapa 7:**<br /><br /> Modificação de arquivo local será substituído pela versão original do armazenamento de versão.<br /><br /> Arquivo é somente leitura.|  
|Obter e substituir o arquivo que está com check-out compartilhado e modificado localmente|1.  Crie um novo projeto.<br />2.  Adicione um item ao projeto.<br />3.  Coloque o projeto sob controle do código-fonte.<br />4.  Check-out do item de projeto como compartilhada.<br />5.  Modificar a cópia local.<br />6.  Obter a versão mais recente do item (**arquivo**, **obter versão mais recente do** \<item >). Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />7.  Clique em **substituir** na caixa de diálogo de aviso.|**Resultado da etapa 6:**<br /><br /> Caixa de diálogo de aviso indica que esse arquivo está checked-out.<br /><br /> **Resultado da etapa 7:**<br /><br /> Modificação de arquivo local será substituído pela versão original do armazenamento de versão.<br /><br /> Arquivo é somente leitura.|  
|Obter um arquivo que existe localmente, mesmo que a versão mais recente no repositório de versão|1.  Crie um novo projeto.<br />2.  Adicione um item ao projeto.<br />3.  Coloque o projeto sob controle do código-fonte.<br />4.  Obter o item (**arquivo**, **controle de origem**, **obter** \<item >).|Arquivo local é alterado.|  
|Obtenha uma solução com um projeto|1.  Crie uma solução com um projeto.<br />2.  Coloque a solução sob controle de origem.<br />3.  Exclua todos os arquivos de projeto localmente.<br />4.  Obter a solução (**arquivo**, **controle de origem**, **obter**).|Todos os arquivos excluídos são restaurados localmente.|  
  
## <a name="see-also"></a>Consulte também  
 [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)