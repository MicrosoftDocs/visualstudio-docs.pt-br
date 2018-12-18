---
title: Definir um personalizado item de caixa de ferramentas de modelagem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML - extending, customizing the toolbox
ms.assetid: a2463606-1100-40ac-97f3-5ba22ca47b7c
caps.latest.revision: 33
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: dcb562eb76e13b5dcb16532ed808b2447de0d6c8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51778404"
---
# <a name="define-a-custom-modeling-toolbox-item"></a>Definir um item de caixa de ferramentas de modelagem personalizado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para tornar mais fácil criar um elemento ou um grupo de elementos de acordo com um padrão que você normalmente usa, você pode adicionar novas ferramentas para a caixa de ferramentas de diagramas de modelagem no Visual Studio. Você pode distribuir esses itens de caixa de ferramentas para outros usuários do Visual Studio.  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
 Uma ferramenta personalizada cria um ou mais novos elementos em um diagrama. Por exemplo, você poderia fazer uma ferramenta personalizada para criar elementos como estes:  
  
-   Um pacote é vinculado ao perfil do .NET e uma classe com o estereótipo do .NET.  
  
-   Um par de classes vinculadas por uma associação para representar o padrão de observador.  
  
> [!NOTE]
>  Você pode usar esse método para criar ferramentas de elemento. Ou seja, você pode criar ferramentas que podem ser arrastadas da caixa de ferramentas para um diagrama. Você não pode criar ferramentas de conector.  
  
##  <a name="DefineTool"></a> Definindo um ferramenta de modelagem personalizado  
  
#### <a name="to-define-a-custom-modeling-tool"></a>Para definir uma ferramenta de modelagem personalizado  
  
1.  Crie um diagrama UML que contém um elemento ou um grupo de elementos.  
  
    -   Esses elementos podem ter relações entre eles e podem ter elementos subsidiários, como portas, atributos, operações ou pinos.  
  
2.  Salve o diagrama usando o nome que você deseja dar a nova ferramenta. Sobre o **arquivo** menu, use **salvar... Como**.  
  
3.  Usando o Windows Explorer, copie os arquivos de dois diagrama para a pasta a seguir ou qualquer subpasta:  
  
     *YourDocuments* **\Visual Studio\Architecture Tools\Custom Toolbox Items**  
  
    -   Crie essa pasta se ela ainda não existir. Talvez você precise criar ambos **ferramentas de arquitetura** e **itens de caixa de ferramentas personalizado**.  
  
    -   Copie os dois arquivos de diagrama, uma com um nome que termina em..." **diagrama**"e o outro com um nome que termina"... **diagram.layout**"  
  
    -   Você pode fazer tantas ferramentas personalizadas como desejar. Use um diagrama para cada ferramenta.  
  
4.  (Opcional) Criar uma **.tbxinfo** do arquivo conforme descrito em [como definir as propriedades de ferramentas personalizado](#tbxinfo)e adicione-o no mesmo diretório. Isso permite que você definir um ícone da caixa de ferramentas, Dica de ferramenta e assim por diante.  
  
    -   Uma única **.tbxinfo** arquivo pode ser usado para definir várias ferramentas. Ele pode se referir a arquivos de diagrama que estão em subpastas.  
  
5.  Reinicie o Visual Studio. A ferramenta adicional será exibida na caixa de ferramentas para o tipo apropriado de diagrama.  
  
### <a name="what-the-custom-tool-will-replicate"></a>A ferramenta personalizada que replicará  
 Uma ferramenta personalizada replicará a maioria dos recursos do diagrama de origem:  
  
- Nomes. Quando um item é criado na caixa de ferramentas, um número é adicionado ao final do nome, se necessário, para evitar nomes duplicados no mesmo namespace.  
  
- As cores, tamanhos e formas  
  
- Estereótipos e perfis de pacote  
  
- Valores de propriedade, como é abstrato  
  
- Itens de trabalho vinculados  
  
- Multiplicidades e outras propriedades de relações  
  
- As posições relativas das formas.  
  
  Os recursos a seguir não serão preservados em uma ferramenta personalizada:  
  
- Formas simples. Essas são formas que não estão relacionadas a elementos de modelo que você pode desenhar em alguns tipos de diagramas.  
  
- Conector de roteamento. Se você rotear conectores manualmente, o roteamento não será preservado quando a ferramenta é usada. As posições de algumas formas aninhadas, por exemplo, portas, não são preservadas em relação a seus proprietários.  
  
##  <a name="tbxinfo"></a> Como definir as propriedades de ferramentas personalizadas  
 Informações de uma caixa de ferramentas (**.tbxinfo**) arquivo permite que você especifique um nome de caixa de ferramentas, o ícone, a dica de ferramenta, a guia e ajudar a palavra-chave para um ou mais ferramentas personalizadas. Dê a ele qualquer nome, como **MyTools.tbxinfo**.  
  
 A forma geral do arquivo é da seguinte maneira:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<customToolboxItems xmlns="http://schemas.microsoft.com/visualstudio/[version]/ArchitectureTools/CustomToolboxItems">  
  <customToolboxItem fileName="MyObserverTool.classdiagram">  
    <displayName>  
       <value>Observer Pattern</value>  
    </displayName>  
    <tabName>  
       <value>UML Class Diagram</value>  
    </tabName>  
    <image><bmp fileName="ObserverPatternIcon.bmp"/></image>  
    <f1Keyword>  
      <value>ObserverPatternHelp</value>  
    </f1Keyword>  
    <tooltip>  
       <value>Create a pair of classes</value>  
    </tooltip>  
  </customToolboxItem>  
</customToolboxItems>  
```  
  
 O valor de cada item pode ser:  
  
- Conforme mostrado no exemplo, `<bmp fileName="…"/>` para o ícone da caixa de ferramentas e `<value>string</value>` para os outros itens.  
  
  \- ou -  
  
- `<resource fileName="Resources.dll"`  
  
   `baseName="Observer.resources" id="Observer.tabname" />`  
  
   Nesse caso, você pode fornecer um assembly compilado na qual os valores de cadeia de caracteres tiverem sido compilados como recursos.  
  
  Adicionar um `<customToolboxItem>` nó para cada item de caixa de ferramentas que você deseja definir.  
  
  Os nós a **.tbxinfo** arquivo são da seguinte maneira. Há um valor padrão para cada nó.  
  
|Nome do nó|Define|  
|---------------|-------------|  
|displayName|O nome do item da caixa de ferramentas.|  
|tabName|Guia de caixa de ferramentas na qual o item deve aparecer. Você pode especificar o nome da guia regular para este tipo de diagrama ou um nome separado.|  
|imagem|O local do bitmap (**bmp**) o arquivo, que deve ter a altura e largura de 16 e uma profundidade de cor de 24 bits.|  
|f1Keyword|A palavra-chave que localiza um tópico da Ajuda.|  
|Dica de ferramenta|Uma dica de ferramenta para essa ferramenta.|  
  
 Você pode editar o arquivo de bitmap no Visual Studio e defina sua altura e largura para 16 na janela Propriedades.  
  
> [!NOTE]
>  Se você começar a usar um arquivo .tbxinfo depois de testar usando arquivos de diagrama por conta própria, você poderá achar que a caixa de ferramentas contém as antigas e novas versões de um item de caixa de ferramentas. Isso também pode ocorrer se o nome do arquivo de diagrama foi digitado incorretamente no arquivo .tbxinfo. Se isso ocorrer, no menu de atalho da caixa de ferramentas escolher **caixa de ferramentas de redefinição de**. Os itens de caixa de ferramentas personalizado desaparecerá. Reinicie o Visual Studio, e os itens corretos de personalizada serão exibida.  
  
##  <a name="Extension"></a> Como distribuir itens de caixa de ferramentas em uma extensão do Visual Studio  
 Você pode distribuir itens de caixa de ferramentas para outro [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] usuários por agrupá-las em um Visual Studio VSIX (extensão). Você pode empacotar os comandos, perfis e outras extensões no mesmo arquivo VSIX. Para obter mais informações, consulte [Implantando extensões do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=160780).  
  
 Da maneira usual para compilar uma extensão do Visual Studio é usar o modelo de projeto do VSIX. Para fazer isso, você deve ter instalado [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)].  
  
#### <a name="to-add-a-toolbox-item-to-a-visual-studio-extension"></a>Para adicionar um Item de caixa de ferramentas para uma extensão do Visual Studio  
  
1.  [Criar e testar um ou mais ferramentas personalizadas](#DefineTool).  
  
2.  [Crie um arquivo .tbxinfo](#tbxinfo) que referencia as ferramentas.  
  
3.  Abra um projeto de extensão existente do Visual Studio.  
  
     \- ou -  
  
     Defina um novo projeto de extensão do Visual Studio.  
  
    1.  No menu **Arquivo**, escolha **Novo**, **Projeto**.  
  
    2.  No **novo projeto** caixa de diálogo **modelos instalados**, escolha **Visual c#**, **extensibilidade**, **VSIX projeto**.  
  
4.  Adicione suas definições de caixa de ferramentas para o projeto. Incluir o **.tbxinfo** de arquivos, os arquivos de diagrama, arquivos de bitmap e quaisquer arquivos de recurso e certifique-se de que eles são incluídos no VSIX.  
  
    -   No Gerenciador de soluções, no menu de atalho do projeto VSIX, escolha **Add**, **Item existente**. Na caixa de diálogo, defina **objetos do tipo: todos os arquivos**. Localize os arquivos, selecione todas elas e, em seguida, escolha **adicionar**.  
  
        > [!NOTE]
        >  Neste projeto, você não pode abrir os arquivos de diagrama no editor de modelo.  
  
5.  Defina as seguintes propriedades de todos os arquivos que você acabou de adicionar. Você pode definir suas propriedades ao mesmo tempo, selecionando-os todos em Gerenciador de soluções. Tenha cuidado para não alterar as propriedades de outros arquivos no projeto.  
  
     **Copiar para diretório de saída** = **sempre copiar**  
  
     **Ação de Build** = **conteúdo**  
  
     **Incluir no VSIX** = **true**  
  
6.  Abra **vsixmanifest**. Ele é aberto no editor de manifesto de extensão.  
  
7.  Sob **metadados**, adicione uma descrição para as ferramentas personalizadas.  
  
     Sob **ativos**, escolha **New** e, em seguida, defina os campos na caixa de diálogo da seguinte maneira:  
  
    -   **Tipo de** = **tipo de extensão personalizada**  
  
    -   Tipo = `Microsoft.VisualStudio.ArchitectureTools.CustomToolboxItems`  
  
        > [!NOTE]
        >  Isso não é uma das opções na lista suspensa. Você tem para inseri-la usando o teclado.  
  
    -   **Código-fonte** = **arquivo no sistema de arquivos**.  
  
    -   **Caminho** = sua **.tbxinfo** de arquivo, por exemplo **MyTools.tbxinfo**  
  
8.  Compile o projeto.  
  
9. **Para verificar se a extensão funciona**, pressione F5. A instância experimental do Visual Studio é iniciado.  
  
     Na instância experimental, crie ou abra um diagrama UML do tipo relevante. Verifique se que sua nova ferramenta aparece na caixa de ferramentas e que ele cria elementos corretamente.  
  
10. **Para obter um arquivo VSIX para implantação:** no Windows Explorer, abra a pasta **.\bin\Debug** ou **.\bin\Release** para localizar o **VSIX** arquivo. Esse é um [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] arquivo de extensão. Ele pode ser instalado em seu computador e também é enviado a outros usuários do Visual Studio.  
  
#### <a name="to-install-custom-tools-from-a-visual-studio-extension"></a>Para instalar ferramentas personalizadas de uma extensão do Visual Studio  
  
1.  Abra o `.vsix` arquivo no Windows Explorer ou no Visual Studio.  
  
2.  Escolher **instalar** na caixa de diálogo que aparece.  
  
3.  Para desinstalar ou desabilitar temporariamente a extensão, abra **extensões e atualizações** da **ferramentas** menu.  
  
## <a name="localization"></a>Localização  
 Você pode tornar uma extensão que, quando ele é instalado em outro computador, exibirá os nomes de ferramenta e dicas de ferramentas no idioma do computador de destino.  
  
#### <a name="to-provide-versions-of-the-tool-in-more-than-one-language"></a>Para fornecer versões da ferramenta em mais de um idioma  
  
1. Crie um projeto de extensão do Visual Studio que contém um ou mais ferramentas personalizadas.  
  
    No **.tbxinfo** do arquivo, use o método de arquivo de recurso para definir a ferramenta `displayName`, caixa de ferramentas `tabName`e a dica de ferramenta. Criar um arquivo de recurso no qual essas cadeias de caracteres são definidas, compilá-lo em um assembly e fazer referência a ele partir do arquivo tbxinfo.  
  
2. Crie assemblies adicionais que contêm arquivos de recurso com cadeias de caracteres em outros idiomas.  
  
3. Coloque cada assembly adicional em uma pasta cujo nome é o código de cultura para o idioma. Por exemplo, coloque uma versão em francês do assembly dentro de uma pasta denominada **fr**.  
  
4. Você deve usar um código de cultura neutra, normalmente com duas letras, não uma cultura específica, como `fr-CA`. Para obter mais informações sobre códigos de cultura, consulte [método CultureInfo GetCultures](http://go.microsoft.com/fwlink/?LinkId=160782), que fornece uma lista completa dos códigos de cultura.  
  
5. Compile a extensão do Visual Studio e distribuí-lo.  
  
6. Quando a extensão está instalada em outro computador, a versão do arquivo de recurso para a cultura do usuário local será carregada automaticamente. Se você não tiver fornecido uma versão para a cultura do usuário, os recursos padrão serão usados.  
  
   Você não pode usar esse método para instalar versões diferentes do diagrama de protótipo. Os nomes de elementos e conectores serão a mesma em todas as instalações.  
  
## <a name="other-toolbox-operations"></a>Outras operações de caixa de ferramentas  
 Normalmente, no [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)], você pode personalizar a caixa de ferramentas por ferramentas de renomeação, movendo-os para as guias da caixa de ferramentas diferentes e excluí-los. Mas essas alterações não serão mantidas para ferramentas de modelagem personalizado criadas com os procedimentos descritos neste tópico. Quando você reinicia [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)], reaparecerão ferramentas personalizadas com seus nomes definidos e os locais de caixa de ferramentas.  
  
 Além disso, suas ferramentas personalizadas desaparecerá se você executar o **caixa de ferramentas de redefinição de** comando. No entanto, eles reaparecerá quando você reiniciar [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)   
 [Definir um perfil para estender UML](../modeling/define-a-profile-to-extend-uml.md)   
 [Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)   
 [Definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md)



