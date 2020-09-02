---
title: '&lt;&gt;Elemento PackageFiles (Bootstrapper) | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <PackageFiles> element [bootstrapper]
ms.assetid: 3ea252d7-18a3-47d8-af83-47feebcfe82b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 81a12f400ee870798759237e202d2ca358fefa69
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "66747521"
---
# <a name="ltpackagefilesgt-element-bootstrapper"></a>&lt;&gt;Elemento PackageFiles (Bootstrapper)
O `PackageFiles` elemento contém `PackageFile` elementos, que definem os pacotes de instalação executados como resultado do `Command` elemento.

## <a name="syntax"></a>Sintaxe

```xml
<PackageFiles
    CopyAllPackageFiles
>
    <PackageFile
        Name
        HomeSite
        CopyOnBuild
        PublicKey
        Hash
    />
</PackageFiles>
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O `PackageFiles` elemento tem o atributo a seguir.

|Atributo|Descrição|
|---------------|-----------------|
|`CopyAllPackageFiles`|Opcional. Se definido como `false` , o instalador baixará apenas os arquivos referenciados do `Command` elemento. Se definido como `true` , todos os arquivos serão baixados.<br /><br /> Se definido como `IfNotHomesite` , o instalador se comportará da mesma forma como se `False` `ComponentsLocation` estiver definido como `HomeSite` , e caso contrário se comportará da mesma forma que se `True` . Essa configuração pode ser útil para permitir que pacotes próprios bootstrappers executem seu próprio comportamento em um cenário do HomeSite.<br /><br /> O padrão é `true`.|

## <a name="packagefile"></a>PackageFile
 O `PackageFile` elemento é um filho do `PackageFiles` elemento. Um `PackageFiles` elemento deve ter pelo menos um `PackageFile` elemento.

 `PackageFile` tem os atributos a seguir.

| Atributo | Descrição |
|---------------| - |
| `Name` | Obrigatórios. O nome do arquivo do pacote. Esse é o nome que o `Command` elemento fará referência ao definir as condições sob as quais um pacote é instalado. Esse valor também é usado como uma chave na `Strings` tabela para recuperar o nome localizado que as ferramentas como [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] usarão para descrever o pacote. |
| `HomeSite` | Opcional. O local do pacote no servidor remoto, se não estiver incluído no instalador. |
| `CopyOnBuild` | Opcional. Especifica se o bootstrapper deve copiar o arquivo de pacote para o disco no momento da compilação. O padrão é true. |
| `PublicKey` | A chave pública criptografada do signatário de certificado do pacote. Obrigatório se `HomeSite` for usado; caso contrário, opcional. |
| `Hash` | Opcional. Um hash SHA1 do arquivo de pacote. Isso é usado para verificar a integridade do arquivo no momento da instalação. Se o hash idêntico não puder ser computado a partir do arquivo de pacote, o pacote não será instalado. |

## <a name="example"></a>Exemplo
 O exemplo de código a seguir define pacotes para o pacote redistribuível .NET Framework e suas dependências, como o Windows Installer.

```xml
<PackageFiles>
    <PackageFile Name="instmsia.exe" HomeSite="InstMsiAExe" PublicKey="3082010A0282010100AA99BD39A81827F42B3D0B4C3F7C772EA7CBB5D18C0DC23A74D793B5E0A04B3F595ECE454F9A7929F149CC1A47EE55C2083E1220F855F2EE5FD3E0CA96BC30DEFE58C82732D08554E8F09110BBF32BBE19E5039B0B861DF3B0398CB8FD0B1D3C7326AC572BCA29A215908215E277A34052038B9DC270BA1FE934F6F335924E5583F8DA30B620DE5706B55A4206DE59CBF2DFA6BD154771192523D2CB6F9B1979DF6A5BF176057929FCC356CA8F440885558ACBC80F464B55CB8C96774A87E8A94106C7FF0DE968576372C36957B443CF323A30DC1BE9D543262A79FE95DB226724C92FD034E3E6FB514986B83CD0255FD6EC9E036187A96840C7F8E203E6CF050203010001"/>
    <PackageFile Name="WindowsInstaller-KB884016-v2-x86.exe" HomeSite="Msi30Exe" PublicKey="3082010A0282010100B22D8709B55CDF5599EB5262E7D3F4E34571A932BF94F20EE90DADFE9DC7046A584E9CA4D1D84441FB647E0F65EEC817DA4DDBD9D650B40C565B6C16884BBF03EE504883EC4F88939A51E394197FFAB397A5CE606D9FDD4C9338BDCD345971E686CEE98399A096B8EAE0445B1342B93A484E5472F70896E400C482017643AF61C2DBFAE5C5F00213DDF835B40F0D5236467443B1A2CA9CDD7E99F1351177FB1526018ECFE0B804782A15FD72C66076910CE74FB218181B6989B4F12F211B66EACA91C7460DB91758715856866523D10232AE64A06FDA5295FDFBDD8D34F5C10C35A347D7E91B6AFA0F45B4E8321D7019BDD1F9E5641FEB8737EA6FD40D838FFD0203010001"/>
    <PackageFile Name="dotnetfx.exe" HomeSite="DotNetFXExe" PublicKey="3082010A0282010100B22D8709B55CDF5599EB5262E7D3F4E34571A932BF94F20EE90DADFE9DC7046A584E9CA4D1D84441FB647E0F65EEC817DA4DDBD9D650B40C565B6C16884BBF03EE504883EC4F88939A51E394197FFAB397A5CE606D9FDD4C9338BDCD345971E686CEE98399A096B8EAE0445B1342B93A484E5472F70896E400C482017643AF61C2DBFAE5C5F00213DDF835B40F0D5236467443B1A2CA9CDD7E99F1351177FB1526018ECFE0B804782A15FD72C66076910CE74FB218181B6989B4F12F211B66EACA91C7460DB91758715856866523D10232AE64A06FDA5295FDFBDD8D34F5C10C35A347D7E91B6AFA0F45B4E8321D7019BDD1F9E5641FEB8737EA6FD40D838FFD0203010001"/>
    <PackageFile Name="dotnetchk.exe"/>
</PackageFiles>
```

## <a name="see-also"></a>Confira também
- [\<Product> elementos](../deployment/product-element-bootstrapper.md)
- [\<Package> elementos](../deployment/package-element-bootstrapper.md)
- [Referência de esquema de produto e pacote](../deployment/product-and-package-schema-reference.md)