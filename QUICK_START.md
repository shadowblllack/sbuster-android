# 🚀 Quick Start — SBuster Android

## ⚡ Compilação Rápida

### Opção 1: Android Studio (Recomendado)

```bash
1. Abra Android Studio
2. File → Open → Selecione a pasta sbuster-android
3. Aguarde sincronização do Gradle
4. Build → Build Bundle(s) / APK(s) → Build APK(s)
5. APK gerado em: app/build/outputs/apk/release/
```

### Opção 2: Gradle CLI

```bash
cd sbuster-android
./gradlew assembleRelease
# APK em: app/build/outputs/apk/release/app-release.apk
```

### Opção 3: Debug (Desenvolvimento)

```bash
./gradlew assembleDebug
# APK em: app/build/outputs/apk/debug/app-debug.apk
```

## 📱 Instalação no Dispositivo

```bash
adb install app/build/outputs/apk/release/app-release.apk
```

## ✅ Verificar Instalação

```bash
adb shell pm list packages | grep sbuster
# Saída: package:com.shadowblack.sbuster
```

## 🎮 Usar o App

1. **Abra SBuster** no seu dispositivo
2. **Toque em BOOST** para limpar memória
3. **Toque em HUD: OFF** para ativar monitoramento flutuante
4. **Toque em REC: PARADO** para gravar gameplay

## 📋 Requisitos Mínimos

- Android 8.0+ (API 26)
- 50MB de espaço livre
- Permissões: Storage, Áudio, Overlay

## 🔧 Troubleshooting

### Erro: "SDK not found"
```bash
# Configure ANDROID_HOME
export ANDROID_HOME=/path/to/android/sdk
```

### Erro: "Gradle sync failed"
```bash
./gradlew clean
./gradlew build
```

### Permissões não funcionam
- Vá em Configurações → Apps → SBuster → Permissões
- Ative todas as permissões manualmente

## 📚 Documentação Completa

- Leia `README.md` para funcionalidades detalhadas
- Leia `DEVELOPMENT.md` para arquitetura e modificações

---

**SBuster v1.0** — Desenvolvido pelo Clã ShadowBlack 🎮
