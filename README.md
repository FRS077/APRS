# APRS

rpi-rw
cd /tmp
sudo wget http://sp2ong.noip.pl/downloads/aprshotspot.tgz
sudo tar xvzfP aprshotspot.tgz

Les scripts d'envoi de données à aprs.fi seront placés dans / etc / aprs /. Le script d'exécution principal est un fichier nommé ' aprshotspot ', le second fichier est utilisé pour envoyer des données et convertir les coordonnées au format utilisé dans aprs.fi

Le contenu des informations telles qu'elles apparaissent peut être ajusté individuellement, il suffit de modifier le fichier aprshotspot :

sudo nano /etc/aprs/aprshotspot

et entrez votre propre contenu d'information sur APRS au lieu de l'exemple:

$description="Pi-Star Hotspot DMR ";

Le numéro SSID dans notre connexion sur APRS est 10 par défaut, mais au lieu de 10, nous pouvons entrer de 1 à 15. Comment déterminer le SSID pour APRS autre que 10 peut être trouvé ici: http://www.aprs.pl/stacja.htm Modifier la valeur SSID dans le fichier en faisant des éditions:

sudo nano /etc/aprs/aprshotspot

et recherchez la définition du SSID:

$ssid="10";

Si nous voulons que les informations sur APRS incluent des informations sur les groupes Romance sur BM que nous sommes disponibles sur notre hotspot, nous pouvons activer les options Remarque clé de génération d'API requise: http://wiki.pistar.uk/PI-Star_integration_with_BrandMeister_API

$tglist="1";

Enregistrez le fichier en utilisant la combinaison de touches : CTRL + X puis la touche " Y "

Nous pouvons exécuter manuellement le script en écrivant la commande:

sudo /etc/aprs/aprshotspot

Nous pouvons vérifier sur la carte http://aprs.fi si nos données sont apparues.

Nous pouvons maintenant ajouter l'exécution cyclique de notre script avec la commande:

cd /etc
sudo nano crontab

et ajoutez les lignes à la fin du fichier:

 */20 * * * *   root    /etc/aprs/aprshotspot > /dev/null 2>&1 &

et entrez-le comme dans l'image ci-dessous dans le cadre rouge (au lieu de 20 minutes, nous pouvons changer le nombre de fois que notre rapport doit être envoyé):

enregistrer le fichier en utilisant la combinaison de touches : CTRL + X puis la touche " Y "

Nous redémarrons le site crontab avec la commande:

sudo /etc/init.d/cron restart

et après 20 minutes, nous avons les positions de notre hotspot sur la carte aprs.fi.
