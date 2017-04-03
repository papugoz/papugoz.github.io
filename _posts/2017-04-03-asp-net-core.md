---
layout: post
comments: true
title: ASP .NET Core Ładowanie kontekstu bazy danych do zewnętrznego serwisu
banner_image: /images/p4.jpg
date: 2017-04-03
categories: asp.net-core, c#,
excerpt_separator: <!--more-->
---
Dzisiaj natknąłem się na problem jak załadować `DbContext` do zewnętrznego serwisu, tak aby wszystko było testowalne. 
  
<!--more-->
Rys sytuacyjny: Mamy system, który pobiera dane do kontrolerów przez zewnętrzną bibliotekę (a ona dalej z bazy).

