# 🌦️ Controle Meteorológico — Coleta de Localização e Consulta Climática

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)

Sistema ponta a ponta para captura de coordenadas geográficas via interface web e consulta automatizada de dados meteorológicos em tempo real utilizando Python.

---

## 📋 Sobre o Projeto

O **Controle Meteorológico** resolve o fluxo de registro de pontos geográficos e monitoramento climático sem a necessidade de um banco de dados tradicional dedicado. O sistema é dividido em duas etapas principais:

1. **Coleta de Localização (Front-end Web):** Uma interface interativa onde o usuário pode buscar endereços, selecionar pontos diretamente em um mapa ou utilizar o GPS do dispositivo em tempo real para registrar um local[cite: 1]. Os dados são enviados de forma transparente para um **Google Forms**, que alimenta automaticamente uma planilha no **Google Sheets**[cite: 1, 2].
2. **Processamento e Consulta Climática (Pipeline Python):** Um notebook em Python (executável no Google Colab) que consome a planilha do Google Sheets em formato CSV, itera sobre cada localidade registrada e consulta a temperatura atual (2 metros acima do solo) por meio da API gratuita **Open-Meteo**[cite: 2].

---

## 🏗️ Arquitetura e Fluxo de Dados

```text
[Interface Web (index.html)] 
       │  (POST via URLSearchParams)
       ▼
[Google Forms] ──► [Google Sheets (Base CSV)]
                          │  (pd.read_csv)
                          ▼
               [Notebook Python / Colab] ◄──► [API Open-Meteo]

```

---

## ✨ Funcionalidades

### 🌐 Interface Web (`index.html`)

* **GPS em Tempo Real:** Rastreamento automático via `navigator.geolocation.watchPosition` com indicador visual de precisão (círculo de raio no mapa).


* **Busca de Endereços (Geocoding):** Autocomplete integrado à API **Nominatim (OpenStreetMap)** com filtro para o Brasil (`countrycodes=br`).


* **Mapa Interativo (Leaflet.js):** Tema escuro personalizado, permitindo clicar no mapa ou arrastar o marcador para ajustar as coordenadas manualmente.


* **Integração Direta com Google Forms:** Envio assíncrono (`no-cors`) formatando latitude e longitude como texto literal para evitar erros de separador decimal no Google Sheets.



### 🐍 Análise e Coleta Meteorológica (`Colete_de_Dados_Metorologicos.ipynb`)

* **Leitura Dinâmica:** Importação direta dos registros atualizados da planilha pública do Google Sheets via `pandas`.


* **Consulta Climática:** Requisições HTTP via biblioteca `requests` à API **Open-Meteo** (`temperature_2m`) para cada par de latitude e longitude cadastrado.



---

## 📂 Estrutura do Repositório

```text
Controle-Meteorologico/
├── index.html                            # Aplicação web de check-in e captura de coordenadas
├── Colete_de_Dados_Metorologicos.ipynb   # Notebook Python para leitura da planilha e consulta à API
└── README.md                             # Documentação do projeto

```

---

## 🚀 Como Utilizar

### 1. Registrar Localizações (Front-end)

1. Clone este repositório:
```bash
git clone [https://github.com/okamA3/Controle-Meteorologico.git](https://github.com/okamA3/Controle-Meteorologico.git)

```


2. Abra o arquivo `index.html` em qualquer navegador moderno (ou hospede-o via GitHub Pages).


3. Preencha o **Nome do Local**, escolha a posição via **GPS**, **Busca de Endereço** ou **Clique no Mapa** e clique em **Registrar Localização**.



> **Nota de configuração:** Caso deseje apontar para o seu próprio formulário, altere a constante `FORM_ACTION_URL` e os atributos `name="entry.XXXX"` no arquivo `index.html`.
> 
> 

### 2. Consultar Dados Meteorológicos (Python / Colab)

1. Abra o notebook `Colete_de_Dados_Metorologicos.ipynb` no **Google Colab** (ou localmente com Jupyter Notebook).


2. Certifique-se de ter as dependências instaladas caso rode localmente:
```bash
pip install pandas requests

```


3. Execute as células em sequência para carregar a tabela do Google Sheets e visualizar o retorno JSON com a elevação e temperatura atual de cada ponto.



---

## 🛠️ Tecnologias Utilizadas

* **Front-end:** HTML5, CSS3 (Custom Properties & Grid/Flexbox), JavaScript (ES6+)


* **Mapas e Geolocalização:** [Leaflet.js v1.9.4](https://leafletjs.com/), [OpenStreetMap / Nominatim API](https://nominatim.org/), Geolocation API


* **Armazenamento:** Google Forms & Google Sheets


* **Análise & Integração:** Python 3, [Pandas](https://pandas.pydata.org/), [Requests](https://requests.readthedocs.io/), [Open-Meteo API](https://open-meteo.com/)



---

## 📄 Licença

Este projeto está sob a licença MIT. Sinta-se à vontade para usar, modificar e distribuir.

```

---

### 💡 Dicas rápidas antes de subir:
1. **Segurança/Privacidade:** Notei que o `index.html` tem a URL real de envio do seu Google Forms e o notebook tem o link público da planilha[cite: 1, 2]. Se o repositório for público, qualquer pessoa poderá enviar dados de teste para esse formulário — o que é ótimo para portfólio/demonstração, mas vale ter em mente.
2. **GitHub Pages:** Como o seu front-end é um arquivo `index.html` puro (HTML + CSS + JS embutidos)[cite: 1], você pode ativar o **GitHub Pages** nas configurações do repositório (`Settings > Pages > Branch: main`) e colocar o link funcional no topo do README!

Se quiser que eu ajuste o tom, adicione alguma seção extra (como prints de tela ou planos futuros) ou traduza para o inglês, é só avisar!

```
