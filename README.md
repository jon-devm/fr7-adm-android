# FR7 ADM — app Android (APK)

App Android do **FR7 ADM Control** (VSS CAP SYSTEMS). Ele abre o sistema publicado
(`https://jn-fr7-control.lovable.app`) em tela cheia, com câmera e localização liberadas,
então toda atualização publicada no sistema já aparece no app, sem reinstalar.

## Baixar e instalar

1. Abra a aba **Releases** deste repositório no celular e baixe o arquivo `FR7-ADM-x.y.z.apk` mais recente.
2. Toque no arquivo e instale. Se o Android pedir, permita **instalar apps desconhecidos** para o navegador.
3. Abra o **FR7 ADM**, entre com o seu e-mail e senha e permita câmera e localização quando pedir.

## Como o APK é gerado

Cada envio para o ramo `main` roda o GitHub Actions (`.github/workflows/android.yml`):
instala o Capacitor, gera o APK assinado e publica em **Releases**.

- Assinatura: segredos `ANDROID_KEYSTORE_BASE64`, `ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_ALIAS` e
  `ANDROID_KEY_PASSWORD`. Sem eles, o APK sai com chave de teste (instala, mas cada build exige reinstalar).
- Versão: `APP_VERSION` no workflow (acompanha a versão do sistema mostrada no rodapé).

## Estrutura

- `capacitor.config.json` — endereço do sistema, nome e ID do app (`br.com.vsscap.fr7adm`).
- `android/` — projeto Android (ícones, permissões, tela cheia em `MainActivity.java`).
- `www/index.html` — tela mostrada quando não há conexão.

Uso licenciado. Venda ou redistribuição proibidas. © VSS CAP SYSTEMS.

## Versão 3 (app nativo)

- **Leitor de códigos nativo** (Google ML Kit): botão "Leitor do Android" no escanear, na ronda e na passagem de posto.
- **Entrada por digital**: depois de entrar com a senha, o app oferece ativar. O acesso fica no cofre do Android (Keystore).
- **Notificações push** (chat, novo cadastro, cadastro aprovado): precisam do segredo `GOOGLE_SERVICES_JSON` neste repositório e do `FIREBASE_SERVICE_ACCOUNT` no servidor do sistema. Sem eles, o APK funciona normalmente, só sem notificações.
- **Sem internet**: abre a última versão guardada e continua registrando; envia tudo quando a rede volta.
