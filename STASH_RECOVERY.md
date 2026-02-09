# Récupération d'un Git Stash Supprimé

## Situation

Vous avez demandé s'il y avait une trace d'un `git stash` qui a été supprimé. 

## Important : Les stashes sont locaux

**Les stashes Git sont stockés localement et ne sont pas transférés lors d'un clone du dépôt.**

Cela signifie que :
- Les stashes ne sont jamais poussés (push) vers un dépôt distant
- Un clone d'un dépôt ne contient pas les stashes de l'original
- Les stashes supprimés ne peuvent être récupérés que sur la machine où ils ont été créés

## Comment récupérer un stash supprimé

Si vous avez supprimé un stash et que vous travaillez sur la machine où il a été créé, vous pouvez le récupérer en utilisant le reflog :

### Étape 1 : Vérifier le reflog des stashes

```bash
git fsck --unreachable | grep commit
```

Cette commande liste tous les commits non-accessibles, y compris les stashes supprimés.

### Étape 2 : Examiner les commits trouvés

Pour chaque commit trouvé, vous pouvez examiner son contenu :

```bash
git show <hash-du-commit>
```

### Étape 3 : Récupérer le stash

Une fois que vous avez identifié le bon commit, vous pouvez le réappliquer :

```bash
# Option 1 : Appliquer les changements sans créer un nouveau stash
git stash apply <hash-du-commit>

# Option 2 : Créer un nouveau stash à partir du commit
git stash store -m "Message du stash récupéré" <hash-du-commit>

# Option 3 : Appliquer et supprimer (comme git stash pop)
git cherry-pick -n <hash-du-commit>
```

### Étape 4 : Utiliser le reflog du stash

Vous pouvez aussi vérifier directement le reflog du stash :

```bash
git log --graph --oneline --decorate $(git fsck --no-reflog | awk '/dangling commit/ {print $3}')
```

## Recherche dans ce dépôt

J'ai effectué une recherche dans le dépôt cloné actuel et n'ai trouvé **aucun commit non-accessible** ou trace de stash supprimé. Cependant, cela est attendu car :

1. Ce dépôt est un clone frais du dépôt distant
2. Les stashes ne sont jamais synchronisés avec le dépôt distant
3. Les stashes supprimés ne peuvent être trouvés que sur la machine locale où ils ont été créés

## Recommandations

Pour récupérer votre stash supprimé :

1. **Retournez sur la machine** où vous avez créé et supprimé le stash
2. **Exécutez les commandes** de récupération mentionnées ci-dessus
3. **Agissez rapidement** : les objets non-accessibles sont supprimés par le garbage collector de Git après environ 30 jours par défaut

## Prévention pour l'avenir

Pour éviter de perdre des stashes importants :

1. Créez une branche temporaire au lieu d'utiliser stash pour du travail important :
   ```bash
   git checkout -b temp/mon-travail-en-cours
   git add .
   git commit -m "WIP: Travail en cours"
   ```

2. Si vous devez utiliser stash, créez une branche de sauvegarde :
   ```bash
   git stash
   git stash branch backup-stash
   ```

3. Listez régulièrement vos stashes :
   ```bash
   git stash list
   ```

## Besoin d'aide ?

Si vous avez besoin d'aide pour récupérer votre stash sur votre machine locale, n'hésitez pas à demander !
