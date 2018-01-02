---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: "Adicionando uma exibição (VB) | Microsoft Docs"
author: Rick-Anderson
description: "Este tutorial ensina as Noções básicas de criação de um aplicativo Web do ASP.NET MVC usando o Microsoft Visual Web Developer 2010 Express Service Pack 1, que é..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 7e8564c743510780b93d56bc1215f4c5b1faeb43
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2017
---
<a name="adding-a-view-vb"></a><span data-ttu-id="60c24-103">Adicionando uma exibição (VB)</span><span class="sxs-lookup"><span data-stu-id="60c24-103">Adding a View (VB)</span></span>
====================
<span data-ttu-id="60c24-104">Por [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="60c24-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="60c24-105">Este tutorial ensina as Noções básicas de criação de um aplicativo Web do ASP.NET MVC usando o Microsoft Visual Web Developer 2010 Express Service Pack 1, que é uma versão gratuita do Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60c24-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="60c24-106">Antes de começar, verifique se que você instalou os pré-requisitos listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="60c24-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="60c24-107">Você pode instalar todos eles clicando no link a seguir: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="60c24-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="60c24-108">Como alternativa, você pode instalar individualmente os pré-requisitos usando os links a seguir:</span><span class="sxs-lookup"><span data-stu-id="60c24-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="60c24-109">Pré-requisitos de Visual Studio Web Developer Express SP1</span><span class="sxs-lookup"><span data-stu-id="60c24-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="60c24-110">Atualização de ferramentas do ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="60c24-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="60c24-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(tempo de execução + ferramentas de suportam)</span><span class="sxs-lookup"><span data-stu-id="60c24-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="60c24-112">Se você estiver usando o Visual Studio 2010 em vez do Visual Web Developer 2010, instale os pré-requisitos clicando no link a seguir: [pré-requisitos do Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="60c24-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="60c24-113">Um projeto do Visual Web Developer com VB.NET código-fonte está disponível para acompanhar este tópico.</span><span class="sxs-lookup"><span data-stu-id="60c24-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="60c24-114">[Baixe a versão VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="60c24-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="60c24-115">Se você preferir c#, alterne para o [versão c#](../cs/adding-a-view.md) deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="60c24-115">If you prefer C#, switch to the [C# version](../cs/adding-a-view.md) of this tutorial.</span></span>


<span data-ttu-id="60c24-116">Nesta seção, vamos modificar o `HelloWorldController` classe para usar um arquivo de modelo de exibição para corretamente encapsulam o processo de geração de respostas HTML para um cliente.</span><span class="sxs-lookup"><span data-stu-id="60c24-116">In this section we're going to modify the `HelloWorldController` class to use a view template file to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="60c24-117">Vamos começar usando um modelo de exibição com o `Index` método o `HelloWorldController` classe.</span><span class="sxs-lookup"><span data-stu-id="60c24-117">Let's start by using a view template with the `Index` method in the `HelloWorldController` class.</span></span> <span data-ttu-id="60c24-118">Atualmente o `Index` método retorna uma cadeia de caracteres com uma mensagem que é embutido dentro da classe do controlador.</span><span class="sxs-lookup"><span data-stu-id="60c24-118">Currently the `Index` method returns a string with a message that is hard-coded within the controller class.</span></span> <span data-ttu-id="60c24-119">Alterar o `Index` método para retornar um `View` do objeto, conforme mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="60c24-119">Change the `Index` method to return a `View` object, as shown in the following:</span></span>

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

<span data-ttu-id="60c24-120">Vamos adicionar agora um modelo de exibição ao nosso projeto que pode ser chamado com o `Index` método.</span><span class="sxs-lookup"><span data-stu-id="60c24-120">Let's now add a view template to our project that we can invoke with the `Index` method.</span></span> <span data-ttu-id="60c24-121">Para fazer isso, clique dentro do `Index` método e clique em **adicionar exibição**.</span><span class="sxs-lookup"><span data-stu-id="60c24-121">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

<span data-ttu-id="60c24-122">[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="60c24-122">[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)</span></span>

<span data-ttu-id="60c24-123">O **adicionar exibição** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="60c24-123">The **Add View** dialog box appears.</span></span> <span data-ttu-id="60c24-124">Deixe as entradas padrão e clique no **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="60c24-124">Leave the default entries and click the **Add** button.</span></span>

<span data-ttu-id="60c24-125">[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="60c24-125">[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)</span></span>

<span data-ttu-id="60c24-126">O *MvcMovie\Views\HelloWorld* pasta e o *MvcMovie\Views\HelloWorld\Index.vbhtml* arquivos são criados.</span><span class="sxs-lookup"><span data-stu-id="60c24-126">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.vbhtml* file are created.</span></span> <span data-ttu-id="60c24-127">Você pode vê-los em **Solution Explorer**:</span><span class="sxs-lookup"><span data-stu-id="60c24-127">You can see them in **Solution Explorer**:</span></span>

<span data-ttu-id="60c24-128">[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="60c24-128">[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)</span></span>

<span data-ttu-id="60c24-129">Adicionar um HTML sob o `<h2>` marca.</span><span class="sxs-lookup"><span data-stu-id="60c24-129">Add some HTML under the `<h2>` tag.</span></span> <span data-ttu-id="60c24-130">A modificação *MvcMovie\Views\HelloWorld\Index.vbhtml* arquivo é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="60c24-130">The modified *MvcMovie\Views\HelloWorld\Index.vbhtml* file is shown below.</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

<span data-ttu-id="60c24-131">Execute o aplicativo e navegue até o &quot;Olá, mundo&quot; controlador (`http://localhost:xxxx/HelloWorld`).</span><span class="sxs-lookup"><span data-stu-id="60c24-131">Run the application and browse to the &quot;hello world&quot; controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="60c24-132">O `Index` método em seu controlador não fazer a quantidade de trabalho; ele simplesmente executou a instrução `return View()`, qual indicado que queremos usar um arquivo de modelo de exibição para renderizar uma resposta ao cliente.</span><span class="sxs-lookup"><span data-stu-id="60c24-132">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which indicated that we wanted to use a view template file to render a response to the client.</span></span> <span data-ttu-id="60c24-133">Porque estamos não especificar explicitamente o nome do arquivo do modelo de exibição a ser usado, o ASP.NET MVC padrão usando o *Index.vbhtml* Exibir arquivo dentro de *\Views\HelloWorld* pasta.</span><span class="sxs-lookup"><span data-stu-id="60c24-133">Because we did not explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.vbhtml* view file within the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="60c24-134">A imagem abaixo mostra a cadeia de caracteres codificada no modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="60c24-134">The image below shows the string hard-coded in the view.</span></span>

<span data-ttu-id="60c24-135">[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="60c24-135">[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)</span></span>

<span data-ttu-id="60c24-136">Parece muito bom.</span><span class="sxs-lookup"><span data-stu-id="60c24-136">Looks pretty good.</span></span> <span data-ttu-id="60c24-137">No entanto, observe que a barra de título do navegador diz &quot;índice&quot; e informa o título grande na página &quot;meu aplicativo MVC.&quot; Vamos alterar os.</span><span class="sxs-lookup"><span data-stu-id="60c24-137">However, notice that the browser's title bar says &quot;Index&quot; and the big title on the page says &quot;My MVC Application.&quot; Let's change those.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="60c24-138">Alterando exibições e páginas de layout</span><span class="sxs-lookup"><span data-stu-id="60c24-138">Changing views and layout pages</span></span>

<span data-ttu-id="60c24-139">Primeiro, vamos alterar o texto &quot;meu aplicativo MVC.&quot; Esse texto é compartilhado e aparece em cada página.</span><span class="sxs-lookup"><span data-stu-id="60c24-139">First, let's change the text &quot;My MVC Application.&quot; That text is shared and appears on every page.</span></span> <span data-ttu-id="60c24-140">Na verdade, aparece em apenas um local em nosso projeto, mesmo que seja em cada página em nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="60c24-140">It actually appears in only one place in our project, even though it's on every page in our application.</span></span> <span data-ttu-id="60c24-141">Vá para o */exibições/compartilhado* pasta **Solution Explorer** e abra o  *\_Layout.vbhtml* arquivo.</span><span class="sxs-lookup"><span data-stu-id="60c24-141">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.vbhtml* file.</span></span> <span data-ttu-id="60c24-142">Esse arquivo é chamado de uma página de layout e é compartilhado &quot;shell&quot; que usam todas as outras páginas.</span><span class="sxs-lookup"><span data-stu-id="60c24-142">This file is called a layout page and it's the shared &quot;shell&quot; that all other pages use.</span></span>

<span data-ttu-id="60c24-143">Observe o `@RenderBody()` linha de código na parte inferior do arquivo.</span><span class="sxs-lookup"><span data-stu-id="60c24-143">Note the `@RenderBody()` line of code near the bottom of the file.</span></span> <span data-ttu-id="60c24-144">`RenderBody`é um espaço reservado em que todas as páginas que você cria aparecem &quot;encapsulado&quot; na página de layout.</span><span class="sxs-lookup"><span data-stu-id="60c24-144">`RenderBody` is a placeholder where all the pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="60c24-145">Alterar o `<h1>` título do  **&quot;**  meu aplicativo MVC&quot; para &quot;aplicativo de filme MVC&quot;.</span><span class="sxs-lookup"><span data-stu-id="60c24-145">Change the `<h1>` heading from **&quot;** My MVC Application&quot; to &quot;MVC Movie App&quot;.</span></span>

[!code-html[Main](adding-a-view/samples/sample3.html)]

<span data-ttu-id="60c24-146">Execute o aplicativo e Observe agora diz &quot;aplicativo de filme MVC&quot;.</span><span class="sxs-lookup"><span data-stu-id="60c24-146">Run the application and note it now says &quot;MVC Movie App&quot;.</span></span> <span data-ttu-id="60c24-147">Clique o **sobre** link e que mostra a página &quot;aplicativo de filme MVC&quot;também.</span><span class="sxs-lookup"><span data-stu-id="60c24-147">Click the **About** link, and that page shows &quot;MVC Movie App&quot;, too.</span></span>

<span data-ttu-id="60c24-148">Completo  *\_Layout.vbhtml* arquivo é mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="60c24-148">The complete *\_Layout.vbhtml* file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="60c24-149">Agora, vamos alterar o título da página de índice (exibição).</span><span class="sxs-lookup"><span data-stu-id="60c24-149">Now, let's change the title of the Index page (view).</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

<span data-ttu-id="60c24-150">Abra *MvcMovie\Views\HelloWorld\Index.vbhtml*.</span><span class="sxs-lookup"><span data-stu-id="60c24-150">Open *MvcMovie\Views\HelloWorld\Index.vbhtml*.</span></span> <span data-ttu-id="60c24-151">Há dois locais para fazer uma alteração: primeiro, o texto que aparece no título do navegador e, em seguida, no cabeçalho de secundário (o `<h2>` elemento).</span><span class="sxs-lookup"><span data-stu-id="60c24-151">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="60c24-152">Verifique-os ligeiramente diferentes para ver qual parte do código altera qual parte do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="60c24-152">We'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

<span data-ttu-id="60c24-153">Execute o aplicativo e navegue até`http://localhost:xx/HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="60c24-153">Run the application and browse to`http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="60c24-154">Observe que o título do navegador, o cabeçalho primário e os títulos secundários foram alterados.</span><span class="sxs-lookup"><span data-stu-id="60c24-154">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="60c24-155">É fácil fazer grandes alterações em seu aplicativo com pequenas alterações para um modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="60c24-155">It's easy to make big changes in your application with small changes to a view.</span></span> <span data-ttu-id="60c24-156">(Se as alterações não forem exibidas no navegador, talvez o conteúdo armazenado em cache esteja sendo exibido.</span><span class="sxs-lookup"><span data-stu-id="60c24-156">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="60c24-157">Pressione Ctrl+F5 no navegador para forçar a resposta do servidor a ser carregada.)</span><span class="sxs-lookup"><span data-stu-id="60c24-157">Press Ctrl+F5 in your browser to force the response from the server to be loaded.)</span></span>

<span data-ttu-id="60c24-158">[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="60c24-158">[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)</span></span>

<span data-ttu-id="60c24-159">Nosso pequeno &quot;dados&quot; (nesse caso o &quot;Olá, mundo!&quot; mensagem) é inserido no código, embora.</span><span class="sxs-lookup"><span data-stu-id="60c24-159">Our little bit of &quot;data&quot; (in this case the &quot;Hello World!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="60c24-160">Nosso aplicativo MVC tem V (views), e temos C (controladores), mas ainda não M (modelo).</span><span class="sxs-lookup"><span data-stu-id="60c24-160">Our MVC application has V (views) and we've got C (controllers), but no M (model) yet.</span></span> <span data-ttu-id="60c24-161">Em breve, examinaremos como criar um banco de dados e recuperar dados de modelo dele.</span><span class="sxs-lookup"><span data-stu-id="60c24-161">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="60c24-162">Passando dados do controlador para a exibição</span><span class="sxs-lookup"><span data-stu-id="60c24-162">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="60c24-163">Antes de ir para um banco de dados e falar sobre modelos, no entanto, vamos primeiro falar sobre passando informações do controlador para um modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="60c24-163">Before we go to a database and talk about models, though, let's first talk about passing information from the Controller to a View.</span></span> <span data-ttu-id="60c24-164">Queremos passar o que requer um modelo de exibição para renderizar uma resposta HTML para um cliente.</span><span class="sxs-lookup"><span data-stu-id="60c24-164">We want to pass what a view template requires in order to render an HTML response to a client.</span></span> <span data-ttu-id="60c24-165">Esses objetos são normalmente criados e passados por uma classe de controlador para um modelo de exibição, e eles devem conter apenas os dados que o modelo de exibição requer — e não mais.</span><span class="sxs-lookup"><span data-stu-id="60c24-165">These objects are typically created and passed by a controller class to a view template, and they should contain only the data that the view template requires — and no more.</span></span>

<span data-ttu-id="60c24-166">Anteriormente com o `HelloWorldController` classe, o `Welcome` método de ação levou um `name` e um `numTimes` parâmetro e saída, em seguida, os valores de parâmetro para o navegador.</span><span class="sxs-lookup"><span data-stu-id="60c24-166">Previously with the `HelloWorldController` class, the `Welcome` action method took a `name` and a `numTimes` parameter and then output the parameter values to the browser.</span></span> <span data-ttu-id="60c24-167">Em vez de ter o controlador de continuar a processar essa resposta diretamente, vamos em vez disso, colocaremos esses dados em um recipiente para o modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="60c24-167">Rather than have the controller continue to render this response directly, let's instead we'll put that data in a bag for the View.</span></span> <span data-ttu-id="60c24-168">Controladores e exibições podem usar um `ViewBag` objeto para armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="60c24-168">Controllers and Views can use a `ViewBag` object to hold that data.</span></span> <span data-ttu-id="60c24-169">Que será passado um modelo de exibição automaticamente e usada para processar a resposta HTML usando o conteúdo do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="60c24-169">That will be passed over to a view template automatically, and used to render the HTML response using the contents of the bag as data.</span></span> <span data-ttu-id="60c24-170">Dessa forma, o controlador está preocupado com algo e o modelo de exibição com outro — que nos permite manter limpa &quot;separação de preocupações&quot; dentro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="60c24-170">That way the controller is concerned with one thing and the view template with another — enabling us to maintain clean &quot;separation of concerns&quot; within the application.</span></span>

<span data-ttu-id="60c24-171">Como alternativa, podemos pode definir uma classe personalizada, em seguida, criar uma instância do objeto em nossa própria, preenchê-lo com dados e passá-lo para o modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="60c24-171">Alternatively, we could define a custom class, then create an instance of that object on our own, fill it with data and pass it to the View.</span></span> <span data-ttu-id="60c24-172">Que é geralmente chamado um ViewModel, porque ele é um modelo personalizado para o modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="60c24-172">That is often called a ViewModel, because it's a custom Model for the View.</span></span> <span data-ttu-id="60c24-173">Para pequenas quantidades de dados, no entanto, a ViewBag funciona muito bem.</span><span class="sxs-lookup"><span data-stu-id="60c24-173">For small amounts of data, however, the ViewBag works great.</span></span>

<span data-ttu-id="60c24-174">Volte para o *HelloWorldController.vb* alteração do arquivo de `Welcome` método dentro do controlador para colocar a mensagem e NumTimes em ViewBag.</span><span class="sxs-lookup"><span data-stu-id="60c24-174">Return to the *HelloWorldController.vb* file change the `Welcome` method inside the controller to put the Message and NumTimes into the ViewBag.</span></span> <span data-ttu-id="60c24-175">A ViewBag é um objeto dinâmico.</span><span class="sxs-lookup"><span data-stu-id="60c24-175">The ViewBag is a dynamic object.</span></span> <span data-ttu-id="60c24-176">Isso significa que você pode colocar tudo o que você quiser ele.</span><span class="sxs-lookup"><span data-stu-id="60c24-176">That means you can put whatever you want in to it.</span></span> <span data-ttu-id="60c24-177">A ViewBag tem propriedades não definidas até que você insira algo dentro dele.</span><span class="sxs-lookup"><span data-stu-id="60c24-177">The ViewBag has no defined properties until you put something inside it.</span></span>

<span data-ttu-id="60c24-178">Completo `HelloWorldController.vb` com a nova classe no mesmo arquivo.</span><span class="sxs-lookup"><span data-stu-id="60c24-178">The complete `HelloWorldController.vb` with the new class in the same file.</span></span>

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

<span data-ttu-id="60c24-179">Agora nosso ViewBag contém dados que serão passados para o modo de exibição automaticamente.</span><span class="sxs-lookup"><span data-stu-id="60c24-179">Now our ViewBag contains data that will be passed over to the View automatically.</span></span> <span data-ttu-id="60c24-180">Novamente, como alternativa, poderia passaram no nosso próprio objeto assim se podemos gostou:</span><span class="sxs-lookup"><span data-stu-id="60c24-180">Again, alternatively we could have passed in our own object like this if we liked:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

<span data-ttu-id="60c24-181">Agora precisamos de um `WelcomeView` modelo!</span><span class="sxs-lookup"><span data-stu-id="60c24-181">Now we need a `WelcomeView` template!</span></span> <span data-ttu-id="60c24-182">Execute o aplicativo para que o novo código é compilado.</span><span class="sxs-lookup"><span data-stu-id="60c24-182">Run the application so the new code is compiled.</span></span> <span data-ttu-id="60c24-183">Feche o navegador, clique dentro de `Welcome` método e depois clique em **adicionar modo de exibição**.</span><span class="sxs-lookup"><span data-stu-id="60c24-183">Close the browser, right-click inside the `Welcome` method, and then click **Add View**.</span></span>

<span data-ttu-id="60c24-184">Aqui está o que seu **adicionar exibição** aparência de caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="60c24-184">Here's what your **Add View** dialog box looks like.</span></span>

<span data-ttu-id="60c24-185">[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="60c24-185">[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)</span></span>

<span data-ttu-id="60c24-186">Adicione o seguinte código sob o `<h2>` elemento no novo *bem-vindo.* arquivo vbhtml.</span><span class="sxs-lookup"><span data-stu-id="60c24-186">Add the following code under the `<h2>` element in the new *Welcome.*vbhtml file.</span></span> <span data-ttu-id="60c24-187">Vamos fazer um loop e dizer &quot;Hello&quot; quantas vezes o usuário diz que deveríamos!</span><span class="sxs-lookup"><span data-stu-id="60c24-187">We'll make a loop and say &quot;Hello&quot; as many times as the user says we should!</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

<span data-ttu-id="60c24-188">Execute o aplicativo e navegue até`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`</span><span class="sxs-lookup"><span data-stu-id="60c24-188">Run the application and browse to `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`</span></span>

<span data-ttu-id="60c24-189">Agora dados é obtidos com a URL e passados para o controlador automaticamente.</span><span class="sxs-lookup"><span data-stu-id="60c24-189">Now data is taken from the URL and passed to the controller automatically.</span></span> <span data-ttu-id="60c24-190">O controlador de pacotes de dados em um `Model` objeto e etapas de objeto para o modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="60c24-190">The controller packages up the data into a `Model` object and passes that object to the view.</span></span> <span data-ttu-id="60c24-191">O modo de exibição que exibe os dados como HTML para o usuário.</span><span class="sxs-lookup"><span data-stu-id="60c24-191">The view than displays the data as HTML to the user.</span></span>

<span data-ttu-id="60c24-192">[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="60c24-192">[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)</span></span>

<span data-ttu-id="60c24-193">Bem, isso foi um tipo de um &quot;M&quot; para modelo, mas não o tipo de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="60c24-193">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="60c24-194">Vamos ver o que aprendemos e criar um banco de dados de filmes.</span><span class="sxs-lookup"><span data-stu-id="60c24-194">Let's take what we've learned and create a database of movies.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="60c24-195">[Anterior](adding-a-controller.md)
[Próximo](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="60c24-195">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>