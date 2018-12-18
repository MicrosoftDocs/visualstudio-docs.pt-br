---
title: Criando tabela de comando XML (. Arquivos VSCT) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VSCT files, designing
ms.assetid: bb87a322-bac4-4258-92bc-9a876f05d653
caps.latest.revision: 28
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6c7a4e07c45c5d651af057e1eb33c23d37601cb3
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51762816"
---
# <a name="designing-xml-command-table-vsct-files"></a>Criando tabela de comando XML (. Arquivos de VSCT)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um arquivo de tabela (. VSCT) do comando XML descreve o layout e aparência de itens de comando para um VSPackage. Itens de comando incluem caixas de combinação, botões, menus, barras de ferramentas e grupos de itens de comando. Este tópico descreve arquivos de tabela de comandos XML, como eles afetam os menus e itens de comando e como criá-los.  
  
## <a name="commands-menus-groups-and-the-vsct-file"></a>Comandos, Menus, grupos e o arquivo. VSCT  
 arquivos. VSCT são organizados em torno de comandos, menus e grupos de comando. Marcas XML no arquivo. VSCT representam cada um desses itens, juntamente com outros itens associados, como botões de comando, o posicionamento de comando e bitmaps.  
  
 Quando você cria um novo VSPackage, executando o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] modelo de pacote, o modelo gera um arquivo. VSCT com os elementos necessários para um comando de menu, a janela da ferramenta ou o editor personalizado, dependendo de suas seleções. Esse arquivo. VSCT, em seguida, pode ser modificado para atender aos requisitos de um VSPackage específico. Para obter exemplos de como modificar um arquivo. VSCT, consulte os exemplos [estendendo Menus e comandos](../../extensibility/extending-menus-and-commands.md).  
  
 Para criar um arquivo. VSCT em branco, consulte [como: criar um. Arquivo VSCT](../../extensibility/internals/how-to-create-a-dot-vsct-file.md). Depois de criar, adicionar elementos, atributos e valores XML para o arquivo para descrever o layout do item de comando. Para um esquema XML detalhado, consulte o [referência de esquema de XML do VSCT](../../extensibility/vsct-xml-schema-reference.md).  
  
## <a name="differences-between-ctc-and-vsct-files"></a>Diferenças entre arquivos. ctc e. VSCT  
 Enquanto o significado por trás de marcas XML em um arquivo. VSCT é os mesmos, como aqueles em que o agora preterido o formato de arquivo. CTC, sua implementação é um pouco diferente.  
  
- O novo  **\<extern >** marca é onde você pode referenciar outros arquivos. h para ser compilado, como aquelas para o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] barra de ferramentas.  
  
- Embora o suporte a arquivos. VSCT a **/include** instrução, como arquivos. CTC, ele também apresenta uma nova \< **Importar >** elemento. A diferença é que **/include** traz **todos os** da informação, mas \< **Importar >** traz apenas os nomes.  
  
- Enquanto os arquivos. ctc exigem um arquivo de cabeçalho no qual você define suas diretivas de pré-processador, um não é necessário para os arquivos. VSCT. Em vez disso, colocar suas diretivas na tabela de símbolo, localizada na  **\<símbolo >** elementos, localizados na parte inferior do arquivo. VSCT.  
  
- recurso de arquivos. VSCT de um  **\<anotação >** marca, que permite que você insira todas as informações que desejar, como anotações ou até mesmo as imagens.  
  
- Valores são armazenados como atributos no item.  
  
- Sinalizadores de comando podem ser armazenadas individualmente ou empilhados.  IntelliSense, no entanto, não funciona em sinalizadores de comando empilhadas. Para obter mais informações sobre os sinalizadores de comando, consulte o [elemento Command Flag](../../extensibility/command-flag-element.md).  
  
- Você pode especificar vários tipos, como listas suspensas de divisão, combos, etc.  
  
- GUIDs não validar.  
  
- Cada elemento de interface do usuário tem uma cadeia de caracteres que representa o texto que é exibido com ele.  
  
- Pai é opcional. Se omitido, o valor "Desconhecido" grupo"é usado.  
  
- O argumento de ícone é opcional.  
  
- A seção de bitmap – o mesmo que um. ctc de arquivo, exceto que agora você pode especificar um nome de arquivo por meio de href que será obtido pelo compilador vsct.exe em tempo de compilação.  
  
- ResID – a ID de recurso de bitmap antigo pode ser usada e ainda funciona da mesma forma como em arquivos. ctc.  
  
- HRef – um novo método que permite que você especifique um nome de arquivo para o recurso de bitmap. Ele pressupõe que são usados, portanto, você pode omitir a seção usada. Primeiro, o compilador pesquisará para recursos locais para o arquivo, em seguida, em qualquer compartilhamento de rede e todos os recursos definidos pelo comutador/i.  
  
- KeyBinding – Você não precisa especificar um emulador. Se você especificar um, o compilador assumirá que o editor e o emulador são os mesmos.  
  
- Keychord – foi descartada. O novo formato é Key1, Mod1, Key2, Mod2.  Você pode especificar um caractere, hexadecimal ou constante VK.  
  
  O novo compilador, vsct.exe, compila arquivos. ctc e. VSCT. O compilador ctc.exe antigo, no entanto, não reconhece nem compilar arquivos. VSCT.  
  
  Você pode usar o compilador vsct.exe para converter um arquivo CTO já existente em um arquivo. VSCT. Para obter mais informações sobre isso, consulte [como: criar um. Arquivo VSCT de um existente. Arquivo CTO](../../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file.md).  
  
## <a name="the-vsct-file-elements"></a>Os elementos do arquivo. VSCT  
 A tabela de comando tem a hierarquia e os elementos a seguir:  
  
 [Elemento CommandTable](../../extensibility/commandtable-element.md) — representa todos os comandos, grupos de menus e menus associados com o VSPackage.  
  
 [Elemento extern](../../extensibility/extern-element.md) — faz referência a todos os arquivos. h externa você deseja mesclar com o arquivo. VSCT.  
  
 [Incluir elemento](../../extensibility/include-element.md) — faz referência a todos os arquivos adicionais de cabeçalho (. h) você deseja compilar juntamente com o arquivo your.vsct. Um arquivo. VSCT pode incluir arquivos. h que contém constantes que definem os comandos, grupos de menus e menus que fornece o IDE ou outro VSPackage.  
  
 [Comandos do elemento](../../extensibility/commands-element.md) — representa todos os comandos individuais que podem ser executados. Cada comando tem os seguintes elementos quatro filho:  
  
 [Elemento menus](../../extensibility/menus-element.md) — representa todos os menus e barras de ferramentas do VSPackage. Menus são contêineres para grupos de comandos.  
  
 [Elemento Groups](../../extensibility/groups-element.md) — representa todos os grupos em VSPackage. Grupos são coleções de comandos individuais.  
  
 [Botões elemento](../../extensibility/buttons-element.md) — representa todos os botões de comando e itens de menu em um VSPackage. Botões são controles visuais que podem ser associados a comandos.  
  
 [Elemento bitmaps](../../extensibility/bitmaps-element.md) — representa todos os bitmaps para todos os botões em VSPackage. Os bitmaps são imagens que são exibidas ao lado ou nos botões de comando, dependendo do contexto.  
  
 [Elemento CommandPlacements](../../extensibility/commandplacements-element.md) — indica mais locais onde os comandos individuais devem ser colocado no local nos menus do VSPackage.  
  
 [Element Visibilityconstraints](../../extensibility/visibilityconstraints-element.md) — especifica ou não um comando em todos os exibe vezes ou somente em determinados contextos, como quando uma caixa de diálogo específica ou a janela é exibida. Menus e comandos que têm um valor para esse elemento serão exibido somente quando o contexto especificado está ativo. O comportamento padrão é exibir o comando em todos os momentos.  
  
 [Elemento KeyBindings](../../extensibility/keybindings-element.md) — Especifica quaisquer associações de teclas para os comandos. Ou seja, um ou mais combinações de teclas que devem ser pressionadas para executar o comando, como **CTRL + S**.  
  
 [Elemento UsedCommands](../../extensibility/usedcommands-element.md) — Informs o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ambiente que, embora o comando especificado é implementado por outro código, quando o VSPackage atual está ativo, ele fornece a implementação do comando.  
  
 `Symbols Element` – Contém os nomes de símbolo e IDs de GUID para todos os seus comandos no pacote.  
  
## <a name="vsct-file-design-guidelines"></a>. Diretrizes de Design do arquivo VSCT  
 Para desenvolver com êxito um arquivo. VSCT, siga estas diretrizes.  
  
-   Comandos podem ser colocados somente em grupos, grupos podem ser colocados somente nos menus e menus podem ser colocados apenas em grupos. Somente os menus, na verdade, são exibidos no IDE, grupos e comandos não são.  
  
-   Submenus não podem ser atribuídos diretamente a um menu, mas devem ser atribuídos a um grupo, que por sua vez é atribuído a um menu.  
  
-   Comandos, submenus e grupos podem ser atribuídos a um grupo de gerenciamento do domínio pai ou menu usando o campo pai da sua diretiva de definição.  
  
-   Organizar uma tabela de comando somente por meio dos campos pai nas diretivas tem uma limitação significativa. As diretivas que definem objetos podem levar o argumento de apenas um pai.  
  
-   Reutilização de comandos, grupos ou submenus requer o uso de uma diretiva de novo para criar uma nova instância do objeto com seu próprio `GUID:ID` par.  
  
-   Cada `GUID:ID` par deve ser exclusivo. Reutilizar um comando que, por exemplo, foi colocado em um menu, uma barra de ferramentas, ou em um menu de contexto, é tratada pelo <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface.  
  
-   Comandos e submenus também podem ser atribuídos a vários grupos e grupos podem ser atribuídos a vários menus usando o [comandos elemento](../../extensibility/commands-element.md).  
  
## <a name="vsct-file-notes"></a>. Notas de arquivo VSCT  
 Se você fizer alterações em um arquivo. VSCT depois de compilá-lo e colocá-lo em uma DLL de satélite nativo, você deve executar **devenv.exe /setup /nosetupvstemplates**. Isso força os recursos de VSPackage especificados no registro experimental para ser lidos novamente e o banco de dados interno que descreve [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] seja recriado.  
  
 Durante o desenvolvimento, é possível que vários projetos de VSPackage seja criado e registrado na seção do registro experimental que pode levar a bagunça confusa no IDE. Para corrigir isso, você pode redefinir o hive experimental para as configurações padrão para remover todos os VSPackages e as alterações que fez o IDE. Para redefinir o hive experimental, use a ferramenta de CreateExpInstance.exe que vem com o SDK do Visual Studio. Você pode encontrá-lo em  
  
 **% PROGRAMFILES (x86) %\Visual Studio \<versão > SDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe**  
  
 Execute a ferramenta usando a linha de comando **CreateExpInstance /Reset**. Lembre-se de que essa ferramenta remove do hive experimental todos os os VSPackages registrados não são normalmente instalados com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Ampliar menus e comandos](../../extensibility/extending-menus-and-commands.md)

