---
title: Propriedades de arquivo, JavaScript | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- javascript.project.property.expandedsdknode.fileversion
- javascript.project.property.expandedsdknode.uri
- javascript.project.property.expandedsdknode.filename
- javascript.project.property.reference.description
- javascript.project.property.reference.specificversion
- javascript.project.property.reference.identity
- javascript.project.property.fullpath
- javascript.project.property.packageaction
- javascript.project.property.reference.package
- javascript.project.property.copytooutputdirectory
- javascript.project.property.expandedsdknode.sdkpath
- javascript.project.property.reference.filetype
- javascript.project.property.reference.culture
- javascript.project.property.filename
- javascript.project.property.reference.resolvedpath
- javascript.project.property.reference.version
ms.assetid: 085913b8-a97b-45f7-85fa-bbb0902f3ee9
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 8db05d62bd1a8b1e1bf5fee6642810c654265c97
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49909725"
---
# <a name="file-properties-javascript"></a>Propriedades de arquivo, JavaScript
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
É possível usar propriedades de arquivo para indicar quais ações o sistema de projeto deve executar nos arquivos. Por exemplo, é possível definir propriedades de arquivo para indicar se um arquivo deve ser adicionado ao pacote como um arquivo de recurso.  
  
 É possível selecionar qualquer arquivo no Gerenciador de Soluções e, em seguida, examinar suas propriedades na janela Propriedades. Os arquivos JavaScript têm quatro propriedades: **Copiar para Diretório de Saída**, **Ação do Pacote**, **Nome de Arquivo** e **Caminho do Arquivo**.  
  
## <a name="file-properties"></a>Propriedades do Arquivo  
 Esta seção descreve as propriedades comuns aos arquivos JavaScript.  
  
### <a name="copy-to-output-directory-property"></a>Propriedade Copiar para Diretório de Saída  
 Esta propriedade especifica as condições sob as quais o arquivo de origem selecionado será copiado para o diretório de saída. Selecione **Não copiar** se o arquivo nunca deve ser copiado para o diretório de saída. Selecione **Copiar sempre** se o arquivo sempre deve ser copiado para o diretório de saída. Selecione **Copiar se for mais novo** se o arquivo deve ser copiado somente quando ele for mais recente que um arquivo existente de mesmo nome no diretório de saída.  
  
### <a name="package-action"></a>Ação do Pacote  
 A propriedade **Ação do Pacote** indica o que o Visual Studio faz com um arquivo quando um build é executado. A **Ação do Pacote** pode ter um valor dentre vários:  
  
- **Nenhum** – O arquivo não está incluído no manifesto do pacote. Um exemplo é um arquivo de texto que contém a documentação, como um arquivo Leiame.  
  
- **Conteúdo** – O arquivo está incluído no manifesto do pacote. Por exemplo, essa configuração é o valor padrão para um arquivo .htm, .js, .css, de imagem, de áudio ou de vídeo.  
  
- **Manifesto** – O arquivo não está incluído no manifesto do pacote. Em vez disso, o arquivo é usado para entrada ao gerar o manifesto do pacote. Esse é o valor padrão do arquivo package.appxmanifest.  
  
- **Recurso** – O arquivo não está incluído no manifesto do pacote. Em vez disso, o conteúdo do arquivo é indexado no PRI (Índice de Recurso do Pacote) que entra no manifesto do pacote. Normalmente, ele é usado para arquivos de recurso.  
  
  O valor padrão para **Ação do Pacote** depende da extensão do arquivo adicionado à solução.  
  
### <a name="file-name-property"></a>Propriedade Nome de Arquivo  
 Exibe o nome de arquivo como um valor somente leitura. Para renomear o arquivo, é necessário clicar com o botão direito do mouse no Gerenciador de Soluções e selecionar **Renomear**.  
  
### <a name="full-path-property"></a>Propriedade do caminho completo  
 Exibe o caminho completo no arquivo como um valor somente leitura. Para alterar o caminho do arquivo, é possível arrastar e soltar o arquivo no Gerenciador de Soluções.  
  
## <a name="reference-file-properties"></a>Propriedades do arquivo de referência  
 Esta seção descreve as propriedades comuns aos arquivos referenciados em um [!INCLUDE[win8_app_js](../../includes/win8-app-js-md.md)]. Quando você seleciona uma referência como um arquivo .winmd, uma referência de SDK, uma referência projeto a projeto ou uma referência de assembly no Gerenciador de Soluções, outras propriedades podem ser exibidas na janela Propriedades, de acordo com o tipo de arquivo.  
  
### <a name="culture"></a>Cultura  
 Exibe o idioma associado à referência.  
  
### <a name="file-type"></a>Tipo de arquivo  
 Exibe o tipo de arquivo da referência.  
  
### <a name="file-version"></a>Versão do arquivo  
 Exibe a versão de arquivo da referência.  
  
### <a name="identity"></a>Identidade  
 Exibe a identidade da referência usada no projeto, armazenado no arquivo de projeto.  
  
### <a name="package"></a>Pacote  
 Exibe o nome do manifesto do pacote associado à referência.  
  
### <a name="resolved-path"></a>Caminho da resolução  
 Exibe o caminho da referência usada no projeto.  
  
### <a name="sdk-path"></a>Caminho do SDK  
 Exibe o caminho para o arquivo do SDK referenciado.  
  
### <a name="uri"></a>URI  
 Exibe o URI que deve ser incluído nos arquivos HTML ou JavaScript do projeto para incluir o arquivo como um arquivo de origem.  
  
### <a name="version"></a>Versão  
 Exibe a versão da referência.  
  
## <a name="see-also"></a>Consulte também  
 [NIB: Propriedades do projeto (Visual Studio)](http://msdn.microsoft.com/en-us/eb4c97ed-f667-4850-98d0-6e2a4d21bbca)



