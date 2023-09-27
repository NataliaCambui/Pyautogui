# Pyautogui
Automação de processos com python

Aprendi a realizar uma automação, que preenche produtos de uma planilha em um banco de dados de uma empresa fictícia, utilizando a biblioteca pyautogui.
A automação abre o chrome
Realiza login e senha
Localiza planilha.csv e inclui os itens em um banco de dados. 


import pyautogui
import time
import pandas

#1 passo: Entrar no sistema da empresa
pyautogui.press("win")
pyautogui.PAUSE = 0.2
pyautogui.write("chrome")
pyautogui.press("enter")
time.sleep(3)     
#1. Entrar no link
pyautogui.write("//dlp.hashtagtreinamentos.com/python/intensivao/login")
pyautogui.press("enter")
time.sleep(3)     

#Esperar o site carregar
time.sleep(3)  

# 2. Fazer loguin
pyautogui.click(x = 707, y = 498)
pyautogui.write("cambui.natalia@gmail.com")
pyautogui.press("tab")
pyautogui.write("123456")
pyautogui.press("tab")
pyautogui.press("enter")
               
#3. passo: importar a base de dados do produto
tabela = pandas.read_csv("produtos.csv")
print(tabela)

#4 Passo: Cadastrar um produto
for linha in tabela.index:
    pyautogui.click(x = 691, y = 351)
    codigo = tabela.loc[linha,"codigo"]
    #—> preencher os campos
    pyautogui.write(str(codigo))
    pyautogui.press("tab")
    pyautogui.write(str(tabela.loc[linha,"marca"]))
    pyautogui.press("tab")
    pyautogui.write(str(tabela.loc[linha,"tipo"]))
    pyautogui.press("tab")
    pyautogui.write(str(tabela.loc[linha,"categoria"]))
    pyautogui.press("tab")
    pyautogui.write(str(tabela.loc[linha, "preco_unitario"]))
    pyautogui.press("tab")
    pyautogui.write(str(tabela.loc[linha, "custo"]))
    pyautogui.press("tab")
    obs = tabela.loc[linha,"obs"]               
    if not pandas.isna(obs):
        pyautogui.write(str(tabela.loc[linha, "obs"]))
    #—> apertar para enviar
    pyautogui.press("tab") 
    pyautogui.press("enter")
    pyautogui.scroll(5000)
