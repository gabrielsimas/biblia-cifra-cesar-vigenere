[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/gabrielsimas/biblia-cifra-cesar-vigenere/blob/master/MVP_BibliaCifraCesarVigenere.ipynb)

# Criptoanálise Clássica com Machine Learning: Um MVP para a PUC-Rio

## Um projeto de Data Science & Analytics para decodificação de cifras de César e Vigenère.

Este repositório contém o MVP (Minimum Viable Product) desenvolvido para a Pós-Graduação em Ciência de Dados e Analytics da Pontifícia Universidade Católica do Rio de Janeiro (PUC-Rio). O projeto explora a aplicação de um pipeline híbrido de Machine Learning e criptoanálise estatística para classificar e decifrar textos criptografados com cifras clássicas.

---

### Tabela de Conteúdos
* [Sobre o Projeto](#sobre-o-projeto)
* [Arquitetura da Solução](#arquitetura-da-solução)
* [O Dataset](#o-dataset)
* [Resultados Principais](#resultados-principais)
* [Estrutura do Repositório](#estrutura-do-repositório)
* [Como Executar](#como-executar)
* [Autor](#autor)

---

### Sobre o Projeto

O objetivo central deste trabalho foi desenvolver um sistema capaz de realizar duas tarefas de criptoanálise a partir de um texto cifrado:

1.  **Classificação:** Identificar qual cifra foi utilizada (Cifra de César ou Cifra de Vigenère).
2.  **Decodificação:** Reverter o processo de criptografia para recuperar o texto original em português.

O projeto se destaca pela criação de um dataset original a partir da Bíblia Sagrada em português e pela jornada de desenvolvimento, que pivotou de uma complexa abordagem inicial com Redes Neurais para uma solução híbrida e pragmática, culminando em um pipeline avançado com múltiplos modelos de Machine Learning.

---

### Arquitetura da Solução

A solução final é um pipeline híbrido orquestrado em Python, composto pelos seguintes estágios:

1.  **Classificador Principal (César vs. Vigenère):**
    * Um modelo **XGBoost** treinado para classificar o tipo de cifra com base em atributos estatísticos extraídos do texto cifrado. Os principais atributos utilizados foram o **Índice de Coincidência (IC)** e a **distribuição de frequência de caracteres**.

2.  **Pipeline de Decodificação Condicional:**
    * Com base na previsão do classificador, o texto é direcionado para o decodificador apropriado:
        * **Se for César:** É aplicado um decodificador estatístico que testa todas as 25 chaves de deslocamento e escolhe aquela que maximiza a semelhança com a frequência de letras da língua portuguesa.
        * **Se for Vigenère:** É acionado um sub-pipeline avançado de Machine Learning, composto por dois modelos especialistas:
            1.  **Modelo Preditor de Tamanho de Chave (XGBoost):** Prevê o comprimento da chave com base em um vetor de ICs médios.
            2.  **Modelo Preditor de Letras da Chave (XGBoost):** Prevê cada letra da chave com base na distribuição de frequência dos sub-textos cifrados.

Este design modular permite a aplicação da ferramenta mais adequada para cada desafio, combinando a velocidade e precisão do XGBoost com a lógica da criptoanálise clássica.

---

### O Dataset

O dataset utilizado foi inteiramente gerado para este projeto. Versículos da Bíblia Sagrada em português foram processados e cifrados com as cifras de César e Vigenère de forma balanceada. O dataset final, salvo em formato Parquet, contém não apenas os textos, mas também metadados cruciais como a `chave_usada`, permitindo o treinamento supervisionado dos modelos.

---

### Resultados Principais

* **Classificador Principal:** O modelo XGBoost alcançou uma performance excepcional, com **99.68% de acurácia** na distinção entre as cifras no conjunto de teste.
* **Decodificador de César:** O pipeline estatístico obteve **100% de sucesso** na decodificação de todos os textos corretamente classificados como César.
* **Decodificador de Vigenère:** A abordagem final com Machine Learning demonstrou a capacidade de decifrar uma parcela dos textos. A análise conclusiva do projeto demonstrou que a performance é limitada pela natureza dos dados (versículos curtos), que não possuem a profundidade estatística necessária para uma criptoanálise consistentemente bem-sucedida, mesmo com técnicas avançadas de ML.

---

### Como Executar

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/seu-usuario/seu-repositorio.git](https://github.com/seu-usuario/seu-repositorio.git)
    cd seu-repositorio
    ```
2.  **Ambiente:** O projeto foi desenvolvido no Google Colab. Recomenda-se o uso deste ambiente para garantir a compatibilidade das bibliotecas.
3.  **Instale as dependências:** As bibliotecas necessárias (`xgboost`, `scikit-learn`, `pandas`, `numpy`) são instaladas diretamente no notebook.
4.  **Execute o Notebook:** Abra o arquivo `MVP_BibliaCifraCesarVigenere.ipynb` no Google Colab ou em um ambiente Jupyter e execute as células em ordem. Certifique-se de que os caminhos para os arquivos de dataset e modelos estejam corretos.

---

### Autor

* **Luís Gabriel Nascimento Simas**

---