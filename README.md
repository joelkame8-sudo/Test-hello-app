# Minimal Android App with GitHub Actions

Ce projet est une application Android minimale configurée avec Gradle (Kotlin DSL).

## Fonctionnalités
- Une seule activité principale (`MainActivity`)
- Un texte "Hello World!" au centre
- Un bouton "Cliquez-moi" qui affiche un message (Toast) lorsqu'il est cliqué
- Intégration continue via GitHub Actions pour compiler automatiquement l'APK (`assembleDebug`) à chaque push/pull request sur `main` ou `master`.

## Structure du projet

- `settings.gradle.kts` : Configuration globale de Gradle et inclusion du module `:app`.
- `build.gradle.kts` : Configuration globale des plugins de build Android et Kotlin.
- `gradle.properties` : Propriétés Gradle (utilisation d'AndroidX, JVM options, etc.).
- `app/` :
  - `build.gradle.kts` : Définition des dépendances (AndroidX, Material components) et configuration de build de l'application.
  - `src/main/AndroidManifest.xml` : Fichier manifeste de l'application. Utilise l'icône système par défaut pour rester minimal.
  - `src/main/res/` : Ressources de l'application (layouts XML, strings, couleurs, thèmes).
  - `src/main/java/com/example/minimalapp/MainActivity.kt` : Code source Kotlin avec l'implémentation de l'activité.
- `.github/workflows/android.yml` : Workflow GitHub Actions pour compiler l'APK de débogage et le téléverser en tant qu'artefact.

## Compiler localement

Pour compiler l'application localement, vous devez avoir **Java 17** installé.

1. Installez Gradle localement si ce n'est pas déjà fait.
2. Pour générer les scripts de wrapper Gradle (`gradlew`) locaux, exécutez la commande suivante à la racine du projet :
   ```bash
   gradle wrapper --gradle-version 8.4
   ```
3. Compilez l'APK en mode debug :
   ```bash
   ./gradlew assembleDebug
   ```
L'APK généré sera disponible dans le dossier `app/build/outputs/apk/debug/app-debug.apk`.

## CI/CD (GitHub Actions)

À chaque `push` ou `pull_request` sur les branches `main` ou `master`, le workflow GitHub Actions :
1. Configure JDK 17.
2. Installe Gradle 8.4.
3. Exécute la compilation via `gradle assembleDebug`.
4. Sauvegarde et rend disponible au téléchargement le fichier `app-debug.apk` sous forme d'artefact de build.