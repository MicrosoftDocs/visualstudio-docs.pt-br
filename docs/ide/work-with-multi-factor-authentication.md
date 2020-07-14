---
title: Trabalhar com contas que exigem a autenticação multifator
ms.date: 05/27/2020
ms.topic: conceptual
description: Saiba como usar o Visual Studio com contas que exigem autenticação multifator.
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 699580689bcf00d00d2a6e07f814be4d1265bb1d
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283540"
---
# <a name="how-to-use-visual-studio-with-accounts-that-require-multi-factor-authentication"></a>Como usar o Visual Studio com contas que exigem autenticação multifator

Ao colaborar com usuários convidados externos, é uma boa ideia proteger seus aplicativos e dados com políticas de **acesso condicional (CA)** , como a **MFA (autenticação multifator)**.  

Uma vez habilitado, os usuários convidados precisarão de mais do que apenas um nome de usuário e senha para acessar seus recursos e devem atender aos requisitos de segurança adicionais. As políticas de MFA podem ser impostas no nível do locatário, aplicativo ou usuário convidado individual, da mesma maneira que podem ser habilitadas para membros da sua própria organização. 

## <a name="how-is-the-visual-studio-experience-affected-by-mfa-policies"></a>Como a experiência do Visual Studio é afetada pelas políticas de MFA?
As versões do Visual Studio anteriores a 16,6 podem ter degradado experiências de autenticação quando usadas com contas que habilitaram políticas de autoridade de certificação, como MFA, e estão associadas a dois ou mais locatários.

Esses problemas podem fazer com que sua instância do Visual Studio solicite a reautenticação várias vezes por dia. Talvez seja necessário inserir novamente suas credenciais para locatários autenticados anteriormente, mesmo durante a mesma sessão do Visual Studio.

## <a name="using-visual-studio-with-mfa-policies"></a>Usando o Visual Studio com políticas de MFA
Na versão 16,6, adicionamos novos recursos ao Visual Studio 2019 que simplificam o modo como os usuários podem acessar recursos protegidos por meio de políticas de CA, como a MFA. Para usar esse fluxo de trabalho aprimorado, você precisará optar por usar o navegador da Web padrão do sistema como o mecanismo para adicionar e autenticar novamente as contas do Visual Studio.  

> [!WARNING]
> Não usar esse fluxo de trabalho pode disparar uma experiência degradada, resultando em vários prompts de autenticação adicionais ao adicionar ou reautenticar contas do Visual Studio. 

### <a name="enabling-system-web-browser"></a>Habilitando o navegador da Web do sistema

> [!NOTE] 
> Para obter a melhor experiência, recomendamos que você apague os dados do navegador da Web padrão do seu sistema antes de prosseguir com esse fluxo de trabalho. Além disso, se você tiver contas corporativas ou de estudante em suas configurações do Windows 10 em **acesso corporativo ou de estudante**, verifique se elas estão autenticadas corretamente.

Para habilitar este fluxo de trabalho, vá para a caixa de diálogo opções do Visual Studio **(ferramentas > opções...)**, selecione a guia **contas** e selecione **navegador da Web do sistema** em **Adicionar e autenticar contas usando:** DropDown. 

:::image type="content" source="media/select-system-web-browser.png" alt-text="Selecione navegador da Web do sistema no menu.":::

### <a name="sign-into-additional-accounts-with-mfapolicies"></a>Entrar em contas adicionais com políticas de MFA 
Depois que o fluxo de trabalho do navegador da Web do sistema estiver habilitado, você poderá entrar ou adicionar contas ao Visual Studio como faria normalmente, por meio da caixa de diálogo Configurações de conta **(arquivo > configurações de conta...)**.   
</br>
:::image type="content" source="media/add-personalization-account.png" alt-text="Adicione uma nova conta de personalização ao Visual Studio." border="false":::

Essa ação abrirá o navegador da Web padrão do sistema, solicitará que você entre em sua conta e validará qualquer política de MFA necessária.

Com base em suas atividades de desenvolvimento e configuração de recursos, você pode ser solicitado a inserir novamente suas credenciais durante a sessão. Isso pode ocorrer quando você adiciona um novo recurso ou tenta acessar um recurso sem ter atendido anteriormente seus requisitos de autorização de autoridade de certificação/MFA.

> [!NOTE] 
> Para obter a melhor experiência, mantenha seu navegador aberto até que todas as políticas de CA/MFA sejam validadas para seus recursos. Fechar o navegador pode resultar na perda do estado de MFA criado anteriormente e pode solicitar prompts de autorização adicionais.

## <a name="reauthenticating-an-account"></a>Reautenticando uma conta  
Se houver um problema com sua conta, o Visual Studio poderá solicitar que você insira novamente suas credenciais de conta.  

:::image type="content" source="media/reauthenticate-account.png" alt-text="Reautenticar sua conta do Visual Studio.":::

Clicar em **reinserir suas credenciais** abrirá o navegador da Web padrão do sistema e tentará atualizar automaticamente suas credenciais. Se não for bem-sucedida, você será solicitado a entrar em sua conta e validar qualquer política de CA/MFA necessária.

> [!NOTE] 
> Para obter a melhor experiência, mantenha seu navegador aberto até que todas as políticas de CA/MFA sejam validadas para seus recursos. Fechar o navegador pode resultar na perda do estado de MFA criado anteriormente e pode solicitar prompts de autorização adicionais.

## <a name="how-to-opt-out-of-using-a-specific-azure-active-directory-tenant-in-visual-studio"></a>Como recusar o uso de um locatário específico de Azure Active Directory no Visual Studio

O Visual Studio 2019 versão 16,6 oferece a flexibilidade para filtrar locatários específicos, que os ocultam do Visual Studio. A filtragem elimina a necessidade de autenticar com esse locatário, mas também significa que você não poderá acessar nenhum recurso associado. 

Essa funcionalidade é útil quando você tem vários locatários, mas deseja otimizar seu ambiente de desenvolvimento direcionando um subconjunto específico. Ele também pode ajudar em instâncias quando você não pode validar uma política de CA/MFA específica, pois você pode filtrar o locatário incorreto. 

### <a name="how-to-filter-out-a-tenant"></a>Como filtrar um locatário
Para filtrar os locatários associados à sua conta do Visual Studio, abra a caixa de diálogo Configurações de conta **(arquivo > configurações de conta...)** e clique em **aplicar filtro**. 
</br>
</br>

:::image type="content" source="media/apply-filter.png" alt-text="Aplicar filtro." border="false":::

A caixa de diálogo **Filtrar conta** será exibida, permitindo que você Selecione quais locatários deseja usar com sua conta. 

:::image type="content" source="media/select-filter-account.png" alt-text="Selecione a conta a ser filtrada.":::

## <a name="see-also"></a>Veja também

- [Entrar no Visual Studio](signing-in-to-visual-studio.md)
- [Entrar no Visual Studio para Mac](/visualstudio/mac/signing-in)
- [Trabalhar com várias contas de usuário](work-with-multiple-user-accounts.md)
