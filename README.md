# Desafio de Cibersegurança: Simulação Didática de Ransomware em Python

> **Aviso Legal:** Este projeto foi desenvolvido **estritamente para fins educacionais e de pesquisa em segurança da informação**, como parte do Bootcamp de Cibersegurança da **DIO (Digital Innovation One)**. O objetivo é compreender o mecanismo básico de cifragem simétrica utilizado por malwares do tipo ransomware para fins de conscientização e desenvolvimento de mecanismos de defesa. Qualquer uso malicioso ou não autorizado deste conhecimento é de inteira responsabilidade do executor.

---

## Visão Geral do Projeto

Ransomwares são ameaças cibernéticas que bloqueiam o acesso a dados de uma vítima — geralmente criptografando arquivos — e exigem o pagamento de um resgate para fornecer a chave de recuperação.

Neste laboratório prático, implementamos uma versão simplificada e controlada desse conceito:
1. **Script Criptografador (`encrypter.py`)**: Localiza um arquivo de teste específico, criptografa seus dados utilizando o algoritmo **AES (Advanced Encryption Standard)** em modo **CTR**, remove o arquivo original e salva a versão cifrada com uma extensão identificadora (`.ransomwaretroll`).
2. **Script Descriptografador (`decrypter.py`)**: Localiza o arquivo cifrado, processa a decifragem utilizando a mesma chave simétrica e restaura os dados originais.

---

## Estrutura de Arquivos

```text
.
├── encrypter.py         # Script que realiza a cifragem do arquivo alvo
├── decrypter.py         # Script que realiza a restauração do arquivo
├── teste.txt            # Arquivo de teste utilizado como cobaia no laboratório
├── requirements.txt     # Dependências necessárias do projeto
├── .gitignore           # Arquivos e diretórios ignorados pelo Git
└── README.md            # Documentação técnica completa
```

---

## Detalhamento Técnico

### Algoritmo de Criptografia
- **AES (Advanced Encryption Standard)**: Cifra simétrica de bloco amplamente adotada pela indústria.
- **Modo CTR (Counter Mode)**: Transforma a cifra de bloco em uma cifra de fluxo (stream cipher), gerando blocos de chave a partir de um contador criptografado e aplicando uma operação lógica `XOR` sobre os dados originais.
  - *Vantagem técnica*: Não exige *padding* (preenchimento para múltiplos de 16 bytes).
- **Chave Simétrica**: Uma chave fixa de 16 bytes (`b"testeransomwares"`), totalizando 128 bits de entropia definida para o ambiente de testes.

---

## Como Executar o Projeto

### 1. Pré-requisitos
Certifique-se de possuir o **Python 3.8+** instalado em seu sistema operacional.

### 2. Preparação do Ambiente
Recomenda-se a criação de um ambiente virtual para instalação das dependências:

```bash
# Criar o ambiente virtual
python3 -m venv venv

# Ativar o ambiente virtual no Linux/macOS:
source venv/bin/activate

# Ativar no Windows (PowerShell):
# .\venv\Scripts\Activate.ps1

# Instalar as dependências
pip install -r requirements.txt
```

### 3. Passo a Passo da Simulação

#### Passo A: Conferir o arquivo original
Verifique o conteúdo do arquivo `teste.txt`:
```bash
cat teste.txt
# Exibe o relatório de teste confidencial da simulação
```

#### Passo B: Executar a Cifragem
Execute o script de criptografia:
```bash
python3 encrypter.py
```
*O que acontece:*
- O arquivo `teste.txt` é lido e excluído.
- Um novo arquivo chamado `teste.txt.ransomwaretroll` é criado com o conteúdo cifrado.

#### Passo C: Executar a Restauração (Decifragem)
Para reverter o processo e recuperar os dados originais:
```bash
python3 decrypter.py
```
*O que acontece:*
- O arquivo `teste.txt.ransomwaretroll` é decifrado e removido.
- O arquivo `teste.txt` é restaurado com seu conteúdo original intacto.

---

## Boas Práticas de Defesa contra Ransomware

Na cibersegurança defensiva, a compreensão dos vetores de ataque permite estruturar melhores controles de segurança:

1. **Estratégia de Backup 3-2-1**:
   - 3 cópias dos dados importantes;
   - 2 mídias de armazenamento diferentes;
   - 1 cópia armazenada fora do ambiente (*off-site* ou em nuvem com retenção imutável).
2. **Princípio do Menor Privilégio (PoLP)**:
   - Limitar as permissões de gravação e execução de usuários e aplicações aos recursos estritamente necessários.
3. **Soluções de EDR e Antivírus Comportamental**:
   - Monitorar acessos anômalos em massa ao sistema de arquivos (ex.: múltiplas operações de leitura/escrita com exclusão em rajada).
4. **Conscientização e Treinamento**:
   - Prevenir os vetores iniciais de infecção mais frequentes, como *phishing* e anexos maliciosos de e-mail.

---

## Referências

- [Repositório Base - Digital Innovation One](https://github.com/cassiano-dio/cibersecurity-desafio-ransomware)
- [Documentação Oficial do PyAES](https://pypi.org/project/pyaes/)
- [NIST Special Publication 800-38A - Modes of Operation](https://csrc.nist.gov/publications/detail/sp/800-38a/final)
