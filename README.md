# hng_stage_1_task
Script Overview
Here’s a detailed breakdown of the script:

Checking Input Argument: The script checks if the input file is provided as an argument.
if [ -z "$1" ]; then
    echo "Usage: $0 <name-of-text-file>"
    exit 1
fi

Initialization: It initializes log and password files and ensures the secure directory exists.
# Function to generate a random password
generate_password() {




    # using 'openssl rand -base64 12’ to generate a 12-character password
    openssl rand -base64 12
}

# Read input file line by line
while IFS=';' read -r username groups; do
    # Create groups if they don't exist
    for group in $(echo "$groups" | tr ',' ' '); do
      groupadd "$group" 2>/dev/null || echo "Group $group already exists"
    done

create user
useradd -m "$username" -G "$groups" 2>/dev/null || echo "User $username already exists"

command that sets passwords
password=$(generate_password)
echo "$username:$password" | chpasswd

Command that logs actions
echo "$(date '+%Y-%m-%d %H:%M:%S') - Created user $username with groups: $groups" >> "$log_file"

Command that stores password securely
echo "$username:$password" >> "$password_file"
done < "$input_file"

Conclusion
This script simplifies managing users and groups on a Linux system, ensuring security and efficiency. Automating these tasks not only saves time but also reduces the risk of human error.

For more information on the HNG internship program and to learn how to become a world-class developer, visit HNG Internship(https://hng.tech/internship) and [HNG Premium(https://hng.tech/premium).
