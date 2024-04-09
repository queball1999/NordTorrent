# NordTorrent 🚀
![aecbad10d71b7e716255d933554930cb-1726288407](https://github.com/queball1999/NordTorrent/assets/57122349/8b38a242-f2cc-478c-8dab-85087ea3d097)

Welcome to **NordTorrent**! A seamless solution for running qBittorrent securely behind a NordVPN layer, all set up with a minimal, user-friendly "one-click" configuration. NordTorrent harnesses the robust privacy features of NordVPN, funneling all qBittorrent traffic through a secure, encrypted VPN tunnel. This ensures that your torrenting activity remains private and your internet connection is secure from prying eyes. With NordTorrent, you get the best of both worlds: the vast capabilities of qBittorrent for managing your torrents, combined with the enhanced privacy and security offered by NordVPN. All of these are accessible through a convenient web management portal at `localhost:8089`.

## 📦 What's Inside?

NordTorrent offers a pre-configured Docker setup that packages qBittorrent with NordVPN, creating a secure torrenting environment right out of the box. This setup ensures that **every bit** of qBittorrent's traffic is routed exclusively through NordVPN's secure servers. Here’s why that’s important:

- **Privacy Protection**: With all traffic encrypted and routed through NordVPN, your torrenting activity is hidden from ISPs and potential eavesdroppers. NordVPN's no-logs policy means your activity remains yours alone.

- **Security Enhancement**: Leveraging NordVPN's world-class encryption and secure server network, NordTorrent protects your device from exposure to malicious entities often lurking in peer-to-peer networks.

- **Access Without Borders**: NordVPN’s global server network allows you to connect to peers across the world, potentially improving download speeds and bypassing geo-restrictions.

- **Simplicity and Accessibility**: Despite the sophisticated backend technology, accessing and managing your torrents is as simple as opening your web browser and navigating to `localhost:8089`.

Experience an unparalleled level of privacy and security in your torrenting activities with NordTorrent, all while maintaining the ease and flexibility of qBittorrent's powerful features.

## 🚀 Quick Start

1. **Clone the Repository:**
   First things first, we want to clone the repository.

    ```bash
    git clone https://github.com/queball1999/NordTorrent.git
    cd NordTorrent
    ```

2. **Get Your NordVPN Secret Key:**
   Next, you need to retrieve your NordVPN secret key. Replace `myemail@domain.com`, `mypassword`, and `mytoken` with your NordVPN credentials and token:

   ```bash
   docker run --rm --cap-add=NET_ADMIN -e USER=myemail@domain.com -e PASS=mypassword -e TOKEN=mytoken bubuntux/nordvpn:get_private_key
   ```
   In order to obtain a toke, please visit [How to obtain NordVPN Token](https://support.nordvpn.com/Connectivity/Linux/1905092252/How-to-log-in-to-NordVPN-on-Linux-with-a-token.htm#:~:text=Go%20to%20nordaccount.com%20and,Click%20on%20Generate%20new%20token).
   
3. **Edit the docker-compose.yaml File:**
   Open the docker-compose.yaml and add your NordVPN secret key:

    ```bash
    nano docker-compose.yaml
    ```

4. **Launch NordTorrent:**
   With your secret key in place, start your secure torrenting environment:

   ```bash
   docker-compose up -d
   ```
    Ensure you are running this command in the same directory as the docker-compose.yaml
  
6. **Access qBittorrent:**
   Open your web browser and go to localhost:8089 to start managing your torrents securely. The default credentials are ```admin \ adminadmin```

## 📖 Configuration
  ### Changing the Download Path in qBittorrent
  The download path for qBittorrent within the Docker container is determined by the volume mounts specified in your docker-compose.yaml file. By default, you might have something like this:

  ```yaml
  volumes:
    - "./downloads/QBitTorrent:/downloads"
  ```
  This line mounts the host directory ./downloads/QBitTorrent to the /downloads directory inside the container. To change the download location, you simply need to adjust the host path. 
  
  ### Here's a step-by-step guide:
  
  Identify the New Download Location: Determine where on your host machine you want qBittorrent to download files. For example, let's say you want to use /data/torrents/qbittorrent as the new location.

  ### Update the docker-compose.yaml File:
  Open your docker-compose.yaml file in a text editor:

  ```bash
  nano docker-compose.yaml
  ```
  Find the volumes section under the qBittorrent service and update the path before the colon (:) to your new desired download location, like so:

  ```yaml
  volumes:
    - "/data/torrents/qbittorrent:/downloads"
  ```
  Ensure that the path you specify exists on your host machine, or create it if necessary.

  ### Apply the Changes:
  After saving your changes to the docker-compose.yaml file, you'll need to recreate the qBittorrent container for the changes to take effect. Navigate to the directory containing your docker-compose.yaml file and run:

  ```bash
  docker-compose up -d
  ```
  This command recreates the qBittorrent container with the new volume mount, effectively changing the download path to the new location you specified.
  
  ### Verify in qBittorrent:
    Once the container is up and running, access the qBittorrent web UI at localhost:8089, and navigate to the settings. Under the Downloads section, you should see that the default save path reflects the path inside the container (/downloads),     which is now mapped to your new host directory.

## 🤝 Contributing
Contributions are welcome! Whether it's reporting issues, submitting improvements, or adding features, feel free to fork the repository and submit pull requests.

## 📝 License
This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments
Thanks to the creators of qBittorrent and the developers behind the NordVPN Docker integration for making this project possible.

## ⚠ Disclaimer
Disclaimer: This setup is intended for research and educational purposes only. The use of torrent services should comply with all applicable laws and regulations. It is not encouraged to use NordTorrent for illegal activities. Always ensure that your actions are legal and ethical.
