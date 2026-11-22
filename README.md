# ZYON FF MOD MENU v2.0 — Security Core

Projeto Android em Kotlin + Jetpack Compose, interface preta e vermelha.

## Incluído
- Painel inicial, perfis e simulador independente de precisão.
- Auditoria local do próprio aplicativo:
  - build marcada como debuggable;
  - depurador conectado;
  - indicadores básicos conhecidos de root;
  - SHA-256 do certificado de assinatura instalado.
- Perfis de sensibilidade criptografados com AES-GCM usando chave Android Keystore.
- Backup Android desativado para evitar exportação automática dos dados privados do app.
- Sem permissão de internet, overlay, acessibilidade ou acesso ao processo do Free Fire.

## Abrir e compilar
1. Extraia o ZIP.
2. Abra a pasta no Android Studio.
3. Instale Android SDK 35 e JDK 17.
4. Aguarde o Gradle Sync.
5. Selecione Build > Build APK(s).
6. APK debug: `app/build/outputs/apk/debug/app-debug.apk`.

## Fixar o certificado da versão de produção
A tela de segurança mostra o SHA-256 do certificado instalado. Para que a checagem de assinatura seja conclusiva:
1. Gere/defina a chave de assinatura de release no Android Studio.
2. Instale uma build assinada com essa chave e copie o SHA-256 exibido.
3. Adicione ao `gradle.properties`:
   `ZYON_RELEASE_CERT_SHA256=SEU_SHA256_HEXADECIMAL`
4. Gere novamente a versão release com a mesma chave.

Se o valor não for configurado, a auditoria exibirá a fixação como pendente. Builds debug e release normalmente usam certificados diferentes.

## Limites técnicos
As verificações locais são sinais de diagnóstico e podem ser contornadas ou gerar falsos positivos. Não equivalem a atestado remoto. Para distribuição pela Google Play, uma etapa posterior pode integrar Play Integrity API com validação no servidor. Isso exige projeto Google Cloud/Play Console e backend próprio.

O aplicativo não injeta código, não modifica memória/processos do Free Fire e não oferece bypass, ESP ou automação de partidas. Não há promessa de imunidade a banimentos; a arquitetura mantém o app separado do jogo.


## Compilar usando somente o celular (GitHub Actions)
Este ZIP inclui `.github/workflows/android.yml` para compilar o APK na nuvem.

1. No navegador do celular, entre em https://github.com e crie uma conta ou entre.
2. Crie um repositório novo, por exemplo `zyon-ff-mod-menu`. Deixe-o privado se preferir.
3. Extraia o ZIP no celular. No GitHub, abra o repositório e use **Add file > Upload files**.
   Envie o conteúdo da pasta do projeto, incluindo a pasta oculta `.github`.
4. Faça **Commit changes** na branch `main`.
5. Abra a aba **Actions**, selecione **Build ZYON FF APK** e toque em **Run workflow** se não iniciar automaticamente.
6. Quando terminar com status verde, abra a execução e baixe o artefato `zyon-ff-debug-apk`.
7. Extraia o artefato ZIP baixado; dentro estará `app-debug.apk`. Toque nele para instalar.

Observação: o GitHub Actions compila em um servidor remoto; você controla tudo pelo celular,
mas não compila localmente no aparelho. O APK debug é para testes. Para distribuição,
gere uma versão release assinada com uma chave privada guardada com segurança.
