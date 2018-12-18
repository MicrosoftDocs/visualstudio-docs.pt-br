---
title: 'Área de teste 2: Obter do controle de origem | Microsoft Docs'
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
- source control plug-ins, getting items from source control
- source control [Visual Studio SDK], getting items from
ms.assetid: cbd345c5-ca43-4630-b7a4-85564f4e2090
caps.latest.revision: 19
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 96b00cfc9965b6006fa51b3cd313566658d604bd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51786152"
---
# <a name="test-area-2-get-from-source-control"></a>Área de teste 2: obter do controle do código-fonte
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Esta área de teste aborda os casos de teste para recuperar itens do repositório de versão por meio do comando Get. Esses casos de teste podem ser aplicados para ambos os locais e para projetos da Web.  
  
## <a name="command-menu-access"></a>Acesso ao Menu de comando  
 O seguinte [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] caminhos de menu de ambiente de desenvolvimento integrado são usados nos casos de teste.  
  
##### <a name="get-latest-version"></a>Obter a versão mais recente:  
  
-   **Arquivo**, **controle de origem**, **obter versão mais recente**.  
  
-   **Arquivo**, **obter versão mais recente**.  
  
-   Menu de atalho **obter última versão**.  
  
-   Get: **arquivo**, **controle de fonte**, **obter**.  
  
## <a name="expected-behavior"></a>Comportamento esperado  
  
##### <a name="get-latest-version"></a>Obter a versão mais recente:  
 Executa uma recuperação de modo silencioso (sem interface do usuário) da versão mais recente do item do repositório de versão.  
  
##### <a name="get"></a>Obter:  
 Exibe a **obter** caixa de diálogo e permite que o usuário fazer alterações ao conjunto de arquivos que será recuperado, bem como para modificar as opções que afetam como os arquivos são recuperados.  
  
## <a name="test-cases"></a>Casos de teste  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Obter a versão mais recente de um arquivo que não existe localmente|1.  Criar um projeto.<br />2.  Adicione um item ao projeto.<br />3.  Coloque o projeto sob controle do código-fonte.<br />4.  Exclua a cópia local do item.<br />5.  Obter a versão mais recente do item (Menu de atalho **obter última versão**).|Arquivo de item é recuperado localmente.|  
|Obter um arquivo que não existe localmente|1.  Criar um projeto.<br />2.  Adicione um item ao projeto.<br />3.  Coloque o projeto sob controle do código-fonte.<br />4.  Exclua a cópia local do item.<br />5.  Obter o item (**arquivo**, **controle do código-fonte**, **obter** \<item >).|Arquivo de item é recuperado localmente.|  
|Obter um arquivo de check-out feito exclusivamente e modificado localmente|1.  Criar um projeto.<br />2.  Adicione um item ao projeto.<br />3.  Coloque o projeto sob controle do código-fonte.<br />4.  Check-out do item de projeto exclusivamente.<br />5.  Modificar a cópia local.<br />6.  Obter a versão mais recente do item (**arquivo**, **obter versão mais recente do** \<item >). Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />7.  Clique em **substituir** botão na caixa de diálogo de aviso.|**ReResult da etapa 6** `:`<br /><br /> Caixa de diálogo de aviso indica que esse arquivo foi extraído.<br /><br /> **ReResult da etapa 7:**<br /><br /> Arquivo local modificado é substituído pela versão original do repositório de versão.<br /><br /> Arquivo é leitura/gravação.|  
|Obter e substituir o arquivo que está com check-out, compartilhado e modificado localmente|1.  Crie um novo projeto.<br />2.  Adicione um item ao projeto.<br />3.  Coloque o projeto sob controle do código-fonte.<br />4.  Check-out do item de projeto como compartilhado.<br />5.  Modificar a cópia local.<br />6.  Obter a versão mais recente do item (**arquivo**, **obter versão mais recente do** \<item >). Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />7.  Clique em **substituir** na caixa de diálogo de aviso.|**Resultado da etapa 6:**<br /><br /> Caixa de diálogo de aviso indica que esse arquivo foi extraído.<br /><br /> **Resultado da etapa 7:**<br /><br /> Arquivo local modificado é substituído pela versão original do repositório de versão.<br /><br /> Arquivo é leitura/gravação.|  
|Obter um arquivo que existe localmente, mesmo que a versão mais recente no repositório de versão|1.  Crie um novo projeto.<br />2.  Adicione um item ao projeto.<br />3.  Coloque o projeto sob controle do código-fonte.<br />4.  Obter o item (**arquivo**, **controle do código-fonte**, **obter** \<item >).|Arquivo local não é alterado.|  
|Obtenha uma solução com um projeto|1.  Crie uma solução com um projeto.<br />2.  Coloque a solução sob controle do código-fonte.<br />3.  Exclua todos os arquivos de projeto localmente.<br />4.  Obter a solução (**arquivo**, **controle do código-fonte**, **obter**).|Todos os arquivos excluídos são restaurados localmente.|  
  
## <a name="see-also"></a>Consulte também  
 [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)

