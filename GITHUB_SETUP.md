# 🚀 Compilar SBuster via GitHub Actions

## O que é GitHub Actions?

**GitHub Actions** é um serviço de CI/CD (Integração Contínua) que compila seu app automaticamente na nuvem quando você faz push do código. Você não precisa de Android Studio ou SDK local!

## ✅ Passo a Passo

### 1. Criar Conta GitHub (Gratuita)

- Acesse: https://github.com
- Clique em "Sign up"
- Complete o cadastro

### 2. Criar um Novo Repositório

1. Clique em "+" (canto superior direito)
2. Selecione "New repository"
3. **Nome:** `sbuster-android`
4. **Descrição:** "SBuster - Game Performance Booster for Blood Strike"
5. **Público** (para que todos vejam)
6. Clique em "Create repository"

### 3. Fazer Upload do Código

**Opção A: Via Git CLI (Recomendado)**

```bash
# Clone o repositório
git clone https://github.com/SEU_USUARIO/sbuster-android.git
cd sbuster-android

# Copie os arquivos do SBuster para aqui
cp -r /home/ubuntu/sbuster-android/* .

# Adicione ao Git
git add .
git commit -m "Initial SBuster commit with Kotlin source"
git push origin main
```

**Opção B: Via GitHub Web Interface**

1. Abra seu repositório no GitHub
2. Clique em "Add file" → "Upload files"
3. Arraste os arquivos da pasta `/home/ubuntu/sbuster-android/`
4. Clique em "Commit changes"

### 4. Ativar GitHub Actions

1. No repositório, clique em "Actions"
2. Você verá o workflow "Build SBuster APK"
3. Clique em "Run workflow"
4. Aguarde a compilação (5-10 minutos)

### 5. Baixar o APK

1. Após a compilação, clique no workflow
2. Você verá "Artifacts" com dois APKs:
   - **sbuster-debug** — Para testes
   - **sbuster-release** — Para produção
3. Clique para baixar

## 📱 Instalar no Celular

### Via USB

```bash
adb install sbuster-debug.apk
```

### Via Download Direto

1. Baixe o APK no celular
2. Abra o arquivo
3. Toque em "Instalar"

### Via Compartilhamento

1. Baixe no computador
2. Compartilhe via WhatsApp, Telegram, Drive, etc.
3. Abra no celular e instale

## 🔄 Compilar Novamente

Sempre que você fizer mudanças:

```bash
git add .
git commit -m "Descrição das mudanças"
git push origin main
```

GitHub Actions compilará automaticamente!

## 📊 Monitorar Compilação

1. Acesse seu repositório
2. Clique em "Actions"
3. Você verá o histórico de compilações
4. Clique em uma compilação para ver detalhes

## ⚠️ Troubleshooting

### Erro: "Build failed"

1. Verifique se o `build.gradle.kts` está correto
2. Verifique se o `AndroidManifest.xml` tem todas as permissões
3. Verifique se não há erros de sintaxe Kotlin

### Erro: "Gradle build timeout"

- GitHub Actions tem limite de 6 horas por job
- Se o build demora muito, otimize o `build.gradle.kts`

### Erro: "SDK not found"

- O workflow instala o SDK automaticamente
- Se falhar, verifique a versão do `compileSdk` no `build.gradle.kts`

## 💡 Dicas

- **Primeira compilação leva mais tempo** (10-15 minutos)
- **Compilações subsequentes são mais rápidas** (5-7 minutos)
- **Você pode compilar múltiplas vezes por dia** (limite: 2000 minutos/mês)
- **Tudo é gratuito** para repositórios públicos

## 🎯 Próximos Passos

1. Crie o repositório no GitHub
2. Faça push do código
3. Execute o workflow
4. Baixe o APK
5. Teste no seu celular!

---

**Precisa de ajuda?** Consulte a documentação oficial:
- GitHub Actions: https://docs.github.com/en/actions
- Android Gradle: https://developer.android.com/build
- Kotlin: https://kotlinlang.org/docs/

**Sucesso! 🚀**
