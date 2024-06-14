#Programmed by Garrett Strahan
#This will create users in Juniper MIST

import requests
import json

# Set your Mist API token and site ID
token = "YOUR_API_TOKEN"
site_id = "YOUR_SITE_ID"

# Mist API endpoints
base_url = "https://api.mist.com/api/v1"
user_endpoint = f"{base_url}/orgs/me/sites/{site_id}/users"

# Function to create a user
def create_user(email, role):
    headers = {
        "Authorization": f"Token {token}",
        "Content-Type": "application/json"
    }
    data = {
        "email": email,
        "role": role  # Role can be 'admin', 'engineer', or 'read_only'
    }
    response = requests.post(user_endpoint, headers=headers, data=json.dumps(data))
    
    if response.status_code == 200:
        print("User created successfully.")
    else:
        print(f"Error creating user: {response.text}")

# Example usage
if __name__ == "__main__":
    email = input("Enter email address of the user: ")
    role = input("Enter role of the user (admin/engineer/read_only): ")
    create_user(email, role)