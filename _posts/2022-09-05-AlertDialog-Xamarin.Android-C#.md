---
layout: post
title:  "AlertDialog Xamarin Android C#"
date:   2022-09-05 15:00:00 -0300
categories: Dicas javascript
frase: 'Mil poderão cair ao teu lado, e dez mil à tua direita; mas tu não serás atingido".'
pag: Salmos 91:7
---

### Explicação de cada linha

- Instância da classe AlertDialog
- ``` Android.App.AlertDialog.Builder builder = new Android.App.AlertDialog.Builder(this); ```

- Criamos o AlertDialog com o método Builder
- ``` Android.App.AlertDialog alerta = builder.Create(); ```

- define se o diálogo pode ser cancelado pela tecla Android.Views.KeyEvent.KEYCODE_BACK.
- ``` SetCancelable(true)  ```

- Define o ícone
- ``` alerta.SetIcon(Android.Resource.Drawable.IcDialogInfo); ```

- Define o título
- ``` alerta.SetTitle(""); ```

- Define a mensagem
- ``` alerta.SetMessage("Mensagem de exemplo."); ```

- Cria um botão com um evento click (Callback)  `IMPORTANTE:` Podemos exibir no máximo três botões.
- ``` alerta.SetButton("", (s, ev) => {} ```

- Mostra o alerta na tela
- alerta.Show();

### Exemplo de uso

```
  Android.App.AlertDialog.Builder builder = new Android.App.AlertDialog.Builder(this);
  Android.App.AlertDialog alerta = builder.Create();
  alerta.SetCancelable(true);
  alerta.SetIcon(Android.Resource.Drawable.IcDialogInfo);
  alerta.SetTitle("Título de Confirmação!");
  alerta.SetMessage("Mensagem de exemplo.");
  alerta.SetButton("Sim", (s, ev) =>
  {
      // Função de callback
  });
  alerta.SetButton2("Não", (s, ev) =>
  {
     // Função de callback
  });
  alerta.Show();
```
