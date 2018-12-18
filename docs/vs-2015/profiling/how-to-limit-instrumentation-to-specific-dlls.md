---
title: Como limitar a instrumentação a DLLs específicas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- performance tools, runtime profiling control window
ms.assetid: 17c5996f-e3d0-4e44-b175-52b401b0f2d5
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 054a281d445f5910e9a2d635bb453dd283425453
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51803455"
---
# <a name="how-to-limit-instrumentation-to-specific-dlls"></a>Como limitar a instrumentação a DLLs específicas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao usar o método de criação de perfil de instrumentação, é possível limitar a coleta de dados de criação de perfil a uma ou mais DLLs em um aplicativo. Para analisar uma ou mais DLLs em um aplicativo, você deve criar uma sessão de desempenho que inclui os arquivos .dll como destino. É possível especificar as DLLs que você deseja analisar como projetos em uma solução do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou como arquivos binários independentes.  
  
### <a name="to-limit-instrumentation-to-specific-dlls-in-a-visual-studio-solution"></a>Para limitar a instrumentação a DLLs específicas em uma solução do Visual Studio  
  
1.  Abra a solução que contém a DLL no [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)].  
  
2.  No menu **Analisar**, selecione **Iniciar o Assistente de Desempenho**.  
  
3.  Escolha **Instrumentação** como o método de criação de perfil e, em seguida, clique em **Avançar**.  
  
4.  Em **Para quais dos seguintes destinos disponíveis você deseja criar o perfil?**, selecione o nome do projeto .dll e, em seguida, clique em **Avançar**.  
  
5.  Clique em **Concluir** para sair do assistente e exibir a nova sessão de desempenho na janela **Gerenciador de Desempenho**.  
  
6.  Clique com botão direito do mouse em **Destinos** e, em seguida, selecione **Adicionar Projeto de Destino**.  
  
7.  Na lista **Adicionar Projeto de Destino**, selecione o projeto executável que você deseja usar para exercer a DLL.  
  
     Opcional. Você pode adicionar todos os projetos DLL que desejar analisar.  
  
8.  Para evitar a coleta de dados de um projeto adicionado, clique com o botão direito do mouse no nome do projeto e desmarque a caixa de seleção **Instrumento**.  
  
### <a name="to-specify-specific-dlls-to-profile-as-independent-binaries"></a>Para determinar DLLs específicas a serem analisadas como binários independentes  
  
1.  Abra [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)].  
  
2.  No menu **Analisar**, selecione **Iniciar o Assistente de Desempenho**.  
  
3.  Em **Para quais dos seguintes destinos disponíveis você deseja criar o perfil?**, selecione **Criar o perfil de uma biblioteca de vínculo dinâmico (.DLL)** e, em seguida, clique em **Avançar**.  
  
4.  Na segunda página do assistente, realize as seguintes etapas:  
  
    -   Digite o caminho e o nome do arquivo .dll que você deseja analisar em **Caminho de Dll**. Você também pode clicar no botão de reticências (...) para localizar o arquivo na caixa de diálogo **Biblioteca de Vínculo Dinâmico cujo perfil deve ser criado**. Observe que você deve especificar a cópia do arquivo .dll que será inicializado pelo arquivo executável (.exe) que você selecionar a seguir.  
  
    -   Digite o caminho e o nome do arquivo executável (.exe) que exercerá o .dll em **Caminho do executável**. Você também pode clicar no botão de reticências (...) para localizar o arquivo na caixa de diálogo **Executável a Ser Iniciado**.  
  
    -   Opcional. Digite todos argumentos de linha de comando que você deseja passar para o arquivo executável em **Argumentos de Linha de Comando**. Se necessário, especifique o diretório de trabalho para o aplicativo em **Diretório de trabalho**.  
  
    -   Clique em **Avançar**.  
  
5.  Escolha **Instrumentação** como o método de criação de perfil e, em seguida, clique em **Avançar**.  
  
6.  Clique em **Concluir** para sair do assistente e exibir a nova sessão de desempenho na janela **Gerenciador de Desempenho**.  
  
7.  Opcional. Para adicionar mais arquivos .dll, clique com botão direito do mouse em **Destinos** e, em seguida, selecione **Adicionar Binário de Destino**. Selecione os arquivos na caixa de diálogo **Adicionar Binário de Destino**.  
  
    > [!NOTE]
    >  Não especifique o arquivo executável (.exe) que exerce as DLLs.  
  
## <a name="see-also"></a>Consulte também  
 [Controlling Data Collection](../profiling/controlling-data-collection.md)  (Controlando a coleta de dados)  
 [Como limitar a instrumentação a funções específicas](../profiling/how-to-limit-instrumentation-to-specific-functions.md)



