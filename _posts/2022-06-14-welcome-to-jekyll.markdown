---
layout: post
title:  "Comparando Strings com Java!"
date:   2022-06-14 11:35:59 -0300
categories: Dicas de Java
---
Existe várias maneiras de comparar `Strings` no Java. Vou usar neste exemplo, duas formas de comparação. A primeira e mais comum é usando o método `equals` simples. A segunda é utilizando o `equalsIgnoreCase`.


1-Exemplo usando `equals`:

{% highlight ruby %}

String txtNome = txtNome.getText("Exemplo"); #=> Imagine uma entrada de dados que o usuário digitou "Exemplo" e enviou o formulário.
String nome = "exemplo"; #=> Criei uma variável do tipo String;Recebendo o mesmo valor da entrada de dados, porém com a primeira letra minúscula.

if(txtNome.equals(nome)){
  #=> Segundo o exemplo acimao o fluxo do código seguiria e não entraria nessa condição.
}

O método `equals` diferencia letras minúsculas de maiúsculas.

{% endhighlight %}

2- Exemplo usando `equalsIgnoreCase`:

{% highlight ruby %}

Usaremos as mesmas variáveis e valores do primeiro código.

if(txtNome.equalsIgnoreCase(nome)){
  #=> Neste caso, o fluxo do código entraria nessa condição.
}

O método `equalsIgnoreCase` trata letras minúsculas e maiúsculas, como se fossem iguais.

{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
