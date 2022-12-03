# MeuApp_Cotacao

from kivy.app import App<br>
from kivy.lang import Builder<br>
import requests<br>

GUI = Builder.load_file("tela.kv")<br>

class MeuAplicativo(App):<br>
    def build(self):<br>
        return GUI<br>

    def on_start(self):<br>
        self.root.ids["moeda1"].text = f"Dólar R${self.pegar_cotacao('USD')}"<br>
        self.root.ids["moeda2"].text = f"Euro R${self.pegar_cotacao('EUR')}"<br>
        self.root.ids["moeda3"].text = f"Bitcoin R${self.pegar_cotacao('BTC')}"<br>
        self.root.ids["moeda4"].text = f"Ethereum R${self.pegar_cotacao('ETH')}"<br>

    def pegar_cotacao(self, moeda):<br>
        link = f"https://economia.awesomeapi.com.br/last/{moeda}-BRL"<br>
        requisicao = requests.get(link)<br>
        dic_requisicao = requisicao.json()<br>
        cotacao = dic_requisicao[f"{moeda}BRL"]["bid"]<br>
        return cotacao<br>



MeuAplicativo().run()<br>
