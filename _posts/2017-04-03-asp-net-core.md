---
layout: post
comments: true
title: ASP .NET Core Ładowanie kontekstu bazy danych do zewnętrznej biblioteki (EF6)
banner_image: /images/p4.jpg
date: 2017-04-03
categories: asp.net-core, c#,
excerpt_separator: <!--more-->
---
Dzisiaj natknąłem się na problem jak załadować `DbContext` do zewnętrznego serwisu, tak aby wszystko było testowalne. 
  
<!--more-->
Rys sytuacyjny: Mamy system, który pobiera dane do kontrolerów przez zewnętrzną bibliotekę (a ona dalej z bazy). [Dokumentacja microsoftowa](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection) opisuje tylko prosty przypadek, kiedy mamy serwisy bez zależności, a dane pobieramy z `DbContextu` bezpośrednio w kontrolerze.  
Wszystko fajnie, tylko nie każda aplikacja jest na sztywno spięta z bazą danych. Niektóre posiadają opcje wyboru typu bazy danych do której się łączą (może kiedyś opiszę ten przypadek), inne są częścią większego serwisu i dla jednolitości kodu posiadają wspólną bibliotekę odpowiadającą za połączenie.  
W moim wypadku miałem doczynienia z sytuacją drugą. Posiadałem serwis, którego konstruktor jako argument przyjmował instancję typu `ApplicationDbContext` a następnie w oparciu o nią zarządzał dostępem do danych.  
Co z tym można zrobić? Okazuje się że z pomocą przychodzi DI wbudowane w ASP.NET core, któe pozwala nam odpowiednio poinstuować aplikację by instancje serwisu otrzymywały nasz DbContext.
W `ConfigureServices` ustawiamy swoją konfigurację:

```c#
public void ConfigureServices(IServiceCollection services)
{
  services.AddTransient<IService, Service>(new ApplicationDbContext((Configuration.GetConnectionString("ConnectionString")));
}
```  

Tym sposobem możemy przekazać również inne zależności, jak inne serwisy.  
Jeżeli jendak zależy nam na bardziej rozbudowanym wstrzykiwaniu zależności, powinniśmy zastanowić się nad skorzystaniem z innego rozwiązania niż moduł wbudowany we framework który, jak przyznał sam Microsoft, jest przeznaczony do tylko podstawowego zarządzania zależnościami.  
Osobiście mi do gustu najbardziej przypadł [Autofac](https://autofac.org), ze względu na bardzo dobrze wsparcie dla ASP.NET Core.