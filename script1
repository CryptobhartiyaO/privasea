# Infinite loop to keep retrying the script if any part fails
while true; do
    printf "\n"
    cat <<EOF
                             __           __       __                       __                            
                            /\ \__       /\ \     /\ \                     /\ \__  __                     
  ___   _ __   __  __  _____\ \ ,_\   ___\ \ \____\ \ \___      __     _ __\ \ ,_\/\_\  __  __     __     
 /'___\/\`'__\/\ \/\ \/\ '__`\ \ \/  / __`\ \ '__`\\ \  _ `\  /'__`\  /\`'__\ \ \/\/\ \/\ \/\ \  /'__`\   
/\ \__/\ \ \/ \ \ \_\ \ \ \L\ \ \ \_/\ \L\ \ \ \L\ \\ \ \ \ \/\ \L\.\_\ \ \/ \ \ \_\ \ \ \ \_\ \/\ \L\.\_ 
\ \____\\ \_\  \/`____ \ \ ,__/\ \__\ \____/\ \_,__/ \ \_\ \_\ \__/.\_\\ \_\  \ \__\\ \_\/`____ \ \__/.\_\
 \/____/ \/_/   `/___/> \ \ \/  \/__/\/___/  \/___/   \/_/\/_/\/__/\/_/ \/_/   \/__/ \/_/`/___/> \/__/\/_/
                   /\___/\ \_\                                                              /\___/        
                   \/__/  \/_/                                                              \/__/        
EOF

    printf "\n\n"

##########################################################################################
    #                                                                                        
    #                🚀 THIS SCRIPT IS PROUDLY CREATED BY **CRYPTOBHARTIYA**! 🚀                  
    #                                                                                        
    #   🌐 Join our revolution in decentralized networks and crypto innovation!               
    #                                                                                        
    # 📢 Stay updated:                                                                      
    #     • Follow us on Telegram: https://t.me/cryptobhartiya                         
    #     • Follow us on X: https://x.com/cryptobhartiyaO                                         
    ##########################################################################################

    # Green color for advertisement
    GREEN="\033[0;32m"
    RESET="\033[0m"

    # Print the advertisement using printf
    printf "${GREEN}"
    printf "🚀 THIS SCRIPT IS PROUDLY CREATED BY **CRYPTOBHARTIYA**! 🚀\n"
    printf "Join the movement & shape the next era of decentralization:\n"
    printf "   • Telegram: https://t.me/cryptobhartiya\n"
    printf "   • X (formerly Twitter): https://x.com/GACryptoO\n"
    printf "${RESET}"



 # Privanetix Node Setup Script

    # Update and install necessary dependencies
    echo "🔄 Updating package list and installing dependencies..."
    sudo apt update && sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
    if [ $? -ne 0 ]; then
        echo "❌ Error: Package installation failed. Retrying..."
        continue
    fi

    # Add Docker's official GPG key using gpg and store it in the trusted keyring directory
echo "🔑 Adding Docker's GPG key..."
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/trusted.gpg.d/docker-archive.gpg
if [ $? -ne 0 ]; then
    echo "❌ Error: Adding Docker GPG key failed. Retrying..."
    continue
fi

    # Add Docker's official repository
    echo "📦 Adding Docker repository..."
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    if [ $? -ne 0 ]; then
        echo "❌ Error: Adding Docker repository failed. Retrying..."
        continue
    fi

    # Update package list again
    echo "🔄 Updating package list..."
    sudo apt update
    if [ $? -ne 0 ]; then
        echo "❌ Error: Package list update failed. Retrying..."
        continue
    fi

    # Install Docker
    echo "🐳 Installing Docker..."
    sudo apt install -y docker-ce
    if [ $? -ne 0 ]; then
        echo "❌ Error: Docker installation failed. Retrying..."
        continue
    fi

    # Start and enable Docker service
    echo "🚀 Starting and enabling Docker service..."
    sudo systemctl start docker
    sudo systemctl enable docker
    if [ $? -ne 0 ]; then
        echo "❌ Error: Starting Docker service failed. Retrying..."
        continue
    fi

    # Function to restart Docker and retry pulling the image until it works
    pull_docker_image() {
        while true; do
            # Try pulling the Docker image
            echo "📥 Pulling Privanetix Node Docker image..."
            sudo docker pull privasea/acceleration-node-beta
            if [ $? -eq 0 ]; then
                echo "✅ Docker image pulled successfully."
                break # Exit the loop if the image is pulled successfully
            else
                echo "❌ Error: Pulling Docker image failed. Retrying..."
                # Restart Docker service and try again if pulling fails
                sudo systemctl daemon-reload
                sudo systemctl restart docker
                if [ $? -ne 0 ]; then
                    echo "❌ Error: Restarting Docker service failed. Retrying..."
                    continue
                fi
                echo "🔄 Retrying Docker image pull..."
            fi
        done
    }

    # Pull Docker image (retry until success)
    pull_docker_image || continue

    # Create the program running directory
    echo "📂 Creating program directory..."
    sudo mkdir -p /privasea/config
    sudo chown -R $USER:$USER /privasea
    cd /privasea
    if [ $? -ne 0 ]; then
        echo "❌ Error: Creating program directory failed. Retrying..."
        continue
    fi

    # Generate a new keystore
    echo "🔐 Generating new keystore..."
    sudo docker run -it -v "/privasea/config:/app/config" privasea/acceleration-node-beta:latest ./node-calc new_keystore
    if [ $? -ne 0 ]; then
        echo "❌ Error: Keystore generation failed. Retrying..."
        continue
    fi

    # Rename the keystore file in the /privasea/config folder to wallet_keystore
    echo "📝 Checking for a keystore file starting with 'UTC--' to rename it to 'wallet_keystore'..."

    # Navigate to the configuration directory
    cd /privasea/config

    # Find the file that starts with "UTC--" (handles unique file names)
    keystore_file=$(ls | grep "^UTC--")

    if [ -z "$keystore_file" ]; then
        echo "❌ Error: No keystore file found in /privasea/config. Retrying..."
        continue
    fi

    # Rename the keystore file to wallet_keystore
    echo "🔄 Renaming '$keystore_file' to 'wallet_keystore'..."
    mv "$keystore_file" "wallet_keystore"

    # Verify the rename was successful
    if [ -f "wallet_keystore" ]; then
        echo "✅ The keystore file has been successfully renamed to 'wallet_keystore'."
    else
        echo "❌ Error: Failed to rename the keystore file. Retrying..."
        continue
    fi

    echo "✅ Setup completed successfully!"
    echo "Please note down your node address and keystore password for future reference."
    break # Exit the loop if everything is successful
done
