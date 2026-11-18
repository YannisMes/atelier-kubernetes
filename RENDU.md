# Rendu — Atelier Kubernetes

> Complétez ce fichier au fil de l'atelier, puis faites un commit et un push (voir la section « Rendu » du README).

**Nom / Prénom :**
**Groupe :**

---

## Exercice 1 — Cluster

1. Combien de nœuds affiche `kubectl get nodes` ? Quel est le rôle de chacun ?
   la commande affiche 3 noeuds:
    k3d-lab-server-0 joue le rôle de control-place : il héberge l'API serverle scheduler, le controller-manager et etcd, et décide où placer les pods.
    k3d-lab-agent-0  et k3d-lab-agent-1 sont  les workers . Leur colonne ROLES affiche <none>, car k3s n’étiquette pas les workers, mais ils exécutent les pods applicatifs.
   
2. Que montre `docker ps` ? Qu'est-ce qu'un « nœud » dans k3d, concrètement ?
   >docker ps nous montre 4 conteneurs. Dans k3d, un nœud Kubernetes est un conteneur Docker qui fait tourner k3s.

## Exercice 2 — Premier déploiement

3. Quels objets Kubernetes ont été créés par `kubectl create deployment` ? (indice : `kubectl get all`)
   >La commande crée un Deployment nommé web. Celui-ci crée à son tour un ReplicaSet, qui crée un Pod avec nginx dedans. Je n’ai donc pas créé le pod moi-même : c’est le Deployment qui s’en occupe par l’intermédiaire du ReplicaSet. Ensuite, kubectl expose a créé un Service pour pouvoir accéder au pod.
4. Vous avez supprimé le pod `web-...` : que s'est-il passé, et pourquoi ?
   >Quand j’ai supprimé le pod, un nouveau pod avec un nom différent s’est recréé tout de suite et est repassé en Running en quelques secondes. C’est parce que le Deployment est configuré pour avoir 1 pod en permanence. Le ReplicaSet voit qu’il n’y en a plus et en recrée un automatiquement. Kubernetes compare en continu ce qu’on lui a demandé (1 pod) avec ce qui existe vraiment et  corrige l’écart tout seul.

## Exercice 3 — Modifier un conteneur en direct

5. Après suppression du pod, votre message « Bienvenue... » a-t-il survécu ? Pourquoi ?
   >
6. Pourquoi le `port-forward` a-t-il cessé de fonctionner après la suppression du pod ?
   >

## Exercice 4 — Déclaratif

7. Quelle différence entre `kubectl create` et `kubectl apply` ?
   >
8. À quoi sert le `selector` d'un Service ? Que se passe-t-il s'il ne correspond à aucun pod ?
   >

## Exercice 5 — Scaling & mises à jour

9. Sur quels nœuds se trouvent vos 3 réplicas ? Collez la sortie de `kubectl get pods -l app=site -o wide`.
   ```

   ```
10. Avec l'image `nginx:9.99`, quel statut avait le pod ? Quelle commande vous a donné la cause ?
    >
11. Pendant la panne, le site restait-il accessible ? Pourquoi ?
    >

## Exercice 6 — Portainer & Mario

12. URL publique de votre Mario :
    >
13. Retrouvez le Deployment `mario` en ligne de commande. Portainer et `kubectl` parlent-ils au même composant ? Lequel ?
    >

## Bonus (facultatif)

14. Bonus réalisés et remarques :
    >

---

**Score obtenu avec `./scripts/check.sh` :** ... / ...
