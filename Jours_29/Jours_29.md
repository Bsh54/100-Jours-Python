## Envoyer des e-mails et des SMS avec Python

Dans les chapitres précédents, nous avons vu comment générer automatiquement des documents Excel, Word et PDF avec des programmes Python. Nous pouvons aller plus loin en envoyant par e-mail les documents générés à des destinataires spécifiés, puis en informant les destinataires par SMS que nous avons envoyé l'e-mail. Ces tâches peuvent également être résolues facilement et agréablement avec des programmes Python.

### Envoyer des e-mails

Aujourd'hui, malgré la popularité des logiciels de messagerie instantanée, le courrier électronique reste l'une des applications les plus utilisées sur Internet. Les entreprises envoient des offres d'emploi aux candidats, les sites web envoient des liens d'activation de compte aux utilisateurs, les banques font la promotion de leurs produits financiers auprès des clients, etc., presque tous ces envois se font par e-mail, et ces tâches devraient être effectuées automatiquement par des programmes.

Nous pouvons utiliser HTTP (Hypertext Transfer Protocol) pour accéder aux ressources d'un site web. HTTP est un protocole de niveau application, construit sur TCP (Transmission Control Protocol). TCP fournit un service de transmission de données fiable pour de nombreux protocoles de niveau application. Pour envoyer des e-mails, nous utilisons SMTP (Simple Mail Transfer Protocol), qui est également un protocole de niveau application construit sur TCP, définissant les détails de communication entre l'expéditeur et le serveur de messagerie. Python simplifie ces opérations via le module `smtplib` avec l'objet `SMTP_SSL`. Les méthodes `login` et `send_mail` de cet objet permettent d'envoyer des e-mails.

Essayons d'abord d'envoyer un e-mail très simple, sans pièces jointes, images ou autres contenus hypertexte. Pour envoyer un e-mail, il faut d'abord se connecter à un serveur de messagerie. Nous pouvons configurer notre propre serveur de messagerie, mais cela n'est pas facile pour les débutants. Nous pouvons plutôt utiliser un service de messagerie tiers. Par exemple, j'ai créé un compte sur <www.126.com>. Après connexion, je peux activer le service SMTP dans les paramètres, ce qui équivaut à obtenir un serveur de messagerie. Les étapes sont les suivantes.

Après avoir scanné le code QR ci-dessus avec votre téléphone, vous pouvez obtenir un code d'autorisation en envoyant un SMS. Une fois le SMS envoyé, cliquez sur "J'ai envoyé" pour obtenir le code d'autorisation. Ce code doit être conservé en sécurité, car s'il est divulgué, d'autres personnes pourraient utiliser votre identité pour envoyer des e-mails. Ensuite, nous pouvons écrire le code pour envoyer un e-mail, comme indiqué ci-dessous.

```python
import smtplib
from email.header import Header
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText

# Créer l'objet principal de l'e-mail
email = MIMEMultipart()
# Définir l'expéditeur, le(s) destinataire(s) et l'objet
email['From'] = 'xxxxxxxxx@126.com'
email['To'] = 'yyyyyy@qq.com;zzzzzz@1000phone.com'
email['Subject'] = Header('Rapport sur le travail du premier semestre', 'utf-8')
# Ajouter le contenu du corps de l'e-mail
content = """Selon les médias allemands, le syndicat des conducteurs de train allemand a voté le 9,
et une grève nationale est prévue à partir du 10. La grève du fret a commencé le 10 à 19h00.
Ensuite, de 2h00 le 11 à 2h00 le 13, une grève de 48 heures aura lieu pour le transport de passagers et les infrastructures ferroviaires à l'échelle nationale."""
email.attach(MIMEText(content, 'plain', 'utf-8'))

# Créer l'objet SMTP_SSL (connexion au serveur de messagerie)
smtp_obj = smtplib.SMTP_SSL('smtp.126.com', 465)
# Se connecter avec le nom d'utilisateur et le code d'autorisation
smtp_obj.login('xxxxxxxxx@126.com', 'code d autorisation du serveur de messagerie')
# Envoyer l'e-mail (expéditeur, destinataire(s), contenu de l'e-mail (chaîne))
smtp_obj.sendmail(
    'xxxxxxxxx@126.com',
    ['yyyyyy@qq.com', 'zzzzzz@1000phone.com'],
    email.as_string()
)
```

Pour envoyer un e-mail avec des pièces jointes, il suffit de traiter le contenu de la pièce jointe en encodage BASE64, ce qui le rend presque identique à un texte ordinaire. BASE64 est une méthode de représentation des données binaires basée sur 64 caractères imprimables. Elle est couramment utilisée dans les situations où des données binaires doivent être représentées, transmises ou stockées, y compris dans les e-mails. Pour ceux qui ne comprennent pas ce codage, je recommande de lire l'article [《Notes sur Base64》](http://www.ruanyifeng.com/blog/2008/06/base64.html). Comme mentionné précédemment, le module `base64` de la bibliothèque standard de Python prend en charge l'encodage et le décodage BASE64.

Le code ci-dessous montre comment envoyer un e-mail avec une pièce jointe.

```python
import smtplib
from email.header import Header
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from urllib.parse import quote

# Créer l'objet principal de l'e-mail
email = MIMEMultipart()
# Définir l'expéditeur, le(s) destinataire(s) et l'objet
email['From'] = 'xxxxxxxxx@126.com'
email['To'] = 'zzzzzzzz@1000phone.com'
email['Subject'] = Header('Veuillez trouver ci-joint le certificat de départ', 'utf-8')
# Ajouter le contenu du corps de l'e-mail (contenu formaté avec des balises HTML)
content = """<p>Cher ancien collègue,</p>
<p>Le certificat de départ dont vous avez besoin est en pièce jointe, veuillez le trouver ci-joint !</p>
<br>
<p>Cordialement,</p>
<hr>
<p>Sun Meili, aujourd'hui</p>"""
email.attach(MIMEText(content, 'html', 'utf-8'))
# Lire le fichier à joindre
with open(f'resources/Certificat_de_depart_de_Wang_Dachui.docx', 'rb') as file:
    attachment = MIMEText(file.read(), 'base64', 'utf-8')
    # Spécifier le type de contenu
    attachment['content-type'] = 'application/octet-stream'
    # Traiter le nom de fichier chinois en codage pour cent
    filename = quote('Certificat de départ de Wang Dachui.docx')
    # Spécifier comment traiter le contenu
    attachment['content-disposition'] = f'attachment; filename="{filename}"'

# Créer l'objet SMTP_SSL (connexion au serveur de messagerie)
smtp_obj = smtplib.SMTP_SSL('smtp.126.com', 465)
# Se connecter avec le nom d'utilisateur et le code d'autorisation
smtp_obj.login('xxxxxxxxx@126.com', 'code d autorisation du serveur de messagerie')
# Envoyer l'e-mail (expéditeur, destinataire, contenu de l'e-mail (chaîne))
smtp_obj.sendmail(
    'xxxxxxxxx@126.com',
    'zzzzzzzz@1000phone.com',
    email.as_string()
)
```

Pour faciliter l'envoi d'e-mails avec Python, j'ai encapsulé le code ci-dessus dans une fonction. Pour l'utiliser, il suffit d'ajuster le domaine du serveur de messagerie, le port, le nom d'utilisateur et le code d'autorisation.

```python
import smtplib
from email.header import Header
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from urllib.parse import quote

# Domaine du serveur de messagerie (modifier)
EMAIL_HOST = 'smtp.126.com'
# Port du service de messagerie (généralement 465)
EMAIL_PORT = 465
# Compte pour se connecter au serveur de messagerie (modifier)
EMAIL_USER = 'xxxxxxxxx@126.com'
# Code d'autorisation pour activer le service SMTP (modifier)
EMAIL_AUTH = 'code d autorisation du serveur de messagerie'


def send_email(*, from_user, to_users, subject='', content='', filenames=[]):
    """Envoyer un e-mail
    
    :param from_user: expéditeur
    :param to_users: destinataire(s), séparés par des points-virgules pour plusieurs destinataires
    :param subject: objet de l'e-mail
    :param content: contenu du corps de l'e-mail
    :param filenames: chemins des fichiers à joindre
    """
    email = MIMEMultipart()
    email['From'] = from_user
    email['To'] = to_users
    email['Subject'] = subject

    message = MIMEText(content, 'plain', 'utf-8')
    email.attach(message)
    for filename in filenames:
        with open(filename, 'rb') as file:
            pos = filename.rfind('/')
            display_filename = filename[pos + 1:] if pos >= 0 else filename
            display_filename = quote(display_filename)
            attachment = MIMEText(file.read(), 'base64', 'utf-8')
            attachment['content-type'] = 'application/octet-stream'
            attachment['content-disposition'] = f'attachment; filename="{display_filename}"'
            email.attach(attachment)

    smtp = smtplib.SMTP_SSL(EMAIL_HOST, EMAIL_PORT)
    smtp.login(EMAIL_USER, EMAIL_AUTH)
    smtp.sendmail(from_user, to_users.split(';'), email.as_string())
```

### Envoyer des SMS

L'envoi de SMS est également une fonctionnalité courante dans les projets. Les codes d'inscription, les codes de vérification et les informations marketing des sites web sont généralement envoyés aux utilisateurs par SMS. L'envoi de SMS nécessite le support de plateformes tierces. Prenons l'exemple de la [plateforme Luosimao](https://luosimao.com/) pour montrer comment envoyer des SMS avec un programme Python. Nous ne détaillerons pas ici l'inscription et l'achat de services SMS ; vous pouvez consulter le service client de la plateforme.

Ensuite, nous pouvons utiliser la bibliothèque `requests` pour envoyer une requête HTTP à la passerelle SMS fournie par la plateforme. En fournissant le numéro de téléphone du destinataire et le contenu du SMS comme paramètres, nous pouvons envoyer le SMS. Voici le code correspondant.

```python
import random

import requests


def send_message_by_luosimao(tel, message):
    """Envoyer un SMS (en appelant la passerelle SMS de Luosimao)"""
    resp = requests.post(
        url='http://sms-api.luosimao.com/v1/send.json',
        auth=('api', 'clé allouée par la plateforme après inscription'),
        data={
            'mobile': tel,
            'message': message
        },
        timeout=10,
        verify=False
    )
    return resp.json()


def gen_mobile_code(length=6):
    """Générer un code de vérification de téléphone de longueur spécifiée"""
    return ''.join(random.choices('0123456789', k=length))


def main():
    code = gen_mobile_code()
    message = f'Votre code de vérification SMS est {code}, ne le divulguez à personne ! 【Cours Python】'
    print(send_message_by_luosimao('13500112233', message))


if __name__ == '__main__':
    main()
```

La requête ci-dessus à la passerelle SMS de Luosimao `http://sms-api.luosimao.com/v1/send.json` renverra des données au format JSON. Si elle renvoie `{'error': 0, 'msg': 'OK'}`, cela signifie que le SMS a été envoyé avec succès. Si la valeur d'`error` n'est pas `0`, consultez la [documentation de développement officielle](https://luosimao.com/docs/api/) pour comprendre quel est le problème. Les types d'erreurs courants sur la plateforme Luosimao sont illustrés ci-dessous.

Actuellement, la plupart des plateformes SMS exigent que le contenu du SMS inclue une signature. La capture d'écran ci-dessous montre la signature SMS "【Cours Python】" que j'ai configurée sur la plateforme Luosimao. Certains SMS contenant des informations sensibles nécessitent également une configuration préalable de modèles SMS. Les lecteurs intéressés peuvent étudier cela par eux-mêmes. Généralement, pour prévenir l'utilisation frauduleuse des SMS, les plateformes exigent également la configuration d'une "liste blanche d'IP". Si vous ne savez pas comment configurer cela, consultez le service client de la plateforme.

Bien sûr, il existe de nombreuses plateformes SMS en France. Les lecteurs peuvent choisir en fonction de leurs besoins (généralement en considérant le budget, le taux de livraison des SMS, la facilité d'utilisation, etc.). Pour utiliser des services SMS dans des projets commerciaux, il est recommandé d'acheter des forfaits auprès des plateformes SMS.

### Résumé

En fait, l'envoi d'e-mails, comme l'envoi de SMS, peut également être effectué en faisant appel à des services tiers. Dans les projets commerciaux réels, il est recommandé de configurer son propre serveur de messagerie ou d'acheter des services tiers pour envoyer des e-mails, c'est l'option la plus fiable.