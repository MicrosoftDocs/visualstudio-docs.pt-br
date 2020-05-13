---
title: Debug XAML in Blend | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 29a37182-2a2c-47e4-a4a9-2d5412738fed
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8e032f9f99087df26c82b4984c2267a35236bf6e
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81444603"
---
# <a name="debug-xaml-in-blend"></a>Depurar XAML no Blend
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar as ferramentas no [!INCLUDE[blend_first](../includes/blend-first-md.md)] para depurar o XAML em seu aplicativo. Ao compilar um projeto, qualquer erro é exibido no painel **Resultados**. Clique duas vezes em um erro para localizar a marcação relacionada ao erro. Se você precisar de mais espaço para trabalhar, oculte o painel **Resultados** pressionando F12.  
  
## <a name="syntax-errors"></a>Erros de sintaxe  
 Erros de sintaxe ocorrem quando o XAML ou os arquivos code-behind não seguem as regras de formatação do idioma. A descrição do erro pode ajudar a entender como corrigir o problema. A lista também especifica o nome do arquivo e o número da linha em que se encontra o erro. Os erros de XAML são listados na guia **Marcação** do painel **Resultados**.  
  
> [!TIP]
> XAML é uma linguagem de marcação baseada em XML e segue as regras de sintaxe XML.  
  
 Algumas causas comuns de erros de sintaxe XAML são:  
  
- Uma palavra-chave com erro de ortografia ou de capitalização.  
  
- Aspas faltando ao redor de atributos ou cadeias de caracteres de texto.  
  
- Está faltando um elemento XAML em uma marca de fechamento.  
  
- Um elemento XAML está em um local onde não é permitido.  
  
  Para obter mais informações sobre sintaxe XAML comum, confira [Guia de sintaxe XAML básica](https://msdn.microsoft.com/library/windows/apps/hh700351.aspx).  
  
  Você também pode identificar e resolver erros de sintaxe code-behind simples, erros de compilação e de tempo de execução no [!INCLUDE[blend_subs](../includes/blend-subs-md.md)]. No entanto, os erros de code-behind podem ser mais fáceis de identificar e resolver no Visual Studio.  
  
### <a name="debugging-sample-xaml-code"></a>Depurando código XAML de exemplo  
 O exemplo a seguir detalhará a uma sessão de depuração XAML simples no [!INCLUDE[blend_subs](../includes/blend-subs-md.md)].  
  
##### <a name="to-create-a-project"></a>Para criar um projeto  
  
1. No [!INCLUDE[blend_subs](../includes/blend-subs-md.md)], abra o menu **Arquivo** e clique em **Novo Projeto**.  
  
    Na caixa de diálogo **Novo Projeto**, é exibida uma lista de tipos de projetos no lado esquerdo. Quando você clica em um tipo de projeto, os modelos de projeto associados a ele aparecem do lado direito.  
  
2. Na lista de tipos de projetos, clique em **XAML (Windows Store)**.  
  
3. Na lista de modelos de projeto, clique **em Blank App**.  
  
4. Na caixa de texto `DebuggingSample` **Nome,** digite .  
  
5. Na caixa de texto **Localização**, verifique a localização do projeto.  
  
6. Na lista **Linguagem**, clique em **Visual C#** e em **OK** para criar o projeto.  
  
7. Clique com o botão direito do mouse na superfície de design e clique em **Exibir Código-Fonte** para alternar para o modo de exibição **Divisão**.  
  
8. Copie o código a seguir clicando no link **Copiar** no canto superior direito do código.  
  
   ```  
   <Grid HorizontalAlignment="Left" Height="222" VerticalAlignment="Top>  
        <Button content="Button" x:Mame="Home" HorizontalAlignment="Left" VerticalAlignment="Top"/>  
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,38,0,0">  
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,75,0,0"/>  
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,112,0,0"/>  
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top Margin="0,149,0,0"/>  
   </Grid>  
  
   ```  
  
9. Localize o elemento **Grid** padrão e coloque o código entre as marcações **Grid** inicial e final. Quando você terminar, seu código deverá parecer como este:  
  
    ```  
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">  
         <Grid HorizontalAlignment="Left" Height="222" VerticalAlignment="Top>  
              <Button content="Button" x:Mame="Home" HorizontalAlignment="Left" VerticalAlignment="Top"/>  
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,38,0,0">  
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,75,0,0"/>  
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,112,0,0"/>  
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top Margin="0,149,0,0"/>  
         </Grid>  
    </Grid>  
  
    ```  
  
10. Pressione Ctrl+Shift+B para compilar o projeto.  
  
    Uma mensagem de erro aparece alertando você que o projeto não pode ser criado e o painel **Resultados**, listando os erros, aparece na parte inferior do aplicativo.  
  
    ![Depurar XAML no Blend for Visual Studio](../debugger/media/blend-debugxaml-xaml.png "blend_debugXAML_XAML")  
  
### <a name="resolving-xaml-errors"></a>Resolvendo erros de XAML  
 Quando são detectados erros de XAML, a superfície de design exibe um alerta informando que seu projeto contém marcação inválida. À medida que você resolve os erros, a lista de erros no painel **Resultados** é atualizada. Quando você tiver resolvido todos os erros, a superfície de design é habilitada e seu aplicativo é exibido na superfície de design.  
  
##### <a name="to-resolve-the-xaml-errors"></a>Para resolver os erros de XAML  
  
1. Clique duas vezes no primeiro erro da lista. A descrição é "O valor '<' não é um válido em um atributo". Quando você clica duas vezes no erro, o ponteiro encontra o local correspondente no código. O `<` que precede `Button` é válido e não um atributo, conforme sugerido na mensagem de erro. Se você observar a linha de código precedente, notará que as marcas de aspas de fechamento para o atributo `Top` estão faltando. Digite as marcas de aspas de fechamento. Observe que a lista de erros no painel **Resultados** é atualizada de acordo com suas alterações.  
  
2. Clique duas vezes na descrição "'0' não é válido no início de um nome." `Margin="0,149,0,0"`parece estar bem formado. No entanto, observe que a codificação de cor da `Margin` não corresponde a outras instâncias de `Margin` no código. Como as marcas de cotação de fechamento estão faltando do par de nome/valor precedente (`VerticalAlignment="Top`), `Margin="` que é lido como parte do valor do atributo precedente, e 0 é lido como o início de um par de nome/valor. Digite as marcas de aspas de fechamento para `Top`. A lista de erros no painel **Resultados** é atualizada de acordo com suas alterações.  
  
3. Clique duas vezes no erro restante, "A marca XML de fechamento 'Button' é discrepante." O ponteiro está localizado na tag **Grid** de fechamento (`</Grid>`), sugerindo que o erro está dentro do objeto `Grid`. Observe que o segundo objeto `Button` está sem a marcação de fechamento. Depois de adicionar a `/` de fechamento, a lista de painéis dos **Resultados** é atualizada. Agora que esses erros iniciais foram resolvidos, dois erros adicionais foram identificados.  
  
4. Clique duas vezes em "O membro 'content' não é reconhecido nem acessível." O `c` em `content` deve estar em maiúsculas. Substitua o "c" minúsculo pelo "c" maiúsculo.  
  
5. Clique duas vezes em "A propriedade 'Mame' não existe no `https://schemas.microsoft.com/winfx/2006/xaml` namespace." O "M" em "Mame" deve ser um "N." Substitua o "M" com um "N". Agora que o XAML pode ser analisado, o aplicativo aparece na superfície de design.  
  
    ![Depuração de XAML em Blend para Visual Studio](../debugger/media/blend-debugartboard-xaml.png "blend_debugArtboard_XAML")  
  
    Pressione Ctrl+Shift+B para compilar um projeto e confirmar que não há restam erros.  
  
## <a name="debugging-in-visual-studio"></a>Depurando no Visual Studio  
 Você pode abrir projetos do [!INCLUDE[blend_subs](../includes/blend-subs-md.md)] no Visual Studio para depurar o código de maneira mais fácil em seu aplicativo. Para abrir um projeto do [!INCLUDE[blend_subs](../includes/blend-subs-md.md)] no Visual Studio, clique com o botão direito do mouse no projeto no painel **Projetos** e clique em **Editar no Visual Studio**. Quando você encerrar sua sessão de depuração no Visual Studio, pressione Ctrl+Shift+S para salvar todas as mudanças e voltar para o [!INCLUDE[blend_subs](../includes/blend-subs-md.md)]. Você será solicitado a recarregar o projeto. Clique em **Sim para Todos** para continuar trabalhando no [!INCLUDE[blend_subs](../includes/blend-subs-md.md)].  
  
 Para obter mais informações sobre como depurar seu aplicativo, consulte [depurar aplicativos do Windows Store no Visual Studio](https://msdn.microsoft.com/library/windows/apps/hh441472.aspx).  
  
## <a name="getting-help"></a>Obtendo ajuda  
 Se você precisar de mais [!INCLUDE[blend_subs](../includes/blend-subs-md.md)] ajuda para depurar seu aplicativo, você pode procurar nos [fóruns da comunidade](https://social.msdn.microsoft.com/Forums/windowsapps/home?category=windowsapps) de aplicativos da Windows Store para obter postagens relacionadas ao seu problema ou postar uma pergunta.
