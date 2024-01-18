<!-- Imagem redimensionada -->
<img src="https://digitalcollege.com.br/wp-content/webp-express/webp-images/uploads/2022/05/logo-digital.png.webp" alt="texto alt" width="300">

# Módulo de Python - Formação Data Analytics - Aula 01

# Projeto: Análise Base de Dados - Diabetes

O projeto consiste em utilizar a Linguagem Python para analisar uma Base de Dados em arquivo CSV, com informações de pacientes com Diabetes 💼🔗


## 🚀 Começando


> **Foi dividida a análise em 4 etapas:**

1. **Preparação do Ambiente Python**:

Nesta etapa, fizemos a criação de um ambiente virtual chamado Digital, para que os projetos desse módulo estive isolado de demais projetos existentes.

Dentro das pasta Projetos, foi ativado o ambiente virtual Digital e salvo a base de dados (CSV), com as informações de saúde.

Istalamos as bibliotecas/extensão:
   
**Watermark:** é uma biblioteca em Python que permite a fácil adição de marcas d'água (watermarks) em notebooks Jupyter. Essa biblioteca é comumente utilizada para adicionar informações sobre versões de bibliotecas, data de execução e outras informações relevantes aos resultados gerados em notebooks.

**ipython-sql:** é uma extensão do IPython (Interactive Python) que facilita a interação com bancos de dados SQL diretamente nos notebooks Jupyter. Ela permite a execução de comandos SQL de forma interativa e integrada com o ambiente de programação Python, facilitando a análise de dados armazenados em bancos de dados relacionais.

**pandas:** é uma biblioteca popular em Python utilizada para manipulação e análise de dados. Ela oferece estruturas de dados flexíveis, como o DataFrame, que permite a organização e manipulação eficiente de conjuntos de dados tabulares. O pandas simplifica tarefas comuns em análise de dados, como filtragem, limpeza, agregação e visualização.

**psycopg2:** é uma biblioteca de adaptação do PostgreSQL para Python. Essa biblioteca fornece uma interface de programação para permitir a comunicação eficiente entre aplicativos Python e bancos de dados PostgreSQL. Ela é utilizada para executar consultas SQL, inserir, atualizar e recuperar dados de bancos de dados PostgreSQL diretamente em programas Python.


2. **Importando as bibliotecas**: Nesta etapa, importamos as bibliotecas psycopg2 e pandas, para darmos sequência ao projeto e criação do dataframe.

3. **Desafio Proposto**
   
![image](https://github.com/NayaraWakewski/PythonDigital/assets/79403619/c4047f40-3a01-4c5d-958a-eb9ef45b5b22)
 

## 🚀 RESOLUÇÃO DESAFIO

> Nessa etapa utilizamos PYTHON para análise dos dados, criação do dataframe, conexão com o banco de dados postgres e criação de tabelas e consultas SQL.

**Resolução feita em um Jupyter Notebook, conforme parte do Script abaixo; (Script completo em anexo no repositório).

```python

# Lendo o arquivo CSV e criando o Dataframe
df = pd.read_csv('arquivos/diabetes.csv')

#Consultando a quantidade de linhas e colunas
df.shape

#Consultando informações do dataframe
df.info()

.....

#Código de inserção dos dados, no banco de dados Postgres, com o tratamento de erros de inserção no código.

for index, row in df.iterrows():
    try:
        crsr.execute("""INSERT INTO public.diabetes(pregnancies, glucose, blood_pressure, skin_thickness,
                     insulin, bmi, diabetes_pedigree_function, age, outcome)
                     VALUES (%s, %s, %s, %s, %s, %s, %s, %s, %s)""",
                     (row['Pregnancies'], row['Glucose'], row['BloodPressure'], row['SkinThickness'], row['Insulin'], row['BMI'],
                      row['DiabetesPedigreeFunction'], row['Age'], row['Outcome']))
        conn.commit()
    except Exception as e:
        print(f"Erro ao inserir linha {index}: {str(e)}")
        conn.rollback()  # Reverta a transação em caso de erro

# Feche o cursor após o loop
crsr.close()

.....

#Criando a tabela de pacientes
%%sql

CREATE TABLE IF NOT EXISTS public.pacientes
(
    id serial,
    pregnacies integer,
    glucose integer,
    blood_pressure integer,
    skin_thicknes integer,
    insulin integer,
    bmi numeric(18,1),
    diabetes_pedigree_function numeric(18,3),
    age integer,
    outcome integer,
    CONSTRAINT pacientes_pkey PRIMARY KEY (id)
)


```

## 🚀 **Resultado de Algumas Análises**





## ⚙️ Arquivos no Repositório:


-**Arquivo Jupyter Notebook**.

-**Arquivo CSV da base de Dados**.



## 🎁 Expressões de gratidão

* Compartilhe com outras pessoas esse projeto 📢;
* Quer saber mais sobre o projeto? Entre em contato para tomarmos um :coffee:;

---
⌨️ com ❤️ por [Nayara Vakevskii](https://github.com/NayaraWakewski) 😊
