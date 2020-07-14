---
title: 'Como: atualizar uma extensão do Visual Studio | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- update package
- update extension
- new package version
ms.assetid: 93f79774-7b79-4dd6-94ad-13698f72c257
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ee81fe30e10253239bc51dd9d2f199340debc65a
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905624"
---
# <a name="how-to-update-a-visual-studio-extension"></a>Como: atualizar uma extensão do Visual Studio
Você pode atualizar uma extensão do Visual Studio no sistema usando **extensões e atualizações** para instalar a versão atualizada. Se você criar uma versão atualizada de uma extensão, poderá significar que ela foi atualizada incrementando o número de versão no manifesto do VSIX.

 As atualizações são instaladas quando o manifesto do VSIX da extensão de entrada tem o mesmo `ID` que o instalado e um número mais alto `Version` . Se o `Version` número for o mesmo ou inferior, o pacote não poderá ser instalado. Se os `ID` valores não corresponderem, o pacote que ainda não está instalado será reconhecido como uma extensão separada.

 Para ajudar a evitar conflitos durante o desenvolvimento, recomendamos que você desinstale versões anteriores de extensões em andamento e também desinstale ou desabilite qualquer outra extensão potencialmente conflitante.

## <a name="to-update-an-extension-on-your-system"></a>Para atualizar uma extensão em seu sistema

1. No menu **Ferramentas**, clique em **Extensões e Atualizações**.

2. No painel esquerdo, clique em **atualizações**.

3. No painel central, clique na atualização que você deseja instalar.

     O número de versão da extensão atualizada é exibido no painel direito, junto com outras informações.

4. Na parte inferior do painel direito, clique em **Atualizar**.

## <a name="to-publish-an-update-of-an-extension"></a>Para publicar uma atualização de uma extensão

1. No Visual Studio, abra a solução para a extensão que você deseja atualizar. Faça as alterações.

    > [!IMPORTANT]
    > Todas as extensões de usuário não assinadas não são atualizadas automaticamente. Você deve sempre assinar suas extensões.

2. Em **Gerenciador de soluções**, abra *código-fonte... manifest*.

3. No designer de manifesto, aumente o valor do número no campo **versão** .

4. Salve a solução e Compile-a.

5. Carregue o novo arquivo *. vsix* (na pasta * \bin\Debug \* do projeto) no site da [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) .

     Quando um usuário que tem uma versão anterior da extensão abrir **extensões e atualizações**, a nova versão será exibida na lista **atualizações** , desde que a ferramenta esteja definida para procurar atualizações automaticamente.

     Você pode habilitar ou desabilitar a verificação automática de atualizações na parte inferior do painel **atualizações** (**habilitar/desabilitar detecção automática de atualizações disponíveis**), que altera a configuração verificar se há **atualizações** em **ferramentas**  >  **Opções**  >  **Environment**  >  **extensões de ambiente e atualizações**.

    > [!NOTE]
    > A partir do Visual Studio 2015 atualização 2, você pode especificar (em **ferramentas**  >  **Opções**  >  **Environment**  >  **extensões de ambiente e atualizações**) se deseja atualizações automáticas para extensões por usuário, todas as extensões de usuário ou ambas (a configuração padrão).

## <a name="see-also"></a>Confira também
- [Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)
- [Localizar e usar extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md)
