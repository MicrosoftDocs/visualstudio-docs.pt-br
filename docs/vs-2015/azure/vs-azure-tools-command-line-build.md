---
title: Compilação de linha de comando do Azure | Microsoft Docs
description: Compilação de linha de comando do Azure
author: ghogen
manager: douge
assetId: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/05/2017
ms.author: ghogen
ms.openlocfilehash: fce752d91ebaa765e18efef117a3b6efe750119c
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001312"
---
# <a name="building-azure-projects-from-the-command-line"></a>Compilando projetos do Azure da linha de comando
Usando o Microsoft Build Engine (MSBuild), você pode criar produtos nos ambientes de laboratório de compilação em que o Visual Studio não está instalado. MSBuild usa um formato XML para arquivos de projeto extensíveis e totalmente suportado pela Microsoft. Usando o formato de arquivo do MSBuild, é possível descrever quais itens devem ser compilados para uma ou mais plataformas e configurações.

Você também pode executar o MSBuild na linha de comando, e este tópico descreve essa abordagem. Definindo propriedades na linha de comando, você pode criar configurações específicas de um projeto. Da mesma forma, você também pode definir os destinos que o MSBuild compila. Para obter mais informações sobre parâmetros de linha de comando e MSBuild, consulte [referência de linha de comando do MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).

## <a name="msbuild-parameters"></a>Parâmetros do MSBuild
A maneira mais simples para criar um pacote é executar o MSBuild com o `/t:Publish` opção. Por padrão, esse comando cria um diretório em relação à pasta raiz do projeto, como `<ProjectDirectory>\bin\Configuration\app.publish\`. Quando você compila um projeto do Azure, dois arquivos são gerados: o arquivo do pacote em si e o arquivo de configuração que acompanha este artigo:

* Arquivo de pacote (`project.cspkg`)
* Arquivo de configuração (`ServiceConfiguration.TargetProfile.cscfg`)

Por padrão, cada projeto do Azure inclui um arquivo de configuração de serviço para compilações (depuração) locais e outro para compilações de nuvem (preparo ou produção). No entanto, você pode adicionar ou remover arquivos de configuração de serviço conforme necessário. Quando você compila um pacote dentro do Visual Studio, será perguntado qual arquivo de configuração de serviço a ser incluído com o pacote. Quando você compila um pacote usando o MSBuild, o arquivo de configuração de serviço local é incluído por padrão. Para incluir um arquivo de configuração de serviço diferente, defina as `TargetProfile` propriedade do comando MSBuild (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).

Se você quiser usar um diretório alternativo para o pacote armazenado e arquivos de configuração, defina o caminho usando o `/p:PublishDir=Directory\` opção, incluindo o separador de barra invertida à direita.

## <a name="next-steps"></a>Próximas etapas
Depois que o pacote é compilado, você pode implantá-lo para o Azure.