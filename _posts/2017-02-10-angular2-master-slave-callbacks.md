---
layout: post
title: Angular2 callbacks
banner_image: /images/p2.jpg
date: 2017-02-10
categories: angular2
excerpt_separator: <!--more-->
---
Migrując mój aktualny projekt na Angulara2 (na czymś trzeba się uczyć), szukałem czegoś podobnego do callbacków z Angulara 1.X. Przyznam, że znalezienie, a może wręcz sformułowanie odpowiedniego pytania zajęło mi chwilę.. gdyż okazało się że zastąpiono je czymś innym.

  
<!--more-->  
Lubię jak kawałki aplikacji są jak najbardziej generyczne, przez co nie muszę potem przepisywać ich w innych miejscach. Tak, dla większości to oczywistość, jednak spotkałem wielu programistów, dla których jednak nią nie było.  

Przykładowa sytuacja:  
Mam komponent dodawania serwisu oraz komponent jego edycji (teoretycznie mógłby być to ten sam komponent, ale załóżmy, żę sytuacja wymaga dwóch) W obydwu, poza innymi rzeczami, jest sobie formularz – taki sam dla obydwu sytuacji. Zawiera on pola do wypełnienia, oraz przyciski **wstecz** i **zapisz**. Przyjmuje informacje o serwisie poprzez atrybut z dekoratorem `@input`  

```javascript
export class ServiceFormComponent { 
  @Input() service: Service; 
  save() { } 
  goBack() { } 
} 
```  

No i wszystko fajnie, tylko jak teraz poinformować komponent wyżej, że tam na dole dodaliśmy/zaktualizowaliśmy dobie nasz obiekt?  
Na odsiecz idzie nam dekorator `@output` który informuje nadrzędny komponent by oczekiwał na... No właśnie na co?  

[Może na umówiony znak sygnał?](https://youtu.be/g71NzMdaxho?t=1m12s) 

I właśnie tutaj z pomocą przychodzi `EventEmitter`. To właśnie on jest informatorem, który ma zawiadomić rodzica, a następnie przekazać to co zawiera.