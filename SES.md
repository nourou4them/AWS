## Envoi de mails via AWS

Simple Email Service => Enregistrement de domaines et d'adresses mails

                        Statistiques d'envois de mails
                        Paramètres serveur SMTP
                        Gestion des templates 
                        Gestion des notifications (accusé de réception, ouverture du mail, echec d'envoi...)

Amazon Ligne de commande (awscli)

                        Gestion des clés d'accès
                        Création des templates
                        Gestion de la base de données 

## Template
### 1er fichier json

    Création de la template
    Nom + sujet + contenu du mail (html + texte)
    Insertion de tags
                        
### 2e fichier json

    Expéditeur 
    Destinataire : un ou multiples
    Config set (règles et canaux de notification)

    Plus : itération de tags, insertion de liens




1 - Créer une "topic" [une rubrique] => https://us-west-2.console.aws.amazon.com/sns/v2/home?region=us-west-2#/topics
        
        Créer une rubrique 
        Noter l'ARN
        Créer un abonnement pour recevoir les notifications d'échec d'envoi du mail

2 - Créer la config 

        Console => https://us-west-2.console.aws.amazon.com/ses/home?region=us-west-2#configuration-set-list: 
        Create Configuration set

3 - Créer le template 

        nano nom_du_template.json
        Mettre le nom du template, l'objet du mail, les tags (ou variables)
        aws ses create-template --cli-input-json file://nom_du_template.json

4 - Créer l'email personnalisé

        Renseigner le PreferencesSet et le nom du template
        Renseigner les données liées aux tags
        Renseigner l'adresse mail destinataire.

5 - Envoyer

        aws ses send-templated-email --cli-input-json file://myemail.json
