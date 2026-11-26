# Lösning

## Nyckelkommandon

```bash
git log --oneline
git reset --hard <commit-id>
git status
git log --oneline
git push --force-with-lease
```

## Så gör du

Börja med att undersöka historiken:

```bash
git log --oneline
```

Du ska hitta den felaktiga committen och sedan identifiera committen som ligger precis före den.

Exempel:

```text
effb3f8 Add incorrect version for Case 04
8857b45 Update case 04 problem and solution
```

Här är `effb3f8` den felaktiga versionen.

Versionen innan felet är:

```text
8857b45
```

Återställ branchen till den tidigare versionen:

```bash
git reset --hard 8857b45
```

Kontrollera sedan:

```bash
git status
git log --oneline
```

Den felaktiga committen ska inte längre ligga överst i din lokala branch.

Eftersom branchen på GitHub fortfarande innehåller den felaktiga committen behöver historiken uppdateras med:

```bash
git push --force-with-lease
```

## Därför händer det

Git sparar projektets historik i commits.

När en felaktig commit redan finns i branchen kan du gå tillbaka till en tidigare commit med `git reset --hard`.

Det flyttar branchen tillbaka till den valda committen och återställer filerna till hur de såg ut då.

Eftersom GitHub fortfarande har den nyare historiken krävs en force-push för att uppdatera remote-branchen.

`--force-with-lease` är säkrare än vanlig `--force` eftersom Git kontrollerar att remote-branchen inte har ändrats av någon annan sedan du senast hämtade den.

## Tips

- Använd `git log --oneline` för att hitta rätt commit.
- Kontrollera commit-id noggrant innan du kör `git reset --hard`.
- I det här caset ska du gå tillbaka till committen precis innan den felaktiga versionen.
- `git reset --hard` tar bort senare lokala ändringar, så använd kommandot med försiktighet.
- Kontrollera med `git status` och `git log --oneline` innan du pushar.
- Använd `git push --force-with-lease` i stället för vanlig `git push` eftersom branch-historiken har ändrats.