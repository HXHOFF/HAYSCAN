### SCAN HAY : SERVEUR DISCORDhttps://discord.gg/wJVYgwZu                               
Pour effectuer des opérations de cybersécurité sous Kali Linux ou Termux, voici des commandes et scripts adaptés à ces environnements. Nous allons couvrir deux aspects : scanner les réseaux Wi-Fi à proximité et héberger une page de phishing.

### Scanner les Réseaux Wi-Fi à Proximité

Sous Kali Linux ou Termux, on peut utiliser `airodump-ng` pour scanner les réseaux Wi-Fi. Voici un script Bash pour automatiser ce processus :

#### Script Bash pour Scanner les Réseaux Wi-Fi

1. **Installation de `aircrack-ng` (si nécessaire)** :
    ```sh
    sudo apt-get update
    sudo apt-get install aircrack-ng
    ```

2. **Script Bash** :
    ```sh
    #!/bin/bash

    # Mettre l'interface en mode moniteur
    INTERFACE="wlan0"
    sudo ip link set $INTERFACE down
    sudo iw dev $INTERFACE set type monitor
    sudo ip link set $INTERFACE up

    # Lancer le scan avec airodump-ng
    sudo airodump-ng $INTERFACE

    # Remettre l'interface en mode gestion
    sudo ip link set $INTERFACE down
    sudo iw dev $INTERFACE set type managed
    sudo ip link set $INTERFACE up
    ```

Sauvegarde ce script sous le nom `wifi_scan.sh`, rends-le exécutable, puis exécute-le :
```sh
chmod +x wifi_scan.sh
sudo ./wifi_scan.sh
```

### Héberger une Page de Phishing

Pour héberger une page de phishing, tu peux utiliser un serveur web Python. Voici comment le faire sous Kali Linux ou Termux :

#### Script Python pour Héberger une Page de Phishing

1. **Préparation du répertoire de la page de phishing** :
    Crée un répertoire nommé `phishing_site` et place-y ta page HTML.

2. **Script Python** :
    ```python
    import http.server
    import socketserver

    PORT = 8080
    DIRECTORY = "phishing_site"

    class Handler(http.server.SimpleHTTPRequestHandler):
        def __init__(self, *args, **kwargs):
            super().__init__(*args, directory=DIRECTORY, **kwargs)

    def run_server():
        with socketserver.TCPServer(("", PORT), Handler) as httpd:
            print(f"Serving phishing site at port {PORT}")
            httpd.serve_forever()

    if __name__ == "__main__":
        run_server()
    ```

Sauvegarde ce script sous le nom `phishing_server.py`, puis exécute-le :
```sh
python3 phishing_server.py
```

Accède ensuite à l'adresse `http://localhost:8080` pour voir la page hébergée.

### Notes de Sécurité

- **Scanner les Réseaux Wi-Fi** : Assure-toi d'avoir l'autorisation de scanner les réseaux Wi-Fi. Scanner les réseaux sans autorisation peut être illégal.
- **Hébergement de Pages de Phishing** : Utilise cette technique uniquement pour des tests de cybersécurité éthiques avec l'autorisation appropriée. L'utilisation de pages de phishing sans consentement est illégale et contraire à l'éthique.

En respectant les lois et les politiques de cybersécurité, ces outils peuvent t'aider à évaluer et à renforcer la sécurité de tes réseaux et systèmes. 
