---
title: 'Como: atualizar uma extensão do Visual Studio | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- update package
- update extension
- new package version
ms.assetid: 93f79774-7b79-4dd6-94ad-13698f72c257
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8bf951215dfb4f6837c157a7b8510fba2d09f140
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39500181"
---
# <a name="how-to-update-a-visual-studio-extension"></a>Como: atualizar uma extensão do Visual Studio
Você pode atualizar uma extensão do Visual Studio em seu sistema por meio **extensões e atualizações** para instalar a versão atualizada. Se você criar uma versão atualizada de uma extensão, significam como atualizados incrementando o número de versão no manifesto do VSIX.  
  
 As atualizações são instaladas quando o manifesto do VSIX da extensão de entrada tem o mesmo `ID` como instalado e uma maior `Version` número. Se o `Version` número é igual ou inferior, o pacote não pode ser instalado. Se o `ID` valores não coincidirem, o pacote que ainda não estiver instalado é reconhecido como uma extensão separada.  
  
 Para ajudar a evitar conflitos durante o desenvolvimento, é recomendável que você desinstale as versões anteriores das extensões em andamento e também Desinstale ou desabilite quaisquer outras extensões potencialmente conflitantes.  
  
## <a name="to-update-an-extension-on-your-system"></a>Para atualizar uma extensão em seu sistema  
  
1.  Sobre o **ferramentas** menu, clique em **extensões e atualizações**.  
  
2.  No painel esquerdo, clique em **atualizações**.  
  
3.  No painel central, clique na atualização que deseja instalar.  
  
     O número de versão da extensão atualizado é exibido no painel direito, junto com outras informações.  
  
4.  Na parte inferior do painel direito, clique em **atualização**.  
  
## <a name="to-publish-an-update-of-an-extension"></a>Para publicar uma atualização de uma extensão  
  
1.  No Visual Studio, abra a solução para a extensão que você deseja atualizar. Faça as alterações.  
  
    > [!IMPORTANT]
    >  Sem sinal que todas as extensões de usuário não são atualizadas automaticamente. Você sempre deve assinar suas extensões.  
  
2.  Na **Gerenciador de soluções**, abra *source.extension.manifest*.  
  
3.  No designer de manifesto, aumente o valor do número na **versão** campo.  
  
4.  Salve a solução e compilá-lo.  
  
5.  Carregar o novo *. VSIX* arquivo (no * \bin\Debug\* pasta do projeto) para o [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) site da Web.  
  
     Quando um usuário que tenha uma versão anterior da extensão é aberto **extensões e atualizações**, a nova versão será exibido na **atualizações** listar, desde que a ferramenta esteja definida para procurar atualizações automaticamente.  
  
     Você pode habilitar ou desabilitar a verificação automática de atualizações na parte inferior da **atualizações** painel (**Habilita/desabilita a detecção automática de atualizações disponíveis**), as alterações que o **verificar as atualizações** definindo no **ferramentas** > **opções** > **ambiente**  >  **Extensões e atualizações**.  
  
    > [!NOTE]
    >  A partir do Visual Studio 2015 atualização 2, você pode especificar (em **ferramentas** > **opções** > **ambiente**  >  **Extensões e atualizações**) se você deseja atualizações automáticas para extensões por usuário, todas as extensões de usuário ou ambas (a configuração padrão).  
  
## <a name="see-also"></a>Consulte também  
 [Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)   
 [Localizar e usar extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md)