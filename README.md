# retele
Notite, instructiuni si proiecte Packet Tracer din laboratorul de Retele.


Prerequisites:
O adresă IP (vorbim de IPv4) este reprezentată pe 32 de biți. Pentru a identifica o (sub)rețea, este nevoie de o adresă IP și de un subnet mask (SM; tot 32 de biți: un șir de 1, urmat doar de 0-uri (descompus în baza 2)).

Rolul SM este de a delimita adresa de rețea de adresele asignabile.

Algebră booleană: 1 & x = x; 0 & x = 0


Algoritm calculare IP-uri (simplificat, ca limba chineză; pentru demonstrație completă, vezi laborator):

__1. Descompui în baza 2 octetul al parte_întreagă_superioară(SM/8)-lea__

Exemplu:

avem adresa IP 192.168.13.14/26

25/8 = 3, deci ne uităm în ultimul (al 4-lea) octet (1..7 primul octet, 9...15 al doilea octet etc)

_cu primii 3 octeți nu facem nimic!

Descompunem 14 în baza 2 (pe 8 biți = un octet): 8+6=8+4+2 --> 0000 1110

__2. Te uiți la SM și vezi cât e SM%8__

Exemplu:

26%8 = 2

__3. Facem & logic între descompunerea de la pasul 1 și numărul de biți de la pasul 2__

Exemplu:

Prin urmare, vom folosi primii doi biți din descompunerea de la pasul 1, deoarece SM va avea doar 0-uri după acești 2 de 1.

00 00 1110 &

11 00 0000

--^ până aici contează de fapt

__4. Copiem ce e sus până nu mai avem 1 jos (1 & x = x), iar după avem doar 0 (0 & x = 0)__

__Deoarece 1 & x = x, copiem octeții de la stânga din adresa IP, iar pe cei de la dreapta (pe acest exemplu nu e cazul) îi înlocuim cu 0.__

Exemplu:

00 00 0000 (primii 2 sunt copiați; restul de 6 sunt "făcuți" 0 de SM)

__5. Punem totul cap la cap__

Exemplu:

192.168.13.0

primii 3 octeți au fost copiați fără modificări (pasul 1), iar ultimul octet a fost luat de la pasul 4

__6. Foarte important, adăugăm SM! (altfel, nu se poate, nu bun)__

Exemplu:

192.168.13.0/26

Aceasta este adresa de rețea (NA = network address) calculată din adresa IP 192.168.13.14/26

Adresa de rețea NU se asignează!

Adresa de rețea este ÎNTOTDEAUNA număr par!

__7. Determinăm adresa de broadcast (în cursul profului de la curs sunt rețelele de difuzare)__

__La NA adăugăm 2^n - 1, unde n = 32 - SM__

Exemplu

32-26=6

2^6 - 1 = 64 - 1 = 63 // 2^0 + 2^1 + ... + 2^(n-1) = 2^n - 1

BA: 192.168.13.63

Adresa de broadcast NU se asignează!

Adresa de broadcast este ÎNTOTDEAUNA număr impar!

Ce am uitat? Să adăugăm SM!

BA: 192.168.13.63/26

Exemplu 2:

Dacă avem o situație mai generală (adică nu ne uităm doar la ultimul octet), putem privi adresa IP ca un număr în baza 256.

Adică?

Avem NA: 172.16.64.0/18

(putem să verificăm că aceea chiar este o NA: 64 = 0100 0000)

n = 32 - SM = 32 - 18 = 14

Ca să nu calculăm 2^14, îl "spargem"

2^8 - 1 se vor duce pe ultimul octet ( = 255; minus 1 din formula cu 2^n - 1)

Rămânem cu 2^6 pentru al treilea octet

(De ce? Am zis că putem privi & IP ca pe un nr în baza 256. Atunci acel 2^6 va fi înmulțit cu (2^8)^1!

Ultimul octet este înmulțit cu 1 = (2^8)^0)

64+64 = 128 (primul 64 din octetul 3, al doilea 64 din 2^6)
Am obținut BA: 172.16.128.255/18

__8. Punem din nou totul cap la cap__

Exemplu:

NA: 192.168.13.0/26

BA: 192.168.13.63/26

Acestea sunt limitele între care putem să asignăm adrese IP pentru host-uri în rețeaua dată de NA

__9. Operațiile matematice foarte complicate__

Exemplu:

NA: 192.168.13.0/26

BA: 192.168.13.63/26

RA: 192.168.13.1 - 192.168.13.62/26

Sub forma asta ultima vrea rezultatele, indiferent ce metodă aplici (da' să fie corecte).
