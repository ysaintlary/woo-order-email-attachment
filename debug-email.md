# Debug : e-mail « Commande terminée » non envoyé

## Symptôme

Après le renommage du plugin (v1.5.0), l'e-mail « Commande terminée » de WooCommerce ne part plus.

## Diagnostic à faire

1. **Identifier le périmètre** : l'e-mail ne part pas du tout, ou il part sans la pièce jointe XLSX ?
2. **Tester sans le plugin** : désactiver « YS | Woo Order Email Attachment » et relancer l'e-mail. S'il part, c'est le plugin qui bloque.
3. **Vérifier les logs PHP** du serveur : chercher une erreur liée à `WOCEA` ou `XLSXWriter`.
4. **WP Mail SMTP** : les autres e-mails WooCommerce fonctionnent-ils (nouvelle commande, etc.) ?
5. **Vérifier les permissions** : le dossier `wp-content/uploads/woo-order-email-attachment/` doit être accessible en écriture par PHP.

## Pistes

- Le renommage a changé le répertoire d'upload de `sls-csv-order-attachment` à `woo-order-email-attachment` — vérifier que le nouveau dossier se crée correctement.
- WP Mail SMTP avec envoi optimisé copie les pièces jointes avant le traitement en file d'attente — si le fichier XLSX n'existe pas au moment de la copie, l'envoi peut échouer.
