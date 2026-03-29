# SBuster — Game Booster Android Nativo

**SBuster** é um aplicativo Android nativo desenvolvido em **Kotlin** para a comunidade Blood Strike pelo **Clã ShadowBlack**. É um Game Booster tático que otimiza a performance do dispositivo para jogos.

## 🎮 Funcionalidades

### 1. **Booster Engine** (Motor de Otimização)
- Limpeza real de memória RAM
- Eliminação de processos em background desnecessários
- Limpeza de cache de aplicativos
- Trim de memória agressivo
- Otimização automática antes de abrir jogos

### 2. **Gravador de Tela (Pro-Clip)**
- Gravação de gameplay em 1080p/60fps
- Suporte a áudio interno (game) e externo (microfone)
- Formato MP4 com codec H.264
- Salvamento automático em galeria
- Estilo ADV Gravador com alta fidelidade

### 3. **HUD Flutuante (Overlay)**
- Monitoramento em tempo real de FPS
- Monitoramento de RAM disponível
- Monitoramento de temperatura do dispositivo
- Overlay semi-transparente que não interfere com jogos
- Atualização a cada 500ms

### 4. **Modo Imersivo**
- Interface sem barras de navegação
- Experiência fullscreen total
- Compatível com Android 5.0+

### 5. **UI Cyberpunk ShadowBlack**
- Paleta de cores: Vermelho (#FF0000) + Ciano (#00F2FF)
- Design terminal hacker
- Botão BOOST circular com efeito neon
- Cards com borda ciano

## 📋 Requisitos

- **Android SDK**: API 26+ (Android 8.0+)
- **Gradle**: 8.1.0+
- **Kotlin**: 1.9.0+
- **Java**: 11+

## 🛠️ Compilação

### Via Android Studio

1. Abra o Android Studio
2. Selecione "Open an Existing Project"
3. Navegue até a pasta `sbuster-android`
4. Aguarde o Gradle sincronizar
5. Clique em "Build" → "Build Bundle(s) / APK(s)" → "Build APK(s)"

### Via Gradle CLI

```bash
cd sbuster-android
./gradlew assembleRelease
```

O APK será gerado em: `app/build/outputs/apk/release/app-release.apk`

## 📦 Instalação

```bash
adb install app/build/outputs/apk/release/app-release.apk
```

## 🔐 Permissões Necessárias

O app solicita as seguintes permissões:

- `KILL_BACKGROUND_PROCESSES` — Matar processos em background
- `RECORD_AUDIO` — Gravação de áudio
- `WRITE_EXTERNAL_STORAGE` — Salvar gravações
- `SYSTEM_ALERT_WINDOW` — HUD flutuante
- `PACKAGE_USAGE_STATS` — Monitorar uso de apps

## 🎯 Uso

### Booster Engine
1. Toque no botão **BOOST** no centro da tela
2. O app limpará memória e matará processos
3. Aguarde a conclusão (barra de progresso)

### HUD Flutuante
1. Toque em **HUD: OFF** para ativar
2. Um overlay aparecerá no canto superior direito
3. Toque novamente para desativar

### Gravador de Tela
1. Toque em **REC: PARADO** para iniciar gravação
2. O app gravará a tela com áudio
3. Toque novamente para parar
4. Vídeo será salvo em: `/storage/emulated/0/Movies/SBuster/`

## 📁 Estrutura do Projeto

```
sbuster-android/
├── app/
│   ├── src/main/
│   │   ├── java/com/shadowblack/sbuster/
│   │   │   ├── MainActivity.kt
│   │   │   └── service/
│   │   │       ├── BoosterService.kt
│   │   │       ├── ScreenRecorderService.kt
│   │   │       └── HUDOverlayService.kt
│   │   ├── res/
│   │   │   ├── layout/
│   │   │   │   └── activity_main.xml
│   │   │   ├── drawable/
│   │   │   │   └── boost_button_bg.xml
│   │   │   └── values/
│   │   │       ├── strings.xml
│   │   │       ├── colors.xml
│   │   │       └── themes.xml
│   │   └── AndroidManifest.xml
│   ├── build.gradle.kts
│   └── proguard-rules.pro
├── build.gradle.kts
├── settings.gradle.kts
└── README.md
```

## 🔧 Configuração Avançada

### Modificar Paleta de Cores

Edite `app/src/main/res/values/colors.xml`:

```xml
<color name="primary_red">#FF0000</color>
<color name="primary_cyan">#00F2FF</color>
```

### Ajustar Resolução de Gravação

Em `ScreenRecorderService.kt`, modifique:

```kotlin
setVideoSize(1080, 1920)  // Largura x Altura
setVideoFrameRate(60)      // FPS
setVideoEncodingBitRate(5000000)  // Bitrate em bps
```

### Customizar HUD

Em `HUDOverlayService.kt`, ajuste:

```kotlin
x = 0      // Posição X
y = 100    // Posição Y
```

## 🐛 Troubleshooting

### "Permission Denied" ao gravar
- Conceda permissões manualmente em Configurações → Apps → SBuster → Permissões

### HUD não aparece
- Ative "Permitir exibição sobre outros apps" em Configurações → Apps → SBuster

### Booster não funciona
- Alguns dispositivos podem bloquear `killBackgroundProcesses()` — isso é normal

## 📝 Licença

Desenvolvido pelo **Clã ShadowBlack** para a comunidade Blood Strike.

## 👥 Créditos

- **Desenvolvedor**: Clã ShadowBlack
- **Comunidade**: Blood Strike Players
- **Inspiração**: ADV Gravador, Game Boosters

---

**SBuster v1.0** — *Resistência e suporte à comunidade de Blood Strike* 🎮
