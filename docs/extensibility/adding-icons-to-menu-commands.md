---
title: Adicionando ícones a comandos de Menu | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- icons [Visual Studio], adding to toolbars
- toolbars [Visual Studio], adding icons to commands
- commands [Visual Studio], adding icons
ms.assetid: 362a0c7e-5729-4297-a83f-1aba1a37fd44
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 0d01e64915004eb21a92c21a67291dc4f034112d
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39154999"
---
# <a name="add-icons-to-menu-commands"></a>Adicionar ícones a comandos de menu
Comandos podem aparecer nos menus e barras de ferramentas. Na barra de ferramentas, é comum para um comando a ser exibido com apenas um ícone (para economizar espaço) ao mesmo tempo nos menus de que um comando normalmente aparece com um ícone e o texto.  
  
 Ícones são 16 pixels de largura por 16 pixels de altura e podem ser a intensidade de cor de 8 bits (256 cores) ou a profundidade de cor de 32 bits (cor true). ícones de cores de 32 bits são preferidos. Ícones normalmente são organizados em uma única linha horizontal em um único bitmap, embora vários bitmaps são permitidos. Esse bitmap é declarado na *VSCT* arquivo juntamente com os ícones individuais disponíveis no bitmap. Consulte a referência para o [elemento Bitmaps](../extensibility/bitmaps-element.md) para obter mais detalhes.  
  
## <a name="add-an-icon-to-a-command"></a>Adicionar um ícone para um comando  
 O procedimento a seguir pressupõe que você tenha um projeto de VSPackage existente com um comando de menu. Para saber como fazer isso, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
1.  Crie um bitmap com uma profundidade de cor de 32 bits. Um ícone é sempre um múltiplo de 16 pixels de largura e de 16 x 16 para que este bitmap deve ser 16 pixels de altura.  
  
     Cada ícone é colocado no bitmap próximos uns dos outros em uma única linha. Use o canal alfa para indicar casas de transparência em cada ícone.  
  
     Se você usar uma profundidade de cor de 8 bits, use o magenta, `RGB(255,0,255)`, como a transparência. No entanto, os ícones de cores de 32 bits são preferidos.  
  
2.  Copie o arquivo de ícone para o *recursos* diretório em seu projeto de VSPackage. No **Gerenciador de soluções**, adicionar o ícone para o projeto. (Selecione **recursos**e no menu de contexto, clique em **Add**, em seguida, **Item existente**e selecione o arquivo de ícone.)  
  
3.  Abra o *VSCT* arquivo no editor.  
  
4.  Adicionar um `GuidSymbol` elemento com um nome de **testIcon**. Criar um GUID (**ferramentas** > **criar GUID**, em seguida, selecione **formato de registro** e clique em **cópia**) e cole-o `value` atributo. O resultado deve ter esta aparência:  
  
    ```xml  
    <!-- Create your own GUID -->  
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">  
    ```  
  
5.  Adicionar um `<IDSymbol>` para o ícone. O `name` atributo é a ID do ícone e o `value` indica sua posição na fita, se houver. Se houver apenas um ícone, adicione 1. O resultado deve ter esta aparência:  
  
    ```xml  
    <!-- Create your own GUID -->  
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">  
        <IDSymbol name="testIcon1" value="1" />  
    </GuidSymbol>  
    ```  
  
6.  Criar uma `<Bitmap>` no `<Bitmaps>` seção o *. VSCT* arquivo para representar o bitmap que contém os ícones.  
  
    -   Defina as `guid` valor para o nome da `<GuidSymbol>` elemento que você criou na etapa anterior.  
  
    -   Defina as `href` valor para o caminho relativo do arquivo de bitmap (nesse caso **recursos\\< nome do arquivo de ícone\>**.  
  
    -   Defina o `usedList` valor para o IDSymbol que você criou anteriormente. Esse atributo especifica uma lista delimitada por vírgulas dos ícones para ser usado em um VSPackage. Ícones não está na lista são excluídos do formulário de compilação.  
  
         O bloco de Bitmap deve ter esta aparência:  
  
        ```xml  
        <Bitmap guid="testIcon" href="Resources\<icon file name>" usedList="testIcon1"/>  
        ```  
  
7.  Existentes `<Button>` elemento, defina o `Icon` elemento com os valores de GUIDSymbol e IDSymbol que você criou anteriormente. Aqui está um exemplo de um elemento de botão com esses valores:  
  
    ```xml  
    <Button guid="guidAddIconCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">  
        <Parent guid="guidAddIconCmdSet" id="MyMenuGroup" />  
        <Icon guid="testIcon" id="testIcon1" />  
        <Strings>  
            <ButtonText>My Command name</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
8.  Teste seu ícone. Compile o projeto e comece a depuração. Na instância experimental, encontre o comando. Ele deve mostrar o ícone que você adicionou.  
  
## <a name="see-also"></a>Consulte também  
 [Ampliar menus e comandos](../extensibility/extending-menus-and-commands.md)   
 [Referência de esquema XML do VSCT](../extensibility/vsct-xml-schema-reference.md)