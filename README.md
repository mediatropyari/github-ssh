#!/bin/bash

# Step 1: Generate SSH Key Pair (if not already done)
# Replace "your_email@example.com" with your GitHub email
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/.ssh/id_rsa_github

# Step 2: Check SSH Agent
eval "$(ssh-agent -s)"

# Step 3: Add Your Private Key to the SSH Agent
ssh-add ~/.ssh/id_rsa_github

# Step 4: Verify SSH Connection
ssh -T git@github.com

# Step 5: Clone with SSH (Optional)
# Replace "username" with your GitHub username and "repo" with the repository name
git clone git@github.com:username/repo.git

# Step 6: Automate SSH Agent Setup on Login
# Add the following lines to your .bashrc file
# Start the SSH agent if it's not running
if ! pgrep -q ssh-agent; then
    eval "$(ssh-agent -s)"
fi

# Add your SSH key to the agent (adjust the path if needed)
ssh-add ~/.ssh/id_rsa_github

# Step 7: Apply Changes
# To apply the changes without logging out and back in
source ~/.bashrc

# Step 8: Add Public Key to GitHub Account
# Copy the contents of your public key to the clipboard
# Use the following command to print your public key
cat ~/.ssh/id_rsa_github.pub
# Then, go to your GitHub account settings > SSH and GPG keys > New SSH key
# Paste the copied public key into the "Key" field and save it
