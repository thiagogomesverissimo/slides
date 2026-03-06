---
author: Thiago Gomes Verissimo
date: 2026-03-06
format:
  revealjs:
    incremental: true
    slide-number: true
    theme: solarized
    transition: fade
title: Laravel
---

## O que é o Laravel?

Laravel é um **framework PHP moderno** para desenvolvimento de
aplicações web.

Ele fornece:

-   estrutura organizada de código
-   ferramentas prontas para desenvolvimento
-   segurança e boas práticas
-   alta produtividade

------------------------------------------------------------------------

## Por que usar um framework?

Sem framework:

-   código desorganizado
-   repetição de código
-   manutenção difícil

Com framework:

-   estrutura padronizada
-   reutilização de código
-   desenvolvimento mais rápido

------------------------------------------------------------------------

## Arquitetura MVC

Laravel utiliza o padrão **MVC**.

MVC significa:

**Model -- View -- Controller**

------------------------------------------------------------------------

## Model

Responsável por representar os **dados da aplicação**.

Funções principais:

-   comunicação com o banco de dados
-   regras de negócio
-   relacionamentos entre dados

Exemplo:

``` php
class Post extends Model
{
}
```

------------------------------------------------------------------------

## View

Responsável pela **interface com o usuário**.

Mostra os dados gerados pela aplicação.

No Laravel usamos **Blade**.

Exemplo:

``` php
<h1>{{ $post->title }}</h1>
```

------------------------------------------------------------------------

## Controller

O controller faz a **mediação entre Model e View**.

Responsabilidades:

-   receber requisições
-   processar dados
-   retornar respostas

Exemplo:

``` php
class PostController extends Controller
{
    public function index()
    {
        $posts = Post::all();
        return view('posts.index', compact('posts'));
    }
}
```

------------------------------------------------------------------------

## Fluxo de uma requisição

Usuário\
↓\
Rota\
↓\
Controller\
↓\
Model\
↓\
View\
↓\
Resposta ao usuário

------------------------------------------------------------------------

## Criando um projeto Laravel

``` bash
composer create-project laravel/laravel blog
```

Entrar no diretório:

``` bash
cd blog
```

Executar servidor local:

``` bash
php artisan serve
```

------------------------------------------------------------------------

## Estrutura do Laravel

Principais diretórios:

    app/
    routes/
    resources/
    database/
    public/

------------------------------------------------------------------------

## Arquivo de rotas

As rotas web ficam em:

    routes/web.php

Exemplo:

``` php
Route::get('/', function () {
    return view('welcome');
});
```

------------------------------------------------------------------------

# CRUD

CRUD representa as operações básicas de banco de dados.

-   **Create**
-   **Read**
-   **Update**
-   **Delete**

------------------------------------------------------------------------

## Exemplo de aplicação

Vamos criar um sistema simples de **posts**.

Cada post terá:

-   título
-   conteúdo

------------------------------------------------------------------------

## Criando Model e Migration

``` bash
php artisan make:model Post -m
```

Isso cria:

-   o model `Post`
-   uma migration para a tabela

------------------------------------------------------------------------

## Migration

Arquivo criado em:

    database/migrations

Exemplo:

``` php
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->text('content');
    $table->timestamps();
});
```

Executar migrations:

``` bash
php artisan migrate
```

------------------------------------------------------------------------

## Criando Controller

``` bash
php artisan make:controller PostController
```

------------------------------------------------------------------------

## Método index

Responsável por listar registros.

``` php
public function index()
{
    $posts = Post::all();

    return view('posts.index', compact('posts'));
}
```

------------------------------------------------------------------------

## Rota para listar posts

``` php
Route::get('/posts', [PostController::class, 'index']);
```

------------------------------------------------------------------------

# CREATE

Criar novo registro.

Controller:

``` php
public function store(Request $request)
{
    Post::create($request->all());

    return redirect('/posts');
}
```

------------------------------------------------------------------------

## Formulário de criação

``` html
<form method="POST" action="/posts">

@csrf

<input type="text" name="title">

<textarea name="content"></textarea>

<button type="submit">
Salvar
</button>

</form>
```

------------------------------------------------------------------------

# READ

Listar registros.

Controller:

``` php
$posts = Post::all();
```

View:

``` php
@foreach($posts as $post)

<h2>{{ $post->title }}</h2>

@endforeach
```

------------------------------------------------------------------------

# UPDATE

Atualizar registro.

``` php
public function update(Request $request, $id)
{
    $post = Post::find($id);

    $post->update($request->all());

    return redirect('/posts');
}
```

------------------------------------------------------------------------

# DELETE

Excluir registro.

``` php
public function destroy($id)
{
    $post = Post::find($id);

    $post->delete();

    return redirect('/posts');
}
```

------------------------------------------------------------------------

## Rotas Resource

Laravel pode criar automaticamente todas as rotas CRUD.

``` php
Route::resource('posts', PostController::class);
```

Isso cria automaticamente:

    index
    create
    store
    show
    edit
    update
    destroy

------------------------------------------------------------------------

## Resumo

Laravel oferece:

-   arquitetura MVC
-   ORM Eloquent
-   sistema de rotas
-   migrations
-   controllers
-   Blade templates

Essas ferramentas permitem desenvolver aplicações web **de forma
organizada e produtiva**.

------------------------------------------------------------------------

## Exercício

Criar um CRUD completo para:

-   alunos
-   produtos
-   tarefas

Utilizando:

-   Model
-   Migration
-   Controller
-   Views
