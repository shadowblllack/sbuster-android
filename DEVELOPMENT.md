# Guia de Desenvolvimento — SBuster

## Arquitetura

O SBuster é estruturado em **3 serviços principais**:

### 1. MainActivity
- Interface principal com botões de controle
- Monitoramento de FPS, RAM e Temperatura
- Ativação do Booster Engine

### 2. BoosterService
Responsável por otimização:
- `cleanMemory()` — Força garbage collection e limpeza de cache
- `killBackgroundProcesses()` — Mata processos desnecessários
- `optimizeForGame()` — Otimização pré-game
- `getMemoryStats()` — Retorna estatísticas de memória

### 3. ScreenRecorderService
Responsável por gravação:
- Captura de tela via MediaRecorder
- Gravação de áudio interno (REMOTE_SUBMIX)
- Salvamento em MP4 com codec H.264
- Classe alternativa `AdvancedScreenRecorder` com MediaProjection

### 4. HUDOverlayService
Responsável por overlay flutuante:
- Cria uma janela overlay semi-transparente
- Atualiza FPS, RAM e Temperatura em tempo real
- Posicionável em qualquer lugar da tela

## Fluxo de Execução

```
MainActivity
    ├── onCreate()
    │   ├── enableImmersiveMode()
    │   ├── initializeViews()
    │   ├── startPerformanceMonitoring()
    │   └── setupButtonListeners()
    │
    ├── activateBooster()
    │   └── BoosterService.cleanMemory()
    │       ├── System.gc()
    │       ├── clearAppCache()
    │       └── trimMemory()
    │
    ├── toggleHUD()
    │   └── startService(HUDOverlayService)
    │       └── createHUDOverlay()
    │           └── startMonitoring()
    │
    └── toggleScreenRecorder()
        └── startService(ScreenRecorderService)
            └── startRecording()
```

## Modificações Comuns

### Adicionar Novo Botão

1. Adicione em `activity_main.xml`:
```xml
<Button
    android:id="@+id/newButton"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="Novo Botão" />
```

2. Inicialize em `MainActivity.kt`:
```kotlin
private lateinit var newButton: Button

private fun initializeViews() {
    newButton = findViewById(R.id.newButton)
}

private fun setupButtonListeners() {
    newButton.setOnClickListener {
        // Ação aqui
    }
}
```

### Adicionar Novo Serviço

1. Crie `NewService.kt` em `service/`:
```kotlin
class NewService : Service() {
    override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
        // Lógica aqui
        return START_STICKY
    }

    override fun onBind(intent: Intent?): IBinder? = null
}
```

2. Registre em `AndroidManifest.xml`:
```xml
<service
    android:name=".service.NewService"
    android:enabled="true"
    android:exported="false" />
```

3. Inicie de `MainActivity.kt`:
```kotlin
startService(Intent(this, NewService::class.java))
```

### Modificar Cores

Edite `app/src/main/res/values/colors.xml` e use em layouts:
```xml
android:textColor="@color/primary_cyan"
android:background="@color/background_dark"
```

## Testes

### Testar Booster
```kotlin
val booster = BoosterService(context)
val stats = booster.getMemoryStats()
println("RAM disponível: ${stats.availableMemory}MB")
```

### Testar HUD
1. Ative HUD via botão
2. Abra um jogo
3. Verifique se o overlay aparece sem interferir

### Testar Gravação
1. Clique em REC
2. Abra um jogo e jogue por 30 segundos
3. Clique em REC novamente
4. Verifique em `/storage/emulated/0/Movies/SBuster/`

## Performance

### Otimizações Implementadas
- Coroutines para operações assíncronas
- Garbage collection agressivo
- Trim de memória periódico
- Overlay com FLAG_NOT_FOCUSABLE (não consome eventos)

### Benchmarks Esperados
- Limpeza de memória: ~2-3 segundos
- Overhead de HUD: <5% CPU
- Gravação: ~50-60% CPU (dependendo do dispositivo)

## Debugging

### Ativar Logs
Em `MainActivity.kt`:
```kotlin
Log.d("SBuster", "FPS: $fps, RAM: $ram")
```

### Ver Logs via ADB
```bash
adb logcat | grep SBuster
```

### Debugar Serviços
```bash
adb shell dumpsys activity services
```

## Próximas Melhorias

- [ ] Integração com APIs nativas de temperatura real
- [ ] Suporte a perfis de performance personalizados
- [ ] Detecção automática de jogos
- [ ] Notificações de alerta (RAM/Temperatura crítica)
- [ ] Estatísticas de uso em tempo real
- [ ] Integração com MediaProjection para gravação real
- [ ] Suporte a HDR em gravações
- [ ] Compressão automática de vídeos

## Recursos Úteis

- [Android Developer Docs](https://developer.android.com/)
- [Kotlin Coroutines](https://kotlinlang.org/docs/coroutines-overview.html)
- [MediaRecorder API](https://developer.android.com/reference/android/media/MediaRecorder)
- [Window Manager](https://developer.android.com/reference/android/view/WindowManager)

---

**Desenvolvido com ❤️ pelo Clã ShadowBlack**
