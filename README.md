# AgentLang
ia feita com pyautogui
import os

from dotenv import load_dotenv
from langchain.tools import tool
from langchain_community.utilities import SQLDatabase
from langchain_openai import ChatOpenAI
from langgraph.prebuilt import create_react_agent

# Lendo a variavel local de ambiente (.env)
load_dotenv()

db = SQLDatabase.from_uri("sqlite:///locadora.db")

schema = db.get_table_info(
    table_names=[
        "Cliente",
        "Filme",
        "ItemLocacao"
    ]
)

@tool
def execute_sql(query: str) -> str:
    """
    Executa consultas SQL
    """
    print("\nSQL: ")
    print(query)
    return db.run(query)

llm = ChatOpenAI(
    base_url="https://integrate.api.nvidia.com/v1",
    api_key=os.getenv("NVIDIA_API_KEY"),
    model="meta/llama-3.3-70b-instruct",
    temperature=0
)

SYSTEM_PROMPT = f"""
Voce é um especialista em Linguagem SQL.
Banco Disponivel: {schema}

regras:
- Utilize execute_sql.
- Use apenas SELECT.
- Responda em portugues.
- Mostre os Dados retornados pela Consulta.
- Não escreva apenas o formato do resultado.
- Sempre apresente os valores encontrados.
- Por fim Explique os resultados encontrados em linguagem natural portugues do Brasil.
"""

agent = create_react_agent(
    model=llm,
    tools=[execute_sql],
    prompt=SYSTEM_PROMPT
)

while True:
    pergunta = input("\nPergunta: ")
    if pergunta.lower() == "sair":
        break
    resposta = agent.invoke({
        "messages": [{
            "role": "user",
            "content": pergunta
        }]
    })
    print("\nResposta:")
    print(resposta["messages"][-1].content)
