## O diagrama do meu RAG

Para entender na prática, nada melhor que um desenho. Este é o diagrama do RAG que eu uso hoje — e repare: **o usuário humano está ao centro do processo**, não no início. Ele é o ponto central, a razão de tudo existir.

```mermaid
flowchart TD
    %% Centro: o usuário humano
    GABRIEL["👤 Gabriel Subtil<br/>(usuário humano)"]

    %% RAGs próprios (auto-hospedados)
    BS["📚 BookStack<br/>(estante de livros)"]
    WIKI["📖 Wiki.js<br/>(wiki)"]
    BW["🔐 Bitwarden<br/>(cofre de senhas)"]

    %% Ferramentas de IA
    HERMES["🤖 Hermes Agent"]
    VSC["💻 VS Code / Antigravity IDE"]

    %% RAGs públicos
    CTX7["🌐 Context7<br/>(RAG público - docs de código)"]

    %% Web search
    WEB["🔎 Web Search"]

    %% Conexões do usuário humano (centro)
    GABRIEL --- HERMES
    GABRIEL --- VSC
    GABRIEL --- BS
    GABRIEL --- WIKI
    GABRIEL --- BW

    %% Ferramentas se conectam aos RAGs próprios
    HERMES --- BS
    HERMES --- WIKI
    HERMES --- BW
    VSC --- BS
    VSC --- WIKI
    VSC --- BW

    %% Web search
    HERMES --- WEB
    VSC --- WEB

    %% RAGs públicos via MCP
    HERMES --- CTX7
    VSC --- CTX7
```

**Como ler o diagrama:** eu (Gabriel) estou no centro. Me conecto diretamente aos meus RAGs (BookStack, Wiki.js, Bitwarden) e às minhas ferramentas de IA (Hermes Agent e VS Code). Essas ferramentas também se conectam aos mesmos RAGs — então, quando eu peço algo ao Hermes Agent ou ao VS Code, eles buscam no mesmo conhecimento que eu uso. E tanto o Hermes Agent quanto o VS Code fazem **web search** e usam **RAGs públicos** (como o Context7) para ter documentação atualizada de código.

## RAGs públicos (sugestão)

Nem todo RAG precisa ser seu. Muitos conhecimentos já existem em repositórios públicos — não faz sentido todo time de TI manter um banco de dados de manual de todos os códigos quando existe um repositório público. Aqui está uma tabela de RAGs públicos que você pode usar:

| RAG público | Intenção | Como eu utilizo |
|---|---|---|
| **Context7** | Documentação atualizada de código | Via MCP (quem tem acesso: meu VS Code e meu Hermes Agent) |
