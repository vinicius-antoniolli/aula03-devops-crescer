# 🤯 O Problema

- [Notion do projeto](https://glen-boat-8a6.notion.site/ShareSolving-io-Arezzo-76cc8dd51168467ea1b5beac7e367977)

#### Atualmente diante da vasta imensidão da internet, os usuarios tem enfrentado dificuldade em encontrar conhecimentos centralizados, tendo que procurar em diversas fontes diferentes e não encontrando facilmente um conteúdo correto e concreto.
- Encontrar conteúdo de qualidade em um local centralizado com diversos assuntos;
- Economizar tempo no processo de busca de conteúdos específicos;
- Ter um local com grades de conhecimento e documentações específicas.


# 💡 Proposta de Solução
## Visão Geral🧐

A área da tecnologia é muito grande, com diversos caminhos para a solução de um mesmo problema, é inviavel conhecer todas as tecnologias e frameworks, pois é um processo que levaria um tempo imenso, poder encontrar de maneira fácil uma solução viável e que vai resolver o necessário para o usuario, irá tornar mais simples e agradável o processo de aprendizado;
A proposta consiste em uma aplicação em que o usuario pode buscar por algum conteúdo e a aplicação traz todos os conteúdos relacionados, sempre pelo mais bem avaliado.
O usuario pode enriquecer a aplicação com quaisquer de seus conhecimentos e avaliar o conhecimentos e conteúdos dos demais usuarios.
Pode também conversar e interagir com outros usuarios através de um chat e um campo de dúvidas e interações na aplicação.

## Aplicacão
- Cadastro de usuarios
- Usuarios postam os conteúdos: videos curtos, dúvidas(se der tempo).
- Vídeos serão avaliados pelos proprios usuarios
- Vídeos serão tageados para filtrar o conteúdo que o usuario quer ver
- Ao pesquisar por um vídeo ou tag, trará como resultado os relacionados com a pesquisa, paginados e organizado pelas avaliações
- Usuario poderá criar um RoadMap com as tecnologias que ele está trabalhando, assim trazendo os melhores conteúdos daquela's trilha's escolhida's
- Usuario poderá pesquisar e interagir com outros usuarios através de um chat
- Usuario poderá entrar nos perfis de outros usuarios, trazendo os conteúdos publicado pelo usuario, tambem paginado e organizado por data de postagem.

## Complexidade
### WebSocket
- Usuario poderá pesquisar e interagir com outros usuarios através de um chat em tempo real

# 👥 Definição de Usuários
## Usuario

Consistem em quem fará a utilizacao da aplicação, postagem dos conteúdos e avaliação dos demais conteúdos postados.

# 🔌 Integração

### A integração ocorrerá via banco de dados e minIO. Será recebido uma carga de dados de:

### MinIO
- Fará o upload do vídeo através da aplicação

### Banco de dados (Postgres)
#### Tabelas do banco de dados:

### Usuario
- id_usuario [PK]
- nome_completo
- email
- senha
- data_nascimento
- foto_perfil
- descricao
- genero

========= ↓
### Video
- id_video [PK]
- url (Aqui ficará a URL gerada pelo MinIO)

### Tag_video
- id_tag_video [PK]
- id_video [FK]
- tag

### Avaliacao_video
- id_avaliacao_video [PK]
- id_video [FK]
- avaliacao

### Duvida_video
- id_avalicao_video [PK]
- id_video [FK]
- duvida
- id_comentario_duvida

========= ↑

### Comentario_duvida
- id_comentario_duvida [PK]
- id_duvida_video [FK]
- comentario

## 🔒 Autenticação
Autenticação será feita através do spring security e tambem terá um login integrado com o google, algumas referências:
- [Spring security](https://spring.io/projects/spring-security)
- [Google oAuth2.0](https://developers.google.com/identity/protocols/oauth2)
- [Google oAuth2 login + Spring security](https://www.baeldung.com/spring-security-5-oauth2-login)

## ⚙️ Funcionalidades

### Upload de um novo vídeo
#### Ao fazer o upload de um novo vídeo na plataforma o usuario deve informar:
- Titulo do vídeo
- Tags do vídeo
- Descricao do vídeo
- Arquivo de vídeo

### Cadastro de usuarios
#### Ao se cadastrar na plataforma o usuario deve informar:
- Nome completo
- Email
- Senha
- Confirmacao de senha
- Data de nascimento
- Foto de perfil (opcional)
- Descrição
- Gênero

### Perfil de usuarios
#### Ao entrar no perfil de outros usuarios o usuario autenticado poderá:
- Ver os vídeos postados pelo usuario
- Enviar mensagem direta para o usuario (CHAT)
- Avaliar os vídeos do usuario
- Ver os dados do perfil do usuario

### Video-aulas
#### Ao entrar em uma video-aula o usuario terá as opções de:
- Avaliar a video-aula
- Criar uma pergunta ou dúvida e através dela interagir com outros usuarios
- Curtir o video
- Visitar videos relacionados ao que ele esta vendo
- Avaliação dos vídeos vai de 1 a 5, sendo 1 ruim e 5 ótimo

### Criação de trilha de conhecimento
#### Ao iniciar uma nova trilha de conhecimento o usuario terá as opções de:
- Escolher as categorias do projeto (linguagem, ferramentas, banco de dados)
- Gerar um minicurso com os categorias selecionadas, filtradas por maior avaliação
