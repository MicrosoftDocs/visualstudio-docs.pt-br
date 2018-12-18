---
title: Abrir e salvar itens de projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], file persistence
- files [Visual Studio], opening and saving
- editors [Visual Studio SDK], file persistence
ms.assetid: f71898ad-335f-4c43-a177-4da87078afd1
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 895306a70d386b7a895b52b22704ec42a07d17ce
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31130583"
---
# <a name="opening-and-saving-project-items"></a>Abrir e salvar itens de projeto
Quando você adiciona um novo tipo de projeto, você deve gerenciar a abrir e salvar seus arquivos de projetos no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente de desenvolvimento integrado (IDE). Os tópicos a seguir abordam as diferentes abordagens para abrir e salvar arquivos.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Exibir arquivos usando o comando Abrir Arquivo](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)  
 Fornece uma explicação passo a passo de como o IDE manipula o **abrir arquivo** comando e a função de projetos em resposta a esse comando.  
  
 [Exibir arquivos usando o comando Abrir com](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)  
 Fornece uma explicação detalhada, passo a passo de como o IDE manipula o **abrir com** comando, solicitando a abertura de um arquivo que tem algumas opções de editores padrão.  
  
 [Como abrir editores específicos a um projeto](../../extensibility/how-to-open-project-specific-editors.md)  
 Fornece instruções passo a passo para especificar que os arquivos de um determinado tipo em seu projeto devem ser abertos usando um editor específico do projeto.  
  
 [Como abrir editores padrão](../../extensibility/how-to-open-standard-editors.md)  
 Fornece instruções passo a passo para especificar como habilitar o IDE abrir um editor padrão para arquivos em seu tipo de projeto.  
  
 [Como abrir editores para documentos abertos](../../extensibility/how-to-open-editors-for-open-documents.md)  
 Fornece instruções passo a passo para abrir um editor específico do projeto para um arquivo aberto.  
  
 [Salvar um documento padrão](../../extensibility/internals/saving-a-standard-document.md)  
 Fornece uma explicação detalhada de como o IDE manipula o **salvar**, **Salvar como**, e **Salvar tudo** comandos para um documento aberto em um editor padrão.  
  
 [alvar um documento personalizado](../../extensibility/internals/saving-a-custom-document.md)  
 Fornece um diagrama e uma explicação detalhada de como o IDE manipula o **salvar**, **Salvar como**, e **Salvar tudo** comandos para documentos abertos em um editor personalizado.  
  
 [Determinar qual Editor abre um arquivo em um projeto](../../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)  
 Descreve o processo que segue o IDE para selecionar o editor apropriado ou o designer para um arquivo.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Criar designers e editores personalizados](../../extensibility/creating-custom-editors-and-designers.md)  
 Lista os quatro tipos de editores que o IDE pode hospedar e fornece descrições de cada editor.  
  
 [Tipos de projeto](../../extensibility/internals/project-types.md)  
 Discute como projetos de controle de forma que o código é compilado e criado, como editores são abertos e como os itens de projeto são formatados.