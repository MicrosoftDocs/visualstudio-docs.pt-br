---
title: Solução de problemas e problemas conhecidos (Ferramentas do Visual Studio para Unity) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8f5db192-8d78-4627-bd07-dbbc803ac554
caps.latest.revision: 7
author: conceptdev
ms.author: crdun
manager: ghogen
ms.openlocfilehash: 94240d5af43944b23890a32b757fe1b4f14b77ec
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755512"
---
# <a name="troubleshooting-and-known-issues-visual-studio-tools-for-unity"></a>Solucionando problemas e problemas conhecidos (Visual Studio Tools for Unity)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Nesta seção, você encontrará soluções para problemas comuns das Ferramentas do Visual Studio para Unity, as descrições de problemas conhecidos e aprenderá como ajudar a melhorar as Ferramentas do Visual Studio para Unity por meio de relatórios de erro.  
  
## <a name="troubleshooting"></a>Solução de problemas  
 Para resolver alguns problemas comuns das Ferramentas do Visual Studio para Unity, consulte as seções a seguir.  
  
### <a name="migrating-from-unityvs-to-visual-studio-tools-for-unity"></a>Migrar do UnityVS para as Ferramentas do Visual Studio para Unity  
 Caso esteja migrando do UnityVS para as Ferramentas do Visual Studio para Unity, será necessário gerar novas soluções do Visual Studio para os projetos do Unity.  
  
##### <a name="to-migrate-your-unity-project-from-unityvs-18-to-visual-studio-tools-for-unity-19"></a>Migrar um projeto do Unity do UnityVS 1.8 para as Ferramentas do Visual Studio para Unity 1.9  
  
1.  Exclua a solução e os arquivos de projeto antigos do projeto do Unity. No diretório raiz do projeto do Unity, localize os arquivos .sln e .*proj do Visual Studio e exclua todos eles.  
  
2.  Importe as Ferramentas do Visual Studio para Unity para o pacote do Unity no projeto do Unity. Para obter informações sobre como importar o pacote VSTU, consulte Configurar as Ferramentas do Visual Studio para Unity na página [Introdução](../cross-platform/getting-started-with-visual-studio-tools-for-unity.md).  
  
3.  Gerar novas soluções e arquivos de projeto. Caso deseje gerá-los neste momento, escolha **Ferramentas do Visual Studio** e **Gerar Arquivos de Projeto** no menu principal do Editor do Unity. Caso contrário, é possível ignorar essa etapa; as Ferramentas do Visual Studio para Unity gerarão os novos arquivos automaticamente quando você escolher **Ferramentas do Visual Studio** e **Abrir no Visual Studio**.  
  
### <a name="visual-studio-wont-load-the-solution-that-visual-studio-tools-for-unity-created"></a>O Visual Studio não carregará a solução criada pelas Ferramentas do Visual Studio para Unity  
 Para obter mais informações, consulte [a resposta para essa pergunta do stackoverflow](http://stackoverflow.com/a/24035907/36702).  
  
### <a name="on-windows-8-visual-studio-asks-to-download-the-unity-target-framework"></a>No Windows 8, o Visual Studio solicita o download da estrutura de destino do Unity  
 O UnityVS requer o .NET Framework 3.5, que não é instalado por padrão no Windows 8. Para corrigir esse problema, siga as instruções para baixar e instalar o .NET Framework 3.5.  
  
## <a name="known-issues"></a>Problemas Conhecidos  
 Há problemas conhecidos nas Ferramentas do Visual Studio para Unity, decorrentes de como o depurador interage com a versão mais antiga do compilador C# do Unity. Estamos trabalhando para corrigi-los, mas você pode enfrentar os seguintes problemas nesse meio tempo.  
  
-   O Unity pode falhar durante a depuração.  
  
-   O Unity pode congelar durante a depuração.  
  
-   A intervenção ou saída de métodos pode se comportar incorretamente, especialmente em iteradores ou em instruções switch.  
  
## <a name="reporting-errors"></a>Erros de relatório  
 Ajude-nos a melhorar a qualidade das Ferramentas do Visual Studio para Unity enviando relatórios de erro quando ocorrerem falhas, congelamentos ou outros erros. Isso nos ajuda a investigar e corrigir problemas nas Ferramentas do Visual Studio para Unity. Obrigado!  
  
### <a name="how-to-report-an-error-when-visual-studio-freezes"></a>Como relatar um erro quando o Visual Studio congela  
 Há relatórios que indicam que, às vezes, o Visual Studio congela ao depurar com as Ferramentas do Visual Studio para Unity, mas precisamos de mais dados para entender esse problema. Ajude-nos a investigá-lo seguindo as etapas abaixo.  
  
##### <a name="to-report-that-visual-studio-freezes-while-debugging-with-visual-studio-tools-for-unity"></a>Para relatar que o Visual Studio congela durante a depuração com as Ferramentas do Visual Studio para Unity  
  
1. Abra uma nova instância do Visual Studio.  
  
2. Abra o diálogo Anexar ao Processo. Na nova instância do Visual Studio, escolha **Depurar** e **Anexar ao Processo** no menu principal.  
  
3. Anexe o depurador à instância congelada do Visual Studio. No diálogo **Anexar ao Processo**, selecione a instância congelada do Visual Studio na tabela **Processos Disponíveis** e, em seguida, escolha o botão **Anexar**.  
  
4. Pause o Depurador. Na nova instância do Visual Studio, escolha **Depurar**, **Interromper Tudo** no menu principal ou pressione **Ctrl+Alt+Break**.  
  
5. Crie um despejo de thread. Na janela Comando, digite o comando a seguir e pressione **Enter**.  
  
   ```powershell  
   Debug.ListCallStack /AllThreads /ShowExternalCode  
   ```  
  
    Talvez seja necessário tornar a janela **Comando** visível primeiro. No Visual Studio, escolha **Exibir**, **Outras Janelas**, **janela Comando** no menu principal.  
  
6. Por fim, envie o despejo de thread para [vstusp@microsoft.com](mailto:vstusp@microsoft.com), junto com uma descrição do que você estava fazendo quando o Visual Studio congelou.

