---
title: Suuruusluokat
permalink: /suuruusluokat
hide: true
---
    
# Suuruusluokat

Algoritmiikassa usein esiintyviä merkintöjä ovat:

* _Yläraja_: Funktio $$g(n)$$ on luokkaa $$O(f(n))$$ eli $$g(n)=O(f(n))$$, jos on olemassa vakiot $$c$$ ja $$n_0$$ niin, että $$g(n) \le c f(n)$$ aina kun $$n \ge n_0$$.

* _Alaraja_: Funktio $$g(n)$$ on luokkaa $$\Omega(f(n))$$  eli $$g(n)=\Omega(f(n))$$, jos on olemassa vakiot $$c$$ ja $$n_0$$ niin, että $$g(n) \ge c f(n)$$ aina kun $$n \ge n_0$$.

* _Tarkka arvio_: Funktio $$g(n)$$ on luokkaa $$\Theta(f(n))$$ eli $$g(n)=\Theta(f(n))$$, jos se on sekä luokkaa $$O(f(n))$$ että luokkaa $$\Omega(f(n))$$.

Vakion $$c$$ tarkoituksena on, että saadaan arvio kasvunopeuden suuruusluokalle välittämättä vakiokertoimista. Vakion $$n_0$$ ansiosta riittää tarkastella kasvunopeutta suurilla $$n$$:n arvoilla.

## Rajojen todistaminen

Tarkastellaan funktiota $$g(n)=5n+3$$.

Todistetaan, että $$g(n)$$ on luokkaa $$O(n)$$. Tässä tapauksessa $$f(n)=n$$. Voimme arvioida $$5n+3 \le 5n+n = 6n$$, kun $$n \ge 3$$, eli vakiot $$c=6$$ ja $$n_0=3$$ toteuttavat ehdon $$g(n)\le c f(n)$$, kun $$n \ge n_0$$.

Todistetaan sitten, että $$g(n)$$ on luokkaa $$\Omega(n)$$. Nyt voidaan arvioida $$5n+3 \ge 5n$$, kun $$n \ge 1$$, eli vakiot $$c=5$$ ja $$n_0=1$$ toteuttavat ehdon $$g(n) \ge cf(n)$$, kun $$n \ge n_0$$.

Koska $$g(n)$$ on sekä luokkaa $$O(n)$$ että luokkaa $$\Omega(n)$$, se on myös luokkaa $$\Theta(n)$$.

Todistetaan vielä, että $$g(n)$$ ei ole luokkaa $$O(1)$$. Jos näin olisi, pitäisi pystyä valitsemaan vakiot $$c$$ ja $$n_0$$ niin, että $$g(n) \le c$$, kun $$n \ge n_0$$. Kuitenkaan ei ole mahdollista valita vakiota $$c$$ niin, että $$5n+3 \le c$$, kun $$n$$ voi kasvaa miten suureksi tahansa. Niinpä $$g(n)$$ ei ole luokkaa $$O(1)$$.

## Algoritmin analysointi

Algoritmin _aikavaativuus_ (_time complexity_) ilmaisee suuruusluokan sille, montako askelta algoritmi suorittaa, kun syötteen koko on $$n$$.

Tarkastellaan seuraavaa algoritmia:

{% highlight python linenos %}
def count_even(numbers):
    result = 0
    for x in values:
        if x % 2 == 0:
            result += 1
    return result
{% endhighlight %}

Algoritmi suorittaa kerran rivit 2 ja 6 ja $$n$$ kertaa rivit 3 ja 4. Rivin 5 algoritmi suorittaa vähintään $$0$$ kertaa ja enintään $$n$$ kertaa. Niinpä algoritmi suorittaa vähintään $$2n+2$$ askelta ja enintään $$3n+2$$ askelta.

Algoritmin aikavaativuus on  $$O(n)$$, koska voidaan arvioida $$3n+2 \le 4n$$, kun $$n \ge 2$$. Toisaalta algoritmin aikavaativuus on $$\Omega(n)$$, koska voidaan arvioida $$2n+2 \ge 2n$$, kun $$n \ge 1$$. Niinpä algoritmin aikavaativuus on myös $$\Theta(n)$$.

Tarkastellaan vielä seuraavaa algoritmia:

{% highlight python linenos %}
def has_even(numbers):
    for x in values:
        if x % 2 == 0:
            return True
    return False
{% endhighlight %}

Tämä algoritmi päättyy heti, kun rivin 3 ehto toteutuu. Algoritmi suorittaa vähintään $$3$$ askelta ja enintään $$2n+1$$ askelta.

Algoritmin aikavaativuus $$O(n)$$ ja toisaalta $$\Omega(1)$$.  Aikavaativuutta ei voida kuvata $$\Theta$$-merkinnällä, koska askelten määrälle ei saada samaa ylärajaa ja alarajaa.

## O-merkinnän käyttäminen

Aikavaativuus $$O(f(n))$$ tarkoittaa, että algoritmi suorittaa _pahimmassa tapauksessa_ $$O(f(n))$$ askelta. Tämä on yleensä hyvä tapa ilmoittaa algoritmin tehokkuus, koska silloin annetaan takuu siitä, että algoritmin ajankäytöllä on tietty yläraja, vaikka syöte olisi valittu mahdollisimman ikävästi algoritmin kannalta.

Huomaa, että $$O$$-merkintä tarkoittaa _mitä tahansa_ ylärajaa eikä välttämättä tarkkaa ylärajaa. Niinpä jos algoritmi suorittaa $$3n$$ askelta, sen aikavaativuus on $$O(n)$$ mutta myös $$O(n^2)$$ ja $$O(n^3)$$. Kuitenkin yleensä $$O$$-merkinnällä annetaan tarkka yläraja, joka antaa todellisen kuvan algoritmin tehokkuudesta.

Asiaa voi ajatella niin, että $$O$$-merkintää käytetään algoritmin _markkinoinnissa_. Jos aikavaativuus ilmoitetaan liian suurena, tämä ei sinänsä ole väärin mutta yleisölle tulee liian hidas kuva algoritmista.

## Lisää suuruusluokista

Suuruusluokkia voidaan käyttää aikavaativuuksien lisäksi muutenkin algoritmien analysoinnissa. Esimerkiksi voidaan sanoa, että listassa on $$O(n)$$ alkiota tai algoritmi muodostuu $$O(n)$$ kierroksesta.

Algoritmin _tilavaativuus_ (_space complexity_) ilmaisee, paljonko muistia algoritmi tarvitsee toimiakseen syötteeseen kuluvan muistin lisäksi. Tarkastellaan esimerkkinä seuraavia funktioita:

```python
def count_even(numbers):
    result = 0
    for x in numbers:
        if x % 2 == 0:
            result += 1
    return result
```

```python
def count_even(numbers):
    even_numbers = []
    for x in numbers:
        if x % 2 == 0:
            even_numbers.append(x)
    return len(even_numbers)
```

Ensimmäisen funktion tilavaativuus on $$O(1)$$, koska siinä on vain muuttuja `result`. Toisen funktion tilavaativuus on $$O(n)$$, koska listalle `even_numbers` lisätään $$O(n)$$ lukua. Molemmissa funktioissa aikavaativuus on $$O(n)$$. 
