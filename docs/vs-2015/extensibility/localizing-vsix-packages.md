---
title: Localizar pacotes VSIX | Microsoft Docs
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
- localize package
- localize extension
- localized deployment
ms.assetid: 10e80b13-b39e-466c-a7c8-774a862355af
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 2f6bc666e244fed2bc2922ce4878434730a643e5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51750594"
---
# <a name="localizing-vsix-packages"></a>Localizando pacotes do VSIX
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode localizar um pacote VSIX criando um arquivo Extension.vsixlangpack para cada idioma de destino e, em seguida, colocando-os na pasta correta. Quando um pacote localizado estiver instalado, o nome localizado da extensão é exibido junto com uma descrição localizada. Se você fornecer um arquivo de licença localizada ou uma URL que aponta para informações localizadas, eles também são exibidos.  
  
 Se o conteúdo do seu pacote do VSIX inclui um VSPackage que adiciona os comandos de menu ou outra interface de usuário, consulte [comandos de Menu Localizando](../extensibility/localizing-menu-commands.md) para obter informações sobre como localizar os novos elementos de interface do usuário.  
  
## <a name="directory-structure"></a>Estrutura de diretórios  
 Quando um usuário instala uma extensão **extensões e atualizações** verifica o nível superior do pacote VSIX para uma pasta cujo nome corresponde à localidade do Visual Studio do computador de destino. Se **extensões e atualizações** localiza um .vsixlangpack de arquivos na pasta, ele substitui os valores localizados no arquivo para os valores correspondentes no arquivo .vsixmanifest. Esses valores são exibidos quando a extensão está sendo instalada. O exemplo a seguir mostra a estrutura de diretório para um pacote VSIX que está localizado em espanhol (es-ES) e francês (fr-FR).  
  
 MyExtension.dll  
  
 vsixmanifest  
  
 [Content_Types]. XML  
  
 es-ES  
  
 Extension.vsixlangpack  
  
 fr-FR  
  
 Extension.vsixlangpack  
  
> [!NOTE]
>  Os modelos de projeto com suporte de VSIX no [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] gerar um manifesto do VSIX e nomeie-o vsixmanifest. Quando o Visual Studio compila o projeto, ele copia o conteúdo desse arquivo para vsixmanifest no pacote VSIX.  
  
## <a name="the-extensionvsixlangpack-file"></a>O arquivo Extension.vsixlangpack  
 O arquivo Extension.vsixlangpack segue o [esquema de pacote de idiomas do VSIX](../extensibility/vsx-language-pack-schema-reference.md). Esse esquema possui um [VSIXLanguagePack](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md) elemento raiz e esses quatro elementos filhos: [LocalizedName](../extensibility/localizedname-element-vsix-language-pack-schema.md), [LocalizedDescription](../extensibility/localizeddescription-element-vsix-language-pack-schema.md), [MoreInfoURL](../extensibility/moreinfourl-element-vsix-language-pack-schema.md), e [licença](../extensibility/license-element-vsix-language-pack-schema.md). Esses elementos filho correspondem para o `Name`, `Description`, `MoreInfoURL`, e `License` elementos filho do `Identifier` elemento do arquivo Extension vsixmanifest.  
  
 Quando você cria um arquivo vsixlangpack, você deve definir a `Include in Vsix` propriedade para `true`. Caso contrário, o texto de instalação localizado será ignorado.  
  
#### <a name="to-set-the-include-in-vsix-property"></a>Para definir a incluir no Vsix propriedade  
  
1.  Na **Gerenciador de soluções**, clique no arquivo Extension.vsixlangpack e, em seguida, clique em **propriedades**.  
  
2.  Na grade de propriedade, clique em **incluir em Vsix**e defina seu valor como `true`.  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 O exemplo a seguir mostra as partes relevantes de um arquivo Extension vsixmanifest, junto com o arquivo Extension.vsixlangpack correspondente para espanhol. Os valores do pacote de idiomas substituem os valores do manifesto, se a localidade do Visual Studio do computador de destino é definida como Spanish.  
  
### <a name="code"></a>Código  
 [Vsixmanifest]  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<VSIX ...>  
  <Identifier ...>  
    <Name>Family Tree</Name>  
    <Description>This extension places a custom treeview control in the toolbox that is optimized for handling family tree information.</Description>  
    <License>EULA.rtf</License>  
    <MoreInfoURL>http://www.contoso.com/products/FamilyTree.htm</MoreInfoURL>  
    ...  
  </Identifier>  
  <References .../>  
  <Content .../>  
</VSIX>  
```  
  
 [Extension.vsixlangpack]  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<VsixLanguagePack Version="1.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema-lp/2010">  
  <LocalizedName>Arbol de Familia</LocalizedName>  
  <LocalizedDescription> Esta extensión pone control personalizado en la caja de herramientas por manejar información de familia.</LocalizedDescription>  
  <License>es\Eula.rtf</License>  
  <MoreInfoUrl> http://www.contoso.com/products/es/ArbolDeFamilia.htm</MoreInfoUrl>  
</VsixLanguagePack>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Elemento do VSIX LanguagePack](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md)   
 [Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)   
 [Modelo de projeto VSIX](../extensibility/vsix-project-template.md)

