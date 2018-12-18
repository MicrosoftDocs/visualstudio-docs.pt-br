---
title: Suporte a NGen no VSIX v3 | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 1472e884-c74e-4c23-9d4a-6d8bdcac043b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3b5f9c7b297d98836ca3e5c017d2a0d440a30470
ms.sourcegitcommit: 9765b3fcf89375ca499afd9fc42cf4645b66a8a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/20/2018
ms.locfileid: "46495473"
---
# <a name="ngen-support-in-vsix-v3"></a>Suporte a NGen no VSIX v3

Com o Visual Studio 2017 e o novo VSIX v3 extensão (versão 3) o manifesto formato, agora podem de desenvolvedores de extensão "ngen" seus assemblies no momento da instalação.

Abaixo está um trecho do MSDN que explica o que "ngen" faz:

>Gerador de imagem nativa (*Ngen.exe*) é uma ferramenta que melhora o desempenho de aplicativos gerenciados. *Ngen.exe* cria imagens nativas, que são arquivos que contêm código compilado de máquina de processador específico e as instala no cache de imagem nativa no computador local. O tempo de execução pode usar imagens nativas do cache em vez de usar o compilador JIT (Just-In-Time) para compilar o assembly original.
>
>de [Ngen.exe (gerador de imagem nativa)](/dotnet/framework/tools/ngen-exe-native-image-generator)

Em ordem "NGen" um assembly, o VSIX deve ser instalado "por instância por máquina". Isso pode ser habilitado marcando a caixa de seleção de "todos os usuários" `extension.vsixmanifest` designer:

![Verifique todos os usuários](media/check-all-users.png)

## <a name="how-to-enable-ngen"></a>Como habilitar o Ngen

Para habilitar o ngen para um assembly, você pode usar o **propriedades** janela no Visual Studio.

Há 4 propriedades que podem ser definidas:

1. **NGen** (booliano) – se for true, o instalador do Visual Studio será "ngen" do assembly.
2. **Aplicativo NGen** (cadeia de caracteres) - Ngen fornece a oportunidade de usar um aplicativo *App. config* arquivo a fim de resolver as dependências do assembly. Esse valor deve ser definido como um aplicativo cuja *App. config* você deseja usar (relativo ao diretório de instalação do Visual Studio).
3. **Arquitetura NGen** (enum) – a arquitetura nativamente compilar o assembly. As opções são: um. B NotSpecified. X86 c. X64 d. Todos
4. **Prioridade do NGen** (número inteiro entre 1 e 3) - nível de prioridade do Ngen o está documentado em [níveis de prioridade Ngen.exe](/dotnet/framework/tools/ngen-exe-native-image-generator#priority-levels).

Aqui está uma visão de **propriedades** janela em ação:

![NGen nas propriedades](media/ngen-in-properties.png)

Isso adicionará os metadados para a referência de projeto dentro do projeto do VSIX *. csproj* arquivo:

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
    <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
    <Name>ClassLibrary1</Name>
    <Ngen>True</Ngen>
    <NgenApplication>vsn.exe</NgenApplication>
    <NgenArchitecture>X86</NgenArchitecture>
    <NgenPriority>2</NgenPriority>
</ProjectReference>
 ```

 >**Observação:** você pode editar o arquivo. csproj diretamente, se você preferir.

## <a name="extra-information"></a>Informações adicionais

As alterações de propriedade designer se aplicam a mais do que apenas as referências de projeto; Você pode definir os metadados do Ngen para os itens dentro de seu projeto, bem desde que os itens são assemblies do .NET (usando os mesmos métodos descritos acima).