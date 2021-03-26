---
title: 'Área de teste 2: obter do controle do código-fonte | Microsoft Docs'
description: Essa área de teste abrange os casos de teste para recuperar itens do repositório de versão com Get. Esses casos de teste podem ser aplicados a projetos locais e para a Web.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting items from source control
- source control [Visual Studio SDK], getting items from
ms.assetid: cbd345c5-ca43-4630-b7a4-85564f4e2090
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ab6a35aa896d7a68e151007d6f694672f7477688
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073424"
---
# <a name="test-area-2-get-from-source-control"></a>Área de teste 2: Obter do controle do código-fonte
Essa área de teste abrange os casos de teste para recuperar itens do repositório de versão por meio do comando Get. Esses casos de teste podem ser aplicados a projetos locais e para a Web.

## <a name="command-menu-access"></a>Acesso ao menu de comando
 Os seguintes [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caminhos de menu do ambiente de desenvolvimento integrado são usados nos casos de teste.

##### <a name="get-latest-version"></a>Obter última versão:

- **Arquivo**, **controle do código-fonte**, **obter última versão**.

- **Arquivo**, **obtenha a versão mais recente**.

- Menu de atalho, **obter versão mais recente**.

- Get: **File**, **controle do código-fonte**, **Get**.

## <a name="expected-behavior"></a>Comportamento esperado

##### <a name="get-latest-version"></a>Obter última versão:
 Executa uma recuperação silenciosa (sem interface do usuário) da versão mais recente do item do repositório de versão.

##### <a name="get"></a>Obter:
 Exibe a caixa de diálogo **obter** e permite que o usuário faça alterações no conjunto de arquivos que será recuperado, bem como modifique as opções que afetam o modo como os arquivos são recuperados.

## <a name="test-cases"></a>Casos de teste

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Obter a versão mais recente de um arquivo que não existe localmente|1. Crie um projeto.<br />2. adicionar um item ao projeto.<br />3. Coloque o projeto sob controle do código-fonte.<br />4. excluir cópia local do item.<br />5. obter a versão mais recente do item (menu de atalho, **obter versão mais recente**).|O arquivo de item é recuperado localmente.|
|Obter um arquivo que não existe localmente|1. Crie um projeto.<br />2. adicionar um item ao projeto.<br />3. Coloque o projeto sob controle do código-fonte.<br />4. excluir cópia local do item.<br />5. obter o item (**arquivo**, **controle do código-fonte**, **Get** \<item> ).|O arquivo de item é recuperado localmente.|
|Obter um arquivo cujo check-out foi feito exclusivamente e modificado localmente|1. Crie um projeto.<br />2. adicionar um item ao projeto.<br />3. Coloque o projeto sob controle do código-fonte.<br />4. Confira exclusivamente o item de projeto.<br />5. modifique a cópia local.<br />6. Obtenha a versão mais recente do item (**arquivo**, **obtenha a versão mais recente do** \<item> ). Se essa etapa for concluída com sucesso, continue na próxima etapa.<br />7. Clique no botão **substituir** na caixa de diálogo de aviso.|**Resultado da etapa 6**`:`<br /><br /> A caixa de diálogo de aviso indica que o check-out do arquivo foi feito.<br /><br /> **Resultado da etapa 7:**<br /><br /> O arquivo local modificado é substituído pela versão original do repositório de versão.<br /><br /> O arquivo é leitura/gravação.|
|Obter e substituir o arquivo que está com check-out, compartilhado e modificado localmente|1. Crie um novo projeto.<br />2. adicionar um item ao projeto.<br />3. Coloque o projeto sob controle do código-fonte.<br />4. Confira o item de projeto como compartilhado.<br />5. modifique a cópia local.<br />6. Obtenha a versão mais recente do item (**arquivo**, **obtenha a versão mais recente do** \<item> ). Se essa etapa for concluída com sucesso, continue na próxima etapa.<br />7. clique em **substituir** na caixa de diálogo de aviso.|**Resultado da etapa 6:**<br /><br /> A caixa de diálogo de aviso indica que o check-out do arquivo foi feito.<br /><br /> **Resultado da etapa 7:**<br /><br /> O arquivo local modificado é substituído pela versão original do repositório de versão.<br /><br /> O arquivo é leitura/gravação.|
|Obter um arquivo que existe localmente, igual à versão mais recente no repositório de versão|1. Crie um novo projeto.<br />2. adicionar um item ao projeto.<br />3. Coloque o projeto sob controle do código-fonte.<br />4. obter o item (**arquivo**, **controle do código-fonte**, **Get** \<item> ).|O arquivo local está inalterado.|
|Obter uma solução com um projeto|1. Crie uma solução com um projeto.<br />2. Coloque a solução sob controle do código-fonte.<br />3. exclua todos os arquivos de projeto localmente.<br />4. Obtenha a solução (**arquivo**, **controle do código-fonte**, **Get**).|Todos os arquivos excluídos são restaurados localmente.|

## <a name="see-also"></a>Confira também
- [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
