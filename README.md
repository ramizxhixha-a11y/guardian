# AURA8 · Bug Splitting Forensic Auditor

Détection d'incohérences de découpage, audit forensique de fichiers, recovery, et base de connaissances auto-apprenante. **100% offline. 100% navigateur.**

## Ce que ça fait

- **Audit automatique** : scanner intelligent qui détecte 11 types d'incohérences (fichiers lourds, accolades déséquilibrées, JSON invalide, lignes trop longues, encoding mixte, TODOs, nesting excessif, blocs dupliqués, références orphelines, trailing whitespace, et patterns AURA8).
- **Recovery d'urgence** : backup auto avant chaque audit/fix, force-restore, comparaison avec backup pour repérer pertes.
- **Suggestions** : heuristiques basées sur les patterns appris dans la KB. Pas de LLM — c'est de l'algorithmie déterministe.
- **Base de connaissances** : chaque pattern détecté + fix appliqué est mémorisé (localStorage). Import/export JSON.
- **Profil AURA8** : pré-configuré avec marqueurs `@section`, conventions de découpage logique.
- **Tests intégrés** : 20 tests réels exécutés dans le navigateur, visibles dans l'onglet TESTS. Aucun mock.
- **Auto-fix** : corrige automatiquement les line-endings et trailing whitespace. Les autres issues sont signalées avec une suggestion de fix.

## Lancement

Ouvre `index.html` dans n'importe quel navigateur moderne. C'est tout. Aucune dépendance, aucun build, aucun serveur.

## Déploiement GitHub Pages

```bash
git init
git add index.html README.md .github/
git commit -m "AURA8 v1.0"
git remote add origin https://github.com/<user>/<repo>.git
git push -u origin main
```

Puis : Settings → Pages → Source: `main` / `(root)`. Ton outil est à `https://<user>.github.io/<repo>/`.

Le workflow `.github/workflows/pages.yml` déploie automatiquement à chaque push sur `main`.

## Honnêteté technique

**Ce que c'est** :
- Une heuristique de détection de patterns sur fichiers texte
- Un système de persistance via localStorage
- Une UI forensique avec console live

**Ce que ce n'est pas** :
- Un LLM (les "suggestions IA" sont des heuristiques + KB apprise)
- Un analyseur syntaxique complet (pas d'AST, juste du pattern-matching robuste)
- Un service cloud (tout reste local)

## Tests

Onglet **TESTS** → bouton "RUN ALL TESTS". 20 tests couvrent : hashing, formatters, tous les détecteurs, backup/restore, persistance, KB.

État au moment du release : **20/20 PASS**.

## Configurabilité

Onglet **CONFIG** :
- Seuil "fichier lourd"
- Seuil ligne anormale
- Taille de chunk recommandée
- Profondeur de nesting max
- Auto-backup avant fix : on/off
- Auto-apprentissage KB : on/off
- Trace verbose : on/off
- Profil : Generic / AURA8 / JS / Python / Markdown / JSON

## Export

- Audit JSON complet (fichiers + issues + KB + stats)
- Audit Markdown
- Issues seules (JSON)
- KB seule (JSON, importable)
- Backups (JSON, importable pour restore)

## Licence

MIT.
