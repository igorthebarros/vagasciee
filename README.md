Web Scrap de vagas de estágio em Python, usando as bibliotecas Selenium e Pandas.

#Importa libs necessárias.
from selenium import webdriver
import pandas as pd
from pandas.io.html import  read_html

#Inicializa Selenium com Webdriver.
browser = webdriver.Firefox()
#Passa o link de acesso ao Webdriver.
browser.get('https://autoweb.cieepr.org.br/CIEE.Autenticacao.MVC/Acesso')

#Guarda dentro de variáveis os elementos para interação com a página(css selector).
cpf = browser.find_element_by_css_selector('#CPF')
senha = browser.find_element_by_css_selector('#Password')
entrar = browser.find_element_by_css_selector('#formLogin > input.btn.btn-outline-primary')

#Insere informações de login às variáveis citadas anteriormente.
cpf.send_keys('000.000.000-00')
senha.send_keys('xxxxxx')
#Envia as informações pelo botão da variável "entrar".
entrar.submit()

#Aguarda 5s para a página seguinte carregar.
browser.implicitly_wait(5)

#Dentro do portal CIEE, salva elemento "vagas" para acesso(css selector).
vagas = browser.find_element_by_css_selector('#RedirecionarModuloVagaEstagioAntigo > a:nth-child(1)')
#Clica no elemento "vagas" para acessar
vagas.click()

#Aguarda 5s para a página seguinte carregar.
browser.implicitly_wait(5)

#Guarda dentro de uma variável a tabela de vagas do portal (xpath).
tabelaVagas = browser.find_element_by_xpath('//*[@id="cph_gvVagasEst"]')
#Pega o html da tabela
html_tabelaVagas = tabelaVagas.get_attribute('outerHTML')

#Com o Pandas, lê o elemento table do portal.
tabelaPandas = read_html(html_tabelaVagas, attrs={"class":"estiloGridEstudante"})

#Insere em um Data Frame o conteúdo da table.
for rows in tabelaPandas:
    df = pd.DataFrame(rows)

#'Printa' o conteúdo do Data Frame.
print(df)
