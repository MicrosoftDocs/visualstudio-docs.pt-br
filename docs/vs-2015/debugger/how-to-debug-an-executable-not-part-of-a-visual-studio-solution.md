---
title: 'Como: depurar um executável não faça parte de uma solução do Visual Studio | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], executables
- executable files, importing
- executable files, debugging outside of projects
ms.assetid: 3ea176e8-1ce5-42c4-b7a2-abe3a2765033
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a7fb9b0a31f078ce197851bccb1f4c85f24408a0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51798658"
---
# <a name="how-to-debug-an-executable-not-part-of-a-visual-studio-solution"></a>Como depurar um executável que não faça parte de uma solução do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Às vezes, convém depurar um executável que não é parte de um projeto [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Pode ser um executável criado fora do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou um executável que você recebeu de outra pessoa.  
  
 A resposta usual para esse problema é iniciar a parte externa executável do Visual Studio e anexá-la a ele usando o depurador [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Para obter mais informações, consulte[anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
 Anexar a um aplicativo requer algumas etapas manuais, por isso demora alguns segundos. Este pequeno atraso significa que a anexação não ajudará se você estiver tentando depurar um problema que ocorre durante a inicialização. Além disso, se você estiver depurando um programa que não aguarda a entrada do usuário, e fecha rapidamente, você poderá não ter tempo para anexar a ele. Se você tiver o [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] instalado, poderá criar um projeto EXE para tal programa.  
  
### <a name="to-create-an-exe-project-for-an-existing-executable"></a>Para criar um projeto EXE para um executável existente  
  
1.  Sobre o **arquivo** menu, clique em **abra** e selecione **projeto**.  
  
2.  No **Abrir projeto** caixa de diálogo, clique na lista suspensa lista ao lado de **nome do arquivo** caixa e selecione **todos os arquivos de projeto**.  
  
3.  Localizar o executável e, em seguida, clique em **Okey**.  
  
     Isso cria uma solução temporária que contém o executável.  
  
### <a name="to-import-an-executable-into-a-visual-studio-solution"></a>Para importar um executável em uma solução do Visual Studio  
  
1.  Sobre o **arquivo** , aponte para **Add Project**e, em seguida, clique em **projeto existente**.  
  
2.  No **Adicionar projeto existente** caixa de diálogo, clique na lista suspensa lista ao lado de **nome do arquivo** caixa e selecione **todos os arquivos de projeto**.  
  
3.  Localize e selecione o executável.  
  
4.  Clique em **OK**.  
  
5.  Iniciar o executável escolhendo um comando de execução, tais como **inicie**, da **depurar** menu.  
  
    > [!NOTE]
    >  Nem todas as linguagens de programação oferecem suporte a projetos EXE. Instale o [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] se precisar usar esse recurso.  
  
     Quando você estiver depurando um executável sem código-fonte, os recursos de depuração disponíveis serão limitados, independente de você anexar a um executável em execução ou adicionar o executável a uma solução do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Se o arquivo executável for compilado sem informações de depuração em um formato compatível, os recursos disponíveis serão mais limitados. Se você tiver o código-fonte, a melhor abordagem será importar o código-fonte para o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e criar uma compilação de depuração do executável no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)   
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Arquivos DBG](http://msdn.microsoft.com/en-us/91e449e9-8b65-4123-960f-2107cd1f1cfd)



