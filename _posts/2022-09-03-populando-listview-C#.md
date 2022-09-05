---
layout: post
title:  "Populando um ListView em C#"
date:   2022-09-05 15:00:00 -0300
categories: C# xamarin android
frase: 'Ora, a fé é o firme fundamento das coisas que se esperam, e a prova das coisas que não se vêem".'
pag: Hebreus 11
---

## Criando um ```ListView``` delimitando seu tamanho, populando, capturando e controlando eventos com ```ItemClick```.

### O que vamos ver aqui é basicamente uma ```"tag select do html5"```.

- Criamos um ```widget``` no axml.
-  ``` id="@+id/list" ``` Definimos um id para fazer a manipulação.
-  ``` background="#ccc" ``` Fundo cinza para facilitar o entendimento.
-  ``` android:layout_height="50dp" ``` Deixamos a altura limitada em 50dp pois esse é o objetivo.

Arquivo axml (view)

```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <LinearLayout
        android:orientation="vertical"
        android:minWidth="25px"
        android:minHeight="25px"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/linearLayout1">

        <LinearLayout
            android:layout_marginTop="20dp"
            android:layout_marginBottom="20dp"
            android:gravity="center"
            android:orientation="horizontal"
            android:minWidth="25px"
            android:minHeight="25px"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/linearLayout2">

        </LinearLayout>
        <ListView
            android:background="#ccc"
            android:minWidth="25px"
            android:minHeight="25px"
            android:layout_width="match_parent"
            android:layout_height="50dp"
            android:id="@+id/list" />
    </LinearLayout>
</RelativeLayout>
```

- ``` ListView _lv; ```
- ``` string[] itens; ```
- Declaramos duas variáveis, uma do tipo ListView e outra nosso array de exemplo.
- ``` _lv = FindViewById<ListView>(Resource.Id.list); ``` ligamos nossa variável da atividade com o widget da view.
- ``` itens = new string[] { "item 1", "item 2", "item 3" }; ``` iniciamos o array e "populamos" ele com dados simples.
- ``` _lv.ItemClick += _lv_ItemClick; ``` Criando o evento de click para cada item do nosso array
- ``` popularListView(); ``` Chamamos o método que vai encher nosso ListView com os dados fornecidos no array de exemplo (itens)
- No método popularListView() temos a seguinte linha
- ``` _lv.Adapter = new ArrayAdapter(this, Android.Resource.Layout.SimpleListItem1, itens); ```
- O primeiro argumento é o contexto.
- O segundo o estilo da nossa lista (temos várias em c#)
- o último nossa lista propriamente dita

- no evento ``` _lv_ItemClick ``` podemos observar que ele nos da um argumento. 
- Será por ele que vamos conseguir pegar a posição do array e "printar" na tela usando ``` Toast ```.
- ``` Toast.MakeText(this, itens[e.Position], ToastLength.Long).Show(); ```
- Com isso a cada click podemos saber qual item foi selecionado pelo usuário.

Arquivo cs (atividade)
```
using System;
namespace teste
{
    [Activity(Label = "@string/app_name", Theme = "@style/AppTheme", MainLauncher = true)]
    public class MainActivity: Activity
    {
        ListView _lv;
        string[] itens;
        
        protected override void OnCreate(Bundle savedInstanceState)
        {
            base.OnCreate(savedInstanceState);
            // Set our view from the "main" layout resource
            SetContentView(Resource.Layout.activity_main);
            _lv = FindViewById<ListView>(Resource.Id.list);

            itens = new string[] { "item 1", "item 2", "item 3" };

            _lv.ItemClick += _lv_ItemClick;
            popularListView();

        }

        private void _lv_ItemClick(object sender, AdapterView.ItemClickEventArgs e)
        {
            Toast.MakeText(this, itens[e.Position], ToastLength.Long).Show();
        }

        public void popularListView()
        {
            _lv.Adapter = new ArrayAdapter(this, Android.Resource.Layout.SimpleListItem1, itens);
        }
    }
}
```
