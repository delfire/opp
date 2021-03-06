---
layout: post
title: "Menos é Mais"
date: 2016-11-28
description:
  Existe uma quantidade ideal para a quantidade de argumentos, 
  métodos, atributos e classes dentro de uma unidade.
image: /images/photo-14541995559820-04de78c094e9.jpg
categories: 
  - Objetos
tags:
  - codigo
keywords:
  - menos é mais
  - quantidade de atributos
  - quantidade de argumentos
  - quantidade de métodos
--- 

Já pensou qual seria a quantidade ideal para argumentos em um 
método? E a quantidade de métodos em uma Interface ou Classe?
E quantas Classes você codificaria dentro de uma única unidade?

Vamos tentar obter alguns números.

<!--more-->

![Unsplash image]({{ page.image }})

## Introdução {#introducao}

O tamanho de uma Classe, ou seja, a quantidade de métodos que
ela implementa diz muito sobre ela. Uma Classe com muitos métodos
está fazendo coisas demais, possui
[responsabilidades]({% post_url 2016-03-07-classes-devem-implementar-apenas-uma-responsabilidade %})
demais.

Podemos utilizar o mesmo princípio para argumentos de métodos. 
Mais argumentos, mais informação, mais comunicações com outros
Objetos. Então, teoricamente, o método está fazendo coisas demais.

Nesse artigo vou lhe mostrar alguns números ideais.

Não presumo que você irá concordar com tudo o que ler abaixo mas, 
concordando ou não, esses são *meus* números.

## Métodos {#metodos}

Interfaces devem ser pequenas, com poucos métodos.
Não é por que a Interface representa
um `Carro` que ela deverá conter todos os métodos inimagináveis
para implementar o comportamento de um Carro. 

Cada Interface deve ter o número de métodos que represente uma
[entidade]({% post_url 2016-02-29-objetos-representam-entidades %})
num contexto bem *delimitado*.

O número de métodos ideal está entre **1 e 5** para Interfaces e,
consequentemente, é o mesmo para Classes.

No entanto eu não considero a sobrecarga de métodos nessa contagem, ou seja, se
a Classe possui 3 métodos `Save` sobrecarregados, eu considero apenas
como 1 método. Mas, mesmo que possa haver muitos métodos sobrecarregados,
não quer dizer que a inteligência está dentro desses métodos. Não.
Quase tudo pode ser [delegado]({% post_url 2016-10-03-delegacao-de-implementacao-de-interfaces %})
à outros Objetos mais especialistas.

## Construtores {#construtores}

Os construtores [primários e secundários]({% post_url 2016-03-21-construtores-da-classe-primario-secundarios %})
sempre serão sobrecargas. Então você poderá ter quantos quiser.

Mas eu prefiro ter apenas 1 construtor e muitos
[Métodos *New*]({% post_url 2016-01-10-interfaces-e-o-metodo-estatico-new %}). Assim eu me
beneficio de duas maneiras: a) A Classe só terá um meio para construir
Objetos e b) Os métodos *New* obrigam outros desenvolvedores a utilizarem 
instâncias de Interfaces e não instâncias de Classe.

## Argumentos {#argumentos}

Utilize a menor quantidade possível de argumentos nos métodos.
Um método com muitos argumentos é difícil de escrever, entender e ler.
Lembre-se que a maior parte do trabalho de um programador é *ler* o código e não
escrevê-lo.

O mesmo para argumentos dos [construtores]({% post_url 2016-03-21-construtores-da-classe-primario-secundarios %})
da Classe.

O número ideal para os argumentos está entre **0 e 5**.

## Variáveis locais {#variaveis-locais}

Antes de utilizar a técnica do [Método *New*]({% post_url 2016-01-10-interfaces-e-o-metodo-estatico-new %}),
eu precisava utilizar um número maior de variáveis, somente para
ter a [contagem de referência](http://docwiki.embarcadero.com/RADStudio/Seattle/en/Using_Reference_Counting)
funcionando sem vazamentos de memória.

Não mais.

Agora eu utilizo cada vez menos variáveis locais e esse é um indício
de um código mais Orientado a Objetos. Variáveis locais são utilizados
em código *procedural*. Você precisa de uma variável para *guardar* algum
valor, enquanto executa outro processamento, e então utiliza a variável
que guardou em outro processamento... procedural.

O número ideal para variáveis locais está entre **0 e 3**.

## Atributos {#atributos}

Os atributos de um Objeto devem estar em conformidade com o que
ele representa. Se você tem um método que retorna o Objeto no formato
de XML, por exemplo, mas não utiliza esse formato em nenhum outro 
método, então você não deveria ter um atributo que representa um XML.
Em vez disso, crie o Objeto só quando ele for necessário, ou seja, 
quanto o método que retorna um XML for requisitado.

O número ideal para atributos está entre **1 e 7**.

Aqui, no entanto, você pode quebrar essa regra *temporariamente* se
necessário, devido a prazos, complexidade, etc. Você pode aumentar
o número de atributos e refatorar depois sem problemas, pois eles estarão 
[encapsulados]({% post_url 2016-05-30-heranca-pode-ser-o-mal-da-orientacao-a-objetos-parte-2 %}#encapsulamento)
dentro da Classe. 

Ninguém sabe o que acontece dentro de um Objeto, não é?

O que não pode ocorrer é ter um Objeto que não encapsula *nenhum* atributo.
Um Objeto *sempre* deve encapsular alguma coisa, porque ele representa
algo. Ele deve ter algum [estado]({% post_url 2016-04-04-objetos-sem-estado %})
que é implementado por seus atributos.

## Classes na Unidade {#classes}

A linguagem Object Pascal foi uma das primeiras a implementar o conceito
de *packages* ou *namespaces*.

Sim, estou falando das *units*.

Cada [Unidade]({% post_url 2016-10-24-unidades-limitrofes %}) pode conter Classes 
públicas ou privadas.

O número ideal para Classes dentro da mesma Unidade está entre **1 e 11**.

Dificilmente eu utilizo Classes privadas, pois sempre acho que elas podem 
ser utilizadas em outros módulos. No entanto, se necessário, Classe privadas — 
não importa se é privado no nível de Classe ou de Unidade — podem ser implementadas 
seguindo as mesmas regras dos atributos. 
Como são privadas, podem ser alteradas sem problemas futuramente.

## Conclusão {#conclusao}

Definir números máximos de usabilidade, é o mesmo que *restringir*.
E restrição pode ser uma coisa boa. Restrição nos faz pensar em como tornar as
coisas mais *eficazes* e com menos *desperdícios*.

Pense bem. Para fazer uma viagem para fora do seu país, por exemplo, você precisa 
planejar com cuidado o que levar na mochila.
Você deve escolher o que é mais *importante* e *essencial*, e nada a mais.
O motivo é viajar *leve* e curtir ao máximo, sem se preocupar com inúmeros objetos
ou malas cheias de coisas que você estaria arrastando com você.

É muito mais difícil *pensar* no que é essencial ao invés de "por tudo na mala",
mas é um exercício que vale a pena fazer. Você fica abismado ao saber que necessita
de tão pouco.

O mesmo vale para o seu código. Mantenha tudo *leve* e *simples*.
Apenas com o essencial. Porque **menos, é mais**.

Até logo.