---
layout: post
title:  "AlertDialog Xamarin Android C#"
date:   2022-09-05 15:00:00 -0300
categories: Dicas javascript
frase: 'Mil poderão cair ao teu lado, e dez mil à tua direita; mas tu não serás atingido".'
pag: Salmos 91:7
---

```
  Android.App.AlertDialog.Builder builder = new Android.App.AlertDialog.Builder(this);
  Android.App.AlertDialog alerta = builder.Create();
  alerta.SetCancelable(true);
  alerta.SetIcon(Android.Resource.Drawable.IcDialogInfo);
  //define o titulo
  alerta.SetTitle("Título de Confirmação!");
  //define a mensagem
  alerta.SetMessage("Mensagem de exemplo.");
  //define os 3 botões
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
