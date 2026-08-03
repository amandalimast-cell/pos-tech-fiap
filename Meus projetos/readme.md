# Pós Tech Fiap - AI Data Scientist

### Inicio em 30 de Junho de 2026

Conceitos em python para deixar registrado.

### .. antes de um caminho de pasta
O conceito por trás: caminhos relativos vs. absolutos

Um caminho de arquivo pode ser absoluto (parte da raiz do sistema, ex: `C:/Users/.../data/arquivo.csv)` ou relativo - parte do diretório onde o processo está sendo executado — o chamado working directory, ou diretório de trabalho atual).

O `".."` é um símbolo especial reconhecido pelo sistema operacional (não é sintax

### Em tópicos

- O que o `..` resolve: se o notebook está em `meu_projeto/notebooks/` e o dado está em `meu_projeto/data/`, **não dá pra acessar o CSV com um caminho direto** — é preciso "sair" de `notebooks/ primeiro`. `../data/arquivo.csv` faz exatamente isso: sobe um nível (sai de notebooks/, chega em meu_projeto/) e desce em data/.

- De onde ele é resolvido: o caminho relativo é sempre calculado a partir do working directory do processo Python (os.getcwd()), não necessariamente da pasta onde o arquivo .ipynb está fisicamente salvo. Isso é uma pegadinha comum em notebooks.

- Quando funciona: só funciona se o notebook for executado (o kernel for iniciado) com o working directory sendo **notebooks/**. É o comportamento padrão do Jupyter/VS Code na maioria dos casos — o kernel inicia na pasta onde o .ipynb está.

- Quando quebra: se alguém rodar o notebook de outro lugar (ex: abrir o Jupyter a partir da raiz do repositório, ou rodar via script/CI a partir de outra pasta), o working directory muda e o ../data/... vai apontar para o lugar errado, gerando `FileNotFoundError`.

### Como conferir
    import os
    print(os.getcwd())  # mostra o working directory atual

### Alternativa mais robusta
    from pathlib import Path
    BASE_DIR = Path(__file__).resolve().parent  # ou Path().resolve() em notebook
    caminho_entrada = BASE_DIR.parent / "data" / "desafio_nps_fase_1.csv"

(em notebook, `__file__` não existe por padrão, então times costumam fixar o BASE_DIR manualmente ou usar `os.chdir()` no início do notebook para garantir consistência)


