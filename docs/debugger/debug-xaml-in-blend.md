---
title: Depurar XAML no Blend | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 29a37182-2a2c-47e4-a4a9-2d5412738fed
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: f2fa98a1e737ca06cc9b190da349b6e735dcb7df
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49838953"
---
# <a name="debug-xaml-in-blend"></a>Depurar XAML no Blend
Você pode usar as ferramentas no [!INCLUDE[blend_first](../debugger/includes/blend_first_md.md)] para depurar o XAML em seu aplicativo. Quando você compila um projeto, todos os erros são exibidos na **resultados** painel. Clique duas vezes em um erro para localizar a marcação relacionada ao erro. Se você precisar de mais espaço de trabalho, você pode ocultar a **resultados** painel pressionando F12.  

## <a name="syntax-errors"></a>Erros de sintaxe  
 Erros de sintaxe ocorrem quando o XAML ou os arquivos code-behind não seguem as regras de formatação do idioma. A descrição do erro pode ajudar você a entender como corrigi-lo. A lista também especifica o nome do arquivo e o número da linha em que se encontra o erro. Erros XAML são listados na **marcação** guia o **resultados** painel.  

> [!TIP]
>  XAML é uma linguagem de marcação baseada em XML e segue as regras de sintaxe XML.  

 Algumas causas comuns de erros de sintaxe XAML são:  

- Uma palavra-chave com erro de ortografia ou de capitalização.  

- Aspas faltando ao redor de atributos ou cadeias de caracteres de texto.  

- Está faltando um elemento XAML em uma marca de fechamento.  

- Um elemento XAML existe em um local onde não é permitido.  

  Para obter mais informações sobre a sintaxe XAML comuns, consulte [guia de sintaxe XAML básica](http://go.microsoft.com/fwlink/?LinkId=329942).  

  Você também pode identificar e resolver erros de sintaxe code-behind simples, erros de compilação e de tempo de execução no [!INCLUDE[blend_subs](../debugger/includes/blend_subs_md.md)]. No entanto, os erros de code-behind podem ser mais fáceis de identificar e resolver no Visual Studio.  

### <a name="debugging-sample-xaml-code"></a>Depurando código XAML de exemplo  
 O exemplo a seguir detalhará a uma sessão de depuração XAML simples no [!INCLUDE[blend_subs](../debugger/includes/blend_subs_md.md)].  

##### <a name="to-create-a-project"></a>Para criar um projeto  

1. Na [!INCLUDE[blend_subs](../debugger/includes/blend_subs_md.md)], abra o **arquivo** menu e, em seguida, clique **novo projeto**.  

    No **novo projeto** caixa de diálogo, uma lista de tipos de projeto aparece no lado esquerdo. Quando você clica em um tipo de projeto, os modelos de projeto associados a ele aparecem do lado direito.  

2. Na lista de tipos de projeto, clique em **Universal do Windows**.  

3. Na lista de modelos de projeto, clique em **aplicativo em branco (Universal Windows)**.  

4. No **nome** caixa de texto, digite `DebuggingSample`.  

5. No **local** texto, verifique se o local do projeto.  

6. No **linguagem** , clique em **Visual c#** e, em seguida, clique em **Okey** para criar o projeto.  

7. Clique com botão direito na superfície de design e, em seguida, clique em **Exibir código-fonte** para alternar para o **divisão** modo de exibição.  

8. Copie o código a seguir clicando o **cópia** link no canto superior direito do código.  

   ```xml
   <Grid HorizontalAlignment="Left" Height="222" VerticalAlignment="Top>  
        <Button content="Button" x:Mame="Home" HorizontalAlignment="Left" VerticalAlignment="Top"/>  
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,38,0,0">  
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,75,0,0"/>  
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,112,0,0"/>  
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top Margin="0,149,0,0"/>  
   </Grid>  
   ```  

9. Localize o padrão **grade**e cole o código entre a abertura e fechamento **grade** marcas. Quando você terminar, seu código deverá parecer como este:  

    ```xml
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

    Uma mensagem de erro aparece alertando que o projeto não pode ser criado, e o **resultados** listando os erros de painel aparece na parte inferior do aplicativo.  

    ![Depurar XAML no Blend para Visual Studio](../debugger/media/blend_debugxaml_xaml.png "blend_debugXAML_XAML")  

### <a name="resolving-xaml-errors"></a>Resolvendo erros de XAML  
 Quando são detectados erros de XAML, a superfície de design exibe um alerta informando que seu projeto contém marcação inválida. Como resolver os erros, a lista de erros na **resultados** painel é atualizado. Quando você tiver resolvido todos os erros, a superfície de design é habilitada e seu aplicativo é exibido na superfície de design.  

##### <a name="to-resolve-the-xaml-errors"></a>Para resolver os erros de XAML  

1. Clique duas vezes no primeiro erro da lista. A descrição é "O valor '<' não é um válido em um atributo". Quando você clica duas vezes no erro, o ponteiro encontra o local correspondente no código. O `<` que precede `Button` é válido e não um atributo, conforme sugerido na mensagem de erro. Se você observar a linha de código precedente, notará que as marcas de aspas de fechamento para o atributo `Top` estão faltando. Digite as marcas de aspas de fechamento. Observe que a lista de erros na **resultados** painel será atualizado para refletir as alterações.  

2. Clique duas vezes a descrição "'0' não é válido no início de um nome." `Margin="0,149,0,0"` parece estar bem formada. No entanto, observe que a codificação de cor da `Margin` não corresponde a outras instâncias de `Margin` no código. Como as marcas de cotação de fechamento estão faltando do par de nome/valor precedente (`VerticalAlignment="Top`), `Margin="` que é lido como parte do valor do atributo precedente, e 0 é lido como o início de um par de nome/valor. Digite as marcas de aspas de fechamento para `Top`. A lista de erros na **resultados** painel será atualizado para refletir as alterações.  

3. Clique duas vezes no erro restante, "A marcação XML de fechamento 'Button' é discrepante." O ponteiro está localizado em fechamento **grade** marca (`</Grid>`), sugerindo que o erro está dentro do `Grid` objeto. Observe que o segundo objeto `Button` está sem a marcação de fechamento. Depois de adicionar o fechamento `/`, o **resultados** painel lista é atualizada. Agora que esses erros iniciais foram resolvidos, dois erros adicionais foram identificados.  

4. Clique duas vezes em "O membro 'content' não é reconhecido nem acessível." O `c` em `content` deve estar em maiúsculas. Substitua o "c" minúsculo pelo "c" maiúsculo.  

5. Clique duas vezes em "a propriedade 'Mame' não existe no '<http://schemas.microsoft.com/winfx/2006/xaml>' namespace." O "M" em "Mame" deve ser um "N." Substitua o "M" com um "N". Agora que o XAML pode ser analisado, o aplicativo aparece na superfície de design.  

    ![Depurar XAML no Blend para Visual Studio](../debugger/media/blend_debugartboard_xaml.png "blend_debugArtboard_XAML")  

    Pressione Ctrl+Shift+B para compilar um projeto e confirmar que não há restam erros.  

## <a name="debugging-in-visual-studio"></a>Depurando no Visual Studio  
 Você pode abrir projetos do [!INCLUDE[blend_subs](../debugger/includes/blend_subs_md.md)] no Visual Studio para depurar o código de maneira mais fácil em seu aplicativo. Para abrir um [!INCLUDE[blend_subs](../debugger/includes/blend_subs_md.md)] do projeto no Visual Studio, clique com botão direito no projeto na **projetos** do painel e, em seguida, clique em **Editar no Visual Studio**. Quando você encerrar sua sessão de depuração no Visual Studio, pressione Ctrl+Shift+S para salvar todas as mudanças e voltar para o [!INCLUDE[blend_subs](../debugger/includes/blend_subs_md.md)]. Você será solicitado a recarregar o projeto. Clique em **Sim para tudo** para continuar trabalhando no [!INCLUDE[blend_subs](../debugger/includes/blend_subs_md.md)].  

 Para obter mais informações sobre como depurar seu aplicativo, consulte [aplicativos de UWP de depuração no Visual Studio](http://go.microsoft.com/fwlink/?LinkId=329944).  

## <a name="getting-help"></a>Obtendo ajuda  
 Se você precisar de mais ajuda para depurar seus [!INCLUDE[blend_subs](../debugger/includes/blend_subs_md.md)] aplicativo, você pode pesquisar os [fóruns da comunidade UWP](http://go.microsoft.com/fwlink/?LinkId=280308) para postagens relacionadas ao seu problema ou postar uma pergunta.
