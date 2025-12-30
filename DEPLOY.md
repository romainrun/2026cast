# Guide de déploiement - Cast Receiver sur GitHub Pages

## Étape 1 : Créer le repository GitHub

1. Allez sur [GitHub](https://github.com) et connectez-vous
2. Cliquez sur le bouton **"+"** en haut à droite → **"New repository"**
3. Nommez le repository : `2026-countdown-cast-receiver` (ou un autre nom)
4. Cochez **"Public"** (obligatoire pour GitHub Pages gratuit)
5. **Ne cochez PAS** "Initialize with README"
6. Cliquez sur **"Create repository"**

## Étape 2 : Uploader les fichiers

### Option A : Via l'interface GitHub (simple)

1. Dans votre nouveau repository, cliquez sur **"uploading an existing file"**
2. Glissez-déposez les 3 fichiers suivants depuis le dossier `cast_receiver/` :
   - `index.html`
   - `manifest.json`
   - `background.js`
3. Cliquez sur **"Commit changes"**

### Option B : Via Git (si vous avez Git installé)

```bash
cd /Users/romain.ricquebourg/Projects/2026Resolutions/cast_receiver
git init
git add index.html manifest.json background.js
git commit -m "Initial commit - Cast receiver"
git branch -M main
git remote add origin https://github.com/VOTRE_USERNAME/2026-countdown-cast-receiver.git
git push -u origin main
```

## Étape 3 : Activer GitHub Pages

1. Dans votre repository GitHub, allez dans **Settings** (en haut)
2. Dans le menu de gauche, cliquez sur **Pages**
3. Sous **Source**, sélectionnez :
   - Branch: `main` (ou `master`)
   - Folder: `/ (root)`
4. Cliquez sur **Save**
5. Attendez quelques minutes que GitHub déploie
6. Votre URL sera : `https://VOTRE_USERNAME.github.io/2026-countdown-cast-receiver/`
7. **Testez l'URL** dans votre navigateur - vous devriez voir le countdown

## Étape 4 : Enregistrer le Receiver dans Google Cast Console

1. Allez sur [Google Cast Console](https://cast.google.com/publish)
2. Connectez-vous avec votre compte Google
3. Cliquez sur **"Add New Application"**
4. Sélectionnez **"Custom Receiver"**
5. Remplissez le formulaire :
   - **Application Name** : `2026 Countdown`
   - **Receiver URL** : `https://VOTRE_USERNAME.github.io/2026-countdown-cast-receiver/index.html`
   - **Category** : `Entertainment` (ou autre)
6. Cliquez sur **"Save"**
7. **IMPORTANT** : Copiez le **Application ID** (Receiver ID) - il ressemble à `ABCD1234` ou `12345678`
   - Vous le trouverez dans la liste des applications après la création

## Étape 5 : Mettre à jour l'app Android

1. Ouvrez le fichier : `app/src/main/java/com/kns/resolutions/cast/CastOptionsProvider.kt`
2. Trouvez la ligne avec `DEFAULT_MEDIA_RECEIVER_APPLICATION_ID`
3. Remplacez-la par votre Receiver ID :

```kotlin
override fun getCastOptions(context: Context): CastOptions {
    return CastOptions.Builder()
        .setReceiverApplicationId("VOTRE_RECEIVER_ID_ICI") // Remplacez par votre ID
        .build()
}
```

4. Rebuild et déployez l'app

## Étape 6 : Tester

1. Assurez-vous que votre téléphone et votre TV sont sur le même Wi-Fi
2. Ouvrez l'app sur votre téléphone
3. Cliquez sur l'icône Cast
4. Sélectionnez votre TV
5. Le countdown devrait maintenant s'afficher sur votre TV ! 🎉

## Dépannage

- **La TV montre toujours l'icône Cast** : Vérifiez que le Receiver ID est correct dans `CastOptionsProvider.kt`
- **"Receiver not found"** : Vérifiez que GitHub Pages est activé et que l'URL est accessible
- **Le countdown ne se met pas à jour** : Vérifiez que les deux appareils sont sur le même Wi-Fi

## Notes importantes

- Le receiver doit être accessible via HTTPS (GitHub Pages le fait automatiquement)
- Le Receiver ID peut prendre quelques minutes à être actif après la création
- Si vous changez le Receiver ID, vous devrez peut-être redémarrer l'app

