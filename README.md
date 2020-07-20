Web Scrap de vagas de estágio em Python, usando as bibliotecas Selenium e Pandas.

Passos que segui para criar o script:

- Importar libs necessárias;
- Inicializar Selenium com Webdriver(Firefox);
- Passa o link de acesso ao Webdriver('https://autoweb.cieepr.org.br/CIEE.Autenticacao.MVC/Acesso');
- Guardar dentro de variáveis os elementos para interação com a página usando css selector(CPF, Senha, Botão de entrar);
- Inserir informações de login às variáveis citadas anteriormente;
- Enviar as informações clicando no botão de entrar(.submit());
- Aguardar 5s para a página seguinte carregar;
- Dentro do portal CIEE, guardar em uma variável o elemento "vagas" para acesso(css selector);
- Clicar no elemento "vagas" para acessar(.click());
- Aguarda 5s para a página seguinte carregar;
- Guardar dentro de uma variável a tabela de vagas do portal(xpath);
- Pegar o html da tabela;
- Com o Pandas, ler o elemento table do portal;
- Inserir em um Data Frame o conteúdo da table.
