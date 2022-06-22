---
layout: post
title:  "Criando modal com javascript puro"
date:   2022-06-22 06:00:00 -0300
categories: Dicas javascript
frase: 'Então o Senhor Deus declarou: "Não é bom que o homem esteja só; farei para ele alguém que o auxilie e lhe corresponda".'
pag: Gênesis 2:18
---

### O objetivo é focar na lógica por trás do modal. Explicarei as partes do `CSS` que realmente importam para funcionar, e deixarei o arquivo completo para consulta no final do artigo.

Para começar vamos deixar o `HTML` assim:

```
  <div class="the-modal" >
    <button type="button" class="btnModal">Modal</button>
    <div class="modal">
      <button class="btnSair">x</button>
    </div>
  </div>
  
```

Agora precisamos fazer alguns ajustes no arquivo `CSS`.

A classe `the-modal` é apenas para âncorar e ajustar o modal no centro da tela.
```
.the-modal{
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
```

Note, a classe `modal` principia com `display: none;`, assim, ocultando todo o modal.
Faça um teste, remova o `display-none` e coloque `block` na classe `modal`. Você notará que temos um quadrado na cor violeta. 
Obs: Coloque o `display-none` novamente.
```
.modal{
  display: none;
  position: absolute;
  transition: .5s;
  margin: auto;
  width: 300px;
  height: 300px;
  background-color: #6A5ACD;
  border: solid 1px #000;
}
```

Se você fez o teste, notou que o botão herdou o mesmo estilo do modal.
Basicamente, vamos deixar ele no topo da nossa página e estilizar o botão sair.
```
.btnModal{
  position: absolute;
  top: 0;
  width: 80px;
  height: 30px;
  font-size: 1.1em;
  cursor: pointer;
}

.btnSair{
  position: absolute;
  right: 0;
  top: 0;
  background-color: transparent;
  border: none;
  cursor: pointer;
  width: 30px;
  height: 30px;
  font-size: 1.2em;
}

.btnSair:hover{
  background-color:#C0C0C0;
}
```
Agora vamos para parte que particularmente mais gosto, código puro.
Código `JavaScript`.
Nota: Vou adicionar um modal com efeito de transição mais abaixo.

A priori, criei três constantes (Pedaços de memória ram, que não mudam de valor).
```
const btnModal = document.querySelector(".btnModal")
const btnSair = document.querySelector(".btnSair")
const modal = document.querySelector(".modal")
const body = document.querySelector("body")
```
Uma das estruturas de `event click` usando `JavaScript`.
Deixei o modal visível e "removi o foco do fundo".
```
btnModal.onclick = () => {
  modal.style.display = "block"; 
  body.style.backgroundColor = "#363636"
}
```
Simplismente, voltamos ao estado default.
```
btnSair.onclick = () => {
  modal.style.display = "none";
  body.style.backgroundColor = "#C0C0C0"
}
```
O modal básico está feito, agora vamos dar uma melhorada nele.
É possível adicionar efeitos de animações com `CSS` e chamar com `JavaScript`.
Vou usar o `keyframes` para fazer as animações e adicionar o efeito em tempo de execução.

```
.fadeIn{
  animation-name: fadeIn;
  animation-duration:.5s;
}

@keyframes fadeIn {
  from{
    opacity: 0;
  }
  to{
    opacity: 1;
  }
}

```

Adicionamos a classe do `fade` (efeito) aqui.
O código mais "refinado", com efeito ficaria algo assim:
```
btnModal.onclick = () => {
  modal.classList.add('fadeIn')
  modal.style.display = "block"; 
  body.style.backgroundColor = "#363636"
}
```
Bom, tem mais um bonûs.
A título de curiosidade. 
### E se quiséssemos dar efeito de transição, na hora que o evento sair fosse disparado?
Para isso, precisamos entender como o código é executado.
Porque este exemplo não funcionária?
Quando o efeito fosse chamado, o modal quase no mesmo instânte ficaria invisível.
```
btnSair.onclick = () => {
  modal.classList.remove('fadeIn')
  modal.classList.add('fadeOut')
  modal.style.display = "none";
  body.style.backgroundColor = "#C0C0C0"
}
```
Por conseguinte, temos funções assíncronas, no caso do `JavaScript` para esse caso específico.
Precisamos dar um tempo para o efeito ser executado e depois ocultar o display.
O método setTimeOut, precisa de dois parâmetros, callback (É uma função passada a outra função como argumento, que é então invocado dentro da função externa para completar algum tipo de rotina ou ação.) e tempo para chamar a callback.
```
btnSair.onclick = () => {
  modal.classList.remove('fadeIn')
  modal.classList.add('fadeOut')
  
  setTimeout(()=> {
    modal.style.display = "none";
    body.style.backgroundColor = "#C0C0C0"
  }, 1000)
}
```

Resumo: Com este artigo vimos como criar um modal simples com `JavaScript` puro, `keyframes`, animações `CSS` e conceitos como `callbacks`, métodos assíncronos.
