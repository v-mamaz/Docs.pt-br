---
uid: web-api/overview/security/integrated-windows-authentication
title: Autenticação do Windows integrada | Microsoft Docs
author: MikeWasson
description: Descreve como usar a autenticação integrada do Windows na API Web ASP.NET.
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: 13dead421abf7ded73cbb2e5f87e54b1a869b5d4
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824275"
---
<a name="integrated-windows-authentication"></a>Autenticação integrada do Windows
====================
por [Mike Wasson](https://github.com/MikeWasson)

Autenticação integrada do Windows permite que os usuários façam logon com suas credenciais do Windows, usando Kerberos ou NTLM. O cliente envia as credenciais no cabeçalho de autorização. Autenticação do Windows é mais adequada para um ambiente de intranet. Para obter mais informações, consulte [autenticação do Windows](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).

| Vantagens | Desvantagens |
| --- | --- |
| -Incorporada ao IIS. -Não envia as credenciais do usuário na solicitação. -Se o computador cliente pertença ao domínio (por exemplo, o aplicativo de intranet), o usuário não precisa inserir credenciais. | -Não é recomendado para aplicativos da Internet. -Requer suporte a Kerberos ou NTLM no cliente. -Cliente deve estar no domínio do Active Directory. |

> [!NOTE]
> Se o aplicativo estiver hospedado no Azure e você tiver um domínio do Active Directory local, considere a possibilidade de federar seu AD local com o Azure Active Directory. Dessa forma, os usuários podem fazer com suas credenciais locais, mas a autenticação é realizada pelo Azure AD. Para obter mais informações, consulte [autenticação do Azure](../../../visual-studio/overview/2012/windows-azure-authentication.md).


Para criar um aplicativo que usa a autenticação do Windows integrada, selecione o modelo "Aplicativo de Intranet" no Assistente de projeto MVC 4. Este modelo de projeto coloca a seguinte configuração no arquivo Web. config:

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

No lado do cliente, autenticação do Windows integrada funciona com qualquer navegador que ofereça suporte a [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) esquema de autenticação, que inclui a maioria dos principais navegadores. Para aplicativos de cliente .NET, o **HttpClient** classe dá suporte à autenticação do Windows:

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

A autenticação do Windows é vulnerável a ataques de solicitação forjada (CSRF) entre sites. Ver [impedindo solicitação intersite forjada (CSRF) ataques](preventing-cross-site-request-forgery-csrf-attacks.md).
