# Guia: Enviando seu projeto para o GitHub

Seu projeto está pronto para ser enviado para o GitHub! Siga os passos abaixo:

## 1. Criar repositório no GitHub

1. Acesse https://github.com/new
2. Dê um nome ao repositório (ex: `apple-fruit-hedging`)
3. Adicione uma descrição: "Analysis of hedging strategies for apple fruit futures using exchange rate and climate data"
4. Deixe como **Public** (para ser visível) ou **Private** (para uso pessoal)
5. NÃO marque "Initialize with README" (já temos um)
6. Clique em **Create repository**

## 2. Conectar repositório local ao GitHub

Após criar o repositório, você verá uma página com instruções. Execute os comandos abaixo:

```powershell
cd "g:\Meu Drive\Colab Notebooks\apple-fruit-hedging"
git branch -M main
git remote add origin https://github.com/SEUUSUARIO/apple-fruit-hedging.git
git push -u origin main
```

**Substituir:**
- `SEUUSUARIO` pelo seu username do GitHub

## 3. Autenticação

Na primeira vez, o Git pedirá suas credenciais. Você tem duas opções:

### Opção A: Personal Access Token (Recomendado)
1. Gere um token em: https://github.com/settings/tokens
2. Quando pedir password, cole o token

### Opção B: GitHub CLI
```powershell
gh auth login
```

## 4. Comandos úteis para o futuro

Após cada mudança no seu projeto:

```powershell
cd "g:\Meu Drive\Colab Notebooks\apple-fruit-hedging"

# Ver status
git status

# Adicionar arquivos
git add .

# Fazer commit
git commit -m "Descrição da mudança"

# Enviar para GitHub
git push
```

## 5. Estrutura que foi criada

```
apple-fruit-hedging/
├── notebooks/
│   └── Apple.ipynb                    # Seu notebook principal
├── data/
│   ├── APFUTURES2020-2025.txt        # Dados históricos de preços
│   ├── APOPTIONS2023-2025.txt        # Dados de opções
│   ├── taxa de juros china.txt       # Taxa de juros China
│   └── apple_dfs_backup.csv          # Backup dos dados processados
├── .gitignore                         # Arquivos a ignorar no Git
├── README.md                          # Documentação do projeto
├── requirements.txt                   # Dependências Python
└── .git/                              # Repositório Git local
```

## 6. Próximos passos (opcional)

- Adicione um badge de status no README
- Configure GitHub Actions para CI/CD (testes automáticos)
- Crie issues para rastrear melhorias futuras
- Considere adicionar um arquivo CONTRIBUTING.md se quiser colaboradores

## Suporte

Se tiver dúvidas sobre Git ou GitHub, consulte:
- Git: https://git-scm.com/doc
- GitHub: https://docs.github.com/
