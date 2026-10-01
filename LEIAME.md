# Bookly — Flutter

Biblioteca pessoal. Um projeto só, que roda em Android, iOS, web, macOS,
Windows e Linux. Ardósia `#0B0A11` com violeta `#7A5CE0`.

## Rodar

    flutter create . --platforms=android,ios,web
    flutter pub get
    flutter run

O `flutter create .` só gera as pastas de plataforma (android/, ios/, web/).
Ele não sobrescreve nada dentro de `lib/`.

## Estrutura

    lib/
      main.dart                  entrada, inicializa o Supabase se estiver ligado
      theme.dart                 cores, tipografia e o atalho de responsividade
      data.dart                  CONFIG do banco, modelos e repositório
      widgets/
        logo_b.dart              o B da marca (CustomPainter) e o lockup
        book_3d.dart             o livro: lombada + bloco de páginas em 3D
        shelf.dart               a estante, com paralaxe e o puxão no hover
        dock.dart                a pílula de navegação
      screens/
        splash_screen.dart       a abertura com o B se montando
        login_screen.dart        entrar (sem lógica enquanto useDb = false)
        home_screen.dart         casca do app + tela da estante
        book_screen.dart         tela do livro
        reader_screen.dart       o leitor, em tela cheia
        saved_screen.dart        páginas salvas

## Ligar o banco

Em `lib/data.dart`, na classe `Config`, vire `useDb` para `true`. A URL e a
anon key já são as do projeto do Nártiva. O `main.dart` chama
`Supabase.initialize()` sozinho quando a flag está ligada, e o `Repo` passa a
ler a tabela `books` em vez dos três livros de demonstração.

Enquanto estiver `false`, o botão Entrar avisa e entra assim mesmo, com os
livros de demonstração, para dar para navegar pelo app.

## O que ainda não existe

As páginas salvas vivem em memória (`Repo._salvas`), porque o Nártiva não tem
tabela para isso. Quando criar a `saved_pages`, troque `Repo.salvas` e
`Repo.salvarPagina` e o resto do app continua igual.

O leitor mostra um trecho fixo (`trechoDemo` em `data.dart`). Para ler PDF de
verdade entra um `pdfrx` ou `syncfusion_flutter_pdfviewer` na tela do leitor.
