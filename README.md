# 🛠️ Oracle Cloud Out of Capacity Script

A robust Python automation tool designed to monitor Oracle Cloud Infrastructure (OCI) for instance availability and automatically provision "Always Free" instances (AMD & Ampere) when capacity becomes available.

![License](https://img.shields.io/github/license/praveenkarunarathne/Oracle_Cloud_Out_Of_Capacity_Script)
![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Docker](https://img.shields.io/badge/Docker-Supported-blue)

## ✨ Features

*   **Automatic Provisioning**: Continuously checks for instance availability and attempts to launch.
*   **Multi-Architecture**: Supports both AMD (VM.Standard.E2.1.Micro) and Ampere (VM.Standard.A1.Flex) shapes.
*   **Telegram Integration**: Real-time status updates and success notifications sent directly to your Telegram.
*   **Smart Retries**: Implements intelligent retry logic with backoff to handle rate limiting (429 errors).
*   **Docker Support**: Easily deployable via Docker for containerized execution.
*   **Resource Management**: Checks for existing resources to avoid exceeding free-tier limits.

## 🚀 Getting Started

### Prerequisites

*   **Oracle Cloud Account**: You need an active OCI account.
*   **OCI Configuration**: API Key and Configuration file.
*   **Telegram Bot**: Token and Chat ID (UID) for notifications.
    *   Use [**@BotFather**](https://t.me/BotFather) to create your bot.
    *   (Optional) Use [**@MissRose_bot**](https://t.me/MissRose_bot) for group management or automation tasks.
*   **Python 3.8+** or **Docker**.

### 🌐 Creating VCN and Subnet (Optional)

*   **Destination CIDR Block**: `0.0.0.0/0`

### 📥 One-Click Download (Linux/Mac)

You can use the provided script to quickly download the necessary files and choose your version.

```bash
bash <(curl -s https://raw.githubusercontent.com/praveenkarunarathne/Oracle_Cloud_Out_Of_Capacity_Script/refs/heads/main/download_script.sh)
```

## ⚙️ Configuration

1.  **OCI Config**:
    Place your OCI configuration file content into the `config` file in the project root (or ensure access to `~/.oci/config`).
    See [Oracle Documentation](https://docs.oracle.com/en-us/iaas/Content/API/Concepts/apisigningkey.htm) for details on how to generate this.

2.  **Environment Variables**:
    Edit the `.env` file with your details. Key parameters include:

    ```env
    # OCI Details
    AVAILABILITY_DOMAINS=your_ad_1,your_ad_2
    DISPLAY_NAME=OCI-Instance-01
    COMPARTMENT_ID=ocid1.compartment.oc1..xxxx
    SUBNET_ID=ocid1.subnet.oc1.phx.xxxx
    SSH_AUTHORIZED_KEYS=ssh-rsa AAAAB3Nza...

    # Source Image Image (Find in OCI Console)
    IMAGE_ID=ocid1.image.oc1.phx.xxxx
    # OR Boot Volume
    BOOT_VOLUME_ID=xxxx

    # Telegram (Get from @BotFather)
    BOT_TOKEN=123456789:ABCdefGHIjklMNOpqrsTUVwxyz
    UID=123456789

    # Instance Resources
    OCPUS=4
    MEMORY_IN_GBS=24
    ```

    *   **Note**: For AMD instances, set `OCPUS=1` and `MEMORY_IN_GBS=1`. For Ampere, max free tier is `OCPUS=4` and `MEMORY_IN_GBS=24`.

## 🐳 Running with Docker

The easiest way to run the script is using Docker.

```bash
docker run --name oci-script \
  -d \
  -v $(pwd):/app \
  --restart unless-stopped \
  --log-opt max-size=10k --log-opt max-file=1 \
  praveenkarunarathne/oci-out-of-capacity-script
```

**View Logs:**

```bash
docker logs -f oci-script
```

## 🐍 Running with Python

1.  **Install Dependencies**:

    ```bash
    pip install -r requirements.txt
    ```

2.  **Run the Script**:

    *   For **AMD** (VM.Standard.E2.1.Micro):
        ```bash
        python "Amd 1 ram 1 cpu/bot.py"
        ```
    *   For **Ampere** (VM.Standard.A1.Flex):
        ```bash
        python "Ampere 24 ram 4 cpu/bot.py"
        ```

## 🌐 OCI Resources

*   **Operating System Images**: [Find Image OCIDs](https://docs.oracle.com/en-us/iaas/images/)
*   **Telegram Bot**: [Create via @BotFather](https://t.me/BotFather)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## ⚠️ Disclaimer

This script is for educational purposes only. Use it at your own risk. The author is not responsible for any costs or issues arising from the use of this script. Ensure you understand Oracle Cloud's terms of service regarding automation.
