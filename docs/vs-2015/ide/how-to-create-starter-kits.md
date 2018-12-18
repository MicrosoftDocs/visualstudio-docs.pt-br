---
title: Como criar Kits de Início | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Starter Kits, creating
ms.assetid: ed7d1844-7c01-424a-a831-5003efe0f7bc
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 163fcc07318ae02ff88fda13d4ea6300d513806e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49857400"
---
# <a name="how-to-create-starter-kits"></a>Como criar kits de início
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um kit de início contém código para um aplicativo completo e a documentação sobre como modificar ou expandir o aplicativo. Criar um kit de início é fundamentalmente o mesmo que criar um modelo de projeto normal, a única diferença é que um Kit de Início contem arquivos de documentação definidos para abrir quando um projeto baseado no Kit de Início é criado.  
  
## <a name="designing-and-developing-a-starter-kit"></a>Projetando e desenvolvendo um kit de início  
 Primeiro, é necessário identificar o tipo de kit de início que você deseja desenvolver e definir o seu público-alvo. Em seguida, crie o projeto e a documentação para atender aos seus objetivos.  
  
 Se você estiver criando um aplicativo de exemplo ou plug-in:  
  
- Crie um projeto que compile sem erros.  
  
- Adicione o código de modelo para implementar tarefas adicionais (opcionais).  
  
- Prepare a documentação.  
  
  Se você estiver criando uma ferramenta de aprendizado:  
  
- Crie um projeto que compile sem erros.  
  
- Organize os recursos, como snippets de código e modelos de item.  
  
- Prepare a documentação.  
  
## <a name="creating-a-template"></a>Criando um modelo  
 Depois de concluir o projeto e a documentação, você estará pronto para criar o modelo de projeto para o kit de início. Esse processo é exatamente o mesmo que criar um modelo de projeto.  
  
 Os tópicos a seguir contêm informações sobre a criação de modelos.  
  
 [Como criar modelos de projeto](../ide/how-to-create-project-templates.md)  
 Explica como usar o assistente **Exportar Modelo** para criar um modelo.  
  
 [Como atualizar modelos existentes](../ide/how-to-update-existing-templates.md)  
 Descreve como editar um modelo exportado. Use este procedimento para modificar o arquivo .vstemplate para personalizar seu kit de início.  
  
## <a name="see-also"></a>Consulte também  
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)   
 [Personalizando modelos](../ide/customizing-project-and-item-templates.md)   
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)



